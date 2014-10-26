A Computer Scientist in a Business School
Random thoughts of a computer scientist who is working behind the enemy lines; and lately turned into a double agent.
WEDNESDAY, MARCH 16, 2011

Uncovering an advertising fraud scheme. Or "the Internet is for porn"
You have heard about fraud and online advertising. You may have seen the Wall Street Journal video  "Porn Sites Scam Advertisers", or even read the story at today's Wall Street Journal about "Off Screen, Porn Sites Trick Advertisers" (Hint: to avoid the WSJ paywall, search the title of the article through Google News and click from there, to read the full article).

Since I am intimately familiar with the story covered by WSJ (i.e., I was part of the team at AdSafe that uncovered it), I thought it would be also good to cover the technical aspects in more detail, uncovering the way in which this advertising fraud scheme operated.

It is long but (I think) interesting. It is a story of a one-man-making-a-million-dollar-per-month fraud scheme. It shows how a moderately sophisticated advertising fraud scheme can generate very significant monetary benefits for the fraudster: Profits of millions of dollars per year.

If you want to skip the technical sleuthing details, you can skip directly to the overall picture and the discussion.


Disclaimer: In the story below, I will only mention by name the sites performing the fraudulent activities. All the brand names that you see are just for illustration purposes. They are not the ones affected by this case of fraud. Also remember that this is a personal blog. The views and opinions that I express here are my own and do not necessarily represent the views of AdSafe or the views of New York University.


The erroneous classifier

It all started while working at AdSafe. For those not familiar with AdSafe: The role of AdSafe is to provide brand protection services to online advertisers. In plain English, AdSafe analyzes website content and can block ads from appearing on individual web pages with content inappropriate for a brand. Porn, hate speech, gambling, celebrity gossip, torrents, are among the many categories that we detect.

On a nice Monday, the data science team gets the notification: The web page classifier was detecting a large number of porn web pages within legitimate, clean, big-brand-name websites. Think of websites such as BabyCenter, MSN MoneyCentral, HGTV, and so on. These sites would never have anything racy in their pages. However, we could see them being classified as having hard-core porn!

Why do we detect porn in clean sites? None of the pages within the sites contained anything offensive. No porn, no offensive material. Nothing. The website was clean as it gets. What was going on?


The invisible iframe hosting

The lifesaver was a technique developed at AdSafe: The key to the solution was the ability to read the address of the top frame that was hosting the ad(*). We were detecting porn because the ads that were supposed to appear within a "clean publisher" site were appearing within the frame of a porn website. Think of HGTV as an illustrative, but not the real, example of such a "clean publisher."

(*) For the technically curious: reading the address of the top frame is a challenging problem. For security reasons, browsers do not allow cross-domain scripting. So, it is not possible to just call the "top" object and read its properties. We have a proprietary solution for this.

By using this technique, we got our explanation: The HGTV website was appearing within an iframe of a porn website. In our case, the porn website was www.hqtubevideos.com.

WTF? This made no sense. Why would the porn website display HGTV (and the associated ads) within an iframe? Why would the porn site generate this "invisible" traffic towards HGTV? Just so that HGTV would get paid for the CPM ads? Or was the porn site trying to decrease the clickthrough rate of HGTV and ruin the performance the CPC campaigns? Did the porn website love HGTV so much and it was trying to increase its traffic? No way. Did HGTV employ a porn website to increase its traffic? No way, either.

Made no sense whatsoever.


Checking the structure of the porn website

So, we decided to investigate. Let's see what is going on. First, we go and see the HTML source of www.hqtubevideos.com/play.html that was the top frame what we were detecting. Here is the source:




The highlighted part shows an interesting redirection. We go to the www.hqtubevideos.com/index.php, but with the parameter ?x=1 at the end.

Loading the page www.hqtubevideos.com/index.php without this parameter loads a "vanilla" porn website. A few semi-suspicious attempts to add the website in the bookmarks in the beginning. Then porn pictures and links to affiliate sites. Plenty of porn but nothing to set an alarm. So far, so good.

They key, though, is this parameter ?x=1. Loading the www.hqtubevideos.com/index.php?x=1 we see a key part added in the website, at the very bottom. Here is the corresponding source.



Aha! A 0x0 iframe, loading the following URLs:
www.hqtubevideos.com/counter.php
www.hqtubevideos.com/counter2.php
The first URL seems to be loading some randomized hashid. Ignore.

The second URL, www.hqtubevideos.com/counter2.php, is a little bit more interesting and puzzling:



What is going on? Why would a porn site link to these domains? What is the connection? 


The parked domains

