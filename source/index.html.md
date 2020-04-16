---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - csharp: C#
  - javascript

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
















## Get Users

```javascript
function GetUsers() {
  var request = new XMLHttpRequest();
  var url = "https://tazuz-d281a.firebaseio.com/Users.json?auth=1DfXFRPwRe9OveIAnKiZUlzXaYb3rozZyHdD1OLA";

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

> The above command returns JSON structured like this:

```json
[
  {
    Age:18,
    Name:"John Doe"
  },
  {
    Age:15,
    Name:"Jane Doe"
  }
]

[
  {
    "id": 1,
    "country": "Mexico",
    "flag-image-url": "http://FLAGIMAGEURL.png"
  },
  {
      "id": 2,
      "country": "Australia",
      "flag-image-url": "http://FLAGIMAGEURL.png"
  }
  {...}
]
```

This endpoint retrieves information of all countries participating containing the sports they participate in.

### HTTP Request

`GET http://jmp2019.com/api/v1/countries`

### Query Headers

Header | Default | Description
--------- | ------- | -----------
Authorization | null | You need to insert your APIKEY to get results.
















## Get All Country/Sports Data

```csharp
static HttpClient client = new HttpClient();

public JArray GetCountrySportsData()
{
    HttpWebRequest response = (HttpWebRequest)WebRequest.Create("http://jmp2019.com/api/v1/COUNTRY");

    response.UseDefaultCredentials = true;
    response.Headers.Add("Authorization", "APIKEY");

    HttpWebResponse answer = (HttpWebResponse)response.GetResponse();

    if (answer.StatusCode == HttpStatusCode.OK)
    {
        Stream value = answer.GetResponseStream();
        StreamReader _value = new StreamReader(value);
        if (value == null)
        {
            Console.WriteLine("Api Value Is Null");
        }

        var data = JArray.Parse(_value.ReadToEnd());
        return data;
    }
    return null;
}

JArray data = GetCountrySportsData();
```

```javascript

```

> You must replace <code>APIKEY</code> with your personal API key.

> You must replace <code>COUNTRY</code> with a specific country name.

> The above command returns JSON structured like this:

```json
[
  {
      "id": 5,
      "name": "Swimming",
      "sports-logo-url": "http://SPORTSLOGOURL.png",
      "players": [
      {
          "id": 2560,
        "Name": "John Doe",
        "player-image-url": "http://PLAYERIMAGEURL.png",
        "Birth Date": "15/10/2001",
        "Nationality": "Mexico",
        "Height": 1.85,
        "Category": "Junior",
        "Competitions": ["500 meter Backstroke", "100 meter Freestyle", "200 meter Breaststroke"],
        "Gold Medals": 0,
        "Silver Medals": 2,
        "Bronze Medals": 1
      },
      {...}
      ]
  },
  {
      "id": 8,
      "name": "Basketball",
      "sports-logo-url": "http://SPORTSLOGOURL.png",
      "players": [
      {
          "id": 2315,
        "Name": "Jane Doe",
        "player-image-url": "http://PLAYERIMAGEURL.png",
        "Birth Date": "08/05/1997",
        "Nationality": "Mexico",
        "Height": 1.92,
        "Category": "Open",
        "Position": "Point Guard",
        "Points": 20
      },
      {...}
      ]
  },
  {...}
]
```

This endpoint retrieves information of all players that participate in each sport for a certain country.

### HTTP Request

`GET http://jmp2019.com/api/v1/COUNTRY`

### Query Headers

Header | Default | Description
--------- | ------- | -----------
Authorization | null | You need to insert your APIKEY to get results.

### URL Parameters

Parameter | Type | Description
--------- | ------- | -----------
COUNTRY | String | The name of the country you want information from. If the country contains two words separate them with: <code>-</code>

<aside class="notice">Note: Player Keys and Values may vary depending on the sport.</aside>
















## Get All Sports Data

```csharp
static HttpClient client = new HttpClient();

public JArray GetSportsData()
{
    HttpWebRequest response = (HttpWebRequest)WebRequest.Create("http://jmp2019.com/api/v1/sports");

    response.UseDefaultCredentials = true;
    response.Headers.Add("Authorization", "APIKEY");

    HttpWebResponse answer = (HttpWebResponse)response.GetResponse();

    if (answer.StatusCode == HttpStatusCode.OK)
    {
        Stream value = answer.GetResponseStream();
        StreamReader _value = new StreamReader(value);
        if (value == null)
        {
            Console.WriteLine("Api Value Is Null");
        }

        var data = JArray.Parse(_value.ReadToEnd());
        return data;
    }
    return null;
}

JArray data = GetSportsData();
```

