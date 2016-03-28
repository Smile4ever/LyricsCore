LyricsCore
==========

LyricsCore is a lyrics API written in PHP. It fetches the lyrics text from many lyrics websites, as listed below. These lyrics can then be used in any application by sending a request to the (hosted) LyricsCore API.

Examples
========

The LyricsCore API can be used like this from the Linux command line:

	FORMAT=text FILENAME="Roxette - Dangerous" php index.php

This request outputs the lyrics text only, properly formatted. If you want something more, you can opt for the output format xml:

	FORMAT=xml FILENAME="Roxette - Dangerous" php index.php

outputs:

	<song>
		<artist>Roxette</artist>
		<title>Dangerous</title>
		<source>MetroLyrics</source>
		<url></url>
		<lyrics>
			<p>Here comes the lyrics text. This text still has the original HTML formatting.</p>
			<p>Of course there are many paragraphs</p>
		</lyrics>
	</song>

Hosted PHP API
==============

If you have uploaded index.php to lyricscore.eu5.org/api/v1/, you can use the API as follows: 
  
  http://lyricscore.eu5.org/api/v1/?filename=Roxette%20-%20Dangerous

It is advised you host the API yourself and you keep up to date with the changes made. That way you will have optimal coverage of as many songs as possible, and you won't be confronted by downtime on lyricscore.eu5.org.

I also strongly advise to have multiple hosted LyricsCore API's at your disposal, in case one goes down.

Parameters and values
=====================

Passing input values:
* artist (must be used together with title)
* title (must be used together with artist)
* filename (can be any filename)

Example filenames:
* "Roxette - Dangerous"
* "Roxette - Dangerous.mp4"
* "Roxette - Dangerous (1983)"
* "Roxette - Dangerous (1983).mp4"
* "Roxette - Dangerous (anything).anything"
* "Roxette-Dangerous.mp3"
* "Roxette-Dangerous"

Controlling the output:
* format ['', text, xml, json] (empty means html, use one of the three defined formats in your application)
* mode ['', 'debug'] (empty means normal operation, so the debug mode is disabled)

If you use the LyricsCore API without hosting it, you need to use CAPITAL LETTERS for the parameters. Otherwise, the parameter names are the same.

Usage in an external program
============================

It is advised that the application that uses this API reads the metadata from the music file and passes this to the API using the artist and title parameters. If metadata is not available, passing a file name will suffice.

A file name cannot contain the sign "&", but you can replace this by "and" before passing it to the LyricsCore API. There are no other known limitations.

Debug mode
==========

There is a debug mode built in. This debug mode shows any requests made by the LyricsCore API, in order to determine why a filename (artist+title) does not return a correct lyrics text. The debug mode can be enabled by setting the parameter "mode" to "debug". 

	http://lyricscore.eu5.org/api/v1/?filename=Patti%20Austin%20and%20James%20Ingram%20-%20Baby%20Come%20To%20Me&mode=debug

returns the output:

	DEBUG: Patti Austin and James Ingram
	DEBUG: MetroLyrics: artist_metro (patti-austin-and-james-ingram) contains and
	DEBUG: first artist: http://www.metrolyrics.com/baby-come-to-me-lyrics-patti-austin.html

	Here comes the lyrics text.

The debug mode can be useful to see what goes wrong and where.

Websites
========

These websites are supported:
- MetroLyrics
- LyricsMania
- Lyrics.com
- SonicHits
- AZLyrics
- LyricsMode
- MusixMatch
- Golyr.de
- Songteksten.net
