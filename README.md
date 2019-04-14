install the pulseaudio package:

`apt-get install pulseaudio`

Copy the appropriate files in this repository to appropriate
locations. You will need to modify the callsign in /etc/direwolf.conf

Set pulseaudio to start on boot:

`systemctl enable pulseaudio`

FLDigi should use pulseaudio directly.  The "Server String" is
`unix:/var/run/pulse/native` and the audio will show up on the
left connector.

Direwolf and any other programs should use the following ALSA
audio devices:
  * draws-capture-right
  * draws-playback-right

This will cause them to use the right connector. Pins and levels
should still be set appropriately using alsamixer and friends.

You may need to do the following:

`chmod 000 /usr/bin/start-pulseaudio-x11`

If the onboard audio interface has been enabled by `config.txt` this setup
will attempt to use it as a monitor channel.  It will send the audio from the
left and right DRAWS ports to the respective channels on the onboard
interface.  This allows those with radios that mute when the DIN connector
is in use to monitor the channels.  It *may* also be possible to route over
a bluetooth audio connection, but developer does not currently have the
equipment to test such a proposition.  You may need to execute the following:

For HDMI audio in an HDMI monitor/TV: `amixer -D hw:CARD=ALSA cset numid=3 2`
For the headphone jack on the Pi: `amixer -D hw:CARD=ALSA cset numid=3 1`

Tests have not been extensive, but things do seem to work
reliably so far.  Receive has been more extensively tested than
transmit.

It is not recommended to mess around with the sound too much in the GUI while
in this configuration.
