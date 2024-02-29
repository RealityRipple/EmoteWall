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
Simply download the emotes.html file and open it in your favorite text editor. The notes in `CONFIG.md` will explain how to configure everything. Then add a new Browser source and select the file locally, or upload the file to a webserver and use its URL.

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

### Kappagen
Each emote-splosion uses the number of emotes defined in the kappa count preference mentioned in [CONFIG.md](./CONFIG.md), except Pyramid, which uses a constant number based on the `pyramidDist` array, and Text, which uses the `alnumDist` array to construct specific words or phrases. If the trigger includes specific emotes (via kappagen, cheer, or resub message), the ratio of one emote to another will be maintained. If a user with kappa access posts "!kappagen PunchTrees PunchTrees SSSsss" then two thirds of the emotes in the emote-splosion will be "PunchTrees", and one third will be "SSSsss".

### Emote Priority
Priority for emotes with identical names (case-sensitive) uses this exact order:
 1) Cheermotes
 2) User Emotes + Golden Kappa
 3) Channel Emotes
 4) Global Emotes
 5) Emojis

The order between services is always:
 1) First-Party (Twitch, YouTube, or Kick)
 2) FrankerFaceZ
 3) BetterTTV
 4) 7TV

This priority order is slightly different from existing extensions, and prioritizes the ability to override global emotes with channel-themed ones, as well as allowing third-party User emotes to override any others, except cheers.

### Cheers
The cheer style will be used for kappagens. If a user cheers 1000 bits in a single 1000 bit emote, then the kappagen will be made of the 1000-bit cheers. However, if the user cheers 1000 bits using multiple smaller cheer emotes, those emotes will be used for the kappagen instead.

### Twitch API
There are only a few actual problems with Twitch's API; many of the issues listed below are things that could be improved or made more efficient, not things that are broken.

> #### [Emote Dimensions](//twitch.uservoice.com/forums/310213/suggestions/46824100)
> Emotes that are not square may be shrunk to fit while maintaining the original aspect ratio for certain animations, such as the Pyramids and Text kappagens, and Cubes. Some emote sizes are non-standard and not correctly provided. The dimensions of non-square images are stored in the OBS Browser Source's IndexedDB, so that after the first time the image is displayed, the correct dimensions will be used. This also means that some emotes (notably Twitch's basic smile set) may be squashed the very first time they're displayed.
>
> A built-in command exists for the broadcaster and all channel moderators to clear this cache in case of some kind of failure, by using exactly the message `!cesc`, which stands for Clear Emote Size Cache. The cache will be cleared immediately; no restart is required.

> #### [Followers](//twitch.uservoice.com/forums/310213/suggestions/44000865)
> Follower detection is a bit of a mess, as a `following` status is not included in message tags like subscription or other badge-visible account types (such as Mods, VIPs, or Artists). Having a follower tag would prevent unnecessary API calls when users chat or use commands. The Emote Wall attempts to smartly handle this issue with a local cache of accounts and their follower states, if being a follower is used for any access (chat, kappagen, or other commands).

> #### [Gift Subs](//twitch.uservoice.com/forums/310213/suggestions/46400620)
> Bulk gift subscriptions are sometimes listed in the wrong order - the bulk alert is shown after each individual gift sub, sometimes by a long period of time. Adding a `Bulk ID` or other marker to identify when a gift is part of a `submysterygift` would be extremely useful. The Emote Wall currently introduces a small delay of two seconds before a gift triggers a Kappagen, to check for additional `subgift` or `submysterygift` events. In certain cases, multiple individual kappagens may be triggered by a single bulk gift, even when a specific Kappagen has been set for bulk gifts. Switching to EventSub's `channel.chat.notification` event support may be required if the IRC API isn't improved.

> #### [Clearing Messages](//twitch.uservoice.com/forums/310213/suggestions/47556635)
> Deleting a message doesn't include the sender's account ID, which slows down erasing the message from the user's message cache in the Emote Wall.

> #### [Stream Tags](//twitch.uservoice.com/forums/310213/suggestions/46153474)
> Showing a kappagen when users mention a stream's tag in chat, the same way as users tagged in the stream title, would require tags to be included in `channel.update` events.

> #### [Scope Selection](//twitch.uservoice.com/forums/310213/suggestions/46215865)
> Choosing specific access scope is done through the website or the wizard before going to the Twitch site, which is a little awkward. Checkboxes on optional scopes would let you choose which access to give without listing every access type twice, once on my site, then again on Twitch's auth page.

> #### [Tip Messages](//twitch.uservoice.com/forums/310213/suggestions/43599900)
> Displaying the emotes in third-party donation/tip messages is currently impossible because you're not allowed to get a user's available emotes by API call. Instead, if the tip sender matches a Twitch account, the Emote Wall will use that account's profile photo as an emote for the triggered kappagen.

