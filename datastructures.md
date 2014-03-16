#Icelake Data Structures

Icelake specifies a few simple data structures to facilitate ease of use. These data-structures are kept simple, strings and integers only, to facilitate easy (de)serialization to and from formats such as JSON and YAML. It is left up to Snowflake to decide how to handle the raw data from these datastructures. As well, Icelake scrape methods can be exposed to JSONRPC for use in other frontends. 

##SearchResult
A `SearchResult` is a simple class that allows Icelake to compare the result with the game ROM's title. It consists of 2 attributes. 

* `game_title` is the scraped title of the result given the original game name as a search query. Icelake will use `difflib` to compare this to the original game name to judge if a result is relevant.
* `source_id` is the identification number of a result in a scrape source. This value is used to get more information about a game if the `SearchResult` is deemed relevant.

##GameInfo
A `GameInfo` is returned to Snowflake and contains information that will be shown to the user. A `GameInfo` has the following attributes.

* `title` is the title of the game.
* `publisher` is the name of the publisher of the game.
* `platform` is the Icelake ID of the platform this game was released for.
* `description` is the description of the game from the scraper source.
* `genre` is the genre of the game from the scraper source.
* `boxart_url` should be a url to an image of the game's boxart, if available. If not, then the value should default to the string `ICELAKE_NOBOXURL`
* `release_year` should be the 4-digit year in which the game was released, for example, `1990`. If not available, the value should default to `0000`
* `release_day` should be the 2-digit day number, for example, `01`, in which the game was released. If not available, the value should default to `00`.
* `release_month` should be the 2-digit month number, for example, `01` for January, in which the game was released. If not available, the value should default to `00`. 
*  `metadata` is an array of assorted non-standard metadata.

##PlatformInfo
A `PlatformInfo` is determined from the platform's YAML config file. A `PlatformInfo` object has the following attributes. 

* `platform_id` is the Icelake ID of the platform.
* `full_name` is the full name of the platform, for example, `Super Nintendo Entertainment System`
* `short_name` is the abbreviated name of the platform, for example `SNES`. If unavailable, it should default to the string `ICELAKE_NOSHORTNAME`.
* `company` is the production company of the platform, for example, `Nintendo`. If unavailable, it should default to the string `ICELAKE_NOCOMPANY`.
* `release_year` should be the 4-digit year in which the game was released, for example, `1990`. If not available, the value should default to `0000`
* `release_day` should be the 2-digit day number, for example, `01`, in which the game was released. If not available, the value should default to `00`.
* `release_month` should be the 2-digit month number, for example, `01` for January, in which the game was released. If not available, the value should default to `00`. 
* `emulator` should be the `emulator_name` of the emulator used for this platform. 
* `commandline` should be the command-line options of the emulator used for this platform. Icelake defines 2 variables that can be used for the `commandline` attribute.
    - `[ICELAKE_ROMNAME]` is the filename of the ROM or ISO that will be passed to the command-line options of the emulator.
	- `[ICELAKE_GAMECONFIG]` is an optional configuration file for the ROM that will be passed to the command-line options of the emulator. Not all emulators support this option.
* `logo_url` should be a url to an image of the platform's logo, if available. If not available, the value should default to `ICELAKE_NOLOGOURL`.
* `hardware_image_url` should be an url to the image of the hardware, preferably from http://commons.wikimedia.org/wiki/User:Evan-Amos/VideoGames. If not available, the value should default to `ICELAKE_NOHARDWAREIMAGE`. 
* `scrapers` is an array, in order of preference, of scrapers that will be used to get game information for this platform.
* `file_extensions` is an array of file extensions that ROMs for this platform appear in.
* `metadata` is an array of assorted non-standard metadata.

##EmulatorInfo
An `EmulatorInfo` is read from an emulator's YAML config file. An `EmulatorInfo` object has the following attributes. 

* `emulator_name` is the name of the emulator. The YAML file should be named this value. 
* `emulator_path` is the path of the emulator's main executable.
* `emulator_config` is the path of the emulator's main configuration file. 