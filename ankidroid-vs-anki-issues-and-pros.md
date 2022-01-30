# AnkiDroid vs Anki (desktop) issues and pros

Indeed, AnkiDroid isn't even created nor maintained by the Anki creator, so it is subjected to various issues. Although I haven't met any rendering issues so far, there are other issues.

## Issues

### Cannot edit card template

I just cannot find a button to do this.

### Card browser not just as simple and useful

Well, the layout is different, and it has to adapt to mobile too (i.e. responsive design).

### Editing the note on AnkiDroid breaks multi-line HTML

- `<br>` is auto-injected between new lines. This includes supposedly HTML as well.
- Pasting rich text eventually gets formatting removed. It superficially works, until you save and preview. (Unless you use HTML tags.)

### Japanese glyph support

Apparently, even if user interface is set to 日本語 (Japanese), [it still cannot render some Kanji properly](/japanese-issues).

## Pros / Features

### AnkiDroid specific links

I noticed that this is made by [Takoboto app](https://play.google.com/store/apps/details?id=jp.takoboto).

```html
intent:#Intent;package=jp.takoboto;action=jp.takoboto.WORD;i.word=1252490;S.browser_fallback_url=http%3A%2F%2Ftakoboto.jp%2F%3Fw%3D1252490;end
```

### Whiteboard

This can be done by finding "Enable whiteboard" from the top-right menu. It works regardless of having S pen or not.

### Long vertical display

This is obvious if you are using a tablet.
