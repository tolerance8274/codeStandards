# camera

This is a simple webservice for taking screenshots of sites using a real browser using Selenium. It's meant to be a building block for setting up your own visual regression testing. Features:

* Automatically restarts the browser when necessary for basic error recovery.
* Takes screenshots by hiding scrollbars, scaling images consistently using nearest neighbor, and taking into account browser chrome/UI dimensions.
* Attempts to resize the browser window height to fit the webpage.


## Getting started

### Using straight Docker

```bash
docker run -d --name selenium --expose 4444 selenium/standalone-chrome:3.0.1-aluminum
docker run -d --name camera --link selenium -e SELENIUM_BROWSER=chrome -e SELENIUM_REMOTE_URL=http://selenium:4444/wd/hub -p 3000:3000 digdep/camera
```

## Taking a screenshot

The webservice has one endpoint (the `width` parameter defaults to 1280):

```
GET /capture?url=&width=
```

```
HTTP/1.1 200 OK
Content-Type: image/png

[data]
```

(Replace `localhost` with your Docker host if necessary. If using Docker Machine on OS X, use `$ docker-machine url` to find that out.)
