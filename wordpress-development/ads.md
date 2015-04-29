# Ads Explained

**Type of ads:** 
* Freewheel Display
* Freewheel Pre-roll (Video)
* Polar (using Freewheel)

## Freewheel
* _Request URI:_ Sent to Freewheel. Looks like:
```
http://2912a.v.fwmrm.net/ad/g/1?nw=379215&sfid=918347&csid=fs_homepage&caid=&pvrn=708210157-994480735&resp=ad;pageType=homepage;ptgt=s&envp=g_js&slid=leaderboard&w=728&h=90&slau=Leaderboard%20728x90
```
* _MRM Network ID:_ Constant associated with our account, `nw=379215`
* _Site Section Network ID:_ Another constant for our account, `sfid=918347`
* _Site Section ID:_ Used by ad sales to target particular sections. With the 2015 site launch, we have two sections:
Homepage, `csid=fs_homepage`
Other (for everything else), `csid=fs_other`
* _Freewheel Ad Targeting:_ The process for running a sold ad on any particular post. Ad sales team generates a tag in Freewheel, `Tags/LegendaryFilms` for instance. This tag's `caid` is then set, e.g. `caid="Tags/LegendaryFilms"`
This functionality is already built. See Production->Ad tab. 
![screen shot 2015-04-29 at 5 28 51 pm](https://cloud.githubusercontent.com/assets/1636964/7401847/4b3614b4-ee95-11e4-961d-d2b11bc5e294.png)

Other parameters:
* `slid` & `slau`: Used to identify different types of ads, e.g. Rectangle, Banner, MobileBanner etc. 
* `cd`: Another important query param, used to set multiple width and height in the request, e.g. `cd=1,1|300,250`
_Note: The `cd` attribute be used to serve 1x1 pixel (still under testing)_


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


## Polar
Polar is implemented for branded content. This integration consists of two Polar touch points:
* [Media Voice](https://mediavoice.com/present) (Polar CMS): This is where ad sales team populates data
* [Plugin to generate script](http://plugin.mediavoice.com/bookmarklet/ui/index.html#)
Handlebar template: Polar uses handlebar js to generate the ad. 

Polar ad templates implemented as of 03/19: 
- Homepage 
- Article
- Article Collection

The Fusion theme implementation of Polar is [here in polar-ad.js](https://github.com/fusioneng/fusion-theme/blob/master/assets/js/src/polar-ad.js).

The essence lies in the following excerpted code:
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

The article collection template is trickier than homepage or article. We are using `onRender()` function for chaining, so that after the first ad loads, it calls the next one and so on. 

The template is very important because everything else is a constant. For example if we want to change the article collection template to a single ad campaign, we need to do is to pass another template instead of `collectionWrapperTemplate` in above code sample. 

**Polar for Future:**
Internalizing the template: It would be nice to internalize the handlebar templates rather than to use the media voice plugin each time we have to make a change to the existing template or create a new one. Only caveat to this – how could we get data from Polar? 
