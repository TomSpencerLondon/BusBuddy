# Bus Buddy

## What is it?
A way to get realtime data for the buses arriving at your local bus stop using Amazon Echo's voice recognition capabilities.

## What does it do?
First you need to obtain the five-digit code displayed on the bus stop you want to get data for.
Then there are three ways of accessing the application:

1. Alexa, ask Bus Buddy to set my bus stop to 53128
1. Alexa, ask Bus Buddy, when is my next bus?  
1. Alexa, ask Bus Buddy which buses stop at my bus stop?

In response, Bus Buddy will tell you the time in minutes until the arrival of the next bus at your stop, or the various lines that stop there.

## What's going on behind the scenes?
Making Bus Buddy required us to link three separate Amazon services and Transport for London's API together.

We created a new application, or "skill", for Alexa using Amazon's developer portal. This is where you create the user interface, defining what code will run when users say particular phrases to their Echo devices. It is possible to set multiple variations of the phrases that will trigger each of these paths through the programme, which Amazon calls "intents", so that you should be able to be able to ask "when is the next bus" or "what time is my next bus" and it will still work. This is also where we are able to assign a variable, the five-digit bus stop code, in the programme, using a system called "slots".

The code that actually runs when the device recognises one of these phrases is saved in Amazon's Lambda website, which is a place to store code in the cloud, and is available via Amazon Web Services (which requires a different login from the developer portal). We opted to write our programme in node.js, although other languages are also available.

Thirdly, we hooked our programme up to two separate tables on Amazon's database service, which is called DynamoDB, and is also available via Amazon Web Services (AWS). The first of these tables converts the publicly-available five-digit bus stop code into a separate nine-character id that Transport for London requires to get data back from its API. The second of these persists the user's preference of bus stop, so that they don't have to set this each time they want to know the time of the next bus.

If the device receives and understands the relevant message, code saved to Lambda queries the TfL API via a simple http get request. The data is returned as json, which is parsed and converted into a format that the device can read back to the user. Here is a detailed diagram of the flow of the programme:

![alt text](https://github.com/andyrow123/bus-buddy/blob/master/img/diagram.jpg "Flow through Bus Buddy application")

## What were the challenges?
Figuring out how the different parts of Amazon's infrastructure fitted together was quite complicated, given the time available (one week). Testing was also a challenge. Although Amazon makes a bespoke testing framework available on the web interface to the Lambda service, it is only possible to use this once you have uploaded and saved over your previous iteration, with no easy way to roll back the changes if you find your tests unexpectedly fail.

Version control was also a challenge. Re-uploading new iterations to Lambda tended to take precedence over committing and pushing the code to GitHub, as this was the only real way to find out if the code was working as expected. Future Alexa-based projects would benefit from more conscientious usage of git.
