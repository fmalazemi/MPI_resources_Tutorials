# Client 
  - Using MPI (or any other framework), the client look for a server. 
  - Once a server is found, open a channel and then:
    - Send modules need to be executed (each module through seperate MPI send/recv, maybe?). 
    - Inform Server about data location (or send data?) . 
    - How Client will recieve the output? I don't know
  - If data is received to client then we need to store data. 
  - Are we done? Closed the MPI channel
# Server
  - Start
  - Publish  
  - wait for Clients to connect
  - Once a client is connected 
    - Wait for list of module and data
    - For each module spwan a seperate process in the server that loads data and executes the module
    - Send output back to client (or store in a database?) 
    - Close connection
  - Wait for another client. 






