3.0 ﻿Urls and Views
------------------------------
Static Path
------------------------------

▪ Definition - A static path is a fixed URL that doesn’t change and always points to the same resource.

Example:

    path('about/', views.about, name='about')

▪ URL: /about/

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Always calls the about view function.

▪ Use Case:

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Static content (e.g., "About Us," "Contact").

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Pages with no variable data.

--------------------------------------
Dynamic Path
--------------------------------------

▪ Definition - A dynamic path includes variable segments that can change depending on the URL input, making it reusable for multiple resources.

    path('users/<int:id>/', views.user_detail, name='user_detail')

&nbsp;&nbsp;&nbsp;&nbsp; ▪ URLs: /users/1/, /users/42/, /users/100/

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Calls the same view (user_detail) but passes the id as a parameter.

▪ Use Case:

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Resources with variable data (e.g., user profiles, blog posts, product pages).

---------------------------------------------
When to Use Each?
---------------------------------------------
▪ Static Path: For fixed pages like "Home," "About Us," or "Privacy Policy."

▪ Dynamic Path: For pages that depend on external data or identifiers, like user profiles, blog posts, or product pages.

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Dynamic content where specific data is fetched based on a parameter.

----------------------------------------------
Default Path Converters
----------------------------------------------

▪ <strong>str</strong> - matches any non-empty string, excluding "/"

▪ <strong>int</strong> - matches zero or any positive integer

▪ <strong>slug</strong> - matches any slug string consisting of ASCII
letters, numbers, hyphens, and underscores

▪ <strong>path</strong> - matches any non-empty string, including "/"

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Allows you to match a complete URL path

▪ <strong>uuid</strong> - matches a formatted UUID

----------------------------------------------------
Including URLs in Django
----------------------------------------------------

▪ What Is It?

&nbsp;&nbsp;&nbsp;&nbsp; ▪ The <strong>include()</strong> function in Django allows you to split your URL configurations into smaller, modular parts.

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Instead of defining all routes in the main urls.py file, you can delegate specific URL patterns to other apps or modules.

--------------------------------------------------------
When Do We Use It?

&nbsp;&nbsp;&nbsp;&nbsp; ▪ When your project has multiple apps, each with its own set of routes (e.g., blog, users, shop).

&nbsp;&nbsp;&nbsp;&nbsp; ▪ To keep the main urls.py file concise and organized.

Example 1.0

Main urls.py:

    from django.contrib import admin
    from django.urls import path, include
    
    urlpatterns = [
        path('admin/', admin.site.urls),
        path('blog/', include('blog.urls')),  # Delegates to blog app's URLs
        path('users/', include('users.urls')),  # Delegates to users app's URLs
    ]

Example 2.0

App-Specific urls.py (e.g., blog/urls.py):

    from django.urls import path
    from . import views
    
    urlpatterns = [
        path('', views.blog_home, name='blog_home'),
        path('<int:id>/', views.blog_detail, name='blog_detail'),
    ]

Key Benefits:

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Cleaner, easier-to-read urls.py structure.

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Encourages modular app design, especially in large projects.

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Allows for independent development and testing of apps. 

----------------------------------------------
Including a URLpatterns List
----------------------------------------------

▪ You can include a URLpatterns list.

Example:

    urlpatterns = [
        path('profile/', include([
            path('create/', views.create, name='profile_create'),
            path('edit/', views.edit, name='profile_edit'),
            path('delete/', views.delete, name='profile_delete'),
        ])),
    ]

▪ It removes redundancy from URL configuration
modules, especially when a single pattern prefix is
used repeatedly.

---------------------------------------------------------------
Function-Based Views (FBVs)
---------------------------------------------------------------

▪ Function-Based Views in Django handle requests and responses using Python functions.

&nbsp;&nbsp;&nbsp;&nbsp; ▪ HttpRequest object: The first argument (typically named request) represents the incoming HTTP request.

&nbsp;&nbsp;&nbsp;&nbsp; ▪ *args: Captures unnamed URL pattern matches.

