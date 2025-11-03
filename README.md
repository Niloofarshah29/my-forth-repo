# my-forth-repo
test
import sys
import json
from pathlib import Path

FILE = Path("todos.json")

def load():
    return json.loads(FILE.read_text()) if FILE.exists() else []

def save(todos):
    FILE.write_text(json.dumps(todos, indent=2))

def add(task):
    todos = load()
    todos.append({"task": task, "done": False})
    save(todos)
    print(f"Added: {task}")

def list_tasks():
    for i, t in enumerate(load(), start=1):
        status = "✔" if t["done"] else "✘"
        print(f"{i}. {t['task']} [{status}]")

if le(sys.argv) > 1:
    cmd = sys.argv[1]
    if cmd == "add":
        add(" ".join(sys.argv[2:]))
    elif cmd == "list":
        list_tasks()
    else:
        print("Usage: python todo.py [add <task> | list]")
