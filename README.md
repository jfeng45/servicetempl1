# A Self-Evolved Microservice Framework in Go

Other language: 
### **[中文](README.zh.md)**

This is a major upgrade version of [jfeng45/servicetmpl](https://github.com/jfeng45/servicetmpl).

The followings are a series of articles to explain the different areas of the application design:

+ [Go Microservice with Clean Architecture-A Major Upgrade](
https://medium.com/@jfeng45/go-microservice-with-clean-architecture-a-major-upgrade-34a4cedb0b06)
+ [A Self-Evolved Microservice Framework in Go](https://medium.com/@jfeng45/a-self-evolved-microservice-framework-in-go-d9bf87c10ab0)
+ [A Non-Intrusive Transaction Management Lib in Go — How to Use It](https://medium.com/swlh/a-non-intrusive-transaction-management-lib-in-go-how-to-use-it-a3e751cc1dd4)
+ [A Non-Intrusive Transaction Management Lib in Go — How it Works?](https://medium.com/nerd-for-tech/a-non-intrusive-transaction-management-lib-in-go-how-it-works-51d4b2ede8af)


## Getting Started

### Installation and Setting Up

Don't need to finish all steps in this section up-front to get the code up running. The simplest way is to get the code from github and run it and come back to install the part when there is a real need. However, it will encounter an error when accesses the database. So, I'd recommend you install at least one database ( MySQL is better), then most of the code will work. 

#### Download Code

```
go get github.com/jfeng45/servicetmpl1
```

#### Set Up MySQL

There are two database implementations, MySQL and CouchDB, but most functions are implemented in MySQL. You'd better install at least one of them. 
```
Install MySQL
run SQL script in script folder to create database and table
```
#### Install CouchDB

The code works fine without it. CouchDB is created to show the feature of switching database by changing configuration.
 
Installation on [Windows](https://docs.couchdb.org/en/2.2.0/install/windows.html)

Installation on [Linux](https://docs.couchdb.org/en/2.2.0/install/unix.html)

Installation on [Mac](https://docs.couchdb.org/en/2.2.0/install/mac.html)

CouchDB [Example](https://github.com/go-kivik/kivik/wiki/Usage-Examples)

#### Set up CouchDB

```
Access "Fauxton" through browser: http://localhost:5984/_utils/# (login with: admin/admin).
Create new database "service_config" in "Fauxton".
Add the following document to the database ( "_id" and "_rev" are generated by database, no need to change it):
{
  "_id": "80a9134c7dfa53f67f6be214e1000fa7",
  "_rev": "4-f45fb8bdd454a71e6ae88bdeea8a0b4c",
  "uid": 10,
  "username": "Tony",
  "department": "IT",
  "created": "2018-02-17T15:04:05-03:00"
}
```
#### Install Cache Service (Another Microservice)

Without it, calling another Microservice piece won't work, the rest of application works fine. Please follow instructions in [reservegrpc](https://github.com/jfeng45/reservegrpc) to set up the service.

### Start Application

#### Start MySQL Server
```
cd [MySQLroot]/bin
mysqld
```

#### Start CouchDB Server
```
It should already have been started
```
#### Start Cache Service

Please follow instructions in [reservegrpc](https://github.com/jfeng45/reservegrpc) to start the server.

#### Run main

##### Run as a local application
In "main()" function of "main.go", there are two functions "testMySql()" and "testCouchDB()". 
"testMySql()" reads configurations from "configs/appConifgDev.yaml" and accesses MySQL. "testCouchDB()" reads from "configs/appConifgProd.yaml" and access CouchDB.
There are multiple functions in "testMySql()", you can focus on testing one each time by commenting out others.
```
cd [rootOfProject]/cmd
go run main.go
```
##### Run as a gRPC Microservice application

Start gRPC Server
```
cd [rootOfProject]/cmd/grpcserver
go run grpcServerMain.go
```
Start gRPC Client
```
cd [rootOfProject]/cmd/grpcclient
go run grpcClientMain.go
```

## License

[MIT](LICENSE.txt) License


