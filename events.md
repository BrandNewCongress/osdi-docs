# Events

This page defines Events, EventRSVPS

{% include global_fields.md %}

## Events

| Name		| Type		| Description
|-----------|-----------|------------------
| id		| string	| Identifier of the event
| status	| string	| Status of the event.  Possible values are:
|			|			| "confirmed" The Event is confirmed (Default)
|			|			| "tentative"
|			|			| "cancelled"
| created_date	| datetime	| Date and Time of creation
| modified_date	| datetime	| Date and Time of update
| origin_system | string | Human readable text identifiying the system where this event was created.
| title	| string	| title of event 
| name	| string	| name of event
| description| string	| description of the event
| instructions| string | Instructions for the event after attendees have RSVPed
| summary	| string	| summary of event
| browser_url | string | A URL string pointing to the publicly available petition page on the web
| location	| Address	| A single instance of Address representing the location of the event
| creator	| Person*	| A single instance of Person representing the creator of the event
| organizer | Person*	| A single instance of Person representing the organizer of the event
| start_date		| datetime	| start time for the event
| end_date		| datetime	| end time for the event
| all_day_date| date	| date only for all day events
| all_day	| boolean	| true if the event is an all day event
| recurrence| TBD		| TBD
| transparence| string	| Whether the event blocks time on the calendar. Default, can be overridden by a user. Optional. Possible values are:
|			|			| "opaque" - The event blocks time on the calendar. This is the default value.
|			|			| "transparent" - The event does not block time on the calendar.
| visibility| string	| Visibility of the event.  Possible values are
|			|			| "public" visible on public web interfaces
|			|			| "private" not visible on public web interfaces
| attendees	| Attendance[]*| A Collection of Attendance resources
| guestsCanInviteOthers | boolean | Attendees can invite guests to the event
| reminders | list		| a list of reminder elements
| .method	| string	| "email", "sms"
| .minutes	| integer	| number of minutes before the start of the event to send reminder
| capacity  | integer	| the max capacity for attendees of an event
| total_accepted| integer | read-only computed property of attending guests count

## Attendance

| Name		| Type		| Description
|-----------|-----------|------------------
| id		| string	| Identifier
| event		| Event*	| Event that this attendance refers to
| person	| Person*	| Person that is attending the referenced event
| status	| string	| The attendee's response status. Possible values
| 			|			| "declined" The attendee declined
|			|			| "tentative" The attendee tentatively accepted
|			|			| "accepted" The attendee accepted
|			|			| "needs action" The attendee needs help
| attended 	| boolean	| true if the person actually attended
| comment	| string	| An optional comment from the attendee
| invited_by | Person*	| Person that invited this attendee.  This is expected to be used for guests

## Event Guests
To handle guests, additional attendance records are created with the invited_by attribute set to point to the attendee this guest is associated with.

If guest information (such as name, etc) is not given, then the person resource is null.


## Event Attendance Helper
The Event Attendance Helper provides a simple method for registering an RSVP for an event.

The Event Attendance Helper URL can be determined from the donations collection under the "event_attendance_helper" link relation on a specific event resource

The response to a Event Attendance Helper is the full representation of the attendance, with a link to the person resource created and optional embedded resources for person, event or invited_by resource.

Some initial implementations may only support helpers, direct RESTful access may not be supporter.  In those cases,_links may be omitted in responses.

### Parameters
The Event Attendance Helper takes the following parameters in its body
* Inlined Person - A "person" attribute containing any valid attributes of a person resource are valid in the input representation
* Optional Inlined "invited_by" Person - A "person" attribute containing any valid attributes of a person resource are valid in the input representation
* Attendance attributes - any valid Attendance resource attribute

### Example

