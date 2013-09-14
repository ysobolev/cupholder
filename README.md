cupholder
=========

*cupholder - because that's where you place your coffee while riding the autobahn*

A simple coffeescript WAMP client.

Here is some example code
    
    wamp = require "cupholder"

    client = new wamp.Client "ws://localhost:9000/", debug=true
    client.on "error", (e) -> console.error e
    client.on "open", () ->
        console.log "session opened"
        promise = client.authenticate "username", "password"
        promise.then (result) ->
            console.log "authenticated"
            client.subscribe "http://example.com/feed"
            client.publish "http://example.com/comments", "hi", excludeMe=false
        , (error) ->
            console.error error[1]

    client.on "close", () ->
        console.log "session closed"

    client.on "event", (uri, event) ->
        console.log uri, event

