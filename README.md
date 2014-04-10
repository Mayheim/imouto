# Dota 2 Match Announcement Plugin

## Goal

Implement a skybot plugin to announce upcoming Dota 2 matches.

## Functional Process

There is a pre-parsed match list available at

> [http://api.dotaprj.me/jd/matches/v130/api.json](http://api.dotaprj.me/jd/matches/v130/api.json)

### Core functions

1. Download the match list from the API
  1. The API returns a json formatted array that contains html markup, one item for every upcoming match. 
  2. Python parses json easily. 
2. Parse the list using regex
  1. The HTML markup needs to be parsed with regex to obtain match info that can be processed by python.
  2. see below for samples and the regex pattern to use
3. Repeat on a fixed timer or sleep

### Plugin functions

1. Set up a timer or sleep scheduled for the next match time
2. Make an announcement when the sleep or timer is up
3. Respond to user queries with upcoming match info

