# To-Do-app
from fastapi import FastAPI
from pydantic import BaseModel
app = FastAPI()
# Define a task model
class Task(BaseModel):
title: str
description: str = None
completed: bool = False
# Create a list of tasks
tasks = []
# Create an endpoint to create a new task
@app.post("/tasks")
async def create_task(task: Task):
tasks.append(task)
return {"message": "Task created successfully"}
# Create an endpoint to get all tasks
@app.get("/tasks")
async def get_tasks():
return tasks
# Create an endpoint to get a specific task by index
@app.get("/tasks/{task_index}")
async def get_task(task_index: int):
return tasks[task_index]
# Create an endpoint to update a specific task by index
@app.put("/tasks/{task_index}")
async def update_task(task_index: int, task: Task):
tasks[task_index] = task
return {"message": "Task updated successfully"}
# Create an endpoint to delete a specific task by index
@app.delete("/tasks/{task_index}")
async def delete_task(task_index: int):
tasks.pop(task_index)
return {"message": "Task deleted successfully"}
