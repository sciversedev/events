
This repository contains the (tidied up) code from my entry for the Elsevier
SciVerse challenge at JISC Dev8D 2011.

http://wiki.2011.dev8d.org/w/Bounties#Web2.0_Apps_for_Science_-_Elsevier

Sam Adams
sea36@cam.ac.uk


== SciVerse Search API ==

I (and other competitors in the SciVerse challenge) found that there is quite
a high barrier to getting started developing SciVerse apps, due in part to the
relatively complex API. After getting fed up fighting with the API I created a
much simpler client API, which hides the complexities of the SciVerse API,
leaving app developers free to focus on the content of their applications.

Source: api/sciverse_search.js 

Usage:

var sciverse = new SciverseSearch();
sciverse.setSearchCluster(SciverseSearch.Cluster.SCIDIR);
sciverse.setView(SciverseSearch.View.COMPLETE);
sciverse.setResultCount(25);
sciverse.setStartOffset(100);
sciverse.setSearchCompleteCallback(function() {
	for (var i = 0; i < sciverse.results.length; i++) {
		var entry = sciverse.results[i];
		
		// do something with entry
	}
});
sciverse.execute(query);


Note:

User prefs must be initialised by including the following in the
gadget configuration, and specifying the gadget's API Key.

<Module>
	<ModulePrefs ... </ModulePrefs>

	<UserPref name="secureAuthtoken" datatype="hidden" />
	<UserPref name="contentApiKey" datatype="hidden" default_value="-- put api key here --" />

	...
</Module>



== Sample Apps ==

The gadgets/ directory contains a number of sample applications:

* gadgets/debugcontext.xml

	Adds a 'debug' panel that displays the current application context.
	
	
* gadgets/googlenews.xml

	Adds a news panel, that carries out a Google News search on the current
	ScienceDirect or Hub search terms, and displays the five most relevant
	headlines.


* gadgets/searchmetrics.xml

	Adds a search assistant panel that fetches the first 150 results for the
	current ScienceDirect of Hub search terms, and generates a plot of the
	number of papers published per year from that set, and identifies the
	ten authors with the most papers amongst the results.