```javascript

```

> You must replace <code>APIKEY</code> with your personal API key.

> The above command returns JSON structured like this:

```json
[
  {
    "id": 5,
    "sport": "Swimming",
    "sports-logo-url": "http://SPORTSLOGOURL.png"
  },
  {
      "id": 8,
      "sport": "Basketball",
      "sports-logo-url": "http://SPORTSLOGOURL.png"
  }
  {...}
]
```

This endpoint retrieves information of all sports in the Maccabiah containing the countries that participate in each one and the players that participate in each country.

### HTTP Request

`GET http://jmp2019.com/api/v1/sports`

### Query Headers

Header | Default | Description
--------- | ------- | -----------
Authorization | null | You need to insert your APIKEY to get results.

















## Get All Sport/Countries Data

```csharp
static HttpClient client = new HttpClient();

public JArray GetSportCountriesData()
{
    HttpWebRequest response = (HttpWebRequest)WebRequest.Create("http://jmp2019.com/api/v1/SPORT");

    response.UseDefaultCredentials = true;
    response.Headers.Add("Authorization", "APIKEY");

    HttpWebResponse answer = (HttpWebResponse)response.GetResponse();

    if (answer.StatusCode == HttpStatusCode.OK)
    {
        Stream value = answer.GetResponseStream();
        StreamReader _value = new StreamReader(value);
        if (value == null)
        {
            Console.WriteLine("Api Value Is Null");
        }

        var data = JArray.Parse(_value.ReadToEnd());
        return data;
    }
    return null;
}

JArray data = GetSportCountriesData();
```

```javascript

```

> You must replace <code>APIKEY</code> with your personal API key.

> You must replace <code>SPORT</code> with a specific sport name as listed on the left.

> The above command returns JSON structured like this:

```json
[
  {
      "id": 15,
      "name": "Brazil",
      "flag-image-url": "http://FLAGIMAGEURL.png",
      "players": [
      {
          "id": 2560,
        "Name": "John Doe",
        "player-image-url": "http://PLAYERIMAGEURL.png",
        "Birth Date": "15/10/2001",
        "Nationality": "Brazil",
        "Height": 1.85,
        "Category": "Junior",
        "Competitions": ["500 meter Backstroke", "100 meter Freestyle", "200 meter Breaststroke"],
        "Gold Medals": 0,
        "Silver Medals": 2,
        "Bronze Medals": 1
      },
      {...}
      ]
  },
  {
      "id": 13,
      "name": "Chile",
      "flag-image-url": "http://FLAGIMAGEURL.png",
      "players": [
      {
          "id": 3561,
        "Name": "Jane Doe",
        "player-image-url": "http://PLAYERIMAGEURL.png",
        "Birth Date": "08/05/1997",
        "Nationality": "Chile",
        "Height": 1.92,
        "Category": "Open",
        "Competitions": ["300 meter Freestyle", "200 meter Breaststroke"],
        "Gold Medals": 3,
        "Silver Medals": 0,
        "Bronze Medals": 0
      },
      {...}
      ]
  },
  {...}
]
```

This endpoint retrieves information of all players that participate in each country for a certain sport.

### HTTP Request

`GET http://jmp2019.com/api/v1/SPORT`

### Query Headers

Header | Default | Description
--------- | ------- | -----------
Authorization | null | You need to insert your APIKEY to get results.

### URL Parameters

Parameter | Type | Description
--------- | ------- | -----------
SPORT | String | The name of the sport you want the standings of. Its value can be any of the following: `Open-Waters`, `Chess`, `Basketball`, `Cycling`, `Horse-Riding`, `Soccer`, `Futsal`, `Olimpic-Gymnastics`, `Rhythmic-Gymnastics`, `Golf`, `Field-Hockey`, `Karate`, `Macabiman`, `Triathlon`, `Half-Marathon`, `Swimming`, `Paddle`, `Squash`, `Softball`, `Tenis`, `Table-Tenis`, `Archery`, `Volleyball`, `Beach-Volleyball`, `Water-Polo`

<aside class="notice">Note: Player Keys and Values may vary depending on the sport.</aside>














## Get List of Competitions by Sport

