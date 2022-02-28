<p align="center">
<h1 align="center">Resty</h1>
<p align="center">Simple HTTP and REST client library for Go (inspired by Ruby rest-client)</p>
<p align="center"><a href="#features">Features</a> section describes in detail about Resty capabilities</p>
</p>
<p align="center">
<p align="center"><a href="https://github.com/go-resty/resty/actions/workflows/ci.yml?query=branch%3Amaster"><img src="https://github.com/go-resty/resty/actions/workflows/ci.yml/badge.svg" alt="Build Status"></a> <a href="https://codecov.io/gh/go-resty/resty/branch/master"><img src="https://codecov.io/gh/go-resty/resty/branch/master/graph/badge.svg" alt="Code Coverage"></a> <a href="https://goreportcard.com/report/go-resty/resty"><img src="https://goreportcard.com/badge/go-resty/resty" alt="Go Report Card"></a> <a href="https://github.com/go-resty/resty/releases/latest"><img src="https://img.shields.io/badge/version-2.7.0-blue.svg" alt="Release Version"></a> <a href="https://pkg.go.dev/github.com/go-resty/resty/v2"><img src="https://pkg.go.dev/badge/github.com/go-resty/resty" alt="GoDoc"></a> <a href="LICENSE"><img src="https://img.shields.io/github/license/go-resty/resty.svg" alt="License"></a> <a href="https://github.com/avelino/awesome-go"><img src="https://awesome.re/mentioned-badge.svg" alt="Mentioned in Awesome Go"></a></p>
</p>
<p align="center">
<h4 align="center">Resty Communication Channels</h4>
<p align="center"><a href="https://gitter.im/go_resty/community?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge"><img src="https://badges.gitter.im/go_resty/community.svg" alt="Chat on Gitter - Resty Community"></a> <a href="https://twitter.com/go_resty"><img src="https://img.shields.io/badge/twitter-@go__resty-55acee.svg" alt="Twitter @go_resty"></a></p>
</p>

