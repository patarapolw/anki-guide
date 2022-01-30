# Japanese rendering issues

Some Kanji characters do not render properly without some settings due [Han unification](https://en.wikipedia.org/wiki/Han_unification). I believe this is also region specifics, which affect the default settings.

This can be fixed on the card via some Japanese font.

```css
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+JP&display=swap');

.card {
 font-family: 'Noto Sans JP';
}
```
