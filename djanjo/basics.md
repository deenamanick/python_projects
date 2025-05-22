**Project Idea :Online Learning Portal** --- In Progress Currenlty on hold
 
- A simple E-learning platform for students with Admin, Teacher, and Student roles using python.

- This app will have multiple functionalities split across different Django apps.

🧠 **What Is Django?**

- Django is a tool (framework) that helps you build websites and web applications using the Python programming language.

- Think of Django like Lego blocks — it gives you pieces that you can combine to make websites faster and more securely


🧠**What is git bash**

- It's is an application for Microsoft Windows environments which provides an emulation layer for a Git command line experience

- Bash is an acronym for Bourne Again Shell. A shell is a terminal application used to interface with an operating system through written commands.

🚀**Project Overview:**

- A beginner-friendly Django-based online learning portal with:

- User roles (Admin, Teacher, Student)

- Course management

- Quiz module

- Modular architecture using multiple Django apps

🛠**Key Features**

1.User Roles: Admin, Teacher, Student

2.Course Listing: Add/view courses with description and PDFs/videos

3.Enroll System: Students can enroll in courses

4.Quiz Module: Each course has related quizzes

5.Result System: View quiz scores instantly

6.Responsive UI using Bootstrap in static folder

**🗂️Apps Breakdown:**

**1.app_A → users:**

- Handles user registration, login, roles (Student/Teacher/Admin).
- User profile page.

**2.app_B → courses:**

- Teachers can create and manage courses.
- Students can view course lists, enroll, and access course content.

**3.app_C → quizzes:**

- Teachers can create quizzes for each course.
- Students can take quizzes and view scores.

