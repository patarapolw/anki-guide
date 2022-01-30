# HTML/JS/CSS - what are supported

- Supported
  - [Web Components](#web-components)
  - JQuery
  - wanakana.js
  - CSS `@import`
- Issues
  - Templating using Note data
  - [Synchronization and file size](/sync-size.md) with templating tips
  - Creating or editing Note Types requires full sync.

Of course, there is [an official guide here](https://docs.ankiweb.net/templates/styling.html).

## Templating

Templating is done with a mustache-like syntax. However, it doesn't support HTML cleaning. Therefore, this may break.

```html
<p><a href="http://jisho.org/search/{{japanese}}">Open in Jisho</a></p>
```

You might not realize it, but Note fields in Anki are always filled with HTML, but hidden by default. Therefore, some of it may be covered by `<p>` tag, or there may be `<b>` tag inside it.

Therefore, a real correct way for this (in EJS syntax) is

```html
<p><a href="http://jisho.org/search/<%= encodeURIComponent(cleanHTMLTags(japanese)) %>">Open in Jisho</a></p>
```

You might need to write a function to clean HTML tags, however.

```html
<script>
  function cleanHTMLTags(s) {
    const div = document.createElement('div')
    div.innerHTML = s
    return div.innerText
  }
</script>
```

I also realized that such safety can also be done on JavaScript side, however does not obliviate the need of proper templating engine.

```html
<p><a class="a-jisho">Open in Jisho</a></p>

<script>
  function cleanHTMLTags(s) {
    const div = document.createElement('div')
    div.innerHTML = s
    return div.innerText
  }

  document.querySelector('a.a-jisho').href = "http://jisho.org/search/" + encodeURIComponent(cleanHTMLTags("<%= japanese %>"))
</script>
```

## Collapsible `<br>`

A correct answer is to use `<p>` or `<div>` instead. It will automatically collapse, if there is no visible content.

## Web Components

```html
<script>
class TTSElement extends HTMLElement {
  constructor() {
    super()

    this.attachShadow({ mode: 'open' })

    const wrapper = document.createElement('span')
    wrapper.innerText = '▶️'
    wrapper.style.cursor = 'pointer'

    const q = this.textContent
    const apiKey = ''
    const origin = 'https://jaquiz-api.herokuapp.com/'
    if (q) {
      const elAudio = document.createElement('audio')
      elAudio.style.display = 'none'

      const setSrc = (...sources) => {
        elAudio.textContent = ''
				const u = new URL(origin)

        sources.map((s) => {
          const elSource = document.createElement('source')
          const u = new URL(s.url, origin)
          elSource.src = u.href
          elSource.type = s.type || 'audio/mpeg'

          elAudio.append(elSource)
        })
      }

      setSrc({
        url: `/api/tts/tts.mp3?q=${encodeURIComponent(q)}`,
      })

      this.addEventListener('click', () => {
        elAudio.play()
      })

      wrapper.append(elAudio)

      const u = new URL('/api/wk/audio', origin)
      u.searchParams.set('q', q)

      if (apiKey) {
        fetch(u.href, {
          headers: {
            Authorization: `Bearer ${apiKey}`,
          },
        })
          .then((r) => r.json())
          .then(({ audios }) => {
            setSrc(...audios)
          })
      }
    }

    this.shadowRoot.append(wrapper)
  }
}

try {
	customElements.define('el-tts', TTSElement)
} catch (e) {}
</script>
```
