
[Microservices](https://www.nginx.com/blog/introduction-to-microservices/)

### Tackling the complex

The goal of microservices is to sufficiently decompose the application in order to facilitate agile application development and deployment.

### The factors of complexity and corresponding solutions

![complexity and factor](https://www.nginx.com/wp-content/uploads/2016/04/Richardson-microservices-part1-3_scale-cube.png)

### The bennefit of Microservices

1. Enforces a level of modularity
2. Be developed independently by a team that is focused on that service. The developers are free to choose whatever technologies make sense, provided that the service honors the API contract

## The drawbacks of Microservices

In a microservices‑based application, however, you need to update multiple databases owned by different services. Using distributed transactions is usually not an option, and not only because of the CAP theorem.
Chain of service dependance. 

## Building Microservices: Using an API Gateway

### Why API Gateway

### Benefit

![Encapsulate the interanl structure](https://cdn.wp.nginx.com/wp-content/uploads/2016/04/Richardson-microservices-part2-2_microservices-client.png)

### Drawback

The highly available component that must be developed, deployed, and managed.

## Building Microservices: Inter-Process Communication in a Microservices Architecture

### Interaction Category
x | One-to-One | One-to-Many
 ---|---|---
Synchronous |	Request/response |
Asynchronous | Notification	| Publish/subscribe
 x|Request/async response | Publish/async responses

Services Interactions
![Interaction](https://www.nginx.com/wp-content/uploads/2015/07/Richardson-microservices-part3_taxi-service.png)

Asychronous Communication
![Async](https://www.nginx.com/wp-content/uploads/2015/07/Richardson-microservices-part3_pub-sub-channels.png)

Synchronous Communicaiton
![Sync](https://www.nginx.com/wp-content/uploads/2015/07/Richardson-microservices-part3_rest.png)

## Service Discovery in a Microservices Architecture

Why - Look for service
![look for service](https://www.nginx.com/wp-content/uploads/2016/04/Richardson-microservices-part4-1_difficult-service-discovery.png)

1. Client site registry
2. Server site registry

## Event-Driven Data Management for Microservices

Why - Resolve the problem of distributed data management
![no shared database](https://cdn.wp.nginx.com/wp-content/uploads/2015/12/Richardson-microservices-part5-separate-tables-e1449727641793.png)

Use event to maintain materialized view that pre-join data owned by mulitple microservices.
![message broker](https://cdn.wp.nginx.com/wp-content/uploads/2015/12/Richardson-microservices-part5-subscribe-e1449727516992.png)

### Achieve Atomicity

1. Publishing event uing local transation
2. Mining database transaction log
3. Using Event Sourcing via event store
![Event Source](https://cdn.wp.nginx.com/wp-content/uploads/2015/12/Richardson-microservices-part5-event-sourcing-e1449711558668.png?_ga=2.85714576.866796380.1616939644-1644638523.1616770910)

## API Proxy vs API Gateway

> An API Proxy is the interface that developers use to access backend services. An API Proxy acts  as an intermediary. It makes requests on behalf of something else. service mesh is used alongside most of the service implementations as a sidecar and it’s independent of the business functionality of the services.
Both an API proxy and API gateway provide access to your backend services. An API gateway can even act as a simple API proxy. However, an API gateway has a more robust set of features — especially around security and monitoring — than an API proxy.
The key differentiators between API Gateways and service mesh is that API Gateways is a key part of exposing API/Edge services where service mesh is merely an inter-service communication infrastructure which doesn’t have any business notion of your solution.

![Proxy vs. Gateway](https://www.akana.com/sites/akana/files/image/2019-05/Gateway4-2.jpg)

API Gateway -> Composited Microservices -> Mesh -> Atomic Microservices
![](https://miro.medium.com/max/1000/1*JHrJe_8TO05wRQvwhwoKfA.png)

Reference Architecture
![](https://docs.microsoft.com/zh-tw/dotnet/architecture/microservices/multi-container-microservice-net-applications/media/implement-api-gateways-with-ocelot/eshoponcontainers-identity-service-position.png)
>**test**
>*test*

### Title 3

#### Title 4

* item 1
   1. test 1.1
   2. test 2.2
      * test 2.1
      * test 2.2
* item 2
* item 3

1. item 1
2. item 2
3. item 3

```javascript
function ToDoCtrl($scope) {
    $scope.totalTodos = 5;
}
```

[Google](http://google)

Name|Adress
--------|--------
xxx | xxx
xxx | sdfsdfsdfsdfsdf