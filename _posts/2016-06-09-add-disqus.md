---
layout: post
title:  "깃허브 블로그에 disqus 서비스로 댓글 적용"
date:   2016-06-09 17:20:00 +0900
categories: jekyll
tags: ['jekyll', 'disqus', 'blog', 'comment', '댓글']
---
깃허브를 기반으로 블로그를 생성하고 여러가지 커스터마이징을 진행하고 있습니다.

첫번째로 진행하는 것은 댓글 기능을 추가하는 것인데요.

여기저기 둘러보니 disqus를 이용해서 댓글 기능을 추가하고 계시더군요.

disqus의 자세한 내용은 검색해 보면 많은 내용이 나오니 참고하시구요.

제가 참고한 블로그는 [Disqus - github 블로그에 댓글 기능 추가하기](http://djflexible.github.io/blog/disqus.html){:target="_blank"} 입니다.

disqus에 가입하고 Site를 만들어 셋팅하는 것까지는 그리 어렵지 않았습니다.

그런데 소스를 적용하는 부분이 문제더군요.

disqus의 installation code를 생성하면 아래와 같이 생성됩니다.

{% highlight html %}
<div id="disqus_thread"></div> <script> /** * RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS. * LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables */ /* var disqus_config = function () { this.page.url = PAGE_URL; // Replace PAGE_URL with your page's canonical URL variable this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable }; */ (function() { // DON'T EDIT BELOW THIS LINE var d = document, s = d.createElement('script'); s.src = '//******.disqus.com/embed.js'; s.setAttribute('data-timestamp', +new Date()); (d.head || d.body).appendChild(s); })(); </script> <noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript" rel="nofollow">comments powered by Disqus.</a></noscript>
{% endhighlight %}

주석 라인과 실제 코드 라인이 뒤석여 실제로 코드가 정상 실행되지 않는 상태가 되었습니다.

위의 코드를 동작하도록 간단히 컨벤션을 적용할 필요가 있었습니다.

아래는 컨벤션이 적용된 코드입니다.

{% highlight html %}
<div id="disqus_thread"></div>
<script>
/**
* RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
* LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables
*/
/* var disqus_config = function () { this.page.url = PAGE_URL;
// Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = PAGE_IDENTIFIER;
// Replace PAGE_IDENTIFIER with your page's unique identifier variable };
*/
(function() {
// DON'T EDIT BELOW THIS LINE
var d = document, s = d.createElement('script');
s.src = '//******.disqus.com/embed.js';
s.setAttribute('data-timestamp', +new Date());
(d.head || d.body).appendChild(s); })();
</script>
<noscript>
Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript" rel="nofollow">comments powered by Disqus.</a>
</noscript>
{% endhighlight %}

코드를 변경하고 나니 정상적으로 댓글 기능이 동작하게 되었습니다.