```csharp
static HttpClient client = new HttpClient();

public JArray GetListOfCompetitions()
{
    HttpWebRequest response = (HttpWebRequest)WebRequest.Create("http://jmp2019.com/api/v1/SPORT/competitions");

    response.UseDefaultCredentials = true;
    response.Headers.Add("Authorization", "APIKEY");

    HttpWebResponse answer = (HttpWebResponse)response.GetResponse();

    if (answer.StatusCode == HttpStatusCode.OK)
    {
        Stream value = answer.GetResponseStream();
        StreamReader _value = new StreamReader(value);
        if (value == null)
        {
            Console.WriteLine("Api Value Is Null");
        }

        var data = JArray.Parse(_value.ReadToEnd());
        return data;
    }
    return null;
}

JArray data = GetListOfCompetitions();
```

```javascript

```

> You must replace <code>APIKEY</code> with your personal API key.

> You must replace <code>SPORT</code> with a specific sport name as listed on the left.

> The above command returns JSON structured like this:

```json
[
  {
    "id": 256,
    "name": "500 meter Breaststroke",
    "sport": "Swimming"
  },
  {
    "id": 257,
    "name": "300 meter Freestyle",
    "sport": "Swimming"
  }
  {...}
]
```

This endpoint retrieves a list of all competitions inside a certain sport.

### HTTP Request

`GET http://jmp2019.com/api/v1/SPORT/competitions`

### Query Headers

Header | Default | Description
--------- | ------- | -----------
Authorization | null | You need to insert your APIKEY to get results.

### URL Parameters

Parameter | Type | Description
--------- | ------- | -----------
SPORT | String | The name of the sport you want the standings of. Its value can be any of the following: `Open-Waters`, `Chess`, `Basketball`, `Cycling`, `Horse-Riding`, `Soccer`, `Futsal`, `Olimpic-Gymnastics`, `Rhythmic-Gymnastics`, `Golf`, `Field-Hockey`, `Karate`, `Macabiman`, `Triathlon`, `Half-Marathon`, `Swimming`, `Paddle`, `Squash`, `Softball`, `Tenis`, `Table-Tenis`, `Archery`, `Volleyball`, `Beach-Volleyball`, `Water-Polo`













## Get Standings for a Competition


```csharp
static HttpClient client = new HttpClient();

public JArray GetCompetitionStandings()
{
    HttpWebRequest response = (HttpWebRequest)WebRequest.Create("http://jmp2019.com/api/v1/standings/COMPETITION");

    response.UseDefaultCredentials = true;
    response.Headers.Add("Authorization", "APIKEY");

    HttpWebResponse answer = (HttpWebResponse)response.GetResponse();

    if (answer.StatusCode == HttpStatusCode.OK)
    {
        Stream value = answer.GetResponseStream();
        StreamReader _value = new StreamReader(value);
        if (value == null)
        {
            Console.WriteLine("Api Value Is Null");
        }

        var data = JArray.Parse(_value.ReadToEnd());
        return data;
    }
    return null;
}

JArray data = GetCompetitionStandings();
```

```javascript

```

> You must replace <code>APIKEY</code> with your personal API key.

> You must replace <code>COMPETITION</code> with a specific competition name.

> The above command returns JSON structured like this:

> Swimming-300 meter Freestyle:

```json
[
  {
    "id": 155,
    "position": 1,
    "name": "John Doe",
    "country-short": "CAN",
    "image-url": "http://IMAGEURL.png",
    "stats": {
          "Heat 1": "2:57",
          "Heat 2": "1:32",
          "Heat 3": "1:45",
          "Total": "6:14"
    }
  },
  {
    "id": 172,
    "position": 2,
    "name": "Jane Doe",
    "country-short": "VEN",
    "image-url": "http://IMAGEURL.png",
    "stats": {
          "Heat 1": "2:41",
          "Heat 2": "2:02",
          "Heat 3": "1:55",
          "Total": "6:38"
    }
  },
  {...}
]
```

> Basketball Open:
```json
[
  {
    "id": 155,
    "position": 1
    "name": "Canada",
    "country-short": "CAN",
    "image-url": "http://IMAGEURL.png,
    "stats": {
        "W-L": "32-6",
        "%": "0.842",
        "PF": "113.5",
        "PA": "107.5"
    }
  },
  {
    "id": 172,
    "position": 2
    "name": "Venezuela",
    "country-short": "VEN",
    "image-url": "http://IMAGEURL.png,
    "stats": {
        "W-L": "20-18",
        "%": "0.526",
        "PF": "109.0",
        "PA": "109.0"
    }
  },
  {...}
]
```

