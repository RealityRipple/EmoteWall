Configuration Information
-------------------------

* `twitch`   
  *Settings related to the Twitch login process.*

  > **NOTE**: OAuth refresh tokens expire automatically (usually after around half a year). If you don't use the Emote Wall for around this long, you may have to log in again. Regular OAuth tokens expire much sooner (usually after 60 days). If you use the manual oauth method, please make sure to update these values on a regular basis.

  * `channel`  
    *The name of the channel to join. Also used to choose an IRC nickname.*  
     - [ ] If `false`, the interactive login process will be enabled.

  * `client`  
    *The Client ID value is used to track which third-party project is accessing your account.*  
    This emote wall does not require a constant ID, and will work with whatever tool you use to get an OAuth ID (see below).

  * `oauth`   
    *The OAuth ID value is used in lieu of a password to access the Twitch API.*  
    By default, this value is not required.  
    If you do not wish to use the `oauth_refresh` method, which relies on a file on my webserver, you can generate your own OAuth2 token manually using a third-party Twitch Token Generator, and set this value to the token you receive. However, it will expire and require updating manually.

  * `oauth_refresh`  
    *A refresh token to get a new Twitch OAuth ID when the current one expires.*  
    This value is used instead of the oauth value above, by default. Using a refresh token allows the emote wall to stay logged in for a much longer period of time. Please note that this feature makes use of the browser's Local Storage to store new OAuth Tokens and Refresh Tokens as they're generated.  
    New OAuth Tokens are generated every 60 minutes, and Twitch may or may not send a new Refresh Token at the same time. If the token expires, the Local Storage values will be erased on the next refesh attempt automatically.

    > **How to generate an OAuth ID and matching Client ID:**
    > - Visit <https://realityripple.com/Tools/Twitch/EmoteWall/>
    > - Click the "Authenticate on Twitch" button under "Do-it-Yourself" and log in
    > - Fill out the captcha prompt, if necessary
    > - Copy the Client ID value and paste it into "client:"
    > - Copy the OAuth Refresh value and paste it into "oauth_refresh:"

    If you ever stop using this emote wall, please log into Twitch and visit <https://www.twitch.tv/settings/connections>. Under "Other Connections", click the "Disconnect" button next to "RealityRipple's Home-Made Emote Wall".

     - [ ] If both `oauth` and `oauth_refresh` are `false` (or missing), the interactive login process will be enabled.

  * `scope`  
    *A list of scopes which the OAuth ID provides access to.*  
    Please make sure this list reflects any scope selections you made while creating the token above.

  * `share`  
    *Share your Twitch channel on the Emote Wall home page!*

* `youtube`  
    *Settings related to the YouTube login process.*

  > **NOTE**: OAuth tokens expire automatically (usually after 60 days). Please make sure to update these values on a regular basis, if not using the interactive login process.

  * `client`  
    *The Client ID value is used to track which third-party project is accessing your account.*  
    This emote wall does not require a constant ID, and will work with whatever tool you use to get an OAuth ID (see below).

  * `oauth`  
    *The OAuth ID value is used in lieu of a password to access the Google API.*  
    By default, this value is not required.  
    If you do not wish to use the oauth_refresh method, which relies on a file on my webserver, you can generate your own OAuth2 token manually using a third-party YouTube Token Generator, and set this value to the token you receive. However, it will expire and require updating manually.

  * `oauth_refresh`  
    *A refresh token to get a new YouTube OAuth ID when the current one expires.*  
    This value is used instead of the oauth value above, by default. Using a refresh token allows the emote wall to stay logged in for a much longer period of time. Please note that this feature makes use of the browser's Local Storage to store new OAuth Tokens and Refresh Tokens as they're generated.  
    New OAuth Tokens are generated every 60 minutes, and YouTube may or may not send a new Refresh Token at the same time. If the token expires, the Local Storage values will be erased on the next refesh attempt automatically.

    > How to generate an OAuth ID and matching Client ID:
    > - Visit <https://realityripple.com/Tools/Twitch/EmoteWall/>
    > - Click the "Authenticate on YouTube" button under "Do-it-Yourself" and log in
    > - Fill out the captcha prompt, if necessary
    > - Copy the Client ID value and paste it into "client:"
    > - Copy the OAuth Refresh value and paste it into "oauth_refresh:"

    If you ever stop using this emote wall, please log into YouTube and visit <https://myaccount.google.com/permissions>. Under "Apps with access to your account", click the "Disconnect" button next to "RealityRipple's Home-Made Emote Wall".
     - [ ] If both `oauth` and `oauth_refresh` are `false` (or missing), the interactive login process will be enabled.

  * `connect_to`  
    *Settings to control which YouTube broadcast to connect to.*

    * `title`  
      *The broadcast title of the stream to connect to.*  
      This forces a specific connection, regardless of the status list (below). The `sort`, `max`, and `recheck` settings still apply, though, in case of multiple broadcasts with identical titles.

    * `list`  
      *An array of broadcast statuses which will be connected to.*  
      The list can include the following:
      | Status           | Meaning |
      | :----:           | :------ |
      | `'created'`      | The broadcast has incomplete settings, so it is not ready to transition to a `'live'` or `'testing'` status, but it has been created and is otherwise valid. |
      | `'ready'`        | The broadcast settings are complete and the broadcast can transition to a `'live'` or `'testing'` status. |
      | `'live'`         | The broadcast is active. |
      | `'liveStarting'` | The broadcast is in the process of transitioning to `'live'` status. |
      | `'testing'`      | The broadcast is only visible to the partner. |
      | `'testStarting'` | The broadcast is in the process of transitioning to `'testing'` status. |
      | `'complete'`     | The broadcast is finished. |
      | `'revoked'`      | This broadcast was removed by an admin action. |

    * `max`  
      *The maximum simultaneous chats to connect to.*  
      In most use cases, you will only need `1`, but rate limits allow up to `3` active connections at once.

    * `sort`  
      *An associative array of broadcast attributes and their sort order.*  
      The attributes can be any of these:
       | Attribute           | Meaning |
       | :-----------------: | :------ |
       | `'actualStartTime'` | The date and time that the broadcast actually started. Any non-live broadcasts will end up at the bottom of a list with this sort. |
       | `'publishedAt'`     | The date and time that the broadcast was added your live broadcast schedule.
       | `'title'`           | The broadcast's title, in localized alphabetical order.
       | `'description'`     | The broadcast's description, in localized alphabetical order.

      The value for each entry may be either `'desc'` or `'asc'` for descending or ascending order.

    * `recheck`  
      *A boolean value to determine if the Emote Wall should continue checking the status of broadcasts after a broadcast has already been successfully found.*
       - [ ] If `true`, broadcasts will be checked every 30 seconds.  
         - New broadcasts that match the above parameters will be connected to.  
         - Existing broadcasts that were matched and no longer match will be disconnected from.
       - [ ] If `false`, broadcasts will be checked every 30 seconds until a connection is made.  
         - Any matching broadcasts on the first success will be connected to.  
         - No further broadcast status checks will be made.  
         - No additional connections will be made, even if less than `max`.  
         - No existing broadcasts will be disconnected from.

  * `share`  
    *Share your YouTube channel on the Emote Wall home page!*

