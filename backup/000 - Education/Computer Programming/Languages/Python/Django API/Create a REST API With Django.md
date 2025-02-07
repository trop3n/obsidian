---
up: "[[000 - Education/Computer Programming/Languages/Python/Python|Python]]"
tags:
  - "#education/computerprogramming/languages/python/django"
---



> A Django model is a class that allows the mapping of the database table to a Python class and allows operations on the table through functions.

Since we're building a course catalog application, store the details about each course in an *application object*. 

- To do that, create a model named `Course`.
- For each course, add the following properties:
	- `title`: The name of the course.
	- `created_date`: course record creation name. 

```python
from django.db import models

# Create your models here.

class Course(models.Model)

    title = models.CharField(max_length=100)

    created = models.DateTimeField(auto_now_add=True)

```

```python
from django.db import models
```

> This section of code is accessing the django.db framework and import it's `models` library.

# Task 3: Make Migrations

Add the model to the database using database migration.

To do that, create a new migration using the `/usercode/projects/manage.py` file to add the `Course` model to the database.

1. Navigate to the terminal.
2. Use `cd /usercode/project` to change to the project directory
3. Create the migration using the following command: `python3 manage.py makemigrations api`
4. Apply the migration using the following command: `python3 manage.py migrate`

### Makemigrations API Terminal Output:
```bash
Migrations for 'api':
  api/migrations/0001_initial.py
    - Create model Course
```
### Migrate Terminal Output:
```bash
Operations to perform:
  Apply all migrations: admin, api, auth, contenttypes, sessions
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying admin.0003_logentry_add_action_flag_choices... OK
  Applying api.0001_initial... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying auth.0008_alter_user_username_max_length... OK
  Applying auth.0009_alter_user_last_name_max_length... OK
  Applying auth.0010_alter_group_name_max_length... OK
  Applying auth.0011_update_proxy_permissions... OK
  Applying auth.0012_alter_user_first_name_max_length... OK
  Applying sessions.0001_initial... OK
```
# Task 4: Set up URL Connections

Django applications use the base URLs available in the `/usercode/project/project/urls.py` file to access the application accordingly.

To connect the API with the base application, complete the following steps:

- Set up the URLs for API Methods
- Connect the API URLs with the base application
### Solution:

Add the following code in `/usercode/project/api/urls.py` to import modules and create an empty list of `urlpatterns`:

```Python
from django.urls import path
from . import views
urlpatterns=[]
```

Update the `/usercode/project/project/urls.py` file with the following code:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/', include('api.urls'))
]
```
# Task 5: Create Serializers

> **Serializers** help to serialize or convert complex data such as `querysets` and model instances to native Python data types.

These data types can be rendered to `JSON`, `XML` or other content types.

Serializers provide deserialization, allowing parsed data to be converted back into complex kinds after validating the incoming data.

In this task, create a serializer for your model `Course` in the `/usercode/project/api/models.py` file.
### Solution:

Add the following code in `/usercode/project/api/serializers.py` file:

```python
from dataclasses import field
from statistics import mode
from rest_framework import serializers
from .models import Course

class CourseSerializer(serializers.ModelSerializer):
    """Allows converting complex data into native Python datatypes."""
    class Meta:
        model = Course
        fields = '__all__'
```

# Task 6: Import Modules

In this task, create an API to perform different operations on the Course model.

To work with the API, import the following models to the `/usercode/project/api/views.py` file:

- `Response` from `rest_framework.response` to return response of API call.
- `api_view` from `rest_framework.decorators` to decorate the API response.
- `CourseSerializer` from the `serializer` file to convert the complex object to simple Python objects.
- `Course` model that we created ourself.
- `status` from `rest_framework` to add status with the API response.
- `get_object_or_404` from `django.shortcuts` to return a `404` error if no data is found.
### Solution:

```python
from rest_framework.response import Response
from rest_framework.decorators import api_view
from .serializers import CourseSerializer
from .models import Coursefrom rest_framework import status
from django.shortcuts import get_object_or_404
```
# Task 7: Create an Overview Endpoint

> We're all set with pre-settings for the API creation. The task is to create ***endpoints*** that can be called directly.

Create a new API call that returns a simple string overview of all the API calls. To do that, create a new API method and assign a URL to the API.

Add the code and perform the following steps:

- To reach the directory, use the following command:
```
cd /usercode/project
```
- Use the following command to run the project:
```
python3 manage.py runserver 0.0.0.0:8080
```
### Solution:

Add the following code in `/usercode/project/api/views.py` file:

```python
@api_view(['GET'])
def ApiOverview(request):
    api_urls = {      
	'To Return all Courses': '/courses',      
	'To add a new Course': '/courses/add',
	'Update an Course': '/courses/{CourseId}/update',
	 'Delete an Course': '/courses/{CourseId}/delete',
	 }    
	 return Response(api_urls)
