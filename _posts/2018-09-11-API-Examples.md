---
date: 2018-09-10
title: API Examples
categories:
  - Documentation
type: Document
showSidebar: true
published: true
nav_ordering: 6
pageTitle: API Examples
desc: Examples on how to use the APIs.
---

## APIs with JSON support
**From release 1.1.0 only.**

### 1. Create

This creates a new record in the registry.

```
POST - /add,  
Content Type - application/json 
```
**Request Body**
```
{
  "id": "open-saber.registry.create",
  "ver": "1.0",
  "ets": "11234",
  "params": {
    "did": "",
    "key": "",
    "msgid": ""
  },
  "request": {
    "Teacher": {
      "signatures": {
        "@type": "sc:GraphSignature2012",
        "signatureFor": "http://localhost:8080/serialNum",
        "creator": "https://example.com/i/pat/keys/5",
        "created": "2017-09-23T20:21:34Z",
        "nonce": "2bbgh3dgjg2302d-d2b3gi423d42",
        "signatureValue": "eyiOiJKJ0eXA...OEjgFWFXk"
      },
      "serialNum": 6,
      "teacherCode": "12234",
      "nationalIdentifier": "1234567890123456",
      "teacherName": "Marvin Pande",
      "gender": "GenderTypeCode-MALE",
      "birthDate": "1990-12-06",
      "socialCategory": "SocialCategoryTypeCode-GENERAL",
      "highestAcademicQualification": "AcademicQualificationTypeCode-PHD",
      "highestTeacherQualification": "TeacherQualificationTypeCode-MED",
      "yearOfJoiningService": "2014",
      "teachingRole": {
        "@type": "TeachingRole",
        "teacherType": "TeacherTypeCode-HEAD",
        "appointmentType": "TeacherAppointmentTypeCode-REGULAR",
        "classesTaught": "ClassTypeCode-SECONDARYANDHIGHERSECONDARY",
        "appointedForSubjects": "SubjectCode-ENGLISH",
        "mainSubjectsTaught": [
          "SubjectCode-SOCIALSTUDIES",
          "SubjectCode-ENGLISH"
        ],
        "appointmentYear": "2015"
      },
      "inServiceTeacherTrainingFromBRC": {
        "@type": "InServiceTeacherTrainingFromBlockResourceCentre",
        "daysOfInServiceTeacherTraining": "10"
      },
      "inServiceTeacherTrainingFromCRC": {
        "@type": "InServiceTeacherTrainingFromClusterResourceCentre",
        "daysOfInServiceTeacherTraining": "2"
      },
      "inServiceTeacherTrainingFromDIET": {
        "@type": "InServiceTeacherTrainingFromDIET",
        "daysOfInServiceTeacherTraining": "5.5"
      },
      "inServiceTeacherTrainingFromOthers": {
        "@type": "InServiceTeacherTrainingFromOthers",
        "daysOfInServiceTeacherTraining": "3.5"
      },
      "nonTeachingAssignmentsForAcademicCalendar": {
        "@type": "NonTeachingAssignmentsForAcademicCalendar",
        "daysOfNonTeachingAssignments": "6"
      },
      "basicProficiencyLevel": [
        {
          "@type": "BasicProficiencyLevel",
          "proficiencySubject": "SubjectCode-MATH",
          "proficiencyAcademicQualification": "AcademicQualificationTypeCode-PHD"
        },
        {
          "@type": "BasicProficiencyLevel",
          "proficiencySubject": "SubjectCode-ENGLISH",
          "proficiencyAcademicQualification": "AcademicQualificationTypeCode-HIGHERSECONDARY"
        },
        {
          "@type": "BasicProficiencyLevel",
          "proficiencySubject": "SubjectCode-SOCIALSTUDIES",
          "proficiencyAcademicQualification": "AcademicQualificationTypeCode-SECONDARY"
        }
      ],
      "disabilityType": "DisabilityCode-NA",
      "trainedForChildrenSpecialNeeds": "YesNoCode-YES",
      "trainedinUseOfComputer": "YesNoCode-YES"
    }
  }
}


```
**Response**
```
{
    "id": "open-saber.registry.create",
    "ver": "1.0",
    "ets": 1539344132210,
    "params": {
        "resmsgid": "",
        "msgid": "96345148-464e-452a-8541-fd9a0d5c9243",
        "err": "",
        "status": "SUCCESSFUL",
        "errmsg": ""
    },
    "responseCode": "OK",
    "result": {
        "entity": "http://localhost:8080/……-adfe-00badaa25097"
    }
}
```

