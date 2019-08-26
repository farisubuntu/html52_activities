
## Web Video Text Track (WebVTT) quick review:
  
- The W3C Web Media Text Tracks community Group [https://www.w3.org/community/texttracks/] **working** on the "WebVTT: The Web video Text Tracks Format [http://dev.w3.org/htmnl5/webvtt/] **specification (a format used for defining files that will contain text for captions and subtitles,...etc.**
- The WebVTT files are used with the src attribute of the `<track>` elemenmt, tyhat can be used inside a `<video>`...`</video>` .
- The MIME type of WebVTT is **text/vtt**.
- A WebVTT file (.vtt) contains cues, which can be either a single line or multiple lines, as shown below: 
  
  *  Example of vtt file:
   ```
    WEBVTT
    00:01.000 --> 00:04.000
    Never drink liquid nitrogen.

    00:05.000 --> 00:09.000
    - It will perforate your stomach.
    - You could die.
  

- You can style WebVTT cues by looking for elements which match the ::cue pseudo-element.

```css
video::cue {
  background-image: linear-gradient(to bottom,
   dimgray, lightgray);
  color: papayawhip;
}

video::cue(b) {
  color: peachpuff;
}
```

- You can also define your style inside the WebVTT file directly by inserting CSS rules into the file with each rule preceded by the string "STYLE" all by itself on a lilne of text:
```html
WEBVTT

STYLE
::cue {
  background-image: linear-gradient(to bottom, dimgray, lightgray);
  color: papayawhip;
}
/* Style blocks cannot use blank lines nor "dash dash 
greater than" */

NOTE comment blocks can be used between style blocks.

STYLE
::cue(b) {
  color: peachpuff;
}

00:00:00.000 --> 00:00:10.000
- Hello <b>world</b>.

NOTE style blocks cannot appear after 
the first cue.
```

- **A cue** is a single subtitle block that has a single start time, end time, and textual payload. Example 6 consists of the header, a blank line, and then five cues separated by blank lines. A cue consists of five components:

An optional cue identifier followed by a newline.
Cue timings.
Optional cue settings with at least one space before the first and between each setting.
One or more newlines.
The cue payload text.

> Example 7 - Example of a cue

```html
1 - Title Crawl
00:00:05.000 --> 00:00:10.000 line:0 position:20%
     size:60% align:start

Some time ago in a place rather distant....
```

> #### Continue => https://developer.mozilla.org/en-US/docs/Web/API/WebVTT_API

> for comperhensive ref: https://www.w3.org/TR/webvtt1/#webvtt-file

>   also: **https://codepen.io/farisubuntu/pen/pozNwrL**

---

### HTML5 media - review:
- Consider this HTML file:
```html

  <!DOCTYPE HTML>
<html>
  <body>
    <video controls autoplay>
      <source src="your_video.mp4" type="video/mp4"/>
      <track default kind="captions" srclang="en" 
      label="English" src="your_caption_file.vtt"/>
    </video>
  </body>
</html>
```
The `<track>` tag is sort of like a script that "plays" along with the video. We can use multiple tracks in the same video element. The `default` attribute indicates that a the track will be enabled automatically.

Let's run down all the `<track>` attributes while we're at it:

-   `srclang` indicates what language the track is in.
-   `kind` represents the type of track it is and there are five kinds:
    -   `subtitles` are usually translations and descriptions of different parts of a video.
    -   `descriptions` help unsighted users understand what is happening in a video.
    -   `captions` provide un-hearing users an alternative to audio.
    -   `metadata` is a track that is used by scripts and cannot be seen by users.
    -   `chapters` assist in navigating video content.
>   Note: if 'kind' not present/omitted then equal='subtitles' and if if its value is Invalid then equal 'metadata'.
> 
-   `label` is a title for the text track that appears in the caption track
-   `src` is the source file for the track. It cannot come from a cross-origin source unless `crossorigin` is specified.

While WebVTT is designed specifically for video, you can still use it with audio by placing an audio file within a `<video>` element.

- The track element CAN NOT be used with a <em>file://URL</em>; instead use http:// and a web server.
- Your server must use a special MIME format for the .vtrt files: **text/vtt;charset=utf-8**
> continue 
    **[css-tricks/imporoving-video-accessibility-with-webvtt/]**

### Tools: 

- linux: 
  - gnome-subtitles
  - ________
  - handbrake
  - super
-js library for converting to the WebVTT  format on the fly:
 <a>JS_videosub [http://www.storiesinflight.com/js_videosub/]

