# Ads Explained

**Type of ads:** 
* Freewheel Display
* Freewheel Pre-roll (Video)
* Polar (using Freewheel)

**Important terminology:**
* Request URI: Sent to Freewheel. Looks like:
```
http://2912a.v.fwmrm.net/ad/g/1?nw=379215&sfid=918347&csid=fs_homepage&caid=&pvrn=708210157-994480735&resp=ad;pageType=homepage;ptgt=s&envp=g_js&slid=leaderboard&w=728&h=90&slau=Leaderboard%20728x90
```
* MRM Network ID: Constant associated with our account
nw=379215
* Site Section Network ID: Another constant for our account
sfid=918347
* Site Section Id: Used by ad sales people to target particular sections, for ex., Homepage, Culture, Justice (before re-launch). After relaunch, we have two sections:
Homepage (csid=fs_homepage), targeting Homepage.
Other (csid=fs_other), targeting everything else. 
* Freewheel Ad Targeting: When running sold ad on any particular post. To do this ad sales team generates a tag in Freewheel, “Tags/LegendaryFilms” for instance. This tag is then set to “caid”:
caid=”Tags/LegendaryFilms”
This functionality is already built. See Production->Ad tab. https://fusiondotnet.wordpress.com/wp-admin/post.php?post=105604&action=edit
* slid & slau: Query params used by ad sales team to identify different types of ads, Rectangle, Banner, MobileBanner etc. 
cd: Another important query param, used to set multiple width and height in the request. 
* cd=1,1|300,250
Can be used to serve 1x1 pixel (still under testing)

**NOTE**: Above terminology is more or less based on the request URI we generate and send to Freewheel. 


**POLAR:**
Recently, we started implementing Polar ads for branded content. Its a bit complicated than implementing regular ads. There are following components:
* Media Voice (Polar CMS): This is where ad sales team populates data. 
https://mediavoice.com/present
* Plugin to generate script (http://plugin.mediavoice.com/bookmarklet/ui/index.html#)
Handlebar template: Polar uses handlebar js to generate the ad. 

Types of Polar ads implemented by us (as of 03/19): 
Homepage 
Article
Article Collection

Each of the above mentioned is using their own template which is generated via plugin mentioned above. (reference file: assets/js/src/polar-ads.js)



Gist of Polar lies in the below code (find it in polar-ads.js)
```
 ads.setPropertyID("NA-FUSINET-11236680"); // Unique ID associated with Fusion’s account
        ads.setSecondaryPageURL("/sample/publisher/sponsored.html");
        ads.insertPreview({
            label: fusionData['polar'].label, //identifier for homepage or article or any other post where Polar ads are appearing 
            unit: { // Freewheel settings
                "server": "freewheel",
                "hostName": "2912a.v.fwmrm.net",
                "network": fusionData['polar'].freewheelNetworkId,
                "csid": "fs_other",
                "profile": "168234:Display",
                "ssto": "",
                "slau": fusionData['polar'].adUnit, 
            },
            location: "#polar-ad", // location where Polar ads are placed after page load
            infoText: "",
            infoButtonText: "",
            template: fusionData['polar'].isHome ? homepageTemplate : collectionWrapperTemplate, // template to use 
            onRender: function($element) {
            	if( ! fusionData['polar'].isHome ) {
	                addCollectionItem('#polar-col2'); // chaining for collection template. 
	                addCollectionItem('#polar-col3');// chaining for collection template
            	}
            },
            onFill: function(data) {},
            onError: function(error) {}
        });
        
        ads.configureSecondaryPage({
            track: function() {}
        });
```

Article collection is a little tricky. we are using `onRender()` function for chaining. After the first ad loads, it calls the next one and so on. 

So, really, its just a template which is of uttermost importance. Everything else is a constant. For example if we want to change the article collection template to a single ad campaign. All we need to do is to pass another template instead of collectionWrapperTemplate in above code sample. 




**Polar for Future:**
Internalizing the template: It would be nice to internalize the handlebar templates rather than to use the media voice plugin each time we have to make a change to the existing template or create a new one. Only caveat to this is how to get data from Polar? 


# Wordpress Implementation

**Files to reference:**
* /inc/class-ads.php
* /parts/ads/freewheel-ad.php

**Wordpress Settings**
* In dashboard, you have an option to go to settings->ads, if you want to turn on/off freewheel/polar ads on the whole site. 
* On each article, there is a setting under Production->ad to turn on/off freewheel/polar ad on that article page. NOTE: this takes higher precedence than the general setting mentioned above. 
* Also, on each article, there is a setting to target sold campaign under Production->ad. 
 * Select `enable` from drop-down list for Freewheel Tag
 * Enter the tag which you got from Sales team. This tag is generated in Freewheel Admin by our Sales team. 
 
When we implement ads using
```
<?php echo Fusion()->get_ad( array(
	'type'          => 'Banner',
	'desktop_only'  => true,
	'class'         => array( 'header-ad' ),
	'id'		=> 'header-ad-desktop'
)); ?>
```
couple of things are happening behind the scene.
1. Front End UI is generated using the `class` and `id` parameters which are later used to control the styles.
2. We generate the request URI using 
	* the `type` of ad (Banner, in the example above).
	* Site section id is dependent on the section you are on. Currently its `fs_homepage` for hompepage and `fs_other` for everything else.

**How does this magic happens?**
If you have work with ads, you must have noticed following object:
* tq.path=’/homepage/homepage’
* tq.caid=’’
* tq.keywords=’’
* tq.show=’’
* tq.id=’’
* tq.section=’homepage’
* tq.realsection=’’
* tq.subsection=’’
* tq.altsection=’’
* tq.objType=’’
* tq.byline=’’
* tq.othersubs=’’

This got carried forward from how ABC News was doing their ads. I am sure some of these variables does make sense if you read the terminology. 

We are mostly using tq.caid (for ad targeting) and tq.section (for site section id). I am not sure of the other variables, though, which we should definitely ask Peter (from ABC News) and update this document. My guess is that these are for some type of targeting, for example if we want to target a whole show. we would set tq.show, for instance. 



**PROBLEMS:**
* We don't have access to Freewheel Admin as the contract lies with ABC News. Only ABC employees are allowed to access Freewheel Admin. Will it be helpful? 
 * For one, we will be able to see how the ads are rendered behind the scene. Meaning, how FW process the request? If the request fails, what are the exact problems (specially helpful while debugging video pre-roll). 
 * Secondly, as we sell more campaigns, we will need to switch to ad targeting. Meaning, show sold campaign on articles. For this, ad sales team has to create a tag in FW. If we have access to admin, it will save a lot of time. 