* `kick`  
  *Settings related to the Kick login process.*

  * `channel`  
    *The name of the channel to join.*
     - [ ] If `false`, no connection to Kick will be made.

* `streamlabs`
  *Settings related to Streamlabs tips.*

  * `token`  
    *The Socket Token is used in lieu of a password to access the Streamlabs API.*
     > How to generate a Socket Token:
     > - Visit <https://realityripple.com/Tools/Twitch/EmoteWall/>
     > - Click the "Streamlabs Tip Support" button and log in
     > - Copy the Token value and paste it into "token:"

    If you ever stop using this emote wall, please log into Streamlabs and visit <https://streamlabs.com/dashboard#/settings/api-settings>. Under "Connected Apps", click the "Revoke Access" button next to "RealityRipple's Home-Made Emote Wall". If you want to use a different Streamlabs OAuth generator (or do it yourself), feel free.

  * `curMul`  
    *This value is the currency multiplier.*  
    The ranges of Streamlabs `tip` entries (see below) will match against this multiplier. For example, if you use USD and want to set ranges by penny amount, then set this value to `100`. If you want to use dollar amounts, set the value to `1`.
     > **NOTE**: Any decimal amount will be rounded down after multiplying, so $3.95 will be handled as "395" pennies when multiplied by `100`, or "3" dollars when multiplied by `1`.

  * `dispMul`  
    *This value is the currency multiplier when the currency is being displayed.*  
    For kappagen events such as `'Text'`, the Streamlabs tip amount will be multiplied by this number before being displayed. For example, if you use USD and want to display the value as cents, then set this value to `100`. If you want to show dollar amounts, set this value to `1`.

  * `dispDec`  
    *This value is the decimal count when the currency is being displayed.*  
    After being multiplied by the dispMul value above, the Streamlabs tip amount will be rounded to this many decimal places. For example, an amount of $3.95 rounded to `0` decimal places will be "3", to `1` would be "3.9", and to `2` would be "3.95".

  * `dispPre`  
    *This value should be added before any currency amount as a prefix, such as a dollar sign (`'$'`).*

  * `dispSuf`  
    *This value should be added after any currency amount as a suffix, such as the word `' dollars'`.*  
    > **NOTE:** Usually only `dispPre` or `dispSuf` should be used, not both at the same time.

* `streamelements`  
  *Settings related to StreamElements tips.*  
     > **NOTE**: Please only use `oauth_refresh` or `token`, not both. `token` does not expire, but is also less secure. OAuth is recommended, if possible.

  * `oauth_refresh`  
    *A refresh token to get a new StreamElements OAuth ID when the current one expires.*  
    The OAuth ID value is used in lieu of a password to access the StreamElements API.
     > How to generate an OAuth ID:
     > - Visit <https://realityripple.com/Tools/Twitch/EmoteWall/>
     > - Click the "StreamElements Tip Support" button and log in
     > - Copy the Token value and paste it into "oauth_refresh:"

    If you ever stop using this emote wall, please log into StreamElements and visit <https://streamelements.com/dashboard/account/security>. Click the "Reset my Personal Access Token" button. If you want to use a different StreamElements OAuth generator (or do it yourself), feel free.  

  * `token`  
    *The JWT Token is used in lieu of a password to access the StreamElements API.*
     > How to grab your JWT Token from the StreamElements Dashboard:
     > - Visit <https://streamelements.com/dashboard/account/channels>
     > - Click the "Show secrets" button
     > - Copy the JWT Token value and paste it into "token:"

  * `curMul`  
    *This value is the currency multiplier.*  
    The ranges of StreamElements tip entries (see below) will match against this multiplier. For example, if you use USD and want to set ranges by penny amount, then set this value to `100`. If you want to use dollar amounts, set the value to `1`.
     > **NOTE**: Any decimal amount will be rounded down after multiplying, so $3.95 will be handled as "395" pennies when multiplied by `100`, or "3" dollars when multiplied by `1`.

  * `dispMul`  
    *This value is the currency multiplier when the currency is being displayed.*  
    For kappagen events such as `'Text'`, the StreamElements tip amount will be multiplied by this number before being displayed. For example, if you use USD and want to display the value as cents, then set this value to `100`. If you want to show dollar amounts, set this value to `1`.

  * `dispDec`  
    *This value is the decimal count when the currency is being displayed.*  
    After being multiplied by the dispMul value above, the StreamElements tip amount will be rounded to this many decimal places. For example, an amount of $3.95 rounded to `0` decimal places will be "3", to `1` would be "3.9", and to `2` would be "3.95".

  * `dispPre`  
    *This value should be added before any currency amount as a prefix, such as a dollar sign (`'$'`).*

  * `dispSuf`  
    *This value should be added after any currency amount as a suffix, such as the word `' dollars'`.*  
    > **NOTE:** Usually only `dispPre` or `dispSuf` should be used, not both at the same time.

