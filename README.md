<p align="center">


 <a href="https://www.gitbook.com/book/kataras/iris/details"><img  width="600" src="https://raw.githubusercontent.com/iris-contrib/website/gh-pages/assets/book/cover_6_flat_alpha.png"></a>

<br/>

<a href="https://travis-ci.org/kataras/iris"><img src="https://img.shields.io/travis/kataras/iris.svg?style=flat-square" alt="Build Status"></a>

<a href="https://github.com/avelino/awesome-go"><img src="https://img.shields.io/badge/awesome-%E2%9C%93-ff69b4.svg?style=flat-square" alt="https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg"></a>

<a href="#"><img src="https://img.shields.io/badge/platform-Any-ec2eb4.svg?style=flat-square" alt="Platforms"></a>

<a href="https://github.com/kataras/iris/blob/master/LICENSE"><img src="https://img.shields.io/badge/license-MIT%20%20-E91E63.svg?style=flat-square" alt="License"></a>


<a href="https://golang.org"><img src="https://img.shields.io/badge/powered_by-Go-3362c2.svg?style=flat-square" alt="Built with GoLang"></a>

<br/>


<a href="https://github.com/kataras/iris/releases"><img src="https://img.shields.io/badge/%20version%20-%204.4.4%20-blue.svg?style=flat-square" alt="Releases"></a>

<a href="https://github.com/iris-contrib/examples"><img src="https://img.shields.io/badge/%20examples-repository-3362c2.svg?style=flat-square" alt="Examples"></a>

<a href="https://www.gitbook.com/book/kataras/iris/details"><img src="https://img.shields.io/badge/%20docs-reference-5272B4.svg?style=flat-square" alt="Practical Guide/Docs"></a>

<a href="https://kataras.rocket.chat/channel/iris"><img src="https://img.shields.io/badge/%20community-chat-00BCD4.svg?style=flat-square" alt="Chat"></a><br/><br/>


The <a href="https://github.com/kataras/iris#benchmarks">fastest</a> backend web framework for Go.
<br/>
Easy to <a href="https://www.gitbook.com/book/kataras/iris/details">learn</a>,  while it's highly customizable. <br/>
Ideally suited for both experienced and novice <b>Developers</b>.
<br/>
<br/>

<img src="https://raw.githubusercontent.com/smallnest/go-web-framework-benchmark/4db507a22c964c9bc9774c5b31afdc199a0fe8b7/benchmark.png" href="#benchmarks" alt="Benchmark Wizzard July 21, 2016- Processing Time Horizontal Graph" />

</p>




Quick Look
------------

```go
package main

import "github.com/kataras/iris"

func main() {
  // serve static files, just a fav here
  iris.Favicon("./favicon.ico")

  // handle "/" - HTTP METHOD: "GET"
  iris.Get("/", func(ctx *iris.Context) {
    ctx.Render("index.html", nil)
  })

  iris.Get("/login", func(ctx *iris.Context) {
    ctx.Render("login.html", iris.Map{"Title": "Login Page"})
  })

  // handle "/login" - HTTP METHOD: "POST"
  iris.Post("/login", func(ctx *iris.Context) {
    secret := ctx.PostValue("secret")
    ctx.Session().Set("secret", secret)

    ctx.Redirect("/user")
  })

  // handle websocket connections
  iris.Config.Websocket.Endpoint = "/mychat"
  iris.Websocket.OnConnection(func(c iris.WebsocketConnection) {
    c.Join("myroom")

    c.On("chat", func(message string){
      c.To("myroom").Emit("chat", "From "+c.ID()+": "+message)
    })
  })

  // serve requests at http://localhost:8080
  iris.Listen(":8080")
}
```

What's inside?
------------

- Focus on high performance
- Automatically install TLS certificates from https://letsencrypt.org
- Robust routing and middleware ecosystem
- Define virtual hosts and (wildcard) subdomains with path level routing
- Graceful shutdown
- Limit request body
- I18N
- Serve static files
- Log requests
- Gzip response
- Authentication
 - OAuth, OAuth2 supporting 27+ popular websites
 - JWT
 - Basic Authentication
 - HTTP Sessions
- Add / Remove trailing slash from the URL with option to redirect
- Redirect requests
 - HTTP to HTTPS
 - HTTP to HTTPS WWW
 - HTTP to HTTPS non WWW
 - Non WWW to WWW
 - WWW to non WWW
- View system supporting more than six template engines
- Highly scalable rich render (Markdown, JSON, JSONP, XML...)
- Websocket API similar to socket.io  
- Hot Reload
- Typescript integration + Web IDE
- Checks for updates at startup

