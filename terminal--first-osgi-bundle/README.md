# ```Terminal/CMD:``` First OSGi Bundle

This ***First OSGi Bundle*** tutorial will drive you through a sample OSGi bundle project. We will see “How to develop OSGi Bundle”  and  this tutorial is intended for beginners who are about to start learning OSGi. We will use only ```Terminal``` or ```CMD``` .

<br>

<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary><h2 style="display: inline-block">Table of Contents</h2></summary>
  <ol>
    <li>
      <a href="#prerequisites">Prerequisites</a>
      <ul>
        <li><a href="#a-setting-up-with-equinox">(a) Setting up with Equinox</a></li>
        <li><a href="#b-setting-up-with-felix">(b) Setting up with Felix</a></li>
      </ul>
    </li>
    <li>
      <a href="#first-osgi-bundle">First OSGi Bundle</a>
    </li>
    <li>
      <a href="#install-bundle">Install Bundle</a>
      <ul>
        <li><a href="#a-install-bundle-with-equinox">(a) Install bundle with Equinox</a></li>
        <li><a href="#b-install-bundle-with-felix">(b) Install bundle with Felix</a></li>
      </ul>
    </li>
  </ol>
</details>

---
## Prerequisites:
---
What is required to start OSiI Project?
1. Lets start developing simple OSGi bundle. <br>
(a) ```Equinox```: Eclipse IDE is built on top of OSGi. <br>
<b>OR</b> <br>
(b) ```Felix```: Apache Felix is a community effort to implement the OSGi Framework and Service platform and other interesting OSGi-related technologies . <br>

2. ```Java```

<br>

---
### (a) Setting up with Equinox
<br>

Download Equinox from https://download.eclipse.org/equinox/ and install it in local folder (e.g. ***/home/user/equinox-osgi/```equinox-SDK-3.5.1```/***).

<br>

---
### (b) Setting up with Felix
<br>

Download Felix from https://felix.apache.org/documentation/downloads.html and install it in local folder (e.g. ***/home/user/felix-osgi/```org.apache.felix.main.distribution-7.0.1```/***).

<br>

---
## First OSGi Bundle
---
Create folder hierarchy like:
```
OSGi-tutorial  
│
└───org
│   └───osgi
│       └───tutorial
│           │   HelloWorldActivator.java           
│   
└───META-INF
    │   MANIFEST.MF
```


```/org/osgi/tutorial/HelloWorldActivator.java```
```java
package org.osgi.tutorial;

import org.osgi.framework.BundleActivator;
import org.osgi.framework.BundleContext;

public class HelloWorldActivator implements BundleActivator{
    public void start(BundleContext context) throws Exception {
        System.out.println("Hello World!");
    }

    public void stop(BundleContext context) throws Exception {
        System.out.println("Goodbye World!");
    }
}
```

<br>

```/META-INF/MANIFEST.MF```
```java
Manifest-Version: 1
Bundle-Name: OSGi Tutorial Bundle  (org.osgi.tutorial)
Bundle-SymbolicName: org.osgi.tutorial
Bundle-Version: 1.0.0
Bundle-Activator: org.osgi.tutorial.HelloWorldActivator
Bundle-Description: This is OSGi Bundle Tutorial.
Import-Package:  org.osgi.framework
Export-Package: org.osgi.tutorial
```

<br>

You will have to build ```org.osgi.tutorial.jar``` manually. First use the javac compiler to generate class files:

<br>

---
## Install bundle 
---

### (a) Install bundle with Equinox
Then use the command for option <b>(a) Equinox</b>:
```java
javac -cp ../equinox-osgi/plugins/org.eclipse.osgi_3.5.1.R35x_v20090827.jar -d ../OSGi-tutorial/classes ../OSGi-tutorial/org/osgi/tutorial/HelloWorldActivator.java

cd ../OSGi-tutorial
jar -cvfm org.osgi.tutorial.jar META-INF/MANIFEST.MF -C classes .
 

cd ~/equinox-osgi/equinox-SDK-3.5.1/plugins
java -jar org.eclipse.osgi_3.5.1.R35x_v20090827.jar -console -configuration runtime
```