* `display`  
  *Settings related to the animation of the emote wall.*

  * `styles`  
    *An array of animation styles which individual emotes randomly perform.*  
    You may turn on and off elements in this array by "commenting out" a style, by putting two slashes before the name:
    ```
    // 'Still',        <-- disabled
       'StraightLine', <-- allowed
    ```

  * `access`  
    *A bitwise flag representing which users' messages show up on the emote wall.*  
    Account types are represented by the following values:
    |   Flag  | Meaning                  | Twitch | YouTube | Kick | Variations     |
    | ------: | :----------------------- | :----: | :-----: | :--: | :------------- |
    | `0x800` | broadcaster              |   T    |   YT    |  K   |                |
    | `0x400` | moderator badge          |   T    |   YT    |  K   |                |
    | `0x200` | founder badge            |   T    |         |  K   |                |
    | `0x100` | vip badge                |   T    |         |  K   |                |
    | `0x080` | artist badge             |   T    |         |      |                |
    | `0x040` | tier 3 subscriber badge  |   T    |         |  K   | K: OG          |
    | `0x020` | tier 2 subscriber badge  |   T    |         |      |                |
    | `0x010` | tier 1 subscriber badge  |   T    |   YT    |  K   | YT: Member     |
    | `0x008` | verified user            |        |   YT    |  K   |                |
    | `0x004` | cheer badge              |   T    |         |      |                |
    | `0x002` | follower                 |   T    |   YT    |  K   | YT: Subscriber |
    | `0x001` | stranger                 |   T    |   YT    |  K   |                |

    Just put a vertical pipe (`|`) in between each of the values representing levels of access:
    | Access                                      | Meaning                                                |
    | :------------------------------------------ | :----------------------------------------------------- |
    | `0x800 \| 0x400`                            | broadcaster and moderator only                         |
    | `0x800 \| 0x400 \| 0x100 \| 0x040 \| 0x020` | broadcasters, mods, VIPs, and tier 2 and 3 subscribers |
    | `0x800 \| 0x010 \| 0x002`                   | boradcaster, tier 1 subscribers, and followers         |

    If you know how bitwise flags work, you can also use them in more complicated ways:
    | Access          | Meaning                                     |
    | :-------------- | :------------------------------------------ |
    | `0xFFF`         | all users from the broadcaster to strangers |
    | `0xFFF ^ 0x003` | all users except followers and strangers    |
    | `0x070`         | all subscribers                             |

  * `duplicates`  
    *A boolean or integer to toggle duplicate emotes per message.*
     - [ ] If `true`, every emote posted in chat will be shown.
     - [ ] If `false`, only one of each emote per message will be shown.
     - [ ] If `greater than 1`, sets the maximum number of identical emotes shown from any message.

  * `useEmoji`  
    *Toggles display of emojis on the emote wall, and lets you choose an emoji font style.*
     - [ ] If `true`, emojis will be shown using the "**twemoji**" font.
     - [ ] If `false`, emojis will not be shown on the emote wall.
     - [ ] If `'twemoji'`, emojis will be shown using the "**twemoji**" font.
     - [ ] If `'openmoji'`, emojis will be shown using the "**openmoji**" font.
     - [ ] If `'noto'`, emojis will be shown using the "**noto**" font.
     - [ ] If `'blob'`, emojis will be shown using the "**blobmoji**" font.

  * `extended`  
    *Settings related to third-party emotes.*

    * `useFFZ`  
      *Toggles display of FrankerFaceZ emotes.*

    * `useBTTV`  
      *Toggles display of BetterTTV emotes.*

    * `use7TV`  
      *Toggles display of 7TV emotes.*  
      This value may also be set to the string `'AVIF'`. If set, 7TV emotes will use the AVIF format instead of the WebP format.

    * `useZWE`  
      *Toggles display of Zero-Width (overlapping) emotes.*  
      If `false`, this will hide ZWEs entirely.
       > **NOTE**: ZWE display requires more objects on-screen, which can be process-intensive, and precise timing is required for accurate overlay. ***CHAOS MAY ENSUE***.

    * `fillZWE`  
      *Toggles the fill style of Zero-Width (overlapping) emotes.*
      - [ ] If `true`, ZWEs will be stretched or squashed to fit non-square emotes.
      - [ ] If `false`, ZWEs will be placed in the center of non-square emotes.

  * `hue`  
    *Rotate the hue of all emotes.*
     - [ ] If a number between `1` and `359`, all colors will be rotated by that many degrees.
     - [ ] If `'rave'`, all colors will constantly rotate.
     - [ ] Otherwise, no color rotation will occur.
     > **NOTE**: If a command to toggle rave or turn rave on exists, rave will be off at startup.

  * `kappa`  
    *Settings related to emote-splosions and the !kappagen command.*

    * `count`  
      *The number of emotes to display per kappagen.*  
      This value should be less than the emote `max` value seen below (best would be 1/4th or less), if `"cfg.display.emote.max"` is used, or it will be truncated to match.

    * `styles`  
      *Similar to the array of styles for normal emotes, but this one lists emote-splosion types.*   
      Please do not try to add normal styles to the kappa list or vice versa. This is an associative array which can have custom settings for certain styles (namely `'TheCube'` and `'Text'` - see below).

      * `[ALL]`  
        *Settings related to multiple kappagens.*  
        These settings will be the default for all instances of their respective kappagens. Each setting below may or may not apply to a specific kappagen style.

        * `count`  
          *The number of emotes to display for this specific kappagen.*  
          This value should be less than the emote `max` value seen below (best would be 1/4th or less), if `"cfg.display.emote.max"` is used, or it will be truncated to match. If unset, this will default to the global kappa count preference listed above.
           > **NOTE**: If this preference is in an event below (not in this general kappa context), then an additional value is possible: `-1`, which will refer to the AMOUNT value present in the event. This can be the number of raiders, bits cheered, dollars tipped, subs gifted, or months subscribed.

      * `Conga`  
        *Settings related to Conga kappagen.*  
        These settings will override the default for all instances of `'Conga'` kappagen.

        * `avoidMiddle`
           - [ ] If `true`, conga lines will only show up on the top or bottom three rows to avoid the middle of the screen.
           - [ ] If `false`, conga lines will show up on any row of the screen.

      * `TheCube`  
        *Settings related to The Cube kappagen.*  
        These settings will be the default for all instances of `'TheCube'` kappagen.

        * `size`  
          *A decimal value representing the height of The Cube kappagen, relative to the smallest screen dimension.*  
          If the height of the screen is less than the width, each emote will be equal to the height of the screen multiplied by this ratio.  
          Suggested: `8 / 10` (80%).

        * `center`
           - [ ] If `true`, The Cube will show up in the exact center of the screen.
           - [ ] If `false`, The Cube will show up in a random location.

        * `rotations`  
          *The maximum number of rotations a kappa cube might spin while on screen.*  
          This effectively controls the maximum possible speed at which cubes will rotate.

      * `Text`  
        *Settings related to Text kappagen.*  
        These settings will be the default for all instances of `'Text'` kapagen.

        * `message`  
          *An array of alphanumeric strings (letters, numbers, and spaces), one of which will randomly be used.*

        * `time`  
          *The number of seconds the `'Text'` kappagen should show the final result for.*  
          This value should be adjusted depending on the average message length, for readability.

    * `access`  
      *Similar to the access flag for normal emotes, but controls which users can use the !kappagen command.*

    * `aliases`  
      *An array of kappagen command aliases which can be used to force-trigger kappagens.*

    * `cooldown`  
      *The number of seconds between force-triggered kappagens using an above alias.*  
      Any commands sent before the cooldown will be ignored, unless the another command shares the same alias.

    * `conga`  
      *Global settings related to Conga kappagen.*

      * `contagious`  
        This setting applies to all `'Conga'` kappagens.
         - [ ] If `true`, while one `'Conga'` kappagen is visible, all additional kappagens will also be `'Conga'`.
         - [ ] If `false`, `'Conga'` kappagns will behave like any other kappagen.

      * `time`  
        *The number of seconds the `'Conga'` kappagen should show up on the screen for.*  
        This setting applies to all `'Conga'` kappagens.  
        This value lets you increase or decrease the chances of keeping a "contagious" `'Conga'` line going.

      * `avoidMiddle`  
        This setting will be the default for all instances of `'Conga'` kappagen.  
         - [ ] If `true`, `'Conga'` lines will only show up on the top or bottom three rows to avoid the middle of the screen globally.
         - [ ] If `false`, the setting will default to any more specific avoidMiddle `'Conga'` settings.

  * `statuses`  
    *Display status notices whenever a connection is made or a connection issue occurs.*
    - [ ] If `true`, any changes in connectivity will show a notice for a moment.
    - [ ] If `false`, no status information will be displayed.

