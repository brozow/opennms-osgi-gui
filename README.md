opennms-osgi-gui
================

Sample App for adding an OSGi GUI to opennms maps menu

This sample app builds a VERY BASIC Vaadin app as an OSGi bundle.

This app uses blueprint to register itself with the OpenNMS web
container at the /example url (making its URL http://<server>:8980/opennms/example)

You can try this out as follows:

1. Checkout this repository and build it on your system
   ```
   $ MAVEN_OPTS=-Xmx1g mvn install
   ```
   This will build your vaadin bundle and copy it into your mvn local
   repository.  This will also install a feature descriptor file that you
   can use with opennms to install an entire feature that is made up of
   many OSGi bundles.

2. Next you need to make sure the bundle and feature file are added
   the OSGi bundle repository that OpenNMS uses to find OSGi bundles.
   This repository has the same format as an mvn repository
   ```
   $ cp -r ~/.m2/repository/org/opennms/example <opennms.home>/system/org/opennms
   ```
3. Now log into the OpenNMS's osgi terminal. (Note: OpenNMS must be running for this to work)
   ```
   $ ssh -p 8101 admin@localhost
   ```
4. Now you needs to tell OpenNMS to add your feature file to the list
   of features the OpenNMS knows about

   ```
   opennms> features:addurl mvn:org.opennms.example/vaadin-osgi/1.0-SNAPSHOT/xml/feature
   ```

5. Once you have completed this you can do 

   ```
   opennms> feature:list | grep vaadin

   [uninstalled] [1.0-SNAPSHOT   ] vaadin-osgi-example		      vaadin-osgi-example     Example Vaadin GUI install with OSGi
   [installed  ] [1.13.1-SNAPSHOT] vaadin-snmp-events-and-metrics	opennms-1.13.1-SNAPSHOT OpenNMS Features Admin UI for SNMP Events and Metrics
   [installed  ] [1.13.1-SNAPSHOT] vaadin-node-maps		         opennms-1.13.1-SNAPSHOT OpenNMS Features Node Maps
   [installed  ] [1.13.1-SNAPSHOT] vaadin				               opennms-1.13.1-SNAPSHOT OpenNMS Features :: Topology :: Vaadin + Dependencies
   [installed  ] [1.13.1-SNAPSHOT] vaadin-dashboard		         opennms-1.13.1-SNAPSHOT OpenNMS Features Dashboard
   ```
   As you can see the vaadin-osgi-example is listed

6. In install and run the example issue the following command

   ```
   opennms> feature:install -v vaadin-osgi-example
   ```
7. Now log into the OpenNMS GUI.  After logging in, you can visit the url for the example. [http://localhost:8980/opennms/example](http://localhost:8980/opennms/example).

   You should see the 'Click Me' button and if you click it you will see a 'Thank you'






