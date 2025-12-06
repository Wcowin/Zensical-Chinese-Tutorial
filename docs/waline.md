---
title: 留言板
hide:
  - footer
  - feedback
# comments: true
# disqus: true
hide_comment: true
---

<!-- # 留言板 -->

<!-- <link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/Wcowin/Wcowin.github.io@main/docs/stylesheets/poem.css"> -->


<h1 style="text-align:center;">畅所欲言</h1>




<!-- tw开始 -->

<!-- <head>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.12.0/dist/katex.min.css" integrity="sha384-AfEj0r4/OFrOo5t7NnNe46zW/tFgW6x/bCJG8FqQCEo3+Aro6EYUG4+cU+KJWu/X" crossorigin="anonymous" />
  <script defer="" src="https://cdn.jsdelivr.net/npm/katex@0.12.0/dist/katex.min.js" integrity="sha384-g7c+Jr9ZivxKLnZTDUhnkOnsh30B4H0rpLUpJ4jAIKs4fnJI+sEnkvrMWph2EDg4" crossorigin="anonymous"></script>
  <script defer="" src="https://cdn.jsdelivr.net/npm/katex@0.12.0/dist/contrib/auto-render.min.js" integrity="sha384-mll67QQFJfxn0IYznZYonOWZ644AWYC+Pt2cHqMaRhXVrursRwvLnLaebdGIlYNa" crossorigin="anonymous"></script>

 </head>
<body>
  <link rel="preload" href="https://registry.npmmirror.com/twikoo/1.6.44/files/dist/twikoo.min.js" as="script">

  <div id="tcomment" class="loading"></div>
  <script>
  function loadTwikoo() {
    const script = document.createElement('script');
    script.src = 'https://registry.npmmirror.com/twikoo/1.6.44/files/dist/twikoo.min.js';
    script.onload = function() {
      initTwikoo();
    };
    script.onerror = function() {
      console.error('Twikoo 脚本加载失败');
      document.getElementById('tcomment').innerHTML = '评论系统加载失败，请刷新页面重试';
    };
    document.head.appendChild(script);
  }
  function initTwikoo() {
    const commentEl = document.getElementById('tcomment');
    commentEl.classList.remove('loading');
    twikoo.init({
      envId: 'https://superb-salamander-e730b6.netlify.app/.netlify/functions/twikoo',
      el: '#tcomment',
      lang: 'zh-CN',
      path: location.pathname,
      onCommentLoaded: function () {
        console.log('评论加载完成');
      },
      onError: function(err) {
        console.error('Twikoo 初始化失败:', err);
        commentEl.innerHTML = '评论系统初始化失败，请检查网络连接';
      }
    });
  }
  if (document.readyState === 'loading') {
    document.addEventListener('DOMContentLoaded', loadTwikoo);
  } else {
    loadTwikoo();
  }
  </script>
</body> -->


<div id="cusdis_thread"
  data-host="https://cusdis.com"
  data-app-id="655cf3bc-734a-4d88-8317-be350621334c"
  data-page-id="{{ PAGE_ID }}"
  data-page-url="{{ PAGE_URL }}"
  data-page-title="{{ PAGE_TITLE }}"
></div>
<script async defer src="https://cusdis.com/js/cusdis.es.js"></script>