* `emote`  
  *Settings related to individual emote display.*

  * `time`  
    *The number of seconds an emote should show up on the screen for.*

  * `max`  
    *The maximum nuber of emotes to show on the screen at one time.*  
    Set this value to `0` for infinite emotes.  
    This value should be greater than any kappa `count` values seen above or below (best would be 4x or more), as it will limit any single kappagen events to this maximum.

  * `queue`  
    *The maximum number of emotes to save in queue.*  
    Set this value to `0` for an infinite queue.  
    This value will be ignored if the previous value (`"cfg.emote.max"`) is infinite (`0`).

  * `size`  
    *Settings related to the size of emotes.*

    * `ratio`  
      *Emotes show up in multiple sizes due to the kappagen feature.*  
      There are a total of five sizes that an emote can be:
      - [ ] `'TheCube'` kappagen's faces are squares equal to 80% of the smaller screen dimension (usually height on PC).
      - [ ] `'Pyramid'` kappagen emotes have a height equal to 1/19th of the screen's width (changes with the `pyramidDist` array).
      - [ ] `'Text'` kappagen emotes are dynamically sized to allow the message to fit on the screen.
      - [ ] `'Fireworks'`, `'Spiral'`, and `'Confetti'` kappagen emotes have a height equal to the `small` ratio (see below).
      - [ ] All standard emotes and kappagens not listed above will use the `normal` ratio (see below).

      Most normal emotes will limit by height, except `'TheCube'`, which fits in the center of every side, and `'Pyramid'`, `'SmallPyramid'`, `'Text'`, and `'Conga'`, which need squares to work correctly.

      * `normal`  
        *A decimal value representing the height of each emote, relative to the smallest screen dimension.*  
        If the height of the screen is less than the width, each emote will be equal to the height of the screen multiplied by this ratio. Suggested `1 / n` where `n` is greater than `10`.

      * `small`  
        *A decimal value representing the height of small emotes, relative to the smallest screen dimension.*  
        If the height of the screen is less than the width, each emote will be equal to the height of the screen multiplied by this ratio. Suggested `1 / n` where `n` is greater than `20`.

    * `min`  
      *The minimum height of an emote, in pixels.*

    * `max`  
      *The maximum height of an emote, in pixels.*

    * `variation`  
      *An integer variable that determines how often occasional random large or small emotes show up.*
      - [ ] If `false`, no variations will occur.

  * `cube`  
    *Settings related to The Cube emote.*

    * `rotations`  
      *The maximum number of rotations a cube might spin while on screen.*  
      This effectively controls the maximum possible speed at which cubes will rotate.

  * `in`  
    *Settings related to the showing of an emote.*
    > **NOTE**: Some kappagen styles do not use these. See the notes next to each kappagen style name.

    * `fade`  
      *A boolean to toggle the "fade in" style.*

    * `zoom`  
      *A boolean to toggle the "zoom in" style.*

  * `out`  
    *Settings related to the hiding of an emote.*
    > **NOTE**: Some kappagen styles do not use these. See the notes next to each kappagen style name.

    * `fade`  
      *A boolean to toggle the "fade out" style.*

    * `zoom`  
      *A boolean to toggle the "zoom out" style.*

