# Grade_ease
An AI-powered Grading Assistant helps teachers evaluate written work by using pre-designed rubrics or allowing them to upload their own.
Architecture
GradeMate is built using JavaScript for the frontend and Python for the backend. Specifically, the frontend is a ReactJS app while the backend is a Django app, functioning as an API endpoint for the frontend.

Requirements
The required programming languages are Node.js and Python. Versions used: Python 3.12.3, Node v22.3.0, npm 10.8.1.

For installation of JavaScript and Python dependencies, see the setup instructions below.

Set-Up Instructions
1.(Optional) Create and activate a virtual environment.
1.A. Using the command line, install virtualenv:
```bash
pip install virtualenv
```
Note: if using Homebrew to manage packages, the command is likely brew install virtualenv.

1.B. Create a virtual environment by first navigating to the project folder and then running this command:
```bash
virtualenv venv
```
This command creates a virtual environment called "venv" contained in the homonymous folder. By using the same name for the virtual environment, git will know to ignore it (since it's listed in the .gitignore file).
1.C. Activate the virtual environment:
```bash
source venv/bin/activate
```
2.Create and store the GOOGLE_API_KEY.
Obtain a Google API KEY here: https://aistudio.google.com/app/apikey

3.Prepare the .env file
Create a Django secret key by running the following command.
```bash
python -c "from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())"
```
Create a .env file in the project directory. Add the required environment variables:
```bash
GOOGLE_API_KEY="<Insert-API-Key-here>"
DJANGO_SECRET_KEY="<Insert-Django-Key-here>"
DJANGO_DEBUG="True"
SECURITY_SETTINGS="False"
```
4.Install dependencies.
Using npm for JavaScript dependencies, from the frontend directory:
```bash
npm install
```
Using pip for Python dependencies, from the project directory:
```bash
pip install -e .
```
5.Run the development servers.
To start the Django backend:
```bash
python manage.py runserver
```
For the ReactJS frontend (from the frontend directory):
```bash
npm start
```
Note: Since the two development servers need to run at the same time, open each in a separate terminal.
7.View the app at http://localhost:3000
Tips for deployment
Before running the code on a live website, use the .env file on the host server to turn on the security settings and turn off the Django debug mode.

.env file:
```bash
DJANGO_DEBUG="False"
SECURITY_SETTINGS="True"
```
Deployment
To avoid installing Node.js on the app's hosting server, it is possible to use the static files generated from running npm run build locally. Since running the build locally does not allow accessing environment variables from the host server, we added a frontend/src/config.json file to store the URL of the host server. This is needed by the frontend to make API requests to the backend.

The script prepare_static_for_hosting.py automates the steps to obtain and collect required static files, including obtaining the host base URL, running the ReactJS build, and collecting Django static files. If hosting on a different site, the URLs specified in the script for the development and production sites need to be updated accordingly.

Additional Instructions
(Optional) Modifying the db.sqlite3 database
The recommended way to modify the database is through the admin site. Make sure that the backend server is running, and then, from a browser, navigate to the admin site: http://localhost:8000/admin. The admin site allows both viewing and modifying the data. It also allows managing users and user group authentication and authorization.

It is also possible to view and modify the db.sqlite3 database with a database browsing App, such as DB Browser for SQLite (downloadable here: https://sqlitebrowser.org/). However, using the admin site is recommended.

(Optional) Replacing the db.sqlite3 database with other external data
The developer can also replace the existing db.sqlite3 database with new data in the format expected by the backend/management/commands/load_grading_rubric_data.py file.

To run this loading function, first delete the db.sqlite3 database and then run the following command.

python manage.py load_grading_rubric_data
Note: As of release 0.0.1, the load_grading_rubric_data module assumes a specific location for the rubrics_data_for_loading directory. Adjust path in script accordingly.

To migrate the database and set-up an admin account, please consult Django documentation.

Helpful Resources
We consulted the following tutorials and documentation to help us integrate ReactJS with the Django framework and prepare to deploy on PythonAnywhere:

The Perfect Match: How to Integrate ReactJS with Django Framework for Stunning Web Apps
Modern JavaScript for Django developers
Streaming LLM Output with Django, React, and LangChain
Deploying Django to production
PythonAnywhere: Deploying an existing Django project on PythonAnywhere
PythonAnywhere: How to connect production React frontend with a Python backend





