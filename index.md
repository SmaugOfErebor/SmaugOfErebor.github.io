## Code Review

Click [here](./Media/CodeReview.html) to watch the code review.

This code review highlights:
1. The existing functionality before any enhancements were applied
2. A code analysis focusing on structure, logic, efficiency, security, and documentation.
3. The three enhancements that were planned in the following areas:
	- Software engineering and design
	- Algorithms and data structure
	- Databases

## Enhancement 1 - Software Engineering and Design

For this enhancement, I took the first step toward improving the search functionality. Before this enhancement, searching for a campsite would only succeed for an exact match. When a match was found, that match would be opened in its own activity to view information about it. When the search failed, only a failure message appeared as shown below:

![Old Search Failure](https://raw.githubusercontent.com/SmaugOfErebor/SmaugOfErebor.github.io/master/Media/OldSearchFail.png)

This is not the behavior a typical user would expect. Convention is that when searching for anything, a list is returned with the most relevant results at the top of the list. To make progress toward this behavior, I made a new activity in the app that displays any given list of campsite objects.

To accomplish this, I had to create a custom list adapter. Essentially, I had to tell my app how to convert a single campsite object into a list view item. The app needed to know which pieces of information to extract from the object and what type of control would display that information.

At this point, searching still only succeeded with an exact match, but the foundation had been laid for searching to return a list of campsites to be displayed. The campsite result list view as it stands at the end of this enhancement is shown below:

![New Search Success](https://raw.githubusercontent.com/SmaugOfErebor/SmaugOfErebor.github.io/master/Media/NewSearchSuccess.png)

The complete list of changes and a full diff of the code can be found [here](https://github.com/SmaugOfErebor/CampsiteLocator/commit/f10ca31b90846a4cee252e6713d31cf5352ba210).

## Enhancement 2 - Algorithms and Data Structure

For this enhancement, I built upon the search result list view created in the first enhancement. Now that I had a list view, I needed to fill it. I developed an algorithm to perform a fuzzy search based on the campsite name as a search criteria. The algorithm creates and executes multiple SQL queries to expand the search results, providing the expected behavior to the user.

The algorithm determines n-grams to be used and creates queries based on those n-grams. The result is a list of results with an exact match at the top, with results containing an exact match of an individual word below that, and with results containing matches of misspelled words below that. The new results in the list view using the search criteria "Colorado Camp" are shown below:

![New Search Results](https://raw.githubusercontent.com/SmaugOfErebor/SmaugOfErebor.github.io/master/Media/NewSearchResults.png)

The new results in the list view using the incorrectly spelled search criteria "Goergia" are shown below:

![Typo Search Results](https://raw.githubusercontent.com/SmaugOfErebor/SmaugOfErebor.github.io/master/Media/TypoSearchResults.png)

The complete list of changes and a full diff of the code can be found [here](https://github.com/SmaugOfErebor/CampsiteLocator/commit/1fd988dea1f880fd8675cb40c7f51dd0a8d02d2b).

## Enhancement 3 - Databases

For this enhancement, I expanded on and improved the search functionality. After implementing the fuzzy search in the second enhancement, the app had to make many queries to the database to compile results. To improve this shortcoming, I used the SQL OR operator to combine as many queries as I could. There are still multiple queries being made, but the number is significantly reduced.

Additionally, I enabled more criteria to search the database with. Searching can now be done not only by name, but by state and by city as well. Determining the order I wanted to return results in and actually making that happen were the biggest challenges during this enhancement. My priority for search results was based on the selected state. I imagine that a user using this app would likely have a better idea of the location they want to camp in than the name of the campsite. A user would likely think, "I want to go camping this weekend" but probably not, "I wonder what state I want to camp in this weekend." If a user knows the name of a campsite they wish to visit, they probably have a good idea of which state it is in.

I also used the same fuzzy search functionality developed in the last enhancement on the city search criteria. There is no priority difference between the campsite name and the campsite city. This is because both of those search criteria are entered by the user where spelling errors can be expected. For the state search criteria, the string will be spelled correctly as they are all hardcoded in my strings.xml file (and if anything was spelled incorrectly, that would be my fault).

The new results in the list view using the incorrectly spelled search criteria "Goergia", the state Arkansas, and the city Portsmouth are shown below:

![Multi Search Results](https://raw.githubusercontent.com/SmaugOfErebor/SmaugOfErebor.github.io/master/Media/MultiSearchResults.png)

The state criteria is prioritized over all else, so the Arkansas camp displays first. Second in this list is the result containing a misspelled version of the word Georgia.

The complete list of changes and a full diff of the code can be found [here](https://github.com/SmaugOfErebor/CampsiteLocator/commit/eac2779f8ebb94a39c37d7131050d4f123ae4da2).