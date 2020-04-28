---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript
//  - csharp: C#

toc_footers:
  - Documentation for <a href='https://tazuz.org'>Tazuz API</a>
  - Created by Daniel Darwich
  - Request a Developer Key with
  - ddarwichh@atid.edu.mx


includes:
  - errors

search: true
---

# Introduction

Welcome to the Tazuz API! You can use our API to access all endpoints, which can get information on sports, standings, transportation, and more in our database.

We have language bindings in C# and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

Tazuz uses API keys to allow access to the API. You can register a new Maccabiah API key at our [developer portal](http://tazuz.org).

Tazuz expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: APIKEY`

<aside class="notice">
You must replace <code>APIKEY</code> with your personal API key.
</aside>

# Tazuz Backend
















## Get Users by University

```javascript
function GetUsers() {
  var request = new XMLHttpRequest();
  var url = "https://tazuz-d281a.firebaseio.com/UNIVERSITY/Users.json?auth=APIKEY";

  request.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      var object = JSON.parse(this.responseText);
      Users(object);
    }
  };
  request.open("GET", url, true);
  request.send();
}

function Users(object) {
  console.log(Object.values(object));
}

GetUsers();
```

> You must replace <code>APIKEY</code> with your personal API key.

> You must replace <code>UNIVERSITY</code> with a universities initials.

> The above command returns JSON structured like this:

```json
[

{
"Mail":"jbond@idc.com",
"Name":"James Bond",
"Tribes":["Soccer", "Tennis"],
"University":"IDC"
},

{
"Mail":"dbeckham@idc.com",
"Name":"David Beckham",
"Tribes":["Baseball", "Surf", "Yoga"],
"University":"IDC"
}

]
```

This endpoint retrieves a list of all users by university containing their basic information.

### HTTP Request

`GET https://tazuz-d281a.firebaseio.com/UNIVERSITY/Users.json?auth=APIKEY`

### URL Parameters

Parameter | Type | Description
--------- | ------- | -----------
Authorization | String | You need to insert your APIKEY to get results.
University | String | You need to insert the initials of a university to get results. (IDC, TAU)















## Get All Tribes in University

```javascript
function GetTribes() {
  var request = new XMLHttpRequest();
  var url = "https://tazuz-d281a.firebaseio.com/UNIVERSITY/Tribes.json?auth=APIKEY";

  request.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      var object = JSON.parse(this.responseText);
      Tribes(object);
    }
  };
  request.open("GET", url, true);
  request.send();
}

function Tribes(object) {
  console.log(Object.keys(object));
}

GetTribes();
```

> You must replace <code>APIKEY</code> with your personal API key.

> You must replace <code>UNIVERSITY</code> with a universities initials.

> The above command returns JSON structured like this:

```json
["Soccer", "Basketball", "Yoga", "Surf"]
```

This endpoint retrieves a list of all tribes in a university.

### HTTP Request

`GET https://tazuz-d281a.firebaseio.com/UNIVERSITY/Tribes.json?auth=APIKEY`

### URL Parameters

Parameter | Type | Description
--------- | ------- | -----------
Authorization | String | You need to insert your APIKEY to get results.
University | String | You need to insert the initials of a university to get results. (IDC, TAU)















## Get a Specific Tribe's Information

```javascript
function GetTribe() {
  var request = new XMLHttpRequest();
  var url = "https://tazuz-d281a.firebaseio.com/UNIVERSITY/Tribes/TRIBE.json?auth=APIKEY";

  request.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      var object = JSON.parse(this.responseText);
      Tribe(object);
    }
  };
  request.open("GET", url, true);
  request.send();
}

function Tribe(object) {
  console.log(object);
}

GetTribe();
```

> You must replace <code>APIKEY</code> with your personal API key.

> You must replace <code>UNIVERSITY</code> with a universities initials.

> You must replace <code>TRIBE</code> with a tribe's name.

> The above command returns JSON structured like this:

```json
{
  "ImageURL":"https://media2.fdncms.com/eastbayexpress/imager/u/original/17703015/soccer-ball-ss-img.jpg",
  "Information":"The goal of this tribe is to...",
  "Members":["Oribe Peralta", "Javier Hernandez", "Leonel Messi", "Cristiano Ronaldo"],
  "TribeLeader":"David Beckham"
}
```