This endpoint retrieves the standings of a specific competition.

### HTTP Request

`GET http://jmp2019.com/api/v1/standings/COMPETITION`

### Query Headers

Header | Default | Description
--------- | ------- | -----------
Authorization | null | You need to insert your APIKEY to get results.

### URL Parameters

Parameter | Type | Description
--------- | ------- | -----------
COMPETITION | Integer | The ID of the competition you want the standings of.
















## Get All Medals by Country

```csharp
static HttpClient client = new HttpClient();

public JArray GetAllMedals()
{
    HttpWebRequest response = (HttpWebRequest)WebRequest.Create("http://jmp2019.com/api/v1/medals");

    response.UseDefaultCredentials = true;
    response.Headers.Add("Authorization", "APIKEY");

    HttpWebResponse answer = (HttpWebResponse)response.GetResponse();

    if (answer.StatusCode == HttpStatusCode.OK)
    {
        Stream value = answer.GetResponseStream();
        StreamReader _value = new StreamReader(value);
        if (value == null)
        {
            Console.WriteLine("Api Value Is Null");
        }

        var data = JArray.Parse(_value.ReadToEnd());
        return data;
    }
    return null;
}

JArray data = GetAllMedals();
```

```javascript

```

> You must replace <code>APIKEY</code> with your personal API key.

> The above command returns JSON structured like this:

```json
[
  {
    "id": 5,
    "position": 1,
    "name": "Mexico",
    "flag-image-url": "http://FLAGIMAGEURL.png",
    "gold": 9,
    "silver": 12,
    "bronze" 5
  },
  {
      "id": 8,
      "position": 2,
      "name": "Argentina",
      "flag-image-url": "http://FLAGIMAGEURL.png",
      "gold": 7,
    "silver": 7,
    "bronze" 0
  },
  {
      "id": 10,
      "position": 3,
      "name": "Brazil",
      "flag-image-url": "http://FLAGIMAGEURL.png",
      "gold": 4,
    "silver": 9,
    "bronze" 2
  },
  {...}
]
```

This endpoint retrieves the table of all medals earned by each country in the Maccabiah sorted by most gold medals.

### HTTP Request

`GET http://jmp2019.com/api/v1/medals`

### Query Headers

Header | Default | Description
--------- | ------- | -----------
Authorization | null | You need to insert your APIKEY to get results.












## Get Medals by Country on a Sport

```csharp
static HttpClient client = new HttpClient();

public JArray GetMedalsSport()
{
    HttpWebRequest response = (HttpWebRequest)WebRequest.Create("http://jmp2019.com/api/v1/medals/SPORT");

    response.UseDefaultCredentials = true;
    response.Headers.Add("Authorization", "APIKEY");

    HttpWebResponse answer = (HttpWebResponse)response.GetResponse();

    if (answer.StatusCode == HttpStatusCode.OK)
    {
        Stream value = answer.GetResponseStream();
        StreamReader _value = new StreamReader(value);
        if (value == null)
        {
            Console.WriteLine("Api Value Is Null");
        }

        var data = JArray.Parse(_value.ReadToEnd());
        return data;
    }
    return null;
}

JArray data = GetMedalsSport();
```

```javascript

```

> You must replace <code>APIKEY</code> with your personal API key.

> You must replace <code>SPORT</code> with a specific sport name as listed on the left.

> The above command returns JSON structured like this:

```json
[
  {
    "id": 5,
    "position": 1,
    "name": "Mexico",
    "flag-image-url": "http://FLAGIMAGEURL.png",
    "gold": 9,
    "silver": 12,
    "bronze" 5
  },
  {
      "id": 8,
      "position": 2,
      "name": "Argentina",
      "flag-image-url": "http://FLAGIMAGEURL.png",
      "gold": 7,
    "silver": 7,
    "bronze" 0
  },
  {
      "id": 10,
      "position": 3,
      "name": "Brazil",
      "flag-image-url": "http://FLAGIMAGEURL.png",
      "gold": 4,
    "silver": 9,
    "bronze" 2
  },
  {...}
]
```

This endpoint retrieves the table of all medals earned by each country in the Maccabiah sorted by most gold medals filtered by a specific sport.

### HTTP Request

`GET http://jmp2019.com/api/v1/medals/SPORT`

### Query Headers

Header | Default | Description
--------- | ------- | -----------
Authorization | null | You need to insert your APIKEY to get results.

