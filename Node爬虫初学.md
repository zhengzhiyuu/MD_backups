---
title: Node_Spider_初学
date: 2017-07-24 16:17:46
tags: [Node.Js]
categories: [前端,Node.Js]
---
第一次尝试爬虫 ，之前挺好奇的
<!-- more -->
使用的模块：` node内置fs `,` cheerio `,` rquest `
爬取网易云部分歌单...
在网易云歌单url爬取不到...查看源代码的url可以
```js
const fs = require('fs')
const request = require('request')
const cheerio = require('cheerio')

request('http://music.163.com/discover/playlist', (err, res, body) => {
    err ? console.log(err) : console.log('ok')
    let $ = cheerio.load(body)
    let arr = []
    $('img[class=j-flag]').each(function (i, elem) {
        let obj = {
            img: $(this).attr('src'),
            title: $('.msk').eq(i).attr('title'),
            number: $('.nb').eq(i).text(),
            author: $('.s-fc4').eq(i).next().text(),
        }
        arr.push(obj)
    })
    console.log(arr)
    fs.writeFile('song.json', JSON.stringify(arr), err => console.log(err))
})
```
第三版：
爬取图片...
```js
const fs = require('fs')
const request = require('request')
const cheerio = require('cheerio')

let arr = []
for (let i = 0; i < 11; i++) {
    let url = `http://www.jianshu.com/trending/monthly?&page=${i}`
    request(url, (error, response, body) => {
        let $ = cheerio.load(body)
        let title = $('.title')
        title.each(function (index, elem) {
            let author = $('.blue-link').eq(index).text()
            let img = $('.wrap-img').eq(index).find('img').attr('src')
            let title = {
                title: $(this).text().trim(),
                author: author,
                src: $(this).attr('href'),
                index: i + '-' + index,
                img: img
            }
            arr.push(title)
            // console.log(title)
        })
        fs.writeFile('./data/dir.txt', JSON.stringify(arr), error => error ? console.log(error) : console.log(url + ': 目录写入'))
        arr.forEach(i =>
            request('http://www.jianshu.com' + i.src, function (error, response, body) {
                // you need to judge
                if (body) {
                    let $ = cheerio.load(body)
                    let text = $('.show-content').text()
                    fs.writeFile('./data/text_' + i.index + '.txt', text, err => err ? console.log(err) : console.log('ok: ', i.title))
                }
            })
        )
        arr.forEach(i => {
            if (i.img) {
                request('http:' + i.img).pipe(fs.createWriteStream(`./data/img/${i.index}.jpg`))
            }
        })
    })
}
```
第二版：
改进只能抓取20条的缺陷...
从chrome找到分页请求 循环url
```js
const fs = require('fs')
const request = require('request')
const cheerio = require('cheerio')

let arr = []
for (let i = 0; i < 11; i++) {
    let url = `http://www.jianshu.com/trending/monthly?&page=${i}`
    request(url, (error, response, body) => {
        let $ = cheerio.load(body)
        let title = $('.title')
        title.each(function (index, elem) {
            let author = $('.blue-link').eq(i).text()
            let title = {
                title: $(this).text().trim(),
                author: author,
                src: $(this).attr('href'),
                index: i + '-' + index
            }
            arr.push(title)
        })
        fs.writeFile('./data/dir.txt', JSON.stringify(arr), error => error ? console.log(error) : console.log(url + ': 目录写入'))
        arr.forEach(i =>
            request('http://www.jianshu.com' + i.src, function (error, response, body) {
                // you need to judge
                if (body) {
                    let $ = cheerio.load(body)
                    let text = $('.show-content').text()
                    fs.writeFile('./data/text_' + i.index + '.txt', text, err => err ? console.log(err) : console.log('ok: ', i.title))
                }
            })
        )
    })
}
```
初版：
```js
const fs = require('fs')
const request = require('request');
const cheerio = require('cheerio')

function spider(url) {
    request(url, function (error, response, body) {
        console.log('error:', error)
        console.log('statusCode:', response && response.statusCode)
        let $ = cheerio.load(body)
        let arr = []
        $('.title').each(function (i, elem) {
            let author = $('.blue-link').eq(i).text()
            arr[i] = {
                title: $(this).text().trim(),
                author: author,
                src: $(this).attr('href'),
                index: i
            }
        })
        arr.splice(arr.length - 1, 1)
        fs.writeFile('./data/dir.txt', JSON.stringify(arr), err => err ? console.log(err) : console.log('ok'))

        arr.forEach(i =>
            request('http://www.jianshu.com' + i.src, function (error, response, body) {
                let $ = cheerio.load(body)
                let text = $('.show-content').text()
                fs.writeFile('./data/text_' + i.index + '.txt', text, err => err ? console.log(err) : console.log('ok: ', i.title))
            })
        )
    })
}

spider('http://www.jianshu.com/')
```