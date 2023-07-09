# RealityRipple's Home-Made Emote Wall
A home-made emote wall for Twitch.TV, Kick, and YouTube Livestreams, supporting animated Twitch emotes, BetterTTV, FrankerFaceZ, 7TV, and Emojis! Kappagen command and event triggers are also available, with advanced configuration capabilities.

#### Supports
 * Chromium-based browsers
 * Broadcasting tools, such as:
   * OBS Studio
   * SE.Live
   * Streamlabs Desktop
   * Streamlabs Mobile (if your emotes.html file is hosted on a server)

## Building
Simply download the emotes.html file and open it in your favorite text editor. The notes at the beginning of the file will explain how to configure everything. Then add a new Browser source and select the file locally, or upload the file to a webserver and use its URL.

## Download
You can grab the latest release from the [Official Web Site](//realityripple.com/Tools/Twitch/EmoteWall/), which also includes a GUI Wizard for setting up the configuration.

## Notes and Caveats

### Update Procedure

To update this emote wall, simply use the Wizard to import and download it.
 1) Visit the [official page](//realityripple.com/Tools/Twitch/EmoteWall/).
 2) Click "Download Emote Wall" and choose "Use the Wizard".
 3) Import your previous HTML file by clicking "Import from File".
 4) Make any changes you need to make on each page.
 5) At the end of your configuration, hit "Download".

You will receive a new version of your HTML file with your previous settings.

### Emojis
Twitch filters out the ZWJ (Zero-Width Joiner) character which is used for merging many emojis. This system makes use of basic character detection to correctly parse many standard ZWJ-style emojis even without the ZWJ character, however more complicated sets such as the "family units" are not possible to correctly handle. The alternative character 0xE0002 used by some third-party Twitch chat projects will be correctly parsed as a ZWJ according to the rules laid out in the RFC:  
[Emoji RFC](//gist.github.com/Mm2PL/982c76964fe53f80fcf6b6963bba049f)

### Emote Dimensions
Emotes that are not square will be shrunk to fit while maintaining the original aspect ratio.

### Cheers
The cheer style will be used for kappagens. If a user cheers 1000 bits in a single 1000 bit emote, then the kappagen will be made of the 1000-bit cheers. However, if the user cheers 1000 bits using multiple smaller cheer emotes, those emotes will be used for the kappagen instead.

### Kappagen
Each emote-splosion uses the number of emotes defined in the kappa count preference mentioned above, except Pyramid, which uses a constant number based on the pyramidDist array (below). If the trigger includes specific emotes (via kappagen, cheer, or resub message), the ratio of one emote to another will be maintained. If a user with kappa access posts "!kappagen PunchTrees PunchTrees SSSsss" then two thirds of the emotes in the emote-splosion will be "PunchTrees", and one third will be "SSSsss".

### OBS
This emote wall may do better if the browser source has a frame rate limit of 30 or 60. If you use your GPU while streaming, you may wish to disable Browser Source Hardware Acceleration. It may also work better using a smaller screen resolution (such as 720p on a 1080p screen) and then stretching the browser source to fit to the screen using the OBS Transform feature.

### Inefficiencies

This emote wall uses normal <img> objects rather than a HTML Canvas. While this lowers efficiency, it also adds better GIF file support and allows easier user manipulation.

At present, the "zoom in" and "zoom out" feature uses a resource-heavy design. I had hoped the new CSS directive "scale: " would have helped, however it's useless without a "scale-origin" directive to accompany it.

The Bounce animation uses specific position-based drawing rather than actually being animated.

The Cube animation uses eight objects on screen for every image, making it a particularly resource-heavy drawing.

If your computer has trouble with this emote wall, please try disabling these options.
