S# Info for week1 1.2: The timed/text track api:

## Objectivies:

how to  build a menu for choosing the subtitle track language to display,
how to display a synchronized description of a video (useful for disabled people, for example),
how to display a clickable transcript aside the video (similar to what the edX video player does),
how to show chapters,
how to use JSON encoded cue contents (useful for showing external resources in the HTML document while a video is playing),
etc.


## from specification: 

4.7.14.11. Timed text tracks

4.7.14.11.1. Text track model

A media element can have a group of associated text tracks, known as the media element’s list of text tracks. The text tracks are sorted as follows:
S
The text tracks corresponding to track element children of the media element, in tree order.
Any text tracks added using the addTextTrack() method, in the order they were added, oldest first.
Any media-resource-specific text tracks (text tracks corresponding to data in the media resource), in the order defined by the media resource’s format specification.
A text track consists of:

The kind of text track
This decides how the track is handled by the user agent. The kind is represented by a string. The possible strings are:

subtitles
captions
descriptions
chapters
metadata
The kind of track can change dynamically, in the case of a text track corresponding to a track element.

A label
This is a human-readable string intended to identify the track for the user.

The label of a track can change dynamically, in the case of a text track corresponding to a track element.

When a text track label is the empty string, the user agent should automatically generate an appropriate label from the text track’s other properties (e.g., the kind of text track and the text track’s language) for use in its user interface. This automatically-generated label is not exposed in the API.

An in-band metadata track dispatch type
This is a string extracted from the media resource specifically for in-band metadata tracks to enable such tracks to be dispatched to different scripts in the document.

For example, a traditional TV station broadcast streamed on the Web and augmented with Web-specific interactive features could include text tracks with metadata for ad targeting, trivia game data during game shows, player states during sports games, recipe information during food programs, and so forth. As each program starts and ends, new tracks might be added or removed from the stream, and as each one is added, the user agent could bind them to dedicated script modules using the value of this attribute.

Other than for in-band metadata text tracks, the in-band metadata track dispatch type is the empty string. How this value is populated for different media formats is described in steps to expose a media-resource-specific text track.

A language
This is a string (a BCP 47 language tag) representing the language of the text track’s cues. [BCP47]

The language of a text track can change dynamically, in the case of a text track corresponding to a track element.

A readiness state
One of the following:

Not loaded
Indicates that the text track’s cues have not been obtained.

Loading
Indicates that the text track is loading and there have been no fatal errors encountered so far. Further cues might still be added to the track by the parser.

Loaded
Indicates that the text track has been loaded with no fatal errors.

Failed to load
Indicates that the text track was enabled, but when the user agent attempted to obtain it, this failed in some way (e.g., URL could not be resolved, network error, unknown text track format). Some or all of the cues are likely missing and will not be obtained.

The readiness state of a text track changes dynamically as the track is obtained.

A mode
One of the following:

Disabled
Indicates that the text track is not active. Other than for the purposes of exposing the track in the DOM, the user agent is ignoring the text track. No cues are active, no events are fired, and the user agent will not attempt to obtain the track’s cues.

Hidden
Indicates that the text track is active, but that the user agent is not actively displaying the cues. If no attempt has yet been made to obtain the track’s cues, the user agent will perform such an attempt momentarily. The user agent is maintaining a list of which cues are active, and events are being fired accordingly.

Showing
Indicates that the text track is active. If no attempt has yet been made to obtain the track’s cues, the user agent will perform such an attempt momentarily. The user agent is maintaining a list of which cues are active, and events are being fired accordingly. In addition, for text tracks whose kind is subtitles or captions, the cues are being overlaid on the video as appropriate; for text tracks whose kind is descriptions, the user agent is making the cues available to the user in a non-visual fashion; and for text tracks whose kind is chapters, the user agent is making available to the user a mechanism by which the user can navigate to any point in the media resource by selecting a cue.

A list of zero or more cues
A list of text track cues, along with rules for updating the text track rendering. For example, for WebVTT, the rules for updating the display of WebVTT text tracks. [WEBVTT]

The list of cues of a text track can change dynamically, either because the text track has not yet been loaded or is still loading, or due to DOM manipulation.

Each text track has a corresponding TextTrack object.

Each media element has a list of pending text tracks, which must initially be empty, a blocked-on-parser flag, which must initially be false, and a did-perform-automatic-track-selection flag, which must also initially be false.