# to-do-list-app
To-Do List App: Create a simple to-do list app that allows users to add, remove, and mark tasks as completed.
Code:

import tkinter as tk
from tkinter import messagebox

class ToDoListApp:
    def __init__(self, root):
        self.root = root
        self.root.title("To-Do List App")
        self.tasks = []

        # Task list
        self.task_list = tk.Listbox(self.root, width=40, height=10)
        self.task_list.pack(padx=10, pady=10)

        # Task entry
        self.task_entry = tk.Entry(self.root, width=40)
        self.task_entry.pack(padx=10, pady=10)

        # Buttons
        self.add_button = tk.Button(self.root, text="Add Task", command=self.add_task)
        self.add_button.pack(padx=10, pady=5)

        self.remove_button = tk.Button(self.root, text="Remove Task", command=self.remove_task)
        self.remove_button.pack(padx=10, pady=5)

        self.complete_button = tk.Button(self.root, text="Mark as Completed", command=self.mark_as_completed)
        self.complete_button.pack(padx=10, pady=5)

    def add_task(self):
        task = self.task_entry.get()
        if task:
            self.tasks.append(task)
            self.task_list.insert(tk.END, task)
            self.task_entry.delete(0, tk.END)
        else:
            messagebox.showwarning("Warning", "Task cannot be empty")

    def remove_task(self):
        try:
            task_index = self.task_list.curselection()[0]
            self.task_list.delete(task_index)
            self.tasks.pop(task_index)
        except IndexError:
            messagebox.showwarning("Warning", "Select a task to remove")

    def mark_as_completed(self):
        try:
            task_index = self.task_list.curselection()[0]
            task = self.tasks[task_index]
            self.tasks[task_index] = f"[Completed] {task}"
            self.task_list.delete(0, tk.END)
            for task in self.tasks:
                self.task_list.insert(tk.END, task)
        except IndexError:
            messagebox.showwarning("Warning", "Select a task to mark as completed")

if __name__ == "__main__":
    root = tk.Tk()
    app = ToDoListApp(root)
    root.mainloop()


How it works:

1. The app has a GUI with a task list, task entry field, and buttons to add, remove, and mark tasks as completed.
2. The add_task method adds a new task to the list when the "Add Task" button is clicked.
3. The remove_task method removes the selected task from the list when the "Remove Task" button is clicked.
4. The mark_as_completed method marks the selected task as completed by prefixing it with "[Completed]" when the "Mark as Completed" button is clicked.
