#   htp

Notable changes to this project will be documented in this file. This project adheres to [Semantic Versioning 2.0.0](http://semver.org/).

##	[0.6.1] - Feb 7th, 2018

### Changed, RISKY

*	When instance of `stream.Readable` used as HTTP body, errors on the stream will be caught and the request action will be ceased forcely.

##	[0.6.0] - Feb 1st, 2018

###	New

*	Property `beforeCallback` added to `options` argument in `new SimpleAgent(options)`.

##	[0.5.1] - Jan 16, 2018

##	Changed, RISKY

*	In this version, hostname in the URL will be replaced with IP address returned by __dns-agent__ before being passed to `http.request()` or `https.request()` to avoid repetitive DNS requests for resolving the same hostname.  
	在这个版本中，我们用 __dns-agent__ 返回的 IP 地址替换 URL 中的主机名，然后才将其传递至 `http.request()` 或 `https.request()` 方法。__dns-agent__ 本身具备可靠的及可调节的缓存功能，如果针对同一主机名的 URL 地址，发生高并发调用或短时间内的大量调用，这一作法可以有效避免系统重复发起 DNS 解析。

##	[0.5.0] - Jan 8, 2018

##	Fixed, IMPORTANT

*	Fixed the bug that when invoking methods with payload (e.g. POST and PUT) of instanceof of __htp/SimpleAgent__, body of falsed value 0-length string will be ignored.
*	Force the clientRequest to abort and the incommingMessage (response) to destroy on error ocurring.  
	此前，当错误发生后，请求和响应可能并未终止，由此可能导致不可预知的问题。

##	[0.4.2] - Jan 2, 2018

*	On *piping* mode, pass *address* object to listener of event *dns*.

##	[0.4.1] - Jan 2, 2018

###	Fixed

*	Fixed the bug that, on *piping* mode, event *dns* is missed if hostname has been resolved and cached before.
*	Fixed the bug that, on *piping* mode, event *error* is missed.

##	[0.4.0] - Dec 13, 2017

*	[dns-agent](https://www.npmjs.com/package/dns-agent) is depended while __htp__ is resolving domain names.

##	[0.3.0] - Dec 8, 2017

*	Setting *rejectUnauthorized* added.

##	[0.2.0]

###	New

*	Byeond *basic* and *piping* mode, new *pipingOnly* mode is offered.
*	Returned stream in *piping* mode will emit events and may be catched via `on(<eventName>, ...)` method.
*	[README in Simplifed Chinese language](./README.zh_CN.md).

###	Fixed

*	In previous version, `htp/SimpleAgent` will invoke `callback()` (if passed) twice if there is some exception throwed in `callback()` itself.

###	What is difference between *piping* and *pipingOnly* ?

In *piping* mode, you may get data via piping to a writable stream, or reading `response.body` and `response.bodyBuffer` directly in function `callback(err, response)` which is passed as the last argument.

##	[0.1.1] - Nov 23, 2017

###	Fixed

*	In previous versions, __htp__ cannot recognized some key fields in response headers if their names are not lowercased. 

##	[0.1.0] - 2017-11-12

###	Milestone

Now， __htp__ is streamable. E.g.  
```javascript
htp.piping.get('http://www.example.com/').pipe(fs.createWriteStream('index.html'));
```

##	[0.0.5] - 2017-11

__htp/sSimpleAgent__ added.

##	[0.0.4] - 2017-10

Add new *action* property to Errors throwed. Value of the property is made up of the method name and the url joined with a whitespace, e.g.
```javascript
htp.get('http://www.example.com/', function(err, response) {
	if (err) {
		err.action == 'GET http://www.example.com/'; // true
	}
});
```

##  [0.0.3] - 2017-09

No promise created or returned when callback() functions offered.

##	[0.0.2] - 2017-07, https

HTTPS requests are supported.

##	[0.0.1] - 2017-07

Released.

---
This CHANGELOG.md follows [*Keep a CHANGELOG*](http://keepachangelog.com/).
