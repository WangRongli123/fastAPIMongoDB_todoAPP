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
