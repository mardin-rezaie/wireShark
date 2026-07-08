# Project 2 — Web Protocol Stack Analysis with curl and Wireshark

## Responsibility Matrix

|Full Name|Student ID|Section Completed|
|-|-|-|
|Mardin Rezaie|40217023136|Phase 1, Phase 2, Phase 3|

---

## Team Information

|First Name|Last Name|Student ID|Role|
|-|-|-|-|
|Mardin|Rezaie|40217023136|Packet capture, header analysis, RTT analysis, and documentation|

---

## Step-by-Step Report

### Phase 1: Environment Setup and Packet Capture

In this phase, Wireshark was opened and the active network interface (Wi-Fi/Ethernet) was selected. Packet capture was then started, and immediately after starting the capture, the following command was executed in the terminal:

```
curl http://neverssl.com
```

This site was specifically chosen because it never redirects traffic to HTTPS, which allows the HTTP headers to be fully visible and readable in Wireshark.

After the complete response was received in the terminal, the capture was stopped and the final file was saved in `.pcapng` format under the `captures/` directory.

---

### Phase 2: Header Dissection and Protocol Stack

By applying the `http` filter in the Wireshark filter bar, the GET request packet was identified. The information extracted from the three protocol layers is as follows:

**Layer 7 — Application (HTTP):**

* Host: `neverssl.com`
* Protocol Version: `HTTP/1.1`
* User-Agent: curl/8.19.0\\r\\n

**Layer 4 — Transport (TCP):**

* Source Port: 56730
* Destination Port: `80`
* Transport Layer Protocol: TCP

**Layer 3 — Network (IP):**

* Source IP: 192.168.167.222
* Destination IP: 34.223.124.45

> !\[alt text](./screenshots/2-1.png)

> !\[alt text](./screenshots/2-2.png)

> !\[alt text](./screenshots/2-3.png)



---

### Phase 3: Server Behavior and RTT Timing Analysis

The server response packet was identified using the `http` filter. Extracted information:

**Status Code:** `200 OK`

The `200 OK` status code received in the server's response belongs to the successful (2xx) category of HTTP status codes and indicates that the client's GET request was received and processed by the server without any errors or issues. This code means that the requested resource — in this case, the home page of `neverssl.com` — was successfully found on the server, and its content was fully returned in the response body to the client. Unlike codes such as `404`, which indicates that a resource was not found, or `301/302`, which indicates a redirect to another address, receiving a `200` confirms that the request-response cycle completed without any deviation or error, and the client received exactly the content it requested.

**Time Delta:** `255.0982 milliseconds (0.2550982 seconds)`

**Latency Analysis Paragraph:**

In this session, the server responded to the GET request with a `200 OK` status code, indicating successful delivery of the requested content without any errors or redirects. The Time Delta between sending the GET request and receiving this response was 0.2550982 seconds (255.0982 milliseconds), a value that is quite low and falls within the normal range for a healthy HTTP connection. If this value had exceeded the 2-second threshold, there would have been three likely sources of the delay: (1) network latency between the client and server, caused by long routing paths or bandwidth congestion; (2) heavy processing on the server side, such as expensive database queries or high application load; or (3) resource constraints on the client side. Given that in our actual session the server responded with a successful 200 code in under one-third of a second, it can be concluded that neither the network nor the server experienced any performance issues, and the connection was in an excellent state in terms of latency.

> !\[alt text](./screenshots/3-1.png)

> !\[alt text](./screenshots/3-3.png)



---

## Appendices

The actual capture file for this session is located at:

```
captures/1.pcapng
```

---



