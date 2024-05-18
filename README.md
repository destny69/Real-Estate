# Real-Estate
A Real estate web application based on advance python



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

