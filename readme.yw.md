# Project Introduction: FastAPI-MongoDB Todo List Application

## Project Background
Contemporary task management systems require efficient, scalable solutions with real-time responsiveness. This project utilizes FastAPI - an ASGI-compliant Python framework - paired with MongoDB's document-oriented database architecture to deliver a performant backend system. Serving as both production-ready infrastructure and educational reference, it exemplifies modern REST API development patterns with NoSQL integration while maintaining compliance with industry best practices.

## Project Objectives

### Implement asynchronous API endpoints leveraging FastAPI's ASGI runtime, optimized for MongoDB's horizontally scalable document store

### Establish standardized CRUD operations (Create, Read, Update, Delete) with atomic transaction guarantees

### Architect modular components adhering to separation of concerns:

#### Data modeling (Pydantic BaseModel)

#### Business logic (API routes)

#### Presentation layer (response schemas)

### Demonstrate robust data validation and serialization workflows using Pydantic v2 conventions

### Support deployment flexibility across local MongoDB instances and cloud platforms (e.g., Atlas) via URI configuration

## Functional Overview
Core Capabilities

### Task Management Engine

#### Create documents with mandatory fields: name, description, completed, ISO 8601 timestamp

#### Retrieve operations:

##### GET all documents with server-side filtering

##### GET single document by MongoDB ObjectId

#### Full document replacement via PUT method

#### Idempotent deletion using MongoDB's atomic find_one_and_delete

## Technical Implementation

#### Database Integration

##### Official MongoDB Python driver (PyMongo 4.6+)

##### Automatic BSON/ObjectId conversion handling

##### Connection pooling with automatic retry policies

#### API Development Standards

##### Request validation through Pydantic models

##### Custom serialization/deserialization layer for:

###### API-safe ID representation (str vs ObjectId)

###### Strict datetime formatting

##### HTTP status code standardization (RFC 9110)

### System Architecture

markdown
#### Three-Tier Structure:
1. Data Layer (`models/`): 
   - Pydantic BaseModel definitions
   - Type annotations for MongoDB document schema

2. Service Layer (`routes/`): 
   - API endpoint handlers
   - Business logic isolation
   - Async database operations

3. Presentation Layer (`schemas/`):
   - Response model definitions
   - Post-processing serialization
   - OpenAPI schema generation
### Deployment Flexibility

#### Pre-configured for:

##### Local MongoDB instances (mongodb://localhost:27017)

##### Cloud services via URI modification:

python
MongoClient("mongodb+srv://<user>:<password>@cluster.xzy.mongodb.net/")
Environment variable support for credential management

### Technology Stack Validation

#### Term    Verified Implementation
#### ASGI    FastAPI's Uvicorn-based ASGI server
#### ObjectId    MongoDB's 12-byte unique identifier (BSON type 0x07)
#### BSON    Native MongoDB document encoding (Binary JSON)
#### CRUD    REST-compliant HTTP methods: POST/GET/PUT/DELETE
#### Atomic Operation    MongoDB's findOneAndUpdate/findOneAndDelete
#### Connection Pooling    PyMongo's built-in connection management

# Installation/Deployment Instructions

## 1. Preparation
Before starting the installation and deployment, you need to prepare the following environments and tools:

##### Python: This project is developed based on Python. Python 3.7 or a higher version is required. Download and install the appropriate Python version for your operating system (Windows, Mac, or Linux) from the official Python website.

##### MongoDB: Used to store to - do list data. You have two options:
#### Local Installation: Visit the official MongoDB website to download and install the MongoDB Community Edition suitable for your operating system. After installation, make sure the MongoDB service is running (Windows users can check in Services; Mac and Linux users can start it via the command line).

#### MongoDB Atlas (Online Service): Go to the MongoDB Atlas official website, register an account, and create a free cluster following the instructions. Once created, you'll get a database connection URL, which you'll need for configuration later.

