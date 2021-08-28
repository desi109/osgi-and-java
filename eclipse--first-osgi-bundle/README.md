# ```Eclipse:``` First OSGi Bundle

This ***First OSGi Bundle*** tutorial will drive you through – BND tools workspace creation, a sample OSGI bundle project and OSGI runtime creation.We will see “How to develop OSGI Bundle”  and  this tutorial is intended for beginners who are about to start learning OSGI. We will use ```Eclipse```.

<br>

---
## Prerequisites:
---
What is required to start OSGI Project?

1. ```Eclipse IDE```: download latest Eclipse IDE that supports BND tools plugin.
2. ```BND Tools eclipse plugin```
* * Eclipse → Help → Eclipse Marketplace.. → search for ***Bnd tools***
3. ```Equinox```: Eclipse IDE is built on top of OSGI.
Lets start developing simple OSGI bundle.
4. ```Java```

<br>

---
### Setting up Eclipse with Equinox
<br>

Download Equinox from https://download.eclipse.org/equinox/ and install it in local folder (e.g. ***/home/user/equinox-osgi/```equinox-SDK-3.5.1```/***).

* Eclipse → Window → Preferences → Java → Build Path → User Libraries.
* New → type the library name “Equinox”
* Add JARs → add ```org.eclipse.osgi_version.jar``` from ***/home/user/equinox-osgi/equinox-SDK-3.5.1/plugins/*** where version is the actual version tag attached to the JAR file

Next you need to inform Eclipse of the location of the source code. 
* Eclipse → Window → Preferences → Java → Build Path → User Libraries →  Source attachment → Edit
* External File → browse to the file org.eclipse.osgi.source_version.jar from ***/home/user/equinox-osgi/equinox-SDK-3.5.1/plugins/*** where version is the actual version tag attached to the JAR file

You should now have something that looks like:

![Setting up Eclipse with Equinox](https://github.com/desi109/osgi-and-java/eclipse--first-osgi-bundle/images/setting-up-eclipse-with-equinox.png)

<br>

---
## Bnd Workspace Creation
---
All BND based projects requires bnd workspace to get start.Bnd workspace is different from  normal eclipse workspace and BND workspace contains all project dependencies and build configurations for  OSGI projects. Bnd workspace groups all OSGI bundle projects along with conf directory. It also provides Gradle build  support to build projects automatically.
Let’s create Bnd workspace in the eclipse.

* File → New → Bnd OSGi Workspace → select Create in: → give bnd workspace folder location → Next <br>
![Bnd Workspace Creation 1](https://github.com/desi109/osgi-and-java/eclipse--first-osgi-bundle/images/bnd-workspace-creation-1.jpg)

* select ***bndtools/workspace*** → Next <br>
![Bnd Workspace Creation 2](https://github.com/desi109/osgi-and-java/eclipse--first-osgi-bundle/images/bnd-workspace-creation-2.png)

* this will create the ````cnf```` directory <br>
![Bnd Workspace Creation 3](https://github.com/desi109/osgi-and-java/eclipse--first-osgi-bundle/images/bnd-workspace-creation-3.png)

<br>

---
## First OSGi Bundle Creation
---
* File →  New → Bnd OSGi Project → select Project Template: → select ```<<Empty>> 0.0.0--[built-in]``` → Next <br>
![First OSGi Bundle Creation 1](https://github.com/desi109/osgi-and-java/eclipse--first-osgi-bundle/images/first-osgi-bundle-creation-1.png)

What is Project Template? - BND provides list of project templates for web based project, REST/SOAP web services based project like Maven Archie type.

* give Project name: org.osgi.tutorial → Finish <br>
![First OSGi Bundle Creation 2](https://github.com/desi109/osgi-and-java/eclipse--first-osgi-bundle/images/first-osgi-bundle-creation-2.png)

It is  always best practice to give project name as “package name” as OSGI bundles follows this specification. It will create the below project structure and each project will have ```bnd.bnd``` file that contains settings of the project. The ```bnd.bnd``` file has:
* * ***Contents*** and ***Description*** sections - used to auto create MANIFEST.MF file
* * ***Build*** section - used manage project dependencies
* * ***Run*** section - used to Run the OSGI bundle

Update OSGI dependencies :
Open bnd.bnd file and click on build tab.
Under build path,click on + icon.
It will open below path and search for osgi and add osgi.core bundle
Save the file and refresh the project. It will add osgi.core in the referenced libraries.