### 2. Update

This updates an existing record in the registry. Only properties of existing records can be updated via this API. The API will generate an error response if a valid identifier (@id) for the record or the nested records is not sent. These valid identifiers must be existing in database.
```
POST - /update,  
Content Type - application/json
```
**Request Body**
```
{
  "id": "open-saber.registry.update",
  "ver": "1.0",
  "ets": "11234",
  "params": {
    "did": "",
    "key": "",
    "msgid": ""
  },
  "request": {
    "Teacher": {
      "@id": "32f440cc-13a7-4b5e-915c-4272586a3572",
      "signatures": {
        "@type": "sc:GraphSignature2012",
        "signatureFor": "http://localhost:8080/serialNum",
        "created": "2017-09-23T20:21:34Z",
        "creator": "https://example.com/i/pat/keys/5",
        "nonce": "2bbgh3dgjg2302d-d2b3gi423d42",
        "signatureValue": "eyiOiJKJ0eXA...OEjgFWFXkUpdated"
      }
    }
  }
}
OR for nested record-
{
  "id": "open-saber.registry.update",
  "ver": "1.0",
  "ets": "11234",
  "params": {
    "did": "",
    "key": "",
    "msgid": ""
  },
  "request": {
    "TeachingRole": {
      "@id": "436360fd-6f0f-44bd-9b95-bd753ed98812",
      "signatures": {
        "@type": "sc:GraphSignature2012",
        "signatureFor": "http://localhost:8080/appointmentType",
        "created": "2017-09-23T20:21:34Z",
        "creator": "https://example.com/i/pat/keys/5",
        "nonce": "2bbgh3dgjg2302d-d2b3gi423d42",
        "signatureValue": "eyiOiJKJ0eXA...OEjgFWFXkUpdateddd"
      }
    }
  }
}

```
**Response**
```
{
    "id": "open-saber.registry.update",
    "ver": "1.0",
    "ets": 1539614296559,
    "params": {
        "resmsgid": "",
        "msgid": "89ef5506-83f0-4cc5-9025-e352bc236dba",
        "err": "",
        "status": "SUCCESSFUL",
        "errmsg": ""
    },
    "responseCode": "OK"
}
```
### 3. Read

