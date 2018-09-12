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

### Open Saber API Examples

#### Scenario 1: Adding a book in the registry


```
POST - <BASE_URL>/add
```

**Request Body**

```
{
	....  //request wrapper 
	"request": 
	{
		... //context

		"@type": "Book",
		"bookCode": 12345,
		"authorName": "JK Rowling",
		"title": "Harry Potter",
		"publisher": "Times Publishing",
		"tags": 
		[
			"hogwarts",
			"childrens' book",
			"series"
		],

		"genre": 
		[
			"book:BookTypeCode-FANTASY"
		],

		"reviews": 
		[
			{
				"@type": "Review",
				"reviewComment": "Very exciting and fun-filled",
				"reviewerName": "John doe"
			},

			{
				"@type": "Review",
				"reviewComment": "Takes you to a magical world",
				"reviewerName": "Jane doe"
			}
		],

		"releaseYear": 
		{
			"@type": "xsd:gYear",
			"@value": "2000"
		},

		"language": "book:LanguageCode-ENGLISH"
		]
	}
}
```

#### Scenario 2: Reading a book from the registry


```
GET - <BASE_URL>/read/38e57c47-3bf5-4320-a94c-de1ad98c5387 (ID of the book)
```

**Response Body**

```
{
	... //response wrapper
	"result": 
	{
		... // context

		"@graph": 
		[
			{
				"@id": "book:38e57c47-3bf5-4320-a94c-de1ad98c5387",
				"@type": "Book",
				"bookCode": 12345,
				"authorName": "JK Rowling",
				"title": "Harry Potter",
				"publisher": "Times Publishing",
				"tags": 
				[
					"hogwarts",
					"children's book",
					"series"
				],

				"genre": 
				[
					{
						"@id": "book:BookTypeCode-FANTASY"
					}
				],

				"reviews": 
				[
					{
						"@id": "book:38e57c47-3bf5-4320-a94c-de1ad98c5388",
						"@type": "Review",
						"reviewComment": "Very exciting and fun-filled",
						"reviewerName": "John doe"
					},

					{
						"@id": "book:38e57c47-3bf5-4320-a94c-de1ad98c5389",
						"@type": "Review",
						"reviewComment": "Takes you to a magical world",
						"reviewerName": "Jane doe"
					}
				],

				"releaseYear": 
				{
					"@type": "xsd:gYear",
					"@value": "2000"
				},

				"language": 
				{
					"@id": "book:LanguageCode-ENGLISH"
				}
			}
		]
	}
}
```

#### Scenario 3: Reading a review from the registry


```
GET - <BASE_URL>/read/38e57c47-3bf5-4320-a94c-de1ad98c5388 (ID of the review)
```

**Response Body**

```
{
	... //response wrapper
	"result": 
	{
		... //context

		"@graph": 
		[
			{
				"@id": "book:38e57c47-3bf5-4320-a94c-de1ad98c5388",
				"@type": "Review",
				"reviewComment": "Very exciting and fun-filled",
				"reviewerName": "John doe"
			}

		]
	}
}
```

#### Scenario 4: Updating literal properties of a book. For e.g. bookCode and title 


```
POST - <BASE_URL>/update
```

**Request Body**

```

{
	... //request wrapper
	"request": 
	{
		... //context
		"@id": "book:38e57c47-3bf5-4320-a94c-de1ad98c5387", //identifier should point to the IRI of the book to be updated
		"bookCode": 12345,
		"title": "Harry Potter and the Half Blood Prince"
	}
}
```


#### Scenario 5: Updating the review for a book. For e.g. modifying the reviewComments.


```
POST - <BASE_URL>/update
```

**Request Body**

```

{
	... //request wrapper
	"request": 
	{
		... //context
		"@id": "book:38e57c47-3bf5-4320-a94c-de1ad98c5388", //identifier should point to the IRI of the review entity/node to be updated within the book
		"reviewComment": "Very exciting and entertaining"
	}
}
```

#### Scenario 6: Updating single-valued enumerated properties of a book. For e.g. language.

```
POST - <BASE_URL>/update
```

**Request Body**

```

{
	... //request wrapper
	"request": 
	{
		... //context
		"@id": "book:38e57c47-3bf5-4320-a94c-de1ad98c5387", //identifier should point to the IRI of the book entity/node to be updated
		"language":"book:LanguageCode-FRENCH"
	}
}
```

#### Scenario 7: Updating multi-valued enumerated properties of a book. For e.g. genre.

```
POST - <BASE_URL>/update
```

**Request Body**

```

{
	... //request wrapper
	"request": 
	{
		... //context
		"@id": "book:38e57c47-3bf5-4320-a94c-de1ad98c5387", //identifier should point to the IRI of the book entity/node to be updated
		"genre":["book:BookTypeCode-MYSTERY","book:BookTypeCode-DRAMA"]
	}
}
```

#### Scenario 8: Updating multi-valued literal properties of a book. For e.g. tags


```
POST - <BASE_URL>/update
```

**Request Body**

```

{
	... //request wrapper
	"request": 
	{
		... //context
		"@id": "book:38e57c47-3bf5-4320-a94c-de1ad98c5387", //identifier should point to the IRI of the book entity/node to be updated
		"tags":["popular","magic","series","suitable for children"]
	}
}
```

#### Scenario 9: Adding a review to a book

```
POST - <BASE_URL>/add?id=<id>&prop=<propertyName>
```

**Request Body**

```
{
	... //request wrapper
	"request": 
	{
		"@type": "Review",
		"reviewComment": "Gripping and fun-filled series.",
		"reviewerName": "Jane Doe"
	}
}
```

#### Scenario 10: Delete a review of the book

```
DELETE - <BASE_URL>/delete/38e57c47-3bf5-4320-a94c-de1ad98c5388 (ID of the review)
```

**Response Body**

```
{
    ... //response wrapper
	"params":
	{
        "resmsgid": "",
        "msgid": "820ef939-be9f-4de4-81ee-53b987153bbb",
        "err": "",
        "status": "SUCCESSFUL",
        "errmsg": ""
    }
}
```

