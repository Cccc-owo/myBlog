---
title: CloudFlare Workers反向代理网站
description: 你是否会想要访问某些被墙的网站(如谷歌)时因各种原因不便访问呢？在这里，我推荐大家一个临时的解决方案。
tags:
  - CloudFlare
categories:
  - 技术
abbrlink: 9484e8b6
date: 2021-06-29 11:44:40
subtitle:
---

## 前言

你是否会想要访问 **某些被墙的网站** (如谷歌)时因各种原因不便访问呢？

在这里，我推荐大家一个临时的解决方案。

那就是CloudFlare Workers，下面让我们看看吧。

## 原理简介

详见[反向代理](https://baike.baidu.com/item/%E5%8F%8D%E5%90%91%E4%BB%A3%E7%90%86/7793488)、及[CloudFlare Workers](https://www.cloudflare.com/zh-cn/products/workers-kv)

## 步骤

### 注册（已有账号可跳过）

![1](https://cccc-drive.vercel.app/api?path=/Img%C2%B7%E5%9B%BE%E5%BA%8A/CloudFlareWorkers%E5%8F%8D%E4%BB%A3%E7%BD%91%E7%AB%99/1.png&raw=true)

如图1，打开[注册页面](https://dash.cloudflare.com/sign-up)进行注册

### 配置Workers

![2](https://cccc-drive.vercel.app/api?path=/Img%C2%B7%E5%9B%BE%E5%BA%8A/CloudFlareWorkers%E5%8F%8D%E4%BB%A3%E7%BD%91%E7%AB%99/2.png&raw=true)

如图2，单击登陆后主页右侧栏中的Workers

进入之后，单击「计划」并选择「Free」计划。如图3。

![3](https://cccc-drive.vercel.app/api?path=/Img%C2%B7%E5%9B%BE%E5%BA%8A/CloudFlareWorkers%E5%8F%8D%E4%BB%A3%E7%BD%91%E7%AB%99/3.png&raw=true)

接着新建一个 Workers 子域名，如图4。

![4](https://cccc-drive.vercel.app/api?path=/Img%C2%B7%E5%9B%BE%E5%BA%8A/CloudFlareWorkers%E5%8F%8D%E4%BB%A3%E7%BD%91%E7%AB%99/4.png&raw=true)

搞定以上步骤后，回到Workers主页面，并单击创建Worker。如图5。

![5](https://cccc-drive.vercel.app/api?path=/Img%C2%B7%E5%9B%BE%E5%BA%8A/CloudFlareWorkers%E5%8F%8D%E4%BB%A3%E7%BD%91%E7%AB%99/5.png&raw=true)

接着将如下代码复制入左边的脚本编辑处。

``` javascript
// Website you intended to retrieve for users.
const upstream = 'google.com'

// Custom pathname for the upstream website.
const upstream_path = '/'

// Website you intended to retrieve for users using mobile devices.
const upstream_mobile = 'google.com'

// Countries and regions where you wish to suspend your service.
const blocked_region = []

// IP addresses which you wish to block from using your service.
const blocked_ip_address = ['0.0.0.0', '127.0.0.1']

// Whether to use HTTPS protocol for upstream address.
const https = true

// Whether to disable cache.
const disable_cache = false

// Replace texts.
const replace_dict = {
    '$upstream': '$custom_domain',
    '//google.com': ''
}

addEventListener('fetch', event => {
    event.respondWith(fetchAndApply(event.request));
})

async function fetchAndApply(request) {
    const region = request.headers.get('cf-ipcountry').toUpperCase();
    const ip_address = request.headers.get('cf-connecting-ip');
    const user_agent = request.headers.get('user-agent');

    let response = null;
    let url = new URL(request.url);
    let url_hostname = url.hostname;

    if (https == true) {
        url.protocol = 'https:';
    } else {
        url.protocol = 'http:';
    }

    if (await device_status(user_agent)) {
        var upstream_domain = upstream;
    } else {
        var upstream_domain = upstream_mobile;
    }

    url.host = upstream_domain;
    if (url.pathname == '/') {
        url.pathname = upstream_path;
    } else {
        url.pathname = upstream_path + url.pathname;
    }

    if (blocked_region.includes(region)) {
        response = new Response('Access denied: WorkersProxy is not available in your region yet.', {
            status: 403
        });
    } else if (blocked_ip_address.includes(ip_address)) {
        response = new Response('Access denied: Your IP address is blocked by WorkersProxy.', {
            status: 403
        });
    } else {
        let method = request.method;
        let request_headers = request.headers;
        let new_request_headers = new Headers(request_headers);

        new_request_headers.set('Host', upstream_domain);
        new_request_headers.set('Referer', url.protocol + '//' + url_hostname);

        let original_response = await fetch(url.href, {
            method: method,
            headers: new_request_headers,
            body: request.body
        })

        connection_upgrade = new_request_headers.get("Upgrade");
        if (connection_upgrade && connection_upgrade.toLowerCase() == "websocket") {
            return original_response;
        }

        let original_response_clone = original_response.clone();
        let original_text = null;
        let response_headers = original_response.headers;
        let new_response_headers = new Headers(response_headers);
        let status = original_response.status;
  
  if (disable_cache) {
   new_response_headers.set('Cache-Control', 'no-store');
     }

        new_response_headers.set('access-control-allow-origin', '*');
        new_response_headers.set('access-control-allow-credentials', true);
        new_response_headers.delete('content-security-policy');
        new_response_headers.delete('content-security-policy-report-only');
        new_response_headers.delete('clear-site-data');
  
  if (new_response_headers.get("x-pjax-url")) {
            new_response_headers.set("x-pjax-url", response_headers.get("x-pjax-url").replace("//" + upstream_domain, "//" + url_hostname));
        }
  
        const content_type = new_response_headers.get('content-type');
        if (content_type != null && content_type.includes('text/html') && content_type.includes('UTF-8')) {
            original_text = await replace_response_text(original_response_clone, upstream_domain, url_hostname);
        } else {
            original_text = original_response_clone.body
        }
  
        response = new Response(original_text, {
            status,
            headers: new_response_headers
        })
    }
    return response;
}

async function replace_response_text(response, upstream_domain, host_name) {
    let text = await response.text()

    var i, j;
    for (i in replace_dict) {
        j = replace_dict[i]
        if (i == '$upstream') {
            i = upstream_domain
        } else if (i == '$custom_domain') {
            i = host_name
        }

        if (j == '$upstream') {
            j = upstream_domain
        } else if (j == '$custom_domain') {
            j = host_name
        }

        let re = new RegExp(i, 'g')
        text = text.replace(re, j);
    }
    return text;
}


async function device_status(user_agent_info) {
    var agents = ["Android", "iPhone", "SymbianOS", "Windows Phone", "iPad", "iPod"];
    var flag = true;
    for (var v = 0; v < agents.length; v++) {
        if (user_agent_info.indexOf(agents[v]) > 0) {
            flag = false;
            break;
        }
    }
    return flag;
}
```

配置完成后，修改Worker名称，点击「保存并部署」。如图6。

![6](https://cccc-drive.vercel.app/api?path=/Img%C2%B7%E5%9B%BE%E5%BA%8A/CloudFlareWorkers%E5%8F%8D%E4%BB%A3%E7%BD%91%E7%AB%99/6.png&raw=true)

这样就大功告成了，以后就可以随时随地谷歌一下了。

### 成品展示

Demo:<https://google.youwant.workers.dev/>

[稍微修改后访问Github](https://git.youwant.workers.dev)

如图7

![7](https://cccc-drive.vercel.app/api?path=/Img%C2%B7%E5%9B%BE%E5%BA%8A/CloudFlareWorkers%E5%8F%8D%E4%BB%A3%E7%BD%91%E7%AB%99/7.png&raw=true)

温馨提示：使用Worker反代的网站 **无法使用Cookies** ，简单来说就是搜索记录不会保存，账号无法登录。并且 **不要滥用** Worker代理!

## 尾声

当然Workers的功能远远不止如此，也不仅仅可以反代Google **这样的静态网站** ，它还有更多的地方等待着我们探索。多思考、多实践、多查找，这是很重要的。
