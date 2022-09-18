# Design patterns  

[Design patterns](https://refactoring.guru/design-patterns/catalog)  
[Learning JavaScript Design Patterns](https://www.patterns.dev/posts/classic-design-patterns/) 

<details>
<summary>Structural</summary>

Structural patterns are concerned with **object composition** and typically identify simple ways to realize **relationships between different objects**. They help ensure that when one part of a system changes, the entire structure of the system doesn't need to do the same. They also assist in recasting parts of the system which don't fit a particular purpose into those that do.

**Adapter**   
Allows **objects with incompatible interfaces to collaborate**. Adapter is a special object that converts the interface of one object so that another object can understand it. An adapter wraps one of the objects to hide the complexity of conversion happening behind the scenes. The wrapped object isn’t even aware of the adapter. Adapter can also help objects with different interfaces collaborate. Here’s how it works:   

1) The adapter gets an interface, compatible with one of the existing objects.    
2) Using this interface, the existing object can safely call the adapter’s methods.   
3) Upon receiving a call, the adapter passes the request to the second object, but in a format and order that the second object expects.

The client code doesn’t get coupled to the concrete adapter class as long as it works with the adapter via the client interface. Thanks to this, you can introduce new types of adapters into the program without breaking the existing client code. This can be useful when the interface of the service class gets changed or replaced: you can just create a new adapter class without changing the client code.

-  Use the Adapter class when you want to use some existing class, but its interface isn’t compatible with the rest of your code.

- Use when you want to reuse several existing subclasses that lack some common functionality that can’t be added to the superclass. Wrap objects with missing features inside the adapter, gaining needed features dynamically. For this to work, the target classes must have a common interface, and the adapter’s field should follow that interface.

Single Responsibility, Open/Closed

**Decorator**
It lets you **attach new behaviors** to objects by placing these objects inside special wrapper objects that contain the behaviors.   
“Wrapper” is the alternative nickname for the Decorator pattern that clearly expresses the main idea of the pattern. A wrapper is an object that can be linked with some target object. The wrapper contains the same set of methods as the target and delegates to it all requests it receives. However, the wrapper may **alter the result by doing something either before or after it passes the request to the target**.

- Use when you need to be able to assign extra behaviors/functionality to objects at runtime without breaking the code that uses these objects.   
- Use when it’s awkward or not possible to extend an object’s behavior using inheritance.

```

class Server {
  constructor(ip, port) {
    this.ip = ip
    this.port = port
  }

  get url() {
    return `https://${this.ip}:${this.port}`
  }
}

function aws(server) {
  server.isAWS = true
  server.awsInfo = function() {
    return server.url
  }
  return server
}

function azure(server) {
  server.isAzure = true
  server.port += 500
  return server
}

const s1 = aws(new Server('12.34.56.78', 8080))
console.log(s1.isAWS)
console.log(s1.awsInfo())

const s2 = azure(new Server('98.87.76.12', 1000))
console.log(s2.isAzure)
console.log(s2.url)
```

</details>