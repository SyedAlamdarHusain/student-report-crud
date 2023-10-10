# Video Tutorials
- [Video Tutorial of running the source code](https://youtu.be/oq2P988w-MQ)
- [Video Tutorial of running the application](https://www.youtube.com/watch?v=s5rXZN1cev4)

# Installation and Setup
## Prerequisites
Before starting, make sure you have the following software installed on your system:
- MySQL
- XAMPP
- Python 3
- Node.js

## Database Setup
### Install MySQL
If you haven't already installed MySQL, download and install it from the official website.

### XAMPP
1. Download and install XAMPP from the official website.
2. Start Apache and MySQL from XAMPP:
   - Launch XAMPP and start the Apache and MySQL services from the control panel.
3. Access the Dashboard:
   - Open your web browser and go to http://localhost/dashboard/ to access the XAMPP dashboard.
4. Create a Database:
   - In the XAMPP dashboard, navigate to the phpMyAdmin section.
   - Click on "New" to create a new database called "studentreportsyedhusain"

#### IF YOU WISH TO RENAME DATABASE:
The database could be renamed to something else, provided that the change is implemented in the code on line 7 of `App.py`. Navigate to line 7 of the code and change `/syedhusainstudentreport` to something else if you wish to.
```python
app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql+pymysql://root:password@localhost/syedhusainstudentreport'
```

# Run SQL Queries:

In the phpMyAdmin interface, select the "studentreport" database. Go to the SQL tab and execute the following SQL queries to create the required tables:

```sql
CREATE TABLE Students (
    StudentID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(255) NOT NULL,
    CreditsEarned INT NOT NULL
);

CREATE TABLE Instructors (
    InstructorID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(255) NOT NULL,
    Department VARCHAR(255) NOT NULL
);

CREATE TABLE Courses (
    CourseID INT AUTO_INCREMENT PRIMARY KEY,
    CourseTitle VARCHAR(255) NOT NULL,
    InstructorID INT,
    FOREIGN KEY (InstructorID) REFERENCES Instructors(InstructorID)
);

CREATE TABLE Enrollments (
    EnrollmentID INT AUTO_INCREMENT PRIMARY KEY,
    StudentID INT,
    CourseID INT,
    Grade INT,
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID),
    FOREIGN KEY (CourseID) REFERENCES Courses(CourseID),
    UNIQUE (StudentID, CourseID)
);
```
# Flask Setup

## Navigate to the Flask Folder:

Open a terminal or command prompt and navigate to the Flask project folder. Use the terminal for the IndividualAssignmentSource code.

```bash
cd IndividualAssignmentSourceCode\Flask_React_Crud
```

Check If there a another folder Flask_React_Crud inside IndividualAssignmentSourceCode\Flask_React_Crud
If there is then do:
```bash
IndividualAssignmentSourceCode\Flask_React_Crud\Flask_React_Crud
```

# Create and Activate a Virtual Environment:

## Run the following commands in the terminal:

```bash
py -3 -m venv venv
venv\Scripts\activate
```

# Install Python Libraries:
## Install the required Python libraries using pip:

```bash
pip install Flask
pip install pymysql
pip install -U Flask-SQLAlchemy
pip install flask-marshmallow
pip install Flask-Cors
```

# Edit App.py code:

Go on App.py and navigate to the line 7 of code:

```python
app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql+pymysql://root:password@localhost/studentreport'
```
Change password after “root:” to your own password

# Run Flask Application:

Once all the libraries are installed, code is edited, and you are running on venv, run the Flask application using the following command:

```bash
flask run
```

# Flask Run:

If you have error running flask make sure the libraries version matches the version on the requirements.txt

run command:
```python
pip3 freeze > requirements.txt
```

Now compare and make sure that your versions matches this requirements list:

```txt
blinker==1.6.2
click==8.1.7
colorama==0.4.6
Flask==3.0.0
Flask-Cors==4.0.0
flask-marshmallow==0.15.0
Flask-SQLAlchemy==3.1.1
greenlet==3.0.0
gunicorn==21.2.0
itsdangerous==2.1.2
Jinja2==3.1.2
MarkupSafe==2.1.3
marshmallow==3.20.1
packaging==23.2
PyMySQL==1.1.0
SQLAlchemy==2.0.21
typing_extensions==4.8.0
Werkzeug==3.0.0
React Setup:
Navigate to the React Folder:
```

Open a terminal or command prompt and navigate to the React project folder.

# Create a React App:

Run the following commands to create a new React app:
```bash
npx create-react-app myreactdev
```

# Install React Libraries:
## Install the required React libraries using npm:

```bash
npm install react-router-dom --save 
npm install axios --save
```


Run the React Application:
Once all the libraries are installed, start the React development server with the following command:
npm start