> #### [Redeems](//twitch.uservoice.com/forums/932221/suggestions/45492757)
> Channel point redeems show up as both EventSub events and IRC chat events, however there is no shared ID to help you tell that both messages are from a single event. Adding a shared ID would improve channel point redeem detection support.

> #### Legacy Emoji Workaround
> Twitch used to filter out the ZWJ (Zero-Width Joiner) character which is used for merging many emojis. The alternative character 0xE0002 may still replace ZWJs in some third-party Twitch chat projects, and will be correctly parsed as a ZWJ according to the rules laid out in the RFC:  
>
> [Emoji RFC](//gist.github.com/Mm2PL/982c76964fe53f80fcf6b6963bba049f)

### YouTube API
YouTube Livestream support is still under active development, and may not correctly support Monetized Channel events such as memberships, super chats, or stickers. It will, however, detect and send information on such events to the RealityRipple webserver for development purposes, if you enable the `feedback` option in the configuration. Additionally, due to the myriad limitations in the YouTube API, there is currently no method to load any custom channel emojis, and Google's interest in improving the API seems to be, essentially, nonexistent.  
Despite these numerous issues, the Emote Wall still functions on YouTube, and needs your feedback to improve! If you're monetized on YouTube, please let me know if membership and "super" events correctly trigger kappagen events for you!

> #### [Rate Limits](https://issuetracker.google.com/issues/271492711)
> No Server-Sent Events or WebSocket system exists, so clients must poll for new messages once a second, and this polling process is rate-limited. As a result, just reading chat eats up the rate limit quota for the entire project, for like... no reason.

> #### [Emoji Lookup](https://issuetracker.google.com/issues/263926623)
> There is no API for finding global or monetized channel emojis via an HTTP request. The chat system's `liveChatMessage` events likewise do not contain any custom emoji data.

> #### [Subscriber Status](https://issuetracker.google.com/issues/263926624)
> This is much the same as Twitch's follower detection, containing no tag (or property in YouTube's case) to determine if a user is a subscriber, with the inclusion of new subscribers having to be detected via list polling. To make matters worse, a user can make all subscriptions private through the Privacy Settings on YouTube, which also hides the user's subscription from the broadcaster, and thus the API. This means, if a user sets subscriptions to private, the Emote Wall will not know the user is a subscriber.
>
> Additionally, the use of the term "sponsor" instead of "member" has stuck around through the property they do include, but the tier isn't provided.

> #### [Uniform Errors](https://issuetracker.google.com/issues/287881893)
> The API returns differently formatted errors depending on where the error occurs in the API response process, making error handling a nightmare.

> #### [Membership Levels](https://issuetracker.google.com/issues/302886349)
> The different tiers of membership aren't actually organized or in any way comparable to one another.

> #### [Missing Events](https://issuetracker.google.com/issues/129240937)
> The `userBannedEvent` and `messageDeletedEvent` events don't even exist, despite being listed in documentation for years.

> #### [Documentation Issues](https://issuetracker.google.com/issues/304969295)
> Just another one of many problems with vague or incomplete documentation.

> #### [Membership API](https://issuetracker.google.com/issues/302817011)
> Access to member-specific APIs are behind a permission wall, but the documentation doesn't say who has to get permission: the developer or the streamer.

### OBS
This emote wall may do better if the browser source has a frame rate limit of 30 or 60. If you use your GPU while streaming, you may wish to disable Browser Source Hardware Acceleration. It may also work better using a smaller screen resolution (such as 720p on a 1080p screen) and then stretching the browser source to fit to the screen using the OBS Transform feature.

### Inefficiencies

- This emote wall uses normal &lt;img&gt; objects rather than a HTML Canvas. While this lowers efficiency, it also adds better GIF/WebP/AVIF file support and allows easier user manipulation.

- At present, the "zoom in" and "zoom out" feature uses a resource-heavy design. I had hoped the new CSS directive "[scale: ](//developer.mozilla.org/en-US/docs/Web/CSS/scale)" would have helped, however it's useless without a "scale-origin" directive to accompany it, as "[transform-origin](//developer.mozilla.org/en-US/docs/Web/CSS/transform-origin)" is already used for other purposes, and would awkwardly influence the zoom animation.

- The Bounce animation uses specific position-based drawing rather than actually being animated.

- The Cube animation uses eight objects on screen for every image, making it a particularly resource-heavy drawing.

- The Toroidal display feature also creates a dynamic number of objects on screen, to allow for seamless looping.

If your computer has trouble with this emote wall, please try disabling these options.
