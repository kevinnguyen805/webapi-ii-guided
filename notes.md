# Routing Notes 

[client] == makes a request to an [api] == sends a response back to the == [client]

What is the interface for a web API? 
- URI (uniform resource identifier)
- URL (universal resource locator)
- Endpoint (very related to a URI - ROUTES that point to a resource)
- HTTP === network protocol, a set rules for communication (medium of communication)


REST-ish web API  
- everything is a `Resource` 
- Think about the architecture of your application(?)
- Guidelines to REST
     1. everything is a resource. (nouns to a system/application)
          if we were building an API for slack- we would have to manage avatars, messages, threads, channels => 
     2. each resource is accessible via a unique URI.
          single URI per resource (which is why we have IDs in our URL)
          ex: `http:link/users` & `http:link/channel`
          every interaction should happen through a URL we identify our resrouce as 
     3. resources can have multiple representations.
     4. communication is done over a stateless protocol (HTTP).
          * Use HTTP METHODS to express the actions the client can perform
          * EXTREMELY IMPORTANT ONE!!!!!!!!!!!!!!!!!!!
          * URL is always the same, but the difference is we're expressing different actions through different HTTP METHODS
          * NONREST - /listallchannels /createChannel / updateChannel /deleteChannel / findchannel?id=123
          * REST - /GET /channels       POST /channels        PUT /channels      DELETE /channels      GET /channels/123
     5. management of resources is done via HTTP methods.


Restraints to Restraintsclient-server architecture.
stateless architecture: each request should stand on it’s own, and order should not matter. No shared state.
cacheable: improves network performance.
GET, PUT, DELETE should be idempotent (same command executed multiple times, the state of resources on the server is exactly the same, much like pure functions)
POST is not idempotent.
caching is a way to store and retrieve data so that future requests can be fulfilled faster without re-perfoming expensive calculations or operations.
layered system: component A (a client) might or might not communicate directly with component B (the server). There may be other layers between them like logging, caching, DNS servers, load balancers, authentication, etc.
code on demand
the API returns the resource and code to act on it.
the Client only needs to know how to execute the code.
makes the API more flexible, upgradable and extendible.
most web application, send JavaScript code along with the data.
uniform interfaces
each resource should be accesible through a single url. Not a hard requirement, but recommended.
we should be able to manage the resources through these representations (the URL).
every interaction with the resource should happen through the URL identifier we gave to it.
self descriptive messages.
HATEOAS (Hyepermedia As The Engine Of Application State). Much like a choose your own adventure book, the pages are not read in order. You start at page 1 and based on the information available the reader (client) chooses the action to take and that will take them to a different page. A good example of a hypermedia API is the GitHub API.
1. client-server architecture
2. stateless architecture - there is no shared memory on the server - everything is connected (no shared state)
3. acheable - 


Starting guided project
-> npm run server
-> go to POSTMAN -> GET localhost:4000/api/hubs 
-> POST request
     1. body raw + json
     2. {
          "name": "web23"      <-- must be in double quotes!!!!
     }


****** IMPORTANT!!!!!!! 
Routing - takes a particular URI and ties it to some code to execute 

****** IMPORTANT!!!!!!
2 conditions for routing engine to make its magic (VIA REQUEST/ROUTE HANDLER!!!!!!)
1. URI 
2. HTTP Method (from database!)


***** IMPORTANT!!!!!!!
SUB-ROUTING => resource belonging in something else (messages within a channel)
Example:
     /channel/messages      <- points to the messages in a channel (resource within a resource)

****** Users endpoint
     * You always need to start a API link with `/api/`
server.get('/api/hubs/:id/messages', (req, res)=> {})
     1. get to the hub (main/root resource)
     2. pass in an ID (get to a particular hub)
     3. now get the messages within that (particular) hub

* server.post('/api/hubs/:id/messages',(req,res) => {
     ///// const hubId = req.params.id;

     const message = {...req.body, hubId: req.params.id }    <-- explicitly adding an ID (identifiable with the user) to the user object along with text on request body object
})





///////////////////////////////////////////////

EXPRESS ROUTER
1. you need to bring in something from express 
* FILE: hubs-router.js
const router = require('express').Router()

2. export your Express Router so you can use it in your MAIN INDEX.JS FILE
* FILE: hubs-router.js
* REMEMBER TO USE THE "S"
* similar to => export default router; (ES Modules)


3. import into MAIN INDEX.JS file
const HubsRouter = require('./hubs/hubs-router.js')           <-- importing the file 
server.use('api/hubs', hubsRouter)                            <-- main server file setting up the Router to the file 


****** THNGS TO NOTICE 
- router.get('', (req,res) => {})     <- router.get not server.get
- you're importing your database to the ROUTER PAGE not the MAIN PAGE!!!
- remember to change the URLS to '/' as the root of the link you're managing 

- A router can have route/request handlers and middleware 


////


URL QUERY STRING PARAMETER - key value pairs!!! 
What is a Query String?
starts with ? 
     q = express+js
     &
     oq = express+js 
     & 
     aqs = chrome....=chrome 
     & 
     ie = UTF-8
YOU'RE RESPONSIBLE FOR CREATING THIS QUERY STRING!
- Node can read the query string and extract it out - parse it - and give you back a nice object 
- read as:
     req.query = {
          q: 'express+js',
          oq: 'express+js',
          ie: 'UTF-8'
     }


     router.get('/', (req, res) => {
          const query = req.query;

          
     })