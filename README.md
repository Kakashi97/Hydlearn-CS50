# HydLearn
#### Video Demo:  <https://youtu.be/Tbf9K4GRyFQ>
#### Description:


Hydlearn is a simple e-learning website developed as part of the final project for **CS50’s Introduction to Computer Science** course. It is designed to bring together learners and instructors to share knowledge related to the hydraulic and water engineering field. The website allows instructors to create and manage courses, while learners can enroll in these courses, access materials, and interact with instructors.


## Table of Contents

- [Features](#features)
- [Technologies Used](#technologies-used)
- [Installation](#installation)
- [Project Structure](#project-structure)
- [Database Schema](#database-schema)
- [Routes](#routes)


## Features

- **User Authentication:** login and registration for both learners and instructors.
- **Role-based Access:** Different functionalities and pages for learners and instructors.
- **Course Management:** Instructors can create, update, and delete courses.
- **Enrollment System:** Learners can enroll in courses and access course materials.
- **Responsive Design:** Built with Bootstrap to ensure compatibility across different devices and screen sizes.
- **Forums:** Users can create posts and comments with styled text and images.

## Technologies Used

- **Frontend:**
  - HTML
  - CSS
  - JavaScript
  - Bootstrap

- **Backend:**
  - Flask

- **Database:**
  - SQLite3

## Installation

To run this project locally, follow these steps:

1. **Clone the repository:**

    ```bash
    git clone https://github.com/kakashi97/hydlearn.git
    ```

2. **Navigate to the project directory:**

    ```bash
    cd hydlearn
    ```

3. **Create a virtual environment:**

    ```bash
    python3 -m venv venv
    ```

4. **Activate the virtual environment:**

    - On macOS/Linux:

        ```bash
        source venv/bin/activate
        ```

    - On Windows:

        ```bash
        venv\Scripts\activate
        ```

5. **Install the required packages:**

    ```bash
    pip install -r requirements.txt
    ```

6. **Set up the database:**

    ```bash
    flask db init
    flask db migrate
    flask db upgrade
    ```

7. **Run the application:**

    ```bash
    flask run
    ```


## Project Structure

The project follows a standard Flask application structure, with the main components being:
```
Hydlearn/
├── app.py
├── helpers.py
├── templates/
│ ├── layout.html
│ ├── index.html
│ ├── register.html
│ ├── login.html
│ ├── home.html
│ ├── home_instructor.html
│ ├── courses.html
│ ├── course.html
│ ├── forums.html
│ ├── post.html
│ ├── apology.html
├── static/
│ ├── css/
├── uploads/
├── requirements.txt
├── README.md
├── database.db
```


### `layout.html`

The `layout.html` file serves as the base template for all pages in the HydLearn website. It includes the following key components:

- **Meta tags:** Sets the character encoding and viewport for the page.
- **Bootstrap and custom CSS:** Links to Bootstrap and a custom `styles.css` file for styling.
- **Block placeholders:** `{% block %}` tags are used to define areas where content from other templates can be inserted.
- **Navigation bar:** Includes links to the home page, courses, and forums. The navigation bar changes based on whether a user is logged in or not.
- **User authentication:** Shows different options in the navigation bar based on whether the user is logged in or not.
- **Main content area:** `{% block main %}` is used to insert the main content of each page.
- **Bootstrap JavaScript:** Includes the Bootstrap JavaScript bundle for interactive elements.

By using this layout, the website maintains a consistent look and feel across all pages while allowing for dynamic content insertion through Flask's template rendering.

### `index.html`

The `index.html` file is the homepage of the HydLearn website. It extends the `layout.html`and includes the following key components:

- **Carousel:** The homepage features a carousel with three slides, each highlighting a different aspect of HydLearn. The carousel allows users to navigate between slides and includes buttons for quick access to different sections of the website.
- **Dynamic Content:** Each slide contains dynamic content, such as headings, descriptions, and call-to-action buttons, to engage users and encourage them to explore the website further.

By using this layout, the homepage provides an attractive and informative introduction to HydLearn, helping users understand the benefits of the platform and encouraging them to take action.

### `register.html`

The `register.html` file is the registration page for new users. It extends the `layout.html` file and includes the following key components:

- **Sign Up Form:** Allows users to enter their full name, email address, select their account type (learner or instructor), and choose a password. The form includes validation to ensure that all fields are filled out correctly before submission.
- **Terms of Use:** Includes a checkbox for users to agree with the Terms of Use and Privacy Policy before signing up. (It's not implemented)
- **Already have an account:** Provides a link for users who already have an account to log in instead of registering again.

By using this layout, the registration page provides a simple and user-friendly way for new users to sign up for an account on the HydLearn website.

### `login.html`

The `login.html` file is the login page for existing users. It extends the `layout.html` file and includes the following key components:

- **Sign In Form:** Allows users to enter their email address and password to log in to their account. The form includes validation to ensure that both fields are filled out correctly before submission.
- **Don't have an account:** Provides a link for users who do not have an account to sign up for one.

### `apology.html`

The `apology.html` file is used to display an apology message or an error message to users on the HydLearn website. It extends the `layout.html` file and includes the following key components:

- **Message Display:** The main content of the page includes a message (e.g., an apology or an error message) that is passed to the template when rendering the page. This message is displayed prominently to users.

- **Code Display:** Additionally, the page may display an error code or other relevant information to help users understand the nature of the issue.

### `home_instructor.html`

The `home_instructor.html` file is a specific page for instructors after they have logged in. It extends the `layout.html` file  and includes the following key components:

- **Upload New Course Form:** Allows instructors to upload a new course to the website. The form includes fields for the course title, description, lecture file (PDF), and preview image.
- **Uploaded Courses Section:** Displays a list of courses uploaded by the instructor. Each course is displayed as a card with the course title, description, and preview image. 
  - **Edit and Delete Buttons:** Each course card includes buttons to edit or delete the course. These buttons open modal dialogs for editing or confirming deletion of the course.
  - **Edit Course Modal:** Allows instructors to edit the title, description, lecture file, or preview image of a course. The modal includes form fields for each of these properties.
  - **Delete Course Modal:** Asks for confirmation before deleting a course. If confirmed, the course is deleted from the database.

### `home.html`

The `home.html` file is a specific page for learners after they have logged in. It extends the `layout.html` file and includes the following key components:

- **Courses List:** Displays a list of courses available for enrollment. Each course is displayed as a card with the course title, description, and preview image.
  - **Remove Button:** Allows learners to remove a course from their list. Clicking the button opens a modal dialog for confirmation before removing the course.

### `courses.html`

The `courses.html` file displays a list of available courses on the HydLearn website. It extends the `layout.html` file and includes the following key components:

- **Course Cards:** Each course is represented as a card, displaying the course title, description, and instructor name. Learners can click on a course card to view more details about the course.
- **Add to List Button:** For learners, there is an option to add a course to their list of enrolled courses. If a course is already in their list, the button is disabled to prevent duplicate enrollments.
- **View Button:** For instructors, there is a "View" button that allows them to view the course details without enrolling.

### `course.html`

The `course.html` file displays the content of a specific course on the HydLearn website. It extends the `layout.html` file and includes the following key components:

- **Embedded PDF Viewer:** The main content of the page is an embedded PDF viewer that displays the course materials. Users can view the course content directly on the HydLearn website without needing to download the PDF file.

### `forum.html`
The `forum html` file is used to display a forum page where users can start new discussions and view existing posts. It extends the `layout.html` file and includes the following key components:

- **New Discussion Form:** Users can use the form at the top of the page to start a new discussion. The form includes fields for entering a title and content for the new post.

- **Existing Posts:** Below the new discussion form, existing posts are displayed. Each post includes the title, author's name, and date of the post. Users can click on a post to view its full content.

- **Quill Editor:** The form includes a Quill editor for entering the content of new discussions. This editor provides a rich text editing experience, allowing users to format their posts using various styles and options.

- **JavaScript Functions:** The page includes JavaScript functions to initialize the Quill editor, handle form submissions, and format dates for display. 

### `post.html`
The `post.html` file is used to display a single post along with its comments on the HydLearn forums. It extends the `layout.html` fileand includes the following key components:

- **Post Display:** The main content of the page includes the title and content of the post. The post content is rendered using the Quill rich text editor to allow for formatting and styling.

- **Comment Section:** Below the post, the page displays a section for comments. Each comment is displayed with the user's name, the comment message, and the date of the comment. Users can add new comments using the Quill editor.

- **Quill Editor:** The page includes the Quill rich text editor for adding comments. The editor provides options for formatting text, adding links, and inserting images.

- **Script Initialization:** The page includes a script to initialize the Quill editor and handle the submission of new comments. The script ensures that the comment content is properly formatted before submission.


## Database Schema

The database for Hydlearn is managed using SQLite3. Below is the schema used for the database:

```sql
CREATE TABLE users (
   id INTEGER PRIMARY KEY,
   name TEXT NOT NULL,
   email TEXT NOT NULL,
   role TEXT NOT NULL,
   password_hash TEXT NOT NULL
);

CREATE TABLE courses (
   id INTEGER PRIMARY KEY AUTOINCREMENT,
   title TEXT NOT NULL,
   description TEXT,
   instructor_id INTEGER NOT NULL,
   lecture_file BLOB,
   preview BLOB,
   FOREIGN KEY (instructor_id) REFERENCES users(id)
);

CREATE TABLE course_enrollments (
   id INTEGER PRIMARY KEY AUTOINCREMENT,
   learner_id INTEGER NOT NULL,
   course_id INTEGER NOT NULL,
   enrollment_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
   UNIQUE(learner_id, course_id),
   FOREIGN KEY (learner_id) REFERENCES users(id),
   FOREIGN KEY (course_id) REFERENCES courses(id)
);

CREATE TABLE Posts (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    title TEXT NOT NULL,
    user_id INTEGER NOT NULL,
    content TEXT NOT NULL,
    FOREIGN KEY (user_id) REFERENCES users(id)
);

CREATE TABLE Comments (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    user_id INTEGER NOT NULL,
    post_id INTEGER NOT NULL,
    date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    message TEXT NOT NULL,
    visibility TEXT CHECK(visibility IN ('deleted', 'visible', 'hidden')) DEFAULT 'visible',
    FOREIGN KEY (user_id) REFERENCES users(id),
    FOREIGN KEY (post_id) REFERENCES Posts(id)
);
```

## Routes

Below is a description of the main routes used in the application:

- **`/`**: Home page, displays different views for instructors and learners.
- **`/register`**: Registration page for new users.
- **`/login`**: Login page for existing users.
- **`/logout`**: Logs out the current user.
- **`/courses`**: Displays available courses in a card format. Learners can enroll, and instructors can see the instructor name for each course.
- **`/forums`**: Forum page where users can create posts and comment on them.
- **`/post/<id>`**: View and comment on a specific post.
- **`/list/<id>`**: Enroll in a course.
- **`/unlist/<id>`**: Unenroll from a course.
- **`/course/<id>`**: View details of a specific course.
- **`/upload`**: Upload new course materials (instructor only).
- **`/delete/<title>`**: Delete a course (instructor only).
- **`/edit/<id>`**: Edit course details (instructor only).
- **`/view_pdf/<id>`**: View a PDF file associated with a course.
