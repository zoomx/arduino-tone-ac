# toneAC Arduino Library #

## Replacement to the standard tone library with many advantages ##

  * Nearly twice the volume (because it uses two out of phase pins in push/pull fashion)
  * Higher quality (less clicking)
  * Capability of producing higher frequencies (even if running at a lower clock speed)
  * Nearly 1.5k smaller compiled code
  * Bug fixes (standard tone library can generate some odd and unpredictable results)
  * Can set not only the frequency but also the sound volume
  * Less stress on the speaker so it will last longer and sound better

Disadvantages are that it must use certain pins and it uses two pins instead of one. But, if you're flexible with your pin choices, this is a great upgrade. It also uses timer 1 instead of timer 2, which may free up a conflict you have with the tone library. It exclusively uses port registers for the fastest and smallest code possible.


## [Download toneAC v1.2](http://code.google.com/p/arduino-tone-ac/downloads/list) ##

## Show Your Appreciation: ##
Help future development by making a small donation (yes, the FreeRingers payee is correct).<br>
<a href='https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=69G9RA436Q734'><img src='https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif' /></a>
<br>
<b>Supporters:</b>
<br>Louis B. $20 4/30<br>
<br>Regalia S. $5<br>
<br>Shawn C. $30<br>
<br>
<h3>What's toneAC2?</h3>
First off, toneAC is SUPERIOR to toneAC2.  It's called toneAC2 only because it uses timer 2, not because it's a newer version of toneAC.  toneAC2 is an alternate but INFERIOR version of toneAC that uses timer 2 instead of timer 1 and allows for any two pins to be used.  You should use toneAC instead of toneAC2 if at all possible because toneAC more accurate, higher quality, allows for higher frequencies, uses fewer CPU cycles, and creates smaller code.  However, if you're having a conflict with timer 1, or just can't use the default PWM pins for timer 1, then toneAC2 may be your answer. <a href='http://code.google.com/p/arduino-tone-ac/downloads/list'>Download toneAC2 v1.0</a>


<h2>Connection</h2>
Connection is very similar to a piezo or standard speaker.  Except, instead of connecting one speaker wire to ground you connect both speaker wires to Arduino pins.  The pins you connect to are specific, as toneAC lets the ATmega microcontroller do all the pin timing and switching.  This is important due to the high switching speed possible with toneAC and to make sure the pins are alyways perfectly out of phase with each other (push/pull).  See the below list for which pins to use for different Arduinos.  Just as usual when connecting a speaker, make sure you add an inline 100 ohm resistor between one of the pins and the speaker wire.<br>
<br>
<b>Pins 9 & 10</b> - ATmega328, ATmega128, ATmega640, ATmega8, Uno, Leonardo, etc.<br>
<b>Pins 11 & 12</b> - ATmega2560/2561, ATmega1280/1281, Mega<br>
<b>Ping 12 & 13</b> - ATmega1284P, ATmega644<br>
<b>Pins 14 & 15</b> - Teensy 2.0<br>
<b>Pins 25 & 26</b> - Teensy++ 2.0<br>

<img src='http://www.leethost.com/link_pics/toneAC3.png' />


<h2>Example sketch</h2>
<pre><code>#include &lt;toneAC.h&gt;<br>
<br>
void setup() {} // Nothing to setup, just start playing!<br>
<br>
void loop() {<br>
  for (unsigned long freq = 150; freq &lt;= 15000; freq += 10) {  <br>
    toneAC(freq); // Play the frequency (150 Hz to 15 kHz in 10 Hz steps).<br>
    delay(1);     // Wait 1 ms so you can hear it.<br>
  }<br>
  toneAC(0); // Turn off toneAC, can also use noToneAC().<br>
<br>
  while(1); // Stop (so it doesn't repeat forever driving you crazy--you're welcome).<br>
}<br>
</code></pre>


<h2>Syntax</h2>
<ul><li><b>toneAC( frequency [, volume [, length [, background ]]] )</b> - Play a note.<br>
<ul><li><b>frequency</b> - Play the specified frequency indefinitely, turn off with toneAC().<br>
</li><li><b>volume</b> - <code>[</code>optional<code>]</code> Set a volume level. (default: 10, range: 0 to 10 <code>[</code>0 = off<code>]</code>)<br>
</li><li><b>length</b> - <code>[</code>optional<code>]</code> Set the length to play in milliseconds. (default: 0 <code>[</code>forever<code>]</code>, range: 0 to 2^32-1)<br>
</li><li><b>background</b> - <code>[</code>optional<code>]</code> Play note in background or pause till finished? (default: false, values: true/false)<br>
</li></ul></li><li><b>toneAC()</b> - Stop output.<br>
</li><li><b>noToneAC()</b> - Same as toneAC().</li></ul>


<h2>How does it work?</h2>
The library is named toneAC because it produces an alternating push/pull between two pins.  It's not really AC (alternating current) as in-wall electrical wiring because it's a square wave and never produces a negative voltage. However, the effect of the alternating push/pull creates an effective double voltage differential which produces the higher volume level.<br>
<br>
The ATmega's PWM takes care of the alternating push/pull so the accuracy is exact.  When you send a tone to a speaker with the standard tone library, the loudest is at 50% duty cycle (only on half the time).  Which at 5 volts, is like sending only 2.5v to the speaker.  With toneAC, we're sending out of phase signals on two pins.  So in effect, the speaker is getting 5 volts instead of 2.5, making it nearly twice as loud.<br>
<br>
The sound quality difference has to do with allowing the Arduino's PWM to take care of everything and careful programming.  Longer piezo life happens because instead of driving the transducer disc only ever in one direction (deforming the disc and reducing sound and quality), it drives it in both directions keeping the disc uniform.<br>
<br>
<br>
<h2>Cool User Projects Using toneAC</h2>
<table><thead><th> <a href='http://www.youtube.com/watch?feature=player_embedded&v=RRxPJvIBGxM' target='_blank'><img src='http://img.youtube.com/vi/RRxPJvIBGxM/0.jpg' width='425' height=344 /></a> </th><th> <a href='http://www.youtube.com/watch?feature=player_embedded&v=8FrwLX6i0J0' target='_blank'><img src='http://img.youtube.com/vi/8FrwLX6i0J0/0.jpg' width='425' height=344 /></a> </th></thead><tbody>
<tr><td> <a href='http://arduino-info.wikispaces.com/Project-HandBat'><img src='http://www.leethost.com/link_pics/toneAC-handbat.jpg' /></a>                                               </td></tr></tbody></table>


<h2>toneAC History</h2>
<b>01/27/2013 v1.2</b> - Fixed a counter error which went "over the top" and caused periods of silence (thanks Krodal). For advanced users needing tight code, the TONEAC_TINY switch in toneAC.h activates a version of toneAC() that saves 110 bytes. With TONEAC_TINY, the syntax is toneAC(frequency, length) while playing the note at full volume forever in the background. Added support for the ATmega 640, 644, 1281, 1284P and 2561 microcontrollers.<br>
<br>
<b>01/16/2013 v1.1</b> - Option to play notes in background, returning control back to your sketch for processing while note plays (similar to the way the tone library works). Volume is now linear and in the range from 0-10. Now uses prescaler 256 instead of 64 for frequencies below 123 Hz so it can go down to 1 Hz no matter what speed the CPU is clocked at (helpful if using toneAC to control a two-pin dual LED).<br>
<br>
<b>01/11/2013 v1.0</b> - Initial release.<br>
<br>
<br>
<h2>toneAC2 History</h2>
<b>01/27/2013 v1.0</b> - Initial release.