# Notion Video Game Gallery

 This script makes tracking videogames with Notion databases more delightful by automatically adding images and metadata about the games you have played or want to play.

It does so by fetching data from various places around the internet ([Steam](https://store.steampowered.com/), [SteamGrid](https://www.steamgriddb.com/), [IGDB](https://www.igdb.com/), [Youtube](https://www.youtube.com/), [HLTB](https://howlongtobeat.com/)) and using the [Notion API](https://developers.notion.com/) to connect it to your database.

If you want to see the results, you can take a look at [a minimalist example](https://adriansteffan.notion.site/288d8bda00e6470f964b746d96b7219c?v=8991ff720345476285cd3b172e3003b4) or [my lovely collection](https://adriansteffan.notion.site/8358e5f496f846a4a4e9ded10d67fa27?v=4578337d13cb4addb6326c85fe4ab539).

The code could still be improved in various places, but c'mon, this bot is trying his hardest to make your game collection shine, who could judge him for being a bit messy?


## Setup

These steps are needed for both deployment and development.

* Clone the repository
* Rename `config.py.template` to `config.py` and enter the following keys:
    * Create a [Steamgrid-API-Key](https://www.steamgriddb.com/profile/preferences/api)
    * Create a [IGDB Client ID and secret](https://api-docs.igdb.com/#account-creation) 
    * Create an application and a [Youtube-API-Key](https://developers.google.com/youtube/v3/quickstart/python)
    * Create an application and a [Notion-API-Key](https://developers.notion.com/docs/getting-started#step-1-create-an-integration)
* Go to the [example page](https://adriansteffan.notion.site/288d8bda00e6470f964b746d96b7219c?v=8991ff720345476285cd3b172e3003b4), `Duplicate` the page, and delete the example entries
* [Share the database](https://developers.notion.com/docs/getting-started#step-2-share-a-database-with-your-integration) you cloned with the Notion application you created and enter the database link into the `config.py`



### Deployment

For the deployment on your Linux machine, you will need both [docker](https://docs.docker.com/engine/install/) and [docker-compose](https://docs.docker.com/compose/install/).

To build the docker image, run 

```
docker-compose build
```

in the root directory.

After completing the setup, start the container with

```
docker-compose up -d
```

Stop the server with

```
docker-compose down
```


### Development (Local)

For development, you will need a [Python3](https://www.python.org/downloads/) installation.

To install the dependencies, run
```
python3 -m pip install -r requirements.txt
```
in the root directory.

To start the script, run

```
python3 main.py
```
in the root directory.

## Usage

Once the script is running (either locally or on your server), head over to the databse that you cloned.
You can load the game data by setting the `Data Fetched` property. Use `Load All` to set properties and page data and use `Load Images` to refetch the icon, cover, and hero in case the links die.

The game will be identified either using the games Steam-ID or its name:

* If the `SteamID` property is set, the game data will be loaded and all other fields will be updated accordingly. If possible/sensible, the images will be taken directly from Steam.
* If no `SteamID` is present, the name will be used to load the game data, with all image properties being filled by SteamGrid. The title of the page will stay unaffected.

It will take a couple of seconds for your data to update.
You are free to add as many custom properties to the pages as you like, as long as you do not alter the properties that were copied from the example page (you can, however, move/hide them without breaking the code).

## Authors

* **Adrian Steffan** - [adriansteffan](https://github.com/adriansteffan) [website](https://adriansteffan.com/)
