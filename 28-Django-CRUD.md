# Django CRUD

After we defined our models and created some initial library records to work with, it's time to write the code that presents that information to users. The first thing we need to do is determine what information we want to display in our pages, and define the URLs to use for returning those resources. Then we'll create a URL mapper, views, and templates to display the pages.

The following diagram describes the main data flow, and the components required when handling HTTP requests and responses. As we already implemented the model, the main components we'll create are:

URL mappers to forward the supported URLs (and any information encoded in the URLs) to the appropriate view functions.
View functions to get the requested data from the models, create HTML pages that display the data, and return the pages to the user to view in the browser.
Templates to use when rendering data in the views.

As you'll see in the next section, we have 5 pages to display, which is too much information to document in a single article. Therefore, this article will focus on how to implement the home page, and we'll cover the other pages in a subsequent article. This should give you a good end-to-end understanding of how URL mappers, views, and models work in practice.

Defining the resource URLs
As this version of LocalLibrary is essentially read-only for end users, we just need to provide a landing page for the site (a home page), and pages that display list and detail views for books and authors.

The URLs that we'll need for our pages are:

catalog/ — The home (index) page.
catalog/books/ — A list of all books.
catalog/authors/ — A list of all authors.
catalog/book/<id> — The detail view for a particular book, with a field primary key of <id> (the default). For example, the URL for the third book added to the list will be /catalog/book/3.
catalog/author/<id> — The detail view for the specific author with a primary key field of <id>. For example, the URL for the 11th author added to the list will be /catalog/author/11.
The first three URLs will return the index page, books list, and authors list. These URLs do not encode any additional information, and the queries that fetch data from the database will always be the same. However, the results that the queries return will depend on the contents of the database.

By contrast the final two URLs will display detailed information about a specific book or author. These URLs encode the identity of the item to display (represented by <id> above). The URL mapper will extract the encoded information and pass it to the view, and the view will dynamically determine what information to get from the database. By encoding the information in the URL we will use a single set of a URL mapping, a view, and a template to handle all books (or authors).

Note: With Django, you can construct your URLs however you require — you can encode information in the body of the URL as shown above, or include GET parameters in the URL, for example /book/?id=6. Whichever approach you use, the URLs should be kept clean, logical, and readable, as recommended by the W3C. The Django documentation recommends encoding information in the body of the URL to achieve better URL design.

As mentioned in the overview, the rest of this article describes how to construct the index page.

Creating the index page
The first page we'll create is the index page (catalog/). The index page will include some static HTML, along with generated "counts" of different records in the database. To make this work we'll create a URL mapping, a view, and a template.

Note: It's worth paying a little extra attention in this section. Most of the information also applies to the other pages we'll create.

URL mapping
When we created the skeleton website, we updated the locallibrary/urls.py file to ensure that whenever a URL that starts with catalog/ is received, the URLConf module catalog.urls will process the remaining substring.

The following code snippet from locallibrary/urls.py includes the catalog.urls module:

urlpatterns += [
    path('catalog/', include('catalog.urls')),
]
Copy to Clipboard
Note: Whenever Django encounters the import function django.urls.include(), it splits the URL string at the designated end character and sends the remaining substring to the included URLconf module for further processing.

We also created a placeholder file for the URLConf module, named /catalog/urls.py. Add the following lines to that file:

urlpatterns = [
    path('', views.index, name='index'),
]
Copy to Clipboard
The path() function defines the following:

A URL pattern, which is an empty string: ''. We'll discuss URL patterns in detail when working on the other views.
A view function that will be called if the URL pattern is detected: views.index, which is the function named index() in the views.py file.
The path() function also specifies a name parameter, which is a unique identifier for this particular URL mapping. You can use the name to "reverse" the mapper, i.e. to dynamically create a URL that points to the resource that the mapper is designed to handle. For example, we can use the name parameter to link to our home page from any other page by adding the following link in a template:

<a href="{% url 'index' %}">Home</a>.
Copy to Clipboard
Note: We can hard code the link as in <a href="/catalog/">Home</a>), but if we change the pattern for our home page, for example, to /catalog/index) the templates will no longer link correctly. Using a reversed URL mapping is more robust.

