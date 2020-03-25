# Server Benchmarks

A benchmark suite which, **transparently**, stress-tests web servers and generates a report in markdown. It measures the requests per second, data transferred and time between requests and responses.

## Why YABS (Yet Another Benchmark Suite)

It's true, there already enough of benchmark suites to play around. However, most of them don't even contain real-life test applications to benchmark, therefore the results are not always accurate e.g. a route handler executes SQL queries or reads and sends JSON. This benchmark suite is a fresh start, it can contain any type of tests as the tests are running as self-executables and the measuring is done by a popular and trusted 3rd-party software which acts as a real HTTP Client (one more reason of transparency). [Contributions](CONTRIBUTING.md) and improvements are always welcomed here.

## Use case

Measure the performance of application(s) between different versions or implementations (or web frameworks).

This suite can be further customized, through its [tests.yml](tests.yml) file, in order to test personal or internal web applications before their public releases.

## How to run

1. Install [Go](https://golang.org/dl), [Bombardier](https://github.com/codesenberg/bombardier/releases/tag/v1.2.4), [Node.js](https://nodejs.org/en/download/current/) and [.NET Core](https://dotnet.microsoft.com/download)
2. Clone the repository
3. Stress-tests are described inside [tests.yml](tests.yml) file, it can be customized to fit your needs
4. Execute: `go build -o server-benchmarks`
5. Run and wait for the executable _server-benchmarks_ (or _server-benchmarks.exe_ for windows) to finish
6. Read the results from the generated _README.md_ file.

### Docker

The only requirement is [Docker](https://docs.docker.com/).

```sh
$ docker run -v ${PWD}:/data kataras/server-benchmarks
```

## Benchmarks

The following generated README contains benchmark results from builtin tests between popular **HTTP/2 web frameworks as of 2020**.

_Note:_ it's possible that the contents of this file will be updated regularly to accept even more tests cases and frameworks.

## System

|    |    |
|----|:---|
| Processor | Intel(R) Core(TM) i7-8750H CPU @ 2.20GHz |
| RAM | 15.85 GB |
| OS | Microsoft Windows 10 Pro for Workstations |
| [Bombardier](https://github.com/codesenberg/bombardier) | v1.2.4 |
| [Go](https://golang.org) | go1.14.1 |
| [.Net Core](https://dotnet.microsoft.com/) | 3.1.102 |
| [Node.js](https://nodejs.org/) | v13.10.1 |

> Last updated: Mar 25, 2020 at 2:27am (UTC)

## Terminology

**Name** is the name of the framework(or router) used under a particular test.

**Reqs/sec** is the avg number of total requests could be processed per second (the higher the better).

**Latency** is the amount of time it takes from when a request is made by the client to the time it takes for the response to get back to that client (the smaller the better).

**Throughput** is the rate of production or the rate at which data are transferred (the higher the better, it depends from response length (body + headers).

**Time To Complete** is the total time (in seconds) the test completed (the smaller the better).

## Results

### Test:Static

📖 Fires 1000000 requests, receives a static message as response.

| Name | Language | Reqs/sec | Latency | Throughput | Time To Complete |
|------|:---------|:---------|:--------|:-----------|:-----------------|
| [Iris](https://github.com/kataras/iris) | Go |204949 |608.59us |35.76MB |4.88s |
| [Kestrel](https://github.com/dotnet/aspnetcore) | C# |196571 |634.21us |33.36MB |5.09s |
| [Chi](https://github.com/pressly/chi) | Go |191334 |651.97us |33.38MB |5.23s |
| [Gin](https://github.com/gin-gonic/gin) | Go |188961 |660.20us |32.97MB |5.29s |
| [Echo](https://github.com/labstack/echo) | Go |187496 |665.21us |32.71MB |5.33s |
| [Martini](https://github.com/go-martini/martini) | Go |159299 |781.90us |27.82MB |6.27s |
| [Koa](https://github.com/koajs/koa) | Javascript |108606 |1.13ms |21.81MB |9.05s |
| [Express](https://github.com/expressjs/express) | Javascript |87136 |1.43ms |22.49MB |11.45s |
| [Buffalo](https://github.com/gobuffalo/buffalo) | Go |37578 |3.32ms |6.56MB |26.61s |

### Test:Parameterized

📖 Fires 250000 requests with a dynamic parameter of string, receives a hello text based on the parameter as response.

| Name | Language | Reqs/sec | Latency | Throughput | Time To Complete |
|------|:---------|:---------|:--------|:-----------|:-----------------|
| [Iris](https://github.com/kataras/iris) | Go |196439 |634.16us |37.65MB |1.27s |
| [Chi](https://github.com/pressly/chi) | Go |188574 |661.75us |36.09MB |1.33s |
| [Echo](https://github.com/labstack/echo) | Go |179996 |693.60us |34.43MB |1.39s |
| [Gin](https://github.com/gin-gonic/gin) | Go |175949 |708.40us |33.70MB |1.42s |
| [Kestrel](https://github.com/dotnet/aspnetcore) | C# |171922 |726.37us |31.87MB |1.46s |
| [Martini](https://github.com/go-martini/martini) | Go |148154 |841.40us |28.39MB |1.69s |
| [Koa](https://github.com/koajs/koa) | Javascript |92351 |1.62ms |16.50MB |3.25s |
| [Express](https://github.com/expressjs/express) | Javascript |66184 |2.17ms |15.77MB |4.36s |
| [Buffalo](https://github.com/gobuffalo/buffalo) | Go |37705 |3.31ms |7.23MB |6.63s |

### Test:REST

📖 Fires 200000 requests with a dynamic parameter of int, sends JSON as request body and receives JSON as response.

| Name | Language | Reqs/sec | Latency | Throughput | Time To Complete |
|------|:---------|:---------|:--------|:-----------|:-----------------|
| [Iris](https://github.com/kataras/iris) | Go |145521 |0.86ms |39.81MB |1.38s |
| [Gin](https://github.com/gin-gonic/gin) | Go |141640 |0.88ms |38.77MB |1.41s |
| [Echo](https://github.com/labstack/echo) | Go |137591 |0.91ms |37.75MB |1.45s |
| [Chi](https://github.com/pressly/chi) | Go |136044 |0.92ms |36.57MB |1.47s |
| [Kestrel](https://github.com/dotnet/aspnetcore) | C# |120682 |1.04ms |36.93MB |1.67s |
| [Martini](https://github.com/go-martini/martini) | Go |120001 |1.04ms |32.25MB |1.67s |
| [Buffalo](https://github.com/gobuffalo/buffalo) | Go |52407 |2.38ms |14.39MB |3.82s |
| [Koa](https://github.com/koajs/koa) | Javascript |52194 |2.59ms |14.28MB |4.15s |
| [Express](https://github.com/expressjs/express) | Javascript |38824 |3.14ms |14.27MB |5.02s |


## License

This project is licensed under the [MIT License](LICENSE).
