==============================
Basic blog with djangocms-blog
==============================

basic setup for djangocms-blog with Django 2.2, 3 or 3.1

Enabled features:

* Autosetup
* SEO Meta tags
* Taggit

------------------
Run from this repo
------------------

* clone the repo: ``git clone git@github.com:yakky/djangocms-blog-poc.git && cd djangocms-blog-poc``
* create a virtualenv: ``python3.7 -mvenv .venv && . .venv/bin/activate``
* update pip to make sure you are on an up-to-date version: ``pip3 install setuptools-scm  # required by haystack``
* install requirements according to the desired django version:

  * ``pip3 install -r requirements-2.2.txt``
  * ``pip3 install -r requirements-3.0.txt``
  * ``pip3 install -r requirements-3.1.txt``
* create database: ``python manage.py migrate``
* create superuser: ``python manage.py createsuperuser --username=admin``
* run the site: ``python manage.py runserver``


---------------------
Recreate from scratch
---------------------

* create a site dir: ``mkdir mysite && cd mysite``
* create a virtualenv: ``python3.7 -mvenv .venv && . .venv/bin/activate``
* install djangocms-installer: ``pip install djangocms-installer``
* create django CMS site: ``djangocms -p poc  --django-version=stable --cms-version=3.8 blog`` (or ``djangocms -p poc  --django-version=3.0 --cms-version=stable blog`` for django 3.0)
* enter new site: ``cd poc``
* edit settings as below
* update pip to make sure you are on an up-to-date version: ``pip3 install setuptools-scm  # required by haystack``
* install requirements: ``pip3 install djangocms-blog``
* make sure its dependencies are installed: ``pip3 install aldryn-search djangocms-bootstrap4 djangocms-file djangocms-googlemap djangocms-icon djangocms-link djangocms-picture djangocms-snippet djangocms-style djangocms-text-ckeditor djangocms-video``
* create database ``python manage.py migrate``
* run the site ``python manage.py runserver``
* login with user ``admin`` (password: ``admin``)

Blog settings
#############

The settings below assume a djangocms-installer website as many settings are already set by djangocms-installer

* Add the following applications to ``INSTALLED_APPS`` after ``easy_thumbnails`` in ``blog/settings.py``::

    'aldryn_apphooks_config',
    'parler',
    'taggit',
    'taggit_autosuggest',
    'meta',
    'sortedm2m',
    'djangocms_blog',

* Add the following settings at the bottom of ``blog/settings.py``::

    META_SITE_PROTOCOL = 'http'
    META_USE_SITES = True

    META_USE_OG_PROPERTIES=True
    META_USE_TWITTER_PROPERTIES=True
    META_USE_SCHEMAORG_PROPERTIES=True

* Add taggit urlconf in ``blog/urls.py``::

    urlpatterns += i18n_patterns(
        url(r'^admin/', admin.site.urls),  # NOQA
        url(r'^taggit_autosuggest/', include('taggit_autosuggest.urls')),
        url(r'^', include('cms.urls')),
    )
