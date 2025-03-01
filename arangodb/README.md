# ArangoDB
A ArangoDB storage driver using `arangodb/go-driver` and [arangodb/go-driver](https://github.com/arangodb/go-driver).

### Table of Contents
- [Signatures](#signatures)
- [Installation](#installation)
- [Examples](#examples)
- [Config](#config)
- [Default Config](#default-config)

### Signatures
```go
func New(config ...Config) Storage
func (s *Storage) Get(key string) ([]byte, error)
func (s *Storage) Set(key string, val []byte, exp time.Duration) error
func (s *Storage) Delete(key string) error
func (s *Storage) Reset() error
func (s *Storage) Close() error
```
### Installation
ArangoDB is tested on the 2 last (1.14/1.15) [Go versions](https://golang.org/dl/) with support for modules. So make sure to initialize one first if you didn't do that yet:
```bash
go mod init github.com/<user>/<repo>
```
And then install the mysql implementation:
```bash
go get github.com/gofiber/storage/arangodb
```

### Examples
Import the storage package.
```go
import "github.com/gofiber/storage/arangodb"
```

You can use the following possibilities to create a storage:
```go
// Initialize custom config
// *http* is mandatory
store := arangodb.New(arangodb.Config{
	Host:            "http://127.0.0.1",
	Port:            "8529",
    Username:        "username",
    Password:        "password"
	Database:        "fiber",
	Collection:      "fiber_storage",
	Reset:           false,
	GCInterval:      10 * time.Second,
})
```

### Config
```go
type Config struct {
	// Host name where the DB is hosted
	//
	// Optional. Default is "http://127.0.0.1"
	Host string

	// Port where the DB is listening on
	//
	// Optional. Default is 8529
	Port string

	// Server username
	//
	// Mandatory
	Username string

	// Server password
	//
	// Mandatory
	Password string

	// Database name
	//
	// Optional. Default is "fiber"
	Database string

	// Collection name
	//
	// Optional. Default is "fiber_storage"
	Collection string

	// Reset clears any existing keys in existing collection
	//
	// Optional. Default is false
	Reset bool
	// Time before deleting expired keys
	//
	// Optional. Default is 10 * time.Second
	GCInterval time.Duration
}
```

### Default Config
Used only for optional fields
```go
var ConfigDefault = Config{
	Host:       "http://127.0.0.1",
	Port:       "8529",
	Database:   "fiber",
	Collection: "fiber_storage",
	Reset:      false,
	GCInterval: 10 * time.Second,
}
```
