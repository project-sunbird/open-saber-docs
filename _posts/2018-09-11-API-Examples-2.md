---
date: 2018-09-10
title: API Examples
categories:
  - Documentation
type: Document
showSidebar: true
published: true
nav_ordering: 15
pageTitle: "API Examples"
---

### Open Saber API Examples

#### 1. Create 

This creates a new record in the registry.


```
POST - /create
```

**Request Body**

```

{
	"id": "open-saber.registry.create",
	"ver": "1.0",
	"ets": "11234",
	"params": 
	{
		"did": "",
		"key": "",
		"msgid": ""
	},

	"request": 
	{
		"@context": 
		{
			"rdf": "http://www.w3.org/1999/02/22-rdf-syntax-ns#",
			"rdfs": "http://www.w3.org/2000/01/rdf-schema#",
			"teacher": "http://example.com/voc/teacher/1.0.0/",
			"xsd": "http://www.w3.org/2001/XMLSchema#",
			"@vocab": "http://example.com/voc/teacher/1.0.0/",
		},

		"@type": "Teacher",
		"serialNum": 12,
		"teacherCode": "12234",
		"nationalIdentifier": "1234567890123456",
		"teacherName": "Marvin Pande",
		"gender": {
			"@id": "teacher:GenderTypeCode-MALE"
		},
		"birthDate": 
		{
			"@type": "xsd:date",
			"@value": "1990-12-06"
		},

		"socialCategory": 
		{
			"@id": "teacher:SocialCategoryTypeCode-GENERAL"
		},

		"highestAcademicQualification": 
		{
			"@id": "teacher:AcademicQualificationTypeCode-PHD"
		},

		"highestTeacherQualification": 
		{
			"@id": "teacher:TeacherQualificationTypeCode-MED"
		},

		"yearOfJoiningService": 
		{
			"@type": "xsd:gYear",
			"@value": "2014"
		},

		"teachingRole": 
		{
			"@type": "TeachingRole",
			"teacherType": 
			{
				"@id": "teacher:TeacherTypeCode-HEAD"
			},

			"appointmentType": 
			{
				"@id": "teacher:TeacherAppointmentTypeCode-REGULAR"
			},

			"classesTaught": 
			{
				"@id": "teacher:ClassTypeCode-SECONDARYANDHIGHERSECONDARY"
			},

			"appointedForSubjects": 
			{
				"@id": "teacher:SubjectCode-MATH"
			},

			"mainSubjectsTaught": 
			[
				{
					"@id": "teacher:SubjectCode-PHYSICS"
				},

				{
					"@id": "teacher:SubjectCode-MATH"
				}
			],

			"appointmentYear": 
			{
				"@type": "xsd:gYear",
				"@value": "2015"
			}
		},

		"inServiceTeacherTrainingFromBRC": 
		{
			"@type": "InServiceTeacherTrainingFromBlockResourceCentre",
			"teacher:daysOfInServiceTeacherTraining": {
				"@type": "xsd:decimal",
				"@value":"10"
			}
		},

		"inServiceTeacherTrainingFromCRC": 
		{
			"@type": "InServiceTeacherTrainingFromClusterResourceCentre",
			"teacher:daysOfInServiceTeacherTraining": {
				"@type": "xsd:decimal",
				"@value":"2"
				}
		},

		"inServiceTeacherTrainingFromDIET": 
		{
			"@type": "InServiceTeacherTrainingFromDIET",
			"teacher:daysOfInServiceTeacherTraining": {
				"@type": "xsd:decimal",
				"@value":"5.5"
				}
		},

		"inServiceTeacherTrainingFromOthers": 
		{
			"@type": "InServiceTeacherTrainingFromOthers",
			"teacher:daysOfInServiceTeacherTraining": {
				"@type": "xsd:decimal",
				"@value":"3.5"
				}
		},

		"nonTeachingAssignmentsForAcademicCalendar": 
		{
			"@type": "NonTeachingAssignmentsForAcademicCalendar",
			"teacher:daysOfNonTeachingAssignments": {
				"@type": "xsd:decimal",
				"@value":"6"
				}
		},

		"basicProficiencyLevel": 
		[
			{
				"@type": "BasicProficiencyLevel",
				"proficiencySubject": 
				{
					"@id": "teacher:SubjectCode-MATH"
				},

				"proficiencyAcademicQualification": 
				{
					"@id": "teacher:AcademicQualificationTypeCode-PHD"
				}
			},

			{
				"@type": "BasicProficiencyLevel",
				"proficiencySubject": 
				{
					"@id": "teacher:SubjectCode-ENGLISH"
				},

				"proficiencyAcademicQualification": 
				{
					"@id": "teacher:AcademicQualificationTypeCode-HIGHERSECONDARY"
				}
			},

			{
				"@type": "BasicProficiencyLevel",
				"proficiencySubject": 
				{
					"@id": "teacher:SubjectCode-SOCIALSTUDIES"
				},

				"proficiencyAcademicQualification": 
				{
					"@id": "teacher:AcademicQualificationTypeCode-SECONDARY"
				}
			}
		],

		"disabilityType": 
		{
			"@id": "teacher:DisabilityCode-NA"
		},

		"trainedForChildrenSpecialNeeds": 
		{
			"@id": "teacher:YesNoCode-YES"
		},

		"teacher:trainedinUseOfComputer": 
		{
			"@id": "teacher:YesNoCode-YES"
		}
	}
}
```

