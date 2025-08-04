# Project Management and Repository Interaction

## Voice Project Fields
- **Name**: Human-readable identifier for the project.
- **Language**: Language code (e.g., `en-US`) indicating the voice's language.
- **Engine Type**: Target synthesis engine such as Piper, RH Voice, or others.
- **Metadata**: Additional details like description, author, license, or tags.

## Repository Interaction
Projects can be stored locally or synchronized with remote repositories.

- **Import**: Load from a `.zip` archive or clone from a Git repository containing project files and metadata.
- **Export**: Save as a `.zip` archive or push commits to a remote Git repository.
- **Version Control**: Each project is tracked with Git, enabling branching and history for recordings, transcripts, and configuration.

## Switching and Sharing Projects
- The dashboard lists available projects; selecting a different entry switches context.
- To share a project, export it as an archive or push to a shared repository so others can pull or clone it.
- Importing shared archives or repositories adds them to the dashboard for further editing.