View (function-based)
A view is a function that processes an HTTP request, fetches the required data from the database, renders the data in an HTML page using an HTML template, and then returns the generated HTML in an HTTP response to display the page to the user. The index view follows this model — it fetches information about the number of Book, BookInstance, available BookInstance and Author records that we have in the database, and passes that information to a template for display.

Open catalog/views.py and note that the file already imports the render() shortcut function to generate an HTML file using a template and data:

from django.shortcuts import render

# Create your views here.
Copy to Clipboard
Paste the following lines at the bottom of the file:

from .models import Book, Author, BookInstance, Genre

def index(request):
    """View function for home page of site."""

    # Generate counts of some of the main objects
    num_books = Book.objects.all().count()
    num_instances = BookInstance.objects.all().count()

    # Available books (status = 'a')
    num_instances_available = BookInstance.objects.filter(status__exact='a').count()

    # The 'all()' is implied by default.
    num_authors = Author.objects.count()

    context = {
        'num_books': num_books,
        'num_instances': num_instances,
        'num_instances_available': num_instances_available,
        'num_authors': num_authors,
    }

    # Render the HTML template index.html with the data in the context variable
    return render(request, 'index.html', context=context)
Copy to Clipboard
The first line imports the model classes that we'll use to access data in all our views.

The first part of the view function fetches the number of records using the objects.all() attribute on the model classes. It also gets a list of BookInstance objects that have a value of 'a' (Available) in the status field. You can find more information about how to access model data in our previous tutorial Django Tutorial Part 3: Using models > Searching for records.

At the end of the view function we call the render() function to create an HTML page and return the page as a response. This shortcut function wraps a number of other functions to simplify a very common use case. The render() function accepts the following parameters:

the original request object, which is an HttpRequest.
an HTML template with placeholders for the data.
a context variable, which is a Python dictionary, containing the data to insert into the placeholders.
We'll talk more about templates and the context variable in the next section. Let's get to creating our template so we can actually display something to the user!

Template
A template is a text file that defines the structure or layout of a file (such as an HTML page), it uses placeholders to represent actual content.

A Django application created using startapp (like the skeleton of this example) will look for templates in a subdirectory named 'templates' of your applications. For example, in the index view that we just added, the render() function will expect to find the file index.html in /locallibrary/catalog/templates/ and will raise an error if the file is not present.

You can check this by saving the previous changes and accessing 127.0.0.1:8000 in your browser - it will display a fairly intuitive error message: "TemplateDoesNotExist at /catalog/", and other details.

Note: Based on your project's settings file, Django will look for templates in a number of places, searching in your installed applications by default. You can find out more about how Django finds templates and what template formats it supports in the Templates section of the Django documentation.

Extending templates
The index template will need standard HTML markup for the head and body, along with navigation sections to link to the other pages of the site (which we haven't created yet), and to sections that display introductory text and book data.

Much of the HTML and navigation structure will be the same in every page of our site. Instead of duplicating boilerplate code on every page, you can use the Django templating language to declare a base template, and then extend it to replace just the bits that are different for each specific page.

The following code snippet is a sample base template from a base_generic.html file. We'll be creating the template for LocalLibrary shortly. The sample below includes common HTML with sections for a title, a sidebar, and main contents marked with the named block and endblock template tags. You can leave the blocks empty, or include default content to use when rendering pages derived from the template.

In this tutorial we're going to complete the first version of the LocalLibrary website by adding list and detail pages for books and authors (or to be more precise, we'll show you how to implement the book pages, and get you to create the author pages yourself!)

The process is similar to creating the index page, which we showed in the previous tutorial. We'll still need to create URL maps, views, and templates. The main difference is that for the detail pages, we'll have the additional challenge of extracting information from patterns in the URL and passing it to the view. For these pages, we're going to demonstrate a completely different type of view: generic class-based list and detail views. These can significantly reduce the amount of view code needed, making them easier to write and maintain.