## News

  * v2.7.0 [released](https://github.com/go-resty/resty/releases/tag/v2.7.0) and tagged on Nov 03, 2021.
  * v2.0.0 [released](https://github.com/go-resty/resty/releases/tag/v2.0.0) and tagged on Jul 16, 2019.
  * v1.12.0 [released](https://github.com/go-resty/resty/releases/tag/v1.12.0) and tagged on Feb 27, 2019.
  * v1.0 released and tagged on Sep 25, 2017. - Resty's first version was released on Sep 15, 2015 then it grew gradually as a very handy and helpful library. Its been a two years since first release. I'm very thankful to Resty users and its [contributors](https://github.com/go-resty/resty/graphs/contributors).

## Features

  * GET, POST, PUT, DELETE, HEAD, PATCH, OPTIONS, etc.
  * Simple and chainable methods for settings and request
  * [Request](https://pkg.go.dev/github.com/go-resty/resty/v2#Request) Body can be `string`, `[]byte`, `struct`, `map`, `slice` and `io.Reader` too
    * Auto detects `Content-Type`
    * Buffer less processing for `io.Reader`
    * Native `*http.Request` instance may be accessed during middleware and request execution via `Request.RawRequest`
    * Request Body can be read multiple times via `Request.RawRequest.GetBody()`
  * [Response](https://pkg.go.dev/github.com/go-resty/resty/v2#Response) object gives you more possibility
    * Access as `[]byte` array - `response.Body()` OR Access as `string` - `response.String()`
    * Know your `response.Time()` and when we `response.ReceivedAt()`
  * Automatic marshal and unmarshal for `JSON` and `XML` content type
    * Default is `JSON`, if you supply `struct/map` without header `Content-Type`
    * For auto-unmarshal, refer to -
        - Success scenario [Request.SetResult()](https://pkg.go.dev/github.com/go-resty/resty/v2#Request.SetResult) and [Response.Result()](https://pkg.go.dev/github.com/go-resty/resty/v2#Response.Result).
        - Error scenario [Request.SetError()](https://pkg.go.dev/github.com/go-resty/resty/v2#Request.SetError) and [Response.Error()](https://pkg.go.dev/github.com/go-resty/resty/v2#Response.Error).
        - Supports [RFC7807](https://tools.ietf.org/html/rfc7807) - `application/problem+json` & `application/problem+xml`
    * Resty provides an option to override [JSON Marshal/Unmarshal and XML Marshal/Unmarshal](#override-json--xml-marshalunmarshal)
  * Easy to upload one or more file(s) via `multipart/form-data`
    * Auto detects file content type
  * Request URL [Path Params (aka URI Params)](https://pkg.go.dev/github.com/go-resty/resty/v2#Request.SetPathParams)
  * Backoff Retry Mechanism with retry condition function [reference](retry_test.go)
  * Resty client HTTP & REST [Request](https://pkg.go.dev/github.com/go-resty/resty/v2#Client.OnBeforeRequest) and [Response](https://pkg.go.dev/github.com/go-resty/resty/v2#Client.OnAfterResponse) middlewares
  * `Request.SetContext` supported
  * Authorization option of `BasicAuth` and `Bearer` token
  * Set request `ContentLength` value for all request or particular request
  * Custom [Root Certificates](https://pkg.go.dev/github.com/go-resty/resty/v2#Client.SetRootCertificate) and Client [Certificates](https://pkg.go.dev/github.com/go-resty/resty/v2#Client.SetCertificates)
  * Download/Save HTTP response directly into File, like `curl -o` flag. See [SetOutputDirectory](https://pkg.go.dev/github.com/go-resty/resty/v2#Client.SetOutputDirectory) & [SetOutput](https://pkg.go.dev/github.com/go-resty/resty/v2#Request.SetOutput).
  * Cookies for your request and CookieJar support
  * SRV Record based request instead of Host URL
  * Client settings like `Timeout`, `RedirectPolicy`, `Proxy`, `TLSClientConfig`, `Transport`, etc.
  * Optionally allows GET request with payload, see [SetAllowGetMethodPayload](https://pkg.go.dev/github.com/go-resty/resty/v2#Client.SetAllowGetMethodPayload)
  * Supports registering external JSON library into resty, see [how to use](https://github.com/go-resty/resty/issues/76#issuecomment-314015250)
  * Exposes Response reader without reading response (no auto-unmarshaling) if need be, see [how to use](https://github.com/go-resty/resty/issues/87#issuecomment-322100604)
  * Option to specify expected `Content-Type` when response `Content-Type` header missing. Refer to [#92](https://github.com/go-resty/resty/issues/92)
  * Resty design
    * Have client level settings & options and also override at Request level if you want to
    * Request and Response middleware
    * Create Multiple clients if you want to `resty.New()`
    * Supports `http.RoundTripper` implementation, see [SetTransport](https://pkg.go.dev/github.com/go-resty/resty/v2#Client.SetTransport)
    * goroutine concurrent safe
    * Resty Client trace, see [Client.EnableTrace](https://pkg.go.dev/github.com/go-resty/resty/v2#Client.EnableTrace) and [Request.EnableTrace](https://pkg.go.dev/github.com/go-resty/resty/v2#Request.EnableTrace)
      * Since v2.4.0, trace info contains a `RequestAttempt` value, and the `Request` object contains an `Attempt` attribute
    * Debug mode - clean and informative logging presentation
    * Gzip - Go does it automatically also resty has fallback handling too
    * Works fine with `HTTP/2` and `HTTP/1.1`
  * [Bazel support](#bazel-support)
  * Easily mock Resty for testing, [for e.g.](#mocking-http-requests-using-httpmock-library)
  * Well tested client library

### Included Batteries

  * Redirect Policies - see [how to use](#redirect-policy)
    * NoRedirectPolicy
    * FlexibleRedirectPolicy
    * DomainCheckRedirectPolicy
    * etc. [more info](redirect.go)
  * Retry Mechanism [how to use](#retries)
    * Backoff Retry
    * Conditional Retry
    * Since v2.6.0, Retry Hooks - [Client](https://pkg.go.dev/github.com/go-resty/resty/v2#Client.AddRetryHook), [Request](https://pkg.go.dev/github.com/go-resty/resty/v2#Request.AddRetryHook)
  * SRV Record based request instead of Host URL [how to use](resty_test.go#L1412)
  * etc (upcoming - throw your idea's [here](https://github.com/go-resty/resty/issues)).


#### Supported Go Versions

Initially Resty started supporting `go modules` since `v1.10.0` release.

Starting Resty v2 and higher versions, it fully embraces [go modules](https://github.com/golang/go/wiki/Modules) package release. It requires a Go version capable of understanding `/vN` suffixed imports:

- 1.9.7+
- 1.10.3+
- 1.11+


## It might be beneficial for your project :smile:

Resty author also published following projects for Go Community.

  * [aah framework](https://aahframework.org) - A secure, flexible, rapid Go web framework.
  * [THUMBAI](https://thumbai.app) - Go Mod Repository, Go Vanity Service and Simple Proxy Server.
  * [go-model](https://github.com/jeevatkm/go-model) - Robust & Easy to use model mapper and utility methods for Go `struct`.


## Installation

```bash
# Go Modules
require github.com/go-resty/resty/v2 v2.7.0
```

## Usage

The following samples will assist you to become as comfortable as possible with resty library.

```go
// Import resty into your code and refer it as `resty`.
import "github.com/go-resty/resty/v2"
```

#### Simple GET

```go
// Create a Resty Client
client := resty.New()

resp, err := client.R().
    EnableTrace().
    Get("https://httpbin.org/get")

// Explore response object
fmt.Println("Response Info:")
fmt.Println("  Error      :", err)
fmt.Println("  Status Code:", resp.StatusCode())
fmt.Println("  Status     :", resp.Status())
fmt.Println("  Proto      :", resp.Proto())
fmt.Println("  Time       :", resp.Time())
fmt.Println("  Received At:", resp.ReceivedAt())
fmt.Println("  Body       :\n", resp)
fmt.Println()

// Explore trace info
fmt.Println("Request Trace Info:")
ti := resp.Request.TraceInfo()
fmt.Println("  DNSLookup     :", ti.DNSLookup)
fmt.Println("  ConnTime      :", ti.ConnTime)
fmt.Println("  TCPConnTime   :", ti.TCPConnTime)
fmt.Println("  TLSHandshake  :", ti.TLSHandshake)
fmt.Println("  ServerTime    :", ti.ServerTime)
fmt.Println("  ResponseTime  :", ti.ResponseTime)
fmt.Println("  TotalTime     :", ti.TotalTime)
fmt.Println("  IsConnReused  :", ti.IsConnReused)
fmt.Println("  IsConnWasIdle :", ti.IsConnWasIdle)
fmt.Println("  ConnIdleTime  :", ti.ConnIdleTime)
fmt.Println("  RequestAttempt:", ti.RequestAttempt)
fmt.Println("  RemoteAddr    :", ti.RemoteAddr.String())

/* Output
Response Info:
  Error      : <nil>
  Status Code: 200
  Status     : 200 OK
  Proto      : HTTP/2.0
  Time       : 457.034718ms
  Received At: 2020-09-14 15:35:29.784681 -0700 PDT m=+0.458137045
  Body       :
  {
    "args": {},
    "headers": {
      "Accept-Encoding": "gzip",
      "Host": "httpbin.org",
      "User-Agent": "go-resty/2.4.0 (https://github.com/go-resty/resty)",
      "X-Amzn-Trace-Id": "Root=1-5f5ff031-000ff6292204aa6898e4de49"
    },
    "origin": "0.0.0.0",
    "url": "https://httpbin.org/get"
  }

Request Trace Info:
  DNSLookup     : 4.074657ms
  ConnTime      : 381.709936ms
  TCPConnTime   : 77.428048ms
  TLSHandshake  : 299.623597ms
  ServerTime    : 75.414703ms
  ResponseTime  : 79.337µs
  TotalTime     : 457.034718ms
  IsConnReused  : false
  IsConnWasIdle : false
  ConnIdleTime  : 0s
  RequestAttempt: 1
  RemoteAddr    : 3.221.81.55:443
*/
```

#### Enhanced GET

```go
// Create a Resty Client
client := resty.New()

resp, err := client.R().
      SetQueryParams(map[string]string{
          "page_no": "1",
          "limit": "20",
          "sort":"name",
          "order": "asc",
          "random":strconv.FormatInt(time.Now().Unix(), 10),
      }).
      SetHeader("Accept", "application/json").
      SetAuthToken("BC594900518B4F7EAC75BD37F019E08FBC594900518B4F7EAC75BD37F019E08F").
      Get("/search_result")


// Sample of using Request.SetQueryString method
resp, err := client.R().
      SetQueryString("productId=232&template=fresh-sample&cat=resty&source=google&kw=buy a lot more").
      SetHeader("Accept", "application/json").
      SetAuthToken("BC594900518B4F7EAC75BD37F019E08FBC594900518B4F7EAC75BD37F019E08F").
      Get("/show_product")


// If necessary, you can force response content type to tell Resty to parse a JSON response into your struct
resp, err := client.R().
      SetResult(result).
      ForceContentType("application/json").
      Get("v2/alpine/manifests/latest")
```
