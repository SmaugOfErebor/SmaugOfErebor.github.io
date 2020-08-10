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

## Enhancement 3 - Databases