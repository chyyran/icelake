#Icelake Scrapers

##Scraper Interface
All scraper modules are required to have the following methods. 

* `gamename` is the common name of a game
* `platform` is the scraper source's platform identification number. 

A scraper consists of one file named `scraper.py` and a YAML file named `scrapermap.yml` in the same directory.

`_get_games_by_name(gamename)` will get an array of `ScrapeResult`s with just the game name as a search query. 

`_get_games_with_platform(gamename, platform)` will get an array of  `ScrapeResult`s with the game name as well as the platform as a search query.

`get_games(gamename, platform=None)` should be the default way to access game search results, if `platform` is `None`, it will return `_get_games_by_name(gamename)` otherwise it will return `_get_games_with_platform(gamename, platform)`. 

`get_game_data(gameid)` will be called to get more information about a certain game once the `SearchResult` has been verified through the scrape engine.

A scraper should define the following module attributes.

* `__scrapername__` should be the name identifier of the scraper. The directory where the scraper is located should be named this.
* `__scrapersource__` should be the domain name of the website where the information or API is located.
* `__scraperpath__` is the directory name where the scraper is located, `os.path.dirname(os.path.realpath(__file__))` in Snowflake.
* `__scrapermap__` is an array that maps the scraper's platform identification numbers to an Icelake ID using the scraper's `scrapermap.yml` file. In Snowflake, this is implemented as `yaml.load(open(os.path.join(__scraperpath__, "scrapermap.yml")))`

##Scrape Engine
Icelake will include a scrape engine whereby it will automatically judge the validity and relevance of a `SearchResult`. It is recommended that the scrape engine is called rather than the scrapers be accessed directly. The scrape engine should only return one `GameResult`, being the best result for the game. 