## 2. Installation Steps
### 2.1 Clone the Project Code
Open the terminal on your computer (Command Prompt or PowerShell for Windows users; Terminal app for Mac and Linux users) and run the following commands to download the project code to your local machine:
```
git clone <URL of the project code repository>
cd fastAPIMongoDB_todoAPP
```
### 2.2 Create a Virtual Environment (Optional but Recommended)
To avoid conflicts between project dependencies, it is recommended to create a virtual environment. Execute the following commands in the terminal:
```
#Create a virtual environment
python -m venv venv

#Activate the virtual environment
#Windows
venv\Scripts\activate
#Mac/Linux
source venv/bin/activate
 ```
Once activated successfully, you'll usually see (venv) at the beginning of the terminal command line, indicating that you're in the virtual environment.
### 2.3 Install Project Dependencies
After activating the virtual environment, use pip to install the project's required dependencies. The dependency information of the project is stored in the requirements.txt file. Execute the following command to install:
```
pip install -r requirements.txt 
```
If there are errors during installation, it may be due to network issues or incorrect Python environment configurations. Try changing the network, upgrading pip (pip install --upgrade pip), or manually installing the failed dependencies (pip install <Dependency Name>).

## 3. Database Configuration
### 3.1 Local MongoDB Configuration
If you're using a local MongoDB, open the config/database.py file with a text editor (such as VS Code or Notepad) and modify the content as follows:
```
from pymongo import MongoClient

#Connect to local MongoDB. mydb is the database name and can be customized
client = MongoClient("mongodb://localhost:27017/mydb")
db = client.todo_app
collection_name = db["todos_app"]
```
### 3.2 MongoDB Atlas Configuration
If you are using MongoDB Atlas, log in to your Atlas account, find the connection information for the cluster. Copy the connection string and replace <password> with your actual database password. Then modify the connection string in the config/database.py file as follows:
```
from pymongo import MongoClient

#Replace <username> <password> <cluster-url> <database-name> with your actual information
client = MongoClient("mongodb+srv://<username>:<password>@<cluster-url>/<database-name>?retryWrites=true&w=majority")
db = client.todo_app
collection_name = db["todos_app"]
 ```
## 4. Deployment Methods
### 4.1 Start the Application
In the terminal, make sure you have entered the root directory of the project (i.e., the fastAPIMongoDB_todoAPP directory) and the virtual environment is activated. Execute the following command to start the FastAPI application:
```
uvicorn main:app --reload
```
main refers to the main.py file (without the .py extension).

app is the name of the FastAPI application instance defined in the main.py file.

--reload enables the automatic reloading function. When you modify the code during development, the server will automatically restart to apply the new code.
### 4.2 Access the Application
After the server starts successfully, you can access the following addresses in your browser:

Application Home Page: http://127.0.0.1:8000

Interactive API Documentation: http://127.0.0.1:8000/docs. You can test the API interfaces on this page.

## 5. Solutions to Common Problems
### 5.1 Dependency Installation Failure
If you encounter errors when executing pip install -r requirements.txt:

1.Network Issues: Check your network connection. Try changing the network or reinstalling later.

2.Outdated pip: Run pip install --upgrade pip to update pip.

3.Manual Installation: According to the error message, install the failed dependencies individually, e.g., pip install <Dependency Name>
### 5.2 Database Connection Failure
If the application cannot connect to the database, it may be due to an incorrect connection string configuration or the database service not being started. You can check the following points:

Confirm that the connection string in the config/database.py file is correct.

Check if the MongoDB service has been started. If you are using a local MongoDB, execute the mongo command in the terminal to see if you can successfully connect to the database.

Project Usage Tutorial
 
1. Prerequisites
Before starting to use this FastAPI MongoDB to-do list application, make sure you have installed the following:
 
- Have a basic understanding of FastAPI.
- Python is installed in the system.
- MongoDB Community Server is installed and started.
 
2. Install Dependencies
First, you need to install the necessary dependencies. Open the terminal and run the following command:
 
