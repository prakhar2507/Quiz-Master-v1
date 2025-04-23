
# QuizMaster - Online Quiz Platform

QuizMaster is a web-based application built with Flask that allows users to register, attempt quizzes, and view their scores, while administrators can manage users, subjects, chapters, questions, and quizzes. The platform supports role-based access control with separate functionalities for users and admins.

## Features

| **Category**          | **Feature**                     | **Description**                                                                 |
|-----------------------|---------------------------------|---------------------------------------------------------------------------------|
| **User Features**     | Registration and Authentication | Users can register with email, password, full name, qualification, and DOB. Secure login/logout functionality. |
|                       | Dashboard                      | Displays user information, available quizzes, and past scores.                   |
|                       | Quiz Attempt                   | Users can attempt active quizzes, submit answers, and view results with score percentage. |
|                       | Available Quizzes              | Lists all quizzes available for users to attempt.                               |
|                       | Score History                  | View quiz attempt history with quiz names, scores, and attempt dates.           |
|                       | Quiz Result                    | Detailed results of quiz attempts, showing correct and incorrect answers.        |
| **Admin Features**    | Admin Dashboard                | Overview of total users, active users, active quizzes, and recent quiz attempts. |
|                       | User Management                | Add, edit, and delete users; update details like email, password, and qualification. |
|                       | Subject Management             | Create, edit, and delete subjects.                                              |
|                       | Chapter Management             | Add, edit, and delete chapters within subjects; assign chapter numbers.         |
|                       | Question Management            | Add, edit, and delete questions for specific chapters with four options and a correct answer. |
|                       | Quiz Management                | Create, edit, delete quizzes; set properties like name, description, start/end time, duration, and max marks. |
|                       | Quiz Question Assignment       | Add questions to quizzes from the same chapter.                                 |
|                       | Quiz Status Toggle             | Toggle quiz status between active and inactive.                                 |
|                       | Quiz Preview                   | Preview quizzes to review associated questions.                                 |
|                       | Data Integrity                 | Deleting subjects, chapters, quizzes, or questions removes related data (scores, attempts, answers). |
| **Technical Features** | Role-Based Access Control      | Decorators (`admin_required`, `user_required`) restrict access based on roles.  |
|                       | Database                       | SQLite with SQLAlchemy ORM for models (users, admins, quizzes, questions, scores). |
|                       | Session Management             | Flask-Login for user sessions, with user type stored for role differentiation.  |
|                       | Error Handling                 | Robust error handling with flash messages for user feedback.                    |
|                       | Modular Structure              | Blueprints organize routes (`auth`, `user`, `admin`, `routes`) for clean code.  |


## Project Structure

```
QuizMaster/
├── app.py                # Main Flask application setup
├── run.py                # Entry point to run the application
├── extensions.py         # Flask extensions (SQLAlchemy, Migrate, LoginManager)
├── requirements.txt
├── controllers/
│   ├── auth.py           # Authentication routes (register, login, logout)
│   ├── user.py           # User-related routes (dashboard, quiz attempt, scores)
│   ├── admin.py          # Admin-related routes (manage users, subjects, quizzes)
│   ├── routes.py         # General routes (landing page)
│   └── decorators.py     # Custom decorators for role-based access
├── models/
│   ├── __init__.py
│   ├── user.py           # User model
│   ├── admin.py          # Admin model
│   ├── quiz.py           # Quiz, Question, Chapter, Subject models
│   ├── score.py          # Score model
├── templates/            # HTML templates for rendering pages
│   ├── users/            # User-specific templates
│   ├── admin/            # Admin-specific templates
│   ├── register.html
│   └── index.html        # Landing page
└── static/               # Static files (CSS, JS, images)

```

## Prerequisites

-   Python 3.8+
-   Git
-   Virtualenv (recommended)

## Setup Instructions

Follow these steps to set up and run the QuizMaster project locally.

### 1. Clone the Repository

```bash
git clone https://github.com/prakhar2507/Quiz-Master-v1.git
cd QuizMaster

```

### 2. Create a Virtual Environment

```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

```

### 3. Install Dependencies

Install the required Python packages using `pip`:

```bash
pip install -r requirements.txt

```

### 4. Initialize the Database

Run the following commands to set up the SQLite database:

```bash
flask db init
flask db migrate
flask db upgrade

```

### 5. Create an Admin Account

To create an admin account, you can manually add an admin to the database (not included in the provided code). In Terminal:

```bash
flask shell

```

```python
from models.admin import Admin
from werkzeug.security import generate_password_hash
admin = Admin(email="admin@example.com", password_hash=generate_password_hash("adminpassword"))
db.session.add(admin)
db.session.commit()

```

### 6. Run the Application

Start the Flask development server:

```bash
python run.py

```

The application will be available at `http://127.0.0.1:5000`.

### 7. Access the Application

-   **Landing Page**: Navigate to `http://127.0.0.1:5000/` to access the main page.
-   **User Login**: Go to `/user-login` to log in as a user.
-   **Admin Login**: Go to `/admin-login` to log in as an admin.
-   **Register**: New users can register at `/register`.

## Usage

-   **Users**:
    -   Register and log in to access the dashboard.
    -   Browse available quizzes, attempt active quizzes, and view results/scores.
-   **Admins**:
    -   Log in to access the admin dashboard.
    -   Manage users, subjects, chapters, questions, and quizzes via the respective management pages.

## Contributing

1.  Fork the repository.
2.  Create a new branch (`git checkout -b feature-branch`).
3.  Make your changes and commit (`git commit -m "Add feature"`).
4.  Push to the branch (`git push origin feature-branch`).
5.  Open a pull request.

## License

This project is licensed under the MIT License. See the LICENSE file for details.
