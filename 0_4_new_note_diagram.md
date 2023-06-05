Sequence diagram on creating a new note on the page https://studies.cs.helsinki.fi/exampleapp/notes

```mermaid
sequenceDiagram
participant browser
participant server

browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note HTML Payload: Form data
loop ServerSide 
    server->>server: Server gets access to the data via request objects body field. <br> Then server processes it with python or similar back-end language. <br> In this case it is appended to the JSON which is later passed on to the browser.
end
activate server
server-->>browser: Status Code 302, URL redirect
deactivate server
loop BrowserSide
    browser->browser: Browser gets redirected and <br> reloads the /notes page.
end

browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
activate server
server-->>browser: HTML document
deactivate server

browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
activate server
server-->>browser: the css file
deactivate server

browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
activate server
server-->>browser: the JavaScript file
deactivate server

Note right of browser: The browser starts executing the JavaScript code that fetches the JSON from the server

browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
activate server
server-->>browser: [{content: "Hello", date: "2023-06-01T04:36:50828Z"},…]
deactivate server
Note right of browser: The browser executes the callback function that renders the notes
```