Getting Started
------------

### Installation

The only requirement is the [Go Programming Language](https://golang.org/dl), at least v1.7.

```bash
$ go get -u github.com/kataras/iris/iris
```

> If you have installation issues or you are connected to the Internet through China please, [click here](https://kataras.gitbooks.io/iris/content/install.html).

### Need help?

 <a href="https://www.gitbook.com/book/kataras/iris/details"><img align="right" width="125" src="https://raw.githubusercontent.com/iris-contrib/website/gh-pages/assets/book/cover_4.jpg"></a>


 - The most important is to read [the practical guide](https://kataras.gitbooks.io/iris/content/).

 - Explore & download the [examples](https://github.com/iris-contrib/examples).

 - [HISTORY.md](https://github.com//kataras/iris/tree/master/HISTORY.md) file is your best friend.

#### FAQ

Explore [these questions](https://github.com/kataras/iris/issues?q=label%3Aquestion) or navigate to the [community chat][Chat].


Support
------------

Hi, my name is Gerasimos Maropoulos and I'm the author of this project, let me put a few words about me.

I started to design iris the night of the 13 March 2016, some weeks later, iris started to became famous and I have to fix many issues and implement new features, but I didn't have time to work on Iris because I had a part time job and the (software engineering) colleague which I studied.

I wanted to make iris' users proud of the framework they're using, so I decided to interrupt my studies and colleague, two days later I left from my part time job also.

Today I spend all my days and nights coding for Iris, and I'm happy about this, therefore I have zero incoming value.

- :star: the project
- [Donate](https://github.com/kataras/iris/blob/master/DONATIONS.md)
- :earth_americas: spread the word
- [Contribute](#contributing) to the project




| Name        | Description           | Usage  |
| ------------------|:---------------------:|-------:|
| [JSON ](https://github.com/kataras/go-serializer/tree/master/json)      | JSON Serializer (Default)                  |[example 1](https://github.com/iris-contrib/examples/blob/master/serialize_engines/json_1/main.go),[example 2](https://github.com/iris-contrib/examples/blob/master/serialize_engines/json_2/main.go), [book section](https://kataras.gitbooks.io/iris/content/serialize-engines.html)
| [JSONP ](https://github.com/kataras/go-serializer/tree/master/jsonp)      | JSONP Serializer (Default)                  |[example 1](https://github.com/iris-contrib/examples/blob/master/serialize_engines/jsonp_1/main.go),[example 2](https://github.com/iris-contrib/examples/blob/master/serialize_engines/jsonp_2/main.go), [book section](https://kataras.gitbooks.io/iris/content/serialize-engines.html)
| [XML ](https://github.com/kataras/go-serializer/tree/master/xml)      | XML Serializer (Default)                  |[example 1](https://github.com/iris-contrib/examples/blob/master/serialize_engines/xml_1/main.go),[example 2](https://github.com/iris-contrib/examples/blob/master/serialize_engines/xml_2/main.go), [book section](https://kataras.gitbooks.io/iris/content/serialize-engines.html)
| [Markdown ](https://github.com/kataras/go-serializer/tree/master/markdown)      | Markdown Serializer (Default)                  |[example 1](https://github.com/iris-contrib/examples/blob/master/serialize_engines/markdown_1/main.go),[example 2](https://github.com/iris-contrib/examples/blob/master/serialize_engines/markdown_2/main.go), [book section](https://kataras.gitbooks.io/iris/content/serialize-engines.html)
| [Text](https://github.com/kataras/go-serializer/tree/master/text)      | Text Serializer (Default)                  |[example 1](https://github.com/iris-contrib/examples/blob/master/serialize_engines/text_1/main.go), [book section](https://kataras.gitbooks.io/iris/content/serialize-engines.html)
| [Binary Data ](https://github.com/kataras/go-serializer/tree/master/data)      | Binary Data Serializer (Default)                  |[example 1](https://github.com/iris-contrib/examples/blob/master/serialize_engines/data_1/main.go), [book section](https://kataras.gitbooks.io/iris/content/serialize-engines.html)
| [HTML/Default Engine ](https://github.com/kataras/go-template/tree/master/html)      | HTML Template Engine (Default)                  |[example ](https://github.com/iris-contrib/examples/blob/master/template_engines/template_html_0/main.go), [book section](https://kataras.gitbooks.io/iris/content/template-engines.html)
| [Django Engine ](https://github.com/kataras/go-template/tree/master/django)      | Django Template Engine                  |[example ](https://github.com/iris-contrib/examples/blob/master/template_engines/template_django_1/main.go), [book section](https://kataras.gitbooks.io/iris/content/template-engines.html)
| [Pug/Jade Engine ](https://github.com/kataras/go-template/tree/master/pug)      | Pug Template Engine                  |[example ](https://github.com/iris-contrib/examples/blob/master/template_engines/template_pug_1/main.go), [book section](https://kataras.gitbooks.io/iris/content/template-engines.html)
| [Handlebars Engine ](https://github.com/kataras/go-template/tree/master/handlebars)      | Handlebars Template Engine                  |[example ](https://github.com/iris-contrib/examples/blob/master/template_engines/template_handlebars_1/main.go), [book section](https://kataras.gitbooks.io/iris/content/template-engines.html)
| [Amber Engine ](https://github.com/kataras/go-template/tree/master/amber)      | Amber Template Engine                  |[example ](https://github.com/iris-contrib/examples/blob/master/template_engines/template_amber_1/main.go), [book section](https://kataras.gitbooks.io/iris/content/template-engines.html)
| [Markdown Engine ](https://github.com/kataras/go-template/tree/master/markdown)      | Markdown Template Engine                  |[example ](https://github.com/iris-contrib/examples/blob/master/template_engines/template_markdown_1/main.go), [book section](https://kataras.gitbooks.io/iris/content/template-engines.html)
| [Basicauth Middleware ](https://github.com/iris-contrib/middleware/tree/master/basicauth)      | HTTP Basic authentication                  |[example 1](https://github.com/iris-contrib/examples/blob/master/middleware_basicauth_1/main.go), [example 2](https://github.com/iris-contrib/examples/blob/master/middleware_basicauth_2/main.go), [book section](https://kataras.gitbooks.io/iris/content/basic-authentication.html)  |
| [JWT Middleware ](https://github.com/iris-contrib/middleware/tree/master/jwt)      | JSON Web Tokens                  |[example ](https://github.com/iris-contrib/examples/blob/master/middleware_jwt/main.go), [book section](https://kataras.gitbooks.io/iris/content/jwt.html)  |
| [Cors Middleware ](https://github.com/iris-contrib/middleware/tree/master/cors)      | Cross Origin Resource Sharing W3 specification   | [how to use ](https://github.com/iris-contrib/middleware/tree/master/cors#how-to-use)  |
| [Secure Middleware ](https://github.com/iris-contrib/middleware/tree/master/secure) |  Facilitates some quick security wins      | [example](https://github.com/iris-contrib/examples/blob/master/middleware_secure/main.go)  |
| [I18n Middleware ](https://github.com/iris-contrib/middleware/tree/master/i18n)      | Simple internationalization       | [example](https://github.com/iris-contrib/examples/tree/master/middleware_internationalization_i18n), [book section](https://kataras.gitbooks.io/iris/content/middleware-internationalization-and-localization.html)  |
| [Recovery Middleware ](https://github.com/iris-contrib/middleware/tree/master/recovery) | Safety recover the station from panic       | [example](https://github.com/iris-contrib/examples/blob/master/middleware_recovery/main.go)  |
| [Logger Middleware ](https://github.com/iris-contrib/middleware/tree/master/logger)      | Logs every request       | [example](https://github.com/iris-contrib/examples/blob/master/middleware_logger/main.go), [book section](https://kataras.gitbooks.io/iris/content/logger.html)  |
| [Profile Middleware ](https://github.com/iris-contrib/middleware/tree/master/pprof)      | Http profiling for debugging    | [example](https://github.com/iris-contrib/examples/blob/master/middleware_pprof/main.go)  |
| [Editor Plugin](https://github.com/iris-contrib/plugin/tree/master/editor)      | Alm-tools, a typescript online IDE/Editor | [book section](https://kataras.gitbooks.io/iris/content/plugin-editor.html) |
| [Typescript Plugin](https://github.com/iris-contrib/plugin/tree/master/typescript)      | Auto-compile client-side typescript files      |   [book section](https://kataras.gitbooks.io/iris/content/plugin-typescript.html) |
| [OAuth,OAuth2 Plugin](https://github.com/iris-contrib/plugin/tree/master/oauth) |  User Authentication was never be easier, supports >27 providers |    [example](https://github.com/iris-contrib/examples/tree/master/plugin_oauth_oauth2), [book section](https://kataras.gitbooks.io/iris/content/plugin-oauth.html) |
| [Iris control Plugin](https://github.com/iris-contrib/plugin/tree/master/iriscontrol) |   Basic (browser-based) control over your Iris station |    [example](https://github.com/iris-contrib/examples/blob/master/plugin_iriscontrol/main.go), [book section](https://kataras.gitbooks.io/iris/content/plugin-iriscontrol.html) |



Philosophy
------------

The Iris philosophy is to provide robust tooling for HTTP, making it a great solution for single page applications, web sites, hybrids, or public HTTP APIs. Keep note that, today, iris has the clostest performance to the nginx.

Iris does not force you to use any specific ORM or template engine. With support for the most used template engines, you can quickly craft the perfect application.



Benchmarks
------------

This Benchmark test aims to compare the whole HTTP request processing between Go web frameworks.


![Benchmark Wizzard July 21, 2016- Processing Time Horizontal Graph](https://raw.githubusercontent.com/smallnest/go-web-framework-benchmark/4db507a22c964c9bc9774c5b31afdc199a0fe8b7/benchmark.png)

**The results have been updated on July 21, 2016**

Testing
------------

I recommend writing your API tests using this new library, [httpexpect](https://github.com/gavv/httpexpect) which supports Iris and fasthttp now, after my request [here](https://github.com/gavv/httpexpect/issues/2). You can find Iris examples [here](https://github.com/gavv/httpexpect/blob/master/example/iris_test.go), [here](https://github.com/kataras/iris/blob/master/http_test.go) and [here](https://github.com/kataras/iris/blob/master/context_test.go).

Versioning
------------

Current: **v4.4.4**

>  Iris is an active project

Read more about Semantic Versioning 2.0.0

 - http://semver.org/
 - https://en.wikipedia.org/wiki/Software_versioning
 - https://wiki.debian.org/UpstreamGuide#Releases_and_Versions

Todo
------------

Iris is a **Community-Driven** Project, waiting for your suggestions and [feature requests](https://github.com/kataras/iris/issues?utf8=%E2%9C%93&q=label%3A%22feature%20request%22)!

People
------------
The big thanks goes to [all people](https://github.com/kataras/iris/issues?utf8=%E2%9C%93&q=label%3A%22feature+request%22) who help building this framework with feature-requests & bug reports!

The author of Iris is [@kataras](https://github.com/kataras). If **you**'re willing to donate, feel **free** to navigate to the [DONATIONS PAGE](https://github.com/kataras/iris/blob/master/DONATIONS.md).


Contributing
------------
If you are interested in contributing to the Iris project, please see the document [CONTRIBUTING](https://github.com/kataras/iris/blob/master/CONTRIBUTING.md).

License
------------

This project is licensed under the [MIT License](LICENSE), Copyright (c) 2016 Gerasimos Maropoulos.


[Travis Widget]: https://img.shields.io/travis/kataras/iris.svg?style=flat-square
[Travis]: http://travis-ci.org/kataras/iris
[License Widget]: https://img.shields.io/badge/license-MIT%20%20License%20-E91E63.svg?style=flat-square
[License]: https://github.com/kataras/iris/blob/master/LICENSE
[Release Widget]: https://img.shields.io/badge/release-4.4.4%20-blue.svg?style=flat-square
[Release]: https://github.com/kataras/iris/releases
[Chat Widget]: https://img.shields.io/badge/community-chat%20-00BCD4.svg?style=flat-square
[Chat]: https://kataras.rocket.chat/channel/iris
[ChatMain]: https://kataras.rocket.chat/channel/iris
[ChatAlternative]: https://gitter.im/kataras/iris
[Report Widget]: https://img.shields.io/badge/report%20card%20-A%2B-F44336.svg?style=flat-square
[Report]: http://goreportcard.com/report/kataras/iris
[Documentation Widget]: https://img.shields.io/badge/docs-reference%20-5272B4.svg?style=flat-square
[Documentation]: https://www.gitbook.com/book/kataras/iris/details
[Examples Widget]: https://img.shields.io/badge/examples-repository%20-3362c2.svg?style=flat-square
[Examples]: https://github.com/iris-contrib/examples
[Language Widget]: https://img.shields.io/badge/powered_by-Go-3362c2.svg?style=flat-square
[Language]: http://golang.org
[Platform Widget]: https://img.shields.io/badge/platform-Any--OS-gray.svg?style=flat-square
[Awesome]: https://github.com/avelino/awesome-go
[Awesome Widget]: https://img.shields.io/badge/awesome%20go-%E2%9C%93-ff69b4.svg?style=flat-square
