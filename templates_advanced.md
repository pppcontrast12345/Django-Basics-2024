6.0 ﻿Django Templates Advanced
-------------------------------------------

Template Inheritance

▪ Template inheritance enables the creation of a
foundational skeleton template.

▪ This base template encompasses shared elements and
establishes blocks that child templates can customize.

▪ Generally, elements like the header and footer remain
consistent throughout the entire application.

▪ By leveraging template inheritance, we can efficiently
reuse common components across different sections
of our application.

---------------------------------------------------------------
Example: Template Inheritance

                         base.html
    
    <!DOCTYPE html>
    <html lang="en">
    <head>
            <meta charset="UTF-8">
            <title>{% block title %}{% endblock %}</title>
    </head>
    
    <body>
              {% block content %}
              # default code if no content is passed in
              {% endblock %}
    </body>
    </html>

---------------------------------------------------------------

                         index.html
    
    {% extends "base.html" %}
    
    {% block title %}
       Home Page
    {% endblock %}
    
    {% block content %}
             {% for dep in departments.items %}
                  <h2>{{ dep.title }}</h2>
                  <p>{{ dep.description }}</p>
              {% endfor %}
    {% endblock %}

---------------------------------------------------------------
Including Template Snippets

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Template snippets provide a way to include templates within another template

    {% include template-name %}

▪ The template name for inclusion can be specified using

&nbsp;&nbsp;&nbsp;&nbsp; ▪ a variable

    {% include template_name %}

&nbsp;&nbsp;&nbsp;&nbsp; ▪ a quoted string in single or double quotes

    {% include "nav-bar.html" %}

-------------------------------------------------------------

▪ Establish a reusable navigation bar logic that can be implemented
across various templates as needed.

▪ Consider including the code into the base template.

▪ to enhance maintainability and consistency.

                 nav-bar.html
    
    <header>
           <nav>
              {# some navigation bar logic #}
           </nav>
    </header>

--------------------------------------------------------------
▪ Include the template snippet

                    index.html
    
    {% extends "base.html" %}
    
    {% block title %}
    
    Home Page
    
    {% endblock %}
    
    {% block content %}

         {% include "departments/includes/nav-bar.html" %}
         {% for dep in departments.items %}
               <h2>{{ dep.title }}</h2>
               <p>{{ dep.description }}</p>
         {% endfor %}

    {% endblock %}

-----------------------------------------------------------
Include with Context
-----------------------------------------------------------

▪ The included template nav-bar.html is rendered within the
context of the template index.html that includes it.

▪ Additional context can be passed to the included template
using keyword arguments.

    {% include template_name with user='user_name' %}

▪ Alternatively, the included template can be rendered with
only the variables provided or with no variables at all.

    {% include template_name with user='user_name' only %}


---------------------------------------------------------------
Bootstrap (Front-end Framework)
---------------------------------------------------------------

▪ A popular open-source front-end framework.

▪ Simplifies the process of designing and building.

▪ responsive and mobile-first web pages.

▪ Includes a set of pre-designed HTML, CSS, and
JavaScript components.

-----------------------------------------------------------------
Bootstrap - Pros and Cons

▪ Pros:

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Rapid Development

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Responsive Design

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Cross-Browser Compatibility

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Large Community

▪ Cons:

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Generic Look

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Learning Curve

&nbsp;&nbsp;&nbsp;&nbsp; ▪ File Size

&nbsp;&nbsp;&nbsp;&nbsp; ▪ Overhead

