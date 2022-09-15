---
teaser:
  text: Replaces the HTML5 video tag, has Own controller
---

# spz-video

## Usage

A replacement for the HTML5 `video` tag; only to be used for direct HTML5 video file embeds.

The `spz-video` component loads the video resource specified by its `src` attribute lazily, at a time determined by the runtime. You can control an `spz-video` component much the same way as a standard HTML5 `<video>` tag.

The `spz-video` component accepts up to four unique types of HTML nodes as children:

-   `source` tags: Just like in the HTML `<video>` tag, you can add `<source>` tag children to specify different source media files to play.
-   `track` tags to enable subtitles in the video. If the track is hosted on a different origin than the document, you must add the `crossorigin` attribute to the `<spz-video>` tag. Whenever the video has narration or important audio information, make sure to include subtitles/captions for users who may not be able to hear it or have their sound turned off.
-   a placeholder for before the video starts
-   a fallback if the browser doesn’t support HTML5 video: One or zero immediate child nodes can have the `fallback` attribute. If present, this node and its children form the content that displays if HTML5 video is not supported on the user’s browser.

[exspzle preview="inline" playground="true" imports="spz-video"]

```html
<spz-video {% if format=='stories'%}autoplay {% endif %}controls
  width="640"
  height="360"
  layout="responsive"
  poster="{{server_for_email}}/static/inline-exspzles/images/kitten-playing.png">
  <source src="{{server_for_email}}/static/inline-exspzles/videos/kitten-playing.webm"
    type="video/webm" />
  <source src="{{server_for_email}}/static/inline-exspzles/videos/kitten-playing.mp4"
    type="video/mp4" />
  <div fallback>
    <p>This browser does not support the video element.</p>
  </div>
</spz-video>
```

[/exspzle]

## Attributes

### src

Required if no `<source>` children are present. Must be HTTPS.

### poster

The image for the frame to be displayed before video playback has started. By
default, the first frame is displayed.

Alternatively, you can present a click-to-play overlay.

### autoplay

[filter formats="stories"]

Required for videos inside stories.

[/filter]<!-- formats="stories" -->

If this attribute is present, and the browser supports autoplay, the video will be automatically
played as soon as it becomes visible. There are some conditions that the component needs to meet
to be played, [which are outlined in the Video in spz spec](../../../docs/spec/spz-video-interface.md#autoplay).

### controls

This attribute is similar to the `controls` attribute in the HTML5 `video`. If this attribute is present, the browser offers controls to allow the user to control video playback.

### controlsList

Same as [controlsList](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement/controlsList) attribute of HTML5 video element. Only supported by certain browsers.

### loop

If present, the video will automatically loop back to the start upon reaching the end.

### muted (deprecated)

The `muted` attribute is deprecated and no longer has any effect. The `autoplay` attribute automatically controls the mute behavior.


```html
<spz-video
  width="720"
  height="305"
  layout="responsive"
  src="https://yourhost.com/videos/myvideo.mp4"
  poster="https://yourhost.com/posters/poster.png"
  artwork="https://yourhost.com/artworks/artwork.png"
  title="Awesome video"
  artist="Awesome artist"
  album="Amazing album"
>
</spz-video>
```

#### artwork

Specifies a URL to a PNG/JPG/ICO image serving as the video's artwork. If `artwork` is not present, the Media Session API helper uses either the `image` field in the `schema.org` definition, the `og:image`, or the website's `favicon`.

#### artist

Indicates the author of the video file, specified as a string.

#### album

Indicates the album/collection the video was taken from, specified as a string.

#### title

Indicates the name/title of the video, specified as a string. If not provided, the Media Session API helper uses either the `aria-label` attribute or falls back to the page's title.

[filter formats="stories"]

## Actions

### seekTo (currentTime = xxxx)

video percent move to currentTime

### play

play video

### pause

pause video
## Events

### ended

when video play ended
### exitFull

click exit-full

### enterFull

click enter-full

### play

click play btn

### pause

click pause bth
