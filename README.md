# OSGi_Skeleton #
OSGi skeleton project (using Equinox, Java 8 and the Linx command line). 

A basic OSGi skeleton project to get things going. The skeleton includes a simple bundle (aka plugin).

Please note, the JARs in the example commands have version numbers. For legibility the version numbers are not shown.

# Folder structure #
Run

`mkdir -p my-osgi/{configuration,code,plugins}`

Navigate into the my-osgi folder. This is the base folder.

`cd ./my-osgi`

# OSGi Configuration #
Create the config.ini file under the configuration folder.

`touch configuration/config.ini`

`osgi.bundles=org.apache.felix.gogo.runtime@start, org.apache.felix.gogo.command@start, org.apache.felix.gogo.shell@start, org.eclipse.equinox.console@start`

# Equinox JARs #
From an Eclipse installation copy the JARs into the base folder. Your mileage might vary but under Windows the JARs are in the plugins folder of the Eclipse install location. In Linux the plugins might be in the users home folder under ~/.p2/pool/plugins/

`cp ~/.p2/pool/plugins/org.apache.felix.gogo.command.jar ./`

`cp ~/.p2/pool/plugins/org.apache.felix.gogo.runtime.jar ./`

`cp ~/.p2/pool/plugins/org.apache.felix.gogo.shell.jar ./`

`cp ~/.p2/pool/plugins/org.eclipse.equinox.console.jar ./`

`cp ~/.p2/pool/plugins/org.eclipse.osgi.jar ./`

# Code #
Create the folders by typing

`mkdir -p code/{src,src/com/osgi/rcp,bin}`

## Sample Activator ##
Create the Activator. This is the class the OSGi framework calls when the plugin is started.

`touch code/src/com/osgi/rcp/Activator.java`

## MyThread ##
Also create the thread class (which the Activator class). 

`touch code/src/com/osgi/rcp/MyThread.java `

# Compile #
From within in the code folder, compile the Java classes by running

`javac -cp ../org.eclipse.osgi_3.12.50.v20170928-1321.jar -d ./bin src/com/osgi/rcp/Activator.java src/com/osgi/rcp/MyThread.java`

# Manifest file #
Inside the code/src folder create the manifest.

`touch code/src/MANIFEST.MF`

`Manifest-Version: 1.0`
`Bundle-ManifestVersion: 2`
`Bundle-Name: Rcp`
`Bundle-SymbolicName: com.osgi.rcp`
`Bundle-Version: 1.0.0.qualifier`
`Bundle-Activator: com.osgi.rcp.Activator`
`Bundle-Vendor: OSGI`
`Bundle-RequiredExecutionEnvironment: JavaSE-1.8`
`Import-Package: org.osgi.framework;version="1.3.0"`
`Bundle-ActivationPolicy: lazy`

# Create JAR #
Again from within the code folder, run jar

`jar cfm  com.osgi.rcp_1.0.0.201802171416.jar src/MANIFEST.MF -C bin/ .`

Optional, copy the jar to the plugins folder.

# Console #
Navigate to the base folder of the project. To start the Equinox OSGi console, at the command prompt type

`java -jar org.eclipse.osgi.jar -console`

# Install #
To install the plugin, from within the OSGi console type (an absolute path might be required?)

`install file:////absolute/path/to/plugins/com.osgi.rcp.jar`

# Run #
After installing the plugin, an id (the bundle id) is displayed. To start the plugin, at the console prompt type start following by the id.

`start 1`

# Stop #
Use the stop command followed by the bundle id.

`stop 1`

# References #
* How to start osgi console (Equinox) https://stackoverflow.com/questions/25733843/how-to-start-osgi-console-equinox
* OSGi Modularity - Tutorial http://www.vogella.com/tutorials/OSGi/article.html