&nbsp;&nbsp;&nbsp;&nbsp; ▪ **kwargs: Captures named parts of the URL pattern.

▪ Each View Returns:

&nbsp;&nbsp;&nbsp;&nbsp; ▪ HttpResponse object: Represents the response sent back to the client, containing the content (e.g., HTML, JSON) and metadata (headers, status code).

------------------------------------------------------------------------
HttpRequest Object
------------------------------------------------------------------------

▪ Purpose: Represents an incoming request from a client (like a web browser).

▪ Contains:

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Headers: Metadata about the request (e.g., user-agent, cookies).

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Method: HTTP methods like GET, POST, etc.

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Session: Information about the user's session.

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Submitted Data: Form data or query parameters sent with the request.

▪ Usage: Typically passed as the first argument to a view function to process and respond to the client's request.

---------------------------------------------------------------
HttpResponse Object
---------------------------------------------------------------

▪ Purpose: Represents the response sent back to the client.

▪ Contains:

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Content: Data sent to the client (HTML, JSON, etc.).

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Headers: Additional response metadata (e.g., content type, status code).

▪ Views Must Return an HttpResponse Object: This allows the client to receive the response content in the required format.


Example of a Function-Based View:

    from django.http import HttpRequest, HttpResponse


    def my_view(request: HttpRequest, *args, **kwargs) -> HttpResponse:
      # Accessing request data
      user_agent = request.headers.get('User-Agent', 'unknown')
      method = request.method  # GET, POST, etc.

      # Processing the request
      if method == "GET":
          content = f"<h1>Welcome to My View</h1><p>Your browser is: {user_agent}</p>"
      else:
          content = "<h1>Method Not Allowed</h1>"
  
      # Returning a response
      return HttpResponse(content, content_type="text/html")

--------------------------------------------------------------
Django Shortcut Functions
--------------------------------------------------------------

▪ Django shortcut functions are utility functions.

▪ That simplify common tasks in Django development.

▪ They streamline the process of working with the
Model-View-Template (MVT) paradigm by providing
convenient methods:

▪ render()

▪ redirect()

▪ get_object_or_404()

▪ get_list_or_404()

----------------------------------------------------------------------
render()
----------------------------------------------------------------------

▪ Combines a template with a context dictionary.

▪ Returns an HttpResponse object with the
rendered text.

▪ Simplifies the process of rendering dynamic content.

▪ by automatically handling the template rendering.

▪ creating an HTTP response with the
rendered content.

▪ Required arguments:

&nbsp;&nbsp;&nbsp;&nbsp; ▪ request - The HttpRequest object used in
generating the response.

&nbsp;&nbsp;&nbsp;&nbsp; ▪ template_name - The full name of the template to
be used for rendering.

------------------------------------------------------------------------------
redirect()
------------------------------------------------------------------------------

▪ Is used to redirect the user to the appropriate URL.

▪ By passing a hardcoded URL to redirect to:

&nbsp;&nbsp;&nbsp;&nbsp; ▪ redirect('/some/url/')

▪ By passing the name of a view along with optional
positional or keyword arguments.

&nbsp;&nbsp;&nbsp;&nbsp; ▪ redirect(some_view_name, *args, **kwargs) 

▪ It returns an HTTP status code of 302.

---------------------------------------------------
Named URLs
---------------------------------------------------

▪ Add a name to the path in the urls.py module

    from django.urls import path
    from . import views
    
    urlpatterns = [
        path(
            'department/<int:department_id>/',
            views.show_department_by_id,
            name='department_by_id'       # name of the path
        ),
    ]

------------------------------------------------------------
reverse()
------------------------------------------------------------

▪ URL reversing is a process in Django that allows you:

&nbsp;&nbsp;&nbsp;&nbsp; ▪ to generate a URL for a specific view.

&nbsp;&nbsp;&nbsp;&nbsp; ▪ based on its name and any arguments it may require.

    from django.urls import reverse

    
    url = reverse('department-by-id', kwargs={'department_id': 1})

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Helps to decouple URLs from view functions.

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Allows you to generate URLs based on the current state of your application and the data available.

