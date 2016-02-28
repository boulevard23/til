# Guzzle Async

PHP is a single-threaded model, so how does guzzle make async requests?

So basically, the magic all come from CurlMulti. It allows you to create multi curl handlers, and execute them. In the meantime, your php code can still continue execution.

Guzzle has several handlers:

* CurlHandler - via `curl_exec()`
* MultiHandler - via `curl_multi_exec()`
* StreamHandler - via `file_get_contents()`
* ProxyHandler - all of the above; **default**