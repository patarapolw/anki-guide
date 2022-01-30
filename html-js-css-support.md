# HTML/JS/CSS - what are supported

- Supported
  - Web Components
  - JQuery
  - wanakana.js
  - CSS `@import`

Some other Anki issues include

- Creating or editing Note Types requires full sync.
- [Synchronization and file size](/sync-size).

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