This endpoint retrieves a information for a specific tribe in a university.

### HTTP Request

`GET https://tazuz-d281a.firebaseio.com/UNIVERSITY/Tribes/TRIBE.json?auth=APIKEY`

### URL Parameters

Parameter | Type | Description
--------- | ------- | -----------
Authorization | String | You need to insert your APIKEY to get results.
University | String | You need to insert the initials of a university to get results. (IDC, TAU)
Tribe | String | You need to insert a Tribe's name to get results.

<aside class="notice">Note: The tribe's name has to be written exactly as in the tribes list.</aside>

















## Get All Events

```javascript
function GetEvents() {
  var request = new XMLHttpRequest();
  var url = "https://tazuz-d281a.firebaseio.com/UNIVERSITY/Events.json?auth=APIKEY";

  request.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      var object = JSON.parse(this.responseText);
      Events(object);
    }
  };
  request.open("GET", url, true);
  request.send();
}

function Events(object) {
  var newObject = new Object();
  for (const property in object) {
    newObject[property] = Object.values(object[property]); 
  }
  console.log(newObject);
}

GetEvents();
```

> You must replace <code>APIKEY</code> with your personal API key.

> You must replace <code>UNIVERSITY</code> with a universities initials.

> The above command returns JSON structured like this:

```json
{
  "Basketball":[
    {
      "Date":"20-04-20",
      "Time":"20:30",
      "Title":"Friendly Match",
      "Venue":"IDC Basketball Court",
      "VenueID":9
    }
  ],
  "Soccer":[
    {
      "Date":"17-04-20",
      "Time":"09:00",
      "Title":"Greeting Party",
      "Venue":"IDC Patio",
      "VenueID":7
    },
    {
      "Date":"17-04-20",
      "Time":"14:00",
      "Title":"Friendly Match",
      "Venue":"IDC Soccer Court",
      "VenueID":12
    }
  ]
}
```

This endpoint retrieves a list of all events in a university filtered by tribe and ordered chronologically.

### HTTP Request

`GET https://tazuz-d281a.firebaseio.com/UNIVERSITY/Events.json?auth=APIKEY`

### URL Parameters

Parameter | Type | Description
--------- | ------- | -----------
Authorization | String | You need to insert your APIKEY to get results.
University | String | You need to insert the initials of a university to get results. (IDC, TAU)



















## Get List of All Tournaments

```javascript
function GetTournaments() {
  var request = new XMLHttpRequest();
  var url = "https://tazuz-d281a.firebaseio.com/UNIVERSITY/Tournaments.json?auth=APIKEY";

  request.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      var object = JSON.parse(this.responseText);
      Tournaments(object);
    }
  };
  request.open("GET", url, true);
  request.send();
}

function Tournaments(object) {
  console.log(Object.keys(object));
}

GetTournaments();
```

> You must replace <code>APIKEY</code> with your personal API key.

> You must replace <code>UNIVERSITY</code> with a universities initials.

> The above command returns JSON structured like this:

```json
["Mens Basketball", "Soccer"]
```

This endpoint retrieves a list of all tournaments in a university.

### HTTP Request

`GET https://tazuz-d281a.firebaseio.com/UNIVERSITY/Tournaments.json?auth=APIKEY`

### URL Parameters

Parameter | Type | Description
--------- | ------- | -----------
Authorization | String | You need to insert your APIKEY to get results.
University | String | You need to insert the initials of a university to get results. (IDC, TAU)















## Get a Specific Tournament's Matches

```javascript
function GetTournamentMatches() {
  var request = new XMLHttpRequest();
  var url = "https://tazuz-d281a.firebaseio.com/UNIVERSITY/Tournaments/TOURNAMENT/Matches.json?auth=APIKEY";

  request.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      var object = JSON.parse(this.responseText);
      TournamentMatches(object);
    }
  };
  request.open("GET", url, true);
  request.send();
}

function TournamentMatches(object) {
  console.log(Object.values(object));
}

GetTournamentMatches();
```

> You must replace <code>APIKEY</code> with your personal API key.

> You must replace <code>UNIVERSITY</code> with a universities initials.

> You must replace <code>TOURNAMENT</code> with a tournament's name.

> The above command returns JSON structured like this:

