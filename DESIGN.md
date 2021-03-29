**Problem Statement**

“Time is money.” In the type of work environments that many industries have shifted to in light of the pandemic, more office communication is being transmitted virtually than ever before. This presents an interesting problem: how do we keep two people in different timezones working with different currencies on the same page? How do we do that with twenty people? Or two hundred? It was a similar kind of communication error that crashed the Mars Climate Orbiter and wasted $327.6 million (equivalent to $518 million today). How much value is lost in the time spent by all the workers worldwide double-checking their deadlines and currencies or -- even worse -- the value lost by those very same workers not realizing their errors until it’s too late? So much time is spent not only trying to prevent these seemingly minutiae errors, but also reversing them after they’ve grown dangerous. Let’s stop wasting time. Let’s stop wasting money.

**Bot Description**

The International Communication Discord Bot, or ICDB, will be a bot that will be able to automatically convert any times or monetary values from its original posting to the appropriate time zones or currencies of people present in the discord server. This will be done when a user posts a time, such as a meeting or a train time, or the price of a product or service in the server for others to see. The ICDB will respond to the post, read the time or price, and convert it for those who do not share the poster’s timezone or currency. The ICDB will know each user’s timezone and currency by prompting each discord user to input their location to the bot, since discord does not disclose users’ locations, and the ICDB will save their location.
The ICDB solves the issue of international miscommunication due to timezone mix-ups and currency mishaps. By automatically correcting the times and prices posted, it allows for users to never miss a meeting or ineffectively budget due to these kinds of miscommunication. Additionally, if users do catch the time or currency difference, the ICDB saves the user the time required to search for the conversion and to convert it themselves.

**Use Cases** 

**Use Case #1: Time Conversion**

**Preconditions:**
The ICDB has every user’s location stored.  

**Main Flow:**
User provides a specified time with the appropriate prefix, eg. 1:15 pm [S1]. The bot will search for that user’s timezone in its database and compare it to the discord users’ timezones. The bot will determine the conversion between the user’s timezone and the discord users’ timezones, calculate the time for the discord users, and post the different times [S2].

**Subflows:**
[S1] : The user may not provide the appropriate prefix so the bot will assume 24-hour format of the time, eg. 1:15 will be viewed as 1:15 am and 13:15 will be 1:15 pm.
[S2] : If a discord user shares the same timezone as the user, the bot will not go through the conversion process nor post the time as it would be redundant.
Alternative Flows: 
[E1]: Any numbers without a colon will be ignored to avoid unnecessary time conversions when it is not a time.

**Use Case #2: Convert price user mentioned into currency from countries of others users in the Discord**

**Preconditions:**
The ICDB has every user’s location stored.

**Main Flow:**
User provides a specified a decimal amount in a currency of their choice in format $4.00 or 4  dollars. The bot will search for that user’s timezone in its database and compare it to the discord users’ timezones. The bot will determine the conversion between the user’s currency and the discord users’ currency based on location, calculate the currency conversion for the discord users, and post the different currency conversions
[S2] If a discord user shares the same timezone as the user, the bot will not go through the conversion process nor post the currency conversion as it would be redundant.

**Subflows:**
[S1] : The user may not provide the appropriate prefix so the bot will assume 24-hour format of the time, eg. 1:15 will be viewed as 1:15 am and 13:15 will be 1:15 pm.
[S2] : If a discord user shares the same timezone as the user, the bot will not go through the conversion process nor post the time as it would be redundant.

**Alternative Flows: **
[E1]: Any numbers without a proper currency sign will be ignored to avoid unnecessary currency conversions when it is not a form of currency.

**Design Sketches** 

**Transition Flow** 
<img width="489" alt="Screen Shot 2021-03-28 at 8 11 08 PM" src="https://user-images.githubusercontent.com/20996619/112777146-6c406200-900f-11eb-835b-ede387c828cd.png">

**Story Board** 
![storyboard](https://user-images.githubusercontent.com/20996619/112777202-96921f80-900f-11eb-93a3-c1fbbe7971b0.png)

**Architecture Design** 

<img width="691" alt="Screen Shot 2021-03-28 at 9 50 50 PM" src="https://user-images.githubusercontent.com/20996619/112777231-b1649400-900f-11eb-83f4-8a43bf0369c4.png">


1) The bot shall be implemented as an Express server in a Node.js environment. 
2) The system shall use the `discord.js` npm library to listen for messages posted from a Discord server and send back messages with conversions.
3) The system shall send a one-time prompt message when added to a channel to request user timezones and countries.
4) The system shall parse the user locations given in the response and store them in a MongoDB NoSQL database.
5) The system shall parse prices and locations from received messages.
6)The system shall convert currencies using a currency converter API, which it will integrate with via a custom driver that the team will develop. 
7)The system shall convert times using a plain JS time conversion service which the team will develop, possibly using an npm library.
8)The system shall determine which timezones and currencies to convert to using the stored user information from the database.
9)The system shall use a message builder to create the messages with conversions.
10) The system shall use the `discord.js` library to send the messages back to the server.





