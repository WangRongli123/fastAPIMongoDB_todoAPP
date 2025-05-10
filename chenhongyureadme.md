# Installation/Deployment Instructions

## 1. Prerequisites
Before starting the installation and deployment, ensure that the following environments and tools are installed:
Python: This project is developed based on Python. It is recommended to use Python 3.7 or a higher version. You can download and install the version suitable for your operating system from the official Python website.
MongoDB: Used to store to - do list data. You can choose to install a local MongoDB Community Server or use an online service such as MongoDB Atlas.
Local Installation: Download and install the MongoDB Community Edition suitable for your operating system from the official MongoDB website.
MongoDB Atlas: If you want to use an online service, you can register and create a MongoDB Atlas account and create a free cluster.

## 2. Installation Steps
### 1. Clone the Project Code
First, clone the project code to your local machine. Open the terminal (Windows users can use the Command Prompt or PowerShell, while Mac and Linux users can use the Terminal application) and execute the following command:
``` git clone <URL of the project code repository>
cd fastAPIMongoDB_todoAPP
```
Replace <URL of the project code repository> with the actual URL of the project code repository.
### 2. Create a Virtual Environment (Optional but Recommended)
To avoid conflicts between project dependencies, it is recommended to create a virtual environment. Execute the following commands in the terminal:
``` #Create a virtual environment
python -m venv venv

#Activate the virtual environment
#Windows
venv\Scripts\activate
#Mac/Linux
 ```
### 3. Install Project Dependencies
After activating the virtual environment, use pip to install the project's required dependencies. The dependency information of the project is stored in the requirements.txt file. Execute the following command to install:
`pip install -r requirements.txt `

## 3. Database Configuration
### 1. Local MongoDB Configuration
If you are using a locally installed MongoDB, open the config/database.py file and modify the connection string as follows:
from pymongo import MongoClient

client = MongoClient("mongodb://localhost:27017/mydb")
db = client.todo_app
collection_name = db["todos_app"]
### 2. MongoDB Atlas Configuration
If you are using MongoDB Atlas, log in to your Atlas account, find the connection information for the cluster. Copy the connection string and replace <password> with your actual database password. Then modify the connection string in the config/database.py file as follows:
``` from pymongo import MongoClient

client = MongoClient("mongodb+srv://<username>:<password>@<cluster-url>/<database-name>?retryWrites=true&w=majority")
db = client.todo_app
collection_name = db["todos_app"]
 ```
## 4. Deployment Methods
### 1. Start the Application
In the terminal, make sure you have entered the root directory of the project (i.e., the fastAPIMongoDB_todoAPP directory) and the virtual environment is activated. Execute the following command to start the FastAPI application:

`uvicorn main:app --reload `
main is the name of the main.py file (excluding the .py extension).
app is the name of the FastAPI application instance defined in the main.py file.
The --reload option is used to enable the automatic re - loading function. During the development process, when you modify the code, the server will automatically restart to apply the new changes.
### 2. Access the Application
After the server starts successfully, you can access the following addresses in your browser:
Application Home Page: http://127.0.0.1:8000
Interactive API Documentation: http://127.0.0.1:8000/docs. You can test the API interfaces on this page.

## 5. Solutions to Common Problems
### 1. Dependency Installation Failure
If you encounter a dependency installation failure when executing pip install -r requirements.txt, it may be due to network issues or incorrect Python environment configuration. You can try the following solutions:
Check the network connection to ensure that you can access the Python Package Index (PyPI) normally.
Upgrade pip to the latest version: pip install --upgrade pip.
Manually install the missing dependencies: pip install <dependency name>.
### 2. Database Connection Failure
If the application cannot connect to the database, it may be due to an incorrect connection string configuration or the database service not being started. You can check the following points:
Confirm that the connection string in the config/database.py file is correct.
Check if the MongoDB service has been started. If you are using a local MongoDB, execute the mongo command in the terminal to see if you can successfully connect to the database.
