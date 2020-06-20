## A simple example of Go (golang) api with jwt authentication
[![CircleCI](https://img.shields.io/circleci/project/pinbar/go-mux-jwt/master.svg)](https://circleci.com/gh/pinbar/go-mux-jwt)
[![Test Coverage](https://codeclimate.com/github/pinbar/go-mux-jwt/badges/coverage.svg)](https://codeclimate.com/github/pinbar/go-mux-jwt/coverage) [![Code Climate](https://codeclimate.com/github/pinbar/go-mux-jwt/badges/gpa.svg)](https://codeclimate.com/github/pinbar/go-mux-jwt) [![Issue Count](https://codeclimate.com/github/pinbar/go-mux-jwt/badges/issue_count.svg)](https://codeclimate.com/github/pinbar/go-mux-jwt)

### tech stack
* **Go** - a programming language that is fast, uses minimal resources and supports high concurrency
* **Gorilla Mux** - minimalistic request router and dispatcher
* **Gorilla Logging Handler** - middleware for http request/response logging
* **jwt-go** - a jwt library for Go
* **testify** - testing and assertion library
* **dep** - the official dependency management tool for Go
* **gin (optional)** - livereload utility for faster development turnaround in local

### pre-requisites
* Go is installed. To verify, run `go version`
* GOPATH is set (e.g. set to `~/go`)
* PATH includes `GOPATH/bin`
* `dep` is installed
    *  to get it, run `go get -u github.com/golang/dep/cmd/dep`


### getting started
* clone repo or download zip
* get the dependencies by running `dep ensure -update` in the project directory
* in the project directory, run `go build && ./go-mux-jwt`
* launch the browser and point to the baseurl `localhost:3001`
    * port can be changed in `main.go`
* *optional:*
    * use **gin** to monitor for changes and automatically restart the application
        * if you don't have gin, `go get github.com/codegangsta/gin`
        * in the project directory run `gin` (no need to build or run executable, when you do this)
    * update `Gopkg.toml` to use different version(s) for the dependency/vendor libs
        * run `dep ensure -update` after changing the toml file

### running tests
* to run the tests, run `go test` in the project directory
* **test coverage:** 
    * to run tests and generate coverage report, run `go test -cover`. 
    * percentage covered is shown in the terminal upon execution of this command

### api and authentication scenarios
* access the unsecure api `GET /metacortex`
* all `/api/*` calls are secured with JWT authentication
* try accessing the secure api `GET /api/megacity` to see an auth error
* obtain a JWT token here: `/static/authenticate.html`
    * enter programName:programPassword (neo:keanu)
    * the response contains a JWT token for that program
* use the token when calling any secure api (`/api/*`):
    * set the `Authorization` request header and add the jwt token, like so:
    * `Authorization: Bearer \<token\>`
* `GET /api/megacity` can be accessed with any valid token but `GET /api/levrai` can only be accessed with neo's token
