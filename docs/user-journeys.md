# Voice Creator Studio User Journeys and Screen Designs

## Project Lifecycle Journeys

### Creating a Project
1. From the **Dashboard**, click **New Project**.
2. Enter project name, select language and engine (if applicable).
3. Save to create the project and open the **Project Overview**.

### Editing a Project
1. On the **Dashboard**, choose a project and click **Edit**.
2. Modify project details or navigate to specific tabs (Recording, Transcript, Training, Downloads).
3. Save changes; return to the updated project view.

### Deleting a Project
1. On the **Dashboard**, click the **Delete** icon for a project.
2. Confirm the deletion in the modal dialog.
3. Project is removed and the Dashboard refreshes.

## Screen Descriptions & Wireframes

### Dashboard / Project List
List of existing projects with options to create, edit, or delete.

```
+-------------------------------------------------------+
| Voice Creator Studio                                  |
|-------------------------------------------------------|
| [New Project]                                         |
|                                                       |
| Project Name      Last Modified    Actions            |
| ----------------------------------------------------- |
| My Voice Project  2024-05-01       [Edit] [Delete]     |
| Other Project     2024-04-20       [Edit] [Delete]     |
| ...                                                   |
+-------------------------------------------------------+
```

### Recording Screen
Interface for recording audio clips and managing takes.

```
+-------------------------------------------------------+
| Project: My Voice Project         [Dashboard] [Logout] |
|-------------------------------------------------------|
| Script Line: "Read the displayed sentence aloud."     |
|                                                       |
| [ Record ] [ Stop ]   (Waveform Display)              |
|                                                       |
| Recordings:                                           |
| 1. sentence1.wav   [Play] [Delete]                    |
| 2. sentence2.wav   [Play] [Delete]                    |
+-------------------------------------------------------+
```

### Transcript Correction Screen
Review and correct automatically generated transcripts.

```
+-------------------------------------------------------+
| Project: My Voice Project                             |
|-------------------------------------------------------|
| Clip: sentence1.wav [Play]                            |
| Auto Transcript: "The quick bronw fox."               |
| Corrected Transcript: [The quick brown fox.]          |
|                                                       |
| [ Save ] [ Skip ]                                     |
+-------------------------------------------------------+
| Pending Clips:                                        |
| - sentence2.wav                                       |
| - sentence3.wav                                       |
+-------------------------------------------------------+
```

### Training Status Screen
Displays progress and logs for model training.

```
+-------------------------------------------------------+
| Project: My Voice Project                             |
|-------------------------------------------------------|
| Training Status: In Progress                          |
| Progress: [#####-----] 50%                           |
| Estimated Time Remaining: 10m                        |
|                                                       |
| Logs:                                                 |
| [Latest training logs stream here...]                 |
|                                                       |
| [ Cancel Training ]                                   |
+-------------------------------------------------------+
```

### Downloads Screen
Provides links to download trained models and datasets.

```
+-------------------------------------------------------+
| Project: My Voice Project                             |
|-------------------------------------------------------|
| Available Downloads:                                  |
| - Model (Piper)        [Download]                     |
| - Model (RH Voice)     [Download]                     |
| - Dataset (ZIP)        [Download]                     |
|                                                       |
| [Back to Dashboard]                                   |
+-------------------------------------------------------+
```

