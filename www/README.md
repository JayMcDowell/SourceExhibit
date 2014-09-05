MHFM Iphone App - Capstone Project for NSS 2013.

If you are viewing this for NSS -- Open the app in xcode and run the Iphone simulator.  (I showed Adam how to do this, I will be happy to show anyone else as I am really proud of this project and I want it to be seen.)  

The Musicians Hall of Fame and Museum was established in 2006 in Nashville, TN.  It's goal is to honor the sidemen and studio musicians from all genres of music.

Phase 1- completed--
Plan out App -  The challenge here is coming up with things that aren't already on the existing website.  The App will contain 3 main sections (inductees, exhibits and a radio station).  The inductee and exhibit pages will link to video clips.  After researching the options, I decided to use XCode and Phonegap.  

Phase 2 -completed--
Build the HTML and CSS.  Using bootstrap, XCode and the IOS simulator, the app is taking shape.  There are over 110 pages of content.  Create images for loading images and app icons for the different models of iphones/ipods.

Phase 3 -completed--
Enroll in the Apple ios Developer program.  This will allow me to test my app on multiple iphones before it goes "live".  It also enables me to push the app up the the Apple App store when it is completed.

Phase 4 -completed--
Enable scrolling in XCode.  Research and integrate the streaming radio content (this will consist of songs that are performed by the inductees or the instruments in the exhibits).  

Phase 5 -completed--
clean up the video frames in my inductee and exhibit pages.  -Used vidfit.js for this.-

Phase 6
Update splash page images and radio page.

Phase 7
Purchase the new media blanket licenses from Ascap, BMI and SESAC for the streaming music part of the app.  






I'm using Shoutcast.com as well as wavestreaming.com to host the content for my radio station. 

Cloud DJ is a great service that stores about 3 GBs of .mp3 files for broadcast.      


This is some info on the Cloud DJ API.

Cloud DJ has a simple JSON API, you can easily start,stop and check the status of your cloud DJ by using it.
http://open.wavepanel.net/clouddj/start/f257e0c82584d5aee8c73cacca21f22280cdeecb/ http://open.wavepanel.net/clouddj/stop/f257e0c82584d5aee8c73cacca21f22280cdeecb/ http://open.wavepanel.net/clouddj/status/f257e0c82584d5aee8c73cacca21f22280cdeecb/

You can also append ?auth=API_PASSWORD_HERE to any of the above URLs to use it without filling in the form.

Every request returns a JSON encoded object which has a status property, this is set to either true or false depending on the outcome of the request.









This is from the webpage I got the information about the radio implementation from:

Play an MP3 Audio Stream in PhoneGap

function playStream() {
  try {
    var myaudio = new Audio('http://icecast.ksl.com:8000/');
    myaudio.id = 'playerMyAdio';
    myaudio.play();
  } catch (e) {
    alert('no audio support!');
  } 
}
Then, in the HTML page I have the following.

<button onclick="playStream()">Listen Live</button>
If myaudio was created in a global sense (outside of a function) than you can also pause the audio with the following.

myaudio.pause();
Background Audio

In iOS 4.0 and above you can run audio in the background. PhoneGap doesn't currently support this out of the box, but you can add it. To do so, you'll need to do two things; add an item to the info.plist file and add a line of code to PhoneGap.

To the info.plist file, add a new key of “Required background modes”. That key will have an array of options. In “Item 0” of that array set the value to “App plays audio”.

Next, modify the ~/PhoneGapLib/Classes/Sound.m file. Look for the line that contains “if ([resourceURL isFileURL]) {”. It's around line 103. Just below that line, inside the if statement, you'll want to add the following.

[[AVAudioSession sharedInstance] setCategory:AVAudioSessionCategoryPlayback error:nil];
So, that section of code will look like the following.

if ([resourceURL isFileURL]) {
	[[AVAudioSession sharedInstance] setCategory:AVAudioSessionCategoryPlayback error:nil];
	audioFile.player = [[ AVAudioPlayer alloc ] initWithContentsOfURL:resourceURL error:&error];
} else {
	NSData* data = [NSData dataWithContentsOfURL:resourceURL];
	audioFile.player = [[ AVAudioPlayer alloc ] initWithData:data error:&error];
}
Note: Some users have have had trouble finding the Sound.m file. It's not in the XCode project itself. You'll find it beneath your home directory (~) under ~/PhoneGapLib/Classes/ or you can just use Finder to search for Sound.m. Right-click on it and open it in XCode.


