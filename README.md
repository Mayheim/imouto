# Dota 2 Match Announcement Plugin

## Goal

Implement a skybot plugin to announce upcoming Dota 2 matches.

## Functional Process

There is a pre-parsed match list available at

> [http://api.dotaprj.me/jd/matches/v130/api.json](http://api.dotaprj.me/jd/matches/v130/api.json)

1. Download the match list from the API
2. Parse the list using regex
3. Set up a timer or sleep scheduled for the next match time
4. Make an announcement when the sleep or timer is up
