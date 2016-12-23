---
layout: post
title: How to use the Jekyll to set up your blog
category: Learning
tags: Jekyll, Learning
---

# Learning Jekyll Notes

[TOC]

## _config.xml 配置文件

### 全局配置

| 属性          | Example                                  | 解释             |
| ----------- | ---------------------------------------- | -------------- |
| source      | source: DIRName                          | Jekyll 读取文件的目录 |
| destination | destination: DIRName                     | Jekyll 写入文件的目录 |
| safe        | safe: BOOL                               | 禁用自定义插件        |
| exclude     | exclude: [DIR, FILE, ...]                | 排除某些文件         |
| include     | include: [DIR, FILE, ...]                | 强制包含某些文件       |
| timezone    | timezone: [TIMEZONE](https://en.wikipedia.org/wiki/Tz_database) |                |
| encoding    | encoding: ENCODING                       |                |

### 编译选项

| 选项          | 配置               | 解释         |
| ----------- | ---------------- | ---------- |
| future      | future: BOOL     | 用将来的日期发布文章 |
| limit_posts | limit_posts: NUM | 限制文章数量     |

### 服务选项

| 选项      | 配置             | 解释           |
| ------- | -------------- | ------------ |
| port    | port: PORT     | 监听所给的端口      |
| host    | host: HOSTNAME | 监听所给主机名（本地）  |
| baseurl | baseurl: URL   | 网站根路径        |
| detach  | detach: BOOL   | 从终端命令分离出来??? |

#### 默认配置文件

>```HTML
>source:      .
>destination: ./_site
>plugins:     ./_plugins
>layouts:     ./_layouts
>include:     ['.htaccess']
>exclude:     []
>keep_files:  ['.git','.svn']
>gems:        []
>timezone:    nil
>encoding:    nil
>
>future:      true
>show_drafts: nil
>limit_posts: 0
>highlighter: pygments
>
>relative_permalinks: true
>
>permalink:     date
>paginate_path: 'page:num'
>paginate:      nil
>
>markdown:      maruku
>markdown_ext:  markdown,mkd,mkdn,md
>textile_ext:   textile
>
>excerpt_separator: "\n\n"
>
>safe:        false
>watch:       false    # deprecated
>server:      false    # deprecated
>host:        0.0.0.0
>port:        4000
>baseurl:     /
>url:         http://localhost:4000
>lsi:         false
>
>maruku:
>  use_tex:    false
>  use_divs:   false
>  png_engine: blahtex
>  png_dir:    images/latex
>  png_url:    /images/latex
>  fenced_code_blocks: true
>
>rdiscount:
>  extensions: []
>
>redcarpet:
>  extensions: []
>
>kramdown:
>  auto_ids: true
>  footnote_nr: 1
>  entity_output: as_char
>  toc_levels: 1..6
>  smart_quotes: lsquo,rsquo,ldquo,rdquo
>  use_coderay: false
>
>  coderay:
>    coderay_wrap: div
>    coderay_line_numbers: inline
>    coderay_line_numbers_start: 1
>    coderay_tab_width: 4
>    coderay_bold_every: 10
>    coderay_css: style
>
>redcloth:
>  hard_breaks: true
>```

## YAML 头信息

### 预定义全局变量

| 变量名称       | Example                                  | 描述                        | 注释   |
| ---------- | ---------------------------------------- | ------------------------- | ---- |
| layout     | layout: post                             | 到 目录 _layouts 下找寻对应的模板文件。 | 可选   |
| title      | title: Title Display on the page         | 展示在页面上的标题                 | 可选   |
| permalink  | permalink: /year/month/day/title.html    | 设置指定的 URL 地址              | 可选   |
| published  | published: false                         | 设置是否发布                    | 可选   |
| category   | category:                                | 设置分配属性                    | 可选   |
| categories | categories: categoryName1, categoryName2 | 设置多个分类属性                  | 可选   |
| tags       | tags: jekyll, github pages               | 设置page 标签                 | 可选   |

### 自定义变量

| 变量名称 | Example          | 描述     | 注释   |
| ---- | ---------------- | ------ | ---- |
| date | date: 2016-12-23 | 设定文档日期 |      |

## 撰写文档

### 引用文件或图片

图片

`![DisplayText]({{site.url}}/imagePath/imageName.jpg)`

文件

`[DisplayText]({{site.url}}/filePath/fileName.xxx)`

### 文章目录

Liquid 模板语言

```html
<ul>
  {% for post in site.posts %}
  <li>
  	<a href="{{post.url}}">{{post.title}}</a>
  </li>
  {% endfor %}
</ul>
```

Liquid Template Language

### 文章摘要

```html
<ul>
  {% for post in site.posts %}
  <li>
  	<a href="{{post.url}}">{{post.title}}</a>
    {{ post.excerpt }}
    <!-- or this -->
    {{ post.excerpt | remove: '<p>'|remove:'</p>' }}
  </li>
  {% endfor %}
</ul>
```

### 高亮代码片段

Highlight via Pygments

```
{% highlight ruby lineos%}
def show
  @widget = Widget(params[:id])
  respond_to do |format|
    format.html # show.html.erb
    format.json { render json: @widget }
  end
end
{% endhighlight %}
```

Highlight via Markdown

```ruby
def show
  @widget = Widget(params[:id])
  respond_to do |format|
    format.html # show.html.erb
    format.json { render json: @widget }
  end
end
```

