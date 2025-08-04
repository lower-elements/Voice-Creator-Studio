# Voice-Creator-Studio

Historically, TTS voice and language creation has been a laborious and complex task that could only be pulled off by programmers and data scientists. This is beginning to change thanks to the rise of neural TTS models, but unfortunately not everyone has the necessary hardware capable of running these computationally expensive models.

Under certain circumstances, neural models are less practical than older speech systems such as formant synthesis, which are designed for speed. Some neural TTS systems and even non-TTS-related applications, such as [subaligner](https://github.com/baxtree/subaligner), use formant synthesizers like [eSpeak-NG](https://github.com/espeak-ng/espeak-ng) as a backbone. Unfortunately, this means that in order to support multiple languages, Subaligner depends on eSpeak-NG’s language support. eSpeak-NG has good support for a majority of European languages, but it fails at accurately parsing other languages, especially those that use special, non-Latin characters.

As long as languages and voices have to be manually created and tuned by hand by professionals, many languages might never be improved or even created in the first place. We believe anyone with a decent computer and recording equipment should be able to contribute to voice and language creation for any TTS system. Voice-Creator-Studio, referred to as VCS for the rest of this document, aims to make that happen.

## Blueprint

### Interface

The interface should be similar, but not identical, to that of the [Piper Recording Studio](https://github.com/rhasspy/piper-recording-studio) interface, referred to as PRS for the rest of this document. Much like PRS, VCS should be a server-hosted web app. The user records their voice, and the app takes care of cleaning up the audio and transcribing it in the background, though the user will be able to fix transcription errors if need be. Where VCS differs from PRS is that the user will be able to create multiple voice projects or download voice projects from a repository if they don’t want to record their own voice. Safety precautions will be paramount to ensure bad actors cannot easily steal other people’s voices.

### Voice Training

VCS should allow the user to train voices for:

* Neural engines such as Piper or Tortus
* HMM-based systems such as RH Voice, Festival, Flite, or Open JTalk
* Concatenative systems such as Festival or Flite
* Singing synthesis standards such as Utau, Diff Singer, and NNSVS / ENUNU
* Any other system that supports plugins (more on plugins later)

Most notably, VCS should allow the user to create a language configuration for formant systems such as eSpeak-NG simply by recording a voice in that language. Using machine-learning models, VCS will do all the heavy lifting—analyzing intonation and context patterns, writing parameters, etc.—and will compile the synthesizer if need be. The user should never have to worry about any of the complicated parts of voice or language creation for any synthesizer unless they choose to.

### Plugins

VCS is intended to be licensed under the AGPL to ensure all improvements are given back to the open-source community. That said, not all speech engines are licensed under the GPL family of licenses, and the goal of VCS is to make it possible to train voices for as many engines as possible. To that end, a developer should be able to write plugins for new speech engines, and those plugins should be permitted to be licensed separately from VCS itself. We can’t include Piper with VCS due to licensing complications, but we would be able to write a Piper plugin and license it under the MIT license or another similarly permissive license. Plugins will also be able to add other improvements besides support for additional TTS engines.

## Technology Stack & Development Setup

### Backend

* **Language/Framework**: Python with [FastAPI](https://fastapi.tiangolo.com/) provides an async REST API that can easily integrate with machine-learning libraries used for training and synthesis.
* **Packaging**: [Poetry](https://python-poetry.org/) manages dependencies and virtual environments.

### Frontend

* **Framework**: [React](https://react.dev/) with TypeScript via [Vite](https://vitejs.dev/) for fast development and production builds.
* **Styling**: [Tailwind CSS](https://tailwindcss.com/) supplies a utility-first approach that keeps styles consistent and composable.

### Development Tooling

* **Code Quality**: [`pre-commit`](https://pre-commit.com/) runs Black, isort, Flake8, and MyPy for Python code, plus ESLint and Prettier for the frontend.
* **Environment**: [Docker](https://www.docker.com/) images ensure reproducible development and deployment setups.

### Build Pipeline

* **Continuous Integration**: GitHub Actions lint and test both backend and frontend on every pull request.
* **Deployment**: Successful builds publish a multi-service Docker image that serves the FastAPI backend and the static React frontend.

## Project Management and Repository

See [docs/project-management.md](docs/project-management.md) for details on project fields, repository import/export formats, and switching or sharing projects.