#### Request
```javascript
POST /api/v1/events/507/event_attendance_helper

{
	"status" : "accepted",
	"comment" : "I can't wait for this event!",

	"person" : {
		"family_name" : "Smith",
		"given_name" : "John",
		"postal_addresses" : [ { "postal_code" : "20009" } ],
		"email_addresses" : [ { "address" : "jsmith@mail.com" } ]
	},
	"invited_by" : { /* optional */
		"family_name" : "Testy",
		"given_name" : "McTesterson",
		"postal_addresses" : [ { "postal_code" : "20009" } ],
		"email_addresses" : [ { "address" : "testy@mctesterson.com" } ]
	}

} 
````
#### Response
````
{
	"status" : "accepted",
	"comment" : "I can't wait for this event!",
	"attended" : false,
	
	"_links" : {
		"event" : { "href" : "http://server/event/507" },
		"person" : { "href" : "http://server/person/4" },
		"invited_by" : { "href" : "http://server/person/5" }
	}
}



````

# Single resource retrieval

## default embed policy
> TBD

## JSON Representation

	{
	  "id": string,
	  "status": string,
	  "created_date": datetime,
	  "modified_date": datetime,
	  "origin_system": string,
	  "summary": string,
	  "browser_url": string,
	  "description": string,
	  "instructions": string,
	  "_embedded" : {
			"osdi:location" : {
				"venue": "Smith Hall",
				"address1": "430 Erwin Stream",
	            "city": "Altheastad",
	            "state": "FL",
	            "postal_code": "87210-9039",
	            "country_code": "UK",
	            "address_type": "Home",
	            "lat": 44,
	            "lng": 40,
	            "accuracy": "Rooftop",
	            "address_status": "Verified",
	            "primary": true,
	            "_links": {
	              "self": {
	                "href": "http://api.opensupporter.org/api/v1/addresses/42"
	              },
	              "person": {
	                "href": "http://api.opensupporter.org/api/v1/people/21"
	              }
			"osdi:creator" :   {
	            {
		        "first_name": "Lurline",
		        "last_name": "Glover",
		        "middle_name": "Titus",
		        "email": "test-1@example.com",
		        "gender": "Male",
		        "gender_identity": "Male",
		        "twitter_handle": "@Lurline_Glover",
		        "guid": "c199e4a0-b562-0130-dc7c-168c51e904de",
		        "_embedded": {
		          "primary_address": {
		            "address1": "430 Erwin Stream",
		             ...
		          },

			"osdi:organizer" :   {
	            {
		        "first_name": "Lurline",
		        "last_name": "Glover",
		        "middle_name": "Titus",
		        "email": "test-1@example.com",
		        "gender": "Male",
		        "gender_identity": "Male",
		        "twitter_handle": "@Lurline_Glover",
		        "guid": "c199e4a0-b562-0130-dc7c-168c51e904de",
		        "_embedded": {
		          "primary_address": {
		            "address1": "430 Erwin Stream",
		             ...
		          },
			},
	  "start_date": datetime,
	  "end_date" : datetime,
      "all_day" : boolean,
      "all_day_date" : date,

	  "transparency": string,
	  "visibility": string,
	  "attendance_count" : integer,
	  "_embedded" : {
	       "attendance": [
                {
				  "total_records": 80,
					"_links" : {
					    "curies": [{ "name": "osdi", "href": "http://api.opensupporter.org/docs/v1/{rel}", "templated": true }],
						"osdi:event" : {"href" : uri }
						"osdi:person" : {"href" : uri }
					},
					"_embedded" : {
						"osdi:person": {
				        "first_name": "Lurline",
				        "last_name": "Glover",
				        "middle_name": "Titus",
				        "email": "test-1@example.com",
				        "gender": "Male",
				        "gender_identity": "Male",
				        "twitter_handle": "@Lurline_Glover",
				        "guid": "c199e4a0-b562-0130-dc7c-168c51e904de",
				        "_embedded": {
				          "primary_address": {
				            "address1": "430 Erwin Stream",
				             ...
				          }

              			}
					}
					]
	  "guestsCanInviteOthers": boolean,
	  "privateCopy": boolean,
	  "locked": boolean,
	  "reminders": [
			{
				method : "email",
				minutes : "1440"
	        },
			{
				method : "sms",
				minutes : "120"
	        }

	    ],
	  },
	  "_links" : {
	   "curies": [{ "name": "osdi", "href": "http://api.opensupporter.org/docs/v1/{rel}", "templated": true }],
       "self": { "href" : uri },
       "osdi:attendance" : { "href" : uri }
       "osdi:location" : { "href" : uri }
	   "osdi:organizer" : { "href" : uri }
	   "osdi:creator" : { "href" : uri }
      }

	}


# Collection Response

## Default embed policy
When retrieving a collection of events, by default, the full event resource is returned but:

* Included: creator, organizer, location
* Excluded: Attendance collection

All 1:1 relationships are contained in the response

Excluded resources can be accessed directly by de-referencing the appropriate link in the _links collection

## JSON Representation
> TBD
