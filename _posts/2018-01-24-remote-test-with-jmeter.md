---
title: "Distributed test with JMeter"
tags: [tech, performance test, stress test, english, jmeter]
categories: [english, programming]
share-img: /img/jmeter_logo.svg
---

# Introduction

**JMeter** or **Apache JMeter** is an open source project which created by *Apache*, written in pure Java and designed for performance test. With *jMeter* we can do many things, such as load test web application, stress test, enduration test, etc. In this post I will introduce my test scenario for distributed testing with *jMeter*.

![jMeter logo](/img/jmeter_logo.svg)

# Scenario and Plan

I have an application which has just been upgraded to new version for server side programming language. In order to make sure current production environment works smoothly while switching to new update, I created a new server with new implementation. And for that reason, I would like to know the performance of this server. Information such as, "how many concurrent users it can serve?" would help me to decide how many instances I need behide load balancer for the whole web application. And furthermore, metric new server CPU capacity as well as respond time would help me compare to current running server.

<script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
<ins class="adsbygoogle"
     style="display:block; text-align:center;"
     data-ad-layout="in-article"
     data-ad-format="fluid"
     data-ad-client="ca-pub-2750437710821247"
     data-ad-slot="8905029259"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>

For that reason I will start with a scenario that include:

* request to server with first 10 concurrent users (virtual users or thread users)

* increasing concurrent users +10 each time

* monitoring server CPU to see when it around 100%, we can know the capacity of newly created server.

# Structure

First of all, we need to create a **test plan** with *jMeter*. Here is mine:

![Sample jMeter test](/img/sample_jmeter_test.png)

To make it simple, I created a dummy scenario which send *GET* request to *google.com*. In real work project, this configuration is for your real server name, path.

There are many components of *jMeter* but in this test case, I choose some basic components:

* **Thread Users**: In this case is *ConcurrentUsers* which presents how many virtual users to create.

* **HTTP Request**: a simple *GET* request to our server.

* **HTTP Cookie Manager**: adding some cookies for the request. If we have multiple cookies or want to add randomly (for example: different user with different cookie values), we can create a *CSV file* and read from that.

* **CSV Data Set Config**: read information from CSV file. We can have multiple *CSV Data Set Config* components for different purposes. The rule is that: each **thread user** would read one line of *CSV file* and loop back read from beginning if reaching end of file.

* **Constant Throughput Timer**: this one is important if you don't want to end up with a broken server. We use this component to set a fixed throughput. For example: `Constant Throughput Timer = 600` means that we have 600 requests per minute, or QPS is `600 / 60 = 10`. There would be 10 concurrent requests to server each second. In my case, I increase this number +10 each time to evaluate server CPU usage. Without this, if we run for a very long run loop, or loop forever, requests to our server would increase rapidlly and as a result the server would be broken.

To fully understand how to use *jMeter* component, please refer to [official document](http://jmeter.apache.org/usermanual/index.html). There is also a [best practice reference](http://jmeter.apache.org/usermanual/best-practices.html).

After test scenario is created, we need *jMeter servers* structure to run the test script. In my case, I use distributed structure which mean I have an admin server and multiple slave jmeter servers.

![Distributed servers](/img/jmeter_distributed_servers.png)

> Picture credit: https://www.blazemeter.com/blog/how-to-perform-distributed-testing-in-jmeter

For testing purpose, we can use *jMeter GUI* and confirm that our test script is working. But in real project, for a hug number of concurrent users we should use *non-GUI* mode to save resources. If you run on 1 jMeter client only, the command is similar to this:

```
jmeter -n -t test.jmx -l test.jtl
```

* `-n` option: run in *non-GUI* mode.

* `-t test.jmx`: test case to run

* `-l test.jtl`: test log file

In my case, I'm using distributed structure with 1 admin server `admin.jmeter.local` and two slaves server: `slave.jmeter.local.01`, `slave.jmeter.local.02`. We can have more slaves server to scale if number of concurrent users is huge or we want the test more distributed. We also presume that two slaves' IP addresses are `192.168.1.2` and `192.168.1.3`. An other important note is that admin and slaves server must be in same network so that we can use IP addresses.

* `admin.jmeter.local` server contain the test case and run the test case remotely.

* `slave.jmeter.local.01` and `slave.jmeter.local.02`: jMeter servers to run as nodes. We start these servers with command: `jmeter-server`.

Here is the steps to run:

* SSH to slave servers and run jmeter server with command:
    
    ```
    jmeter-server
    ```

  Notice the host and port from output, something similar to this:

    ```
    Created remote object: UnicastServerRef [liveRef: [endpoint:[192.168.1.2:49879](local),objID:[414ada3c:161277cc90c:-7fff, 7832254102280355278]]]
    ```

* SSH to `admin.jmeter.local`, run test case:

    ```
    jmeter -n -t test.jmx -R 192.168.1.2:49879,192.168.1.3:49879
    ```

And that's it! We've run distributed test with *jMeter*. Instead of using option `-R` we can use `-r` with a seperate property file. Please make sure to check [best practices](http://jmeter.apache.org/usermanual/best-practices.html) for this setting. Also check [official document](http://jmeter.apache.org/usermanual/remote-test.html) for distributed test to understand more.

<script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
<ins class="adsbygoogle"
     style="display:block; text-align:center;"
     data-ad-layout="in-article"
     data-ad-format="fluid"
     data-ad-client="ca-pub-2750437710821247"
     data-ad-slot="8905029259"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>