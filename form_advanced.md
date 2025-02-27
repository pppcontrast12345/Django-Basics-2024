7.0 Django Forms Advanced
------------------------------------------

Django Validators

▪ A validator is a function or class designed to assess.

&nbsp;&nbsp;&nbsp;&nbsp; ▪ whether a given value meets specified criteria.

▪ If the value satisfies all criteria, the validator does not
return anything.

▪ If any criteria are not met, it raises a ValidationError.

---------------------------------------------------------------
Django Validators Reusability
---------------------------------------------------------------

▪ You can efficiently reuse validation logic across
different types of fields in Django.

▪ This reusability extends to:

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Models: apply the same validation logic to fields.

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Forms: validation logic can be shared among fields.

&nbsp;&nbsp;&nbsp;&nbsp; ▪ ModelForms: reuse the same validation logic in the
context of a Django ModelForm.

---------------------------------------------------------------
Validating Forms
-------------------------------------------------------------

▪ Form validation occurs during the data cleaning
process in Django.

▪ Raises ValidationError and provides relevant
information about the error.

▪ The cleaned and normalized data is returned as a
Python object.

▪ Each form field is equipped with custom validation
logic tailored to its specific requirements.

---------------------------------------------------------------
ModelForm Validation
---------------------------------------------------------------

▪ In a Django ModelForm, you can implement
validation in two key aspects:

&nbsp;&nbsp; ▪ Validating the Model

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Ensure that the data adheres to the validation rules specified in the corresponding Django model.

&nbsp;&nbsp; ▪ Validating the Form

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Implement custom validation logic specific to the form.

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Considering any additional criteria or constraints
beyond those defined in the model.

---------------------------------------------------------------
Error Messages in Forms
---------------------------------------------------------------

▪ You can customize the error messages associated
with an existing validator

▪ by overriding the default messages

▪ Each validator has a list of error message keys

▪ Pass in a dictionary with keys and error messages

    class NameForm(forms.Form):
        name = forms.CharField(
        error_messages={ 
               'required': 'Please, enter your name'
        })

--------------------------------------------------------------
Form Class Methods
---------------------------------------------------------------

▪ init(self, args, **kwargs)

▪ This method is the constructor for the form class

▪ Used to initialize the form and can be overridden to perform any setups

from django import forms


    class NameForm(forms.ModelForm):
         def init(self,args, kwargs):
             super().init(*args, kwargs)
             # Custom initialization code
              for field_name in self.fields:
                  self.fields[field_name].widget.attrs['readonly'] = 'readonly'
                  self.fields[field_name].required = False


-------------------------------------------------------------
clean() Method
-------------------------------------------------------------

▪ clean(self)

▪ This method is used for overall form cleaning/validation that involves
multiple fields.

▪ It's called after all individual field clean methods.

---------------------------------------------------------------
clean<fieldname>() Method
---------------------------------------------------------------

▪ clean<fieldname>(self)

▪ This method is used to implement custom cleaning/validation for a
specific field.

▪ It's automatically called during form validation

    def clean_email(self):
        email = self.cleaned_data.get('email')
        # Custom cleaning/validation field-specific logic
        if email and not email.endswith('@example.com'):
            raise ValidationError('Wrong domain')
     return email

---------------------------------------------------------------------
Form Instance Methods
---------------------------------------------------------------------

▪ is_valid(self)

▪ This method is used to check if the form data is valid.

▪ It triggers the validation of all fields and returns True if the form is
valid, otherwise False.

▪ save(self, commit=True)

▪ If your form is a ModelForm (associated with a Django model), this
method is used to.

▪ save the form data to the database

                  views.py
     ...
     my_form = MyModelForm(request.POST)
     if my_form.is_valid():
     instance = my_form.save()
     # This saves the form data to the database

---------------------------------------------------------------
Django modelform_factory()
---------------------------------------------------------------

▪ Instead of defining a class, you can use the
standalone function

▪ modelform_factory(model,fields=None,…)

▪ It creates forms from a given model

▪ This approach can be more convenient if you do not
need to make many customizations

               models.py
    
    from django.db import models
    
    
    class Person(models.Model):
       name = models.CharField(max_length=100)
       email = models.EmailField()
    
                  forms.py
    
    from django.forms import modelform_factory
    from .models import Person
    
    PersonForm = modelform_factory(Person, fields=["name", "email"])

--------------------------------------------------------------
Django Formset
--------------------------------------------------------------

▪ Formset is a layer of abstraction to work with.

▪ Multiple forms on the same page.

▪ It allows you to manage and process multiple
forms simultaneously.

▪ Django provides a formset class to handle this.

            forms.py
    
    from django import forms
    from .models import Person
    
    class PersonForm(forms.ModelForm):
      class Meta:
      model = Person
      fields = ['name', 'email']


