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

