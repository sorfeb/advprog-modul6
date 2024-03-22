# Commit 1 Reflection notes
> What is inside the
`handle_connection` method?
> 
This method handles how the server will
behave when it receives a connection request from a browser.
1. It takes a mutable reference `TcpStream` called `stream` as its parameter.
2. The `buf_reader` reference is a `BufReader` wrapping the `TcpStream` that is used for I/O of String data
3. `buf_reader` reads lines from the buffered stream. 
4. The `take_while` function is used to stop reading once an empty line is reached.
5. It collects the lines of String into a vector named `http_request`.
6. Then, it prints out `"Request: {:#?}", http_request`




