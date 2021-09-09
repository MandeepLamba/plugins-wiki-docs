## Overview

The reason I created the plugin was because I wanted to integrate
Jenkins with an external application. Invoking a Jenkins jobs via the
REST API was simple, but getting Jenkins to callback the external
application wasn't straight forward.

All the plugins I'd seen either had to be individually configured per
job (i.e. in a post build step), or their features were limited to
making a HTTP GET/POST request (a bit restrictive).

Basically:

-   I wanted to be able to write my own code
-   I didn't want to repeat myself

So I wrote this plugin. Along the way, I realised it could have some
other applications too:

-   customised logging
-   performance monitoring
-   incident escalation
-   integration with 3rd party applications
-   ???

## Building

Prerequisites:

-   JDK 6 (or above)

To setup for use with Intellij IDEA

To run Jenkins ([http://localhost:8080](http://localhost:8080/)) locally
with the plugin installed:

To build the Jenkins plugin (.jpi) file:

To publish/release the Jenkins plugin:

1.  Update the `version` in `gradle.properties`, to remove "-SNAPSHOT"
    (increment and re-add after publishing)

## Basic Usage

To get started:

1.  Install the plugin (or [run Jenkins
    locally](https://github.com/markyjackson-taulia/groovy-events-listener-plugin#building))
2.  Navigate to the *Jenkins \> Manage Jenkins \> Configuration* page
3.  You should now see a *Global Events Plugin* section (similar to the
    following screenshot).

[![Version
1.0.0](https://github.com/markyjackson-taulia/groovy-events-listener-plugin/raw/master/src/main/site/screenshot-version-1.005.png)](https://github.com/markyjackson-taulia/groovy-events-listener-plugin/blob/master/src/main/site/screenshot-version-1.005.png)

This plugin executes the supplied Groovy code, every time an event is
triggered.

So lets get started with the simplest example.

Now save the changes, kick off a Jenkins job, and you will see "hello
world!" written to the logs three times. Alternatively, there's now
a `Test Groovy Code` button, which will execute the code with
the `event`=`RunListener.onStarted`.

The plugin actually injects a couple of variables, which you can use in
your code. Here's some examples using the `event`and `env` variables.

This code limits the logging to only occur when a Job is
completed! N.B. this behaviour can also be replicated using the
configuration options.

And this one filters on Job's whose name starts with "Foobar"...

There's also a `context` Map variable. You can add your own variables to
this Map, by returning a Map from your code. E.g.

This will keep a record in memory, of how many times Jobs have finished.
You can also achieve the same result, by adding variables directly to
the Map variable... e.g.

You can also use `@Grab` annotations ([only where they are
valid](https://issues.apache.org/jira/browse/GROOVY-6069)) if you'd like
to import external dependencies
(thanks [Daniel](https://github.com/CoreMedia/job-dsl-plugin/commit/830fae7a0fd8a046c620600e46633166804190e3)for
your solution!).

Not bad! And finally, you can import groovy scripts, so you can hide
away some of the heavy lifting... here I'm using
a [RestClient.groovy](https://github.com/markyjackson-taulia/groovy-events-listener-plugin/blob/master/src/main/site/includes/RestClient.groovy) script.

You can pretty much do what ever you want from here... custom logging to
a file, sending performance metrics to an elastic server, sending email
or messenger notifications, calling a SOAP service... the world's your
oyster. If you've got something cool that you want to share, let me know
and I'll add it to
the [examples](https://github.com/markyjackson-taulia/groovy-events-listener-plugin/blob/master/src/main/site/examples)!

For more details on which events trigger the code, what variables are
available and details on configuring logging, please see the [plugin's
help
file](https://cdn.rawgit.com/jenkinsci/groovy-events-listener-plugin/master/src/main/resources/org/jenkinsci/plugins/globalEventsPlugin/GlobalEventsPlugin/help-onEventGroovyCode.html).

## Authors

Marky Jackson - <marky.r.jackson@gmail.comn>

## License

Licensed under the [MIT License
(MIT)](https://github.com/markyjackson-taulia/groovy-events-listener-plugin/blob/master/LICENSE)

  
