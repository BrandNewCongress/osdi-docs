---
layout: default
title: Canvassing Efforts
---

# Canvassing Effort

This page defines the Canvassing Effort resource.

Canvassing Efforts represent specific canvassing/phone banking events planned for a specific time period. The resource contains information about start and end time, people to be canvassed or called, and a [Script](scripts.html) that is used for the effort. 

### Sections

* [Endpoints and URL structures](#endpoints-and-url-structures)
* [Fields](#fields)
    * [Common Fields](#common-fields)
    * [Script Fields](#effort-fields) 
    * [Links](#links)
* [Related Resources](#related-resources)
* [Scenarios](#scenarios)
    * [Scenario: Retrieving a collection of Canvassing Effort resources (GET)](#scenario-retrieving-a-collection-of-canvassing-effort-resources-get)
    * [Scenario: Retrieving an individual Canvassing Effort resource (GET)](#scenario-retrieving-an-individual-canvassing-effort-resource-get)
    * [Scenario: Creating a new Canvassing Effort (POST)](#scenario-creating-a-new-canvassing-effort-post)
    * [Scenario: Modifying a Canvassing Effort (PUT)](#scenario-modifying-a-canvassing-effort-put)
    * [Scenario: Deleting a Canvassing Effort (DELETE)](#scenario-deleting-a-canvassing-effort-delete)
    * [Scenario: Retrieving a collection of targeted People resources (GET)](#scenario-retrieving-a-collection-of-targeted-people-resources-get) 
    * [Scenario: Assigning a collection of targeted People resources (POST)](#scenario-assigning-a-collection-of-targeted-people-resources-post) 
    * [Scenario: Adding a collection of targeted People resources (PUT)](#scenario-adding-a-collection-of-targeted-people-resources-put)
    * [Scenario: Removing a collection of targeted People resources (DELETE)](#scenario-removing-a-collection-of-targeted-people-resources-delete) 
    * [Scenario: Retrieving a collection of Canvass resources (GET)](#scenario-retrieving-a-collection-of-canvass-resources-get)
    * [Scenario: Retrieving a collection of canvassers People resources (GET)](#scenario-retrieving-a-collection-of-canvassers-people-resources-get)
    * [Scenario: Assigning a collection of canvassers People resources (POST)](#scenario-assigning-a-collection-of-canvassers-people-resources-post) 
    * [Scenario: Adding a collection of canvassers People resources (PUT)](#scenario-adding-a-collection-of-canvassers-people-resources-put)
    * [Scenario: Removing a collection of canvassers People resources (DELETE)](#scenario-removing-a-collection-of-canvassers-people-resources-delete) 


{% include endpoints_and_url_structures.md %}

The link relation label for an Canvassing Effort resource is ```osdi:canvassing_effort``` for a single Canvassing Effort resource or ```osdi:canvassing_efforts``` for a collection of Canvassing Effort resources.

_[Back to top...](#)_


## Fields

{% include fields_intro.md %}

{% include global_fields.md %}

_[Back to top...](#)_

### Canvassign Effort Fields

| Name          | Type                | Description
| -----------   | -----------         | --------------
|origin_system      |string     |A human readable identifier of the system where this effort was created. (ex: "OSDI System")
|name               |string     |The name of the Canvassing Effort. Intended for administrative display rather than a public title, though may be shown to a user.
|title              |string     |The title of the Canvassing Effort. Intended for public display rather than administrative purposes.
|description        |string     |A description of the Canvassing Effort, usually displayed publicly. May contain text and/or HTML.
|summary            |string     |A text-only single paragraph summarizing the effort. Shown on listing pages that have more than titles, but not enough room for full description.
|start_time        |string     |The start date and time for the Canvassing Effort.
|end_time        |string     |The end date and time for the Canvassing Effort.
|type           |string      |The type of the Canvassing Effort "in-person","phone banking",etc 

_[Back to top...](#)_

### Links

{% include links_intro.md %}

| Name          | Type       | Description
|-----------    |----------- |-----------
|self           |[Canvassing Effort*](canvassing_efforts.html)    |A self-referential link to the canvassing effort.
|creator        |[Person*](people.html)         |A link to a single Person resource representing the creator of the Canvassing Effort.
|modified_by    |[Person* ](people.html)        |A link to a Person resource representing the last editor of this Canvassing Effort.
|people  |[Person[]*](people.html)  |A link to the collection of targeted People resources for this canvassing effort.
|canvassers  |[Person[]*](people.html)  |A link to the collection of canvassers represented by People resources for this canvassing effort.
|script  |[Script*](script.html) | A link to the script associated with the canvassing effort

_[Back to top...](#)_


## Related Resources

* [Person](people.html)
* [Script](scripts.html)
* [Canvass](canvasses.html)


_[Back to top...](#)_


## Scenarios

{% include scenarios_intro.md %}

### Scenario: Retrieving a collection of Canvassing Effort resources (GET)

Canvassing Effort resources are sometimes presented as collections of canvassing efforts. For example, calling the canvassing_efforts endpoint will return a collection of all the canvassing efforts stored in the system's database associated with your api key.

#### Request

```javascript
GET https://osdi-sample-system.org/api/v1/canvassing_efforts/

Header:
OSDI-API-Token:[your api key here]
```

#### Response

```javascript
200 OK

Content-Type: application/hal+json
Cache-Control: max-age=0, private, must-revalidate

{
    "total_pages": 10,
    "per_page": 25,
    "page": 1,
    "total_records": 250,
    "_links": {
        "next": {
            "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts?page=2"
        },
        "osdi:canvassing_efforts": [
            {
                "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3"
            },
            {
                "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/1efc3644-af25-4253-90b8-a0baf12dbd1e"
            },
            //(truncated for brevity)
        ],
        "curies": [
            {
                "name": "osdi",
                "href": "https://osdi-sample-system.org/docs/v1/{rel}",
                "templated": true
            }
        ],
        "self": {
            "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts"
        }
    },
    "_embedded":
    {
        "osdi:canvassing_efforts": [
            {
                "identifiers": [
                    "osdi_sample_system:a91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bca",
                    "foreign_system:1"
                ],
                "origin_system": "OSDI Sample System",
                "created_date": "2014-03-20T21:04:31Z",
                "modified_date": "2014-03-20T21:04:31Z",
                "name": "Effort 1",
                "title": "Team 1",
                "description": "Effort 1 for Team 1",
                "summary": "Effort 1 for Team 1",
                "start_time": "2016-02-19T8:00:00Z",
                "end_time": "2016-02-20T8:00:00Z",
                "type": "canvassing",
                "_links": {
                    "self": {
                        "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3"
                    },
                    "osdi:creator": {
                        "href": "https://osdi-sample-system.org/api/v1/people/65345d7d-cd24-466a-a698-4a7686ef684f"
                    },
                    "osdi:modified_by": {
                        "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29"
                    },
                    "osdi:people" : {
                            "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/people"
                    },
                    "osdi:script" : {
                            "href": "https://osdi-sample-system.org/api/v1/script/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0ba3"
                    }, 
                     "osdi:canvassers" : {
                        "href":"https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/canvassers"
                    }
                }
            },
            {
                "identifiers": [
                    "osdi_sample_system:a91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bca",
                    "foreign_system:1"
                ],
                "origin_system": "OSDI Sample System",
                "created_date": "2014-03-20T21:04:31Z",
                "modified_date": "2014-03-20T21:04:31Z",
                "name": "Effort 2",
                "title": "Team 1",
                "description": "Effort 2 for Team 1",
                "summary": "Effort 2 for Team 1",
                "start_time": "2016-02-19T8:00:00Z",
                "end_time": "2016-02-20T8:00:00Z",
                "type": "canvassing",
                "_links": {
                    "self": {
                        "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3"
                    },
                    "osdi:creator": {
                        "href": "https://osdi-sample-system.org/api/v1/people/65345d7d-cd24-466a-a698-4a7686ef684f"
                    },
                    "osdi:modified_by": {
                        "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29"
                    },
                    "osdi:people" : {
                            "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/people"
                    },
                    "osdi:script" : {
                            "href": "https://osdi-sample-system.org/api/v1/script/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0ba3"
                    }, 
                     "osdi:canvassers" : {
                        "href" : "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/canvassers"
                    }
                }
            },   
            //truncated for brevity
        ]
    }
}
``` 

_[Back to top...](#)_       

### Scenario: Retrieving an individual Canvassing Effort resource (GET)

Calling an individual Canvassing Effort resource will return the resource directly.

#### Request

```javascript
GET https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0baa

Header:
OSDI-API-Token:[your api key here]
```

#### Response

```javascript
200 OK

Content-Type: application/hal+json
Cache-Control: max-age=0, private, must-revalidate
 {
    "identifiers": [
        "osdi_sample_system:a91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bca",
        "foreign_system:1"
    ],
    "origin_system": "OSDI Sample System",
    "created_date": "2014-03-20T21:04:31Z",
    "modified_date": "2014-03-20T21:04:31Z",
    "name": "Effort 2",
    "title": "Team 1",
    "description": "Effort 2 for Team 1",
    "summary": "Effort 2 for Team 1",
    "start_time": "2016-02-19T8:00:00Z",
    "end_time": "2016-02-20T8:00:00Z",
    "type": "in-person",
    "_links": {
        "self": {
            "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3"
        },
        "osdi:creator": {
            "href": "https://osdi-sample-system.org/api/v1/people/65345d7d-cd24-466a-a698-4a7686ef684f"
        },
        "osdi:modified_by": {
            "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29"
        },
        "osdi:people" : {
                "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/people"
        },
        "osdi:script" : {
                "href": "https://osdi-sample-system.org/api/v1/script/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0ba3"
        }, 
         "osdi:canvassers" : {
            "href":"https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/canvassers"
         }
    }
}
```


_[Back to top...](#)_


### Scenario: Creating a new Canvassing Effort (POST)

Posting to the effort collection endpoint will allow you to create a new effort. The response is the new effort that was created. While each implementing system will require different fields, any optional fields not included in a post operation should not be set at all by the receiving system, or should be set to default values.

#### Request

```javascript
POST https://osdi-sample-system.org/api/v1/canvassing_efforts/

Header:
OSDI-API-Token:[your api key here]

{
    "identifiers": [
        "foreign_system:1"
    ],
    "origin_system": "OSDI Sample System",
    "name": "Effort 2",
    "title": "Team 1",
    "description": "Effort 2 for Team 1",
    "summary": "Effort 2 for Team 1",
    "start_time": "2016-02-19T8:00:00Z",
    "end_time": "2016-02-20T8:00:00Z",
    "type": "in-person",
    "_links": {
        "osdi:script": {
            "href": "https://osdi-sample-system.org/api/v1/script/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0ba3"
        }
    }
}

```

#### Response

```javascript
200 OK

Content-Type: application/hal+json
Cache-Control: max-age=0, private, must-revalidate
{
    "identifiers": [
        "osdi_sample_system:a91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bca",
        "foreign_system:1"
    ],
    "origin_system": "OSDI Sample System",
    "created_date": "2014-03-20T21:04:31Z",
    "modified_date": "2014-03-20T21:04:31Z",
    "name": "Effort 2",
    "title": "Team 1",
    "description": "Effort 2 for Team 1",
    "summary": "Effort 2 for Team 1",
    "start_time": "2016-02-19T8:00:00Z",
    "end_time": "2016-02-20T8:00:00Z",
    "type": "in-person",
    "_links": {
        "self": {
            "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3"
        },
        "osdi:creator": {
            "href": "https://osdi-sample-system.org/api/v1/people/65345d7d-cd24-466a-a698-4a7686ef684f"
        },
        "osdi:modified_by": {
            "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29"
        },
        "osdi:people" : {
                "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/people"
        },
        "osdi:script" : {
                "href": "https://osdi-sample-system.org/api/v1/script/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0ba3"
        }, 
         "osdi:canvassers" : {
                "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/canvassers"
        }
    }
}
```

_[Back to top...](#)_


### Scenario: Modifying a Canvassing Effort (PUT)

You can update an effort by calling a PUT operation on that effort's endpoint. Your PUT should contain fields that you want to update. Missing fields will be ignored by the receiving system. Systems may also ignore PUT values, depending on whether fields you are trying to modify are read-only or not. You may set an attribute to nil by including the attribute using `nil` for value.

{% include array_warning.md %}

#### Request

```javascript
PUT https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0baa

Header:
OSDI-API-Token:[your api key here]

{
    "name": "Effort 2",
    "title": "Canvassing Effort 2"
}

```

#### Response
```javascript
200 OK

Content-Type: application/hal+json
Cache-Control: max-age=0, private, must-revalidate
{
    "identifiers": [
        "osdi_sample_system:a91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bca",
        "foreign_system:1"
    ],
    "origin_system": "OSDI Sample System",
    "created_date": "2014-03-20T21:04:31Z",
    "modified_date": "2014-03-20T21:04:31Z",
    "name": "Effort 2",
    "title": "Team 1",
    "description": "Effort 2 for Team 1",
    "summary": "Effort 2 for Team 1",
    "start_time": "2016-02-19T8:00:00Z",
    "end_time": "2016-02-20T8:00:00Z",
    "type": "in-person",
    "_links": {
        "self": {
            "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3"
        },
        "osdi:creator": {
            "href": "https://osdi-sample-system.org/api/v1/people/65345d7d-cd24-466a-a698-4a7686ef684f"
        },
        "osdi:modified_by": {
            "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29"
        },
        "osdi:people" : {
                "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/people"
        },
        "osdi:script" : {
                "href": "https://osdi-sample-system.org/api/v1/script/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0ba3"
        }, 
         "osdi:canvassers" : {
                "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/canvassers"
        }
    }
}
```


_[Back to top...](#)_


### Scenario: Deleting a Canvassing Effort (DELETE)

You may delete an effort by calling the DELETE command on the Canvassing Effort's endpoint.

#### Request

```javascript
DELETE https://osdi-sample-system.org/api/v1/canvassing_efforts/d32fcdd6-7366-466d-a3b8-7e0d87c3cd8b

Header:
OSDI-API-Token:[your api key here]
```

#### Response

```javascript
200 OK

Content-Type: application/hal+json
Cache-Control: max-age=0, private, must-revalidate

{
    "notice": "This canvassing effort was successfully deleted."
}
```

_[Back to top...](#)_

### Scenario: Retrieving a collection of targeted People resources (GET)


#### Request

```javascript
GET https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0baa/people

Header:
OSDI-API-Token:[your api key here]
```

#### Response

```javascript
200 OK

Content-Type: application/hal+json
Cache-Control: max-age=0, private, must-revalidate

{
    "total_pages": 88,
    "per_page": 25,
    "page": 1,
    "total_records": 2188,
    "_links": {
        "next": {
            "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0baa/people?page=2"
        },
        "osdi:people": [
            {
                "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3"
            },
            {
                "href": "https://osdi-sample-system.org/api/v1/people/1efc3644-af25-4253-90b8-a0baf12dbd1e"
            },
            //(truncated for brevity)
        ],
        "curies": [
            {
                "name": "osdi",
                "href": "https://osdi-sample-system.org/docs/v1/{rel}",
                "templated": true
            }
        ],
        "self": {
            "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0baa/people"
        }
    },
    "_embedded": {
        "osdi:people": [
            {
                "identifiers": [
                    "osdi_sample_system:d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3",
                    "foreign_system:1"
                ],
                "origin_system": "OSDI Sample System",
                "created_date": "2014-03-20T21:04:31Z",
                "modified_date": "2014-03-20T21:04:31Z",
                "given_name": "John",
                "family_name": "Smith",
                "honorific_prefix": "Mr.",
                "honorific_suffix": "Ph.D",
                "additional_name": "Scott",
                "gender": "Male",
                "gender_identity": "Male",
                "party_identification": "Democratic",
                "source": "october_canvass",
                "birthdate": {
                    "month": 6,
                    "day": 2,
                    "year": 1973
                },
                "ethnicities": [
                    "African American"
                ],
                "languages_spoken": [
                    "en",
                    "fr"
                ],
                "employer": "Acme Corp",
                "employer_address": {
                    "venue": "Bull Hall",
                    "address_lines": [
                        "123 Acme Street",
                        "Suite 400"
                    ],
                    "locality": "New Yorkhaven",
                    "region": "NY",
                    "postal_code": "10001",
                    "country": "US",
                    "language": "en",
                    "location": {
                        "latitude": 38.9382,
                        "longitude": -77.3349,
                        "accuracy": "Rooftop"
                    },
                    "status": "Verified"
                },
                "occupation": "Accountant",
                "postal_addresses": [
                    {
                        "primary": true,
                        "address_type": "Home",
                        "address_lines": [
                            "1900 Pennsylvania Ave"
                        ],
                        "locality": "Washington",
                        "region": "DC",
                        "postal_code": "20009",
                        "country": "US",
                        "language": "en",
                        "location": {
                            "latitude": 38.919,
                            "longitude": -77.0379,
                            "accuracy": "Rooftop"
                        }
                    }
                ],
                "email_addresses": [
                    {
                        "primary": true,
                        "address": "johnsmith@mail.com",
                        "address_type": "Personal",
                        "status": "subscribed"
                    }
                ],
                "phone_numbers": [
                    {
                        "primary": true,
                        "number": "11234567890",
                        "extension": "432",
                        "description": "Worksite line",
                        "number_type": "Work",
                        "operator": "ATT",
                        "country": "US",
                        "sms_capable": false,
                        "do_not_call": true
                    }
                ],
                "profiles": [
                    {
                        "provider": "Facebook",
                        "id": "john.doe.1234",
                        "url": "https://facebook.com/john.doe"
                    },
                    {
                        "provider": "Twitter",
                        "id": "eds34d8j2kddfd45",
                        "url": "https://twitter.com/johndoe",
                        "handle": "johndoe"
                    }
                ],
                "custom_fields": {
                    "is_volunteer": "true",
                    "most_important_issue": "Equal pay",
                    "union_member": "true"
                },
                "_links": {
                    "self": {
                        "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3"
                    },
                    "osdi:answers": {
                        "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/answers"
                    },
                    "osdi:attendance": {
                        "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/attendance"
                    },
                    "osdi:signatures": {
                        "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/signatures"
                    },
                    "osdi:submissions": {
                        "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/submissions"
                    },
                    "osdi:donations": {
                        "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/donations"
                    },
                    "osdi:outreaches": {
                        "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/outreaches"
                    },
                    "osdi:taggings": {
                        "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/taggings"
                    },
                    "osdi:items": {
                        "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/items"
                    },
                    "osdi:record_canvass_helper": {
                        "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/record_canvass_helper"
                    }
                }
            },
            {
                "given_name": "Jane",
                "family_name": "Doe",
                "identifiers": [
                    "osdi_sample_system:1efc3644-af25-4253-90b8-a0baf12dbd1e"
                ],
                "origin_system": "OSDI Sample System",
                "created_date": "2014-03-20T20:44:13Z",
                "modified_date": "2014-03-20T20:44:13Z",
                "email_addresses": [
                    {
                        "primary": true,
                        "address": "janedoe@mail.com",
                        "status": "unsubscribed"
                    }
                ],
                "postal_addresses": [
                    {
                        "primary": true,
                        "locality": "Washington",
                        "region": "DC",
                        "postal_code": "20009",
                        "country": "US",
                        "language": "en",
                        "location": {
                            "latitude": 38.919,
                            "longitude": -77.0379,
                            "accuracy": "Approximate"
                        }
                    }
                ],
                "_links": {
                    "self": {
                        "href": "https://osdi-sample-system.org/api/v1/people/1efc3644-af25-4253-90b8-a0baf12dbd1e"
                    },
                    "osdi:answers": {
                        "href": "https://osdi-sample-system.org/api/v1/people/1efc3644-af25-4253-90b8-a0baf12dbd1e/answers"
                    },
                    "osdi:attendance": {
                        "href": "https://osdi-sample-system.org/api/v1/people/1efc3644-af25-4253-90b8-a0baf12dbd1e/attendance"
                    },
                    "osdi:signatures": {
                        "href": "https://osdi-sample-system.org/api/v1/people/1efc3644-af25-4253-90b8-a0baf12dbd1e/signatures"
                    },
                    "osdi:submissions": {
                        "href": "https://osdi-sample-system.org/api/v1/people/1efc3644-af25-4253-90b8-a0baf12dbd1e/submissions"
                    },
                    "osdi:donations": {
                        "href": "https://osdi-sample-system.org/api/v1/people/1efc3644-af25-4253-90b8-a0baf12dbd1e/donations"
                    },
                    "osdi:outreaches": {
                        "href": "https://osdi-sample-system.org/api/v1/people/1efc3644-af25-4253-90b8-a0baf12dbd1e/outreaches"
                    },
                    "osdi:taggings": {
                        "href": "https://osdi-sample-system.org/api/v1/people/1efc3644-af25-4253-90b8-a0baf12dbd1e/taggings"
                    },
                    "osdi:items": {
                        "href": "https://osdi-sample-system.org/api/v1/people/1efc3644-af25-4253-90b8-a0baf12dbd1e/items"
                    },
                    "osdi:record_canvass_helper": {
                        "href": "https://osdi-sample-system.org/api/v1/people/1efc3644-af25-4253-90b8-a0baf12dbd1e/record_canvass_helper"
                    }
                }
            },
            //(truncated for brevity)
        ]
    }
}
``` 


_[Back to top...](#)_

### Scenario: Assigning a collection of targeted People resources (POST)

Posting to the people collection of an individual effort collection endpoint will allow you to assign new people to the canvassing effort. The response will contain a list of people that were assigned.

#### Request

```javascript
POST https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0baa/people

Header:
OSDI-API-Token:[your api key here]

{
    "_links": {
        "osdi:people" : [
            { 
                "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3"
            }, 
            { 
                "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc4"
            }, 
            // truncated for brevity
        ]
}

```

#### Response

```javascript
200 OK

Content-Type: application/hal+json
Cache-Control: max-age=0, private, must-revalidate
{
    "total_pages": 88,
    "per_page": 25,
    "page": 1,
    "total_records": 2188,
    "_links": {
        "next": {
            "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0baa/people?page=2"
        },
        "osdi:people": [
            {
                "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3"
            },
            {
                "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc4"
            },
            //(truncated for brevity)
        ],
        "curies": [
            {
                "name": "osdi",
                "href": "https://osdi-sample-system.org/docs/v1/{rel}",
                "templated": true
            }
        ],
        "self": {
            "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0baa/people"
        }
    }
}
``` 

_[Back to top...](#)_

### Scenario: Adding a collection of targeted People resources (PUT)

Executing a PUT request to the people collection of an individual effort collection endpoint will allow you to add new people to the canvassing effort. The response will contain a list of people that were assigned.

#### Request

```javascript
PUT https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0baa/people

Header:
OSDI-API-Token:[your api key here]

{
    "_links": {
        "osdi:people" : [
            { 
                "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc5"
            }, 
            { 
                "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc6"
            }
        ]
}

```

#### Response

```javascript
200 OK

Content-Type: application/hal+json
Cache-Control: max-age=0, private, must-revalidate
{
    "total_pages": 88,
    "per_page": 25,
    "page": 1,
    "total_records": 2188,
    "_links": {
        "next": {
            "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0baa/people?page=2"
        },
        "osdi:people": [
            {
                "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3"
            },
            {
                "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc4"
            },
            //(truncated for brevity)
            {
                "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc5"
            },
            {
                "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc6"
            },
        ],
        "curies": [
            {
                "name": "osdi",
                "href": "https://osdi-sample-system.org/docs/v1/{rel}",
                "templated": true
            }
        ],
        "self": {
            "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0baa/people"
        }
    }
}
``` 

_[Back to top...](#)_


### Scenario: Removing a collection of targeted People resources (DELETE)

You may unassign people from a canvassing effort by calling the DELETE command on the Canvassing Effort's people collection endpoint. If no people are provided in the request, all of the people are cleared.

#### Request

```javascript
DELETE https://osdi-sample-system.org/api/v1/canvassing_efforts/d32fcdd6-7366-466d-a3b8-7e0d87c3cd8b

Header:
OSDI-API-Token:[your api key here]

{
    "_links": {
        "osdi:people" : [
            { 
                "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc5"
            }, 
            { 
                "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc6"
            }
        ]
}
```


#### Response

```javascript
200 OK

Content-Type: application/hal+json
Cache-Control: max-age=0, private, must-revalidate

{
    "notice": "People were unassigned."
}
```

_[Back to top...](#)_

### Scenario: Retrieving a collection of Canvass resources (GET)

Calling this endpoint allows consumers to see a efforts's canvass history.

#### Request

```javascript
GET https://osdi-sample-system.org/api/v1/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0baa/canvasses

Header:
OSDI-API-Token:[your api key here]
```

#### Response

```javascript
200 OK

Content-Type: application/hal+json
Cache-Control: max-age=0, private, must-revalidate

{
    "total_pages": 10,
    "per_page": 25,
    "page": 1,
    "total_records": 250,
    "_links": {
        "next": {
            "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0baa/canvasses?page=2"
        },
        "osdi:canvasses": [
            {
                "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3"
            },
            {
                "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses/1efc3644-af25-4253-90b8-a0baf12dbd1e"
            },
            //(truncated for brevity)
        ],
        "curies": [
            {
                "name": "osdi",
                "href": "https://osdi-sample-system.org/docs/v1/{rel}",
                "templated": true
            }
        ],
        "self": {
            "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0baa/canvasses"
        }
    },
    "_embedded": {
        "osdi:canvasses": [
            {
                "identifiers": [
                    "osdi_sample_system:d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3",
                    "foreign_system:1"
                ],
                "origin_system": "OSDI Sample System",
                "created_date": "2014-03-20T21:04:31Z",
                "modified_date": "2014-03-20T21:04:31Z",
                "action_date": "2014-03-18T11:02:15Z",
                "contact_type": "in-person",
                "input_type": "mobile",
                "success": false,
                "status_code": "not-home",
                "_links": {
                    "self": {
                        "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3"
                    },
                    "osdi:canvasser": {
                        "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316444"
                    },
                    "osdi:target": {
                        "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29"
                    },
                    "osdi:answers": {
                        "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/answers"
                    },
                    "osdi:taggings": {
                        "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/taggings"
                    }
                }
            },
            {
                "identifiers": [
                    "osdi_sample_system:d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bcf",
                    "foreign_system:1"
                ],
                "origin_system": "OSDI Sample System",
                "created_date": "2014-03-20T21:04:31Z",
                "modified_date": "2014-03-20T21:04:31Z",
                "action_date": "2014-03-18T11:02:15Z",
                "contact_type": "phoneCall",
                "input_type": "paper",
                "success": true,
                "status_code": "",
                "_links": {
                    "self": {
                        "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bcf"
                    },
                    "osdi:canvasser": {
                        "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316444"
                    },
                    "osdi:target": {
                        "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29"
                    },
                    "osdi:answers": {
                            "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bcf/answers"
                    },
                    "osdi:taggings": {
                            "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bcf/taggings"
                    }
                }
            },
            //(truncated for brevity)
        ]
    }
}
``` 

_[Back to top...](#)_ 


### Scenario: Retrieving a collection of canvassers People resources (GET)


#### Request

```javascript
GET https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0baa/canvassers

Header:
OSDI-API-Token:[your api key here]
```

#### Response

```javascript
200 OK

Content-Type: application/hal+json
Cache-Control: max-age=0, private, must-revalidate

{
    "total_pages": 88,
    "per_page": 25,
    "page": 1,
    "total_records": 2188,
    "_links": {
        "next": {
            "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0baa/canvassers?page=2"
        },
        "osdi:people": [
            {
                "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3"
            },
            {
                "href": "https://osdi-sample-system.org/api/v1/people/1efc3644-af25-4253-90b8-a0baf12dbd1e"
            },
            //(truncated for brevity)
        ],
        "curies": [
            {
                "name": "osdi",
                "href": "https://osdi-sample-system.org/docs/v1/{rel}",
                "templated": true
            }
        ],
        "self": {
            "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0baa/canvassers"
        }
    },
    "_embedded": {
        "osdi:people": [
            {
                "identifiers": [
                    "osdi_sample_system:d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3",
                    "foreign_system:1"
                ],
                "origin_system": "OSDI Sample System",
                "created_date": "2014-03-20T21:04:31Z",
                "modified_date": "2014-03-20T21:04:31Z",
                "given_name": "John",
                "family_name": "Smith",
                "honorific_prefix": "Mr.",
                "honorific_suffix": "Ph.D",
                "additional_name": "Scott",
                "gender": "Male",
                "gender_identity": "Male",
                "party_identification": "Democratic",
                "source": "october_canvass",
                "birthdate": {
                    "month": 6,
                    "day": 2,
                    "year": 1973
                },
                "ethnicities": [
                    "African American"
                ],
                "languages_spoken": [
                    "en",
                    "fr"
                ],
                "employer": "Acme Corp",
                "employer_address": {
                    "venue": "Bull Hall",
                    "address_lines": [
                        "123 Acme Street",
                        "Suite 400"
                    ],
                    "locality": "New Yorkhaven",
                    "region": "NY",
                    "postal_code": "10001",
                    "country": "US",
                    "language": "en",
                    "location": {
                        "latitude": 38.9382,
                        "longitude": -77.3349,
                        "accuracy": "Rooftop"
                    },
                    "status": "Verified"
                },
                "occupation": "Accountant",
                "postal_addresses": [
                    {
                        "primary": true,
                        "address_type": "Home",
                        "address_lines": [
                            "1900 Pennsylvania Ave"
                        ],
                        "locality": "Washington",
                        "region": "DC",
                        "postal_code": "20009",
                        "country": "US",
                        "language": "en",
                        "location": {
                            "latitude": 38.919,
                            "longitude": -77.0379,
                            "accuracy": "Rooftop"
                        }
                    }
                ],
                "email_addresses": [
                    {
                        "primary": true,
                        "address": "johnsmith@mail.com",
                        "address_type": "Personal",
                        "status": "subscribed"
                    }
                ],
                "phone_numbers": [
                    {
                        "primary": true,
                        "number": "11234567890",
                        "extension": "432",
                        "description": "Worksite line",
                        "number_type": "Work",
                        "operator": "ATT",
                        "country": "US",
                        "sms_capable": false,
                        "do_not_call": true
                    }
                ],
                "profiles": [
                    {
                        "provider": "Facebook",
                        "id": "john.doe.1234",
                        "url": "https://facebook.com/john.doe"
                    },
                    {
                        "provider": "Twitter",
                        "id": "eds34d8j2kddfd45",
                        "url": "https://twitter.com/johndoe",
                        "handle": "johndoe"
                    }
                ],
                "custom_fields": {
                    "is_volunteer": "true",
                    "most_important_issue": "Equal pay",
                    "union_member": "true"
                },
                "_links": {
                    "self": {
                        "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3"
                    },
                    "osdi:answers": {
                        "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/answers"
                    },
                    "osdi:attendance": {
                        "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/attendance"
                    },
                    "osdi:signatures": {
                        "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/signatures"
                    },
                    "osdi:submissions": {
                        "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/submissions"
                    },
                    "osdi:donations": {
                        "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/donations"
                    },
                    "osdi:outreaches": {
                        "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/outreaches"
                    },
                    "osdi:taggings": {
                        "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/taggings"
                    },
                    "osdi:items": {
                        "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/items"
                    },
                    "osdi:record_canvass_helper": {
                        "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/record_canvass_helper"
                    }
                }
            },
            {
                "given_name": "Jane",
                "family_name": "Doe",
                "identifiers": [
                    "osdi_sample_system:1efc3644-af25-4253-90b8-a0baf12dbd1e"
                ],
                "origin_system": "OSDI Sample System",
                "created_date": "2014-03-20T20:44:13Z",
                "modified_date": "2014-03-20T20:44:13Z",
                "email_addresses": [
                    {
                        "primary": true,
                        "address": "janedoe@mail.com",
                        "status": "unsubscribed"
                    }
                ],
                "postal_addresses": [
                    {
                        "primary": true,
                        "locality": "Washington",
                        "region": "DC",
                        "postal_code": "20009",
                        "country": "US",
                        "language": "en",
                        "location": {
                            "latitude": 38.919,
                            "longitude": -77.0379,
                            "accuracy": "Approximate"
                        }
                    }
                ],
                "_links": {
                    "self": {
                        "href": "https://osdi-sample-system.org/api/v1/people/1efc3644-af25-4253-90b8-a0baf12dbd1e"
                    },
                    "osdi:answers": {
                        "href": "https://osdi-sample-system.org/api/v1/people/1efc3644-af25-4253-90b8-a0baf12dbd1e/answers"
                    },
                    "osdi:attendance": {
                        "href": "https://osdi-sample-system.org/api/v1/people/1efc3644-af25-4253-90b8-a0baf12dbd1e/attendance"
                    },
                    "osdi:signatures": {
                        "href": "https://osdi-sample-system.org/api/v1/people/1efc3644-af25-4253-90b8-a0baf12dbd1e/signatures"
                    },
                    "osdi:submissions": {
                        "href": "https://osdi-sample-system.org/api/v1/people/1efc3644-af25-4253-90b8-a0baf12dbd1e/submissions"
                    },
                    "osdi:donations": {
                        "href": "https://osdi-sample-system.org/api/v1/people/1efc3644-af25-4253-90b8-a0baf12dbd1e/donations"
                    },
                    "osdi:outreaches": {
                        "href": "https://osdi-sample-system.org/api/v1/people/1efc3644-af25-4253-90b8-a0baf12dbd1e/outreaches"
                    },
                    "osdi:taggings": {
                        "href": "https://osdi-sample-system.org/api/v1/people/1efc3644-af25-4253-90b8-a0baf12dbd1e/taggings"
                    },
                    "osdi:items": {
                        "href": "https://osdi-sample-system.org/api/v1/people/1efc3644-af25-4253-90b8-a0baf12dbd1e/items"
                    },
                    "osdi:record_canvass_helper": {
                        "href": "https://osdi-sample-system.org/api/v1/people/1efc3644-af25-4253-90b8-a0baf12dbd1e/record_canvass_helper"
                    }
                }
            },
            //(truncated for brevity)
        ]
    }
}
``` 


_[Back to top...](#)_     

### Scenario: Assigning a collection of canvassers People resources (POST)

Posting to the canvassers collection of an individual effort collection endpoint will allow you to assign new canvassers to the canvassing effort. The response will contain a list of people that were assigned.

#### Request

```javascript
POST https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0baa/canvassers

Header:
OSDI-API-Token:[your api key here]

{
    "_links": {
        "osdi:people" : [
            { 
                "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3"
            }, 
            { 
                "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc4"
            }, 
            // truncated for brevity
        ]
}

```

#### Response

```javascript
200 OK

Content-Type: application/hal+json
Cache-Control: max-age=0, private, must-revalidate
{
    "total_pages": 88,
    "per_page": 25,
    "page": 1,
    "total_records": 2188,
    "_links": {
        "next": {
            "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0baa/canvassers?page=2"
        },
        "osdi:people": [
            {
                "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3"
            },
            {
                "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc4"
            },
            //(truncated for brevity)
        ],
        "curies": [
            {
                "name": "osdi",
                "href": "https://osdi-sample-system.org/docs/v1/{rel}",
                "templated": true
            }
        ],
        "self": {
            "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0baa/canvassers"
        }
    }
}
``` 

_[Back to top...](#)_

### Scenario: Adding a collection of canvassers People resources (PUT)

Calling the DELETE command on the canvassers collection of an individual effort endpoint will allow you to add new canvassers to the canvassing effort. The response will contain a list of people that were assigned.

#### Request

```javascript
PUT https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0baa/canvassers

Header:
OSDI-API-Token:[your api key here]

{
    "_links": {
        "osdi:people" : [
            { 
                "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc5"
            }, 
            { 
                "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc6"
            }
        ]
}

```

#### Response

```javascript
200 OK

Content-Type: application/hal+json
Cache-Control: max-age=0, private, must-revalidate
{
    "total_pages": 88,
    "per_page": 25,
    "page": 1,
    "total_records": 2188,
    "_links": {
        "next": {
            "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0baa/canvassers?page=2"
        },
        "osdi:people": [
            {
                "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3"
            },
            {
                "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc4"
            },
            //(truncated for brevity)
            {
                "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc5"
            },
            {
                "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc6"
            },
        ],
        "curies": [
            {
                "name": "osdi",
                "href": "https://osdi-sample-system.org/docs/v1/{rel}",
                "templated": true
            }
        ],
        "self": {
            "href": "https://osdi-sample-system.org/api/v1/canvassing_efforts/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0baa/canvassers"
        }
    }
}
``` 

_[Back to top...](#)_


### Scenario: Removing a collection of targeted People resources (DELETE)

You may unassign canvassers from a canvassing effort by calling the DELETE command on the Canvassing Effort's canvassers collection endpoint. If no people are provided in the request, all of the canvassers are cleared.

#### Request

```javascript
DELETE https://osdi-sample-system.org/api/v1/canvassing_efforts/d32fcdd6-7366-466d-a3b8-7e0d87c3cd8b/canvassers

Header:
OSDI-API-Token:[your api key here]

{
    "_links": {
        "osdi:people" : [
            { 
                "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc5"
            }, 
            { 
                "href": "https://osdi-sample-system.org/api/v1/people/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc6"
            }
        ]
}
```


#### Response

```javascript
200 OK

Content-Type: application/hal+json
Cache-Control: max-age=0, private, must-revalidate

{
    "notice": "People were unassigned."
}
```

_[Back to top...](#)_ 

