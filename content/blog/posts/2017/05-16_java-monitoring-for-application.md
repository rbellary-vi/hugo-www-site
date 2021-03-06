---
author: "Mike Mackrory"
date: "2017-05-16"
title: "How to Choose the Right Java Monitoring for Your Application"
description: "Metricly provides five different integrations for Java monitoring. Of course, the one that is the “best” choice for you depends on your environment."
category: "DevOps"
url: "/java-monitoring-for-application/"
layout: "single"
---

When [implementing a monitoring solution](/aws-cost-tool) for your Java environment, choosing the correct integration option is an essential part of that decision. The integration option you choose will determine several important characteristics, including:

-   What metrics you are concerned about collecting and analyzing
-   How metrics will be gathered from your application
-   How metrics will be transferred to your Java monitoring provider
-   What additional configuration will be required for your application to fully integrate with the infrastructure monitoring provider

Which Java Monitoring Integration is Best?
------------------------------------------

Metricly provides five different [integrations for monitoring your Java applications](https://docs.metricly.com/integrations/). Of course, the one that is the "best" choice for you will depend on your needs and your environment.

To help you determine the best fit for your needs, this article explores each of the integrations available for use with Metricly. For each, we'll explore what level of effort is involved in setting up the integration, any dependencies the integration relies on, and how to configure the integration and get metrics flowing into your Metricly account.

Before we begin, there are some fundamental questions which might narrow down which of the five Java monitoring options you should look at first.

**Are you looking to examine JVM metrics or Application metrics?**

-   **JVM Metrics**
    -   Consider either the [Java Agent](https://docs.metricly.com/integrations/agents/java-agent/) or JMX integration.

-   **Application Metrics**
    -   Are you using Dropwizard?
        -   With Dropwizard metrics, you have the choice of submitting results through StatsD, or through the Metricly Rest API.
    -   Do you have, or do you wish to have, either a StatsD server or the StatsD daemon running?
        -   Consider the Ananke library.
    -   Would you prefer to submit your metrics through the Metricly Rest API?
        -   Consider the Iris Library.

JVM Metrics Vs. Application Metrics
-----------------------------------

**JVM Metrics**

The Java Virtual Machine (JVM) is the container that allows a Java application to be executed independently of the underlying operating system. When running a Java application, it is important to monitor the health of the underlying JVM. Some important metrics to monitor include:

-   Process availability -- Whether the JVM is running
-   Java Heap Usage -- The memory in use by the JVM
-   Garbage Collection -- How long and how often the Garbage Collector runs
-   Active Threads -- How work is processed through the application
-   Response Time -- How responsive the application is to requests

**Application Metrics**

Users of your application have an expectation that requests should be returned quickly and with accurate results. Application metrics allow you to monitor this and ensure that users are experiencing the application in a positive manner. Some metrics you'll want to monitor are:

-   Duration between request and response
-   Error counts and percentage of total request counts that return errors.
-   Request rate

Choosing Between StatsD and the Metricly Rest API
--------------------------------------------------

StatsD was originally developed by the engineers at Etsy, and is a simple NodeJS daemon that listens for messages, extracts metrics, and can then be used to push the data to a datastore, or a monitoring service like Metricly.

The original StatsD offering has been used as a reference implementation for some other projects, including [Metricly StatsD](/statsd-metricly-advanced-monitoring/). If you already have a StatsD server, you can configure it to push metrics to Metricly. If you don't yet have a StatsD server, one is installed as part of the Metricly [Linux Agent](https://docs.metricly.com/integrations/agents/linux-agent/).

The [Metricly RESTful API](/inside-metricly-api/) allows developers to interact with Metricly, both to push metrics into the Metricly system and to retrieve information programmatically. Metrics are received in the form of events, which are in turn digested by the Metricly system, and are made available for use in Java [monitoring dashboards](/devops-dashboard-best-practices) and Metricly's other analytical offerings.

Let's look at each of the integrations in more detail.

Ananke
------

The name Ananke comes from Greek mythology and refers to a being that embodies necessity, and the idea of a force which exists from the beginning and encompasses all. It's an appropriate name for a metrics library that can monitor all aspects of your application.

The [Ananke](https://docs.metricly.com/integrations/anake/) library gathers and submits metrics to the StatsD daemon, which is a dependency of using this library, and is included in the Metricly Linux Agent. Ananke can report a variety of metrics, including:

-   Counters
-   Events
-   Gauges
-   Histograms
-   Timing measurements

To use Ananke to monitor your application, you'll need to include Ananke as a dependency for your project, and instantiate a StatsDClient which can be accessed from all relevant classes.

    StatsDClient client = new NetuitiveStatsDClient("localhost", "8000");

To submit an event, such as the time for a page to load, you would pass a callable function into the client.

    client.timed(new TimedRequest()   
    .withFunc("pageloadtime()");

Dropwizard
----------

Dropwizard is a collection of libraries that have been curated into a framework which allows developers to focus on creating applications, without having to spend time investigating and building a platform to support the application. One of the libraries available to users of this framework is the Dropwizard Metrics library. This library enables unparalleled insight and visibility into all levels of your application.

Dropwizard metrics are typically accessed through the admin endpoint for the application; however, by including Metricly dropwizard-metrics as a runtime dependency for your project; you can configure the submission of the entire metrics suite to the StatsD daemon, or to the Metricly Restful API.

    metrics:   
      frequency: 1 minute   
    reporters:				     
      - type: statsd       
    host: netuitive-agent       
    port: 8125;

*Different-Java-Integrations-Dropwizard*

    metrics:   
      frequency: 1 minute   
      reporters:     
        - type: netuitive-rest       
        apiKey: YourCustomNetuitiveAPIKey       
    elementName: HelloWorld

*Different-Java-Integrations-RESTAPI-Configuration*

Iris
----

Iris is a Java SDK from Metricly that allows you to interact programmatically with the Metricly API. After including the library as a dependency of your project, you will need to create an instance of the appropriate Metricly client, which is accessible by relevant classes with your application.

    NetuitiveIngestEventRestClient ingestClient = new NetuitiveIngestEventRestClient("username", "password");

*Different-Java-Integrations-Iris*

After creating a list of IngestEvent objects called events, you could then submit them to the ingestClient instance as follows:

    ingestClient.ingest(events);

*Different-Java-Integrations-Iris-Ingest*

An advantage of Iris is that it allows for both creation/submission of metrics to the API, as well as the retrieval of metrics and other Metricly resources from the API. The API is well documented and can be further explored if you have a [Metricly account](/signup).

Java Monitoring Agent
---------------------

The Metricly Java monitoring agent is based on the Zorka Monitoring Agent, an open source monitoring agent for the JVM. The agent provides byte-code instrumentation without needing the change source code, and allows for the collection of standard JVM runtime metrics, including:

-   CPU
-   Memory
-   Garbage Collector (GC)
-   Threads

Additional application metrics are collected and reported as well.

You will need to have an active Metricly account to make use of the agent. To install the agent, you will need to download and unzip the [Metricly Agent](https://github.com/Netuitive/zorka/releases/latest). You will then need to locate the *zorka.properties* file and update it with your API Key provided by Metricly.

**Pro Tip:** You can get your Java API key by logging into your Metricly account, navigating to Integrations, and then clicking on the Java button. Your API key will be displayed right below the header.

Finally, you'll need to restart your JVM, passing in the *-javaagent* flag with the path to the netuitive-zorka directory as a property. Your command should look similar to the following.

    java -javaagent:/opt/netuitive-zorka/netuitive.jar=/opt/netuitive-zorka -jar application.jar

*[Different-Java-Integrations-Java-Agent*

JMX
---

The Metricly JMX solution uses Jolokia to publish metrics to the Metricly Linux agent. The name Jolokia comes from the ghost pepper that is grown largely in eastern Asia, and was chosen to represent the Jolokia project because it was going to be the "hot" new way of gathering metrics using JMX.

To set up the JMX integration, you'll need to first install the [Linux agent](https://docs.metricly.com/integrations/agents/linux-agent/). Log into your Metricly account, navigate to Integrations, and then click on the Linux button. You'll be shown a shell command with your personal API key included to be used for installing the Linux agent on your machine.

Once the Linux agent is installed, you'll want to download the Jolokia jar and install it in the */opt/netuitive-agent/* directory. Next, navigate to the collectors folder (Usually located at */opt/netuitive-agent/conf/collectors)* and open the JolokiaCollector.conf file and change the *enabled* setting to **true.**

Restart the Linux agent, using the appropriate command for your Linux distribution.

    $ service netuitive-agent restart
    $ /etc/init.d/netuitive-agent restart
    $ initctl restart netuitive-agent
    $ systemctl restart netuitive-agent

*Different-Java-Integrations-Restart-Agent*

Finally, add the javaagent flag to the command which starts your application. It should look similar to the command below.

    java -javaagent:/opt/agent.jar=port=8778,host=0.0.0.0 -jar application.jar

*Different-Java-Integrations-Java-Agent-Flag*

Which Java Monitoring Works For You?
------------------------------------

Each of the integrations we looked at here provides a way to push metrics from your application up to Metricly for analysis---and Iris even lets you pull them back down again. What frameworks you're already using, what tools you may already have installed, and which Java monitoring metrics you are looking to gather are key to identifying which will work best for you.
