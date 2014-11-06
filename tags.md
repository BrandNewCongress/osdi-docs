---
layout: default
title: "Tags"
---

# Tags
Tags are binary pieces of information that apply to individual people.

|Name   |Type   |Description
|---    |---    |---
|name   |string |name of tag
|description    |string |plaintext meaning of the tag

# Tagging
Taggings link an individual person or other item type to a specific tag.  For example: a tagging links a tag to a person or event.

|Name   	|Type   |Description
|---    	|---    |---
|resource-type  |link | The tagged item
|item_type | string | The type of resource to use as a key in links collection. eg "osdi:person"
|tag    	|link |The tag itself

# Scenarios

## Create a new tag

To create a tag, send a json document containing the tag name and description

### Request

> curl -X POST -d @tagcreate.json http://api.opensupporter.org/api/v1/tags

```
/* tagcreate.json */
{
     "name" : "acme-team",
     "description" : "Indicates a member of the acme team"
}
```

### Response

```
{
  "name": "acme-team",
  "description": "Indicates a member of the acme team",
  "updated_at": "2014-04-18T19:15:31Z",
  "created_at": "2014-04-18T19:15:31Z",
  "_embedded": {
  },
  "_links": {
    "self": {
      "href": "http://api.opensupporter.org/api/v1/tags/8"
    }
  }
}
```

## Finding a tag reference for use in tagging by using odata query

> curl -v -G --data-urlencode "filter=name eq 'acme-team'" "http://localhost:3000/api/v1/tags"

### Response
```
{
  "per_page": 1,
  "page": 1,
  "total_records": 1,
  "_embedded": {
    "osdi:tags": [
      {
        "name": "acme-team",
        "description": "Indicates a member of the acme team",
        "updated_at": "2014-04-18T19:15:31Z",
        "created_at": "2014-04-18T19:15:31Z",
        "_embedded": {
        },
        "_links": {
          "self": {
            "href": "http://api.opensupporter.org/api/v1/tags/8"
          }
        }
      }
    ]
  },
  "_links": {
    "self": {
      "href": "http://api.opensupporter.org/api/v1/tags"
    }
  }
}
```

## Add a tagging (Implied tagged_item)
Lets tag a user with the new tag
User: Martha Stewart, url: http://api.opensupporter.org/api/v1/people/69/taggings

> curl -X POST -d @../taggingcreate.json http://api.opensupporter.org/api/v1/people/69/taggings


### Request
```
{
     "_links" : {
          "osdi:tag" : {
               "href" : "http://api.opensupporter.org/api/v1/tags/8"
          }
     }
}
```

### Response

```
{
  "updated_at": "2014-04-18T20:01:13Z",
  "created_at": "2014-04-18T20:01:13Z",
  "item_type" : "osdi:person"
  "_embedded": {
    "osdi:tag": {
      "name": "acme-team",
      "description": "Indicates a member of the acme team",
      "updated_at": "2014-04-18T19:15:31Z",
      "created_at": "2014-04-18T19:15:31Z",
      "_embedded": {
      },
      "_links": {
        "self": {
          "href": "http://api.opensupporter.org/api/v1/tags/8"
        }
      }
    }
  },
  "_links": {
    "self": {
      "href": "http://api.opensupporter.org/api/v1/taggings/5"
    },
    "osdi:tag": {
      "href": "http://api.opensupporter.org/api/v1/tags/8"
    },
    "osdi:person": {
      "href": "http://api.opensupporter.org/api/v1/people/69"
    }
  }
}
```
