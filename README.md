# To-Do List Manager

Small command-line to-do list manager in Python.  
Store tasks in a plain text file and manage them interactively
via the console.

## Analysis

Problem
- Users need a simple console app to track tasks with due
  dates, priorities and completion status.

Scenario
- A user runs the app, chooses or creates a task file, then
  adds, edits, marks, views or deletes tasks during a session.

User stories
- As a user, I want to add tasks with title, due date and
  priority so I can track work.
- As a user, I want to view tasks sorted by due date to see
  upcoming items first.
- As a user, I want to filter tasks by status (pending/done).
- As a user, I want to mark tasks as done and edit or delete
  tasks.
- As a user, I want my tasks saved to a plain text file.

## Project Requirements (Course)

This project demonstrates:
1. Interactive console input
2. Data validation for user input and file content
3. File processing (read/write task files)

## Features
- Add, edit, delete tasks
- Mark tasks as done
- View all tasks (sorted by due date)
- View tasks by status (pending/done)
- File chooser dialog if Tkinter is available

## Data format
Each task is one line:
title|due_date|priority|status

- due_date: DD-MM-YYYY or `no date`
- priority: low / medium / high
- status: pending / done

## Data validation (implemented)
- Title: required, trimmed, must not contain `|`.
- Due date: empty → `no date`; otherwise validated as
  DD-MM-YYYY using datetime.strptime.
- Priority: accepts `1/2/3` or `low/medium/high`; normalized to
  `low|medium|high`.
- Status: accepts `1/2` or `pending/done`; normalized.
- File loader: ignores blank/malformed lines and reports
  invalid date, priority, or status values.

## File processing
- Input/output: plain text task file selected or created by
  the user (e.g. tasks.txt).
- The app loads tasks at start and saves after changes.
- Malformed lines in the file are ignored with a warning.

## Implementation

Technology
- Python 3.8+ (standard library)
- Optional: Tkinter for file picker

Key modules used
- os — path and file existence checks
- datetime — date parsing and validation
- tkinter.filedialog (optional) — file chooser UI

Repository structure
```
To_do_lsit_BIT_2025_Official-main/
├── to_do.py          # main program
├── README.md
└── <task files>      # user-selected .txt files with tasks
```

How to run 
1. Open the repository in GitHub Codespaces
2. Open the Terminal
3. Run:
   python to_do.py

## Notes for students / instructors
- The program will create the selected file if it does not
  exist.
- If Tkinter is not available, enter a filename manually.
- Keep backups of task files when experimenting.

## Team & Contributions
Justin Vogler - creating main Code and functions, testing
Seraphin Schobin - improving UX, completing Code
Jeremy Heer - creating data validation, testing

## Contributing
Use this repo as a template for coursework. Work in your
own copy and commit regularly.

## License
This project is provided for educational use only as part of the Programming Foundations module.
MIT License