* `event`  
  *Settings related to channel events which trigger emote-splosions (kappagen).*

  * `twitch`  
    *Settings related to Twitch channel events.*

    * `clear`  
      *A boolean to toggle clearing the screen when chat is cleared.*  
      - [ ] If `true`, the emote wall will be cleared when the `/clear` command is used.
      - [ ] If `false`, the emote wall will ignore the `/clear` command.

    * `raid`  
      *Settings related to kappagens when being raided.*

      * `raiders`  
        *A streamer raids the channel with viewers.*  
        This value can be a boolean, integer, or array:
        - [ ] If `true`, a kappagen will occur on all raids.
        - [ ] If `false`, no kappagen will occur on raids.
        - [ ] If Integer, the value is the minimum raiders required for a raid to trigger a kappagen.
          - [ ] If `0`, no kappagen will occur on raid.
        - [ ] If Array, each key of the array should be a string containing a range of integers, such as `'1'`, `'2-4'` or `'5-9'`, or an open-maximum range such as `'10+'`.  
        Each value can be a boolean or array:
          - [ ] If `true`, a kappagen will occur.
          - [ ] If `false`, no kappagen will occur.
          - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

      * `originEmotes`  
        *A boolean to toggle the use of the raiding streamer's channel emotes for raid kappagens.*
        - [ ] If `true`, raid kappagens will use channel emotes from the raider's channel.
        - [ ] If `false`, raid kappagens will use your channel's emotes.

      * `originExtendedEmotes` -- A boolean to toggle third-party emotes, if originEmotes is enabled.

    * `follow`  
      *A user follows the channel.*  
       Requires `moderator:read:followers` scope.  
       This value can be a boolean or array:
      - [ ] If `true`, a kappagen will occur.
      - [ ] If `false`, no kappagen will occur.
      - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

    * `shoutout`  
       *Settings related to kappagens on a shoutout event.*  
       Requires `moderator:read:shoutouts` scope.

      * `create`  
        *Settings related to kappagens when you shout another channel out.*

        * `styles`  
          *You shout another channel out.*  
          This value can be a boolean or array:
          - [ ] If `true`, a kappagen will occur.
          - [ ] If `false`, no kappagen will occur.
          - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

        * `targetEmotes`  
          *A boolean to toggle the use of the target channel's emotes for shoutout kappagens.*
          - [ ] If `true`, shoutout kappagens will use channel emotes from the target's channel.
          - [ ] If `false`, shoutout kappagens will use your channel's emotes.

        * `targetExtendedEmotes`  
          *A boolean to toggle third-party emotes, if `targetEmotes` is enabled.*

      * `receive`  
        *Settings related to kappagens when another channel shouts you out.*

        * `styles`  
          *You are shouted out by another channel.*  
          This value can be a boolean or array:
          - [ ] If `true`, a kappagen will occur.
          - [ ] If `false`, no kappagen will occur.
          - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

        * `originEmotes`  
          *A boolean to toggle the use of the source channel's emotes for shoutout kappagens.*
          - [ ] If `true`, shoutout kappagens will use channel emotes from the source's channel.
          - [ ] If `false`, shoutout kappagens will use your channel's emotes.

        * `originExtendedEmotes`  
          *A boolean to toggle third-party emotes, if `originEmotes` is enabled.*

    * `tag`  
      *Settings related to kappagens when users tag a channel you've tagged in your stream title.*

      * `styles`  
        *A user posts a message that starts with `"@user"`.*  
        This value can be a boolean or array:
        - [ ] If `true`, a kappagen will occur.
        - [ ] If `false`, no kappagen will occur.
        - [ ]  If an array of kappa styles, a kappagen of one of the listed styles will occur.

      * `access`  
        *A bitwise flag representing which users can trigger this kappagen with a command.*  
        This value will fall back to the general kappagen access value if missing or less than `0`.

      * `targetEmotes`  
        *A boolean to toggle the use of the target channel's emotes for tag kappagens.*
        - [ ] If `true`, tag kappagens will use channel emotes from the target's channel.
        - [ ] If `false`, tag kappagens will use your channel's emotes.

      * `targetExtendedEmotes`  
        *A boolean to toggle third-party emotes, if `targetEmotes` is enabled.*

    * `sub`  
      *Settings related to kappagens on a subscribe event.*

      * `useMsg`  
        - [ ] If `true`, any emotes in resub messages will be used for the kappagen.
        - [ ] If `false`, any emotes in resub messages will show up like normal emotes.

      * `t1`  
        *Settings related to kappagens on a **Tier 1** subscribe event.*

        * `first`  
          *A user subscribes at **Tier 1** for the first time.*  
          This value can be a boolean or array:
          - [ ] If `true`, a kappagen will occur.
          - [ ] If `false`, no kappagen will occur.
          - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

        * `resub`  
          *A user resubscribes at **Tier 1**.*  
          This value can be a boolean, integer, or array:
          - [ ] If `true`, a kappagen will occur on all **Tier 1** resubs.
          - [ ] If `false`, no kappagen will occur on **Tier 1** resubs.
          - [ ] If Integer, the value is the minimum months required for a **Tier 1** resub to trigger a kappagen.
            - [ ] If `0`, no kappagen will occur.
            - [ ] If `1`, a kappagen will occur every month.
            - [ ] If `greater than 1`, the number of months subscribed must be greater than or equal to this number to trigger a kappagen.
          - [ ] If Array, each key of the array should be a string containing a range of integers, such as `'1'`, `'2-4'` or `'5-9'`, or an open-maximum range such as `'10+'`.  
             Each value can be a boolean or array:
            - [ ] If `true`, a kappagen will occur.
            - [ ] If `false`, no kappagen will occur.
            - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

        * `upgrade`  
          *Settings related to "converted" subscriptions.*

          * `gift`  
            *A user upgrades a gift sub to **Tier 1**.*  
            This value can be a boolean or array:
            - [ ] If `true`, a kappagen will occur.
            - [ ] If `false`, no kappagen will occur.
            - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

          * `prime`  
            *A user upgrades a **Prime** sub to **Tier 1**.*  
            This value can be a boolean or array:
            - [ ] If `true`, a kappagen will occur.
            - [ ] If `false`, no kappagen will occur.
            - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

        * `gift`  
          *Settings related to *Tier 1* gifts.*

          * `first`  
            *A user gifts another user their first **Tier 1** subscription.*  
            This value can be a boolean or array:
            - [ ] If `true`, a kappagen will occur.
            - [ ] If `false`, no kappagen will occur.
            - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

          * `resub`  
            *A user gifts another user a **Tier 1** resubscription.*  
            This value can be a boolean, integer, or array:
            - [ ] If `true`, a kappagen will occur on all **Tier 1** gift resubs.
            - [ ] If `false`, no kappagen will occur on **Tier 1** gift resubs.
            - [ ] If Integer, the value is the minimum months required for a **Tier 1** gift resub to trigger a kappagen.
              - [ ] If `0`, no kappagen will occur.
              - [ ] If `1`, a kappagen will occur every month.
              - [ ] If `greater than 1`, the number of months subscribed must be greater than or equal to this number
              to trigger a kappagen.
            - [ ] If Array, each key of the array should be a string containing a range of integers, such as `'1'`, `'2-4'` or `'5-9'`, or an open-maximum range such as `'10+'`.  
             Each value can be a boolean or array:
              - [ ] If `true`, a kappagen will occur.
              - [ ] If `false`, no kappagen will occur.
              - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

          * `bomb`  
            *A user gifts multiple **Tier 1** subscriptions.*  
            This value can be a boolean, integer, or array:
            - [ ] If `true`, a kappagen will occur on any random gift.
            - [ ] If `false`, no kappagen will occur on giftbombs.
            - [ ] If Integer, the value is the minimum gifts required for a gift bomb to trigger a kappagen.
              - [ ] If `0`, no kappagen will occur.
              - [ ] If `1`, a kappagen will occur on any random gift.
              - [ ] If `greater than 1`, the number of gifted users in a **Tier 1** giftbomb must be greater than or equal to this number to trigger a kappagen.
            - [ ]  If Array, each key of the array should be a string containing a range of integers, such as `'1'`, `'2-4'` or `'5-9'`, or an open-maximum range such as `'10+'`.  
             Each value can be a boolean or array:
              - [ ] If `true`, a kappagen will occur.
              - [ ] If `false`, no kappagen will occur.
              - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

      * `t2`  
        *Identical to `t1`, but for **Tier 2** subscriptions.*

      * `t3`  
        *Identical to `t1`, but for **Tier 3** subscriptions.*

      * `prime`  
        *Settings related to kappagens on an Amazon **Prime** subscribe event.*

        * `first`  
          *A user subscribes with **Prime** for the first time.*  
          This value can be a boolean or array:
          - [ ] If `true`, a kappagen will occur.
          - [ ] If `false`, no kappagen will occur.
          - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

        * `resub`  
          *A user resubscribes with **Prime**.*  
          This value can be a boolean, integer, or array:
          - [ ] If `true`, a kappagen will occur on all **Prime** resubs.
          - [ ] If `false`, no kappagen will occur on **Prime** resubs.
          - [ ] If Integer, the value is the minimum months required for a **Prime** resub to trigger a kappagen.
            - [ ] If `0`, no kappagen will occur.
            - [ ] If `1`, a kappagen will occur every month.
            - [ ] If `greater than 1`, the number of months subscribed must be greater than or equal to this number to trigger a kappagen.
          - [ ] If Array, each key of the array should be a string containing a range of integers, such as `'1'`, `'2-4'` or `'5-9'`, or an open-maximum range such as `'10+'`.  
             Each value can be a boolean or array:
            - [ ] If `true`, a kappagen will occur.
            - [ ] If `false`, no kappagen will occur.
            - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

    * `cheer`
      *Settings related to kappagens on a cheer event.*

      * `useMsg`
        - [ ] If `true`, any emotes in cheer messages will also be included in the kappagen.
        - [ ] If `false`, any emotes in cheer messages will show up like normal emotes.

      * `bits`
        *Minimum number of bits for a kappagen.*  
        This value can be a boolean, integer, or array:
        - [ ] If `true`, a kappagen will occur on all cheers.
        - [ ] If `false`, no kappagen will occur on cheers.
        - [ ]  If Integer, the value is the minimum bits required for a cheer to trigger a kappagen.
          - [ ] If `0`, no kappagen will occur on cheer.
        - [ ] If Array, each key of the array should be a string containing a range of integers, such as `'1'`, `'2-499'` or `'2500-4999'`, or an open-maximum range such as `'7500+'`.  
        Each value can be a boolean or array:
          - [ ] If `true`, a kappagen will occur.
          - [ ] If `false`, no kappagen will occur.
          - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

    * `hypechat`
      *Settings related to kappagens on a hype chat event.*

      * `useMsg`
        - [ ] If `true`, any emotes in hype chat messages will also be included in the kappagen.
        - [ ] If `false`, any emotes in hype chat messages will show up like normal emotes.

      * `level`
        *Minimum number of level for a kappagen.*  
        This value can be a boolean, integer, or array:
        - [ ] If `true`, a kappagen will occur on all hype chats.
        - [ ] If `false`, no kappagen will occur on hype chats.
        - [ ]  If Integer, the value is the minimum level required for a hype chat to trigger a kappagen.
          - [ ] If `0`, no kappagen will occur on hype chat.
        - [ ] If Array, each key of the array should be a string containing a range of integers, such as `'1'`, `'2-4'` or `'5-8'`, or an open-maximum range such as `'9+'`.  
        Each value can be a boolean or array:
          - [ ] If `true`, a kappagen will occur.
          - [ ] If `false`, no kappagen will occur.
          - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

    * `badge`  
      *Settings related to users earning bits badges.*  
      This section is more "fluid" than other sections.  
      Each entry is a number (in string form) representing a bits badge and a kappa boolean/array value:  
      ```
      '1': false,
      '100': true,
      '5000': ['Rise', 'Conga']
      ```
       - [ ] If value is `true`, a kappagen will occur when a user earns a bit badge.
       - [ ] If value is `false`, no kappagen will occur when a user earns a bit badge.
       - [ ] If value is an array of kappa styles, a kappagen of one of the listed styles will occur for bit badges.

      If a user earns a bits badge for a number not listed in the array, the system will find the number which is closest to the badge, favoring the lower number in case of a tie.  
      For example:
      ```
      badge: {
       '100': false,
       '5000': true
      }
      ```
      If a user earns a `1000 bits` badge, no kappagen will occur because `1000` is closer to `100` than `5000`.  
      If a user earns their `10000 bits` badge, a kappagen will occur because `5000` is the closest listed number.
      > **NOTE**: The numbers must be strings (in either 'single' or "double" quotes) to function properly.

    * `hypetrain`  
      *Settings related to hype trains.*  
      Requires `channel:read:hype_train` scope.
 
      * `begin`  
        *A hype train begins in your channel.*  
        This value can be a boolean or array:
        - [ ] If `true`, a kappagen will occur.
        - [ ] If `false`, no kappagen will occur.
        - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

      * `success`  
        *Minimum level for a kappagen on hype train completion.*  
        This value can be a boolean, integer, or array:
        - [ ] If `true`, a kappagen will occur on all hype train completions.
        - [ ] If `false`, no kappagen will occur on hype train completions.
        - [ ] If Integer, the value is the minimum level required for a hype train to trigger a kappagen.
          - [ ] If `0`, no kappagen will occur on hype train success.
        - [ ] If Array, each key of the array should be a string containing a range of integers, such as `'1'`, `'2-5'` or `'6-10'`, or an open-maximum range such as `'11+'`.  
        Each value can be a boolean or array:
          - [ ] If `true`, a kappagen will occur.
          - [ ] If `false`, no kappagen will occur.
          - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

    * `poll`  
      *Settings related to polls.*  
      Requires `channel:read:polls` scope.

      * `begin`  
        *A poll begins in your channel.*  
        This value can be a boolean or array:
        - [ ] If `true`, a kappagen will occur.
        - [ ] If `false`, no kappagen will occur.
        - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

      * `end`  
        *A poll ends in your channel.*  
        This value can be a boolean or array:
        - [ ] If `true`, a kappagen will occur.
        - [ ] If `false`, no kappagen will occur.
        - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

    * `prediction`  
      *Settings related to predictions.*  
      Requires `channel:read:predictions` scope.

      * `begin`  
        *A prediction begins in your channel.*  
        This value can be a boolean or array:
        - [ ] If `true`, a kappagen will occur.
        - [ ] If `false`, no kappagen will occur.
        - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

      * `resolved`  
        *A prediction ends in your channel.*  
        This value can be a boolean or array:
        - [ ] If `true`, a kappagen will occur.
        - [ ] If `false`, no kappagen will occur.
        - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

    * `goal`  
      *Settings related to goals.*    
      Requires `channel:read:goals` scope.

      * `begin`  
        *A goal begins in your channel.*  
        This value can be a boolean or array:
        - [ ] If `true`, a kappagen will occur.
        - [ ] If `false`, no kappagen will occur.
        - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

      * `achieved`  
        *A goal ends in your channel.*  
        This value can be a boolean or array:
        - [ ] If `true`, a kappagen will occur.
        - [ ] If `false`, no kappagen will occur.
        - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

    * `charity`  
      *A charity donation is made in the channel.*  
      Requires `channel:read:charity` scope.  
      This value can be a boolean or array:
      - [ ] If `true`, a kappagen will occur.
      - [ ] If `false`, no kappagen will occur.
      - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

    * `timeout`  
      *Minimum time for a kappagen when a user is timed out.*  
      This value can be a boolean, integer, or array:
      - [ ] If `true`, a kappagen will occur on all timeouts.
      - [ ] If `false`, no kappagen will occur on timeouts.
      - [ ] If Integer, the value is the minimum seconds required for a timeout to trigger a kappagen.
        - [ ] If `0`, no kappagen will occur on timeouts.
      - [ ] If Array, each key of the array should be a string containing a range of integers, such as `'1'`, `'5-30'` or `'60-180'`, or an open-maximum range such as `'300+'`.  
      Each value can be a boolean or array:
        - [ ] If `true`, a kappagen will occur.
        - [ ] If `false`, no kappagen will occur.
        - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

    * `ban`  
      *A user is banned in the channel.*  
      This value can be a boolean or array:
      - [ ] If `true`, a kappagen will occur.
      - [ ] If `false`, no kappagen will occur.
      - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

  * `youtube`  
    *Settings related to YouTube channel events.*

    * `sub`  
      *A user subscribes the channel.*  
      This value can be a boolean or array:
      - [ ] If `true`, a kappagen will occur.
      - [ ] If `false`, no kappagen will occur.
      - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

    * `member`  
      *Settings related to kappagens on a membership event.*

      * `useMsg`  
        - [ ] If `true`, any emotes in member milestone messages will be used for the kappagen.
        - [ ] If `false`, any emotes in member milestone messages will show up like normal emotes.

      * `first`  
        *A user becomes a member for the first time.*  
        This value can be a boolean or array:
        - [ ] If `true`, a kappagen will occur.
        - [ ] If `false`, no kappagen will occur.
        - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

      * `milestone`  
        *A user reaches a membership milestone.*  
        This value can be a boolean, integer, or array:
        - [ ] If `true`, a kappagen will occur on all milestones.
        - [ ] If `false`, no kappagen will occur on milestones.
        - [ ] If Integer, the value is the minimum months required for a milestone to trigger a kappagen.
          - [ ] If `0`, no kappagen will occur.
          - [ ] If `1`, a kappagen will occur every month.
          - [ ] If `greater than 1`, the number of months as a member must be greater than or equal to this number to trigger a kappagen.
        - [ ] If Array, each key of the array should be a string containing a range of integers, such as `'1'`, `'2-4'` or `'5-9'`, or an open-maximum range such as `'10+'`.  
        Each value can be a boolean or array:
          - [ ] If `true`, a kappagen will occur.
          - [ ] If `false`, no kappagen will occur.
          - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

      * `giftbomb`  
        *A user gifts multiple memberships.*  
        This value can be a boolean, integer, or array:
        - [ ] If `true`, a kappagen will occur on any random gift.
        - [ ] If `false`, no kappagen will occur on giftbombs.
        - [ ] If Integer, the value is the minimum gifts required for a gift bomb to trigger a kappagen.
          - [ ] If `0`, no kappagen will occur.
          - [ ] If `1`, a kappagen will occur on any random gift.
          - [ ] If `greater than 1`, the number of gifted users in a giftbomb must be greater than or equal to this number to trigger a kappagen.
        - [ ] If Array, each key of the array should be a string containing a range of integers, such as `'1'`, `'2-4'` or `'5-9'`, or an open-maximum range such as `'10+'`.  
        Each value can be a boolean or array:
          - [ ] If `true`, a kappagen will occur.
          - [ ] If `false`, no kappagen will occur.
          - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

    * `superchat`  
      *A user posts a superchat in the channel.*  
      This value can be a boolean or array:
      - [ ] If `true`, a kappagen will occur.
      - [ ] If `false`, no kappagen will occur.
      - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

    * `supersticker`  
      *A user posts a sticker in the channel.*  
      This value can be a boolean or array:
      - [ ] If `true`, a kappagen will occur.
      - [ ] If `false`, no kappagen will occur.
      - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

  * `kick`  
    *Settings related to Kick channel events.*

    * `clear`  
      *A boolean to toggle clearing the screen when chat is cleared.*
      - [ ] If `true`, the emote wall will be cleared when the `/clear` command is used.
      - [ ] If `false`, the emote wall will ignore the `/clear` command.

    * `raid`  
      *Settings related to kappagens when being raided (hosted).*

      * `raiders`  
        *A streamer raids the channel with viewers.*  
        This value can be a boolean, integer, or array:
        - [ ] If `true`, a kappagen will occur on all raids.
        - [ ] If `false`, no kappagen will occur on raids.
        - [ ] If Integer, the value is the minimum raiders required for a raid to trigger a kappagen.
          - [ ] If `0`, no kappagen will occur on raid.
        - [ ] If Array, each key of the array should be a string containing a range of integers, such as `'1'`, `'2-4'` or `'5-9'`, or an open-maximum range such as `'10+'`.  
        Each value can be a boolean or array:
          - [ ] If `true`, a kappagen will occur.
          - [ ] If `false`, no kappagen will occur.
          - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

      * `originEmotes`  
        *A boolean to toggle the use of the raiding streamer's channel emotes for raid kappagens.*
        - [ ] If `true`, raid kappagens will use channel emotes from the raider's channel.
        - [ ] If `false`, raid kappagens will use your channel's emotes.

      * `originExtendedEmotes`  
        *A boolean to toggle third-party emotes, if originEmotes is enabled.*

    * `follow`  
      *A user follows the channel.*  
      This value can be a boolean or array:
      - [ ] If `true`, a kappagen will occur.
      - [ ] If `false`, no kappagen will occur.
      - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

    * `sub`  
      *Settings related to kappagens on a subscribe event.*

      * `first`  
        *A user subscribes for the first time.*  
        This value can be a boolean or array:
        - [ ] If `true`, a kappagen will occur.
        - [ ] If `false`, no kappagen will occur.
        - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

      * `resub`  
        *A user resubscribes.*  
        This value can be a boolean, integer, or array:
        - [ ] If `true`, a kappagen will occur on all resubs.
        - [ ] If `false`, no kappagen will occur on resubs.
        - [ ]  If Integer, the value is the minimum months required for a resub to trigger a kappagen.
          - [ ] If `0`, no kappagen will occur.
          - [ ] If `1`, a kappagen will occur every month.
          - [ ] If `greater than 1`, the number of months subscribed must be greater than or equal to this number to trigger a kappagen.
        - [ ] If Array, each key of the array should be a string containing a range of integers, such as `'1'`, `'2-4'` or `'5-9'`, or an open-maximum range such as `'10+'`.  
        Each value can be a boolean or array:
          - [ ] If `true`, a kappagen will occur.
          - [ ] If `false`, no kappagen will occur.
          - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

      * `gift`  
        *A user gifts another user a subscription.*  
        This value can be a boolean or array:
        - [ ] If `true`, a kappagen will occur.
        - [ ] If `false`, no kappagen will occur.
        - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

      * `giftbomb`  
        *A user gifts multiple subscriptions.*  
        This value can be a boolean, integer, or array:
        - [ ] If `true`, a kappagen will occur on any random gift.
        - [ ] If `false`, no kappagen will occur on giftbombs.
        - [ ]  If Integer, the value is the minimum gifts required for a gift bomb to trigger a kappagen.
          - [ ] If `0`, no kappagen will occur.
          - [ ] If `1`, a kappagen will occur on any random gift.
          - [ ] If `greater than 1`, the number of gifted users in a giftbomb must be greater than or equal to this number to trigger a kappagen.
        - [ ] If Array, each key of the array should be a string containing a range of integers, such as `'1'`, `'2-4'` or `'5-9'`, or an open-maximum range such as `'10+'`.  
        Each value can be a boolean or array:
          - [ ] If `true`, a kappagen will occur.
          - [ ] If `false`, no kappagen will occur.
          - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

    * `poll`  
      *Settings related to polls.*

      * `begin`  
        *A poll begins in your channel.*  
        This value can be a boolean or array:
        - [ ] If `true`, a kappagen will occur.
        - [ ] If `false`, no kappagen will occur.
        - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

      * `end`  
        *A poll ends in your channel.*  
        This value can be a boolean or array:
        - [ ] If `true`, a kappagen will occur.
        - [ ] If `false`, no kappagen will occur.
        - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

    * `timeout`  
      *Minimum time for a kappagen when a user is timed out.*  
      This value can be a boolean, integer, or array:
      - [ ] If `true`, a kappagen will occur on all timeouts.
      - [ ] If `false`, no kappagen will occur on timeouts.
      - [ ] If Integer, the value is the minimum seconds required for a timeout to trigger a kappagen.
        - [ ] If `0`, no kappagen will occur on timeouts.
      - [ ]  If Array, each key of the array should be a string containing a range of integers, such as `'1'`, `'5-30'` or `'60-180'`, or an open-maximum range such as `'300+'`.  
      Each value can be a boolean or array:
        - [ ] If `true`, a kappagen will occur.
        - [ ] If `false`, no kappagen will occur.
        - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

    * `ban`  
      *A user is banned in the channel.*  
      This value can be a boolean or array:
      - [ ] If `true`, a kappagen will occur.
      - [ ] If `false`, no kappagen will occur.
      - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

  * `tip`  
    *Settings related to third-party tip systems.*

    * `useProfileImage`  
      - [ ] If `true`, tips will use the tipper's profile image instead of emotes.
      - [ ] If `false`, tips will use your standard kappagen emotes.

    * `streamlabs`  
      *Settings related to Streamlabs payment events.*
      > **NOTE**: The values used in these ranges can be controlled with the `"cfg.streamlabs.curMul"` setting (see above) based on your default currency in Streamlabs.  

      * `donation`  
        *Minimum tip amount through Streamlabs for a kappagen.*  
        This value can be a boolean, integer, or array:
        - [ ] If `true`, a kappagen will occur on all Streamlabs tips.
        - [ ] If `false`, no kappagen will occur on tips.
        - [ ] If Integer, the value is the minimum amount required for a tip to trigger a kappagen.
          - [ ] If `0`, no kappagen will occur on tips through Streamlabs.
        - [ ] If Array, each key of the array should be a string containing a range of integers, such as `'1'`, `'2-4'` or `'5-19'`, or an open-maximum range such as `'20+'`.  
          Each value can be a boolean or array:
          - [ ] If `true`, a kappagen will occur.
          - [ ]  If `false`, no kappagen will occur.
          - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

      * `pledge`  
        *Minimum pledge amount through Streamlabs for a kappagen.*  
        This value can be a boolean, integer, or array:
        - [ ] If `true`, a kappagen will occur on all Streamlabs pledges.
        - [ ] If `false`, no kappagen will occur on pledges.
        - [ ] If Integer, the value is the minimum amount required for a tip to trigger a kappagen.
          - [ ] If 0, no kappagen will occur on pledges through Streamlabs.
        - [ ] If Array, each key of the array should be a string containing a range of integers, such as `'1'`, `'2-4'` or `'5-19'`, or an open-maximum range such as `'20+'`.  
        Each value can be a boolean or array:
          - [ ] If `true`, a kappagen will occur.
          - [ ] If `false`, no kappagen will occur.
          - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

    * `streamelements`  
      *Minimum tip amount through StreamElements for a kappagen.*  

      > **NOTE**: The values used in these ranges can be controlled with the `"cfg.streamelements.curMul"` setting (see above) based on your default currency in StreamElements.  

      This value can be a boolean, integer, or array:
      - [ ] If `true`, a kappagen will occur on all StreamElements tips.
      - [ ] If `false`, no kappagen will occur on tips.
      - [ ] If Integer, the value is the minimum amount required for a tip to trigger a kappagen.
          - [ ] If `0`, no kappagen will occur on tips through StreamElements.
       - [ ] If Array, each key of the array should be a string containing a range of integers, such as `'1'`, `'2-4'` or `'5-19'`, or an open-maximum range such as `'20+'`.  
        Each value can be a boolean or array:
          - [ ] If `true`, a kappagen will occur.
          - [ ] If `false`, no kappagen will occur.
          - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

