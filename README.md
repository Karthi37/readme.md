# readme.md
Frontend (HTML and JavaScript):
You'll need to create an HTML form to capture the input fields from the user. Here's a simplified example:
<!DOCTYPE html>
<html>
<head>
    <title>Student Enrollment Form</title>
</head>
<body>
    <form id="enrollmentForm">
        <label for="rollNo">Roll No:</label>
        <input type="text" id="rollNo" name="rollNo" required><br>

        <label for="fullName">Full Name:</label>
        <input type="text" id="fullName" name="fullName" required><br>

        <label for="class">Class:</label>
        <input type="text" id="class" name="class" required><br>

        <label for="birthDate">Birth Date:</label>
        <input type="date" id="birthDate" name="birthDate" required><br>

        <label for="address">Address:</label>
        <input type="text" id="address" name="address" required><br>

        <label for="enrollmentDate">Enrollment Date:</label>
        <input type="date" id="enrollmentDate" name="enrollmentDate" required><br>

        <button type="submit">Save</button>
        <button type="button" onclick="resetForm()">Reset</button>
    </form>

    <script>
        function resetForm() {
            document.getElementById("enrollmentForm").reset();
        }
    </script>
</body>
</html>
Backend (Server and Database):
For the backend, you'll need a server-side language (like Python, Node.js, PHP, etc.) and a database (such as MySQL, PostgreSQL, etc.). Here's a conceptual example using Node.js and MySQL:

#npm install express mysql

const express = require('express');
const mysql = require('mysql');
const app = express();

const db = mysql.createConnection({
    host: 'localhost',
    user: 'your_db_user',
    password: 'your_db_password',
    database: 'SCHOOL_DB'
});

db.connect((err) => {
    if (err) throw err;
    console.log('Connected to the database');
});

app.use(express.urlencoded({ extended: false }));
app.use(express.json());

app.post('/enroll', (req, res) => {
    const { rollNo, fullName, class, birthDate, address, enrollmentDate } = req.body;
    const query = 'INSERT INTO STUDENT_TABLE (RollNo, FullName, Class, BirthDate, Address, EnrollmentDate) VALUES (?, ?, ?, ?, ?, ?)';
    db.query(query, [rollNo, fullName, class, birthDate, address, enrollmentDate], (err, result) => {
        if (err) {
            console.error(err);
            res.status(500).send('Error saving data');
        } else {
            console.log('Data saved successfully');
            res.status(200).send('Data saved successfully');
        }
    });
});

app.listen(3000, () => {
    console.log('Server is running on port 3000');
});
