# Exclusion targeting

## Motivation

Campaigns in some cases requires include some users ids in black lists. We currently do is whitlelist of users.

## Current status

We currently have the information of users in segments. In this way we can filter the possible bidding campaigns offered to the user in a certain auction. 
Depending on the tastes and characteristics of the user this can be included in different segments and if this exceeds a maximum of 60 the first 60 are chosen in random order.

For now, campaigns are excluded by:
* Add space blacklist.
* Site Id blacklist.
* Site name blacklist.
* Carrier blacklist.
* Category blacklist.
* Device blacklist.

## Approach

We need to include concept of exclusion targeting in our solutions. That means create a new type of segment call: **Blacklisted segment**.

To implement blacklisted segments is necessary to change code in 3 projects:

* Ventura - Should add a blacklisted segment administration area in location-user tab. 
* Malibu - Should iterate thought campaigns collecting a blacklist segment and pushed to device.
* Venice - In basic bid decision should retrieve from cache and apply filter.