* `commands`  
  *An array of commands which can trigger one or more kappagens, or clear the screen.*  
  Each command is an object with the following properties:

  * `aliases`  
    *An array of kappa command aliases which can be used to force-trigger this kappagen.*

  * `access`  
    *A bitwise flag representing which users can trigger this kappagen with a command.*  
    This value will fall back to the general kappagen access value.

  * `cooldown`  
    *The number of seconds between force-triggered kappagens using an above alias.*  
    Any commands sent before the cooldown will be ignored, unless another command shares the same alias.  
    This value is optional; no value is the same as a value of `0`, which is, no cooldown.

  * `redeem`  
    *An array of style-specific channel point reward names which can be used to force-trigger this kappagen.*  
    Requires `moderator:read:shoutouts` scope.

  * `erase`  
    *If this property exists, the command will erase the screen rather than showing a kappagen.*  
    Any `styles`, `rave`, `raveon`, or `raveoff` properties will be ignored, regardless of the value of `erase`.

  * `rave`  
    *If this property exists, the command will toggle the `'rave'` hue rotation, if enabled, rather than showing a kappagen.*  
    Any `styles`, `raveon`, or `raveoff` properties will be ignored, regardless of the value of `rave`.  
    If `"cfg.display.hue"` is not set to `'rave'`, this command will do nothing.

  * `raveon`  
    *If this property exists, the command will turn on the `'rave'` hue rotation, if enabled, rather than showing a kappagen.*  
    Any `styles` or `raveoff` properties will be ignored, regardless of the value of `raveon`.  
    If `"cfg.display.hue"` is not set to `'rave'`, this command will do nothing.

  * `raveoff`  
    *If this property exists, the command will turn off the `'rave'` hue rotation, if enabled, rather than showing a kappagen.*  
    Any `styles` property will be ignored, regardless of the value of `raveoff`.  
    If `"cfg.display.hue"` is not set to `'rave'`, this command will do nothing.

  * `styles`  
    *A kappagen of one of the listed styles will occur upon command.*  
    This value can be a boolean or array:
    - [ ] If `true`, a kappagen will occur.
    - [ ] If `false`, no kappagen will occur.
    - [ ] If an array of kappa styles, a kappagen of one of the listed styles will occur.

