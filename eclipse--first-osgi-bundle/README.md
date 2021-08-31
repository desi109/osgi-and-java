# ```Eclipse:``` First OSGi Bundle

This ***First OSGi Bundle*** tutorial will drive you through – BND tools workspace creation, a sample OSGi bundle project and OSGi runtime creation.We will see “How to develop OSGi Bundle”  and  this tutorial is intended for beginners who are about to start learning OSGi. We will use ```Eclipse```.

<br>

<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary><h2 style="display: inline-block">Table of Contents</h2></summary>
  <ol>
    <li>
      <a href="#prerequisites">Prerequisites</a>
    </li>
    <li>
      <a href="#setting-up-eclipse-with-equinox">Setting up Eclipse with Equinox</a>
    </li>
    <li>
      <a href="#bnd-workspace-creation">Bnd Workspace Creation</a>
    </li>
    <li>
      <a href="#first-osgi-bundle">First OSGi Bundle</a>
    </li>
  </ol>
</details>

<br>

<br>


---
## Prerequisites
---
What is required to start OSGi Project?

1. ```Eclipse IDE```: download latest Eclipse IDE that supports BND tools plugin.
2. ```BND Tools eclipse plugin```
* * Eclipse → Help → Eclipse Marketplace.. → search for ***Bnd tools***
3. ```Equinox```: Eclipse IDE is built on top of OSGi.
Lets start developing simple OSGi bundle.
4. ```Java```

<br>

---
## Setting up Eclipse with Equinox
---
Download Equinox from https://download.eclipse.org/equinox/ and install it in local folder (e.g. ***/home/user/equinox-osgi/```equinox-SDK-3.5.1```/***).

