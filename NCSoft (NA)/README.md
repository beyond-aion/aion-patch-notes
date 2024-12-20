Most PDFs were created manually from official web articles, since NCSoft only provided PDFs from version 3.5 to 6.2.  
Articles about minor updates consisting only of language corrections and bug fixes have not been converted to PDF.  

In case some of the files need to be recreated, here are the formatting tweaks which have been applied to the page prior to "printing" with Firefox via `Print..` > `Save as PDF...`:  
<details>
  <summary>1.5 - 3.1</summary>

  Source: archived [Game Guide](https://web.archive.org/web/20111227212740/http://gameguide.na.aiononline.com:80/aion/Patch+Notes) and [Powerwiki](https://web.archive.org/web/*/http://powerwiki.na.aiononline.com/aion/*) pages (some page elements needed to be manually removed)  

  ```js
  for (let p of [...document.getElementsByTagName("p")]) { if (p.innerText == " " && p.previous()?.innerText == " ") p.classList.add("print-hidden") }
  document.head.appendChild(document.createElement('style'))
  document.querySelector('style').textContent = " \
    @media print { \
      @page { size: Letter; margin: 1in 0; } \
      #main-container > .inner-container, #div_middle, #div_wrap { width: 720px } \
      html, body { background: none; background-color: #fff !important; } \
      div.heading_p, tr, p, li, h1, h2, h3, h4, h5, h6 { page-break-inside: avoid; } \
      :not(td) > p > strong::after, h1::after, h2::after, h3::after, h4::after, h5::after, h6::after { content: '.'; display: block; height: 100px; margin-bottom: -100px; visibility:hidden; } \
      #wm-ipp-print, #db-container, #bg, #aion-header, #div_left, #pmenu0, #pmenu, #aion-footer-container, body > .skip, body > h1.h_aion, .bt_edit, .wrap_act, #div_center > #div_contents > .wrap_top, .content-wiki:last-of-type { display: none !important; } \
      #div_center { margin: 0 !important; } \
      #div_center > #div_contents > .wrap_contents { padding: 0; } \
      #div_middle, #div_middle > #div_wrap { background: none; } \
      .content p, .content-wiki p { margin: 0; padding: 0; line-height: 18px; } \
      .content, .content-wiki { color: #333; line-height: 150%; font-size: 13px; word-wrap: break-word; word-break: keep-all; white-space: normal; }\
      #div_center > #div_contents > .wrap_contents table[style=\"FLOAT: left; MARGIN-RIGHT: 10px\"] { width: 100%; float: none !important; } \
      .print-hidden { display: none } \
    }"
  ```
</details>
<details>
  <summary>6.5+ & Aion Classic</summary>

  Source: https://www.aiononline.com/news/  
  Set to 80% zoom before printing.  

  ```js
  for (let img of document.getElementsByTagName('img')) { if (img.style.height) { img.style.setProperty('height', img.style.height, 'important') } }
  document.head.appendChild(document.createElement('style'))
  document.querySelector('style').textContent = " \
    @media print { \
      @page { size: Letter; margin: 1in 0; } \
      html { --zoomFactor: 0.8; } \
      html, body, #__next { background-color: #fff; } \
      tr, p:empty, li:empty, h1, h2, h3, h4, h5, h6 { page-break-inside: avoid; } \
      p::before, h1::before, h2::before, h3::before, h4::before, h5::before, h6::before { content: ''; display: block; height: 3px; margin-top: -3px; } \
      \
      td > p, th > p { margin: 0; } \
      .gnb-header, .gnb-footer, #navbar, .featured-news-wrapper, div.btn[data-nchide='true'], #l2-footer, #cookie-manager {display: none;} \
      main.news-article { background-color: #fff; padding: 0; } \
      main.news-article .article-content { margin-left: 1in; margin-right: 1in; width: calc(100% - 2in); } \
      main.news-article .article-content img { height: unset; } \
      main.news-article .article-content > .headline-wrapper > .title { margin: 10px 0 0; } \
      main.news-article > .bottom-wrapper { background-color: unset; } \
      main.news-article > .bottom-wrapper > .article-content { background-color: unset; } \
      main.news-article > .news-article-header { height: calc(8.5in / var(--zoomFactor) / (1920 / 800) + 4px); border-top-width: 4px; border-top-style: solid; } \
      main.news-article > .news-article-header > div.hero-mobile { background-size: cover; image-rendering: optimizequality; } \
    }"
  ```
</details>

The resulting files have then been [compressed](https://www.sejda.com/compress-pdf) at 200 ppi with image quality "Good" and source URLs have been [added to PDF metadata](https://www.sejda.com/edit-pdf-metadata).