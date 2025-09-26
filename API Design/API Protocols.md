# 5. API Protocols and Their Influence on Design

The choice of underlying communication protocol fundamentally shapes the available API design options, performance characteristics, and overall system capabilities. The API design must accommodate the protocol's limitations and, more importantly, leverage its strengths.

## 5.1 Key Protocols and Their Influence

|Protocol|Description|Influence on API Design|Associated API Style|
|---|---|---|---|
|**HTTP (Hypertext Transfer Protocol)**|The foundation of the web. It is a text-based, request-response protocol, typically running over TCP/IP. It is inherently **stateless**.|Enables **RESTful APIs** by providing verbs (methods like GET, POST) and resources (URLs). Its stateless nature forces the API design to be self-contained and idempotent where possible.|REST, GraphQL (which runs _over_ HTTP)|
|**Status Codes**|A critical component of the HTTP protocol. Three-digit codes (e.g., 200, 404, 500) that convey the result and semantic meaning of a server's response.|Essential for **Developer Experience (DX)**. A good API design _must_ map operations clearly to the appropriate status codes (e.g., 201 for resource creation, 400 for bad request).|REST, GraphQL|
|**WebSockets**|A full-duplex communication protocol providing persistent, two-way communication channels over a single TCP connection.|Enables **Real-time APIs** and **Streaming**. Used for features like live updates, chat, and subscriptions where the server needs to push data to the client without a continuous client request.|Real-time APIs, GraphQL Subscriptions|
|**gRPC**|A modern, high-performance RPC framework developed by Google. It uses HTTP/2 for transport and Protocol Buffers for data serialization.|Enables **Efficient Microservice Communication**. Its use of binary data and HTTP/2 features (like multiplexing and server push) results in significantly higher performance and lower latency compared to standard JSON/HTTP APIs.|gRPC|

## 5.2 Key Design Considerations

- **Protocol Choice Affects Structure, Performance, and Capabilities:**
    - **Structure:** HTTP enforces a request/response structure. WebSockets allow for persistent, stream-based structure.
    - **Performance:** Binary protocols (like gRPC/Protocol Buffers) are faster and smaller than text-based protocols (like JSON/HTTP).
    - **Capabilities:** Only protocols like WebSockets allow for server-side push (real-time).
        
- **API Design Must Accommodate Protocol Limitations and Leverage Strengths:**
    - When using **HTTP (REST)**, you must leverage built-in features like **caching headers** and **status codes**.
    - When using **gRPC**, you leverage its **schema-first design** and **streaming capabilities** for efficient service-to-service communication.

---

[[API Design Process]]