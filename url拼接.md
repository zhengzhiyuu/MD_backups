---
title: url拼接
date: 2017-09-21 13:49:07
tags: [前端,工具]
categories: [前端]
---
jsonp url拼接
<!-- more -->
```js
url += (url.indexOf('?') < 0 ? '?' : '&') + param(data)

function param(data) {
  let url = ''
  for (var k in data) {
    let value = data[k] !== undefined ? data[k] : ''
    url += '&' + k + '=' + encodeURIComponent(value)
  }
  return url ? url.substring(1) : ''
}
```