```

Add the following `urlpattern` in the `/usercode/project/api/urls.py` file:

```python
path('', views.ApiOverview),
```

The final code of `/usercode/project/api/urls.py` file will be like this:

```python
from django.urls import path
from . import views
urlpatterns = [  path('', views.ApiOverview),]
```
# Task 8: Create a GET Data Endpoint

> Create a `GET` data endpoint to return all the records of courses available in the database.

To create a new `GET` API, create a new function that gets all the objects from the database and returns a `response` containing all the things.

After that, add a new `route` to this method in the `/usercode/project/api/urls.py` file.

### Solution:

Add the following code in the `/usercode/project/api/views.py` file:

```python
@api_view(['GET'])
def get_courses(request):
    courses = Course.object.all()
    serializer = CourseSerializer(courses, many=True)
    return Response(serializer.data)
```

Add the following `urlpattern` in `/usercode/projects/api/urls.py` file:

```python
path('courses/', views.get_courses, name="ViewCourses"),
```

The final code of the `/usercode/project/api/urls.py` file will be like this:

```python
from django.urls import path
from . import views
urlpatterns = [
    path('', views.ApiOverview),
    path('courses/', views.get_courses, name="ViewCourses"),
]
```
# Task 9: Create an Add Data Endpoint

> For this task, create a new `POST` endpoint, which inserts data into the database. Make a new object of the `Course` model and save it to the database.

After you're done with the task, verify your application by performing the following steps:

Access this URL `<BaseURL>/api/courses/add` containing `/api/courses/add` at the end of the base URL. 

Type the following `JSON` string in the input field and click the `POST` button to add data to the database:

```python
{
"title":"Sample Course"
}
```

### Solution:

1. Create a new method with the name `add_course` in the `/usercode/project/api/views.py` file.

```python
def get_courses(request):
```

2. Get the data from the `request` of the API.

4. Use `serializer` to save the record.

```python
serializer = CourseSerializer(data = request.data)
```

4. Return `201` status for the success and `404` if not found.

```python
if serializer.is_valid():
	serializer.save
	return Response(status=status.HTTP_201_CREATED)
else:
	return Response(status=status.HTTP_404_NOT_FOUND)
```

5. Add the URL of this method in the `/usercode/project/api/urls.py` file.

```python
path('courses/add', views.add_course,name="AddCourse")
```
# Task 10: Create a REST API With Django

> In this task, add a new `PUT` endpoint to update the course title using the `ID` of the course in the URL.

After we're done with the task, verify the application by performing the following steps:

1. A new URL access has been created for you with `<BaseURL>/api/courses/<id>/update`. 

2. Add the following `JSON` string in the input field and click the `PUT` button to update the record with `1`.

```JSON
{"title":"New Title"}
```

3. Verify the update by getting all courses available in the database using the URL `<BaseURL>/api/courses`.
### Solution:

1. Add a new function with the name `update_course` in the `/usercode/project/api/views.py` file.

```python
@api_view(['PUT'])
def update_course(request, id):
```

2. Get the ID from the URL and search for the record from the database with that ID.


```python
try:      
	task = Course.objects.get(id=id)
	except Course.DoesNotExist:      
		return Response(status=status.HTTP_404_NOT_FOUND)  
	serializer = CourseSerializer(task, data=request.data)  
	data = {}  
	if serializer.is_valid():      
		serializer.save()      
		data["success"] = "updated successfully"      
	return Response(data=data)  
return Response(serializer.errors, status = status.HTTP_404_NOT_FOUND)
```
# Task 11: Create a DELETE Data Endpoint

> In this task, create a `DELETE` endpoint to delete the record from the database. 

To create the `DELETE` endpoint, decorate the method with the `DELETE` keyword and delete the record from the database.

After we're done with the task, verify the application by performing the following steps:

1. Create a new URL access with `<BaseURL>/api/courses/<id>/delete`. Click the `DELETE` button to delete the record from the database.
2. Verify the deletion by getting all courses available in the database using the URL `<BaseURL>/api.courses`.

### Solution:

1. Create a new function with name `delete_course` in the `/usercode/project/api/views.py` file and decorate it with `@api_view(['DELETE'])`.

```python
@api_view(['DELETE'])
def delete_course(request, id):  
	try:      
		task = Course.objects.get(id=id)  
	except Course.DoesNotExist:      
		return Response(status=status.HTTP_404_NOT_FOUND)  
	operation = task.delete()  
	data = {}  
	if operation:      
		return Response(status=status.HTTP_202_ACCEPTED)  
	else:      
		return Response(status=status.HTTP_404_NOT_FOUND)
```

2. Add the following code to add a new URL in the `/usercode/project/api/urls.py` file:

```python
path('courses/<str:id>/delete', views.delete_course, name="DeleteCourse"),
```

3. The final code of the `/usercode/project/api/urls.py` file look like this:

```python
from django.urls import path
from . import views
urlpatterns = [  
	path('', views.ApiOverview),  
	path('courses/', views.get_courses, name="ViewCourses"),  
	path('courses/add/', views.add_course,name="AddCourse"),  
	path('courses/<str:id>/update', views.update_course, name="UpdateCourse"),  
	path('courses/<str:id>/delete', views.delete_course, name="DeleteCourse"),
	]
```

