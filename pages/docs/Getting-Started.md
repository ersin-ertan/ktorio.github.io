---
title: Getting Started
tags: [overview]
sidebar: mydoc_sidebar
permalink: getting-started.html
summary: Describes the bare minimum of what a Ktor Application is
---

## Creating a Ktor Application

This tutorial will guide you through the steps on how to create a simple self-hosted Ktor Application that responds to HTTP requests with `Hello, World!`.
Ktor applications can be built using common build systems such as [Maven](https://kotlinlang.org/docs/reference/using-maven.html) or [Gradle](https://kotlinlang.org/docs/reference/using-gradle.html).

### Including the right dependencies

Ktor is split up into several groups of modules, allowing us to include only the functionality that we need. For a list of these modules, please see [Artifacts](artifacts). In our case we
only need to include `ktor-netty` (`ktor-core`, which is required for any Ktor application, is included transitively on including the former).  

These dependencies are hosted on [Bintray](https://bintray.com/kotlin/ktor) and as such the right
repositories need to be added to our build script.

For more detailed guide on setting up build files see

* [Getting Started with Gradle](getting-started-gradle)
* [Getting Started with Maven](getting-started-maven)

### Creating a self-hosted Application

Ktor allows applications to be hosted under Application Server such as Tomcat, or self-host, using Jetty or Netty. In this tutorial we're going to see how to self-host using Netty.

We begin by creating an `embeddedServer`, passing in the host factory as the first argument, the port as the second argument and the actual application code as the fourth argument (third argument is the host which is 0.0.0.0 by default).
The code below defines a single route that responds to the `GET` verb on the url `/` with the text `Hello, world!`

Once we've defined the routes, we start the server by calling `server.start`, passing as argument a boolean to indicate whether we want the main thread
of the application to block.  

```kotlin
import org.jetbrains.ktor.application.*
import org.jetbrains.ktor.host.*
import org.jetbrains.ktor.http.*
import org.jetbrains.ktor.netty.*
import org.jetbrains.ktor.response.*
import org.jetbrains.ktor.routing.*

fun main(args: Array<String>) {
    val server = embeddedServer(Netty, 8080) {
        routing {
            get("/") {
                call.respondText("Hello, world!", ContentType.Text.Html)
            }
        }
    }
    server.start(wait = true)
}
```

### Running the Application

Given that the entry point to our application is the standard Kotlin `main` function, we can simply run it and have our server start, listening on the designated port.

![Output](../../images/docs/hello-world-output.png)


### Next Steps

This was the simplest example of getting a self-hosted Ktor application up and running.
Next steps will be to understand the [Application](application) object as well as [Features](features).

For a more detailed guide to using IntelliJ IDEA see [Getting Started with IDEA](getting-started-idea)
