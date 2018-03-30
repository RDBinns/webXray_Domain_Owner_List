# webXray Domain Owner List

Drawn from the [webXray project](https://github.com/timlib/webXray), this list provides a hierarchical accounting of what entities own commonly found third-party domains on the web.  The goal of making this list separate from the main [webXray](https://github.com/timlib/webXray) codebase is to create a free, independent, community-driven, and comprehensive list which may be used for a variety of tasks in the privacy and compliance space.  Simply put, this data serves a public good, and community involvement is required to keep the list current.

# Structure of the List

The list is a JSON file.  Each entry in the list has the following fields:

* __id__: a numeric identifier (integer) for the entry, this will change whenever the list is expanded and reindexed, do not count on it remaining stable

* __parent_id__: if the entity has a parent owner, the id of the parent

* __owner_name__: a string which is the name of the service (eg. 'Google Analytics') or the company ('Google') which owns the domain
	
* __aliases__: an array of strings representing possible alternate spellings of the owner_name (eg. 'YouTube' and 'You Tube')
	
* __homepage_url__: a string which is the url of the homepage of the service or company
	
* __privacy\_policy\_url__: a string which is the url of the privacy policy of the service or company
	
* __notes__: a string which has pertinent information as to why a domain was assigned to a given owner
	
* __country__: the ccTLD for the country in which the service or company is based
	
* __domains__: an array of domian names (strings) which are owned by the given service or company

# Using the List

JSON was chosen as the format for this list in order to make it highly portable.  If you would like to see an example of how to use the list, please examine the [webxray](https://github.com/timlib/webXray) source code, particularly the [__Analyzer.py__](https://github.com/timlib/webXray/blob/master/webxray/Analyzer.py) class.  Otherwise, feel free to include it in your own projects (per the terms of the license).

# Contributing

There are three ways to contribute: filling in missing data, adding new domains to existing owners, and adding new owners and their domains.

## Filling in Missing Data

There are two major items which are frequently missing in this list: homepage\_url and privacy\_policy\_url.  One way to contribute is to simply find this information and add it in the appropriate places in the existing file.

## Adding New Domains to Existing Domain Owners

Have you found a new domain not in the list?  Is the owner already in the list?  If so, simply add the domain to the domains array and reindex the list (details below).

## Adding New Owners

Have you found a new domain and the owner is not in the list?  If so, you have extra work to do!  

First, make sure you have found all the relevant data for the owner (name, aliases, homepage url, privacy policy url, country, and domains).  Next, paste the following blank entry at the end of the list, but before the closing ']'.

	,{
		"id"				 : MANUALLY_ADD_NEXT_ID_NUMBER,
		"parent_id"			 : null,
		"owner_name"		 : "",
		"aliases"			 : [],
		"homepage_url"		 : null,
		"privacy_policy_url" : null,
		"notes"				 : null,
		"country"			 : null,
		"domains"			 : []
	}
	
Replace the text 'MANUALLY\_ADD\_NEXT\_ID\_NUMBER' with a number which is one higher than the last item in the list (eg if the last item is 100 you should use 101).  Do not put the new id number in quotes, that will create errors.  Next, paste in your new info in the appropriate spaces in the blank entry.  Double check it looks like the other entries, and check for mistakes.

Finally, entering a new owner is not the end of the task, you must also determine if your new entry has a parent owner.  The Crunchbase website is an excellent resource to determine if a given company has been acquired by a larger entity.  If so, check if the parent is already in the list, if so, enter the correct parent\_id and you are done.  

If the parent is not in the database, you must add it using the steps above.  In some cases you will only know the homepage of the parent, in such cases it is fine to have a single entry for the domains array which is the domain of the parent's homepage.

## Reindexing the List

If you have made changes to the list, use Python 3 to run the reindex\_domain\_owners.py script.  It will assign new identifiers and alphabetize the list and the domains.  If you made a mistake in entering the data, the reindexing will crash when attempting to read the file.  If this happens, check to find your mistake.  

Once the list is reindexed you may submit your changes to this repository and they will be checked over for accuracy before being added.