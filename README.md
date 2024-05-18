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