**Response**
```
{
  "id": //identifier , e.g. "open-saber.registry.create",
  "ver": //version "1.0",
  "ets": //epoch timestamp in format "YYYY-MM-DDThh:mm:ssZ+/-nn.nn",
  "params": {
    "resmsgid": "",
    "msgid": "",
    "err": "",
    "status": "successful",
    "errmsg": ""
  },
  "result": {              
     "entity": "http://example.com/voc/teacher/1.0.0/38e57c47-3bf5-4320-a94c-de1ad98c5387"
  }
}
```

#### 2. Read

This API is used to read a record from the registry using the identifier.


```
GET - /read/38e57c47-3bf5-4320-a94c-de1ad98c5387
```

**Response Body**

```

{
	"id": "open-saber.registry.read",
	"ver": "1.0",
	"ets": "11234",
	"ets": 1523634351,
    	"params": {
        	"resmsgid": "",
        	"msgid": "016c7abc-0bfb-432d-8a15-0caaccadef9d",
        	"err": "",
        	"status": "SUCCCESSFUL",
        	"errmsg": ""
    	},
    	"responseCode": "OK",
    	"result": {
	    "@context": 
		{
			"rdf": "http://www.w3.org/1999/02/22-rdf-syntax-ns#",
			"rdfs": "http://www.w3.org/2000/01/rdf-schema#",
			"teacher": "http://example.com/voc/teacher/1.0.0/",
			"xsd": "http://www.w3.org/2001/XMLSchema#",
			"@vocab": "http://example.com/voc/teacher/1.0.0/",
		},
            "@graph": [
		"@id": "teacher:38e57c47-3bf5-4320-a94c-de1ad98c5387",
		"@type": "Teacher",
		"serialNum": 12,
		"teacherCode": "12234",
		"nationalIdentifier": "1234567890123456",
		"teacherName": "Marvin Pande",
		"gender": {
			"@id": "teacher:GenderTypeCode-MALE"
		},
		"birthDate": 
		{
			"@type": "xsd:date",
			"@value": "1990-12-06"
		},

		"socialCategory": 
		{
			"@id": "teacher:SocialCategoryTypeCode-GENERAL"
		},

		"highestAcademicQualification": 
		{
			"@id": "teacher:AcademicQualificationTypeCode-PHD"
		},

		"highestTeacherQualification": 
		{
			"@id": "teacher:TeacherQualificationTypeCode-MED"
		},

		"yearOfJoiningService": 
		{
			"@type": "xsd:gYear",
			"@value": "2014"
		},

		"teachingRole": 
		{
                        "@id": "teacher:38e57c47-3bf5-4320-a94c-de1ad98c5389",
			"@type": "TeachingRole",
			"teacherType": 
			{
				"@id": "teacher:TeacherTypeCode-HEAD"
			},

			"appointmentType": 
			{
				"@id": "teacher:TeacherAppointmentTypeCode-REGULAR"
			},

			"classesTaught": 
			{
				"@id": "teacher:ClassTypeCode-SECONDARYANDHIGHERSECONDARY"
			},

			"appointedForSubjects": 
			{
				"@id": "teacher:SubjectCode-MATH"
			},

			"mainSubjectsTaught": 
			[
				{
					"@id": "teacher:SubjectCode-PHYSICS"
				},

				{
					"@id": "teacher:SubjectCode-MATH"
				}
			],

			"appointmentYear": 
			{
				"@type": "xsd:gYear",
				"@value": "2015"
			}
		},

		"inServiceTeacherTrainingFromBRC": 
		{
                        "@id": "teacher:38e57c47-3bf5-4320-a94c-de1ad98c5381",
			"@type": "InServiceTeacherTrainingFromBlockResourceCentre",
			"teacher:daysOfInServiceTeacherTraining": {
				"@type": "xsd:decimal",
				"@value":"10"
			}
		},

		"inServiceTeacherTrainingFromCRC": 
		{
                        "@id": "teacher:38e57c47-3bf5-4320-a94c-de1ad98c5382",
			"@type": "InServiceTeacherTrainingFromClusterResourceCentre",
			"teacher:daysOfInServiceTeacherTraining": {
				"@type": "xsd:decimal",
				"@value":"2"
				}
		},

		"inServiceTeacherTrainingFromDIET": 
		{
                        "@id": "teacher:38e57c47-3bf5-4320-a94c-de1ad98c5383",
			"@type": "InServiceTeacherTrainingFromDIET",
			"teacher:daysOfInServiceTeacherTraining": {
				"@type": "xsd:decimal",
				"@value":"5.5"
				}
		},

		"inServiceTeacherTrainingFromOthers": 
		{
                        "@id": "teacher:38e57c47-3bf5-4320-a94c-de1ad98c5384",
			"@type": "InServiceTeacherTrainingFromOthers",
			"teacher:daysOfInServiceTeacherTraining": {
				"@type": "xsd:decimal",
				"@value":"3.5"
				}
		},

		"nonTeachingAssignmentsForAcademicCalendar": 
		{
                        "@id": "teacher:38e57c47-3bf5-4320-a94c-de1ad98c5385",
			"@type": "NonTeachingAssignmentsForAcademicCalendar",
			"teacher:daysOfNonTeachingAssignments": {
				"@type": "xsd:decimal",
				"@value":"6"
				}
		},

		"basicProficiencyLevel": 
		[
			{
                                "@id": "teacher:38e57c47-3bf5-4320-a94c-de1ad98c5388",
				"@type": "BasicProficiencyLevel",
				"proficiencySubject": 
				{
					"@id": "teacher:SubjectCode-ENGLISH"
				},

				"proficiencyAcademicQualification": 
				{
					"@id": "teacher:AcademicQualificationTypeCode-HIGHERSECONDARY"
				}
			},

			{
                                "@id": "teacher:38e57c47-3bf5-4320-a94c-de1ad98c5380",
				"@type": "BasicProficiencyLevel",
				"proficiencySubject": 
				{
					"@id": "teacher:SubjectCode-SOCIALSTUDIES"
				},

				"proficiencyAcademicQualification": 
				{
					"@id": "teacher:AcademicQualificationTypeCode-SECONDARY"
				}
			}
		],

		"disabilityType": 
		{
			"@id": "teacher:DisabilityCode-NA"
		},

		"trainedForChildrenSpecialNeeds": 
		{
			"@id": "teacher:YesNoCode-YES"
		},

		"teacher:trainedinUseOfComputer": 
		{
			"@id": "teacher:YesNoCode-YES"
		}
	}
}
```

