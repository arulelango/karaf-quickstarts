keycloak-camel-blueprint: demonstrates a bundle with Camel route that uses `undertow-keycloak` component
==========================
Author: Fuse Team  
Level: Intermediate  
Technologies: Keycloak, PAX-WEB, Blueprint, Camel
Summary: a bundle with Camel route that uses `undertow-keycloak` component
Target Product: Fuse  
Source: <https://github.com/jboss-fuse/karaf-quickstarts/tree/7.x.redhat-7-x/security/keycloak/keycloak-camel-blueprint>


What is it?
-----------
This quickstart demonstrates how to create an OSGi bundle that starts Camel route using `undertow-keycloak` component.


System requirements
-------------------
Before building and running this quick start you need:

* Maven 3.5.0 or higher
* JDK 1.8
* Red Hat Fuse 7


Build and Deploy the Quickstart
-------------------------------

To build the quick start:

1. Change your working directory to `keycloak-camel-blueprint` directory.
2. Run `mvn clean install` to build the quickstart.
3. Start Red Hat Fuse 7 by running bin/fuse (on Linux) or bin\fuse.bat (on Windows).
4. In the Red Hat Fuse console, enter the following commands to install required Keycloak features

        feature:repo-add mvn:org.keycloak/keycloak-osgi-features/${version.org.keycloak}/xml/features
        feature:install -v keycloak-pax-http-undertow

5. In the Red Hat Fuse console, enter the following command to install `keycloak-camel-blueprint` quickstart:

        install -s mvn:org.jboss.fuse.quickstarts.security/keycloak-camel-blueprint/${project.version}

6. There's no need to create a Keycloak configuration inside `etc/` directory, as with this quickstart it's embedded
inside the bundle.


Use the bundle
--------------

This time we won't browse to any URL using web browser. After installing `keycloak-camel-blueprint` bundle, we'll
have a Camel route exposing an endpoint that expectes `Bearer` authentication. This means we need valid OAuth2
token to authenticate.

The quickstart includes `org.jboss.fuse.quickstarts.security.keycloak.camel.CamelClientTest` unit test that shows
(in Java code) the OAuth2 flow required to securely connect to and endpoint exposed by Camel route.

