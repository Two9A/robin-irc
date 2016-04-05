# A rudimentary Robin/IRC bridge

## What do you mean, a "bridge"?

This allows you to connect to Robin from an IRC client, using the username and password you provide in your IRC client configuration. The bridge acts as a locally-running IRC server, and will pass messages back and forth.

## Installation

(This has only been tested on Linux, but should work anywhere PHP does.)

* Dump the contents of this repository somewhere.
* Edit `robin-irc.php` to change your preferences as to filtering and chat colors.
* `php robin-irc.php`

Then configure your preferred IRC client. A sample configuration for irssi follows.

    servers = (
      {
        address = "localhost";
        chatnet = "Robin";
        port = "8194";
        password = "PASSWORD";
        username = "USERNAME";
      }
    );
    chatnets = {
      Robin = {
        type = "IRC";
        nick = "USERNAME";
        autosendcmd = "/^wait 15000";
      };
    };
    channels = (
      { name = "#general"; chatnet = "Robin"; autojoin = "Yes"; },
      { name = "#chat"; chatnet = "Robin"; autojoin = "Yes"; },
      { name = "#trivia"; chatnet = "Robin"; autojoin = "Yes"; },
      { name = "#dev"; chatnet = "Robin"; autojoin = "Yes"; },
      { name = "#rpg"; chatnet = "Robin"; autojoin = "Yes"; },
      { name = "#penis"; chatnet = "Robin"; autojoin = "Yes"; }
    );

Finally, use a web browser to get into a Robin chat (the bridge doesn't have the ability to click on the Participate button).

## Configuration

The included `robin-irc.ini` file comes pre-configured with a few channels and body filters. Once the server is started, the configuration file is read every 5 minutes; thus, filters and channels can be changed without your IRC client dropping connection.

The same refresh interval applies for automatic votes: if the `general.autovote` configuration setting is changed to one of `INCREASE`, `CONTINUE` or `ABANDON`, the new vote will be broadcast within five minutes.

## Caveats

Oh, where do I start?

* You can't see people's votes, and the nick list isn't transferred to the IRC client;
* You can't submit votes yourself, abandon, or leave;
* I have no idea what happens when the chat increases/merges;
* Nothing is done with the join/part messages imparted by Robin;
* The bridge doesn't inform the IRC client when it disconnects/quits...

I could go on, but that's a good starter for ten.
