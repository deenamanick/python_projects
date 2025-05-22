# Django Single Page Login App**

- A minimalist Django web application that loads a single login page at the root URL (`/`).

- Useful as a boilerplate for beginners learning Django's structure and routing.

- Perfect for beginners learning Django’s **MVT (Model-View-Template)** architecture or for setting up a base login UI to extend with authentication.


**🚀Features**

- Django 5+ compatible  
- Simple and clean login form  
- Easy project structure  
- Great starting point for adding authentication  


**📦 Tech Stack**
- Python 3.10+  
- Django 5.x  
- HTML5, CSS (customizable)



Here is a step by step process:

**🧰 Setup Instructions**

**🔹 1. Clone the Repository**
- bash
```
git clone https://github.com/deenamanick/python_projects.git
cd python_projects.git
```

**🔹 2. Create and Activate Virtual Environment**
**✅ Windows**
- bash
```
python -m venv venv
venv\Scripts\activate
```

**✅ macOS/Linux**
- bash
```
python3 -m venv venv
source venv/bin/activate
```

**🔹 3. Install Dependencies**
- bash
```
pip install django

```

**🔹 4. Create Django Project and App**
If you're starting from scratch:

- bash
```
django-admin startproject login_project .
python manage.py startapp login_app
```

**🔹 5. Configure settings.py**

- Add 'login_app' to INSTALLED_APPS
- Add import os

- python
```
'DIRS': [os.path.join(BASE_DIR, 'login_app', 'templates')],
```

**🔹 6. Set Up URLs**

- login_project/urls.py

- python
```
from django.contrib import admin
from django.urls import path, include  # ✅ include is important

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('login_app.urls')),  # root URL to login_app
]

```
- login_app/urls.py
- python
```
from django.urls import path
from . import views

urlpatterns = [
    path('', views.login_view, name='login'),
]
```

**🔹 7. Create the View**
- login_app/views.py

- python
```
from django.shortcuts import render

def login_view(request):
    return render(request, 'login.html')
```

**🔹 8. Create the Template**
- login_app/templates/login.html

- html
```
<!DOCTYPE html>
<html>
<head>
    <title>Login</title>
</head>
<body>
    <h2>Login Page</h2>
    <form method="post">
        {% csrf_token %}
        <label>Username:</label><br>
        <input type="text" name="username"><br><br>

        <label>Password:</label><br>
        <input type="password" name="password"><br><br>

        <button type="submit">Login</button>
    </form>
</body>
</html>
```

**🔹 9. Run Migrations**
- bash
```
python manage.py makemigrations
python manage.py migrate
```

🔹 10. Run the Server
- bash
```
python manage.py runserver
```


**Visit:**
👉 http://127.0.0.1:8000/

You should see your login page!


**📌 Notes**
- No login logic (like authentication) is implemented — just a static form.

- Extend it by integrating Django's built-in User model and authentication views.


**Author
IvanMaxwell
GitHub**


