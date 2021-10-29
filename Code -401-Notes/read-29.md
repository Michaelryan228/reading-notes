Django ships with a built-in User model for authentication and if you'd like a basic tutorial on how to implement log in, log out, sign up and so on see the Django Login and Logout tutorial for more.

However, for a real-world project, the official Django documentation highly recommends using a custom user model instead. This provides far more flexibility down the line so, as a general rule, always use a custom user model for all new Django projects.

But how to implement one? The official documentation example is not actually what many Django experts recommend using. There is a far easier yet still powerful approach to starting off new Django projects with a custom user model which I'll demonstrate here.

Setup
To start, create a new Django project from the command line. We need to do several things:

create and navigate into a dedicated directory called accounts for our code
install Django
make a new Django project called config
make a new app accounts
start the local web server
Here are the commands to run:

$ cd ~/Desktop
$ mkdir accounts && cd accounts
$ pipenv install django~=3.1.0
$ pipenv shell
(accounts) $ django-admin.py startproject config .
(accounts) $ python manage.py startapp accounts
(accounts) $ python manage.py runserver
Note that we did not run migrate to configure our database. It's important to wait until after we've created our new custom user model before doing so.

If you navigate to http://127.0.0.1:8000 you’ll see the Django welcome screen.