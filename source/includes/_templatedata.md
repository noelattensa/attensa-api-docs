# Template Data

## Briefing Variables

All the data that is available to templates is provided by the BriefingRenderer class.

### `items` > `item` : 

These are all the items in the briefing, with standard item data, plus the following:

* `{{title}}`: The title of the item.
* `{{link}}`: A link to the content of the item in the Attensa reading view.
* `{{sourceLink}}`: A link to the content's original source.
* `{{author}}`: The full name of the author of the item. 
* `{{defaultDescription}}`: This will display the full text of the item description.
* `{{cleanDescription}}`: This variable will display the same text as defaultDescription with any HTML stripped off.
* `{{shortDescription}}`: This variable will display the same text as cleanDescription with a limitation to 200 characters.
* `{{publishedDate}}`: This will display the item’s published date.

### `stream` : 

* `{{stream.followersCount}}`: A link to the content's original source.
* `{{stream.publishedDate}}`: The full name of the author of the item. 
* `{{itemCount}}`: This will display the full text of the item description.
* `{{indexedStreams}}`: The first level of non-empty streams under a topic, with the following:
* `{{streamID}}`: Returns the stream's ID.
* `{{streamTitle}}`: The title of the item.
* `{{streamDescription}}`: A link to the content of the item in the Attensa reading view.

### `briefing` : 

* `{{briefing.description}}`: The briefing's description.
* `{{viewAsHTML}}`: A link to the HTML version of the briefing.
* `{{totalNewItems}}`: Is the count of items added since the last briefing was sent. 

### Topic View:

* `{{topicView}}`: A link to the topic view.
* `{{indexedTopicView}}`: A link to the new topic view with an index displayed.
* `{{noNavTopicView}}`: A link to the new topic view with no navigation displayed.
* `{{noNavIndexedTopicView}}`: A link to the new topic view with an index, but no navigation displayed.
