---
node_id: 2032
title: The RackConnect v2.0 API
type: article
created_date: '2012-08-21'
created_by: Juan Perez
last_modified_date: '2016-01-06'
last_modified_by: Catherine Richardson
product: RackConnect
product_url: rackconnect
---

**APPLIES TO:** RackConnect v2.0

The RackConnect API provides a way for you to access certain read-only
information about your Cloud Servers and their RackConnect
configuration. The RackConnect API is available to all customers who can
manage their RackConnect configurations
through [MyRackspace ](https://my.rackspace.com/)Portal interface.

You can use the RackConnect API to access the following information:

-   When you are scripting or automating any post-server-build
    configuration tasks, you can query the API to learn when RackConnect
    automation is done configuring your server. If you have this
    information, you can avoid performing tasks that conflict with
    the automation.

-   When you are setting up the network configuration manually on your
    Cloud Server (when the Configure Network Stack automation feature is
    disabled on your Cloud Account), the API will return the gateway IP
    address to be used as the default gateway on your server. You can
    use this address to correctly configure the Cloud Server
    network stack.

-   When you want to determine the specific actions that the automation
    will perform against one of your Cloud Servers, you can view the
    status of each automation feature for a specific Cloud Server.

**Note:** In addition to using the RackConnect API, you can now use the
Cloud Servers API to query the RackConnect automation status of your
next-generation Cloud Servers. The benefit of using the Cloud Servers
API is that you do not need to perform the query from the same Cloud
Server you want the status of. The limitations of this method are that
only the RackConnect automation status is available, and this method is
compatible only with next-generation Cloud Servers. If you are
interested in this method, see the following article: [How to
programmatically determine the RackConnect v2.0 Automation Status of
your Cloud
Servers.](/how-to/how-to-programmatically-determine-the-rackconnect-v20-automation-status-of-your-cloud)

API Basics
----------

The RackConnect API is exposed via regional endpoints. Use the endpoint
that matches the region where your Cloud Server resides.

-   https://dfw.api.rackconnect.rackspace.com
-   https://hkg.api.rackconnect.rackspace.com
-   https://iad.api.rackconnect.rackspace.com
-   https://lon.api.rackconnect.rackspace.com
-   https://ord.api.rackconnect.rackspace.com
-   https://syd.api.rackconnect.rackspace.com

Note: The URLs for each API operation include a version number. When
future versions of the calls available, this article will be updated. It
is important to note that this version number does not relate to the
version of RackConnect that you are using.

Authentication
--------------

The RackConnect API authenticates all requests based on the source IP
address that is initiating the request. The API endpoints are exposed
only on the Private (ServiceNet) network, so the Private (ServiceNet)
network IP address of your Cloud Server is used to determine the source
of the request and to respond with the appropriate information. API
responses are limited to information only about the specific Cloud
Server from which you are querying. It is important to note that
hypervisor-level protections are in place that prevent these IP
addresses from being spoofed, ensuring that the instance making the
request to the API endpoint is, in fact, your Cloud Server.

*Note: You cannot query the RackConnect API from outside of your Cloud
Server.*

Rate Limiting
-------------

There is a limit of 30 requests per minute from each of your Cloud
Servers. If you exceed the number of allowed requests per minute, you
will receive an HTTP 403 (Forbidden) response code. The counter resets
each minute.

Operations
----------

The following operations are supported by the API. The format query
string parameter is optional on each request. If it is not supplied, the
default response format is used.

**GET /v1/automation\_status?format={format}**

-   Response Formats: text, JSON, XML
-   Default Response Format: text
-   Expected HTTP Response Code: 200
-   Description: Returns the automation status of the Cloud Server
    (DEPLOYING, DEPLOYED, or FAILED)

**GET /v1/automation\_status/details?format={format}**

-   Response Formats: JSON, XML
-   Default Response Format: JSON
-   Expected HTTP Response Code: 200
-   Description: Returns the automation status of the Cloud Server
    (DEPLOYING, DEPLOYED, or FAILED) and an array of Cloud Server tasks
    with their associated statuses

**GET /v1/gateway\_ip?format={format}**

-   Response Formats: text, JSON, XML
-   Default Response Format: text
-   Expected HTTP Response Code: 200
-   Description: Returns the gateway IP address for the Cloud Server. If
    the gateway IP address has not yet been assigned, an HTTP 404
    response code is returned

**GET /v1/automation\_features?format={format}**

-   Response Formats: JSON, XML
-   Default Response Format: JSON
-   Expected HTTP Response Code: 200
-   Description: Returns a collection of automation features and their
    associated statuses for the Cloud Server

API Example
-----------

The following example uses curl to retrieve the automation status.
Alternatively, you can use a web browser to query the RackConnect API.

Request:

    $ curl https://dfw.api.rackconnect.rackspace.com/v1/automation_status?format=text

Response:

    DEPLOYED

Previous Article: [RackConnect Compatibility with Next-Gen Cloud Server
Images](/how-to/rackconnect-v20-compatibility-with-cloud-servers-images)

