

A really simple and easy way to add additional context into any individual pages or entire groups of pages. 

It lets you add a simple key-value pair when needed.

**!Caution!** - Context adder is very barebones. It excels at what it does, but keep in mind that over reliance on this might make future maintenance problematic. 

We're essentially splitting out our code and logic into various places beyond just the codebase, there's the distinct possibility that we might reach a day where we look back wondering "Where the hell is this logic/context being overwritten/changed?"

## How it works

The admin is fairly straightforward.

* *Name* - Descriptive name that explains what context we're adding  
* *Sites* - Context adder needs to know which site we're applying this to, just pick the domain that matches  
* *Pattern* - This can be [regex](https://www.regexbuddy.com/regex.html) if we need some form of pattern matching logic, or it can be a partial URL sans domain (for example: `/stories/2018/mar/01/apple-detective-finds-five-more-apple-varieties-th/`)  
* *Added key* - This is the key (or name, really) of the context we'd like to add.   
* *Added value* - The value of said key/name we'd like to add.   

An example of removing **network ads** from a story page would look like this  
  
> *Name*: Network ad removal for apple detective story  
> *Sites*: www.spokesman.com  
> *Pattern*: `/stories/2018/mar/01/apple-detective-finds-five-more-apple-varieties-th/`  
> *Added key*: `no_network_ads`  
> *Added value*: `True`  



## General list of used context

This is not an exhaustive list by any means, but these are some of the known contexts being used in some templates.

|key             |value                          |effect                       
|----------------|-------------------------------|-----------------------------
|no_ads			 |Boolean (True/False)           |Strips all ads from page
|no_network_ads  |Boolean (True/False)           |Strips network ads from page 


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYxNjk0Nzc0Nl19
-->