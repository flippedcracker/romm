# v1.7.1 (_15-04-2023_)

## Added
 - New UI feel with the new RomM color palette
## Changed
 - Roms size is now human readable
## Fixed
 - Fixed a bug where multi file roms could break the scan if the rom name have a dot.

<br>

# v1.7 (_14-04-2023_)

## Added
 - More options and flexibility to prevent files/folders to be scanned. Check [config.yml](docker/config.example.yml) example
 - Config file example added to docker/config.example.yml
## Changed
 - Rom details page revamped
 - RomM logo revamped

<br>

# v1.6.5 (_12-04-2023_)

## Added
 - Multiple games gallery display modes
## Changed
 - Some fixes and improvements

<br>

# v1.6.4 (_12-04-2023_)

## Added
 - Now RomM allows to fix missmatched games by searching by IGDB id manually
 - WonderSwan and WonderSwan Color support added

<br>

# v1.6.3 (_12-04-2023_)

## Added
 - Support for multi file games: Now RomM can scan a folder with the game name and all of its files inside the folder. No need to match the folder with the files inside. Download feature can download a zip with the entire game and all of the files or just the desired ones.
 - Some UI tweaks

<br>

# v1.6.2 (_04-04-2023_)

## Added
 - Support for commodore64
## Fixed
 - Searching in IGDB for games in not supported platforms doesn't raise an error anymore

<br>

# v1.6.1 (_04-04-2023_)

## Added
 - Now sqlite database location needs to be binded to ``/romm/database``. Check [docker-compose](docker/docker-compose.example.yml) example.
 - Now resources location (games cover) needs to be binded to ``/romm/resources``. Check [docker-compose](docker/docker-compose.example.yml) example.
 - More platforms support. Check [platforms support](https://github.com/zurdi15/romm#platforms-support)
 - Now RomM version appears in the bottom of the settings panel
## Fixed
 - Download feature is now fixed for RomM structucture 1
## Changed
 - Library path binding changed from ``/library`` to ``/romm/library``. Check [docker-compose](docker/docker-compose.example.yml) 

<br>

# v1.6 (_01-04-2023_)

## Added
 - Smart scan: now RomM will only scan the changes in the filesystem, making the scan process too much faster. Added an option to force a full scan.
 - Now game files can be renamed after the name matched in IGDB, keeping the tags.

<br>

# v1.5.1 (_31-03-2023_)

## Fixed
 - Delete game now works properly

<br>

# v1.5 (_30-03-2023_)

**`Breaking change`**

In order to make the new features to work, it is mandatory this time to drop all the database. This will only make you need to re-scan, but you won't lose the cover changes or file changes you made.

I apologize for the inconveniences this may cause, as this is a new software, it may change a little bit the first weeks, at least until I can develop a proper way to migrate between versions. I hope you can understand these initial wipes in order to make a better tool.

## Added
 - Now RomM folder structure is more flexible to match two different patrons by priority. This change makes RomM **Emudeck** compatible at least with single file games platforms. Check [folder structure](readme.md#⚠️-folder-structure)
 - Added config file support to exclude folders and specific extension files to be scanned. Config file can be binded to ``/romm/config.yml`` .To reload config file RomM reload is needed. Check [config](readme.md#configuration).
 - Added tags support for region, revision/version and generic tags. Tags must have the right prefix to allow RomM scan them properly. Check [tags](readme.md#📑-tags-support).

<br>

# v1.4.1 (_29-03-2023_)

## Added
 - Now you can use your games tags (like (USA) or (rev-1)) to filter in the gallery

<br>

# v1.4 (_29-03-2023_)

## Added
 - Gamecube support [platforms support](https://github.com/zurdi15/romm#platforms-support)
 - PC support added (only for single file games like zip, iso, etc) [platforms support](https://github.com/zurdi15/romm#platforms-support)
## Changed
 - Now delete game only deletes it from RomM gallery. To delete it from the filesystem too you need to allow it with the checkbox.

<br>

# v1.3 (_29-03-2023_)

## Fixed
**`Breaking change`** - **This breaking change only applies for mariaDB users**:

Some users reported errors when scanning files with large names because file_names are limited to 100 characters in the database. As I want to give as much flexibility as possible I changed some database columns. 

If you didn't make a lot of manual changes you can just get rid of the database and recreate it, scanning your library again. If you did some changes and don't want to lose the progress, you should do this changes manually from the mariadb container (or wherever you have your mariadb database) since there is not any kind of CLI for this migration.

I am so sorry for any inconvenience this can generate.

Columns to modify (examples in case that you set it with database name as romm, in other case just change the database name in the {db_name}.roms part):
```
 alter table romm.roms modify column file_name varchar(500);
 alter table romm.roms modify column file_name_no_ext varchar(500);
 alter table romm.roms modify column name varchar(500);
 alter table romm.roms modify column r_slug varchar(500);
 alter table romm.roms modify column p_slug varchar(500);
 alter table romm.roms modify column path_cover_l text;
 alter table romm.roms modify column path_cover_s text;
 alter table romm.platforms modify column slug varchar(500);
 alter table romm.platforms modify column name varchar(500);
 alter table romm.platforms modify column path_logo text;
```

<br>

# v1.2.2 (_28-03-2023_)

## Added
 - Notification added when downloading a game
## Changed
 - Database name when using mariadb now can be changed with the new variable DB_NAME. Check [docker-compos.example.yml](https://github.com/zurdi15/romm/blob/master/docker/docker-compose.example.yml)
## Fixed
 - Potential password error when using mariadb if the password have special characters
 - Some other bugs

<br>

# v1.2 (_28-03-2023_)

## Added
 - SQLite support
 - Dreamcast support (https://github.com/zurdi15/romm#platforms-support)
## Changed
 - SQLite is now the database by default if ROMM_DB_DRIVER is not set. Check [docker-compos.example.yml](https://github.com/zurdi15/romm/blob/master/docker/docker-compose.example.yml)
 - Platforms and games are now shown by alphabetical order

<br>

# v1.1 (_27-03-2023_)

## Added
 - Game names parentheses are now omitted when searching game in IGDB, allowing game names to have tags.

<br>
 
# v1.0 (_27-03-2023_)
 
## Added
- Birth of RomM
