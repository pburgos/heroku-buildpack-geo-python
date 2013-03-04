Heroku buildpack: Python
========================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for Python apps, powered by [pip](http://www.pip-installer.org/).

[![Build Status](https://secure.travis-ci.org/heroku/heroku-buildpack-python.png?branch=master)](http://travis-ci.org/heroku/heroku-buildpack-python)

Usage
-----

Example usage:

    $ ls
    Procfile  requirements.txt  web.py

    $ heroku create --stack cedar --buildpack git://github.com/caffeinehit/heroku-buildpack-geo-python.git

    $ git push heroku master
    ...
    -----> Fetching custom git buildpack... done
    -----> Python app detected
    -----> No runtime.txt provided; assuming python-2.7.3.
    -----> Preparing Python runtime (python-2.7.3)
    -----> Installing Distribute (0.6.34)
    -----> Installing Pip (1.2.1)
    -----> Found geo dependency: Proj4 4.8
           Fetching ...
           Unpacking ...
           Installing ...
    -----> Found geo dependency: GEOS 3.3.5
           Fetching ...
           Unpacking ...
           Installing ...
    -----> Found geo dependency: GDAL 1.9.1
           Fetching ...
           Unpacking ...
           Installing ...
    -----> Installing dependencies using Pip (1.2.1)
           Downloading/unpacking Flask==0.7.2 (from -r requirements.txt (line 1))
           Downloading/unpacking Werkzeug>=0.6.1 (from Flask==0.7.2->-r requirements.txt (line 1))
           Downloading/unpacking Jinja2>=2.4 (from Flask==0.7.2->-r requirements.txt (line 1))
           Installing collected packages: Flask, Werkzeug, Jinja2
           Successfully installed Flask Werkzeug Jinja2
           Cleaning up...

You can also add it to upcoming builds of an existing application:

    $ heroku config:add BUILDPACK_URL=git://github.com/heroku/heroku-buildpack-python.git

The buildpack will detect your app as Python if it has the file `requirements.txt` in the root. 

It will use Pip to install your dependencies, vendoring a copy of the Python runtime into your slug. 

Specify a Runtime
-----------------

You can also provide arbitrary releases Python with a `runtime.txt` file.

    $ cat runtime.txt
    python-3.3.0
    
Runtime options include:

- python-2.7.3
- python-3.3.0
- pypy-1.9 (experimental)

Specify Geo Libraries
---------------------

You can specify which libraries should be downloaded by creating a
`geo-python.txt` file. All available libraries are listed here

    $ cat geo-python.txt
    proj4
    proj4-datumgrid
    geos
    gdal

Geographic libraries are installed into `/app/vendor/$library`:

    $ heroku run ls /app/vendor
    gdal-1.9  geos-3.3  proj-4.8
    
    
