Facebook JS SDK, tracked and de-minified
===================================================

This project aims to provide a useful resource to developers who are working with 
Facebook's JS SDK and would like to see what has changed recently. 

My server runs a cronjob every 10 minutes that downloads the latest 
http://connect.facebook.net/en_US/all/debug.js, commits any changes, and then pushes to 
github. 

(debug.js is the non-minified version of http://connect.facebook.net/en_US/all.js that 
you're probably using in production.)

The script does not commit if only the timestamp at the top has changed.

---

Setup
-----

To run your own copy (which I recommend), you'll need to fork the github project, test the shell script, and then 
set up cronjob like so:

    MAILTO="you@[your_site].com"
    # m h dom mon dow command
    0 5 * * * /home/nfriedly/facebook/connect-js/update_fb_github.sh > /dev/null

This setup sends an email if there were errors, but not if everything worked successfully.

Setup on Heroku
---------------

Alternatively, I have been testing running this script on a free heroku instance, and it seems to be working now.
To use heroku, put your github username and password in environmental variables like so:

    heroku config:add GH_USER=<username>
    heroku config:add GH_PASS=<password>
    
Then add the [Heroku Scheduler](https://addons.heroku.com/scheduler) addon and create a task that runs `./heroku.sh` as often as you'd like.

---

Official FB links
-----------------

**Documentation for the JavaScript SDK:** 

* http://developers.facebook.com/docs/reference/javascript/

**Bug Tracker:** 

* https://developers.facebook.com/bugs 

**Recent Changes & Current Status:**

* Change Log: https://developers.facebook.com/docs/changelog/
* Platform Live Status: https://developers.facebook.com/live_status
* JSON feed of current push status and most recent Platform Live Status issue: https://www.facebook.com/feeds/api_status.php

**Upcomming & Long-term Changes:** 

* Code that will be released within a day or two -- be sure to label any bugs as BETA: https://developers.facebook.com/support/beta-tier/
* Developer Blog: https://developers.facebook.com/blog/
* Platform Roadmap: https://developers.facebook.com/roadmap/

---

To Do
-----

* Track individual components (init.js, json.js, xfbml.js, etc)
* Keep a copy of the minified file in addition to debug.js
* Track the xdm.swf file
* Track the beta js
* Figure out how to get error notifications if the heroku process fails

---

Credits
-------

Credit for the idea goes to Roger Hu - http://hustoknow.blogspot.com/

The shell scripts are copyright Nathan Friedly http://nfriedly.com and released under an MIT License.

The JS is copyright Facebook, Inc. and, to the best of my knowledge, released under an Apache 2.0 License

This is obviously not endorsed or supported by Facebook - if it was, they'd probably update their own github account.
