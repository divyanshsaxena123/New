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
