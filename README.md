# plex-music-rating-sync
Plex Agents do not read music ratings when importing music files.
This makes sense from a server-side-of-view.
You don't want all users to have the same ratings or playlists.
Every user should be able to set his / her own ratings and collect his favorite songs in playlists.

This project aims to provide a simple sync tool that synchronizes the track ratings and playlists with a specific PLEX user account and server.

## Features
* synchronize: track ratings, playlists (not automatically generated)
* supported local media players: [MediaMonkey](http://www.mediamonkey.com/)
* dry run without applying any changes
* logging

## Requirements
* Windows
* [MediaMonkey](http://www.mediamonkey.com/) v4.0 or higher
*  _Plex Media Server_ (PMS)
* Python 3.6 or higher with packages:
    * [PlexAPI v3.0.6](https://pypi.org/project/PlexAPI/)
    * [pypiwin32](https://pypi.org/project/pypiwin32/): to use the COM interface
    * [fuzzywuzzy](https://github.com/seatgeek/fuzzywuzzy): for fuzzy string matching
    * [python-Levenshtein](https://github.com/miohtama/python-Levenshtein) (optional): to improve performance of `fuzzywuzzy`
    * [numpy](https://pypi.org/project/numpy/)

## Installation

1. Clone this repository
   `git clone git@github.com:patzm/plex-music-rating-sync.git`
2. `cd plex-music-rating-sync`
3. Install all requirements
   `pip3.6 install -r requirements.txt`

## How to run
The main file is `sync_ratings.py`.
Usage description:
```
usage: sync_ratings.py [-h] [--dry] [--log LOG] [--passwd PASSWD] --player
                       PLAYER --server SERVER --username USERNAME

Synchronizes ID3 music ratings with a Plex media-server

optional arguments:
  -h, --help           show this help message and exit
  --dry                Does not apply any changes
  --log LOG            Sets the logging level
  --passwd PASSWD      The password for the plex user. NOT RECOMMENDED TO USE!
  --player PLAYER      Media player to synchronize with Plex
  --server SERVER      The name of the plex media server
  --username USERNAME  The plex username
```
Start the synchronization:
`./sync_ratings.py --server <server_name> --username <my@email.com|user_name> --player MediaMonkey`
Using the `--dry` flag in combination with `--log DEBUG` is recommended to see what changes will be made.

## Current Issues
* the [PlexAPI](https://pypi.org/project/PlexAPI/) seems to be only working for the administrator of the PMS.

## Upcoming Features
With the current state I have completed all functionality I desired to have.
Consequently I will not continue development unless you request it.
I welcome anyone to join the development of this little cmd-line tool.
Just open a [new issue](https://github.com/patzm/plex-music-rating-sync/issues/new), post a pull request, or ask me to give you permissions for the repository itself. 

These are a few ideas I have for features that would make sense:

* setup routine
* bi-directional sync
* optionally only synchronize track ratings _or_ playlists
* parallelization
* better user-interaction with nicer dialogs
* cache synchronization conflicts to prompt the user at the end of the batch run to resolve them
* iTunes synchronization?

## References
[PlexAPI](https://pypi.org/project/PlexAPI/) simplifies talking to a _PMS_. 

This project uses the MediaMonkey scripting interface using Microsoft COM model.
An introduction can be found [here](http://www.mediamonkey.com/wiki/index.php/Introduction_to_scripting).
The relevant model documentation is available [here](http://www.mediamonkey.com/wiki/index.php/SDBApplication).
