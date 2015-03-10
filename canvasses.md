---
layout: default
title: Canvasses
---

# Canvasses

This page defines the Canvass resource.

A canvass occurs when one person attempts to contact another person for the purpose of obtaining data about that person.  For example, a canvasser visits a voter's home and asks the voter whether she intends to vote in the next election; or, a campaign staffer calls a volunteer to ask whether he intends to attend the candidate's upcoming kick-off event.  The person being contacted is known as the "target" of the canvass, and the target may have [Answers](answers.html) or [Taggings](taggings.html) applied to them as a result of the canvass.  Alternatively, the target may have a non-canvass result (e.g. "not home") applied to them.

It is not necessary to create a Canvass in order to create an Answer or Tagging for a Person.  However, a Canvass can provide useful information about how the Answer or Tagging was collected, which may prove valuable for future organizing purposes.

### Sections

* [Endpoints and URL structures](#endpoints-and-url-structures)
* [Fields](#fields)
    * [Common Fields](#common-fields)
    * [Canvass Fields](#canvass-fields)
    * [Links](#links)
* [Helpers](#helpers)
* [Related Resources](#related-resources)
* [Scenarios](#scenarios)
    * [Scenario: Retrieving a collection of Canvass resources (GET)](#scenario-retrieving-a-collection-of-canvass-resources-for-a-person-get)
    * [Scenario: Retrieving an individual Canvass resource (GET)](#scenario-retrieving-an-individual-canvass-resource-get)
    * [Scenario: Retrieving Answers for an individual Canvass resource (GET)](#scenario-retrieving-answers-for-an-individual-canvass-resource-get)
    * [Scenario: Retrieving Taggings for an individual Canvass resource (GET)](#scenario-retrieving-taggings-for-an-individual-canvass-resource-get)
    * [Scenario: Creating a new Canvass (POST)](#scenario-creating-a-new-canvass-post)
    * [Scenario: Modifying a Canvass (PUT)](#scenario-modifying-a-canvass-put)
    * [Scenario: Deleting a Canvass (DELETE)](#scenario-deleting-a-canvass-delete)


{% include endpoints_and_url_structures.md %}

The link relation label for an Canvass resource is ```osdi:canvass``` for a single Canvass resource or ```osdi:canvasses``` for a collection of Canvass resources.

_[Back to top...](#)_


## Fields

{% include fields_intro.md %}

{% include global_fields.md %}

_[Back to top...](#)_


### Canvass Fields

| Name          | Type      | Description
|-----------    |-----------|--------------
|origin_system		|string     |A human readable identifier of the system where this canvass was created. (ex: "OSDI System")
|action_date		|string		|The date and time the canvass was attempted.
| contact_type  | string | A code indicating the method by which the person was contacted.  For example: "in-person"
| input_type    | string | A code indicating the method by which the canvass is being input into the system. For example: "mobile"
| result_code  | string | A code indicating the status of the contact attempt.  For example: "not-home" indicates that the contact failed because the target was not home, while "success" indicates that the target was contacted successfully.  An empty or missing value for result_code should be assumed to mean that the contact was successful.

_[Back to top...](#)_



### Links

{% include links_intro.md %}

|Name          	|Type		|Description
|-----------    |-----------|--------------
|self			|[Canvass*](canvasses.html)	|A self-referential link to the canvass.
|target		|[Person](people.html)  |A link to a single Person resource representing the person who was contacted.
|answers      |[Answer*](answers.html) | Zero or more answers to [Questions](questions.html) posed during the canvass.
|taggings     |[Tagging*](taggings.html) | Zero or more taggings applied as a result of the canvass.

_[Back to top...](#)_

## Helpers

{% include helpers_intro.md %}

|Name          |Description
|-----------    |-----------
|[record_canvass_helper](record_canvass.html)      |Allows the creation of a Canvass and associated Answers and Taggings.

_[Back to top...](#)_


## Related Resources

* [Question](questions.html)
* [Person](people.html)
* [Answer](answers.html)
* [Tagging](taggings.html)

_[Back to top...](#)_

## Scenarios

{% include scenarios_intro.md %}


### Scenario: Retrieving a collection of Canvass resources for a person (GET)

Calling this endpoint allows consumers to see a person's canvass history.

#### Request

```javascript
GET https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses

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
            "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses?page=2"
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
            "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses"
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
                "result_code": "not-home",
                "_links": {
                    "self": {
                        "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3"
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
                "result_code": "",
                "_links": {
                    "self": {
                        "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bcf"
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

### Scenario: Retrieving an individual Canvass resource (GET)

Calling an individual Canvass resource will return the resource directly, along with all associated fields and appropriate links to additional information about the canvass.

#### Request

```javascript
GET https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3

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
        "osdi_sample_system:d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3",
        "foreign_system:1"
    ],
    "origin_system": "OSDI Sample System",
    "created_date": "2014-03-20T21:04:31Z",
    "modified_date": "2014-03-20T21:04:31Z",
    "action_date": "2014-03-18T11:02:15Z",
    "contact_type": "in-person",
    "input_type": "mobile",
    "result_code": "",
    "_links": {
        "self": {
            "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3"
        },
        "osdi:target": {
            "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29"
        },
        "osdi:answers": {
            "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/answers"
        },
        "osdi:taggings": {
            "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/answers"
        }
    }
}
```

_[Back to top...](#)_

### Scenario: Retrieving Answers for an individual Canvass resource (GET)

Retrieves the Answers that were collected during the Canvass.

#### Request

```javascript
GET https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/answers

Header:
OSDI-API-Token:[your api key here]
```

#### Response

````javascript

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
            "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/answers?page=2"
        },
        "osdi:answers": [
            {
                "href": "https://osdi-sample-system.org/api/v1/questions/c945d6fe-929e-11e3-a2e9-12313d316c29/answers/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3"
            },
            {
                "href": "https://osdi-sample-system.org/api/v1/questions/c945d6fe-929e-11e3-a2e9-12313d316c29/answers/1efc3644-af25-4253-90b8-a0baf12dbd1e"
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
            "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/answers"
        }
    },
    "_embedded": {
        "osdi:answers": [
            {
                "identifiers": [
                    "osdi_sample_system:d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3",
                    "foreign_system:1"
                ],
                "origin_system": "OSDI Sample System",
                "created_date": "2014-03-20T21:04:31Z",
                "modified_date": "2014-03-20T21:04:31Z",
                "action_date": "2014-03-18T11:02:15Z",
                "value": "He's not sure",
                "_links": {
                    "self": {
                        "href": "https://osdi-sample-system.org/api/v1/questions/c945d6fe-929e-11e3-a2e9-12313d316c29/answers/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3"
                    },
                    "osdi:question": {
                        "href": "https://osdi-sample-system.org/api/v1/questions/c945d6fe-929e-11e3-a2e9-12313d316c29"
                    },
                    "osdi:person": {
                        "href": "https://osdi-sample-system.org/api/v1/people/65345d7d-cd24-466a-a698-4a7686ef684f"
                    },
                }
            },
            {
                "identifiers": [
                    "osdi_sample_system:1efc3644-af25-4253-90b8-a0baf12dbd1e"
                ],
                "origin_system": "OSDI Sample System",
                "created_date": "2014-03-20T20:44:13Z",
                "modified_date": "2014-03-20T20:44:13Z",
                "action_date": "2014-03-12T01:45:34Z",
                "responses": [
                    "Y"
                ],
                "_links": {
                    "self": {
                        "href": "https://osdi-sample-system.org/api/v1/questions/c945d6fe-929e-11e3-a2e9-12313d316c29/answers/1efc3644-af25-4253-90b8-a0baf12dbd1e"
                    },
                    "osdi:question": {
                        "href": "https://osdi-sample-system.org/api/v1/questions/c945d6fe-929e-11e3-a2e9-12313d316c29"
                    },
                    "osdi:person": {
                        "href": "https://osdi-sample-system.org/api/v1/people/adb951cb-51f9-420e-b7e6-de953195ec86"
                    }
                }
            },
            //(truncated for brevity)
        ]
    }

````

_[Back to top...](#)_

### Scenario: Retrieving Taggings for an individual Canvass resource (GET)

Retrieves the Taggings that were collected during the Canvass.

#### Request

```javascript
GET https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/taggings

Header:
OSDI-API-Token:[your api key here]
```

#### Response

````javascript

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
            "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/taggings?page=2"
        },
        "osdi:taggings": [
            {
                "href": "https://osdi-sample-system.org/api/v1/tags/c945d6fe-929e-11e3-a2e9-12313d316c29/taggings/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3"
            },
            {
                "href": "https://osdi-sample-system.org/api/v1/tags/c945d6fe-929e-11e3-a2e9-12313d316c29/taggings/1efc3644-af25-4253-90b8-a0baf12dbd1e"
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
            "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3/taggings"
        }
    },
    "_embedded": {
        "osdi:taggings": [
            {
                "identifiers": [
                    "osdi_sample_system:d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3",
                    "foreign_system:1"
                ],
                "origin_system": "OSDI Sample System",
                "created_date": "2014-03-20T21:04:31Z",
                "modified_date": "2014-03-20T21:04:31Z",
                "item_type": "osdi:person",
                "_links": {
                    "self": {
                        "href": "https://osdi-sample-system.org/api/v1/tags/c945d6fe-929e-11e3-a2e9-12313d316c29/taggings/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3"
                    },
                    "osdi:tag": {
                        "href": "https://osdi-sample-system.org/api/v1/tags/c945d6fe-929e-11e3-a2e9-12313d316c29"
                    },
                    "osdi:person": {
                        "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29"
                    }
                }
            },
            {
                "identifiers": [
                    "osdi_sample_system:1efc3644-af25-4253-90b8-a0baf12dbd1e"
                ],
                "origin_system": "OSDI Sample System",
                "created_date": "2014-03-20T20:44:13Z",
                "modified_date": "2014-03-20T20:44:13Z",
                "item_type": "osdi:event",
                "_links": {
                    "self": {
                        "href": "https://osdi-sample-system.org/api/v1/tags/c945d6fe-929e-11e3-a2e9-12313d316c29/taggings/1efc3644-af25-4253-90b8-a0baf12dbd1e"
                    },
                    "osdi:tag": {
                        "href": "https://osdi-sample-system.org/api/v1/tags/c945d6fe-929e-11e3-a2e9-12313d316c29"
                    },
                    "osdi:person": {
                        "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29"
                    }
                }
            },
            //(truncated for brevity)
        ]
    }

````

_[Back to top...](#)_


### Scenario: Creating a new Canvass (POST)

Posting to the Canvasses collection endpoint and including a link to existing Answer and Tagging resource(s) will allow you to create a new canvass that indicates that the indicated Person was canvassed and that the answers and taggings indicated were recorded as a result.  The response is the new canvass that was created.

#### Request

```javascript
POST https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses/

Header:
OSDI-API-Token:[your api key here]

{
    "identifiers": [
        "foreign_system:1"
    ],
    "origin_system": "OpenSupporter",
    "action_date": "2014-03-18T11:02:15Z",
    "contact_type": "in-person",
    "input_type": "mobile",
    "result_code": "",
}
```

#### Response

```javascript
200 OK

Content-Type: application/hal+json
Cache-Control: max-age=0, private, must-revalidate

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
    "input_tinput_typeype": "mobile",
    "result_code": "",
    "_links": {
        "self": {
            "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3"
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
}
```

_[Back to top...](#)_


### Scenario: Modifying a Canvass (PUT)

You can update an Canvass by calling a PUT operation on that canvass's endpoint. Your PUT should contain fields that you want to update. Missing fields will be ignored by the receiving system. Systems may also ignore PUT values, depending on whether fields you are trying to modify are read-only or not. You may set an attribute to nil by including the attribute using `nil` for value.

{% include array_warning.md %}

#### Request

```javascript
PUT https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3

Header:
OSDI-API-Token:[your api key here]

{
    "contact_type": "phoneCall"
}

```

#### Response
```javascript
200 OK

Content-Type: application/hal+json
Cache-Control: max-age=0, private, must-revalidate

{
    "identifiers": [
        "osdi_sample_system:d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3",
        "foreign_system:1"
    ],
    "origin_system": "OSDI Sample System",
    "created_date": "2014-03-20T21:04:31Z",
    "modified_date": "2014-03-20T21:04:31Z",
    "action_date": "2014-03-18T11:02:15Z",
    "contact_type": "phoneCall",
    "input_type": "mobile",
    "result_code": "",
    "_links": {
        "self": {
            "href": "https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses/d91b4b2e-ae0e-4cd3-9ed7-d0ec501b0bc3"
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
}
```

_[Back to top...](#)_


### Scenario: Deleting a Canvass (DELETE)

You may delete a canvass by calling the DELETE command on the canvass's endpoint.

#### Request

```javascript
DELETE https://osdi-sample-system.org/api/v1/people/c945d6fe-929e-11e3-a2e9-12313d316c29/canvasses/d91b4b2e-ae0e-4cd3-9ed7-de9uemdse

Header:
OSDI-API-Token:[your api key here]
```

#### Response

```javascript
200 OK

Content-Type: application/hal+json
Cache-Control: max-age=0, private, must-revalidate

{
    "notice": "This canvass was successfully deleted."
}
```

_[Back to top...](#)_