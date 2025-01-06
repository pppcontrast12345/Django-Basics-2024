8.0 ﻿Class-Based Views Basic
-------------------------------------------
What are CBVs?

&nbsp;&nbsp;&nbsp;&nbsp; ▪ <strong>Class-Based Views</strong> are a programming
paradigm in Django.

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Where views are defined as Python classes
rather than functions.

&nbsp;&nbsp;&nbsp;&nbsp; ▪ These classes encapsulate the logic for handling
HTTP requests and responses.

----------------------------------------------
▪ In Class-Based Views (CBVs), the self attribute is
used to:

&nbsp;&nbsp;&nbsp;&nbsp; ▪ maintain state across different methods within
the class

▪ Since CBVs are implemented as classes, the instance
of the class (self) retains information:

&nbsp;&nbsp;&nbsp;&nbsp;  ▪ throughout the processing of a request

----------------------------------------------------
▪ Class-based views (CBVs) in Django offer a
more organized and object-oriented approach
to handling HTTP requests.

-----------------------------------------------------
CBVs Inheritance Structure
-----------------------------------------------------

▪ Class-Based Views leverage class inheritance to
create a structured and modular organization of
view logic.

▪ This approach allows:

&nbsp;&nbsp;&nbsp;&nbsp;  ▪ The reuse of code.

&nbsp;&nbsp;&nbsp;&nbsp;  ▪ The implementation of the mixin pattern.

---------------------------------------------------------------
Mixin Pattern
---------------------------------------------------------------

▪ CBVs often employ the mixin pattern.

▪ Specific functionality is encapsulated in separate
classes (mixins).

▪ These mixins can then be combined by inheriting
from multiple classes.

&nbsp;&nbsp;&nbsp;&nbsp;  ▪ providing flexibility and code reuse.

-------------------------------------------------------------------
CBVs vs FBVs
-------------------------------------------------------------------

-----------------------

▪ Class-Based Views

-----------------------

▪ Extensibility

▪ Reusability and
Modularity

▪ Organization and
Structure

▪ Built-in Views

▪ Harder to Read

▪ Implicit Code Flow

▪ Hidden Code in Parent
Classes/Mixins

-----------------------

▪ Function-Based Views

-----------------------

▪ Simplicity and Readability

▪ Direct Mapping to
HTTP Methods

▪ Explicit Code Flow

▪ More Concise for
Simple Cases

▪ Hard to Extend

▪ Hard to Reuse

▪ Handling HTTP Methods
via Conditional Branching

---------------------------------------------------------------
Why Using CBVs?
---------------------------------------------------------------

▪ Reusability

▪ CBVs encourage the use of mixins and inheritance.

▪ Making it easier to reuse and extend functionality.

▪ Organization

▪ Views logic can be organized into methods, making the
code more modular and maintainable.

▪ Built-in Views

▪ Django provides ready-to-use class-based views for
common patterns.

-------------------------------------------------------------------
Base Views
-------------------------------------------------------------------

▪ Base Views serve as foundational or parent views
in Django.

▪ Designed to be used independently or inherited from
other views.

▪ These views offer a substantial set of functionalities
essential for crafting Django views.

--------------------------------------------------------------------

▪ Base Views provide a solid starting point.

▪ It's important to note that they might not encompass
all the capabilities needed for every project.

▪ In Django, you commonly find built-in views, such as
generic class-based views, in the
django.views module.

----------------------------------------------------------------------
View Class
-----------------------------------------------------------------------

▪ The View class serves as the foundational master
class-based base view in Django.

▪ All other class-based views inherit from this base.

▪ It defines the HTTP methods that the view can handle:

&nbsp;&nbsp;&nbsp;&nbsp;  ▪ ['get', 'post', 'put', 'patch', 'delete', 'head', 'options', 'trace'].

---------------------------------------------------------------

▪ As the primary building block, the View class provides.

▪ a structure for handling various types of requests.

▪ and forms the basis for the implementation of more
specific class-based views in Django.

-----------------------------------------------------------------

▪ as_view() method is decorated by a @classonlymethod.

▪ It is a class-level method and cannot be accessed through an instance
of the class.

▪ The method iterates over initkwargs, performing validations and
preparing the view for handling requests.

------------------------------------------------------------------

▪ Within the as_view method, the encapsulated view function accepts
the standard parameters.

▪ request, *args, and **kwargs.

▪ During its execution, it binds the instance of the class to the class
attributes using self.

▪ Specifically, it associates self with the class attributes provided
in initkwargs.

▪ Additionally, the function assigns request to self.request, args to
self.args, and kwargs to self.kwargs.

