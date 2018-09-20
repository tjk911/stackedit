
== CommuniMaps! (catch the fever) ==

The sites we built to handle Garage Sales and Open Houses for the classifieds department are in the CommuniMaps app inside of Cannonball. The classifieds department owns a couple urls like spokesmangaragesales.com or something, but those just redirect to [http://maps.spokesman.com/ where we actually serve the sites from].

### Code and importers

The Communimaps app is pretty well documented with docstrings and comments. It operates somewhat like SportsTeam, where a few base models are inherited and customized for the specific content type (so Garage Sales stay nice and simple, but Open Houses can have fields for Bedrooms, Bathrooms, etc.)

There's a TEMPLATE_OPTIONS dict at the top of each models file, which passes some context vars along so that the templates can remain nice and generic. The urls.py for each content type calls a `patterns_for_subsection` function from a base set of urls, so you don't have to define anything special there. This app is something we would have done in a class-based way, if that had been available at the time ;)

But as it is, spinning up a new content type into this kind of framework is pretty simple. Just look at models.garage_sales for a simple implementation, and then at models.open_houses for one that does a little bit more. You basically need three things:

- a new file in the /models dir, defining the TEMPLATE_OPTIONS and inheriting the base models
  - note that your new model that inherits from base.MapItemDate should have a @classmethod returning `template_options`. This lets you add model information to that dict, and that's what your app-specific urls file needs to get.
- a new file in the /urls dir, likely doing nothing more than calling `patterns_for_subsection`
- an importer for the data, with requisite task in tasks.py

Right now, Garage Sales comes from a csv that gets manually uploaded by someone in classifieds, and Open Houses comes in automatically from the AdPerfect system. You can find the import scripts in the /importers dir, and these get triggered every 1/2 hour by tasks in tasks.py. (So if things are failing, it might just be that celery needs a restart.)

### Error emails

There are a couple places where success/error emails are generated, and I'm switching them over to point to ginab and mikeha. It's pretty rare that errors happen, but I do have to check on something once in a while.

One email to watch for will have a subject like: [Django] Communimaps: failed to get numeric price (ID %s)

We try to convert the "List Price" field that the sales reps enter -- e.g. $127,000 -- to a "Numeric Price" integer so that the search filtering can rank by price appropriately. But once in a while, the rep will enter something abnormal into that field, and this error will trigger. There will be a link inside that error email that goes directly to the admin record with the problem.

Here's one where it worked properly:

- http://www.spokesman.com/sradmin/communimaps/openhouse/15488/
- List price: $335,000
- Numeric price: 335000

I hardly get any error alerts any more, because we've tweaked the "Numeric Price" converter to handle all the weird stuff they tend to do. These days, 95% of the time the error emails are triggered because they enter a price that simply *can't* be converted to an integer worth sorting. Like they'll put in a rental rate: "$850/month." In that case, there's no good way to represent that price for search, so just delete the error email and move on. If there *is* a "List Price" that you can eyeball and see what weird character they included that broke things, just fix that field, manually enter a "Numeric Price," save and that's it.

Like I said, though, hardly ever happens.

### Subdomain URL routing

We use `cannonball.core.middleware.multihost.MultiHostMiddleware` to detect requests to maps.spokesman.com (and to data.spokesman.com and m.spokesman.com, for that matter). The middleware checks against the entries in settings.HOST_MIDDLEWARE_URLCONF_MAP, and if it finds a match, it changes the ROOT_URLCONF appropriately. So a request to `maps.spokesman.com` swaps ROOT_URLCONF to `cannonball.communimaps.urls.base` and everything works like you'd expect.

### Local testing

To get the subdomain routing to work locally, you just need to edit your HOSTS file. I have entries like so:

```
127.0.0.1   m.localhost
127.0.0.1   maps.localhost
127.0.0.1   data.localhost
```

So then I can `python manage.py runserver` and hit `maps.localhost:8000` in my browser.

**Addition by Kai 3/21/18**

In your `docker_settings` file, add this: 
```
ALLOWED_HOSTS +=['m.localhost','maps.localhost','data.localhost']
```

~~In your `docker-compose.yml` file, turn off `DEBUG_TOOLBAR` by setting it to False. Debug toolbar does not work with these subdomains.~~

~~Reminder to double check your `.env` file if you have one, your debug toolbar settings might be enforced there instead of your docker-compose.yml file.~~

Credit goes to Peter C. for figuring this part out:  
  
Add the code below to `code/cannonball/communimaps/urls/base.py` and `code/cannonball/data_projects/urls.py` and it'll enable debug toolbar.  
  
```
if getattr(settings, "DEBUG_TOOLBAR", False):
    import debug_toolbar
    urlpatterns = [
        url(r'^__debug__/',include(debug_toolbar.urls)),
    ] + urlpatterns
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0OTY2MDk4MjldfQ==
-->