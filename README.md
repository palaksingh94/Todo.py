# Todo.py
Successfully completed a To-Do List application using Python as part of my internship at CodSoft. This project helped me understand task management logic, user input handling, and basic file operations in Python. It enhanced my problem-solving skills  in Python programming.  #CodSoft #CodSoftInternship #PythonProgramming #ToDoList 
import json
import os

FILE_NAME = "todo_list.json"

# Load tasks from file
def load_tasks():
    if os.path.exists(FILE_NAME):
        with open(FILE_NAME, "r") as file:
            return json.load(file)
    return []

# Save tasks to file
def save_tasks(tasks):
    with open(FILE_NAME, "w") as file:
        json.dump(tasks, file, indent=4)

# Display tasks
def view_tasks(tasks):
    if not tasks:
        print("\nNo tasks found.\n")
        return

    print("\nTo-Do List:")
    for index, task in enumerate(tasks, start=1):
        # The screenshot code for status uses a conditional expression inside an f-string
        status = 'X' if task["completed"] else ' '
        print(f"{index}. [{status}] {task['title']}")
    print() # For a newline after the list

# Add a task
def add_task(tasks):
    title = input("Enter task title: ")
    task = {"title": title, "completed": False}
    tasks.append(task)
    save_tasks(tasks)
    print("Task added successfully!\n")

# Update task title (Based on typical To-Do list functionality, though not fully shown in screenshots)
def update_task(tasks):
    view_tasks(tasks)
    if not tasks:
        return

    try:
        task_no = int(input("Enter task number to update: "))
        if 1 <= task_no <= len(tasks):
            new_title = input("Enter new task title: ")
            tasks[task_no - 1]["title"] = new_title
            save_tasks(tasks)
            print("Task updated successfully!\n")
        else:
            print("Invalid task number.\n")
    except ValueError:
        print("Invalid input. Please enter a number.\n")

# Mark task as completed
def complete_task(tasks):
    view_tasks(tasks)
    if not tasks:
        return

    try:
        task_no = int(input("Enter task number to mark as completed: "))
        # The screenshot code uses task_no - 1 for the list index
        tasks[task_no - 1]["completed"] = True
        save_tasks(tasks)
        print("Task marked as completed!\n")
    except (IndexError, ValueError):
        print("Invalid task number.\n")

# Delete a task
def delete_task(tasks):
    view_tasks(tasks)
    if not tasks:
        return

    try:
        task_no = int(input("Enter task number to delete: "))
        # The screenshot code uses task_no - 1 for pop()
        tasks.pop(task_no - 1)
        save_tasks(tasks)
        print("Task deleted successfully!\n")
    except (IndexError, ValueError):
        print("Invalid task number.\n")

# Main menu function
def main():
    tasks = load_tasks()

    while True:
        print("==== TO-DO LIST MENU ====")
        print("1. View Tasks")
        print("2. Add Task")
        print("3. Update Task")
        print("4. Mark Task as Completed")
        print("5. Delete Task")
        print("6. Exit")

        choice = input("Choose an option (1-6): ")

        if choice == "1":
            view_tasks(tasks)
        elif choice == "2":
            add_task(tasks)
        elif choice == "3":
            update_task(tasks)
        elif choice == "4":
            complete_task(tasks)
        elif choice == "5":
            delete_task(tasks)
        elif choice == "6":
            print("Goodbye!")
            break
        else:
            print("Invalid choice. Try again.\n")

if __name__ == "__main__":
    main()