* Eclipse → Window → Preferences → Java → Build Path → User Libraries.
* New → type the library name “Equinox”
* Add JARs → add ```org.eclipse.osgi_version.jar``` from ***/home/user/equinox-osgi/equinox-SDK-3.5.1/plugins/*** where version is the actual version tag attached to the JAR file

Next you need to inform Eclipse of the location of the source code. 
* Eclipse → Window → Preferences → Java → Build Path → User Libraries →  Source attachment → Edit
* External File → browse to the file org.eclipse.osgi.source_version.jar from ***/home/user/equinox-osgi/equinox-SDK-3.5.1/plugins/*** where version is the actual version tag attached to the JAR file

You should now have something that looks like: <br>
<img src="https://github.com/desi109/osgi-and-java/blob/master/eclipse--first-osgi-bundle/images/setting-up-eclipse-with-equinox.png" title="Setting up Eclipse with Equinox" width="70%">

<br>


---
## Bnd Workspace Creation
---
All BND based projects requires bnd workspace to get start.Bnd workspace is different from  normal eclipse workspace and BND workspace contains all project dependencies and build configurations for  OSGi projects. Bnd workspace groups all OSGi bundle projects along with conf directory. It also provides Gradle build  support to build projects automatically.
Let’s create Bnd workspace in the eclipse.

* File → New → Bnd OSGi Workspace → select Create in: → give bnd workspace folder location → Next <br>
<img src="https://github.com/desi109/osgi-and-java/blob/master/eclipse--first-osgi-bundle/images/bnd-workspace-creation-1.jpg" title="Bnd Workspace Creation 1" width="45%"> <br>

* select ***bndtools/workspace*** → Next <br>
<img src="https://github.com/desi109/osgi-and-java/blob/master/eclipse--first-osgi-bundle/images/bnd-workspace-creation-2.png" title="Bnd Workspace Creation 2" width="55%"> <br>

* this will create the ````cnf```` directory <br>
<img src="https://github.com/desi109/osgi-and-java/blob/master/eclipse--first-osgi-bundle/images/bnd-workspace-creation-3.png" title="Bnd Workspace Creation 3" width="35%"> <br>

<br>

---
## First OSGi Bundle
---
* File →  New → Bnd OSGi Project → select Project Template: → select ```<<Empty>> 0.0.0--[built-in]``` → Next <br>
<img src="https://github.com/desi109/osgi-and-java/blob/master/eclipse--first-osgi-bundle/images/first-osgi-bundle-creation-1.png" title="First OSGi Bundle Creation 1" width="70%">

What is Project Template? - BND provides list of project templates for web based project, REST/SOAP web services based project like Maven Archie type.

* give Project name: org.osgi.tutorial → Finish <br>
<img src="https://github.com/desi109/osgi-and-java/blob/master/eclipse--first-osgi-bundle/images/first-osgi-bundle-creation-2.png" title="First OSGi Bundle Creation 2" width="70%">

It is  always best practice to give project name as “package name” as OSGi bundles follows this specification. It will create the below project structure and each project will have ```bnd.bnd``` file that contains settings of the project.  <br>

Every OSGi Bundle project requires Custom Bundle Activator. Let's create a HelloWorldActivator that implements BundleActivator. <br>
<img src="https://github.com/desi109/osgi-and-java/blob/master/eclipse--first-osgi-bundle/images/hello-world-activator.png" title="HelloWorldActivator" width="90%"> 

<br>


```HelloWorldActivator.java```
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


The ```bnd.bnd``` file has:
* * ***Contents*** and ***Description*** sections - used to auto create MANIFEST.MF file <br>
<img src="https://github.com/desi109/osgi-and-java/blob/master/eclipse--first-osgi-bundle/images/bnd-contents.png" title="Bnd Contents" width="90%"> <br>
<b>How to map BundleActivator in MANIFEST.MF?</b> <br>
BND tools will auto create MANIFEST file from bnd.bnd file. You just need to update the bnd.bnd with version and activator details. You can also provide export package, import package details and all.
Just refresh the project and you can see the generated jar file in “generated”. You can directly deploy this jar file in OSGi container. <br>
<img src="https://github.com/desi109/osgi-and-java/blob/master/eclipse--first-osgi-bundle/images/bnd-description.png" title="Bnd Description" width="90%"> <br>
* * ***Build*** section - used manage project dependencies <br>
<img src="https://github.com/desi109/osgi-and-java/blob/master/eclipse--first-osgi-bundle/images/bnd-build.png" title="Bnd Build" width="90%"> <br> <br>
* * ***Run*** section - used to Run the OSGi bundle. To run the configuration click the green Run button. <br>
<img src="https://github.com/desi109/osgi-and-java/blob/master/eclipse--first-osgi-bundle/images/bnd-run.png" title="Bnd Rub" width="90%"> <br>
* * ***Source*** section <br>
<img src="https://github.com/desi109/osgi-and-java/blob/master/eclipse--first-osgi-bundle/images/bnd-source.png" title="Bnd Source" width="90%"> <br>

```java
-buildpath: osgi.core
Bundle-Activator: org.osgi.tutorial.HelloWorldActivator
Bundle-Version: 1.0.0.${tstamp}

-runfw: org.eclipse.osgi;version='[3.13.100.v20180827-1536,3.13.100.v20180827-1536]'
-runee: JavaSE-11

-runprovidedcapabilities: ${native_capability}

-resolve.effective: active;skip:="osgi.service"

-runbundles: \
	org.apache.felix.gogo.runtime,\
	org.apache.felix.gogo.shell,\
	org.apache.felix.gogo.command,\
	org.osgi.tutorial;version=latest

-runrequires: \
	osgi.identity;filter:='(osgi.identity=org.apache.felix.gogo.shell)',\
	osgi.identity;filter:='(osgi.identity=org.apache.felix.gogo.command)'
	
-runproperties: osgi.console=
Export-Package: org.osgi.tutorial
Bundle-Name: OSGi Tutorial Bundle  (org.osgi.tutorial)
Bundle-Description: This is OSGi Bundle Tutorial.
```
<br>

JAR file: [org.osgi.tutorial.jar](https://github.com/desi109/osgi-and-java/blob/master/eclipse--first-osgi-bundle/OSGi-tutorial/org.osgi.tutorial/generated/org.osgi.tutorial.jar)