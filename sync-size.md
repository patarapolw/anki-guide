# Synchronization and file size

Syncing can be problematic if you include a lot of media; however, relieving to external sources is possible, although not simply Dropbox or Google Drive. Not to mention creating or editing Note Types requires full sync, and you probably want to add additional fields sometimes, anyway.

It may be possible with AWS S3, Google Cloud Storage or Cloudinary, if you set appropriate permission. Otherwise, hosting a website is another option.

Syncing is probably very helpful if you use Anki on mobile, due to [some mobile issues](/ankidroid-vs-anki-issues-and-pros).

## Audio how to

You need HTML for this.

```html
<audio controls="">
    <source src="{{Audio URL}}" type="audio/mpeg">
</audio>
```

I can't manage to make autoplay work, whether via `<audio autoplay>`, `DOMContentLoaded`, `MutationObserver` or even `setTimeout`.

Of course, since it is just URL, you can make a server serving dynamic content, like Text-To-Speech (TTS).

## Image how to

Similar to audio, you need HTML.

```html
<img src="{{Image URL}}">
```

## Font how to

In CSS styling.

```css
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+JP&display=swap');

.card {
 font-family: 'Noto Sans JP';
}
```

However, I can't really enable font files served the other way, so this doesn't work.

```css
@font-face {
  font-family: KanjiStrokeOrders;
  font-display: swap;
  src: url('<<URL to KanjiStrokeOrders font>>.ttf', 'truetype');
}

.stroke-order {
  font-family: KanjiStrokeOrders;
}
```
