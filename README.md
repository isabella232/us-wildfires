us-wildfires
============

Projections
-----------

why we do the reprojections the way we do: http://trac.osgeo.org/proj/wiki/FAQ#ChangingEllipsoidWhycantIconvertfromWGS84toGoogleEarthVirtualGlobeMercator

Install requirements
--------------------

Node.js is required for the static asset pipeline. If you don't already have it, get it like this:

```
brew install node
curl https://npmjs.org/install.sh | sh
```

Then install the project requirements:

```
cd $NEW_PROJET_NAME
npm install less universal-jst
mkvirtualenv $NEW_PROJECT_NAME
pip install -r requirements.txt
```

Install server requirements
---------------------------

```
sudo apt-get install build-essential libwebkit-dev unzip
sudo add-apt-repository ppa:developmentseed/mapbox
sudo apt-get update
sudo apt-get install tilemill
sudo add-apt-repository ppa:ubuntugis/ppa
sudo apt-get update
sudo apt-get install gdal-bin
```

Adding a template/view
----------------------

A site can have any number of rendered templates (i.e. pages). Each will need a corresponding view. To create a new one:

* Add a template to the ``templates`` directory. Ensure it extends ``_base.html``.
* Add a corresponding view function to ``app.py``. Decorate it with a route to the page name, i.e. ``@app.route('/filename.html')``
* By convention only views that end with ``.html`` and do not start with ``_``  will automatically be rendered when you call ``fab render``. 

Run the project locally
-----------------------

A flask app is used to run the project locally. It will automatically recompile templates and assets on demand.

```
workon $NEW_PROJECT_NAME
python app.py
```

Visit ``localhost:8000`` in your browser.

Compile with static assets
--------------------------

Compile LESS to CSS, compile javascript templates to Javascript and minify all assets:

```
workon $NEW_PROJECT_NAME
fab render 
```

(This is done automatically whenever you deploy to S3.)

Test the rendered app
---------------------

If you want to test the app once you've rendered it out, just use the Python webserver:

```
cd www
python -m SimpleHTTPServer
```

Deploy to S3
------------

```
fab staging master deploy
```

Deploy to a server
------------------

The current configuration is for running cron jobs only. Web server configuration is not included.

* Run ``fab staging master setup`` to configure the server.
* Run ``fab staging master deploy`` to deploy the app. 

Rendering the map
-----------------

To render the map locally:

```
fab local_render_map
```

To render the map on the server, you must first define the environment variable ``MAPBOX_SYNC_ACCESS_TOKEN_WILDFIRES``. Then run:

```
TODO
```

To cron render map on the server:

```
TODO
```