When OSGi console is open, install the new org.osgi.tutorial bundle:
```java
osgi> install file:../../GitHub/osgi-and-java/terminal--first-osgi-bundle/OSGi-tutorial/org.osgi.tutorial.jar


osgi> ss
Framework is launched.

id	State       Bundle
0	ACTIVE      org.eclipse.osgi_3.5.1.R35x_v20090827
3	INSTALLED   org.osgi.tutorial_1.0.0

osgi> start 3
Hello World!

osgi> stop 3
Goodbye World!

osgi> ss
Framework is launched.

id	State       Bundle
0	ACTIVE      org.eclipse.osgi_3.5.1.R35x_v20090827
3	RESOLVED    org.osgi.tutorial_1.0.0

```

<br>

<br>

### (b) Install bundle with Felix

Use the command for option <b>(b) Felix</b>:
The folder hierarchy will look like:
```java
javac -cp ../felix-osgi/org.apache.felix.main.distribution-7.0.1/bin/felix.jar -d ../OSGi-tutorial/classes ../OSGi-tutorial/org/osgi/tutorial/HelloWorldActivator.java

cd ../OSGi-tutorial
jar -cvfm org.osgi.tutorial.jar META-INF/MANIFEST.MF -C classes .
 

cd ../felix-osgi/org.apache.felix.main.distribution-7.0.1
java -jar bin/felix.jar 
```

When OSGi console is open, install the new org.osgi.tutorial bundle:
```java
osgi> install file:../../GitHub/osgi-and-java/terminal--first-osgi-bundle/OSGi-tutorial/org.osgi.tutorial.jar


g! lb                                                
START LEVEL 1
   ID|State      |Level|Name
    0|Active     |    0|System Bundle (7.0.1)|7.0.1
    1|Active     |    1|jansi (1.18.0)|1.18.0
    2|Active     |    1|JLine Bundle (3.13.2)|3.13.2
    3|Active     |    1|Apache Felix Bundle Repository (2.0.10)|2.0.10
    4|Active     |    1|Apache Felix Gogo Command (1.1.2)|1.1.2
    5|Active     |    1|Apache Felix Gogo JLine Shell (1.1.8)|1.1.8
    6|Active     |    1|Apache Felix Gogo Runtime (1.1.4)|1.1.4
    7|Installed  |    1|OSGi Tutorial Bundle  (org.osgi.tutorial) (1.0.0)|1.0.0


g! start 7
Hello World!

g! stop 7
Goodbye World!

g! lb                 
START LEVEL 1
   ID|State      |Level|Name
    0|Active     |    0|System Bundle (7.0.1)|7.0.1
    1|Active     |    1|jansi (1.18.0)|1.18.0
    2|Active     |    1|JLine Bundle (3.13.2)|3.13.2
    3|Active     |    1|Apache Felix Bundle Repository (2.0.10)|2.0.10
    4|Active     |    1|Apache Felix Gogo Command (1.1.2)|1.1.2
    5|Active     |    1|Apache Felix Gogo JLine Shell (1.1.8)|1.1.8
    6|Active     |    1|Apache Felix Gogo Runtime (1.1.4)|1.1.4
    7|Resolved   |    1|OSGi Tutorial Bundle  (org.osgi.tutorial) (1.0.0)|1.0.0

```

<br>

```
OSGi-tutorial  
|
└───org.osgi.tutorial.jar
|
└───org
│   └───osgi
│       └───tutorial
│           └───HelloWorldActivator.java           
|
└───META-INF
|   └───MANIFEST.MF
|
└───classes
|   └───org
│       └───osgi
│           └───tutorial
│               └───HelloWorldActivator.class
```



JAR file: [org.osgi.tutorial.jar](https://github.com/desi109/osgi-and-java/blob/master/terminal--first-osgi-bundle/OSGi-tutorial/org.osgi.tutorial.jar)