The final part of the tutorial will demonstrate how to paginate your data when using generic class-based list views.

Book list page
The book list page will display a list of all the available book records in the page, accessed using the URL: catalog/books/. The page will display a title and author for each record, with the title being a hyperlink to the associated book detail page. The page will have the same structure and navigation as all other pages in the site, and we can, therefore, extend the base template (base_generic.html) we created in the previous tutorial.

URL mapping
Open /catalog/urls.py and copy in the line setting the path for 'books/', as shown below. Just as for the index page, this path() function defines a pattern to match against the URL ('books/'), a view function that will be called if the URL matches (views.BookListView.as_view()), and a name for this particular mapping.

urlpatterns = [
    path('', views.index, name='index'),
    path('books/', views.BookListView.as_view(), name='books'),
]
Copy to Clipboard
As discussed in the previous tutorial the URL must already have matched /catalog, so the view will actually be called for the URL: /catalog/books/.

The view function has a different format than before — that's because this view will actually be implemented as a class. We will be inheriting from an existing generic view function that already does most of what we want this view function to do, rather than writing our own from scratch.

For Django class-based views we access an appropriate view function by calling the class method as_view(). This does all the work of creating an instance of the class, and making sure that the right handler methods are called for incoming HTTP requests.

View (class-based)
We could quite easily write the book list view as a regular function (just like our previous index view), which would query the database for all books, and then call render() to pass the list to a specified template. Instead, however, we're going to use a class-based generic list view (ListView) — a class that inherits from an existing view. Because the generic view already implements most of the functionality we need and follows Django best-practice, we will be able to create a more robust list view with less code, less repetition, and ultimately less maintenance.

Open catalog/views.py, and copy the following code into the bottom of the file:

from django.views import generic

class BookListView(generic.ListView):
    model = Book
Copy to Clipboard
That's it! The generic view will query the database to get all records for the specified model (Book) then render a template located at /locallibrary/catalog/templates/catalog/book_list.html (which we will create below). Within the template you can access the list of books with the template variable named object_list OR book_list (i.e. generically "<the model name>_list").

Note: This awkward path for the template location isn't a misprint — the generic views look for templates in /application_name/the_model_name_list.html (catalog/book_list.html in this case) inside the application's /application_name/templates/ directory (/catalog/templates/).

You can add attributes to change the default behavior above. For example, you can specify another template file if you need to have multiple views that use this same model, or you might want to use a different template variable name if book_list is not intuitive for your particular template use-case. Possibly the most useful variation is to change/filter the subset of results that are returned — so instead of listing all books you might list top 5 books that were read by other users.

class BookListView(generic.ListView):
    model = Book
    context_object_name = 'book_list'   # your own name for the list as a template variable
    queryset = Book.objects.filter(title__icontains='war')[:5] # Get 5 books containing the title war
    template_name = 'books/my_arbitrary_template_name_list.html'  # Specify your own template name/location
Copy to Clipboard
Overriding methods in class-based views
While we don't need to do so here, you can also override some of the class methods.

For example, we can override the get_queryset() method to change the list of records returned. This is more flexible than just setting the queryset attribute as we did in the preceding code fragment (though there is no real benefit in this case):

class BookListView(generic.ListView):
    model = Book

    def get_queryset(self):
        return Book.objects.filter(title__icontains='war')[:5] # Get 5 books containing the title war
Copy to Clipboard
We might also override get_context_data() in order to pass additional context variables to the template (e.g. the list of books is passed by default). The fragment below shows how to add a variable named "some_data" to the context (it would then be available as a template variable).

class BookListView(generic.ListView):
    model = Book

    def get_context_data(self, **kwargs):
        # Call the base implementation first to get the context
        context = super(BookListView, self).get_context_data(**kwargs)
        # Create any data and add it to the context
        context['some_data'] = 'This is just some data'
        return context
Copy to Clipboard
When doing this it is important to follow the pattern used above:

First get the existing context from our superclass.
Then add your new context information.
Then return the new (updated) context.


References [1](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Home_page), [2](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Generic_views), [3](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Forms)