This can be used to read an entity from the database, the url path variable id specifies the entity id in the database. The API will generate an error response if the record or the entity does not exist.
```
POST - /read,  
Accept - application/json or application/ld+json 
Default Accept - application/json
```
**Request Body**
```
{
  "id": "open-saber.registry.read",
  "ver": "1.0",
  "ets": "11234",
  "params": {
    "did": "",
    "key": "",
    "msgid": ""
  },
  "request": {
      "id": "9c7a6bf3-d39a-4016-a635-74cb4aa3cb7c",
      "includeSignatures": true
  }
}
```
**Response**
```
{
    "id": "open-saber.registry.read",
    "ver": "1.0",
    "ets": 1539691954358,
    "params": {
        "resmsgid": "",
        "msgid": "acdf5edd-5429-4028-a19e-61c58d5f1f1e",
        "err": "",
        "status": "SUCCESSFUL",
        "errmsg": ""
    },
    "responseCode": "OK",
    "result": [
        {
            "Teacher": {
                "@id": "a09f00c0-6379-48a6-80d8-37d8c03906e8",
                "basicProficiencyLevel": [
                    {
                        "@id": "90ca11ad-95f8-4f09-aa4e-1c0676d24543",
                        "proficiencyAcademicQualification": "AcademicQualificationTypeCode-HIGHERSECONDARY",
                        "proficiencySubject": "SubjectCode-ENGLISH"
                    },
                    {
                        "@id": "46c82782-3713-42b0-b1cb-095a24538dd5",
                        "proficiencyAcademicQualification": "AcademicQualificationTypeCode-SECONDARY",
                        "proficiencySubject": "SubjectCode-SOCIALSTUDIES"
                    },
                    {
                        "@id": "e0fc24af-abf9-4f3b-9575-925045537ae0",
                        "proficiencyAcademicQualification": "AcademicQualificationTypeCode-PHD",
                        "proficiencySubject": "SubjectCode-MATH"
                    }
                ],
                "birthDate": "1990-12-06",
                "disabilityType": "DisabilityCode-NA",
                "gender": "GenderTypeCode-MALE",
                "highestAcademicQualification": "AcademicQualificationTypeCode-PHD",
                "highestTeacherQualification": "TeacherQualificationTypeCode-MED",
                "inServiceTeacherTrainingFromBRC": {
                    "@id": "dc22af6b-f8bf-440b-998d-dd5e5d7c57c1",
                    "daysOfInServiceTeacherTraining": "10"
                },
                "inServiceTeacherTrainingFromCRC": {
                    "@id": "fc580075-bd8c-4c75-b9dd-196a001a620c",
                    "daysOfInServiceTeacherTraining": "2"
                },
                "inServiceTeacherTrainingFromDIET": {
                    "@id": "e1eb790e-6e6b-48cc-b8df-9d0b91245f38",
                    "daysOfInServiceTeacherTraining": "5.5"
                },
                "inServiceTeacherTrainingFromOthers": {
                    "@id": "bef5e773-9f6b-46d3-88d1-9519b2c32822",
                    "daysOfInServiceTeacherTraining": "3.5"
                },
                "nationalIdentifier": "1234567890123456",
                "nonTeachingAssignmentsForAcademicCalendar": {
                    "@id": "f284746d-6ed3-49fc-bbeb-1644d9b759d4",
                    "daysOfNonTeachingAssignments": "6"
                },
                "serialNum": 6,
                "socialCategory": "SocialCategoryTypeCode-GENERAL",
                "teacherCode": "12234",
                "teacherName": "Marvin Pande",
                "teachingRole": {
                    "@id": "70add9f0-7dee-41d3-9f67-2d3e1498fedd",
                    "appointedForSubjects": "SubjectCode-ENGLISH",
                    "appointmentType": "TeacherAppointmentTypeCode-REGULAR",
                    "appointmentYear": "2015",
                    "classesTaught": "ClassTypeCode-SECONDARYANDHIGHERSECONDARY",
                    "mainSubjectsTaught": [
                        "teacher:SubjectCode-ENGLISH",
                        "teacher:SubjectCode-SOCIALSTUDIES"
                    ],
                    "teacherType": "TeacherTypeCode-HEAD"
                },
                "trainedForChildrenSpecialNeeds": "YesNoCode-YES",
                "trainedinUseOfComputer": "YesNoCode-YES",
                "yearOfJoiningService": "2014"
            }
        }
    ]
}
```

### 4. Search 

