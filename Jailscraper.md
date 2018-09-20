---


---

<p>A very basic scraper that checks the Spokane county inmate roster daily, and then matches it with a spreadsheet maintained by SR staff to see if the newsroom needs to be notified.</p>
<p>It’s been helpful for reporting in the past when reporter wants to cross-reference booking and release times, or when we get notified of significant persons in our community being booked.</p>
<p>It’s imperfect though - right now we’re manually setting the payload to trigger the switch to <code>Recently released</code> and <code>Recently booked</code> pages, and that payload changes every now and then and will trigger failure alerts (send through Slack).</p>
<h2 id="where-does-it-live">Where does it live</h2>
<p>It currently lives on Panda2.0, aka Wakanda, under <code>kteoh/jailscraper</code></p>
<h2 id="long-term-goals">Long term goals</h2>
<p>It’d be good to pipe the data into Panda (not to be confused with Pandas, the dataframe library) or some other easily queryable database. Right now the files are living locally on the server.</p>
<p>Adding fuzzy matching would be good as well, and work is in progress to add csvmatch functions into it. It’s a little tricky since that library was built as a CLI tool.</p>
<p><em>Why not fuzzy wuzzy instead of csvmatch?</em></p>
<p>Fuzzy wuzzy only does Levenshtein matching - which checks for character distance.</p>
<p>Levenshtein would check for <code>address</code> and <code>adresse</code>.</p>
<p>But csvmatch has double metaphone built in, which checks for phonetic sounds and would provide a better fuzzy matching system than simply Levenshtein. It might bring up more false positives, but we can tweak that.</p>
<p>For example, double metaphone would convert <code>michael</code> into <code>['MKL', 'MXL']</code></p>
<p>Csvmatch also has the Bilenko method built in, which is a machine learning algorithm. That’d be far longer term as we’d need to teach it to remember (csvmatch wasn’t build to remember).</p>
<h2 id="the-jailscraping-process">The jailscraping process</h2>
<p>There’s a cronjob that runs every morning, and it runs the <code>combo.py</code> and <code>checkmatch.py</code> files.</p>
<p><code>combo.py</code> hits the inmate roster page, and scrapes through their three separate pages, cleans it up, and saves it on our server.</p>
<p>The <strong>full_list</strong> will always scrape fine. But <strong>recently released</strong> and <strong>recently booked</strong> could have issues if the payload has changed.</p>
<p>If any of the page scraping fails, it’ll send a Slack message. Currently it’s targeted specifically at me, this can be modified to any channel (it’s the <code>parse_content</code> function).</p>
<p><code>checkmatch.py</code> checks for matches and notifies set emails about it when there are matches. Currently, these are the people notified</p>
<ul>
<li>Kai Teoh</li>
<li>Rachel Alexander</li>
<li>Chad Sokol</li>
<li>Eli Francovich</li>
<li>Ryan Collingwood</li>
<li>Jonathan Glover</li>
</ul>
<p>This script is highly imperfect - it currently logs into my (read: Kai’s) email account to send out the emails. This means it needs to be updated every 90 days as passwords expire, and the passwords are not stored securely (I know, I know).</p>
<p>There’s no fuzzy matching, and if I remember correctly some weird transformations are done either in <code>combo.py</code> or here in order to try and sanitize the text before matching. This is part of why adding csvmatch is important.</p>
<p>If email errors out, it’ll send a slack message as well - currently directly to me (read: Kai).</p>
<h2 id="other-libraries-supporting-the-app">Other libraries supporting the app</h2>
<p><strong><a href="http://exchange.py">exchange.py</a></strong> - We’re running Microsoft’s exchangelib in order to access an email account to send out an email.</p>
<p><strong><a href="http://google.py">google.py</a></strong> - We’re running google’s library(ies) to oauth into Google Spreadsheet, parse through it and spit it back out for matching purposes. It’s read_only.</p>
<p><strong><a href="http://message.py">message.py</a></strong> - We’re using Slack’s library(ies) to send Slack messages.</p>
<h2 id="other-stuffideas">Other stuff/ideas</h2>
<p>It’s a messy folder, with a lot of old scripts or WIP scripts. Tread carefully for now, it’s on my to-do list to clean it up and rewrite it properly.</p>
<p>We could also Pandas it all into a singular dataframe and pipe it into one collected spreadsheet. Might be able to do some data analysis right off the bat there.</p>

