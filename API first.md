API-First Design, in a nutshell, means that the API comes first then implementation. 
We believe that you’re much more likely to create something the client actually needs or wants with this approach — 
the mobile developers will likely be happy as well! As we are designing APIs we’re keeping Google’s API Design Guide nearby
for good REST API design reference.
So, yeah, we’re talking REST APIs.

Google API design guide - https://cloud.google.com/apis/design/

Since we’re practicing API-First design, let’s see a hypothetical example to get an idea of how this process might play out.

## The Setup
Here we are given client X’s first crack at a REST API for their…todo list application. Here are some of the resource paths:

The Setup
Here we are given client X’s first crack at a REST API for their…todo list application. Here are some of the resource paths:

/addNewTodoList
/getAllTodoLists
/updateTodoList/1
When we want to delete a list…?

/deleteTodoList/1
This is not looking too good, how about the remaining resource paths.

/addNewTodoListItem/1
/markComplete/1

Let’s whip out the Google Design Guide to see how we might handle this situation and we’ll find mention of a Resource-Oriented API.

A resource-oriented API is generally modeled as a resource hierarchy, where each node is either a simple resource
or a collection resource.

## Collections

/todo-lists
/todo-lists/1/items
Resources

/todo-lists/1
/todo-lists/1/items/1

This API won’t do very much (the verbs have been removed). This is where HTTP methods i.e. GET, POST, PUT and DELETE come into play.

Unormalized	|Normalized	|HTTP Method|
|/addNewTodoList -->|	/todo-lists|	POST|
|/getAllTodoLists	-->|/todo-lists|	GET|
|/updateTodoList/1	-->| /todo-lists/1|	PUT|
|/deleteTodoList/1	-->| /todo-lists/1|	DELETE|
|/addNewTodoListItem/1	-->| /todo-lists/1/items|	POST|
|/markComplete/1	-->|/todo-lists/1/items/1|	PATCH  with payload with status/details { "completed": true }|

## A Note On Validation
Dredd is a language-agnostic command-line tool for validating API description document against backend implementation of the API.

Once installed (with npm), validating an API is as simple as passing Dredd the API spec and the endpoint to validate:

$ dredd todo-list.apib http://127.0.0.1:8080
If everything passes, you will see some comforting output like so:

complete: 19 passing, 0 failing, 0 errors, 0 skipped, 19 total
However, if the server disobeys in the slightest:

complete: 18 passing, 1 failing, 0 errors, 0 skipped, 19 total

------------------------------------------------------------------------------------------------------
## https://medium.com/better-practices/api-first-software-development-for-modern-organizations-fdbfba9a66d3

The traditional code-first approach to app development sometimes results in delays, rework,
or a disjointed frankenstein-esque experience for the developer, especially in this cloud-driven landscape.

An API-first approach assumes the design and development of an application programming interface (API) comes before the implementation.
Your team begins by creating an interface for their application. 
After the API has been developed, the team will rely on this interface to build the rest of the application.

By introducing new features as an independent service accessed by API, the rest of the app can be stitched together, 
along with any other future apps.

## When the API comes first
With an API-first approach, instead of starting with code, you could start with design, planning, mocks, and tests.

By also separating the design of the API from its implementation, the architect is constrained only by the data model and business logic.
Your API can now evolve unfettered by any existing user interface or legacy engineering frameworks.

## API-first development
This concept refers to developing the actual API first and foremost. 
When you’re developing new functionality, the functionality should first be exposed as an API in your organization. 
The developers responsible for the rest of the application will be the first consumers of this API. 
This ensures the quality, predictability, and stability to withstand web clients, 
mobile users, and other developer consumers. 
Other projects requiring this functionality can now independently consume the functionality via this API.

## API-first design
This approach takes it a step further and requires planning the intended API’s functionality before building the API itself. 
What functionality will the API have? What data will it expose? 
What will the developer experience be like? How will it scale? How will we add new functionality in the future?

When people talk about API-first, sometimes they’re only referring to API-first development
and sometimes they’re including API-first design as well. For the remainder of this article,
API first will encompass both API-first development and API-first design.

## Why API first?
Clearly, pausing to flesh out the API delays valuable building time. 
Is it worth it? While not all organizations have the liberty to fully plan out their work, 
there are several benefits for choosing this approach that potentially outweigh delaying your time-to-market.

### Earlier validation: getting early feedback on the design allows the team to pivot or adapt to any new inputs 
while the cost of change is still relatively low.
This reduces overall cost over the lifetime of the project.

### Clear abstraction layer: showing only the necessary details to the intended user hides internal complexity. 
This allows others to ramp up more quickly when implementing the new service.

### Decoupling dependencies: by adhering to a contract between internal services, dependencies are decoupled
so that work can progress independent of other teams’ work. Working in parallel minimizes the project’s overall development time.

### Faster growth: building out the API design at an early stage takes future functionality into account, laying the groundwork
for expansion, and accommodates the ability to quickly scale to other apps, devices, and platforms.

### Freedom from constraints: focusing first on the API instead of the code and implementation frees the design from legacy constraints.

Instead, let’s walk through an API-first approach, and learn about one way to build a new product or feature in Postman.

Design the new feature
Get feedback about the new feature
Build the feature
Deploy the changes

Refer link for example using postman -> https://medium.com/better-practices/api-first-software-development-for-modern-organizations-fdbfba9a66d3
-------------------------------------------------------------------------------------------------------------









