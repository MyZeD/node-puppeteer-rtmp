
# node-puppeteer-rtmp
Stream RTMP to Twitch or Google Live using puppeteer. Based on puppeteer-recorder. https://github.com/clipisode/puppeteer-recorder

Thank you to [clipisode](https://github.com/clipisode) <3

## Usage
```javascript
const puppeteer = require('puppeteer');
const { stream } = require('./lib/stream.js');

puppeteer.launch({
  headless: true,
  args: ["--no-sandbox", "--disable-setuid-sandbox"]
}).then(async browser => {
  const page = await browser.newPage();

  await page.goto('https://codepen.io/hexagoncircle/full/joqYEj', { waitUntil: 'networkidle2' });

  await stream({
    page: page,
    key: 'your_youtube_key',
    fps: 30,
    prepare: function (browser, page) { },
    render: function (browser, page, frame) { }
  });

  await browser.close();
});
```

## Options
- browser (default: puppeteer.launch())
- page (default: browser.newPage())
- ffmpeg (default: 'ffmpeg')
- fps (default: '30')
- resolution (default: '1280x720')
- preset (default: 'medium')
- rate (default: '2500k')
- threads (default: '2')
- output (default: 'rtmp://a.rtmp.youtube.com/live2/')

## Attention
- You need FFMPEG with RTMP Support !
- Insert in every output-option a slash to the end
- Slow because Puppeteers 'page.screenshot()' is to slow, i changed it from PNG to JPEG, to be faster (From ~14 to ~18 FPS)
- Don't remove the NullSound in the FFMPEG-Arguments, because youtube-live needs it

