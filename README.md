README

To REQUEST data from the microservice, have the data in a JSON-formatted list of song titles. Then 

REQUEST Details:
Method: POST
URL: http://localhost:8081/
Content-Type: application/json
Request Body: JSON array of song titles in alphabetical groups.

REQUEST Example:

[
  "NewJeans",
  "For Whom The Bell Tolls",
  "West Coast",
  "Breakin' Dishes",
  "Bad Guy"
]

The RESPONSE from the microservice will be a JSON object that outputs the song titles grouped in alphabetical groups, in alphabetical order.

RESPONSE Example:

{
  "Alphabetical Groups:": {
    "Starts with 'B'": [
      "Breakin' Dishes",
      "Bad Guy"
    ],
    "Starts with 'F'": [
      "For Whom The Bells Tolls"
    ],
    "Starts with 'N'": [
      "NewJeans"
    ],
    "Starts with 'W'": [
      "West Coast"
    ]
  }
}

UML Diagram:
![Main Program](https://github.com/user-attachments/assets/3cdee321-d03f-4501-9c5d-1d01dfb6d034)