```
POST - /search,  
Content Type - application/json 
Accept - application/json or application/ld+json
Default Accept - application/json
```
**Request Body**
```
{
  "id": "open-saber.registry.create",
  "ver": "1.0",
  "ets": "11234",
  "params": {
    "did": "",
    "key": "",
    "msgid": ""
  },
  "request": {
    "Teacher": {
      "gender": "GenderTypeCode-MALE"
    }
  }
}

```
**Response**
```
{
  "id": "open-saber.registry.search",
  "ver": "1.0",
  "ets": 1539613525375,
  "params": {
    "resmsgid": "",
    "msgid": "ba2adeda-5680-44b6-908e-e9c28fcfdfcf",
    "err": "",
    "status": "SUCCESSFUL",
    "errmsg": ""
  },
  "responseCode": "OK",
  "result": [
    {
      "Teacher": {
        "basicProficiencyLevel": [
          {
            "proficiencyAcademicQualification": "AcademicQualificationTypeCode-HIGHERSECONDARY",
            "proficiencySubject": "SubjectCode-ENGLISH"
          },
          {
            "proficiencyAcademicQualification": "AcademicQualificationTypeCode-PHD",
            "proficiencySubject": "SubjectCode-MATH"
          },
          {
            "proficiencyAcademicQualification": "AcademicQualificationTypeCode-SECONDARY",
            "proficiencySubject": "SubjectCode-SOCIALSTUDIES"
          }
        ],
        "disabilityType": "DisabilityCode-NA",
        "gender": "GenderTypeCode-MALE",
        "highestAcademicQualification": "AcademicQualificationTypeCode-PHD",
        "highestTeacherQualification": "TeacherQualificationTypeCode-MED",
        "inServiceTeacherTrainingFromBRC": {
          
        },
        "inServiceTeacherTrainingFromCRC": {
          
        },
        "inServiceTeacherTrainingFromDIET": {
          
        },
        "inServiceTeacherTrainingFromOthers": {
          
        },
        "nonTeachingAssignmentsForAcademicCalendar": {
          
        },
        "serialNum": 3,
        "socialCategory": "SocialCategoryTypeCode-GENERAL",
        "teacherName": "Marvin Pande",
        "teachingRole": {
          "appointedForSubjects": "SubjectCode-ENGLISH",
          "appointmentType": "TeacherAppointmentTypeCode-REGULAR",
          "classesTaught": "ClassTypeCode-SECONDARYANDHIGHERSECONDARY",
          "mainSubjectsTaught": "SubjectCode-ENGLISH",
          "teacherType": "TeacherTypeCode-HEAD"
        },
        "trainedForChildrenSpecialNeeds": "YesNoCode-YES",
        "trainedinUseOfComputer": "YesNoCode-YES",
        "yearOfJoiningService": "2014"
      }
    },
    {
      "Teacher": {
        "basicProficiencyLevel": [
          {
            "proficiencyAcademicQualification": "AcademicQualificationTypeCode-SECONDARY",
            "proficiencySubject": "SubjectCode-SOCIALSTUDIES"
          },
          {
            "proficiencyAcademicQualification": "AcademicQualificationTypeCode-HIGHERSECONDARY",
            "proficiencySubject": "SubjectCode-ENGLISH"
          },
          {
            "proficiencyAcademicQualification": "AcademicQualificationTypeCode-PHD",
            "proficiencySubject": "SubjectCode-MATH"
          }
        ],
        "disabilityType": "DisabilityCode-NA",
        "gender": "GenderTypeCode-MALE",
        "highestAcademicQualification": "AcademicQualificationTypeCode-PHD",
        "highestTeacherQualification": "TeacherQualificationTypeCode-MED",
        "inServiceTeacherTrainingFromBRC": {
          
        },
        "inServiceTeacherTrainingFromCRC": {
          
        },
        "inServiceTeacherTrainingFromDIET": {
          
        },
        "inServiceTeacherTrainingFromOthers": {
          
        },
        "nonTeachingAssignmentsForAcademicCalendar": {
          
        },
        "serialNum": 6,
        "socialCategory": "SocialCategoryTypeCode-GENERAL",
        "teacherName": "Marvin Pande",
        "teachingRole": {
          "appointedForSubjects": "SubjectCode-ENGLISH",
          "appointmentType": "TeacherAppointmentTypeCode-REGULAR",
          "classesTaught": "ClassTypeCode-SECONDARYANDHIGHERSECONDARY",
          "mainSubjectsTaught": [
            "teacher:SubjectCode-ENGLISH",
            "teacher:SubjectCode-SOCIALSTUDIES"
          ],
          "teacherType": "TeacherTypeCode-HEAD"
        },
        "trainedForChildrenSpecialNeeds": "YesNoCode-YES",
        "trainedinUseOfComputer": "YesNoCode-YES",
        "yearOfJoiningService": "2014"
      }
    }

  ]
}
```

### 5. Delete

This can be used to remove an entity from the database, the url path variable id specifies the entity id in the database. The API will generate an error response if the record or the entity does not exist.

```
POST - /delete
```
**Request Body**
```
{
  "id": "open-saber.registry.read",
  "ver": "1.0",
  "ets": "11234",
  "params": {
    "did": "",
    "key": "",
    "msgid": ""
  },
  "request": {
      "id": "9c7a6bf3-d39a-4016-a635-74cb4aa3cb7c"
  }
}
```
**Response**
```
{
  "id": "open-saber.registry.delete",
  "ver": "1.0",
  "ets": "",
  "params": {
    "resmsgid": "",
    "msgid": "",
    "err": "",
    "status": "successful",
    "errmsg": ""
  },
  "responseCode": "OK"
}
```