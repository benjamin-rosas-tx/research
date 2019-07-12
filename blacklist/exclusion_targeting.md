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

### Ventura 
Should add a blacklisted users administration area in location-user tab.
  
 * Add new field to campaigns table called exclusion_targeting. Adding blacklisted segments.
 * Add blacklisted_segment_user table. Contain (segment_id, user_id, created_at, updated_at)
 
 * UI update should include new section for blacklisted users. Needed an uploader to load all users to be excluded in campaign.
  
### Malibu 
Should iterate thought campaigns collecting a blacklist segment and pushed to device.

 * Add blacklisted users organizer on Clock work. (*)
 * Organizer worker should publish to venice users blacklists.

### Venice 
In basic bid decision should retrieve from blacklists.

 * Add new DAO for retrieve users blacklists.
 * Update CampaignData model adding including banned user flag.
 * Add new EligibilityFactor for blacklisted user.