#### 3. Update 

This updates an existing record in the registry. 

#### Case 1

Updating a few properties such as ```teacherCode, serialNum and teacherName``` in the teacher record.

```
PATCH - /update/38e57c47-3bf5-4320-a94c-de1ad98c5387
```

**Request Body**

```
{
	"id": "open-saber.registry.update",
	"ver": "1.0",
	"ets": "11234",
	"params": 
	{
		"did": "",
		"key": "",
		"msgid": ""
	},

	"request": 
	{
		"@context": 
		{
			"rdf": "http://www.w3.org/1999/02/22-rdf-syntax-ns#",
			"rdfs": "http://www.w3.org/2000/01/rdf-schema#",
			"teacher": "http://example.com/voc/teacher/1.0.0/",
			"xsd": "http://www.w3.org/2001/XMLSchema#",
			"@vocab": "http://example.com/voc/teacher/1.0.0/",
		},
		"@id": "teacher:38e57c47-3bf5-4320-a94c-de1ad98c5387", //same as the record identifier specified as path parameter in the request
		"@type": "Teacher",
		"serialNum": 546,
		"teacherCode": "6789",
		"teacherName": "Pooja Sharma"
	}
}
```

**Response**

```
{
  "id": //identifier , e.g. "open-saber.registry.update",
  "ver": //version "1.0",
  "ets": //epoch timestamp in format "YYYY-MM-DDThh:mm:ssZ+/-nn.nn",
  "params": {
    "resmsgid": "",
    "msgid": "",
    "err": "",
    "status": "successful",
    "errmsg": ""
  },
  "result": {}
}
```

#### Case 2

Updating a few properties such as ```gender and highestAcademicQualification``` in the teacher record.

```
PATCH - /update/38e57c47-3bf5-4320-a94c-de1ad98c5387
```

**Request Body**

