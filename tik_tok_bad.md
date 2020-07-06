# u/bangorlol describes how shady TikTok is and why nobody should use it

[Original comment](https://www.reddit.com/r/videos/comments/fxgi06/not_new_news_but_tbh_if_you_have_tiktiok_just_get/fmuko1m/)

[/r/bestof post](https://www.reddit.com/r/bestof/comments/hdw64x/ubangorlol_describes_how_shady_tiktok_is_and_why/)

#### Edit: Please read to avoid confusion:  

I'm getting together the data now and enlisted the help of my colleagues who were also involved in the RE process. We'll be publishing data here over the next few days: https://www.reddit.com/r/tiktok_reversing/. I invite any security folk who have the time to post what they've got as well - known domains and ip addresses for sysadmins to filter on, etc. I understand the app has changed quite a bit in recent versions, so my data won't be up to date.



I understand there's a lot of attention on this post right now, but please be patient.

---  


So I can personally weigh in on this. I reverse-engineered the app, and feel confident in stating that I have a very strong understanding for how the app operates (or at least operated as of a few months ago).


TikTok is a data collection service that is thinly-veiled as a social network. If there is an API to get information on you, your contacts, or your device... well, they're using it.  

- Phone hardware (cpu type, number of course, hardware ids, screen dimensions, dpi, memory usage, disk space, etc)  
- Other apps you have installed (I've even seen some I've deleted show up in their analytics payload - maybe using as cached value?)  
- Everything network-related (ip, local ip, router mac, your mac, wifi access point name)  
- Whether or not you're rooted/jailbroken  
- Some variants of the app had GPS pinging enabled at the time, roughly once every 30 seconds - this is enabled by default if you ever location-tag a post IIRC  
- They set up a local proxy server on your device for "transcoding media", but that can be abused very easily as it has zero authentication  


The scariest part of all of this is that much of the logging they're doing is remotely configurable, and unless you reverse every single one of their native libraries (have fun reading all of that assembly, assuming you can get past their customized fork of OLLVM!!!) and manually inspect every single obfuscated function. They have several different protections in place to prevent you from reversing or debugging the app as well. App behavior changes slightly if they know you're trying to figure out what they're doing. There's also a few snippets of code on the Android version that allows for the downloading of a remote zip file, unzipping it, and executing said binary. There is zero reason a mobile app would need this functionality legitimately.


On top of all of the above, they weren't even using HTTPS for the longest time. They leaked users' email addresses in their HTTP REST API, as well as their secondary emails used for password resets. Don't forget about users' real names and birthdays, too. It was allllll publicly viewable a few months ago if you MITM'd the application.


They provide users with a taste of "virality" to entice them to stay on the platform. Your first TikTok post will likely garner quite a bit of likes, regardless of how good it is.. assuming you get past the initial moderation queue if thats still a thing. Most users end up chasing the dragon. Oh, there's also a ton of creepy old men who have direct access to children on the app, and I've personally seen (and reported) some really suspect stuff. 40-50 year old men getting 8-10 year old girls to do "duets" with them with sexually suggestive songs. Those videos are posted publicly. TikTok has direct messaging functionality.


Here's the thing though.. they don't want you to know how much information they're collecting on you, and the security implications of all of that data in one place, en masse, are fucking huge. They encrypt all of the analytics requests with an algorithm that changes with every update (at the very least the keys change) just so you can't see what they're doing. They also made it so you cannot use the app at all if you block communication to their analytics host off at the DNS-level.


For what it's worth I've reversed the Instagram, Facebook, Reddit, and Twitter apps. They don't collect anywhere near the same amount of data that TikTok does, and they sure as hell aren't outright trying to hide exactly whats being sent like TikTok is. It's like comparing a cup of water to the ocean - they just don't compare.



### tl;dr; I'm a nerd who figures out how apps work for a job. Calling it an advertising platform is an understatement. TikTok is essentially malware that is targeting children. Don't use TikTok. Don't let your friends and family use it.

---  

Edit: Well this blew up - sorry for the typos, I wrote this comment pretty quick. I appreciate the gold/rewards/etc people, but I'm honestly just glad I'm finally able to put this information in front of people (even if it may outdated by a few months).


If you're a security researcher and want to take a look at the most recent versions of the app, send me a PM and I'll give you all of the information I have as a jumping point for you to do your thing.

---  


### Edit 2: More research..

/u/kisuka left the following comment [here](https://www.reddit.com/r/videos/comments/fxgi06/not_new_news_but_tbh_if_you_have_tiktiok_just_get/fn1e2e3/):

> Piggy-backing on this. Penetrum just put out their TikTok research: https://penetrum.com/research/tiktok/

## Edit 2: Damn people. You necromanced the hell out of this comment.
## Edit 3: Updated the Penetrum link + added Zimperium's report (requires you request it manually)

The above Penetrum link appears to be gone. Someone else linked the paper here: https://penetrum.com/research

Zimperium put out a report awhile ago too: https://blog.zimperium.com/zimperium-analyzes-tiktoks-security-and-privacy-risks/   

### Edit 4: Messages  

So this post blew up for the third time. I've responded to over 200 replies and messages in the last 24 hours, but haven't gotten to the 80 or so DM's via the chat app. I intend on getting to them soon, though. I'm going to be throwing together a blog or something very soon and publishing some info. I'll update this post as soon as I have it up.
