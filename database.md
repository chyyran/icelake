#Icelake - Database
Icelake defines a few databases to store configuration data and cache games.

Each separate platform will have it's own database to store game data. Every database is an Sqlite3 database that is named for the platform's Icelake ID. It has one table named `games` and has the following table structure.

|uid|filename|title|publisher|platform|description|genre|boxart_url|release_year|release_day|release_month|metadata|
|---|--------|-----|---------|--------|-----------|-----|----------|------------|-----------|-------------|--------|

It follows the `GameInfo` structure with some added attributes, such as uid, and filename. 