```
{
	"id": "open-saber.registry.update",
	"ver": "1.0",
	"ets": "11234",
	"params": 
	{
		"did": "",
		"key": "",
		"msgid": ""
	},

	"request": 
	{
		"@context": 
		{
			"rdf": "http://www.w3.org/1999/02/22-rdf-syntax-ns#",
			"rdfs": "http://www.w3.org/2000/01/rdf-schema#",
			"teacher": "http://example.com/voc/teacher/1.0.0/",
			"xsd": "http://www.w3.org/2001/XMLSchema#",
			"@vocab": "http://example.com/voc/teacher/1.0.0/",
		},
		"@id": "teacher:38e57c47-3bf5-4320-a94c-de1ad98c5387",
		"@type": "Teacher",
		"gender": {
			"@id": "teacher:GenderTypeCode-FEMALE"
		},
                "highestAcademicQualification": 
		{
			"@id": "teacher:AcademicQualificationTypeCode-POSTDOC"
		}

	}
}

```

**Response**
```
{
  "id": //identifier , e.g. "open-saber.registry.update",
  "ver": //version "1.0",
  "ets": //epoch timestamp in format "YYYY-MM-DDThh:mm:ssZ+/-nn.nn",
  "params": {
    "resmsgid": "",
    "msgid": "",
    "err": "",
    "status": "successful",
    "errmsg": ""
  },
  "result": {}
}
```

#### Case 3

Adding a basicProficiencyLevel to the list of ```basicProficiencyLevels```.

```
PUT - /update/38e57c47-3bf5-4320-a94c-de1ad98c5387
```

**Request Body**

```
{
	"id": "open-saber.registry.update",
	"ver": "1.0",
	"ets": "11234",
	"params": 
	{
		"did": "",
		"key": "",
		"msgid": ""
	},

	"request": 
	{
		"@context": 
		{
			"rdf": "http://www.w3.org/1999/02/22-rdf-syntax-ns#",
			"rdfs": "http://www.w3.org/2000/01/rdf-schema#",
			"teacher": "http://example.com/voc/teacher/1.0.0/",
			"xsd": "http://www.w3.org/2001/XMLSchema#",
			"@vocab": "http://example.com/voc/teacher/1.0.0/",
		},
		"@id": "teacher:38e57c47-3bf5-4320-a94c-de1ad98c5387",
		"@type": "Teacher",
		"basicProficiencyLevel": 
		[
			{
				"@type": "BasicProficiencyLevel",
				"proficiencySubject": 
				{
					"@id": "teacher:SubjectCode-MATH"
				},

				"proficiencyAcademicQualification": 
				{
					"@id": "teacher:AcademicQualificationTypeCode-PHD"
				}
			}
		]


	}
}

```

**Response**
```
{
  "id": //identifier , e.g. "open-saber.registry.update",
  "ver": //version "1.0",
  "ets": //epoch timestamp in format "YYYY-MM-DDThh:mm:ssZ+/-nn.nn",
  "params": {
    "resmsgid": "",
    "msgid": "",
    "err": "",
    "status": "successful",
    "errmsg": ""
  },
  "result": {}
}
```


#### 4. Delete

This can be used to remove an entity from an existing record in the database. The API will generate an error response if the record or the entity does not exist. In the below example, we are deleting ```teacher:SubjectCode-PHYSICS``` from the list of ```mainSubjectsTaught``` for the teacher with the identifier(```teacher:38e57c47-3bf5-4320-a94c-de1ad98c5387```).

```
POST - /delete
```

**Request Body**
```
{
	"id": "open-saber.registry.delete",
	"ver": "1.0",
	"ets": "11234",
	"params": 
	{
		"did": "",
		"key": "",
		"msgid": ""
	},

	"request": 
	{
		"@context": 
		{
			"rdf": "http://www.w3.org/1999/02/22-rdf-syntax-ns#",
			"rdfs": "http://www.w3.org/2000/01/rdf-schema#",
			"teacher": "http://example.com/voc/teacher/1.0.0/",
			"xsd": "http://www.w3.org/2001/XMLSchema#",
			"@vocab": "http://example.com/voc/teacher/1.0.0/",
		},
		"@id": "teacher:38e57c47-3bf5-4320-a94c-de1ad98c5387", //label(identifier) of node, which has the property to be deleted,
                "mainSubjectsTaught": [  //property for which the value has to be deleted
				{
					"@id": "teacher:SubjectCode-PHYSICS" //value to be deleted
				}
		]

	}
}

```

**Response**

```
{
  "id": //identifier , e.g. "open-saber.registry.update",
  "ver": //version "1.0",
  "ets": //epoch timestamp in format "YYYY-MM-DDThh:mm:ssZ+/-nn.nn",
  "params": {
    "resmsgid": "",
    "msgid": "",
    "err": "",
    "status": "successful",
    "errmsg": ""
  },
  "result": {}
}
```
