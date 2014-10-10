# erlio #

Erlang url shortener project.

## Goals ##
 * webmachine application
 * eunit tests included
 * upgradable via hot code loading
 * web interface
 * gather stats

## Author(s) ##

 * Tim McGilchrist <timmcgil@gmail.com>

## Copyright ##

Copyright (c) 2012 Tim McGilchrist <timmcgil@gmail.com>.  All rights reserved.


### TODO ###

 * main resource that translates short urls to a 302 redirect (DONE)
 * short resource serves up index.html (DONE)
 * write out long form as Markdown
 * tweak css so we see the full path in the UI. (DONE)
 * add goto button on UI to see we get 302 redirect.

 Nice to have:
 * fault tolerance for event handler, how should it's supervisor look, what
   happens when something errors out?
 * generate shorter unique links
 * gen_event calls to tally statistics on how many urls get visited, etc
 * clean up javascript to provide a copy to paste bin implementation
 * deploy to heroku
 * port to use postgres database
 * check whether link already exists and return correct code
 * add support for viewing events generated by the server


## Resources

 * erlio_assets_resource - serves static assets like JS/CSS/HTML. Also gets a
   link and provides a 302 redirect to the correct location
 * erlio_link_resource   -  gets links from the application
 * erlio_links_resource  - creates links from the application
 * erlio_stats_resource  - displays the stats for the application


Basic Structure
===============

erlio_sup
 |
 \--------------------------------------------------
     |                       |                  |
 webmachine_mochiweb    erlio_store        erlio_events

erlio_sup - the main supervisor under which everything lives
webmachine_mochiweb - http / REST resources
erlio_store - datastore that talks to a persistent data store
erlio_events - out of band event processing, gathering statistics
