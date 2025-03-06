# Results

## Running `curl -I` on Main Page

```sh
curl -I https://gwenhey.github.io/Knowledge_graphs/
```

### **Response:**
```
HTTP/1.1 200 OK
Connection: keep-alive
Content-Length: 1695
Server: GitHub.com
Content-Type: text/html; charset=utf-8
permissions-policy: interest-cohort=()
Last-Modified: Thu, 06 Mar 2025 20:42:57 GMT
Access-Control-Allow-Origin: *
Strict-Transport-Security: max-age=31556952
ETag: "67ca08d1-69f"
expires: Thu, 06 Mar 2025 20:53:28 GMT
Cache-Control: max-age=600
x-proxy-cache: MISS
X-GitHub-Request-Id: 4FF4:15FAC5:5F001F:5FB288:67CA08EF
Accept-Ranges: bytes
Age: 0
Date: Thu, 06 Mar 2025 20:43:28 GMT
Via: 1.1 varnish
X-Served-By: cache-bru1480028-BRU
X-Cache: MISS
X-Cache-Hits: 0
X-Timer: S1741293808.435753,VS0,VE111
Vary: Accept-Encoding
X-Fastly-Request-ID: d5a731bec461438f974dfe0ee59cc88ca14a3a6f
```

Here we see that the page loads successfully. However, the Vary indicates that it only supports compression but does not support content negotiation.

Since I published my data using GitHub Pages, the server does not allow content negotiation for different RDF representations. This means that even if a client requests RDF (e.g., Turtle or JSON-LD), the server will always respond with HTML.

## Running `curl -I -H "Accept: text/turtle"` to Request Turtle Content

```sh
curl -ILH "Accept: text/turtle" https://gwenhey.github.io/Knowledge_graphs/
```

### **Response:**
```
HTTP/1.1 200 OK
Connection: keep-alive
Content-Length: 1695
Server: GitHub.com
Content-Type: text/html; charset=utf-8
permissions-policy: interest-cohort=()
Last-Modified: Thu, 06 Mar 2025 20:42:57 GMT
Access-Control-Allow-Origin: *
Strict-Transport-Security: max-age=31556952
ETag: "67ca08d1-69f"
expires: Thu, 06 Mar 2025 21:28:49 GMT
Cache-Control: max-age=600
x-proxy-cache: MISS
X-GitHub-Request-Id: A3D0:949A5:6F66F1:7033D4:67CA1139
Accept-Ranges: bytes
Age: 0
Date: Thu, 06 Mar 2025 21:18:49 GMT
Via: 1.1 varnish
X-Served-By: cache-bru1480027-BRU
X-Cache: MISS
X-Cache-Hits: 0
X-Timer: S1741295930.856676,VS0,VE117
Vary: Accept-Encoding
X-Fastly-Request-ID: adc57a7550858bbbd34e76ec8006b366a9ac0720
```

Here we see that the response is still HTML.

If a client wants to retrieve the RDF data, they must request the files directly. The links are provided on the main HTML page:

- **Turtle File**: [https://gwenhey.github.io/Knowledge_graphs/gwendolyn.ttl](https://gwenhey.github.io/Knowledge_graphs/gwendolyn.ttl)
- **JSON-LD File**: [https://gwenhey.github.io/Knowledge_graphs/gwendolyn.jsonld](https://gwenhey.github.io/Knowledge_graphs/gwendolyn.jsonld)

---

## Requesting Turtle and JSON-LD Directly

If we request the Turtle file directly, we get the correct response:


```sh
curl -I https://gwenhey.github.io/Knowledge_graphs/gwendolyn.ttl
```
### **Response:**
```
HTTP/1.1 200 OK
Connection: keep-alive
Content-Length: 761
Server: GitHub.com
Content-Type: text/turtle; charset=utf-8
permissions-policy: interest-cohort=()
Last-Modified: Thu, 06 Mar 2025 20:42:57 GMT
Access-Control-Allow-Origin: *
Strict-Transport-Security: max-age=31556952
ETag: "67ca08d1-2f9"
expires: Thu, 06 Mar 2025 21:34:17 GMT
Cache-Control: max-age=600
x-proxy-cache: MISS
X-GitHub-Request-Id: 6E9B:B7347:71C991:729B1C:67CA127D
Accept-Ranges: bytes
Age: 0
Date: Thu, 06 Mar 2025 21:24:17 GMT
Via: 1.1 varnish
X-Served-By: cache-bru1480050-BRU
X-Cache: MISS
X-Cache-Hits: 0
X-Timer: S1741296257.021199,VS0,VE109
Vary: Accept-Encoding
X-Fastly-Request-ID: b79a71a114aa59b0b79c673c0c79a04bb5aa9611
```

The `Content-Type` is now correctly set to `text/turtle`, confirming that the RDF file is accessible when explicitly requested.

The same goes for the JSON-LD file.