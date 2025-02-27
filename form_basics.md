5.0 ﻿Django Form Basics
--------------------------------

Web/HTML Form

▪ Web Form is an online page.

▪ Enables users to input data.

▪ This data is subsequently transmitted to a server
for processing.

▪ Web forms emulate traditional paper documents
where users manually complete specific fields.

▪ They can encompass various elements.

▪ Text boxes, checkboxes, select options, and a submit
button, among others.

---------------------------------------------------------------

▪ In HTML, forms are wrapped within the <form> tag.

▪ When working with forms, it's essential to use either the
GET or POST HTTP methods.

    <body>
      <form action="/your-url/" method="post">
         <!-- input elements --/>
         <!-- submit button --/>
      </form>
    </body>

------------------------------------------------------------------
Django Forms
------------------------------------------------------------------

▪ Django offers a comprehensive set of tools and
libraries that.

▪ Allow developers to create forms using Python code.

▪ Support all features of HTML forms in a
Pythonic manner.

▪ Simplify and automate a significant portion of the
form creation and handling process.

---------------------------------------------------------------------
▪ The form fields in Django correspond to HTML form
<input> elements

    from django import forms
    
    
    class NameForm(forms.Form):
        name = forms.CharField(label='Your Name', max_length=50)
        <form action="/your-url/" method="post">
              <label for="name">Your name: </label>
               <input type="text" id="name" name="name" maxlength="50" required>
              <input type="submit" value="OK">
        </form>

---------------------------------------------------------
Django Form Class
---------------------------------------------------------

▪ The Django Form Class serves several key functions.

▪ Defines the form fields, specifying what data the
form will collect.

▪ Determines the behavior and appearance of
the form.

▪ Handles validation when the form is submitted,
ensuring the data meets the specified criteria.

---------------------------------------------------------
Creating Django Forms
---------------------------------------------------------

▪ To create a form in Django:

▪ Inherit from the Form class.

▪ Add the form fields:

    from django import forms
    
    class NameForm(forms.Form):
       name = forms.CharField(...)

▪ Form and Model classes share most field types and some
common arguments.

--------------------------------------------------------------
views.py

    from .forms import NameForm
    
    def add_new_name(request):
              if request.method == "GET":
                  form = NameForm()
              if request.method == "POST":
                  form = NameForm(request.POST)
                  if form.is_valid():
                  # do something with the data
                  # redirect to the desired page
     return render(request, "index.html", {"form": form})

-------------------------------------------------------------
▪ Create a template with the form

    index.html
    
    <body>
          <form method="post">
              {% csrf_token %}
              {{ form }}
              <button type="submit">Add</button>
          </form>
    </body>

------------------------------------------------------------
Django Form Fields
------------------------------------------------------------

▪ The crucial aspect of creating a form lies in
defining its fields.

▪ Each field incorporates custom validation logic.

▪ Fields can take common arguments.

▪ Some fields accept field-specific arguments.

--------------------------------------------------------------
Form Field Arguments
--------------------------------------------------------

▪ By default, each Field class in Django assumes that a value
is required.

▪ If you pass an empty value, it will raise a ValidationError.

▪ You have the option to specify that a field is not required.

    first_name = forms.CharField(required=False)

-----------------------------------------------------------
Django Widget
-----------------------------------------------------------

▪ It is Django's representation of an HTML input element.

▪ Widgets handle:

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Rendering of HTML

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Extraction of data

▪ Django automatically assigns default widgets:

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Based on the type of data

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Each form field has a corresponding built-in widget

▪ You can specify a different widget for a field:

&nbsp;&nbsp;&nbsp;&nbsp; ▪ By using the widget argument on the field definition

--------------------------------------------------------------
Django Widget Attributes
---------------------------------------------------------------

▪ Widgets in Django provide a way to specify HTML
attributes using Python code.

------------------------------------------------------------
The ModelForm Class
-------------------------------------------------------------

▪ In a database-driven application, there are instances
where the forms mirror the models.

▪ Field types are already specified in the model.

▪ Using the ModelForm can help prevent
redundant definitions.

▪ This approach automatically generates a form based
on a specific model.

------------------------------------------------------------
Form vs ModelForm
------------------------------------------------------------

▪ Form:

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Independent of a model

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Does not directly interact
with models

&nbsp;&nbsp;&nbsp;&nbsp; ▪ E.g., search form, contact form, subscription form

▪ ModelForm:

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Converts a model into a form

&nbsp;&nbsp;&nbsp;&nbsp;  ▪ Directly interacts with models
by adding or editing them

&nbsp;&nbsp;&nbsp;&nbsp; ▪ E.g., registration form, newsletter article form, blog post form

--------------------------------------------------------------
Create a Django Model Form
---------------------------------------------------------------
    forms.py
    
    from django import forms
    from .models import Name
    
    
    class NameForm(forms.ModelForm):
              class Meta:
                    model = Name
                    fields = 'all'
-------------------------------------
▪ Create a view with a corresponding URL path

    views.py
    
    from .forms import NameForm
    
    def add_new_name(request):
              if request.method == "GET":
                   form = NameForm()
              if request.method == "POST":
                   form = NameForm(request.POST)
                   if form.is_valid():
                         form.save()
                         # redirect to the desired page
     return render(request, "index.html", {"form": form})

▪ Create a template with the form

    index.html
    
    <body>
            <form method="post" action="{% url 'my-named-url' %}">
                {% csrf_token %}
                {{ form }}
                <button type="submit">Add</button>
            </form>
    </body>

---------------------------------------------------------------
Class Meta
---------------------------------------------------------------

▪ Similar to the Model, a ModelForm class contains
an inner Meta class with pre-defined options

▪ These Meta options control the behavior and
appearance of the form

▪ A comprehensive list of these options can be found
in Django's ModelFormOptions class, in its
init() method

-------------------------------------------------------------
Model Option
-------------------------------------------------------------

▪ When configuring a ModelForm, it's essential to specify the
model that will be used to generate the form

▪ This value should be set to the Model class itself, not an
instance of it

    from django import forms
    from .models import Name
    
    
    class NameForm(forms.ModelForm):
           class Meta:
                 model = Name
-------------------------------------------------------------
Fields Option

▪ It's crucial to explicitly define the fields that will be edited in
the form

▪ Failing to do so can potentially result in security vulnerabilities

▪ You can use all to include all fields from the model

    from django import forms
    from .models import Name
    
    
    class NameForm(forms.ModelForm):
         class Meta:
              model = Name
              fields = ['first_name', 'last_name']
-----------------------------------------------------------------------------
Exclude Option

▪ Frequently, it's more convenient to specify which fields should be excluded from the form

    from django import forms
    from .models import Name
    
    class NameForm(forms.ModelForm):
           class Meta:
              model = Name
              exclude = ['last_name'] 


-----------------------------------------------------------
Overriding the Default Fields
------------------------------------------------------------

▪ You have the flexibility to change the field type for the model

▪ Use the widgets option

▪ A dictionary mapping field names to widget classes/instances

    class CommentForm(forms.ModelForm):
            class Meta:
                ...
                widgets = {
                    'comment': Textarea(),
                }

▪ You can specify a different label for a field

▪ Use the labels option

▪ A dictionary mapping field names to strings

    class NameForm(forms.ModelForm):
          class Meta:
              ...
              labels = {
                  'first_name': 'Add Your First Name',
              }

▪ You can add help texts for fields

▪ Use the help_texts option

▪ A dictionary mapping field names to strings

    class EmailForm(forms.ModelForm):
        class Meta:
            ...
            help_texts = {
                  'email': 'Please, provide a valid email address',
            }















