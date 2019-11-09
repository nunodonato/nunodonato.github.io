---
published: false
---
### Intro

Last August, after a full year of plumbing, wiring, digging, painting - our family of four has finally moved to our offgrid wooden house.

Off-grid was not the purpose, but given the location, it was not something we could avoid. I always had a personal desire for solar, so for me it was a great chance to materialize it. Our budget was extremely low, so we ended up choosing many parts of our solar system by price instead of quality/reliability. This was a great mistake.

Before moving, I spent many months doing research and using a watt-meter to calculate our average consumption. We had decided to avoid gas-powered equipment in our future house, so electric was the way to go in everything. Usually you'll find the opposite. People that depend on solar as they only source of electric power, usually try to delegate some things to gas. Most common examples of this (at least in my country): gas water heaters and gas stove.

In our case, electric water heater and induction cooktop. Everyone told me it was crazy, especially with such a small system.

How small?

- 9 x 320wh panels
- 5kwh Axpert inverter + charge controller
- 8 x 260ah 12V lead-acid batteries

When I decided on this system, I made a big mistake. Partially my fault, due to insufficient research, and I guess the other part by trusting too much on the guy who sold me the system.

I'm actually quite satisfied with the panels performance, and the inverter seems okay-ish (there are a few known bugs and it doesn't have modern features and connectivity like you'd find in a Victron, but that's fine). 

The real issue is the battery bank. Theoretically, I calculated that a 25kwh bank would be quite sufficient for our needs (my inital estimates were about 5kwh consumption per day). So even with a 3-4 day streak of cloudy days, we should be fine.

It turned out the batteries are **really** bad. I'm still not sure, to this day, if something might have happened that damaged the chemistry, or if they are really low quality. The reality is that I have  maybe a fourth of that capacity. This means that in cloudy days, like today, we really have to save as much as possible. And if we get 3 days in a row, its a big issue because everything depends on our solar system, including water pumped out of a well!

If it were today, I'd just opt for lithium batteries as the price has been coming down and DoD is much higher. But for now, due to financially reasons, that is not an option so I have to deal with what I have.

So this means we need to get smart in how we utilize all energy resources we have, and get the maximum out of it.

Even though I'm very tech oriented, I'm also pro-simpleliving, so I first look into no/low-tech solutions.

**Low/no-tech ideas**

Our 100L water tank heater has a 15000wh resistance. It is the appliance which consumes more electricity in our household (no surprise there). The dishwasher consumes 2000wh, but just for 20min, so a full-cycle is usually around 650wh. If we want hot water for baths, depending on the water temperature inside the tank, we can be looking at 1-2-3hrs of usage, which really drains the battery quite fast in case there's no sufficient power from the panels.

Luckily, my water tank has an easy way to choose the target temperature. Even though we dont need it higher than 40ºC, I use this as an alternative battery bank. usually the temperature is set at 70ºC and I let it heat as much as possible during sunny days. The water gets so hot that we end up using less of it. By doing this, we can have hot water of baths for 2-3 days, without needing to turn it on at all.

Our great saviour is our firewood stove. Using wood for heating is a no-brainer when you are off-grid. And the best thing about it, is that it has a flat top. There are days when I cook breakfast, lunch and dinner using nothing but the firewood stove. I actually enjoy tending the fire, but this would probbaly be a no-go for many people. I also use it to dehydrate fruit, and recentely got 2 tall oven trays that I can stack in order to create a tiny oven and bake things.

![](https://i.imgur.com/aHnai5U.jpg)

Had some really nice sweet potato and chestnuts recentely :)

**The tech-side**

Since my inverter didn't have any cool monitoring capabilties, I tried to find ways to make my own. Luckily it's a very widely used inverter in many countries (under different brands - the main one being Voltronic Power). After digging through some helpful forums (thank god these still exist and people haven't switched to facebook groups for everything) I found this github repository with code to fetch data from the inverter. After a few tweaks, I could connect the inverter to my laptop via USB and have a live reading of what was happening with the panels, inverter and battery status.

The next step was to get a Raspberry Pi to do this job. I opted for the Raspberry Pi Zero W, since low-power usage is my priority. Even though we are talking about only a couple of watts of difference, when a device is plugged in 24/7, things add up pretty quickly.

Now I just needed a way to monitor things easily from my phone. To do that I created a small php script in one of my shared hosting accounts, to receive data from the Pi and store it in a database. I don't really have a specific need for the database, but it can be useful for future stats.

Now I can just browse to a specific page to check the current and last-60min stats:

![](https://i.imgur.com/4mmrLX5.png)

By the way, that is how awful the PV production is on a cloudy-day!

With this system in place, I can safely be outside the house and text my wife when its safe, for example, to turn on the dishwasher. She hasn't yet had a crash-course in understanding voltages and such, mostly because I'm also trying to get a better feel of how it fluctuates with different power draws and different inputs (crazy, actually, but I blame it on the lead-acid)

My next step was to automate things a bit more. I realized I needed some more techie stuff when last week we were out for 5 days and returned to a cold water tank and cloudy days. If I was able to turn on the water heater at a distance, it would be perfect!

So I ordered [this Sonoff smart plug](https://sonoff.tech/product/wifi-smart-plugs/s26) which allows me to do just that. it also connects to Alexa, google home, ifttt, etc, but I dont really use any of that.

I'm now working on another script to run every X minutes on the Pi to monitor the inverter data and turn the water heater on/off accordingly. The decision flow will be like this

![](https://i.imgur.com/R2VLIfN.png)

This will allow for more watertank-heater-uptime and still safely save the batteries, without human intervention.

Can't wait to finish it and put it up and see the difference in hot-water-availability in a week or two.

Haven't yet researched on how to communicate with the plug from a simple script, but hopefully won't be hard. I was hoping ifttt would help me on that, but its pretty much useless unless you want to use pre-made flows and integrations.