The unit test can be run inside `keycloak-camel-blueprint` directory:

    16:26 $ mvn test -Pqtest
    [INFO] Scanning for projects...
    [INFO] 
    [INFO] ----< org.jboss.fuse.quickstarts.security:keycloak-camel-blueprint >----
    [INFO] Building Red Hat Fuse :: Quickstarts :: Security :: Keycloak :: Camel/Blueprint 7.7.0.fuse-780012
    [INFO] -------------------------------[ bundle ]-------------------------------
    [INFO] 
    [INFO] --- maven-resources-plugin:3.0.2:resources (default-resources) @ keycloak-camel-blueprint ---
    [INFO] Using 'UTF-8' encoding to copy filtered resources.
    [INFO] Copying 2 resources
    [INFO] 
    [INFO] --- maven-compiler-plugin:3.7.0:compile (default-compile) @ keycloak-camel-blueprint ---
    [INFO] Nothing to compile - all classes are up to date
    [INFO] 
    [INFO] --- maven-bundle-plugin:3.5.1:manifest (bundle-manifest) @ keycloak-camel-blueprint ---
    [INFO] 
    [INFO] --- maven-resources-plugin:3.0.2:testResources (default-testResources) @ keycloak-camel-blueprint ---
    [INFO] Using 'UTF-8' encoding to copy filtered resources.
    [INFO] Copying 1 resource
    [INFO] 
    [INFO] --- maven-compiler-plugin:3.7.0:testCompile (default-testCompile) @ keycloak-camel-blueprint ---
    [INFO] Nothing to compile - all classes are up to date
    [INFO] 
    [INFO] --- maven-surefire-plugin:2.20.1:test (default-test) @ keycloak-camel-blueprint ---
    [INFO] 
    [INFO] -------------------------------------------------------
    [INFO]  T E S T S
    [INFO] -------------------------------------------------------
    [INFO] Running org.jboss.fuse.quickstarts.security.keycloak.camel.CamelClientTest
    16:26:18 DEBUG [org.apache.http.wire] : http-outgoing-0 >> "POST /auth/realms/fuse7karaf/protocol/openid-connect/token HTTP/1.1[\r][\n]"
    16:26:18 DEBUG [org.apache.http.wire] : http-outgoing-0 >> "Authorization: Basic Y2FtZWwtdW5kZXJ0b3ctZW5kcG9pbnQ6ZjU5MWE4YWUtNWE4Mi00MGRlLTkxOTAtZWE4NGNlY2EwNWE3[\r][\n]"
    16:26:18 DEBUG [org.apache.http.wire] : http-outgoing-0 >> "Content-Length: 52[\r][\n]"
    16:26:18 DEBUG [org.apache.http.wire] : http-outgoing-0 >> "Content-Type: application/x-www-form-urlencoded[\r][\n]"
    16:26:18 DEBUG [org.apache.http.wire] : http-outgoing-0 >> "Host: localhost:8180[\r][\n]"
    16:26:18 DEBUG [org.apache.http.wire] : http-outgoing-0 >> "Connection: Keep-Alive[\r][\n]"
    16:26:18 DEBUG [org.apache.http.wire] : http-outgoing-0 >> "User-Agent: Apache-HttpClient/4.5.5 (Java/1.8.0_261)[\r][\n]"
    16:26:18 DEBUG [org.apache.http.wire] : http-outgoing-0 >> "[\r][\n]"
    16:26:18 DEBUG [org.apache.http.wire] : http-outgoing-0 >> "grant_type=password&username=admin&password=passw0rd"
    16:26:19 DEBUG [org.apache.http.wire] : http-outgoing-0 << "HTTP/1.1 200 OK[\r][\n]"
    16:26:19 DEBUG [org.apache.http.wire] : http-outgoing-0 << "Connection: keep-alive[\r][\n]"
    16:26:19 DEBUG [org.apache.http.wire] : http-outgoing-0 << "Cache-Control: no-store[\r][\n]"
    16:26:19 DEBUG [org.apache.http.wire] : http-outgoing-0 << "Set-Cookie: KC_RESTART=; Version=1; Expires=Thu, 01-Jan-1970 00:00:10 GMT; Max-Age=0; Path=/auth/realms/fuse7karaf/; HttpOnly[\r][\n]"
    16:26:19 DEBUG [org.apache.http.wire] : http-outgoing-0 << "Pragma: no-cache[\r][\n]"
    16:26:19 DEBUG [org.apache.http.wire] : http-outgoing-0 << "Content-Type: application/json[\r][\n]"
    16:26:19 DEBUG [org.apache.http.wire] : http-outgoing-0 << "Content-Length: 3944[\r][\n]"
    16:26:19 DEBUG [org.apache.http.wire] : http-outgoing-0 << "Date: Fri, 21 Aug 2020 14:26:19 GMT[\r][\n]"
    16:26:19 DEBUG [org.apache.http.wire] : http-outgoing-0 << "[\r][\n]"
    16:26:19 DEBUG [org.apache.http.wire] : http-outgoing-0 << "{"access_token":"<token>","expires_in":300,"refresh_expires_in":1800,"refresh_token":"<token>","token_type":"bearer","not-before-policy":0,"session_state":"b9e01cd3-56c7-4ba6-bc5f-dead940afb51","scope":"profile email"}"
    16:26:19 INFO [org.jboss.fuse.quickstarts.security.keycloak.camel.CamelClientTest] : token: <token>
    16:26:19 DEBUG [org.apache.http.wire] : http-outgoing-1 >> "GET /admin-camel-endpoint HTTP/1.1[\r][\n]"
    16:26:19 DEBUG [org.apache.http.wire] : http-outgoing-1 >> "Authorization: Bearer <token>[\r][\n]"
    16:26:19 DEBUG [org.apache.http.wire] : http-outgoing-1 >> "Host: localhost:8383[\r][\n]"
    16:26:19 DEBUG [org.apache.http.wire] : http-outgoing-1 >> "Connection: Keep-Alive[\r][\n]"
    16:26:19 DEBUG [org.apache.http.wire] : http-outgoing-1 >> "User-Agent: Apache-HttpClient/4.5.5 (Java/1.8.0_261)[\r][\n]"
    16:26:19 DEBUG [org.apache.http.wire] : http-outgoing-1 >> "[\r][\n]"
    16:26:19 DEBUG [org.apache.http.wire] : http-outgoing-1 << "HTTP/1.1 200 OK[\r][\n]"
    16:26:19 DEBUG [org.apache.http.wire] : http-outgoing-1 << "Connection: keep-alive[\r][\n]"
    16:26:19 DEBUG [org.apache.http.wire] : http-outgoing-1 << "Content-Length: 40[\r][\n]"
    16:26:19 DEBUG [org.apache.http.wire] : http-outgoing-1 << "Date: Fri, 21 Aug 2020 14:26:19 GMT[\r][\n]"
    16:26:19 DEBUG [org.apache.http.wire] : http-outgoing-1 << "[\r][\n]"
    16:26:19 DEBUG [org.apache.http.wire] : http-outgoing-1 << "Hello admin! Your full name is John Doe."
    16:26:19 INFO [org.jboss.fuse.quickstarts.security.keycloak.camel.CamelClientTest] : response: Hello admin! Your full name is John Doe.
    [INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 1.426 s - in org.jboss.fuse.quickstarts.security.keycloak.camel.CamelClientTest
    [INFO] 
    [INFO] Results:
    [INFO] 
    [INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0
    [INFO] 
    [INFO] ------------------------------------------------------------------------
    [INFO] BUILD SUCCESS
    [INFO] ------------------------------------------------------------------------
    [INFO] Total time:  5.355 s
    [INFO] Finished at: 2020-08-21T16:26:19+02:00
    [INFO] ------------------------------------------------------------------------


Undeploy the Bundle
-------------------

To stop and undeploy the bundle in Fuse:

1. Enter `bundle:list -s` command to retrieve your bundle id and symbolic name
2. To stop and uninstall the bundle enter

        bundle:uninstall <id>

    or (uninstall by symbolic name)

        bundle:uninstall keycloak-camel-blueprint
