# Real-Estate
A Real estate web application based on advance python


auto addition og gitigonere file in python
----> npx gitignore python  



clearing database port in ubuntu
-----> sudo lsof -i :5432
------> sudo service postgresql stop

-----------------------------------------------------------------
<h3> Some Good Practices for Developement Django web-app </h3>
<h4> For Settings.py </h4>
<span> Make saperate folder named as Settings </span>
<p> create three different files </p>
<ul>
<li>
base.py ----> All the common configuration settings for both deveopment and production
</li>
<li>
development.py ---> setings used during development
</li>
<li>
production.py ---->  settings used for production and development
</li>

</ul>

<p> Some tips (for settings.py): </p>
<ul>
<li> 
    used environment variable i.e .env file to secure keys and confidential data
</li>
<li>
make different directory for default apps, local apps, third-party apps
</li>
<li> use loggers to keep record of logs during the runtime of the applicaiton </li>
</ul>

<h3> SETUP.CFG</h3>
<p> function </p>
<p> A powerful tool for defining and maintaining a wide range of configuration related to our python project, helpig ensure consitency, reliability and ease of distribution .
</p>
<p> Metadata about packages , project management , tool configuration i.e configure their behaviours </p>


<h3>.ENV </h3>
<p> A file that contains environment variables and their values. It is used to store sensitive information such as passwords, API keys, and other confidential data</p>

<h3> Loggers in DJango </h3>
<p> Loggers in Django are used for tracking events in your application, which can be helpful for debugging and monitoring purposes. They allow you to record information at various levels (e.g., debug, info, warning, error, critical) and can be configured to output to different locations, such as the console, a file, or an email. </p>
<p> To use loggers in Django, you first need to configure them in your settings.py file. You can do this by adding the following code
</p>
<p>
import logging

logger = logging.getLogger(__name__)

def my_view(request):
    logger.debug('This is a debug message')
    logger.info('This is an info message')
    logger.warning('This is a warning message')
    logger.error('This is an error message')
    logger.critical('This is a critical message')

</p>


<h3>Handlers used in loggers </h3>
<p> Handlers in Django are used to specify where and how log messages are output. They can be configured to output to different locations, such as the console, a file, or an email. </p>

<h3> Filters used in loggers </h3>
<p> Filters in Django are used to modify log messages before they are output. They can be used to filter out certain types of messages, </p>
<p>
Filters in Django are used to filter log messages based on certain criteria. They allow you to specify which log messages should be output based on their level, logger name, or other attributes.

Here's an example of how you might define a filter in Django:

python
Copy code
LOGGING = {
    'version': 1,
    'filters': {
        'require_debug_true': {
            '()': 'django.utils.log.RequireDebugTrue',
        },
    },
    'handlers': {
        'console': {
            'class': 'logging.StreamHandler',
            'filters': ['require_debug_true'],
            'level': 'DEBUG',
        },
    },
    'root': {
        'handlers': ['console'],
        'level': 'WARNING',
    },
}
In this example, we define a logging configuration dictionary in our Django settings file. We specify a filter called require_debug_true, which is a built-in filter provided by Django. This filter only allows log messages to be output if the DEBUG setting is set to True.

We then specify a handler called console, which uses the StreamHandler class to output log messages to the console. We add the require_debug_true filter to the handler, which means that only log messages that pass the filter will be output.

We set the level of the handler to DEBUG, which means that it will output all log messages at the DEBUG level or higher.

You can define your own custom filters by creating a class that inherits from logging.Filter and overriding the filter method.

</p>

<h3> FORMATTERS IN LOGGERS </h3>
<p>ormatters in Django are used to specify the format of log messages. They allow you to customize the appearance of log messages by specifying the order and format of their components, such as the logger name, level, message, and timestamp.

Here's an example of how you might define a formatter in Django:

python
Copy code
LOGGING = {
    'version': 1,
    'formatters': {
        'simple': {
            'format': '%(asctime)s - %(name)s - %(levelname)s - %(message)s',
        },
    },
    'handlers': {
        'console': {
            'class': 'logging.StreamHandler',
            'formatter': 'simple',
            'level': 'DEBUG',
        },
    },
    'root': {
        'handlers': ['console'],
        'level': 'WARNING',
    },
}
In this example, we define a logging configuration dictionary in our Django settings file. We specify a formatter called simple, which uses the Formatter class to format log messages. We set the format of the formatter to %(asctime)s - %(name)s - %(levelname)s - %(message)s, which includes the timestamp, logger name, level, and message in the log message.

We then specify a handler called console, which uses the StreamHandler class to output log messages to the console. We add the simple formatter to the handler, which means that all log messages output by the handler will be formatted using the simple formatter.

You can define multiple formatters in your logging configuration and specify which formatter should be used by which handlers. This allows you to customize the appearance of log messages based on your needs. </p>
 
 <h3> MANAGERS.PY </h3>
 # managers.py
from django.db import models

class CustomManager(models.Manager):
    """
    A custom manager for the MyModel model.
    """
    def get_queryset(self):
        # Override the get_queryset method to filter out inactive objects
        return super().get_queryset().filter(is_active=True)

class AnotherCustomManager(models.Manager):
    """
    Another custom manager for the MyModel model.
    """
    def get_queryset(self):
        # Override the get_queryset method to filter out objects with a specific condition
        return super().get_queryset().filter(condition=True)
 <p>n Django, managers.py is a file that defines custom managers for models. A manager is an interface through which database query operations are provided to Django models.

In the example above, we define two custom managers CustomManager and AnotherCustomManager for a model MyModel. These managers override the get_queryset method to filter out objects based on certain conditions.

The CustomManager filters out inactive objects, and the AnotherCustomManager filters out objects with a specific condition.

You can then use these custom managers in your models like this:

python
Copy code
# models.py
from django.db import models
from.managers import CustomManager, AnotherCustomManager

class MyModel(models.Model):
    # Model fields
    is_active = models.BooleanField(default=True)
    condition = models.BooleanField(default=False)

    # Custom managers
    custom_manager = CustomManager()
    another_custom_manager = AnotherCustomManager()
You can then use the custom managers to query the model like this:

python
Copy code
# Query using the custom manager
active_objects = MyModel.custom_manager.all()

# Query using the another custom manager
objects_with_condition = MyModel.another_custom_manager.all()
Custom managers provide a way to encapsulate complex query logic and make it reusable across your application. They are a powerful tool in Django's ORM and can help you write more efficient and readable code. </p>


<h3> DJOSER </h3>
<p>Djoser is a set of Django REST Framework views and serializers that provide a simple and customizable user registration and authentication system. It includes views for user registration, login, logout, password reset, and account activation.

In the example above, we define two views UserList and UserDetail that use Djoser's UserSerializer to handle user registration and authentication. The UserList view allows users to register and view a list of all users, while the UserDetail view allows users to view and update their own user information.

Djoser provides a simple and flexible way to add user registration and authentication to your Django REST Framework application. It is highly customizable and can be easily integrated with other Django apps and third-party services.

To use Djoser in your Django project, you need to add it to your INSTALLED_APPS setting and include its URLs in your project's urls.py file. You can then use Djoser's views and serializers in your own views and serializers to handle user registration and authentication.</p>



