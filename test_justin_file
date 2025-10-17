from datetime import datetime
from pathlib import Path
import csv

DATA_FILE = Path("tasks.csv")

def load_tasks():
    tasks = []
    if DATA_FILE.exists():
        with DATA_FILE.open(newline="", encoding="utf-8") as f:
            for row in csv.DictReader(f):
                tasks.append(row)
    return tasks

def save_tasks(tasks):
    with DATA_FILE.open("w", newline="", encoding="utf-8") as f:
        writer = csv.DictWriter(f, fieldnames=["title", "due", "category", "status"])
        writer.writeheader()
        writer.writerows(tasks)

def validate_date(s):
    try:
        datetime.strptime(s, "%Y-%m-%d")
        return True
    except ValueError:
        return False

def add_task(tasks):
    while True:
        title = input("Titel der Aufgabe: ").strip()
        if not title:
            print("Titel darf nicht leer sein.")
            continue
        due = input("Fälligkeitsdatum (YYYY-MM-DD): ").strip()
        if not validate_date(due):
            print("Ungültiges Datumsformat. Bitte erneut eingeben.")
            continue
        category = input("Kategorie (optional): ").strip()
        tasks.append({
            "title": title,
            "due": due,
            "category": category,
            "status": "OPEN"
        })
        print("Aufgabe hinzugefügt!")
        break

def view_tasks(tasks):
    if not tasks:
        print("\nKeine Aufgaben vorhanden.\n")
        return
    tasks_sorted = sorted(tasks, key=lambda t: t["due"])
    print("\n# Aufgaben (sortiert nach Fälligkeitsdatum)")
    for i, t in enumerate(tasks_sorted, 1):
        print(f"{i}. [{t['status']}] {t['title']} (Fällig: {t['due']})"
              f"{' - ' + t['category'] if t['category'] else ''}")
    print()

def mark_done(tasks):
    view_tasks(tasks)
    if not tasks:
        return
    while True:
        sel = input("Nummer der Aufgabe, die erledigt ist: ").strip()
        if not sel.isdigit() or not (1 <= int(sel) <= len(tasks)):
            print("Ungültige Auswahl.")
            continue
        idx = int(sel) - 1
        tasks[idx]["status"] = "DONE"
        print(f"'{tasks[idx]['title']}' als erledigt markiert.")
        break

def main():
    tasks = load_tasks()
    while True:
        print("\n=== TO-DO LISTE ===")
        print("1) Aufgabe hinzufügen")
        print("2) Aufgaben anzeigen")
        print("3) Aufgabe als erledigt markieren")
        print("4) Speichern & Beenden")
        choice = input("> ").strip()

        if choice == "1":
            add_task(tasks)
            save_tasks(tasks)
        elif choice == "2":
            view_tasks(tasks)
        elif choice == "3":
            mark_done(tasks)
            save_tasks(tasks)
        elif choice == "4":
            save_tasks(tasks)
            print("Aufgaben gespeichert. Programm beendet.")
            break
        else:
            print("Bitte eine Zahl zwischen 1 und 4 eingeben.")

if __name__ == "__main__":
    main()