![image](https://github.com/user-attachments/assets/249ee7c1-a003-4008-a894-468b0d342949)



**📁 Other Folders in the Structure

**0.config:**

Contains your Django settings, URL routing, and WSGI/ASGI configs.

**1.static:**

CSS, JavaScript, and image files (site styling, logos, etc.).

**2.templates:**

Common base HTML templates, course pages, quiz forms, login/signup.

**3.manage.py:**

Django's main CLI tool to run server, migrations, etc.

**4.db.sqlite3:**

Default development database.

**5.requirements.txt:**

List of all dependencies like


![image](https://github.com/user-attachments/assets/c428e297-8a70-467a-8f17-115efa4950a2)


**HERE IS AN STEP-BY-STEP PROCEDURE FOR THE PROJECT:**


**✅0. Install Python and Django**

- Before you start, make sure Python is installed on your computer.

- Check Python:
Open your terminal or command prompt and type:
```
In bash
python --version
```
- If Python is installed, it will show a version like Python 3.10.x.

- If not,https://www.python.org/downloads/windows/

- If the python isn't available in the terminal then, 

- go check path, here are the steps to do,

**step1;** Go to Start and enter advanced system settings in the search bar.

**step2;** Click View advanced system settings.

**step3;** In the System Properties dialog, click the Advanced tab and then click Environment Variables.

**Depending on your installation:**
**case1:**

- If you selected Install for all users during installation, select Path from the list of System Variables and click Edit.

**case2:**


- If you didn’t select Install for all users during installation, select Path from the list of User Variables and click Edit.
Click New and enter the Python directory path, then click OK until all the dialogs are closed.

**Step 4 ;** Verify the Python Installation


- You can verify whether the Python installation is successful either through the command line or through the Integrated Development Environment (IDLE) application, if you chose to install it.

- Go to Start and enter cmd in the search bar. Click Command Prompt.

**Enter the following command in the command prompt:**

```
In bash or terminal in vscode
python --version
```
for more referance on how to install python refer this web, https://www.digitalocean.com/community/tutorials/install-python-windows-10

**✅1.Install django and create a folder**

**First, create a project folder,**
```
mkdir jeevi_academy
cd jeevi_academy
```

**Then create a virtual environment**(this keeps your project files clean):
```
python -m venv venv
```

**Activate the virtual environment:**

**Windows:**

- In bash,
```
venv\Scripts\activate
```
**Mac/Linux:**

- In bash,
```
source venv/bin/activate
```
**Then install Django:**

- In bash
```
pip install django
```

**✅ 2. Start Your Django Project**


**Create the base project**(called config):

- In bash
  
```
django-admin startproject config .
```

The dot (.) at the end puts files in the current folder.

**You’ll now see files like:**

- manage.py – the main controller for your app

- config/ – where settings are stored

**✅ 3. Start Django Apps**

Apps are like “modules” or “sections” of your website.

**For Jeevi Academy, create three apps:**

- In bash
```
python manage.py startapp users     # For login/register
python manage.py startapp courses   # For course content
python manage.py startapp quizzes   # For quizzes
```
**✅ 4. Tell Django to Use Your Apps**

In config/settings.py, find the INSTALLED_APPS section and add your apps:

- In python
```
INSTALLED_APPS = [
    'users',
    'courses',
    'quizzes',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```
**✅ 5. Run the Server**
This will start your web app locally:

- In bash
```
python manage.py runserver
```
Now visit http://127.0.0.1:8000 in your browser — you’ll see Django’s welcome page 🎉

**✅ Step 6: Use a Custom User Model**
Django has a built-in user system, but we’ll customize it to add a “role.”

 In users/models.py, paste this code:

- python
```
from django.contrib.auth.models import AbstractUser
from django.db import models

class User(AbstractUser):
    ROLE_CHOICES = (
        ('student', 'Student'),
        ('teacher', 'Teacher'),
    )
    role = models.CharField(max_length=10, choices=ROLE_CHOICES, default='student')

    def __str__(self):
        return self.username
```
📝 This code:

Replaces the default user model.

Adds a role field (Student or Teacher).

**✅ Step 7: Tell Django to Use This Model**
In config/settings.py, add:

- python
```
AUTH_USER_MODEL = 'users.User'
```
**✅ Step 8: Create a Register Form**
📁 Create a file: users/forms.py
Add this:

- python
```
from django import forms
from django.contrib.auth.forms import UserCreationForm
from .models import User

class CustomUserCreationForm(UserCreationForm):
    class Meta:
        model = User
        fields = ['username', 'email', 'role', 'password1', 'password2']
```
**✅ Step 9: Create the Register View**

In users/views.py, add:

- python
```
from django.shortcuts import render, redirect
from .forms import CustomUserCreationForm
from django.contrib.auth import login

def register(request):
    if request.method == 'POST':
        form = CustomUserCreationForm(request.POST)
        if form.is_valid():
            user = form.save()
            login(request, user)
            return redirect('home')
    else:
        form = CustomUserCreationForm()
    return render(request, 'users/register.html', {'form': form})
```
**✅ Step 10: Add URLs**
📁 Create a file: users/urls.py

- python
```
from django.urls import path
from . import views

urlpatterns = [
    path('register/', views.register, name='register'),
]
In config/urls.py:

- python

from django.urls import path, include

urlpatterns = [
    path('users/', include('users.urls')),
]
```
**✅ Step 11: Create the HTML Template**
📁 Create: templates/users/register.html

- html
```
{% extends "base.html" %}
{% load crispy_forms_tags %}

{% block content %}
  <h2>Register</h2>
  <form method="post">
    {% csrf_token %}
    {{ form|crispy }}
    <button type="submit">Register</button>
  </form>
{% endblock %}
```
**✅ Step 12: Make Migrations**
In the terminal, run:

- bash
```
python manage.py makemigrations
python manage.py migrate
```
**✅ Step 13: Install crispy-forms** (for nice form styles)
- bash
```
pip install django-crispy-forms crispy-bootstrap5
```
Then update settings.py:

- python
```
INSTALLED_APPS += ['crispy_forms', 'crispy_bootstrap5']
CRISPY_ALLOWED_TEMPLATE_PACKS = "bootstrap5"
CRISPY_TEMPLATE_PACK = "bootstrap5"
```
**✅ Step 14: Course Model**
In courses/models.py:

- python
```
from django.db import models
from users.models import User

class Course(models.Model):
    title = models.CharField(max_length=200)
    description = models.TextField()
    teacher = models.ForeignKey(User, on_delete=models.CASCADE)

    def __str__(self):
        return self.title
```
**✅ Step 15: Admin Setup**
In courses/admin.py:

- python
```
from django.contrib import admin
from .models import Course

admin.site.register(Course)
```
**✅ Step 16: Course Form**
In courses/forms.py:

- python
```
from django import forms
from .models import Course

class CourseForm(forms.ModelForm):
    class Meta:
        model = Course
        fields = ['title', 'description']
```
**✅ Step 17: Views to Add and List Courses**
In courses/views.py:

- python
```
from django.shortcuts import render, redirect
from .forms import CourseForm
from .models import Course
from django.contrib.auth.decorators import login_required

@login_required
def add_course(request):
    if request.user.role != 'teacher':
        return redirect('course_list')

    if request.method == 'POST':
        form = CourseForm(request.POST)
        if form.is_valid():
            course = form.save(commit=False)
            course.teacher = request.user
            course.save()
            return redirect('course_list')
    else:
        form = CourseForm()
    return render(request, 'courses/add_course.html', {'form': form})

def course_list(request):
    courses = Course.objects.all()
    return render(request, 'courses/course_list.html', {'courses': courses})
```
**✅ Step 18: Templates**
1.templates/courses/add_course.html:

- html
```
{% extends "base.html" %}
{% block content %}
<h2>Add Course</h2>
<form method="post">
  {% csrf_token %}
  {{ form|crispy }}
  <button type="submit">Add</button>
</form>
{% endblock %}
```
2.templates/courses/course_list.html:

- html
```
{% extends "base.html" %}
{% block content %}
<h2>Courses</h2>
<ul>
  {% for course in courses %}
    <li>{{ course.title }} by {{ course.teacher.username }}</li>
  {% endfor %}
</ul>
{% endblock %}
```
**✅ Step 19: Add URLs**
courses/urls.py:

- python
```
from django.urls import path
from . import views

urlpatterns = [
    path('add/', views.add_course, name='add_course'),
    path('', views.course_list, name='course_list'),
]

```
And in config/urls.py:

- python
```
path('courses/', include('courses.urls')),
```
**✅ Step 20: Create Models**
In quizzes/models.py, define two models:

- Question – a question that belongs to a course

- Choice – the answer options for the question

- python
```
from django.db import models
from courses.models import Course

class Question(models.Model):
    course = models.ForeignKey(Course, on_delete=models.CASCADE)
    text = models.TextField()

    def __str__(self):
        return self.text

class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    text = models.CharField(max_length=200)
    is_correct = models.BooleanField(default=False)

    def __str__(self):
        return self.text
```
**✅ Step 21: Register in Admin**
In quizzes/admin.py:

- python
```
from django.contrib import admin
from .models import Question, Choice

admin.site.register(Question)
admin.site.register(Choice)
```

Now run:

- bash
```
python manage.py makemigrations
python manage.py migrate
```
**✅ Step 22: Add Quiz Forms**
In quizzes/forms.py:

- python
```
from django import forms
from .models import Question, Choice

class QuestionForm(forms.ModelForm):
    class Meta:
        model = Question
        fields = ['course', 'text']

class ChoiceForm(forms.ModelForm):
    class Meta:
        model = Choice
        fields = ['question', 'text', 'is_correct']
```

**✅ Step 23: Create Views**
In quizzes/views.py:

- python
```
from django.shortcuts import render, redirect
from .models import Question, Choice
from .forms import QuestionForm, ChoiceForm
from courses.models import Course

# Teachers add questions
def add_question(request):
    if request.method == 'POST':
        form = QuestionForm(request.POST)
        if form.is_valid():
            form.save()
            return redirect('question_list')
    else:
        form = QuestionForm()
    return render(request, 'quizzes/add_question.html', {'form': form})

# Teachers add choices
def add_choice(request):
    if request.method == 'POST':
        form = ChoiceForm(request.POST)
        if form.is_valid():
            form.save()
            return redirect('question_list')
    else:
        form = ChoiceForm()
    return render(request, 'quizzes/add_choice.html', {'form': form})

# Students take quiz
def take_quiz(request, course_id):
    questions = Question.objects.filter(course_id=course_id)
    if request.method == 'POST':
        score = 0
        total = 0
        for question in questions:
            selected = request.POST.get(str(question.id))
            if selected:
                choice = Choice.objects.get(id=selected)
                if choice.is_correct:
                    score += 1
                total += 1
        return render(request, 'quizzes/quiz_result.html', {
            'score': score, 'total': total
        })

    return render(request, 'quizzes/take_quiz.html', {
        'questions': questions
    })
```

**✅ Step 24: Create URLs**
In quizzes/urls.py:

- python
```
from django.urls import path
from . import views

urlpatterns = [
    path('add-question/', views.add_question, name='add_question'),
    path('add-choice/', views.add_choice, name='add_choice'),
    path('take/<int:course_id>/', views.take_quiz, name='take_quiz'),
]
And in config/urls.py:
```
- python
```
path('quizzes/', include('quizzes.urls')),
```

**✅ Step 25: Templates**

**1.add_question.html**

- html
```
{% extends "base.html" %}
{% load crispy_forms_tags %}
{% block content %}
<h2>Add Question</h2>
<form method="post">
  {% csrf_token %}
  {{ form|crispy }}
  <button type="submit">Save</button>
</form>
{% endblock %}

```




**2.add_choice.html**

- html
```
{% extends "base.html" %}
{% load crispy_forms_tags %}
{% block content %}
<h2>Add Choice</h2>
<form method="post">
  {% csrf_token %}
  {{ form|crispy }}
  <button type="submit">Save</button>
</form>
{% endblock %}
```



**3.take_quiz.html**

- html
```
{% extends "base.html" %}
{% block content %}
<h2>Quiz</h2>
<form method="post">
  {% csrf_token %}
  {% for question in questions %}
    <h4>{{ question.text }}</h4>
    {% for choice in question.choice_set.all %}
      <label>
        <input type="radio" name="{{ question.id }}" value="{{ choice.id }}">
        {{ choice.text }}
      </label><br>
    {% endfor %}
  {% endfor %}
  <button type="submit">Submit</button>
</form>
{% endblock %}
```

**4.quiz_result.html**

- html
```
{% extends "base.html" %}
{% block content %}
<h2>Result</h2>
<p>Your Score: {{ score }}/{{ total }}</p>
{% endblock %}
```