### URL Parameters

Parameter | Type | Description
--------- | ------- | -----------
SPORT | String | The name of the sport you want the medals of. Its value can be any of the following: `Open-Waters`, `Chess`, `Basketball`, `Cycling`, `Horse-Riding`, `Soccer`, `Futsal`, `Olimpic-Gymnastics`, `Rhythmic-Gymnastics`, `Golf`, `Field-Hockey`, `Karate`, `Macabiman`, `Triathlon`, `Half-Marathon`, `Swimming`, `Paddle`, `Squash`, `Softball`, `Tenis`, `Table-Tenis`, `Archery`, `Volleyball`, `Beach-Volleyball`, `Water-Polo`











## Get Medals by Sport on a Country

```csharp
static HttpClient client = new HttpClient();

public JArray GetMedalsCountry()
{
    HttpWebRequest response = (HttpWebRequest)WebRequest.Create("http://jmp2019.com/api/v1/medals/COUNTRY");

    response.UseDefaultCredentials = true;
    response.Headers.Add("Authorization", "APIKEY");

    HttpWebResponse answer = (HttpWebResponse)response.GetResponse();

    if (answer.StatusCode == HttpStatusCode.OK)
    {
        Stream value = answer.GetResponseStream();
        StreamReader _value = new StreamReader(value);
        if (value == null)
        {
            Console.WriteLine("Api Value Is Null");
        }

        var data = JArray.Parse(_value.ReadToEnd());
        return data;
    }
    return null;
}

JArray data = GetMedalsCountry();
```

```javascript

```

> You must replace <code>APIKEY</code> with your personal API key.

> You must replace <code>COUNTRY</code> with a specific country name.

> The above command returns JSON structured like this:

```json
[
  {
    "id": 5,
    "position": 1,
    "name": "Swimming",
    "flag-image-url": "http://FLAGIMAGEURL.png",
    "gold": 9,
    "silver": 12,
    "bronze" 5
  },
  {
      "id": 8,
      "position": 2,
      "name": "Golf",
      "flag-image-url": "http://FLAGIMAGEURL.png",
      "gold": 7,
    "silver": 7,
    "bronze" 0
  },
  {
      "id": 10,
      "position": 3,
      "name": "Volleyball",
      "flag-image-url": "http://FLAGIMAGEURL.png",
      "gold": 4,
    "silver": 9,
    "bronze" 2
  },
  {...}
]
```

This endpoint retrieves the table of all medals earned on different sports by a country in the Maccabiah sorted by most gold medals.

### HTTP Request

`GET http://jmp2019.com/api/v1/medals/COUNTRY`

### Query Headers

Header | Default | Description
--------- | ------- | -----------
Authorization | null | You need to insert your APIKEY to get results.

### URL Parameters

Parameter | Type | Description
--------- | ------- | -----------
COUNTRY | String | The name of the country you want the medals of.

## Get Schedule and Results by Country

```csharp
static HttpClient client = new HttpClient();

public JArray GetScheduleCountry()
{
    HttpWebRequest response = (HttpWebRequest)WebRequest.Create("http://jmp2019.com/api/v1/medals/COUNTRY");

    response.UseDefaultCredentials = true;
    response.Headers.Add("Authorization", "APIKEY");

    HttpWebResponse answer = (HttpWebResponse)response.GetResponse();

    if (answer.StatusCode == HttpStatusCode.OK)
    {
        Stream value = answer.GetResponseStream();
        StreamReader _value = new StreamReader(value);
        if (value == null)
        {
            Console.WriteLine("Api Value Is Null");
        }

        var data = JArray.Parse(_value.ReadToEnd());
        return data;
    }
    return null;
}

JArray data = GetScheduleCountry();
```

```javascript

```

> You must replace <code>APIKEY</code> with your personal API key.

> You must replace <code>COUNTRY</code> with a specific country name.

> The above command returns JSON structured like this:


> Type 0 Event

```json
{
  "Day 1": [
    {
      "type": 0,
      "name": "Opening Ceremony",
      "description": "This is the description of the opening ceremony.",
      "time": "6:00pm",
      "venue": "CDI",
      "image": "http://IMAGEURL.png"
    }
  ]
}
```

> Type 1 Event

