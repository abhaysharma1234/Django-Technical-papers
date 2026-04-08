# Django Technical Paper

## Introduction
This document explains Django models, on_delete behavior, fields and validators, and core Python concepts like modules and classes. These are essential for backend development using Django.

## 1. Django Models File

The models.py file is used to define the structure of your database in Django. Each model represents a table, and each attribute represents a column.

### Example
    from django.db import models

    class Student(models.Model):
        name = models.CharField(max_length=100)
        age = models.IntegerField()

### Key Points
- Models map to database tables
- Fields map to columns
- Each model is a Python class
- Django ORM is used to interact with the database

## 2. What is on_delete=CASCADE?

on_delete is used to define what happens when a referenced object is deleted.

### CASCADE Behavior
When a parent object is deleted, all related child objects are also deleted automatically.

### Example
    class Course(models.Model):
        name = models.CharField(max_length=100)

    class Student(models.Model):
        course = models.ForeignKey(Course, on_delete=models.CASCADE)

### Explanation
- If a Course is deleted
- All Students linked to that course will also be deleted

### Other on_delete Options
- CASCADE → Delete related objects
- PROTECT → Prevent deletion
- SET_NULL → Set field to NULL
- SET_DEFAULT → Set default value
- DO_NOTHING → No action taken

## 3. Django Fields

Fields define the type of data stored in the database.

### Common Field Types
- CharField → Short text
- TextField → Long text
- IntegerField → Integer values
- FloatField → Decimal numbers
- BooleanField → True/False
- DateField → Date values
- DateTimeField → Date and time
- EmailField → Email validation
- URLField → URL validation
- FileField → File uploads
- ImageField → Image uploads
- ForeignKey → One-to-many relationship
- OneToOneField → One-to-one relationship
- ManyToManyField → Many-to-many relationship

### Example
    name = models.CharField(max_length=100)
    email = models.EmailField()
    created_at = models.DateTimeField(auto_now_add=True)

## 4. Validators in Django

Validators are used to enforce rules on model fields.

### Built-in Validators
- MaxValueValidator → Maximum value limit
- MinValueValidator → Minimum value limit
- MaxLengthValidator → Maximum length
- MinLengthValidator → Minimum length
- EmailValidator → Valid email format
- URLValidator → Valid URL format
- RegexValidator → Custom pattern matching

### Example
    from django.core.validators import MinValueValidator, MaxValueValidator

    age = models.IntegerField(validators=[MinValueValidator(18), MaxValueValidator(60)])

### Purpose
- Ensure valid data
- Prevent incorrect input
- Improve data integrity

## 5. Python Module vs Python Class

### What is a Python Module?
A module is a file containing Python code (functions, variables, classes).

#### Example
    # file: math_utils.py
    def add(a, b):
        return a + b

### Key Points
- A module is a .py file
- Used to organize code
- Can be imported

### What is a Python Class?
A class is a blueprint for creating objects.

#### Example
    class Car:
        def __init__(self, name):
            self.name = name

### Key Points
- Defines structure and behavior
- Used to create objects
- Supports OOP concepts

## Difference Between Module and Class

- Module → A file containing code
- Class → A blueprint inside a module
- Module is used for organization
- Class is used for object creation
- A module can contain multiple classes
- A class cannot contain modules
