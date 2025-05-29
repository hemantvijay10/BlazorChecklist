BlazorChecklist

A simple, server-side Blazor application that lets you maintain a to-do checklist: add new tasks, mark them complete (with timestamps), edit descriptions in-place, and delete unfinished items. This is a learning-stage, practice project—there’s plenty of room for enhancements, but it shows off core Blazor skills, component patterns, and basic SAST hardening.

Features

1. Add new tasks (up to 500 characters), with built-in form validation
2. Edit any existing task inline by clicking its label
3. Complete tasks via checkbox, automatically timestamping the completion time
4. Delete unfinished tasks by clicking the “×” button next to them
5. Delete All to clear the entire list in one click
6. Single-responsibility task model with a unique GUID key for safe updates
7. Uses <EditForm> + data annotations for clean validation UI
8. Employs the @key directive for efficient DOM diffing
9. Accessible ARIA labels on delete buttons

Code Structure

1. BlazorChecklist.razor — the main page component containing markup, form, and task list UI
2. NewTaskModel — a private class decorated with data-annotation attributes for validation
3. TaskItem — a private model class with a Guid Id, Description, completion flag/time, and editing flag
4. Event handlers (AddTask, CompleteTask, DeleteTask, etc.) are keyed by Guid to avoid collision when two tasks share the same text.

How It Works

1. Add Task

User types into the <InputTextArea> bound to _newTask.Description. On submit, the form validates (required + max length) and invokes AddTask(). A new TaskItem with a fresh GUID is appended to the Tasks list, and the input resets.

2. Edit Task

Clicking a task’s label sets EditingTaskId to that task’s GUID. The label is replaced by an <InputText> bound to task.Description. On blur or Enter, EditingTaskId is cleared, returning to read-only mode.

3. Complete Task

Checking the box calls CompleteTask(id), sets IsCompleted = true, and records CheckedAt = DateTime.Now. The checkbox is then disabled, and the time appears next to the task.

4. Delete Task

Clicking the “×” button next to an unfinished task invokes DeleteTask(id). Only tasks where IsCompleted == false may be removed.

5. Delete All

Clears the entire Tasks list in one click.

Future Improvements

1. Persistence: integrate local storage, a web API, or a database to save tasks between sessions.
2. Unit & Integration Tests: Add test coverage.
3. Responsive Design: make the layout adapt to mobile screens.
4. Advanced Editing: allow multi-line tasks, markdown support, and drag-&-drop reordering.
5. Internationalization: support different cultures for timestamp formatting.

Acknowledgements: This project was built as I’m learning Blazor. Thanks to the following course for providing a solid foundation.

Blazor Deep Dive - From Beginner to Advanced in .NET 8 https://www.udemy.com/course/blazor-deep-dive-from-beginner-to-advanced/?couponCode=CP130525BRGB

Feel free to fork, experiment, and submit pull requests!