```json
{
  "Day 5": [
    {
      "type": 1,
      "data": {
        "sport": "Basketball",
        "category": "Masters",
        "venue": "CDI",
        "team1Name": "México",
        "team2Name": "Canada",
        "flag1-image-url": "http://FLAGIMAGEURL.png",
        "flag2-image-url": "http://FLAGIMAGEURL.png",
        "time": "6:00pm"
      },
      "results": {
        "state": "Final",
        "team1Points": 87,
        "team2Points": 95
      }
    }
  ]
}
```

> Type 2 Event

```json
{
  "Day 12": [
    {
      "type": 1,
      "data": {
        "sport": "Karate",
        "category": "Masters",
        "venue": "CDI",
        "team1Name": "México",
        "team2Name": "Canada",
        "team1PlayerName": "John Doe",
        "team2PlayerName": "Jane Doe",
        "flag1-image-url": "http://FLAGIMAGEURL.png",
        "flag2-image-url": "http://FLAGIMAGEURL.png",
        "time": "6:00pm"
      },
      "results": {
        "state": "Final",
        "team1Points": 87,
        "team2Points": 95
      }
    }
  ]
}
```

> Type 3 Event

```json
{
  "Day 2": [
    {
      "type": 1,
      "data": {
        "sport": "Volleyball",
        "category": "Masters",
        "venue": "CDI",
        "team1Name": "México",
        "team2Name": "Canada",
        "flag1-image-url": "http://FLAGIMAGEURL.png",
        "flag2-image-url": "http://FLAGIMAGEURL.png",
        "time": "6:00pm"
      },
      "results": {
        "state": "Final",
        resultsPDF: "http://PDFFILENAME.png"
      }
    }
  ]
}
```

> Type 4 Event

```json
{
  "Day 7": [
    {
      "type": 1,
      "data": {
        "sport": "Tennis",
        "category": "Masters",
        "venue": "CDI",
        "team1Name": "México",
        "team2Name": "Canada",
        "team1PlayerName": "John Doe",
        "team2PlayerName": "Jane Doe",
        "flag1-image-url": "http://FLAGIMAGEURL.png",
        "flag2-image-url": "http://FLAGIMAGEURL.png",
        "time": "6:00pm"
      },
      "results": {
        "state": "Final",
        resultsPDF: "http://PDFFILENAME.png"
      }
    }
  ]
}
```

> Type 5 Event

```json
{
  "Day 11": [
    {
      "type": 1,
      "data": {
        "sport": "Tennis",
        "category": "Masters",
        "venue": "CDI",
        "competitors": [{"name": "John Doe", "country": "México"}, {"name": "Jane Doe", "country": "Canada"}, {...}],
        "time": "6:00pm"
      },
      "results": {
        "state": "Final",
        "resultsPDF": "http://PDFFILENAME.png"
      }
    }
  ]
}
```

This endpoint retrieves the schedule with events and results of every different sport for a country in the Maccabiah sorted by most gold medals. Events will be ordered chronologically.

### HTTP Request

`GET http://jmp2019.com/api/v1/medals/COUNTRY`

### Query Headers

Header | Default | Description
--------- | ------- | -----------
Authorization | null | You need to insert your APIKEY to get results.

### URL Parameters

Parameter | Type | Description
--------- | ------- | -----------
COUNTRY | String | The name of the country you want the schedule of.

### Types of events on JSON response

Events will have a `Type` which will determine what parameters are in it. Events of different types will be combined in the same response ordered chronologically

Type | Usage | Description
--------- | ------- | -----------
`0` | `General events` | This result is returned when an important event is added to the calendar. Example: Opening Ceremony, Closing Party
`1` | Sport with `2 Teams` and `Score Result` | This result is returned when the sport has two teams and the result is only one `String` value for each team. Example: Soccer, Basketball
`2` | Sport with `2 Teams`, `Score Result`, and `Player Names` | This result is returned when the sport is played 1 vs 1, has two teams, and the result is only one `String` value for each team. Example: Chess, Karate
`3` | Sport with `2 Teams` and `Complex Result` | This result is returned when the sport has two teams and the result is more complex. It will contain a special PDF displaying the results. Example: Volleyball
`4` | Sport with `2 Teams`, `Complex Result`, and `Player Names` | This result is returned when the sport is played 1 vs 1, has two teams, and the result is more complex. It will contain a special PDF displaying the results. Example: Tennis
`5` | Sport with `Multiple competitors` | This result is returned when the sport has many competitors. It will contain a special PDF displaying the results. Example: Swimming, Marathon

## Get Schedule and Results by Sport

## Get All Venues

## Get Live Streams Data

## Athlete Central

## Partners And Sponsors

## Contact
