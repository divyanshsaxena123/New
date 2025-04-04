# New
teaching_website/
│
├── static/
│   └── style.css
│
├── templates/
│   ├── base.html
│   ├── home.html
│   ├── courses.html
│   ├── about.html
│   ├── contact.html
│   ├── login.html
│   └── signup.html
│
├── app.py
└── requirements.txtfrom flask import Flask, render_template, redirect, url_for

app = Flask(__name__)

@app.route('/')
def home():
    return render_template('home.html')

@app.route('/courses')
def courses():
    return render_template('courses.html')

@app.route('/about')
def about():
    return render_template('about.html')

@app.route('/contact')
def contact():
    return render_template('contact.html')

@app.route('/login')
def login():
    return render_template('login.html')

@app.route('/signup')
def signup():
    return render_template('signup.html')

if __name__ == '__main__':
    app.run(debug=True)app.run<!DOCTYPE html>
<html>
<head>
    <title>{% block title %}Teaching Website{% endblock %}</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}">
</head>
<body>
    <nav>
        <a href="/">Home</a>
        <a href="/courses{% extends "base.html" %}
{% block title %}Home - Teaching Website{% endblock %}
{% block content %}
    <h1>Welcome to Our Teaching Platform</h1>
    <p>Learn anytime, anywhere with expert-led courses.</p>
{% endblock %}body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
}

nav {
    background-color: #333;
    padding: 10px;
}

nav a {
    color: white;
    margin: 0 15px;
    text-decoration: none;
}

nav a:hover {
    text-decoration: underline;
}

main {
    padding: 20px;
}00
{% extends "base.html" %}
{% block content %}
<h2>Sign Up</h2>
<form method="post">
    <input type="text" name="username" placeholder="Username" required><br>
    <input type="password" name="password" placeholder="Password" required><br>
    <button type="submit">Sign Up</button>
</form>
{% endblock %}from flask import Flask, render_template, redirect, url_for, request, flash
from flask_sqlalchemy import SQLAlchemy
from flask_login import LoginManager, login_user, login_required, logout_user, UserMixin

app = Flask(__name__)
app.secret_key = 'secret123'
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///users.db'
db = SQLAlchemy(app)

login_managerpip install -r requirements.txtrequirements.txtflask
flask_sqlalchemy
flask_loginbody {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
}

nav {
    background-color: #333;
    padding: 10px;
}

nav a {
    color: white;
    margin: 0 15px;
    text-decoration: none;
}

nav a:hover {
    text-decoration: underline;
}

main {
    padding: 20px;
}
{% if current_user.is_authenticated %}
    <a href="/dashboard">Dashboard</a>
    <a href="/logout">Logout</a>
{% else %}
    <a href="/login">Login</a>
{% endif %}{% extends "base.html" %}
{% block content %}
<h2>Your Courses</h2>
<form method="post" action="{{ url_for('add_course') }}">
    <input type="text" name="title" placeholder="Course Title" required><br>
    <class Course(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    title = db.Column(db.String(150), nullable=False)
    description = db.Column(db.String(300))
    user_id = db.Column(db.Integer, db.ForeignKey('user.id'))

@app.route('/dashboard')
@login_required
def dashboard():
    courses = Course.query.filter_by(user_id=current_user.id).all()
    return render_template('dashboard.html', courses=courses)

@app.route('/add_course', methods=['POST'])
@login_required
def add_course():
    title = request.form['title']
    description = request.form['description']
    new_course = Course(title=title, description=description, user_id=current_user.id)
    db.session.add(new_course)
    db.session.commit()
    return redirect(url_for('dashboard'))

@app.route('/delete_course/<int:course_id>')
@login_required
def delete_course(course_id):
    course = Course.query.get_or_404(course_id)
    if course.user_id == current_user.id:
        db.session.delete(course)
        db.session.commit()
    return redirect(url_for('dashboard'))user.idcurrent_user.id{% extends "base.html" %}
{% block content %}
<h2>Sign Up</h2>
<form method="post">
    <input type="text" name="username" placeholder="Username" required><br>
    <input type="password" name="password" placeholder="Password" required><br>
    <button type="submit">Sign Up</button>
</form>
{% endblock %}from flask import Flask, render_template, redirect, url_for, request, flash
from flask_sqlalchemy import SQLAlchemy
from flask_login import LoginManager, login_user, login_required, logout_user, UserMixin

