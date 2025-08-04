# Plugin API and Packaging

Voice Creator Studio (VCS) can be extended with plugins that add new speech engines or augment the core application. This document outlines how plugins integrate with VCS, how they are packaged, and how the platform keeps them isolated and compatible.

## Entry Points and Hooks

- **Entry module**: Each plugin exposes a Python module declared under the `vcs.plugins` entry point. The module must define a `register()` function that receives a `PluginRegistry` instance.
- **Registration**: `register()` returns a dictionary of hooks that the core app uses to call plugin features.
- **Lifecycle hooks**
  - `init(config)` – optional setup step run at plugin load time.
  - `preprocess(dataset_dir)` – prepare data before training.
  - `train(dataset, progress_cb)` – launch training and report progress.
  - `synthesize(text, voice_config)` – generate audio for previews or testing.
- **Data exchange**: Datasets and results are passed as JSON‑serializable objects or paths within a project workspace. Progress callbacks emit percentage and status strings.

## Packaging and Dependencies

- **Format**: Plugins are Python packages distributed as wheels (`.whl`) or source archives. A `vcs_plugin.yaml` manifest at the package root declares:
  - `name`, `version`, `description`
  - `api_version` – targeted VCS plugin API version
  - `dependencies` – additional Python packages or system libraries
- **Dependency management**: VCS installs plugins into an isolated virtual environment using Poetry. Each plugin ships its own `pyproject.toml` with locked dependencies to avoid conflicts. System‑level requirements are pulled from the manifest and installed before activation.

## Security and Version Compatibility

- **Sandboxing**: Plugins run in worker processes with restricted filesystem access and resource limits. Tasks execute in containers that mount only the project workspace and temporary directories. Network access is disabled unless explicitly allowed by the manifest.
- **Permissions**: The registry exposes only limited APIs, preventing plugins from mutating core settings or other projects.
- **Version checks**: At load time VCS verifies `api_version` against the core API semantic version. Incompatible plugins are skipped with a warning. Plugins may also declare minimum compatible core versions and supported operating systems.
- **Updates**: When VCS upgrades its plugin API, shims maintain backward compatibility for at least one minor version, giving plugin authors time to adapt.

