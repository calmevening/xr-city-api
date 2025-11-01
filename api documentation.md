# API
The API uses the .json format and a Bearer auth token.

--------------------------------------------------------------------
## `contents.ssv.xrc.docomo.ne.jp/xrcity/_is_running_`
* get

always returns "202510301500" because 15:00 JST October 30, 2025 is the shutdown date

--------------------------------------------------------------------
## contents.ssv.xrc.docomo.ne.jp/html/app/OPN005.html
get

app TOS

--------------------------------------------------------------------
## https://ssv.xrc.docomo.ne.jp/content-app/v2.0/events
* auth, post
* request json: {"event_id_list":["EV-354225"]}

for returning event metadata

--------------------------------------------------------------------
## https://ssv.xrc.docomo.ne.jp/content-app/v2.0/contents/content-meta-infos
* auth, post
* request json: {"contents_id_list":["e2accf20508d47dc80af03505508ccad"]}

returns info on specific chapters, will return error if user has no access to it

--------------------------------------------------------------------
## https://ssv.xrc.docomo.ne.jp/content-app/v2.0/contents/content-meta-infos/selectable-order
* auth, post
* request json: {"location":{"latitude":14.60185718536377,"longitude":120.98006439208985},"request_count":30,"start_num":10,"contents_order":0}
* normal request_count is 10; 30 requests everything, 40 errors out
* normal start_num is 10; 0 requests from the top

returns a list of scenarios

--------------------------------------------------------------------
## ssv.xrc.docomo.ne.jp/content-app/v1.0/events/product-ids
get

???

--------------------------------------------------------------------
## ssv.xrc.docomo.ne.jp/update/v1.0/app/check-update
auth post

checks for app updates

--------------------------------------------------------------------
## ssv.xrc.docomo.ne.jp/user/v1.0/users/access-token-verification
auth post

response: {"status": true}

--------------------------------------------------------------------
## ssv.xrc.docomo.ne.jp/content-app/v1.0/contents/locations
auth post
* {"location":{"latitude":35.69923561975723,"longitude":139.7716932354213},"radius":6.1317217227778129}

probably returned something when the app was still active, it now only returns:
* {"contents_location_list": []}

--------------------------------------------------------------------
## ssv.xrc.docomo.ne.jp/information-app/v1.0/coupons
auth get

returns an empty json list, probably returned something when the app was still active

--------------------------------------------------------------------
## ssv.xrc.docomo.ne.jp/information-app/v1.0/news
get

returns news, no auth required

--------------------------------------------------------------------
## ssv.xrc.docomo.ne.jp/content-app/v1.0/contents/charged-informations
auth get

returns a list of purchased items

--------------------------------------------------------------------
## ssv.xrc.docomo.ne.jp/content-app/v1.0/contents/content-tags
auth get

returns a list of tags

--------------------------------------------------------------------
## ssv.xrc.docomo.ne.jp/content-app/v1.0/contents/recommended-tags
returns a list of user-specific tags, this upload has my recommended tags as an example

--------------------------------------------------------------------
## ssv.xrc.docomo.ne.jp/content-app/v1.0/collection-boxes
* auth post
* request json: {"request_count":1,"start_num":0,"event_id_list":["EV-354225"]}
* response: {"collection_box_list": []}

???

--------------------------------------------------------------------
## ssv.xrc.docomo.ne.jp/content-app/v1.0/pushes/registration-tokens
* auth push
* request json: {"registration_token":"ec_4NKs9TH-EbEiSyyHGUv:APA91bE105raA77Y-S-DlQg8zcsyn0fiY9Bh1K5i5L4s_ckJxwRifqiYP-etD9x6pgtj9K0QhIRyTGtlwAnpw3XPkkS0Vcduq_AaxXc49HNMMkEaz0iFHuw","delivery_category":{"important_notices":true,"recommendations":true}}
* response: 201

??? possibly connected to chapter unlocks from 7cp6.adj.st (see Steins;Gate XR City upload), seems to be triggered alongside app.adjust.com/sdk_click which references the xrcityapp:// link

