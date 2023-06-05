Sequence diagram on creating a new note on the single-app page at https://studies.cs.helsinki.fi/exampleapp/spa


```mermaid
sequenceDiagram
participant browser
participant server

loop Browser form.onsubmit 
    browser->>browser: Javascript code fetched from server before runs. It <br>fetches the form element from the page and registers event handler for <br>it. Then it creates a new node and adds it to notes list with push <br>comman, rerenders the notes and then sends the new note to the server.
end
browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note Payload: Content-Type: application/json
loop ServerSide 
    server->>server: Server receives the JSON data and processes it.
end



```