* `ignore`  
  *Ignore Lists*

  * `users`  
    *Users who should be ignored.*  
    This value can be `false` or an array:
    - [ ] If `false`, no users will be ignored.
    - [ ] If an array of strings, these user names will not be able to make emotes show up.

  * `emotes`  
    *Emotes which should be ignored.*  
    This value can be `false` or an array:
    - [ ] If `false`, no emotes will be ignored.
    - [ ] If an array of strings, these emotes will not show up.  
       - You can also use `\u{XXXXX}` escape'd emojis.
    > **NOTE**: Kick emote names are user-editable, and don't even show up when posted by mobile app. This feature will not work correctly in such cases.


---


Note on Event and Command Kappagen Entries
------------------------------------------

Keep in mind that kappagen arrays are also associative, and may have independent settings for kappas such as
TheCube and Text. The kappagen style can also contain the following values:  

 * `count`  
   *The number of emotes to show for this kappagen.*  
   This can be an integer or an object.  
   - [ ] If this property does not exist, it will fall back to the count setting for the kappagen style.
     - [ ] If the kappagen style has no count property, then the global kappagen count will be used.
   - [ ] If Integer, this is the number of emotes that will be shown in this kappagen.
   - [ ] If Object:
     * `default`  
       *The number of emotes to show for this kappagen by default.*  
       This must be an integer.
       - [ ] If this property does not exist, it will fall back as the parent count would.
       - [ ] If Integer, this is the number of emotes that will be shown in this kappagen.

     * `dynamic`  
       *This is a boolean value to determine if the count can be changed by users.*  
       - [ ] If this property does not exist, it will fall back to `false`.
       - [ ] If `true`, a user may include a number in the command's parameters, and that number will be used.
       - [ ] If `false`, the default count will be used exclusively.

     * `maximum`  
       *The maximum number of emotes to show for this kappagen if dynamic is set to `true.*  
       This must be an integer.
       - [ ] If this property does not exist, it will fall back to the maximum number of emotes allowed on screen.
       - [ ] If Integer, this is the maximum number of emotes this kappagen style can display.

* `emotes`  
  *A list of emotes that will be used for this kappagen.*  
  This can be an array or an object.
  - [ ] If Array, each entry must be a string containing the name or URL of an emote, or an emoji.
    > **NOTE**: Only your channel or global emotes can be named (including 3rd-party).
  - [ ] If object:
    * `list`  
      This must be an array of strings, the same as the Array entry of the parent `emotes` property above.

    * `dynamic`  
      *This is a boolean value to determine if the displayed emotes can be set by the user.*
      - [ ] If this property does not exist, it will fall back to `true`.
      - [ ] If `true`, a user may include emotes in the command's parameters, and those emotes will be used.
      - [ ] If `false`, only the emotes in the list property above will be used.