```json
[
  {
    "Date":"19-04-20",
    "Ended":true,
    "Team1Name":"Mexico",
    "Team1Score":101,
    "Team2Name":"Colombia",
    "Team2Score":85,
    "Time":"21:00",
    "Venue":"Tel Aviv Basketball Court",
    "VenueID":3
  },
  {
    "Date":"19-04-20",
    "Ended":false,
    "Team1Name":"Argentina",
    "Team1Score":0,
    "Team2Name":"Spain",
    "Team2Score":0,
    "Time":"22:30",
    "Venue":"Tel Aviv Basketball Court",
    "VenueID":3
  }
]
```

This endpoint retrieves a information for all matches of a tournament in a university.

### HTTP Request

`GET https://tazuz-d281a.firebaseio.com/UNIVERSITY/Tournaments/TOURNAMENT/Matches.json?auth=APIKEY`

### URL Parameters

Parameter | Type | Description
--------- | ------- | -----------
Authorization | String | You need to insert your APIKEY to get results.
University | String | You need to insert the initials of a university to get results. (IDC, TAU)
Tournament | String | You need to insert a Tournament's name to get results.

<aside class="notice">Note: The tournaments's name has to be written exactly as in the tournaments list.</aside>






















## Get a Specific Tournament's Standings

```javascript
function GetTournamentStandings() {
  var request = new XMLHttpRequest();
  var url = "https://tazuz-d281a.firebaseio.com/UNIVERSITY/Tournaments/TOURNAMENT/Standings.json?auth=APIKEY";

  request.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      var object = JSON.parse(this.responseText);
      TournamentStandings(object);
    }
  };
  request.open("GET", url, true);
  request.send();
}

function TournamentStandings(object) {
  console.log(object);
}

GetTournamentStandings();
```

> You must replace <code>APIKEY</code> with your personal API key.

> You must replace <code>UNIVERSITY</code> with a universities initials.

> You must replace <code>TOURNAMENT</code> with a tournament's name.

> The above command returns JSON structured like this:

```json
[
  {
    "Name":"Mexico",
    "Points":17,
    "Position":1
  },
  {
    "Name":"Colombia",
    "Points":15,
    "Position":2
  },
  {
    "Name":"Argentina",
    "Points":7,
    "Position":3
  },
  {
    "Name":"Spain",
    "Points":2,
    "Position":4
  }
]
```

This endpoint retrieves a information for all matches of a tournament in a university.

### HTTP Request

`GET https://tazuz-d281a.firebaseio.com/UNIVERSITY/Tournaments/TOURNAMENT/Standings.json?auth=APIKEY`

### URL Parameters

Parameter | Type | Description
--------- | ------- | -----------
Authorization | String | You need to insert your APIKEY to get results.
University | String | You need to insert the initials of a university to get results. (IDC, TAU)
Tournament | String | You need to insert a Tournament's name to get results.

<aside class="notice">Note: The tournaments's name has to be written exactly as in the tournaments list.</aside>
























## Get List of All Venues

```javascript
function GetVenues() {
  var request = new XMLHttpRequest();
  var url = "https://tazuz-d281a.firebaseio.com/UNIVERSITY/Venues.json?auth=APIKEY";

  request.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      var object = JSON.parse(this.responseText);
      Venues(object);
    }
  };
  request.open("GET", url, true);
  request.send();
}

function Venues(object) {
  console.log(Object.values(object));
}

GetVenues();
```

> You must replace <code>APIKEY</code> with your personal API key.

> You must replace <code>UNIVERSITY</code> with a universities initials.

> The above command returns JSON structured like this:

```json
[
  {
    "Name":"IDC Patio",
    "lat":2.234567,
    "lng":-99.075678
  },
  {
    "Name":"IDC Basketball Court",
    "lat":2.234567,
    "lng":-99.075678
  },
  {
    "Name":"IDC Soccer Court",
    "lat":2.234567,
    "lng":-99.075678
  }
]
```

This endpoint retrieves a list of all venues in a university.

### HTTP Request

`GET https://tazuz-d281a.firebaseio.com/UNIVERSITY/Venues.json?auth=APIKEY`

### URL Parameters

Parameter | Type | Description
--------- | ------- | -----------
Authorization | String | You need to insert your APIKEY to get results.
University | String | You need to insert the initials of a university to get results. (IDC, TAU)

