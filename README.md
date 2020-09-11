# EEN.MediaPlayerEEN MediaPlayer JS Library


This javascript library follows the same pattern as drivefs and other EEN client libraries. All functionality will be bundled under the “EEN.mediaPlayer” namespace. The API functionality attempts to mimic the mobile playback API as much as possible. 






## EEN.MediaPlayer.MediaItem ##
The media MediaItem class is designed to provide a single interface to all existing use cases of FLV playback in the EEN system.There is support for API tokens, explicit auth tokens, and custom flv.js parameters. A mediaitem will default to live playback if no start or end time is set on the object.

### Methods ###


| name | parameters | Description |
|------|------------|-------------|
| constructor | string esn | Config class constructor. The camera’s ID (ESN) is a required parameter to create a new MediaItem object. |
| setStartTime | string timestamp | Set the start time of the video request. This can be an absolute time in EENTS format or a custom stream token defined by the user.  |
| setEndTime | string timestamp | Set the end time of the video request. This can be an absolute time in EENTS format or a relative time used for live playback. |
| setAuthToken | string auth_token | Sets EEN auth token for the video fetch request. This will be appended as “A=” on the request URL. Any cookies set in the client for eagleeyenetworks.com will still be sent with the request. |
| setDomain | string domain | Sets the domain name to use for the video request (Ex. login.eagleeyenetworks.com). Will default to the current window’s host. |
| setOptions | Object options | An optional set of configuration options for flv.js. These will override any default options used within this library. This allows fine tuning of any option currently accepted by the flv.js config. More information on these options can be found here - https://github.com/bilibili/flv.js/blob/master/docs/api.md#Config
	
  

### Examples ###


	var config = new EEN.MediaPlayer.MediaItem(‘cafebeef’);
	

	// Live playback with custom flv.js parameters
	var config = new EEN.MediaPlayer.MediaItem(‘cafebeef’);
	config.setOptions({‘lazyLoadMaxDuration’:10*60});
	
  
	// live playback with custom auth key
	var config = new EEN.MediaPlayer.MediaItem(‘cafebeef’);
	config.setAuthKey('c001~thisisatestkey');
	

	// Historical playback
	var config = new EEN.MediaPlayer.MediaItem(‘cafebeef’);
	config.setStartTime('20190205120100.000');
	config.setStartTime('20190205121000.000');
	



## EEN.MediaPlayer.startPlayback(MediaItem, VideoElement) ##
This function handles live and historical playback via a MediaItem configuration. The passed in video element should not define any sources as these will be configured by the library itself. All standard HTML5 video methods and events can be used with this element. 


This function can be called multiple times on the same video element if the user wishes to switch or restart streams.

| Parameter | Type | Description |
|-----------|------|-------------|
| mediaItem | EEN.MediaPlayer.MediaItem | The MediaItem we want to start playback using. See documentation for EEN.MediaPlayer.MediaItem above. |
| videoElement | HTML <video> element | Video element to display the EEN video in. |	

### Example ###

    EEN.MediaPlayer.startPlayback(config, document.getElementById('video-element'))

