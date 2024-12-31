2.0 ﻿Django Introduction
-----------------------------
What is Django?
-----------------------------

▪ *High-level Python Web Framework, known for its:*

▪ *Speed*

▪ *Security*

▪ *Scalability*

▪ *Open-source nature*

-----------------------------------
What is Framework?
-----------------------------------

▪ *A foundational structure or set of tools.*

▪ *Provides a pre-defined structure and
reusable components.*

▪ *Streamlines the development of software applications.*

▪ *Allows developers to focus on specific functionalities.*

▪ *Includes libraries, templates, and predefined patterns
helping developers to work efficiently and consistently.*

-----------------------------------------------
What is MVT?
-----------------------------------------------
&nbsp;&nbsp;&nbsp;&nbsp; ▪ <strong>MVT</strong> *stands for Model-View-Template.*


▪ <strong>Django</strong> *follows the MVT design pattern to develop
web applications.*

▪ <strong>Model</strong> - *defines the structure and behavior of data.*

▪ <strong>View</strong> – *receives an HTTP request and returns an
HTTP response.*

&nbsp;&nbsp;&nbsp;&nbsp; ▪ *Contains the application's business logic.*

▪ <strong>Template</strong> - *the presentation (front-end) layer.*

&nbsp;&nbsp;&nbsp;&nbsp; ▪ *Provides a convenient way to generate dynamic HTML
pages by using a special template syntax (DTL).*

-------------------------------------------------------
Django Application
-------------------------------------------------------

App vs Project

▪ <strong>Django App</strong>:                                        

&nbsp;&nbsp;&nbsp;&nbsp; ▪ *A Web application that does something - e.g., a small task app.*                                      

&nbsp;&nbsp;&nbsp;&nbsp; ▪ *An app can be in multiple projects.*   

▪ <strong>Django Project</strong>:

&nbsp;&nbsp;&nbsp;&nbsp; ▪ *A collection of configurations and apps for a particular website.*

&nbsp;&nbsp;&nbsp;&nbsp; ▪ *A project can contains multiple apps.*

------------------------------------------------------------
Creating a Django App
------------------------------------------------------------

    python mange.py startapp tasks

------------------------------------------------------------
Setting up a Database
------------------------------------------------------------

Psycopg2

&nbsp;&nbsp;&nbsp;&nbsp; ▪ <strong>PostgreSQL</strong> *database adapter for the Python programming language.*

Use the Psycopg2 module to:

&nbsp;&nbsp;&nbsp;&nbsp; ▪ *Connect to PostgreSQL.*

&nbsp;&nbsp;&nbsp;&nbsp; ▪ *Perform SQL queries and database operations.*

&nbsp;&nbsp;&nbsp;&nbsp; ▪ *It is an external module.*

----------------------------------------------------------------
Set up PostgreSQL

▪ *To configure our project to work with PostgreSQL, we need to
set it in the settings.py file.*

    DATABASES = {
        "default": {
            "ENGINE": "django.db.backends.postgresql",
            "NAME": "",
            "USER": "",
            "PASSWORD": "",
            "HOST": "",
            "PORT": "",
        }
    }

------------------------------------------------------------
Django Model
------------------------------------------------------------

▪ *Models represent your application's data.*

▪ *The essential fields and behaviors of the stored data.*

▪ *Each model maps to a single database table.*

▪ *Model is a Python class that subclasses
django.db.models.Model.*

▪ *Each attribute of the model represents a
database field.*

---------------------------------------------------------------
Activating Models
---------------------------------------------------------------

▪ *Use models to create a database schema for the app.*

▪ *Use migrations to apply changes and update the
database schema.*

&nbsp;&nbsp;&nbsp;&nbsp; ▪ *First, create migrations for the added model.*

    python manage.py makemigrations


&nbsp;&nbsp;&nbsp;&nbsp; ▪ *Next, apply those changes to the database.*
            
    python manage.py migrate


--------------------------------------------------------------------------
Django View
--------------------------------------------------------------------------

▪ *The views.py file contains view functions
or classes.*

▪ *Each view takes an HTTP request and returns an
HTTP response.*

▪ *Implements the business logic that needs to be
executed when a given URL is reached.*

▪ *The names of the functions are usually related to
the URL that is being reached.*

-----------------------------------------------------------------------------
Django app/urls.py
-----------------------------------------------------------------------------

▪ *In the urls.py file you configure which function or
logic should be executed when reaching a given URL.*

▪ *Each app should have its own urls.py file
example.*

▪ *The created urls.py file should be included in the
project's urls.py.*

▪ *Import the include() function and use it in the
urlpatterns list.*

---------------------------------------------------------------------------------
Django Admin Site
---------------------------------------------------------------------------------

▪ *It is a built-in admin interface.*

▪ *Trusted users can manage content on the site.*

▪ *One of the benefits of Django.*

<strong>[Access Django Admin Site]</strong>

▪ *First, create a superuser to log in with*

    python manage.py createsuperuser

▪ *Then, start the server and navigate to the admin site.*

-----------------------------------------------------------------------------------------
Make Models Visible
-----------------------------------------------------------------------------------------

▪ *Register all models in a special file in the app
called admin.py.*

    from django.contrib import admin
    from task.models import Task

    admin.site.register(Task) 

-------------------------------------------------------------------------------------------
Django Admin Benefits
-------------------------------------------------------------------------------------------

▪ *Easily manage (create, update, delete) the data stored
in the database.*

▪ *The form is automatically generated.*

--------------------------------------------------------------------------------------------
What is a Django Template?
--------------------------------------------------------------------------------------------

▪ *A text file, written in a special syntax that allows a
dynamic generation of HTML.*

▪ *Serves as a presentation layer in the Model-ViewTemplate (MVT) architecture.*

▪ *Uses a markup language known as Django Template Language (DTL), which extends the standard HTML.*

▪ *Plays a crucial role in separating the logic (handled by views) from the presentation.*

----------------------------------------------------------------------------------------------
Rendering a Template
----------------------------------------------------------------------------------------------

▪ *Instead of using HttpResponse, we can now use the <strong>render</strong>
function that will display the created templatе.*

-----------------------------------------------------------------------------------------------
Adding a Context
-----------------------------------------------------------------------------------------------

▪ *The render function accepts a context as
an argument.*

▪ <strong>Context</strong> - *It is a dictionary passed to the template and used
to display data dynamically.*