-----------------------------------------------------------------------

▪ The binding ensures that the view function has access to the
essential request and argument information.

&nbsp;&nbsp;&nbsp;&nbsp;  ▪ when handling HTTP requests.

▪ facilitating seamless integration with the class-based view.

-------------------------------------------------------------------------

▪ In Django's class-based views, the dispatch() method is a
fundamental part of the view processing flow.

▪ It is responsible for determining which specific method to call
based on the HTTP method of the incoming request.

▪ The dispatch() method acts as a kind of router for directing
the flow of control to the appropriate method.

▪ E.g., get(), post(), etc. based on the type of HTTP request.

▪ You can override specific methods (e.g., get, post) to customize
the behavior for different HTTP methods.

---------------------------------------------------------------------------

The lifecycle of request-response in CBVs involves several stages, from
the initiation of the request to the generation of the response:

1. Initialization
2. as_view() Method
3. dispatch() Method
4. Pre-processing (Optional)
5. HTTP Method-Specific Methods
6. View Logic Execution
7. Response Generation
8. Post-processing (Optional)
9. Response Sent to Client

--------------------------------------------------------------------------------
TemplateView
--------------------------------------------------------------------------------

▪ The TemplateView is designed to render a specified
template, enriching the context with parameters
captured from the URL.

▪ It inherits methods and attributes from three
main classes:

&nbsp;&nbsp;&nbsp;&nbsp;  ▪ TemplateResponseMixin

&nbsp;&nbsp;&nbsp;&nbsp;  ▪ ContextMixin

&nbsp;&nbsp;&nbsp;&nbsp;  ▪ View

-----------------------------------------------------------------------------------
RedirectView
-----------------------------------------------------------------------------------

▪ The RedirectView in Django is designed to perform
redirects to a specified URL.

▪ It inherits from the base View class and returns an
HttpResponsePermanentRedirect.

------------------------------------------------------------------------------------
FormViews
------------------------------------------------------------------------------------

▪ Form Views are a key component of handling
form submissions.

▪ They are responsible for rendering forms to users.

▪ Processing the data submitted in the form.

▪ Performing actions based on that data.

▪ They play a crucial role in creating, updating, and
validating data through forms.

--------------------------------------------------------------------------------------
Generic Editing Views
--------------------------------------------------------------------------------------

▪ In Django, CreateView, UpdateView, and
DeleteView are class-based views that:

&nbsp;&nbsp;&nbsp;&nbsp;  ▪ provide convenient ways to handle the Create,
Update, and Delete (CUD) operations

▪ These views are part of Django's generic class-based
views and can be used to:

&nbsp;&nbsp;&nbsp;&nbsp;  ▪ quickly set up views for common operations


----------------------------------------------------------------------------------------
success_url and reverse_lazy()
----------------------------------------------------------------------------------------

▪ success_url attribute

&nbsp;&nbsp;&nbsp;&nbsp;  ▪ In a class-based view, such as CreateView or UpdateView, the success_url attribute is used to specify the URL to which the user

should be redirected after a successful form submission

▪ This attribute can be set to a URL string or a URL pattern name

▪ <strong>reverse_lazy()</strong>

&nbsp;&nbsp;&nbsp;&nbsp;  ▪ It is a utility function provided by Django to reverse URL patterns at a
lazy, or deferred, time

&nbsp;&nbsp;&nbsp;&nbsp;  ▪ It is used to obtain the URL for a given view or URL pattern name

&nbsp;&nbsp;&nbsp;&nbsp;  ▪ It's particularly useful in situations where the URL configuration is not
fully loaded when the module is imported (such as in class-based views)

---------------------------------------------------------------

▪ The get_success_url method is used to determine dynamically the
URL to which the user should be redirected after a successful form
submission or another successful operation

---------------------------------------------------------------
ModelFormMixin
---------------------------------------------------------------

▪ In Django, ModelFormMixin is a mixin class that
provides functionality:

&nbsp;&nbsp;&nbsp;&nbsp;  ▪ to work with model forms in class-based views

▪ It is commonly used in conjunction with generic classbased views.

▪ CreateView, UpdateView, and DeleteView

▪ It simplifies the process of working with forms
associated with model instances.

---------------------------------------------------------------
Customizing Form Handling
---------------------------------------------------------------

▪ There are key methods you can override to customize form
handling in CBVs

     class ArticleCreateView(CreateView):
        ...
        def form_valid(self, form):
           # Custom logic for valid forms during object creation
        return super().form_valid(form)
    
        def form_invalid(self, form):
           # Custom logic for invalid forms during object creation
        return super().form_invalid(form)
    



