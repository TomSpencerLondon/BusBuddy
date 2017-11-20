# BusBuddy
Makers Academy - Week 9 Challenge

```
Project in one line:
  Find the time until the next bus for a pre-defined route 

User interactions brainstorm:
  MVP
    set pre-defined route (departure and arrival points, but not bus numbers)
    ask 'when is my next bus?'

 next steps
    set time to bus stop
    get next bus times for not pre-defined routes?
    get different routes for different users?
    what is my nearest bus stop
    when is my next train?
    avoid particular bus number? 

What do we need to find out?
  does Alexa know your location?
  how to identify bus stops? 

Program flow:
  set departure point
    skill validates departure point - is real bus stop?
  set arrival point
    ditto validation
  departure and arrival point saved to cloud 

 ask skill when next bus
    skill retrieves departure and arrival points from database
    skill queries api
    skill parses api data
    skill returns result
```
