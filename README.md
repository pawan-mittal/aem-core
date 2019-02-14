## Create Project Guide - [Using Maven Archetype for SPA Starter Kit](https://github.com/adobe/aem-spa-project-archetype)

This guide creates a minimal Adobe Experience Manager project as a starting point for your own SPA projects.

View the tutorial on [Youtube Channel](https://www.youtube.com/channel/UCPTNFDCUiyqOXcX4MGFNgNw) : [Create a React App using AEM SPA Editor](https://www.youtube.com/watch?v=H8CuxJrFUE8)

if you have watched the video, then You can use this code for reference, also get started with SPA coding.

## System requirements

- An AEM 6.4 + SP2, running it locally (default PORT 4502)
- [Java](https://www.java.com/en/download/) 1.8 or higher
- [Maven](https://maven.apache.org/) 3.5.0 or higher
- [Node.js](https://nodejs.org/en/) v10+
- [npm](https://www.npmjs.com/) 6+

- Include the [Adobe Public Maven Repository](adobe-public-maven-repo) in your maven settings

It is recommended to set up the local AEM instances with `nosamplecontent` run mode.

Modules of the generated project is defined in [src/main/resources/archetype-resources](src/main/resources):

* [core](core/): OSGi bundle containing:
  * Java classes (e.g. Sling Models, Servlets, business logic)
* [ui.apps/src/main/content/jcr_root/apps](content/jcr_root/apps/):
  * AEM components with their scripts and dialog definitions
* [ui.content/src/main/content/jcr_root/conf](content/jcr_root/conf/): 
  * AEM content package with editable templates stored at `/conf`
* [ui.content/src/main/content/jcr_root/content](content/jcr_root/content/): 
  * AEM content package containing sample content (for development and test purposes)
* [angular-app](angular-app/): Angular application in case frontend chosen is set to be "angular" at project generation 
* [react-app](react-app/): React application in case frontend chosen is set to be "react" at project generation 
* [all](all/): Combines all modules to be installed as content package in AEM

## Required parameters

This archetype requires following parameters:
- `groupId` - Maven artifact groupId for all projects
- `artifactId`(default is `${groupId}.${projectName}`) - Maven artifact "root" artifactId, is suffixed for the individual modules
- `version` (default is `1.0.0-SNAPSHOT`) - Maven artifact version
- `package` (default is `${groupId}.${projectName}`) - Java class package name
- `projectName` (default is `mysamplespa`) - Used for building AEM apps path, content path, conf etc. Should not include spaces or special character.
- `projectTitle` (default is `My Sample SPA`) - Descriptive project name
- `componentGroup` (default is `${projectTitle}`) - Name of the component group in AEM Editor
- `optionFrontend` (default is `react`) - Type of frontent project, allowed options: either angular or react

## Install project in AEM

```
$ mvn clean install -PautoInstallPackage
```

## Provided Maven profiles
The generated maven project support different deployment profiles when running the Maven install goal `mvn install` within the reactor.

Id                        | Description
--------------------------|------------------------------
autoInstallBundle         | Install core bundle with the maven-sling-plugin to the felix console
autoInstallPackage        | Install the ui.content and ui.apps content package with the content-package-maven-plugin to the package manager to default author instance on localhost, port 4502. Hostname and port can be changed with the aem.host and aem.port user defined properties. 
autoInstallPackagePublish | Install the ui.content and ui.apps content package with the content-package-maven-plugin to the package manager to default publish instance on localhost, port 4503. Hostname and port can be changed with the aem.host and aem.port user defined properties.

The profile `integrationTests` is also available for the verify goal, to run the provided integration tests on the AEM instance.

#### Update the CORS configuration of the AEM instance (for React App)
1. Navigate to the Configuration Manager on the AEM instance at http://localhost:4502/system/console/configMgr
2. Look for the configuration: Adobe Granite Cross-Origin Resource Sharing Policy
3. Create a new configuration with the following additional values:
    * Allowed Origins: http://localhost:3000
    * Supported Headers: Authorization
    * Allowed Methods: OPTIONS
    
# Result
 AEM SPA Page - http://localhost:4502/editor.html/content/aemsamplereactapp/en.html
 
 React App - http://localhost:3000/content/aemsamplereactapp/en/home.html

### SAMPLE - Create project in batch mode (shown in [Youtube Video](https://www.youtube.com/watch?v=H8CuxJrFUE8))

In batch mode all the required parameters muse be set via `-Dparameter=value` argument. 

*Note: -DarchetypeVersion value must be synced with [AEM SPA Archetype version](https://github.com/adobe/aem-spa-project-archetype)*
```
$ mvn archetype:generate -B \
     -DarchetypeCatalog=local  \
     -DarchetypeGroupId=com.adobe.cq.spa.archetypes  \
     -DarchetypeArtifactId=aem-spa-project-archetype  \
     -DarchetypeVersion=1.0.5-SNAPSHOT \
     -Dpackage=com.sample.spa.react \
     -DgroupId=com.sample.spa.react \
     -DartifactId=samplereactapp \
     -Dversion=1.0.0-SNAPSHOT \
     -DprojectTitle="AEM Sample React App"  \
     -DprojectName=aemsamplereactapp  \
     -DcomponentGroup="AEM Sample React App" \
     -DoptionFrontend=react
```