We started by doing a whois to figure out the ownership of this domains. Unfortunately, the registration information for the hqtubevideos is private and protected. However, the registration info for all the other domains is available. Not surprisingly, we see a common ownership for all these seven domains:

Registrant:
Thomas Schneider
519 S. York Road
Dillsburg, Pennsylvania 17019
United States
Registered through: GoDaddy.com, Inc. (http://www.godaddy.com)
Domain Name: RELAXHEALTH.COM
Created on: 11-Mar-09
Expires on: 11-Mar-12
Last Updated on: 10-Jan-11
Administrative Contact:
Schneider, Thomas garret.and@gmail.com
519 S. York Road
Dillsburg, Pennsylvania 17019
United States
7174327575 Fax --
Technical Contact:
Schneider, Thomas garret.and@gmail.com
519 S. York Road
Dillsburg, Pennsylvania 17019
United States
7174327575 Fax --
Domain servers in listed order:
NS1.ROLENEWS.COM
NS2.ROLENEWS.COM

Now we start seeing something being uncovered. Would this guy, Thomas Schneider, be behind this? Too easy to be true. We went and did a reverse whois to find other domains that contained the email garret.and@gmail.com. And here we are: The email is associated with the registration of 89 other domains, which are registered under a variety of last names, but all listing garret.and@gmail.com as the contact email:
aboutclimax.com
aboutclinical.com
aboutcouples.com
abouterectile.com
abouterection.com
achieveday.com
achievedrugs.com
afterdeaths.com
afterdrugs.com
associatedmagazine.com
atlantea.org
baldnesshealth.com
basehealth.com
becomeerect.com
begineducate.com
behaviordesire.com
beingdizzy.com
bestcialis.com
bestclimax.com
bigcouples.com
bodychemical.com
bodyclimax.com
bodyday.com
bundlehealth.com
calnam.com
cancerdamage.com
carecouples.com
carloschongdds.com
ceaifa.com
cialisc.com
cigarettesfinder.com
clubofheads.com
coacaz.com
college-grants1.com
college-scholarships1.com
collinshall.com
conditionnews.com
couponvi.com
criminaldefenseattorneys2.com
criminaldefenselawfirms1.com
detailedhealth.com
drinkershealth.com
drinkingmagazine.com
eurovision-2008.com
experiencemedical.com
fantasiesmagazine.com
fearhealth.com
gendergibe.org
government-grants1.org
groupovienna.net
hardballdollars.com
hawgsandpaws.org
impotencemagazine.com
letscurepeyronies.com
levitrav.com
medicationmagazine.com
moorehabitat.org
nighttimemagazine.com
ownmeds.com
panimarock.com
playmeds.com
powerfulselling.com
printcoupons1.com
propeciav.com
relationshipmeds.com
relaxhealth.com
rml-inc.com
rxvis.com
savewhalompark.com
sex-tvs.com
shopwizz.biz
signbysign.com
steve-magic.com
styleandmore.net
syncsql.com
takemedical.com
taylor-training.com
testosteronehealth.com
thedongman.com
traumamedical.com
twohealth.com
viagracomp.com
viagraeds.com
viagramagazine.com
viagravi.com
washealth.com
waymagazine.com
weightmedical.com
worldcuplive1.com

Let's see what we have so far: The owner of a porn domain loads in a set of 0x0 iframes, a set of other websites, all operated by the same owner. But still, no clear motivation. Also, the connection with the publishers that we checked remains elusive.


Re-directions within the parked domains

Now, let's see what is going on within these URL calls, such as www.takemedical.com/go_with_post.php. Here is the HTML source of one of those URLs:



Interesting. Another redirection. The site automatically submits a search form, searching for the term "hihijiji". Loading the page in the browser with the GET method (as opposed to the POST method indicated in the form), takes us to the normal page of a parked domain.

But let's submit with the POST method:
curl www.takemedical.com/search.php -d token=hihijiji
Ha! The result is different:

<iframe frameborder="No" height="1" src="index2.php" width="1"> </iframe>
We uncovered a hidden URL. This is the point where everything will start falling into place.




Re-directions and generating click fraud with normal click patterns

Within this hidden URL is where all the interesting things are happening! Let's load www.takemedical.com/index2.php and see the network activity. (In Chrome, go to Tools, Developer Tools, and then to the Network tab.). Here is the screenshot:




Indeed, here is where all the action is happening: These innocent sounding parked domain load all sorts of ad sites, and then "clicks" on the ads. By click, we do not mean any actual click. Instead the site loads the URL in the ad, that is typically a redirection to the ad server, which then redirects to the advertised URL. After this "click" within the iframe we finally have the publisher website (the "HGTV" that we mentioned before)!

Interestingly enough, the click fraud was very well-done: It was not loading all the time the same website. Sometimes it was mevio, other times it was tremor, other times bodyarchitect.tv, and so on. And once we have been redirected enough times from the same IP address, the final redirect was going to find.fm, to execute a straight-forward search. Clever! Engage in fraud, but be careful not to trigger any alarms.

Also, notice that the traffic patterns for the clicks are not bot-generated. These are actual users. With real and different web browsers. Different IP addresses. Different times of the day, following the usual traffic patterns per region. Good job: these click-fraud patterns are the least likely to be caught as they have patterns very similar to normal traffic.

For those interested in the details, here is the set of screenshots with the redirects:


















Update (3/17/2011): Initially, I did not want to post screenshots with the actual ad networks that were being defrauded, as it was not my intention to involve them in the story. However, since they were mentioned in the Wall Street Journal article already, and they have taken measures against this, I am posting them now. Here are the screenshots with ad loads from the networks. Warning: NSFW.

















The role of parked domains: Laundering traffic

At this point, we now know how this person makes money. Clearly, there is click-fraud: the scammer is employing click-fraud services to click on the pay-per-click ads "displayed" in his parked domains. If some of the ads are also pay-per-impression, he may also get paid for these invisible impressions that happen within the 0x0 iframe.

Why the parked domains though? Why not doing the same directly within the porn site? The answer is simple: Traffic laundering.

What do I mean by "traffic laundering"? First, the ad networks are unlikely to place many ads within a porn site. On the other hand, they have ad-placement services for parked domains. Second, the publishers that get the traffic from the parked domains see in the referral URLs some legitimately-sounding domain names, not a porn site. Even if they go and check the site, they will only see an empty site full of ads. Nothing too suspicious. Hats off to the scammer. Clever scheme.

You think we are done? No. There is one more piece in the puzzle. How does the scammer attract visitors to the porn site?


Generating traffic through an adult traffic exchange

The other interesting part: The porn website does not really contain porn! There are a few images but most of the links are to other porn website that actually host the video. In other words, the scammer does not even pay the cost of hosting porn!

However, according to QuantCast and Compete, the website has a pretty significant number of unique visitors per month. Here is the traffic over the last year:







This porn website gets 500K to 1M unique visitors per month! That is a lot of traffic for a website without any real content! So, how does the guy get all the traffic?

The answer surprised me. Apparently, there is an exchange (yes, my dear readers, an exchange!) for buying and selling adult traffic! Its name: TrafficHolder.com

Do you want to buy traffic for people interested in midget sex? The price is \$2.94 per thousand visitors. Interested in latex? The cost is \$2.54 per thousand visitors. Interested in HD video? \$3.54 per thousand visitors. (The running price catalog and the available traffic volume is available at http://www.trafficholder.com/cgi-bin/traffic/manager/buying100.cgi)

How do the porn sites sell traffic to each other? Through pop-ups, pop-unders, by causing the first click to the website to redirect to the buyer's site. The term for this traffic is "skimmed traffic"

Following the trail, we figured out the source of the traffic for hqtubevideos.com: It was coming from the (very popular, apparently) website www.pornoxo.com. The reports from QuantCast and Compete confirm that PornoXo gets approximately 1 million unique visitors per month. If you visit the PornoXo.com website, you will see that the first click will create a pop-under that loads the page hqtubevideos.com/play.html. This is the page responsible for all the fraud that I described above.

Based on the exchange prices and the visitorship at PornoXo, this traffic has a cost of \$3K/month for hqtubevideos.com, which is significant. So, we need to figure out how the scammer recovers this cost.


How much money are we talking about?

So, the key question now: How much money the hqtubevideos.com generates through the scheme? To get a feeling of how much fraud is going on, please do the following:
Open Chrome
Open the options, and then Tools, then Developer Tools. This will load the monitoring tool.
Switch to the "Network" tab
Visit http://www.hqtubevideos.com/play.html and see what is being loaded in the background (my own counting was approximately 1 ad loading per 10 seconds)
Let's do some back-of-the-envelope, very conservative, approximations:
The site gets 500K-1M visitors per month
The cost of this traffic is approximately \$1.5K to \$3K per month
Each unique visit loads 7 sites, which then generate clicks. Let's assume that there is no reload of the invisible sites, to keep the estimates low.
Assuming 500K visitors and that just one click out of the seven sites goes through, this is 500K clicks per month (low estimate)
Assuming 1M visitors and that all clicks, in all 7 sites, go through, this is 7M clicks per month (high estimate)
The a low-end estimate for CPC click costs is 30 cents, out of which we can assume that the scammer gets, say, 10 cents.
This generates a total income of \$50K to \$700K per month
The scheme is running for 8 months now, generating total revenue of \$400K to \$5M so far. (And you thought that investment bankers were getting paid a lot...)
Notice that these approximations assume that the site only generates the direct clicks discussed above. You will notice that there is no end in the loading of ads, if you leave the website open for a while. Given that the site visitors come from PornoXo, there is a good chance they will keep watching the porn video at PornoXo, leaving hqtubevideos to load the ads in the background.

But even with the modest estimates listed above, we are talking about a business that generates tens of thousands of dollars, with really minimum requirements. This is a scheme that a single person can set up in a week...


Overall picture

Trying to put all pieces together, I created the following graphical summary to see what is going on:




Let's follow the flow of the users:
Scammer buys user traffic from PornoXo.com and sends it to HQTubeVideos.
HQTubeVideos loads, in invisible iframes, some parked domains with innocent-sounding names (relaxhealth.com, etc)
In the parked domains, ad networks serve display and PPC ads.
The click-fraud sites click on the ads that appear within the parked domains.
The legitimate publishers gets invisible/fraudulent traffic through the (fraudulently) clicked ads from parked domains.
Brand advertisers place their ad on the websites of the legitimate publishers, which in reality appear within the (invisible) iframe of HQTubeVideos.
AdSafe detects the attempted placement within the porn website, and prevents the ads of the brand publisher from appearing in the legitimate website, which is hosted within the invisible frame of the porn site.
Notice how nicely orchestrated is the whole scheme: The parked domains "launder" the porn traffic. The ad networks place the ads in some legitimately-sounding parked domains, not in a porn site. The publishers get traffic from innocent domains such as RelaxHealth, not from porn sites. The porn site loads a variety of publishers, distributing the fraud across many publishers and many advertisers.



Who has the incentives to fight this?

And now let's see who has the incentives to fight this. It is fraud, right? But I think it is well-executed type of fraud. It targets and defrauds the player that has the least incentives to fight the scam.

Who is affected? Let's follow the money:
The big brand advertisers (Continental, Coca Cola, Verizon, Vonage,...) pay the publishers and the ad networks for running their campaigns.
The publishers pay the ad network and the scammer for the fraudulent clicks.
The scammer pays PornoXo and TrafficHolder for the traffic.
The ad networks see clicks on their ads, they get paid, so not much to worry about. They would worry if their advertisers were not happy. But here we have a piece of genius:

The scammer did not target sites that would measure conversions or cost-per-acquisition. Instead, the scammer was targeting mainly sites that sell pay-per-impression ads and video ads. If the publishers display CPM ads paid by impression, any traffic is good, all impressions count. It is not an accident that the scammer targets publishers with video content, and plenty of pay-per-impression video ads. The publishers have no reason to worry if they get traffic and the cost-per-visit is low.

Effectively, the only one hurt in this chain are the big brand advertisers, who feed the rest of the advertising chain.

Do the big brands care about this type of fraud? Yes and no, but not really deeply. Yes, they pay for some "invisible impressions". But this is a marketing campaign. In any case, not all marketing attempts are successful. Do all readers of Economist look at the printed ads? Hardly. Do all web users pay attention to the banner ads? I do not think so. Invisible ads are just one of the things that make advertising a little bit more expensive and harder. Consider it part of the cost of doing business. In any case, compared to the overall marketing budget of these behemoths, the cost of such fraud is peanuts.

The big brands do not want their brand to be hurt. If the ads do not appear in places inappropriate for the brand, things are fine. Fighting the fraud publicly? This will just associate the brand with fraud. No marketing department wants that.

Note also that the fraudster does not target a single publisher, does not target a single advertiser. The damage is amortized so nicely that nobody feels that it is a big deal. A mastery of the long tail...

Well, but what if fraud is big? What if big bucks are wasted? Maybe some newspapers would like to investigate. Let's break the big story. What would be the effect? Publicizing that a significant source of their income (online advertising) is a dangerous thing, full of fraud? Who would like to shoot himself in the foot?


Fraud as (harmless?) parasite

Really. Genius. Defraud many rich guys a little bit each, and ensure that nobody has the incentives to really fight and chase the fraud.

The guy essentially realized that this type of fraud is really behaving like a parasite within a much bigger ecosystem. And it is a parasite that is so costly to remove that it makes sense to leave it there. As long as the parasite does not annoy the host too much, things will be fine.

Only if fraud becomes really big there will be the real incentive to fight advertising fraud. Until then, you know how to make \$500K/month...
