# Lists 
Lists are server side collections, saved queries or subsets of other collections.  

A list is a resource type that contains list metadata as well as a link to the items collection.  The items collection is the actual list resources.

## Attributes

| Name          | Type      | Description
|-----------    |-----------|--------------
|identifiers    |Identifier[]	|An array of identifiers
|name		    |string     |Name of list
|description	|string		|A description of a list
|type	        |string     |A string description of the type of resources, eg "events"
|is_dynamic		|bool		|A boolean value that indicates if the list is static or dynamic

## Collections
| Name          | Type      | Description
|-----------    |-----------|--------------
| items			|Type[]*	|A collection of items in the list 

# Scenarios
## Get the list of lists

    GET /api/v1/lists

    200 OK
    Content-Type: application/json

    {
      "total_pages": 1,
      "page": 1,
      "total_records": 1,
      "_embedded": {
        "lists": [
          {
          	"id" : "1",
			"name" : "Ref74 Supporters",
			"description" : "The set of all supporters for Ref74",
			"type" : "osdi:people",
			"is_dynamic" : false,
			"total_members" 3043, # computed field
			"_links" : {
				"self" : {
					"href" : "api/v1/list/1"
				},
				"members" : {
					"href" : "api/v1/people?list=1",
				}
			}
		   },
          {
          	"id" : "2",
			"name" : "Ref74 Donors",
			"description" : "The set of all 2012 donors for Ref74",
			"type" : "osdi:people",
			"is_dynamic" : false,
			"total_members" 3043, # computed field
			"_links" : {
				"self" : {
					"href" : "api/v1/list/2"
				},
				"members" : {
					"href" : "",
				}
			}
		   }


      "_links": {
        "self": {
          "href": "http://osdi-prototype.herokuapp.com/api/v1/lists"
        },
      }
    }

### Get a list
  	GET /api/v1/list/1

  	200 OK
    Content-Type: application/json

  	{
  			"id" : 1,
			"name" : "Ref74 Supporters",
			"description" : "The set of all supporters for Ref74",
			"type" : "osdi:people",
			"total_members" 3043, # computed field
			"is_dynamic" : false,
			"created": datetime,
			"updated": datetime,
			"_links" : {
				"osdi:members" : {
					"href" : "api/v1/people?list=1",
				}
			}
	}

### Create a new list
	POST /api/v1/lists

	{
		"name": "Ref74 Volunteers",
		"type": "osdi:people",
		"description": "A list containing all of our volunteers"
	}

### Add a person to a list
	POST /api/v1/list/1/members

	Content-Type: application/json

	{	
		"data" : Person object
	}

	OR

	{
		"identifier" : "osdi:12345"
	}

	OR

	{
		"guid" : "c1e1d0d0-b562-0130-dc7c-168c51e904de"
	}

### Remove a person from a list
	DELETE /api/v1/list/1/members/12345

### Get members of a list

	GET /api/v1/people?list=1

	OR

	GET /api/v1/list/1/members

	{
    	"total_pages": 1,
    	"page": 1,
    	"total_records": 1,
    	"type": "osdi:people",
    	"_embedded" : {
    		"osdi:people" : [
	    		{
	    			"first_name": "Beyonce",
	    			...
	    		},
	    		...
	    	]
    	},
    	"_links": {
        	"self": {
          		"href": "http://osdi-prototype.herokuapp.com/api/v1/list/1/members"
        	},
        	"osdi:list": {
        		"href": "http://osdi-prototype.herokuapp.com/api/v1/list/1/"
        	}
      	}
    }