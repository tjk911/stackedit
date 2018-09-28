A very basic scraper that checks the Spokane county inmate roster daily, and then matches it with a spreadsheet maintained by SR staff to see if the newsroom needs to be notified.

It's been helpful for reporting in the past when reporter wants to cross-reference booking and release times, or when we get notified of significant persons in our community being booked.

It's imperfect though - right now we're manually setting the payload to trigger the switch to `Recently released` and `Recently booked` pages, and that payload changes every now and then and will trigger failure alerts (send through Slack).

## Where does it live

It currently lives on Panda2.0, aka Wakanda, under `kteoh/jailscraper`

## Long term goals

It'd be good to pipe the data into Panda (not to be confused with Pandas, the dataframe library) or some other easily queryable database. Right now the files are living locally on the server.

Adding fuzzy matching would be good as well, and work is in progress to add csvmatch functions into it. It's a little tricky since that library was built as a CLI tool.

_Why not fuzzy wuzzy instead of csvmatch?_

Fuzzy wuzzy only does Levenshtein matching - which checks for character distance. 

Levenshtein would check for `address` and `adresse`. 

But csvmatch has double metaphone built in, which checks for phonetic sounds and would provide a better fuzzy matching system than simply Levenshtein. It might bring up more false positives, but we can tweak that.

For example, double metaphone would convert `michael` into `['MKL', 'MXL']`

Csvmatch also has the Bilenko method built in, which is a machine learning algorithm. That'd be far longer term as we'd need to teach it to remember (csvmatch wasn't build to remember).

## The jailscraping process

There's a cronjob that runs every morning, and it runs the `combo.py` and `checkmatch.py` files.

`combo.py` hits the inmate roster page, and scrapes through their three separate pages, cleans it up, and saves it on our server. 

The **full_list** will always scrape fine. But **recently released** and **recently booked** could have issues if the payload has changed.

If any of the page scraping fails, it'll send a Slack message. Currently it's targeted specifically at me, this can be modified to any channel (it's the `parse_content` function).

`checkmatch.py` checks for matches and notifies set emails about it when there are matches. Currently, these are the people notified

* Kai Teoh
* Rachel Alexander
* Chad Sokol
* Eli Francovich
* Ryan Collingwood
* Jonathan Glover

This script is highly imperfect - it currently logs into my (read: Kai's) email account to send out the emails. This means it needs to be updated every 90 days as passwords expire, and the passwords are not stored securely (I know, I know).

There's no fuzzy matching, and if I remember correctly some weird transformations are done either in `combo.py` or here in order to try and sanitize the text before matching. This is part of why adding csvmatch is important.

If email errors out, it'll send a slack message as well - currently directly to me (read: Kai).

## Other libraries supporting the app

**exchange.py** - We're running Microsoft's exchangelib in order to access an email account to send out an email.

**google.py** - We're running google's library(ies) to oauth into Google Spreadsheet, parse through it and spit it back out for matching purposes. It's read_only.

**message.py** - We're using Slack's library(ies) to send Slack messages. 

## Other stuff/ideas

It's a messy folder, with a lot of old scripts or WIP scripts. Tread carefully for now, it's on my to-do list to clean it up and rewrite it properly.

We could also Pandas it all into a singular dataframe and pipe it into one collected spreadsheet. Might be able to do some data analysis right off the bat there.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5MTI0NzAzNTZdfQ==
-->