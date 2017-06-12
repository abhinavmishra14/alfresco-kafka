# Alfresco Kafka Integration

This is an Alfresco repository tier AMP that will publish events such as create, update, and delete to an Apache Kafka
topic.

Events are generated using an Alfresco behavior that is bound to `onCreateNode`, `onUpdateProperties`, and `beforeDeleteNode`.

## Build

This project uses the Alfresco Maven SDK to build. The output is an AMP that can be installed into your Alfresco WAR
using the Alfresco Module Management Tool (MMT).

## Configure

There are two configurable settings:

* Topic: Set the topic that the events should be published to. (Default: alfresco-node-events)
* Bootstrap Servers: Set the Kafka servers to publish to. (Default: localhost:9092)

Both of these settings are in the AMPs service-context.xml Spring config file. (TODO: Move these settings to a-g.p.)

## Example

This section includes an example of the event JSON. The events are all the same format with the exception of the event
type, which can be one of:

* CREATE
* UPDATE
* DELETE
* PING

Here is what an event looks like:

    {
	    "nodeRef": "3f375925-fa87-4e34-9734-b98bed2d483f",
	    "eventType": "CREATE",
	    "path": "/{http://www.alfresco.org/model/application/1.0}company_home/{http://www.alfresco.org/model/site/1.0}sites/{http://www.alfresco.org/model/content/1.0}swsdp/{http://www.alfresco.org/model/content/1.0}documentLibrary/{http://www.alfresco.org/model/content/1.0}test/{http://www.alfresco.org/model/content/1.0}test2.txt",
        "created": 1497282061322,
        "modified": 1497282061322,
        "creator": "admin",
        "modifier": "admin",
        "mimetype": "text/plain",
        "contentType": "content",
        "size": 128,
        "parent": "06a154e3-4014-4a55-adfa-5e55040fae2d"
	}

For folders, the size and mimetype are null.

    {
    	"nodeRef": "82f0aeae-c74e-4fd8-a55c-f6d9f40d3e1a",
    	"eventType": "UPDATE",
    	"path": "/{http://www.alfresco.org/model/application/1.0}company_home/{http://www.alfresco.org/model/site/1.0}sites/{http://www.alfresco.org/model/content/1.0}swsdp/{http://www.alfresco.org/model/content/1.0}documentLibrary/{http://www.alfresco.org/model/content/1.0}test/{http://www.alfresco.org/model/content/1.0}test1",
    	"created": 1497280801902,
    	"modified": 1497281940257,
    	"creator": "admin",
    	"modifier": "admin",
    	"mimetype": null,
    	"contentType": "folder",
    	"size": null,
    	"parent": "06a154e3-4014-4a55-adfa-5e55040fae2d"
    }

