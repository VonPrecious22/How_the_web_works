1. URL Parsing.
        When a user type a url for example https://example.come in the browser and press enter, the browser tries to understand the various components which are:
        -Protocol(https): stands for hyper text tranfer protocol secure. it's therefor set of rules that govern the communication between the client and the server.
        -Host(example.com): stands for the domain name of the targeted server.
        -Port(443):The network port for the https traffic.
        -Path: The specific resource that is being requested.
2. DNS Lookup.
        The browser translate the human friendly domain name(example.com) into an IP Address and therefor allocate the server.
3. TCP Connection. 
        -With the IP address known, the browser innitial a TCP(Transfer Control Protocol) connection with the server. The TCP protocol therefor garantees reliable and order delivery. 
4. TLS/SSL Handshake.
       Because the URL uses the https://, the connection is being encrypted. This is being done through the TLS(The Transport Layer Security) handshake which occur through the TCP.
       -During this process, the server and the browser agrees on a mutual TLS supported version.
       -They both agree on an encrypted algorithms and the decyption and encrypted keys.
       -The server present the SSL/TLS certiface aand the browser validates it.  
       -All this therefor makes the connection to be a secure tunnel. Even if it is intercepted, the data therefor becomes unreadable without a session key. 
5.  HTTP Request.
        with a secure connection the browser contruct and send an http request to the server. the request structure are as follows
        -GET/HTTP/1.1. Http method(GET), Path(/), HTTP Version(1.1)
        -Host Header. Required in HTTP/1.1; allows multiple domain on one IP.
        -User-Agent. Identify the browser and operating system to the server.
        -Accept. Tell the server what content type the server can handle. 
        -Accept-Encoding. Support Compression formats(gzip, brotli) to reduce tranfer size.
        -Connection. keep-alive allow reusing the TCP connection for subsequent request.

        When the page load, the browser uses the GET method to retrieve resource from the server.
6. Server Processing.
        -The HTTP request travel accross the internet throuth routers and untill it reaches the web server hosting for e.g example.com.
        -The processing steps for example.com are:
        -Request Routing: The web server determines which application handler should process the request for path / 
        -Authentication Check: If the page requires login, the server validates session cookies or JWT tokens.
        -Business Logic: The application executes code to generate or retrieve content. For a static site like example.com , this may simply read a file from disk.
        -Database Queries: If dynamic, the app queries a database (e.g., PostgreSQL,MongoDB) for content.
        -Template Rendering: The application injects data into an HTML template.
        -Response Preparation: The server constructs the HTTP response with appropriate headers and body.
7. HTTPS Response.
        The server send the HTTP response back through the same secure TLS tunnel.
        -The HTTP respose structure is as follows. 
        HTTP/1.1 200 OK
        Age: 587053
        Cache-Control: max-age=604800
        Content-Type: text/html; charset=UTF-8
        Date: Mon, 16 Aug 2026 18:40:00 GMT
        Etag: "3147526947+ident"
        Expires: Mon, 23 Aug 2026 18:40:00 GMT
        Last-Modified: Thu, 17 Oct 2019 07:18:26 GMT
        Server: ECS (nyb/1XXX)
        Vary: Accept-Encoding
        X-Cache: HIT
        Content-Length: 1256
        <!doctype html>
        <html>
        <head>
        <title>Example Domain</title>
        ...
        </head>
        <body>
        7
        <div>
        <h1>Example Domain</h1>
        <p>This domain is for use in illustrative examples in documents...</p>
        </div>
        </body>
        </html>
8. Browser Rendering.
       -The browser received the HTML response and begins the process of converting it into a visual webpage. 
        1. HTML Parsing → DOM Construction
        -The browser's HTML parser tokenizes the raw HTML into tags, attributes, and text.
        -It builds the DOM (Document Object Model) — a tree structure representing the
        document.
        -If the parser encounters <script> tags without defer or async, it blocks parsing
        to execute the JavaScript immediately.
        2. CSS Parsing → CSSOM Construction
        -The browser fetches linked CSS files (<link rel="stylesheet">).
        -It parses CSS rules and builds the CSSOM (CSS Object Model) — a tree of style
        rules.
        -CSS is render-blocking: the browser waits for all CSS before rendering anything.
        3. JavaScript Execution
        -JavaScript can modify both the DOM and CSSOM.
        -Scripts are executed in the order they appear (unless async or 
        defer is used).
        -JavaScript is parser-blocking by default.
        4. Render Tree Construction 
        -The browser combines the DOM and CSSOM to create the Render Tree.
        -Only visible elements are included (display: none elements are excluded; visibility: hidden elements are included but marked invisible).
        5. Layout (Reflow)
        -The browser calculates the exact position and size of every element in the Render Tree.
        -This process is also called reflow.
        -Layout is computationally expensive and triggered by changes to element geometry.
        6. Paint 
        - The browser fills in pixels — text, colors, images, borders, shadows.
        - Painting occurs in multiple layers (e.g., separate layers for video elements or elements with transform).
        7. Composite
        -The browser combines all layers into the final image displayed on screen.
        -Layers that don't affect each other can be composited independently, improving
        performance.
9. Post-Render and Cleanup.
        The web page now becomes vissible but the browser keeps working in the background.
        



