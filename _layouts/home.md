---
layout: default
---

<!-- Page Header -->
{% if page.background %}
<header class="masthead" style="background-image: url('{{ page.background | prepend: site.baseurl | replace: '//', '/' }}')">
  {% else %}
  <header class="masthead">
    {% endif %}
    <div class="overlay"></div>
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <div class="page-heading">
            <h1>{{ site.title }}</h1>
            {% if site.description %}
            <span class="subheading">{{ site.description }}</span>
            {% endif %}
          </div>
        </div>
      </div>
    </div>
  </header>

  <div class="container">
    <div class="row">
      <div class="col-lg-4 col-md-8 list__category">
      <div>
        <h3>Search Item</h3>
        <form id="contact-form" action="">
           <input id="search" type="search" class="form-control" placeholder="e.g. About us" autocomplete="off">
        </form>
      </div>
      <div class="category">
        <h3>Categories</h3>
        <ul class="nav__category">
          {% for item in site.categories limit : 5 %}
            <li class="item--category">
              <a href="categories/#{{ item | first | slugify }}">
                <i class="fa fa-list-alt" aria-hidden="true"></i>
                {{ item | first }}
              </a>
            </li>
          {% endfor %}
        </ul>
      </div>
      <div class="tags">
        <h3>Tag</h3>
        <ul class="nav__tags">
        <i class="fa fa-tag" aria-hidden="true"></i>
          {% for item in site.tags limit : 15 %}
            <span>
              <a href="tags/#{{ item | first | slugify }}">
                #{{ item | first }}   
              </a>
            </span>
          {% endfor %}
        </ul>
      </div>
      </div>
      <div class="col-lg-8 col-md-10 mx-auto">
        {{ content }}
        <!-- Home Post List -->
        <div id="searchResult">
        </div>
        <div id="allData">
          {% for post in site.posts limit : 5 %}
          <article class="post-preview">
            <a href="{{ post.url | prepend: site.baseurl | replace: '//', '/' }}">
              <h2 class="post-title">{{ post.title }}</h2>
              {% if post.subtitle %}
              <h3 class="post-subtitle">{{ post.subtitle }}</h3>
              {% else %}
              <h3 class="post-subtitle">{{ post.excerpt | strip_html | truncatewords: 15 }}</h3>
              {% endif %}
            </a>
            <p class="post-meta">Posted by
              {% if post.author %} {{ post.author }} {% else %}
              {{ site.author }} {% endif %} on {{ post.date | date: '%B %d, %Y' }}          
            </p>
          </article>
          <hr>
          {% endfor %}
          <!-- Pager -->
          <div class="clearfix">
            <a class="btn btn-primary float-right" href="{{"/posts" | relative_url }}">View All Posts &rarr;</a>
          </div>
        </div>
      </div>
    </div>
  </div>


<script type="text/javascript" src="{{ "/assets/fetch.js" | relative_url }}"></script>
<script type="text/javascript">
  const endpoint = '{{ "/assets/search.json" | relative_url }}';
  const main_author =  '{{ site.author }}'
  const pages = [];
  fetch(endpoint)
    .then(blob => blob.json())
    .then(data => pages.push(...data))
  function findResults(termToMatch, pages) {
    return pages.filter(item => {
      const regex = new RegExp(termToMatch, 'gi');
      return item.title.match(regex) || item.content.match(regex);
    });
  }
  function formatDate(date) {
    if (date && date != ''){
      let date_str = new Date(date)
      return date_str.toDateString()
    } else {
      return ''
    }
  }
  function displayResults() {
    if (field.value && field.value != ''){
      const resultsArray = findResults(this.value, pages);
      const html = resultsArray.map(item => {
      const url = item.url ? item.url : '';
      const title = item.title ? item.title : '';
      const subtitle = item.subtitle ? item.subtitle : '';
      const author = (item.author && (item.author != '' || item.author != '\n' || item.author != '\r')) ? item.author : main_author;
      let date = item.date ? item.date : '';
      date = formatDate(date);
      return `
        <article class="post-preview">
          <a href="${url}">
            <h2 class="post-title">${title}</h2>
            <h3 class="post-subtitle">${subtitle}</h3>
          </a>
          <p class="post-meta">Posted by ${author} on ${date}</p>
        </article>`;
      }).join('');
      if ((resultsArray.length == 0) || (this.value == '')) {
        resultsList.innerHTML = `<p>Sorry, nothing was found</p>`;
        resultsList.style.display = "block";
        allData.style.display = "none";
      } else {
        allData.style.display = "none";
        resultsList.style.display = "block";
        resultsList.innerHTML = html;
      }
    } else {
      resultsList.style.display = "none";
      allData.style.display = "block";
    }
  }
  const allData = document.querySelector('#allData');
  const field = document.querySelector('#search');
  const resultsList = document.querySelector('#searchResult');
  field.addEventListener('keyup', displayResults);
  field.addEventListener('keypress', function(event) {
    if (event.keyCode == 13) {
      event.preventDefault();
    }
  });
</script>
<noscript>Please enable JavaScript to use the search form.</noscript>