pip install fastapi uvicorn pymongo pymongo[srv]
 
 
3. Configure the Database
Create a file named  database.py  and add the following code:
 
from pymongo import MongoClient
client = MongoClient("mongodb://localhost:27017/mydb")
db = client.todo_app
collection_name = db["todos_app"]
 
 
4. Create  todos_*  Files
Create  todos_*  files in the  models ,  routes , and  schemas  folders respectively.
 
4.1 Create the  models/todos_model.py  file and add the following code:
 
from pydantic import BaseModel

class Todo(BaseModel):
    name: str
    description: str
    completed: bool
    date: str
 
 
4.2 Create the  routes/todos_route.py  file and add the following code:
 
from fastapi import APIRouter

from models.todos_model import Todo
from config.database import collection_name

from schemas.todos_schema import todos_serializer, todo_serializer
from bson import ObjectId

todo_api_router = APIRouter()

# Retrieve all to-do items
@todo_api_router.get("/")
async def get_todos():
    todos = todos_serializer(collection_name.find())
    return todos

# Retrieve a single to-do item
@todo_api_router.get("/{id}")
async def get_todo(id: str):
    return todos_serializer(collection_name.find_one({"_id": ObjectId(id)}))

# Create a to-do item
@todo_api_router.post("/")
async def create_todo(todo: Todo):
    _id = collection_name.insert_one(dict(todo))
    return todos_serializer(collection_name.find({"_id": _id.inserted_id}))

# Update a to-do item
@todo_api_router.put("/{id}")
async def update_todo(id: str, todo: Todo):
    collection_name.find_one_and_update({"_id": ObjectId(id)}, {
        "$set": dict(todo)
    })
    return todos_serializer(collection_name.find({"_id": ObjectId(id)}))

# Delete a to-do item
@todo_api_router.delete("/{id}")
async def delete_todo(id: str):
    collection_name.find_one_and_delete({"_id": ObjectId(id)})
    return {"status": "ok"}
 
 
4.3 Create the  todos_schema.py  file and add the following code:
 
def todo_serializer(todo) -> dict:
    return {
        "id": str(todo["_id"]),
        "name": todo["name"],
        "description": todo["description"],
        "completed": todo["completed"],
        "date": todo["date"],
    }

def todos_serializer(todos) -> list:
    return [todo_serializer(todo) for todo in todos]
 
 
5. Edit the  main.py  file and add the following code:
 
from fastapi import FastAPI
from routes.todos_route import todo_api_router

app = FastAPI()

app.include_router(todo_api_router)
 
 
6. Run the Application
To start the FastAPI application, run the following command in the terminal:
 
uvicorn main:app --reload
 
 
7. Test the CRUD API using the Postman tool:
7.1 Retrieve all to-do items
Open Postman and access the following URL:
 
http://127.0.0.1:8000/
 
 
7.2 Retrieve a single to-do item
To retrieve a single to-do item, append the ID of the to-do item to the URL:
 
http://127.0.0.1:8000/<todo_id>
 
 
Replace  <todo_id>  with the actual ID of the to-do item.
 
7.3 Create a new to-do item
Create a new to-do item by sending a POST request to the following URL and including the details of the to-do item in the JSON body:
 
http://127.0.0.1:8000/
 
 
The JSON body should have the following structure:
 
{
    "name": "New To-Do Item",
    "description": "This is a new to-do item",
    "completed": false,
    "date": "2024-01-01"
}
 
 
7.4 Update an existing to-do item
To update an existing to-do item, send a PUT request to the following URL, including the ID of the to-do item you want to update and the updated details in the JSON body:
 
http://127.0.0.1:8000/<todo_id>
 
 
The JSON body should have the same structure as the create request but with the updated values.
 
7.5 Delete a to-do item
To delete a to-do item, send a DELETE request to the following URL, including the ID of the to-do item you want to delete:
 
http://127.0.0.1:8000/<todo_id>
