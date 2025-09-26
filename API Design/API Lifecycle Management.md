# 7. API Lifecycle Management & Network Stack Context

## 7.1 API Lifecycle Management

An API is a product with a finite life that requires continuous management to maintain quality and backward compatibility.

|Phase|Description|Key Focus|
|---|---|---|
|**Design**|Creating the contract, defining use cases, and establishing security and performance requirements.|**Contract-First mentality.**|
|**Development**|Implementation of the API logic based on the approved contract.|**Testing** (unit, integration, acceptance).|
|**Deployment & Monitoring**|Making the API live and continuously tracking its performance, availability, and errors.|**SLO/SLA** adherence and **Observability** (logging, metrics, tracing).|
|**Maintenance**|Fixing bugs, adding minor features, and ensuring continuous security patching.|**Backward Compatibility** and **Stability**.|
|**Deprecation & Retirement**|Phasing out old versions of the API to encourage adoption of new ones before finally removing the old interface.|**Communication** with clients and clear **Versioning** strategy.|

## 7.2 Application Protocols in the Network Stack

APIs primarily operate at the **Application Layer** (Layer 7 of the OSI Model), leveraging the lower layers for actual data transmission.

|OSI Layer|Protocol Examples|API Relevance|
|---|---|---|
|**Application Layer** (L7)|HTTP/HTTPS, WebSockets, gRPC, MQTT, AMQP|**API Focus.** This layer defines the data format and communication rules (the "protocol") the API uses.|
|**Transport Layer** (L4)|TCP (Transmission Control Protocol), UDP (User Datagram Protocol)|**Reliability & Order.** APIs typically run over **TCP** for reliable, ordered, and error-checked delivery (e.g., HTTP).|
|**Network Layer** (L3)|IP (IPv4/IPv6)|**Addressing.** Ensures data packets are routed to the correct destination host.|
|**Data Link Layer** (L2)|Ethernet, Wi-Fi|**Local Delivery.** Handles data transfer between adjacent network nodes.|
|**Physical Layer** (L1)|Copper wire, Fiber optics, Radio waves|**Raw Transmission.** The hardware medium of communication.|

---

[[HTTPS]]