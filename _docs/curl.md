---
layout: docs
title: Curl
permalink: /docs/curl/
---

This [site](https://curl.haxx.se/docs/manual.html) has extensive examples.

GET

```bash
curl http://httpbin.org/ip
curl https://httpbin.org/get?show_env=1
curl -I http://httpbin.org/status/418
curl -u name:passwd http://httpbin.org
```

POST
    
    curl -d "name=Rafael%20Sagula&phone=3320780" http://ulka.io/guest

Nice alternatives
* [httpie](https://github.com/jkbrzt/httpie)  
* [http-prompt](https://github.com/eliangcs/http-prompt)  
* [postman](https://www.getpostman.com/)  
* [Convert curl to request code](http://curl.trillworks.com/)  