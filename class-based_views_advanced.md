9.0 Class-Based Views Advanced
---------------------------------------------------------------
Built-in Generic Views Benefits


▪ Generic views in Django are designed to:

&nbsp;&nbsp;&nbsp;&nbsp;  ▪ simplify the development process

&nbsp;&nbsp;&nbsp;&nbsp;  ▪ by offering convenient interfaces for common tasks developers often face

▪ They provide a high-level abstraction to:

&nbsp;&nbsp;&nbsp;&nbsp;  ▪ perform key operations

&nbsp;&nbsp;&nbsp;&nbsp;  ▪ reducing the need for repetitive code

&nbsp;&nbsp;&nbsp;&nbsp;  ▪ accelerating development

---------------------------------------------------------------
Generic Views - Main Functionalities
---------------------------------------------------------------

▪ The main functionalities of generic views include:

▪ Displaying List and Detail Pages

▪ Presenting collections of objects and their detailed views
without the need for extensive view and template code.

▪ CRUD Operations (Create, Update, Delete)

▪ Offering predefined views for creating, updating and
deleting objects.

▪ Date-Based Object Presentation

▪ А straightforward solution for presenting the objects in
year/month/day archive pages.

---------------------------------------------------------------
Basic DetailView
---------------------------------------------------------------

▪ In a Django DetailView, the self.object attribute refers to the object that
the view is operating upon.

▪ This object is typically an instance of the model specified in the model
attribute and is set by the SingleObjectMixin during the view
processing lifecycle.

-------------------------------------------------------------------

    class ArticleDetailView(DetailView):
      model = Article
      template_name = 'article_details.html'
      
      def get(self, request, args, **kwargs):
         # Access the current object being viewed
         current_article = self.get_object()
         # You can do something with the current_article
      return super().get(request,args, **kwargs)

---------------------------------------------------------------
get_object() Method
---------------------------------------------------------------

▪ The primary purpose of the get_object method is to:

&nbsp;&nbsp;&nbsp;&nbsp;  ▪ fetch and return a single object

&nbsp;&nbsp;&nbsp;&nbsp;  ▪ based on the view's configuration and the URL parameters

▪ It is particularly useful in detail views where you need to:

&nbsp;&nbsp;&nbsp;&nbsp;  ▪ display information about a specific instance of a model.

▪ If the method is not overridden in a class-based view.

▪ The default behavior is provided by the SingleObjectMixin class.

▪ The default implementation uses the model specified in the model
attribute and the primary key from the URL parameters to retrieve the
corresponding object.

▪ By understanding and utilizing the get_object method.

▪ Developers can have greater control over how individual objects are
retrieved and processed in their class-based views.

--------------------------------------------------------------------
    
    
    class ArticleDetailView(DetailView):
     ...
     def get_object(self, queryset=None):
     # Retrieve the current object
     current_object = super().get_object(queryset)
     # Update view count for the article
     current_object.views_count += 1
     current_object.save()
     return current_object