--------------------------------------------------------------------
## https://lbe.xrc.docomo.ne.jp/contents-delivery/contents/v2.0
auth, get

URL parameters
* contents-id - UUID from content-meta-infos
* contents-version - version number from content-meta-infos
* is-original - True/False; false by default
* is-original switches url from APPROVED_OBJECT_DATA_ANDROID (if false) and OBJECT_DATA_ANDROID (if true)

returns an android and ios url for Unity bundle

if user is not authorized nothing is returned
* example: https://lbe.xrc.docomo.ne.jp/contents-delivery/contents/v2.0?contents-id=3884b3acf4944ca39b29f7653444a511&contents-version=9&is-original=true

--------------------------------------------------------------------
## app.adjust.net.in/sdk_click
* post
* Authorization: Signature signature="78AB36B47D7523E16AB6C9137CFF0A01E4BECB61187E8296B0F4F26C3D0813A7BD7D5929BCFAFD4B9DA5D97DE8C7F166F4AAAAEC184AB02DBE0AE6D380032243268866C314A05F584F71EAFFC643B9F9035BF46D5A7F4C0DAFBB96BEE10F64A80C62C46FE0054140E17168382D56AB8248BFEE5E0DC1CED79F095694BEABE0642A1959276810E1170BEF13FD6E901390010A8730F1790461AAD1D45FCB3A2F2131CF5C5A6CB6DCD4A8CD6B5C775DC44F4B98E802C820CE90ACD90402E6A317A294AEC0BD0BF07F94677546082D8CAF78",adj_signing_id="1100000",algorithm="adj5",headers_id="5",native_version="3.20.0"
* Content-Type: application/x-www-form-urlencoded
* User-Agent: Dalvik/2.1.0 (Linux; U; Android 12; SM-A156E Build/4aedf0c.0)
country=US&api_level=32&event_buffering_enabled=0&hardware_name=V417IR+release-keys&app_version=10.06.00001&app_token=9ri4mk5kkmio&installed_at=2025-09-22T20%3A48%3A24.806Z%2B0800&device_type=tablet&language=en&gps_adid=ef8f0b90-43fa-4edd-adb4-fe4f9890bf14&source=deeplink&foreground=1&connectivity_type=1&os_build=V417IR&click_time=2025-09-23T15%3A15%3A45.274Z%2B0800&cpu_type=x86_64&screen_size=large&gps_adid_src=service&subsession_count=2&send_in_background_enabled=0&last_interval=582&offline_mode_enabled=0&screen_density=high&session_count=3&ui_mode=1&gps_adid_attempt=1&session_length=118&created_at=2025-09-23T15%3A15%3A47.324Z%2B0800&device_manufacturer=Samsung&display_width=900&t

response
* {"app_token":"9ri4mk5kkmio","adid":"f1073e763be30e070fbba40bd5e153ea","resolved_click_url":"xrcityapp://contents/6af0ee811b424cccb2dbce653d0f88fd?adj_t=1a4hlzve\u0026adjust_reftag=cJJFZtM1pAHgG"}

--------------------------------------------------------------------
# outdated 10.03 network activity
* POST firebaseinstallations.googleapis.com/v1/projects/xrcity/installations
* post firebase-settings.crashlytics.com
* post app.adjust.com/sdk_click
* post firebaselogging-pa.googleapis.com/v1/firelog/legacy/batchlog
* https://id.dmc.docomo.ne.jp/dcm/auth/spReceive/gafour?idsite=427&dcmanUid=d6e0e115e34668ec16680a61821c7a10&referer=https%3A%2F%2Fcom.nttdocomo.android.xrcity
* contents.ssv.xrc.docomo.ne.jp/xrcity/_is_running_
* post app.adjust.net.in/sdk_click

--------------------------------------------------------------------
UnityPlayer/2021.3.50f1 (UnityWebRequest/1.0, libcurl/8.10.1-DEV) - user agent

https://contents01.ssv.xrc.docomo.ne.jp/ - the domain where actual AR files and thumbnails are kept; Cloudfront/AWS; uses key-pair and tokens; generated URLs last either 5 or 10 minutes

