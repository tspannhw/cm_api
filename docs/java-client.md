---
layout: default
title: Java Client (Deprecated)
id: java-client
permalink: /docs/java-client/
---

#### Table of Contents ####

* toc
{:toc}


Version
=======
From Cloudera Manager version 6.0 i.e. API version 30 onwards, this Java API client
has been deprecated.

Use new [Swagger based Java API client]({{ site.url }}/docs/java-client-swagger/)
for Cloudera Manager version 6.0 i.e. API version 30 onwards.


Setting Up
==========
Merge the following to your Maven project's `pom.xml`:

    <project>
      <repositories>
        <repository>
          <id>cdh.repo</id>
          <url>https://repository.cloudera.com/artifactory/cloudera-repos</url>
          <name>Cloudera Repository</name>
        </repository>
        …
      </repositories>
      <dependencies>
        <dependency>
          <groupId>com.cloudera.api</groupId>
          <artifactId>cloudera-manager-api</artifactId>
          <version>{{ site.latest_cm_version }}</version>  <!-- Or the CM version you have -->
        </dependency>
        …
      </dependencies>
      ...
    </project>

You can also directly download the jar (and sources) from the [Cloudera repository](https://repository.cloudera.com/artifactory/cloudera-repos/com/cloudera/api/cloudera-manager-api/).


Javadoc
=======
Here is the last [javadoc]({{ site.url }}/javadoc/5.14.0/index.html),
for API version 19 (CM 5.14.0)


Basic Usage
===========

The fundamental client handle is a `RootResourceV{{ site.latest_api_version }}`. (Replace
the version number with the version that you are working with.) With the root resource,
you can traverse the REST namespace.

{% highlight java %}
RootResourceV{{ site.latest_api_version }} apiRoot = new ClouderaManagerClientBuilder()
    .withHost("cm.cloudera.com")
    .withUsernamePassword("admin", "admin")
    .build()
    .getRootV{{ site.latest_api_version }}();

// Get a list of defined clusters
ApiClusterList clusters = apiRoot.getClustersResource()
    .readClusters(DataView.SUMMARY);
{% endhighlight %}

To see a full example of cluster deployment using the Java client, see
[whirr-cm](https://github.com/cloudera/whirr-cm). Specifically, jump
straight to [CmServerImpl#configure](https://github.com/cloudera/whirr-cm/blob/edb38ca7faa3e4bb2c23450ff0183c2dd631dcf4/src/main/java/com/cloudera/whirr/cm/server/impl/CmServerImpl.java#L590)
to see the core of the action.