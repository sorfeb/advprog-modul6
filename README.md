# Commit 1 Reflection notes
> What is inside the `handle_connection` method?

This method handles how the server will
behave when it receives a connection request from a browser.
1. It takes a mutable binding ****`TcpStream` called `stream`**** as its parameter.
2. The `buf_reader` binding is a `BufReader` wrapping the `TcpStream` that is used for ****I/O reading of String data****
3. `buf_reader` reads lines from the buffered stream. 
4. The `take_while` function is used to stop reading once an empty line is reached.
5. It collects the lines of String into a vector named `http_request`.
6. Then, it prints out `"Request: {:#?}", http_request`

# Commit 2 Reflection notes
![image](https://github.com/sorfeb/advprog-modul6/assets/112263712/cf8a3013-0cb3-480c-8fd5-ab7b0da724a8)
> What is inside the NEW `handle_connection` method?
1. `status_line` binding prepares an HTTP response to send back to the client. The response includes a status line indicating **"HTTP/1.1 200 OK"**. This means the request was successful.
2. `contents` binding reads the content of `hello.html` into a string variable named contents using `fs::read_to_string`. The server intends to send back the file contents to the client.
3. `response` binding constructs the complete response by formatting the **status line**, **content length**, and **actual contents** of the file into a single string using `format!` macro.
4. `stream.write_all(response.as_bytes()).unwrap();` writes the response to the `TcpStream` by converting it to bytes and using `write_all` method.

# Commit 3 Reflection notes
![image](https://github.com/sorfeb/advprog-modul6/assets/112263712/9c8b5f40-3127-4de4-a67c-fc6112f021b5)
> How to split between response and why the refactoring is needed.

The `if-else` statement that checks the request to `GET / HTTP/1.1`:
- It will show `hello.html` if response to request = `HTTP/1.1 200 OK`
- It will show `404.html` if response to request = `HTTP/1.1 404 NOT FOUND`

Refactoring is needed to make the code more concise by pulling out those differences into separate `if` and `else` lines that will assign the values of the `status_line` and the `filename` to variables. We can then use those variables unconditionally in the code to read the file and write the response and makes it easier to see the difference between the two cases, and it means we have only one place to update the code if we want to change how the file reading and response writing work.

# Commit 4 Reflection notes
> Let’s open two of browser windows, try `127.0.0.1/sleep` in one of them, and try in other
windows `127.0.0.1`. Pay attention that the browser take some time to load. You can imagine if many users try to access it.
See how it works and try to understand why it works like that.

When we try to access the `/sleep` endpoint, the new `handle_connection` function sleeps for 10 seconds 
, which delays processing the request.
The function doesn't use multithreading, causing `/` requests to be blocked until the `/sleep` request is processed.