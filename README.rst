======================================
ZenPacks.community.PredictiveThreshold
======================================


Description
===========

This ZenPack adds a new Predictive Threshold type for determining when to trigger an event. The threshold uses the Holt-Winters Forecasting from RRDTool.

Retrofitting data exists in the Predictive Threshold. It renames the original .rrd with a .old extension. The RemoveHoltData.py script packaged with the ZenPack is a command line tool for converting RRD data back to regular RRD files if you want to convert them back to standard thresholds.

Holt Winters Parameters

    * Alpha = 0.1 # 0-1 , value closer to 1 means more recent observation carries more weight, baseline
    * Beta = 0.0035 # 0-1 , value closer to 1 means more recent observation carries more weight, linear trend
    * Gamma = 0.1 # 0-1 , value closer to 1 means more recent observation carries more weight, seasonal trend
    * Rows = 1440 # rows >=season, 5days, 300second_intervals * 1440 points
    * Season = 288 # 1day, 288points * 300second_intervals
    * Window = 6 # window length .. (eg 6 observations for alerting)
    * Threshold = 3 # number of periods it has to fail in a window before alert sent
    * Delta = 2 # of standard deviations away from predicted value (for alerting)
    * Prediction Color = Color of the predicted value line
    * Confidence Band Color = Color of the confidence bands placed at delta standard deviations from prediction line
    * Tick Color = color of vertical line indicating threshold has been crossed at that value


Requirements & Dependencies
===========================

    * Zenoss Versions Supported: 3.0
    * External Dependencies: 
    * ZenPack Dependencies:
    * Installation Notes: zenhub and zopectl restart after installing this ZenPack.
    * Configuration: 

Limitations
===========

Beware if you are testing and creating a new template that it takes about 2 days before there is enough
data for the Holt-Winters RRA archives to have data so although you see the new lines on the legend of a
graph, there are no data lines for this long.

I don't think installing the ZenPack per se, will corrupt anything you currently have; however it may cause
problems to existing data. Have a look at http://community.zenoss.org/message/50360#50360 - I have seen this
both on the old version with 2.5.2 and with the new. I would take my own backup of RRD files before applying
a predictive threshold.

Download
========
Download the appropriate package for your Zenoss version from the list
below.

* Zenoss 3.0+ `Latest Package for Python 2.6`_

Installation
============
Normal Installation (packaged egg)
----------------------------------
Copy the downloaded .egg to your Zenoss server and run the following commands as the zenoss
user::

   zenpack --install <package.egg>
   zenhub restart
   zopectl restart

Developer Installation (link mode)
----------------------------------
If you wish to further develop and possibly contribute back to this 
ZenPack you should clone the git repository, then install the ZenPack in
developer mode::

   zenpack --link --install <package>
   zenhub restart
   zopectl restart

Configuration
=============

Tested with Zenoss 3.1 

Change History
==============
* 1.0
   * Eric Edgar's version working on Zenoss 2.2
* 2.0
   * Changed by Jane Curry to support Zenoss 3.x
* 2.1
   * Transferred to new github methods

Screenshots
===========
|PredictiveThresholdCreate|
|PredictiveThresholdEdit|
|PredictiveThresholdShow|


.. External References Below. Nothing Below This Line Should Be Rendered

.. _Latest Package for Python 2.6: https://github.com/jcurry/ZenPacks.common.PredictiveThreshold/blob/master/dist/ZenPacks.common.PredictiveThreshold-2.1-py2.6.egg?raw=true

.. |PredictiveThreshold| image:: http://github.com/jcurry/ZenPacks.common.PredictiveThreshold/raw/master/screenshots/PredictiveThresholdCreate.jpg
.. |PredictiveThreshold| image:: http://github.com/jcurry/ZenPacks.common.PredictiveThreshold/raw/master/screenshots/PredictiveThresholdEdit.jpg
.. |PredictiveThreshold| image:: http://github.com/jcurry/ZenPacks.common.PredictiveThreshold/raw/master/screenshots/PredictiveThresholdShow.jpg

                                                                        

