# Routing

![routing](./images/routing.png)

# WebSequenceDiagrams

Paste the following text in [WebSequenceDiagrams](https://www.websequencediagrams.com/)

```
title React Starter Kit

Client->Browser: Initial page request ( / )
Browser->Server: HTTP request ( / ) to server.js
note right of Server : Server includes the ContentApi route
note left of Browser : Page is loaded from bookmark / new browser window
Server->React-Routing: Dispatches a path ( / )
React-Routing->ContentApi: Fetch the jade template from content server
note left of ContentApi: (fetchess jade tempate because no index component found)
React-Routing->React-Routing: Wrap the generated Jade HTML in a ContentPage component
React-Routing->Server: returns state and component
note left of Server: Server renders the ReactJS component
Server->Browser : write the rendered component to the response
Browser->Client: Index page is shown


Client->Browser: Load a component URL ( /contactPage)
note left of Browser : Page is loaded from bookmark / new browser window
Browser->Server: HTTP request ( /contactPage ) to server
Server->React-Routing: Dispatches a path ( /contactPage )
React-Routing->React-Routing: Fetch the ReactJS component associated with route
note right of React-Routing: (finds a ReactJS component so no jade template needed)
React-Routing->Server: returns state and component
note left of Server: Server renders the ReactJS component
Server->Browser : write the rendered component to the response
Browser->Client: contactPage page is shown

Client->Browser: Load a page URL ( /about)
note left of Browser : Page is loaded from bookmark / new browser window
Browser->Server: HTTP request ( /page ) to server
Server->React-Routing: Dispatches a path ( /page )
React-Routing->ContentApi: Fetch the jade template from content server
note left of ContentApi: (jade tempate used because no index component found)
React-Routing->Server: returns state and component
note left of Server: Server renders the ReactJS component
Server->Browser : write the rendered component to the response
Browser->Client: about page is shown


Client->Browser: Javascript function ( /about)
note left of Browser : Page is loaded via javascript (onClick)
Browser->React-Routing: Dispatches a path ( /page )
React-Routing->React-Routing: Fetch the ReactJS component associated with route
note left of Server: Server is bypassed completely
React-Routing->Browser: returns state and component
Browser->Browser: about component is rendered
note left of Browser: Browser renders the component
Browser->Client: about page is shown
```
