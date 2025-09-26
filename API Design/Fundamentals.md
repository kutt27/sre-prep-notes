# 1. Fundamentals of API Design: What is an API?

## 1.1 Definition

**API** stands for **Application Programming Interface**.

An API is fundamentally **a contract that defines how software components should interact** with each other. It is the intermediary that allows two separate software systems to communicate.
## 1.2 The API as a Contract

The API defines a clear, stable, and predictable **contract** between the **Client** (the requester) and the **Server** (the provider of the service).

This contract specifies three core aspects:

1. **What requests can be made:** The available operations (e.g., Get data, Create a resource).
2. **How to make them:** The necessary format, parameters, and protocol (e.g., specific HTTP methods, URL paths, headers).
3. **What responses to expect:** The format of the data that will be returned, including status codes (e.g., success, error) and the structure of the data payload.

## 1.3 Communication Flow

The interaction between the Client and Server follows a clear cycle:

1. **Client → Server:** The Client sends a **Request** based on the rules defined in the API contract.    
2. **Server → Client:** The Server processes the request and sends back a **Response**, adhering to the expected response format in the API contract.

## 1.4 Key Characteristics for Engineers

For a truly effective and deep understanding, an engineer must grasp the two primary characteristics an API provides:

|Characteristic|Description|Significance for Design|
|---|---|---|
|**Abstraction Mechanism**|Hides the complex, underlying implementation details of the Server while exposing only the necessary functionality to the Client.|Allows the Server team to change their internal logic (e.g., switch databases, refactor code) without breaking the Client, as long as the external API contract remains stable.|
|**Service Boundaries**|Defines clear, hard interfaces between different components or systems.|Promotes **Modularity** and **Decoupling**. It makes systems easier to build, test, deploy, and scale independently (a core principle of microservices).|

---
[[Core API Styles]]