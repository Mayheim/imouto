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


#### HTML Markup and regex

The API returns match info in html like so

```html
<tr class='d2mtrow eventSoon' href='http://www.joindota.com/en/matches/109633' title='joinDOTA League Asia Season 1 - Lower-Bracket Final' rel='tooltip' id='109633'><td alt='1397138400' class='push-tt jd_date'>23m</td><td><img src='http://flags.cdn.gamesports.net/ph.gif' title='Philippines' width='14px' height='9px'>  Exe.TnC</td><td>v</td><td><img title='Indonesia' src='http://flags.cdn.gamesports.net/id.gif' width='14px' height='9px'>  RRQ</td></tr>
```

Use this regex to parse it

```
<tr class='d2mtrow eventSoon' href='(?P<jdurl>.*?)' title='(?P<title>.*?)' rel='tooltip' id='\d*'><td alt='(?P<timestamp>\d*)' class='push-tt jd_date'>.*?</td><td><img .*?>\s?(?P<team1>.*?)</td><td>v</td><td><img .*?>\s?(?P<team2>.*?)</td></tr>
```

The regex returns named groups:

* *jdurl* - the URL e.g. http://www.joindota.com/en/matches/109633
* *title* - the Match Title eg. joinDOTA League Asia Season 1 - Lower-Bracket Final
* *timestamp* - the Match scheduled time as a unix timestamp e.g. 1397138400
* *team1* and *team2* - Team names e.g. Exe.TnC and RRQ

Use this code to parse it

```python
# jdregex contains the regex
 jdregex = r"(?i)<tr class='d2mtrow eventSoon' href='(?P<jdurl>.*?)' title='(?P<title>.*?)' rel='tooltip' id='\d*'><td alt='(?P<timestamp>\d*)' class='push-tt jd_date'>.*?</td><td><img .*?>\s?(?P<team1>.*?)</td><td>v</td><td><img .*?>\s?(?P<team2>.*?)</td></tr>"
 
# markup contains the HTML markup for one match
 matchinfo = re.findall(jdregex, markup)

# now matchinfo contains the parsed data
# e.g. matchinfo['title'] gives you the parsed title
```
