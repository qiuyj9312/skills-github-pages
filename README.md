---
layout: default
---
<div class="search-container">
  <input type="text" id="search-input" placeholder="search blog posts..." style="width: 90%;
    height: 35px;
    color: #333;
    background-color: rgba(227,231,236,.2);
    line-height: 35px;
    padding:0px 16px;
    border: 1px solid #c0c0c0;
    font-size: 16px;
    font-weight: bold;
    border-radius: 17px;
    outline: none;
    box-sizing: border-box;
    box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102,175,233,.6);">
  <ul id="results-container"></ul>
</div>

<!--script src="https://unpkg.com/simple-jekyll-search/dest/simple-jekyll-search.min.js"></script-->
<script src="{{ site.baseurl }}/js/simple-jekyll-search.min.js"></script>

<script>
	window.simpleJekyllSearch = new SimpleJekyllSearch({
	searchInput: document.getElementById('search-input'),
	resultsContainer: document.getElementById('results-container'),
	json: '{{ site.baseurl }}/search.json',
	searchResultTemplate: '<li><a href="{url}?query={query}" title="{desc}">{title}</a></li>',
	noResultsText: 'No results found',
	limit: 10,
	fuzzy: false,
	exclude: ['Welcome']
  })
</script>
 
{% if site.posts.size == 0 %}
  <h2>No post found</h2>
{% endif %}

<div class="posts">
  {% for post in paginator.posts %}
  {% unless post.draft %}
    <article class="post">
      <h1>
        <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
      </h1>

      <div clsss="meta">
        <span class="date">
          {{ post.date | date: "%Y-%m-%d" }}
        </span>

        <ul class="tag">
          {% for tag in post.tags %}
          <li>
            <a href="{{ site.url }}{{ site.baseurl }}/tags#{{ tag }}">
              {{ tag }}
            </a>
          </li>
          {% endfor %}
        </ul>
      </div>

      <div class="entry">
        {{ post.excerpt | truncate: 200 }}
      </div>

      <a href="{{ site.baseurl }}{{ post.url }}" class="read-more">Read More</a>
    </article>
  {% endunless %}
  {% endfor %}
</div>

<div class="pagination">
  {% if paginator.previous_page %}
    <span class="prev">
      <a href="{{ site.baseurl }}{{ paginator.previous_page_path }}" class="prev">
        ← 上一页
      </a>
    </span>
  {% endif %}
  {% if paginator.next_page %}
    <span class="next">
      <a href="{{ site.baseurl}}{{ paginator.next_page_path }}" class="next">
        下一页 →
      </a>
    </span>
  {% endif %}
</div>

<!--不算子网站访客统计-->
<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js">
</script>
<!-- pv的方式，单个用户连续点击n篇文章，记录n次访问量 -->
<div align="center">
	<span id="busuanzi_container_site_pv" style="font-family:Consolas;color:Silver;font-size:12px;">
		View:<span id="busuanzi_value_site_pv" style="font-family:Consolas;color:Silver;font-size:12px;"></span>
	</span>
	<!-- uv的方式，单个用户连续点击n篇文章，只记录1次访客数 -->
	<span id="busuanzi_container_site_uv" style="font-family:Consolas;color:Silver;font-size:12px;">
		User:<span id="busuanzi_value_site_uv" style="font-family:Consolas;color:Silver;font-size:12px;"></span>
	</span>
</div>
