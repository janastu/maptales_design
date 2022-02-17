# About
This repository contains design documents for the maptales project. Maptales is an app that allows location-based
narratives to be consumed. The idea is that media can be created in the MPTL format ( a format we have designed ),
then the player will play the media and will open parts of the media based on the location of the user. When the
user is close to a location, particular media might open. Based on their choices in the media, the user might be 
given goals, of places to visit or go to and that will in turn trigger more nodes of the narrative to open.

# MPTL File
MPTL is a zip file that has been renamed .mptl and contains the following files:

    * cover.json - a JSON file with title, sub-title, cover page image, author, tags and other meta information
    about the MPTL file
    * nodes.json - a JSON file with all the data for the stories.
    * index.html - the main file opened by the player
    * css/ - directory with css files which can be included into each node
    * js/ - directory with javascript files which can be included into each node
    * img/ - directory with images which can be included into each node
    * vid/ - directory with videos which can be included into each node
    * aud/ - directory with audios which can be included into each node

# cover.json
The cover.json file has the following format

```json
{
    "title": "Title of the maptale",
    "subTitle": "Sub-title of the maptale",
    "author": "Author of the maptale",
    "pubDate": "2022-02-17T15:39:30+0530",
    "version": "0.1.0",
    "coverImage": "img/cover.png",
    "tags": [ "adventure", "beginners", "story" ]
}

```

# nodes.json
The nodes.json file has the following evolving format.

```json
[
{
    "id": 1,
    "content": "<div>HTML content</div>",
    "script": "console.log('javascript function')",
    "css": "div { color: red; }",
    "location": {
        "type": "Feature",
        "geometry": {
            "type": "Point",
            "coordinates": [ 77.4242413, 13.084221 ]
        },
        "properties": {
            "radius": 20.0
        }
    }
}
]
```

# App
The app is written in Flutter and can be found in the [maptales_player](janastu/maptales_player) repository. The app
has an embedded WebView and plays the contents of index.html in the .mptl file. It uses routing to switch between nodes.
We are currently experimenting with React Router to provide navigation between the various nodes. So the page it 
navigates to is index.html#/node_id . Where `node_id` is the node id provided in the nodes.json file. If an id isn't
provided it assumes the id = 0 which is the start node of the story. This start node displays information about the 
game and directs players to where the start of the game is. Players will have to move to within the start of the 
first node and then the game will begin.
