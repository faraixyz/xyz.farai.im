---
title: "My First Chrome Extension: The Story of QuickPush"
date: 2016-01-17
lastmod: 2019-10-28
description: On the time I made a Chrome Extension to search music on Spotify.
projects: [quickpush]
tech: [js, web-extensions]
tags: [obsolete]
draft: false
---

Over Christmas, I got bored so I decided to use the skills I picked up whilst learning front end development. To do this, I made a QuickPush, a Chrome Extension which searches for music on Spotify.

While I have made a Chrome Extension before, I procrastinated on it for so long that by the time I wanted to finish it, the website's HTML changed. With my new found curiosity, I decided to take another shot at making a Chrome Extension.

## Step 0: The Idea

I like [trap music](https://en.wikipedia.org/wiki/Trap_music). So much so that I would watch [obnoxious YouTube videos](https://www.reddit.com/r/montageparodies/ "/r/montageparodies")[^1] just to expand my playlist of trap songs. When I heard a song I liked, I would have to pull out my phone and search for it. This Chrome Extension would allow me to search for songs without having to leave my web browser. A first world problem, but a problem I could solve.

## Figuring Out How Chrome Extensions Work

To start off with, I installed the unsupported [Chrome Dev Editor](https://chrome.google.com/webstore/detail/chrome-dev-editor/pnoffddplpippgcfjdhbmhkofpnaalpg?utm_source=chrome-ntp-icon) as it would create the files I would need for the project. While the files were set up, I didn't understand what any of the boilerplate code was supposed to do.

At this point, I decided to read the [official documentation] to get an idea of what I was supposed to do. At the same time, I followed a [tutorial by Gabe Berke-Williams](https://robots.thoughtbot.com/how-to-make-a-chrome-extension). Eventually, I was able to get an idea of what all the files did. The files were,

* `manifest.json` defines the extensions metadata which contains the name, accompanying scripts, permissions, assets etc.,
* `background.js` is an optional file which allows the extension to work with the Chrome Browser's features, like opening a new tab. It also allows extensions to communicate with various `content.js` scripts
* `content.js` is another optional file which is needed to manipulate a web page. An extension can have many `content.js` files.
* `popup.html`, `popup.js`, `popup.style` are needed to manipulate popups. This is what I spent most of my time manipulating while making QuickPush.

## Learning how to use Spotify's Web API

**Note: As of July 2017, Spotify changed access control to their API, so these examples won't work without an OAuth Token**

At first, I wanted to include both SoundCloud and Spotify, but the SoundCloud API was really hard to use. I might add SoundCloud in the future.

Using [Spotify's API](https://developer.spotify.com/web-api/), specifically the [`/v1/search`](https://developer.spotify.com/web-api/search-item/) endpoint, I would be able to search Spotify for a given song. The search endpoint requires

* A URI encoded[^2] **query** and,
* An **item type** which could either be a *track*, *album*, *playlist* or *artist*.

Optionally, you can specify
* where to start listing results with an **offset**. Useful when you want to get additional search results beyond your specified limit,
* A **limit** to how many results you want to return (default at 5, maximum at 50), and
* The target **market** you want to search and
* An **OAuth token** if a market is needed.

As an example, let's say that you want to search [this catchy song[VIDEO]](https://www.youtube.com/watch?v=dQw4w9WgXcQ). To do that, you will send an [<abbr title="Asynchronous JavaScript and XML">AJAX</abbr>](https://developer.mozilla.org/en-US/docs/AJAX/Getting_Started) request to

```txt
https://api.spotify.com/v1/search?q=Never+Gonna+Give+You+Up&type=track&limit=2
```

The above will query for a `track` called `Never Gonna Give You Up` limited to `2` results.

I made an AJAX request like so,

```js
//popup.js
//The following code submits a search request to Spotify
 var spotifySearchUrl = "https://api.spotify.com/v1/search?query=$query&offset=0&limit=50&type=track"; //This is Spotify's search uri

 function submitSearch() {
        var searchTerm = encodeURIComponent(query.value);//encodes the query
        var search = spotifySearchUrl.replace(/\$query/, searchTerm);//Adds the query to the URI
        
        //This is the AJAX stuff
        var xhttp = new XMLHttpRequest();
        xhttp.onreadystatechange = function () {
            if (xhttp.readyState == 4 && xhttp.status == 200) {
                var responseText = JSON.parse(xhttp.responseText); //This turns the resulting JSON into a JS string
                renderSpotifySong(responseText);//This will pur the results onto the page
            }
        };
        xhttp.open("GET", search, true);
        xhttp.send(null);
    } 
```
If all goes well, you should get the following response

```json
{  
   "tracks":{  
      "href":"https://api.spotify.com/v1/search?query=Never+Gonna+Give+You+Up&offset=0&limit=2&type=track",
      "items":[  
         {  
            "album":{  
               "album_type":"compilation",
               "available_markets":[  
                  "AD",
                  "AR",
                  "AT",
                  "AU",
                  "BE",
                  "BG",
                  "BO",
                  "BR",
                  "CA",
                  "CH",
                  "CL",
                  "CO",
                  "CR",
                  "CY",
                  "CZ",
                  "DE",
                  "DK",
                  "DO",
                  "EC",
                  "EE",
                  "ES",
                  "FI",
                  "FR",
                  "GB",
                  "GR",
                  "GT",
                  "HN",
                  "HU",
                  "IE",
                  "IS",
                  "IT",
                  "LI",
                  "LT",
                  "LU",
                  "LV",
                  "MC",
                  "MT",
                  "MX",
                  "NI",
                  "NL",
                  "NO",
                  "NZ",
                  "PA",
                  "PE",
                  "PL",
                  "PT",
                  "PY",
                  "RO",
                  "SE",
                  "SI",
                  "SK",
                  "SV",
                  "TR",
                  "UY"
               ],
               "external_urls":{  
                  "spotify":"https://open.spotify.com/album/2mCuMNdJkoyiXFhsQCLLqw"
               },
               "href":"https://api.spotify.com/v1/albums/2mCuMNdJkoyiXFhsQCLLqw",
               "id":"2mCuMNdJkoyiXFhsQCLLqw",
               "images":[  
                  {  
                     "height":640,
                     "url":"https://i.scdn.co/image/aac6bed4cf214652c88137dca9152362eb55f961",
                     "width":640
                  },
                  {  
                     "height":300,
                     "url":"https://i.scdn.co/image/5246898e19195715e65e261899baba890a2c1ded",
                     "width":300
                  },
                  {  
                     "height":64,
                     "url":"https://i.scdn.co/image/7590dba648ae5e3c7c57f2fe05cfd424de55fab4",
                     "width":64
                  }
               ],
               "name":"The Best Of",
               "type":"album",
               "uri":"spotify:album:2mCuMNdJkoyiXFhsQCLLqw"
            },
            "artists":[  
               {  
                  "external_urls":{  
                     "spotify":"https://open.spotify.com/artist/0gxyHStUsqpMadRV0Di1Qt"
                  },
                  "href":"https://api.spotify.com/v1/artists/0gxyHStUsqpMadRV0Di1Qt",
                  "id":"0gxyHStUsqpMadRV0Di1Qt",
                  "name":"Rick Astley",
                  "type":"artist",
                  "uri":"spotify:artist:0gxyHStUsqpMadRV0Di1Qt"
               }
            ],
            "available_markets":[  
               "AD",
               "AR",
               "AT",
               "AU",
               "BE",
               "BG",
               "BO",
               "BR",
               "CA",
               "CH",
               "CL",
               "CO",
               "CR",
               "CY",
               "CZ",
               "DE",
               "DK",
               "DO",
               "EC",
               "EE",
               "ES",
               "FI",
               "FR",
               "GB",
               "GR",
               "GT",
               "HN",
               "HU",
               "IE",
               "IS",
               "IT",
               "LI",
               "LT",
               "LU",
               "LV",
               "MC",
               "MT",
               "MX",
               "NI",
               "NL",
               "NO",
               "NZ",
               "PA",
               "PE",
               "PL",
               "PT",
               "PY",
               "RO",
               "SE",
               "SI",
               "SK",
               "SV",
               "TR",
               "UY"
            ],
            "disc_number":1,
            "duration_ms":213453,
            "explicit":false,
            "external_ids":{  
               "isrc":"GBARL8700052"
            },
            "external_urls":{  
               "spotify":"https://open.spotify.com/track/6JEK0CvvjDjjMUBFoXShNZ"
            },
            "href":"https://api.spotify.com/v1/tracks/6JEK0CvvjDjjMUBFoXShNZ",
            "id":"6JEK0CvvjDjjMUBFoXShNZ",
            "name":"Never Gonna Give You Up",
            "popularity":67,
            "preview_url":"https://p.scdn.co/mp3-preview/c28ac8b0a23f0ffc3789661168068b1efa099d92",
            "track_number":1,
            "type":"track",
            "uri":"spotify:track:6JEK0CvvjDjjMUBFoXShNZ"
         },
         {  
            "album":{  
               "album_type":"album",
               "available_markets":[  
                  "AD",
                  "AR",
                  "AT",
                  "AU",
                  "BE",
                  "BG",
                  "BO",
                  "BR",
                  "CA",
                  "CH",
                  "CL",
                  "CO",
                  "CR",
                  "CY",
                  "CZ",
                  "DE",
                  "DK",
                  "DO",
                  "EC",
                  "EE",
                  "ES",
                  "FI",
                  "FR",
                  "GB",
                  "GR",
                  "GT",
                  "HK",
                  "HN",
                  "HU",
                  "IE",
                  "IS",
                  "IT",
                  "LI",
                  "LT",
                  "LU",
                  "LV",
                  "MC",
                  "MT",
                  "MX",
                  "MY",
                  "NI",
                  "NL",
                  "NO",
                  "NZ",
                  "PA",
                  "PE",
                  "PH",
                  "PL",
                  "PT",
                  "PY",
                  "RO",
                  "SE",
                  "SG",
                  "SI",
                  "SK",
                  "SV",
                  "TR",
                  "TW",
                  "UY"
               ],
               "external_urls":{  
                  "spotify":"https://open.spotify.com/album/6N9PS4QXF1D0OWPk0Sxtb4"
               },
               "href":"https://api.spotify.com/v1/albums/6N9PS4QXF1D0OWPk0Sxtb4",
               "id":"6N9PS4QXF1D0OWPk0Sxtb4",
               "images":[  
                  {  
                     "height":640,
                     "url":"https://i.scdn.co/image/0fb039c2cb59cb5703a8e33e9a998dd4031887df",
                     "width":640
                  },
                  {  
                     "height":300,
                     "url":"https://i.scdn.co/image/028fc62c9e077fa3272ed6343bbd88d741a97f86",
                     "width":300
                  },
                  {  
                     "height":64,
                     "url":"https://i.scdn.co/image/d06720ca93a55cb751dd74c9fac887924b6f7dd0",
                     "width":64
                  }
               ],
               "name":"Whenever You Need Somebody",
               "type":"album",
               "uri":"spotify:album:6N9PS4QXF1D0OWPk0Sxtb4"
            },
            "artists":[  
               {  
                  "external_urls":{  
                     "spotify":"https://open.spotify.com/artist/0gxyHStUsqpMadRV0Di1Qt"
                  },
                  "href":"https://api.spotify.com/v1/artists/0gxyHStUsqpMadRV0Di1Qt",
                  "id":"0gxyHStUsqpMadRV0Di1Qt",
                  "name":"Rick Astley",
                  "type":"artist",
                  "uri":"spotify:artist:0gxyHStUsqpMadRV0Di1Qt"
               }
            ],
            "available_markets":[  
               "AD",
               "AR",
               "AT",
               "AU",
               "BE",
               "BG",
               "BO",
               "BR",
               "CA",
               "CH",
               "CL",
               "CO",
               "CR",
               "CY",
               "CZ",
               "DE",
               "DK",
               "DO",
               "EC",
               "EE",
               "ES",
               "FI",
               "FR",
               "GB",
               "GR",
               "GT",
               "HK",
               "HN",
               "HU",
               "IE",
               "IS",
               "IT",
               "LI",
               "LT",
               "LU",
               "LV",
               "MC",
               "MT",
               "MX",
               "MY",
               "NI",
               "NL",
               "NO",
               "NZ",
               "PA",
               "PE",
               "PH",
               "PL",
               "PT",
               "PY",
               "RO",
               "SE",
               "SG",
               "SI",
               "SK",
               "SV",
               "TR",
               "TW",
               "UY"
            ],
            "disc_number":1,
            "duration_ms":213573,
            "explicit":false,
            "external_ids":{  
               "isrc":"GBARL9300135"
            },
            "external_urls":{  
               "spotify":"https://open.spotify.com/track/4uLU6hMCjMI75M1A2tKUQC"
            },
            "href":"https://api.spotify.com/v1/tracks/4uLU6hMCjMI75M1A2tKUQC",
            "id":"4uLU6hMCjMI75M1A2tKUQC",
            "name":"Never Gonna Give You Up",
            "popularity":60,
            "preview_url":"https://p.scdn.co/mp3-preview/a69cabb16c6c3333db903d1f538e808493689e40",
            "track_number":1,
            "type":"track",
            "uri":"spotify:track:4uLU6hMCjMI75M1A2tKUQC"
         }
      ],
      "limit":2,
      "next":"https://api.spotify.com/v1/search?query=Never+Gonna+Give+You+Up&offset=2&limit=2&type=track",
      "offset":0,
      "previous":null,
      "total":1275
   }
}
```

If you remember seeing `JSON.parse(xttp.responseText)`, `JSON.parse()` converts the the response JSON into a JavaScript object. With this object, we can then render the information into the popup.

## Making the Extension

Having understood how Chrome extensions are structures as well as how to use the Spotify API, I was able to put it all together. For HTML, I decided to keep it very simple. 

```html
<!--popup.html-->
<!-- This code is how a song will render on the page -->
<div class="song spotify temp"><img class="cover" src="http://www.isaacjewelers.com/img/cms/VersaceB.png">
            <ul class="song_info">
                <li class="song_name">This is an unessesarily long ass song title so that I can see </li>
                <li class="song_artist">Artist A, Artist B, Artist C, Artist D, Artist E, Artist FFFFFFFFFFFFF</li>
                <li class="provider"><a href="#" title="See on Spotify" target="_blank"><i class="fa fa-spotify"></i></a></li>
            </ul>
            <div class="actions">
                <button type="button" class="btn addSong" id="$trackId"><i class="fa fa-plus"></i></button>
                <button type="button" class="btn preview play" id="$previewURL"> <i class="fa fa-play"></i></button>
            </div>
```

Each song will be represented by a `<div>` [^3] containing the song's cover art, an unordered list with the song's information as well as another `<div>` containing buttons to hear a preview of the song and to add it to a user's library.

While the HTML was easy to set up, styling the CSS proved difficult. Serves me right for lacking creativity.

Many hours later, I got something which looked halfway decent, with the help of [<abbr title="viewport">vw</abbr> units](https://developer.mozilla.org/en-US/docs/Web/CSS/length) and [flex boxes](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_CSS_flexible_boxes). Cross-browser support wasn't much of a problem since I only intend on supporting Chrome for some reason I can't explain.

{{% figure %}}
![A picture of the UI](/images/quickpush.png)
{{% figcaption %}}
Eh... good enough.
{{% /figcaption %}}
{{% /figure %}}

With the UI covered, it was time to work on the logic in `popup.js`. This is how it works.

1. It gets a search query from the search bar using a listener which listens for new key presses and searches as you type[^4].
2. The search bar's value serves as the input to the function `submitSearch()` function which performs the search using the code in the section *Making the Extension*.
3. The search results are then parsed by the `renderSpotifySongs()` function before they are rendered to the DOM with
4. `addToDOM` which uses pattern matching to put information onto the popup using a template. It also adds an `audioHandler`

If you need clarification, ask me. Otherwise, this blog post is already quite long and I need to move on[^5]. The source code, which I tried to tidy up and explain as best I could, is available on [GitHub](https://github.com/faraixyz/farais-code-graveyard/tree/master/QuickPush).

Testing the extension was just a matter of trial and error. I would try a thing and if it worked, yay. Otherwise, I would go back and hack through the code.

## Publishing

Once version 0.501[^6] was online, I committed the code and pushed it onto [GitHub](https://github.com/faraixyz/farais-code-graveyard/tree/master/QuickPush). In order to get the app on the store, I needed to give Google $5, upload a zip file with my code and add a (really bad) description and image. In the week it's been up, it has had 0 installs.

## What's In Store For Version 1
While this works as an MVP, I still want to do more stuff, such as

* **integrating SoundCloud** since it has a more diverse set of trap music compared to Spotify. SoundCloud's API needed client credentials in order to use it. I didn't know how to hide them, so I left it for another day.
* **allowing users to download songs on SoundCloud** if they're available for download on SoundCloud
* **allowing users to save songs to Spotify**. Right now, users have to click the Spotify logo under a search result to open the Spotify Desktop App in order to save a song. I tried to do this, but I needed to work with [OAuth](https://oauth.net/2/), which I don't understand.

Hopefully, I can get all this done in two weeks.

## Conclusion
Wow, you're awesome! You read this article right to the end. The code can be found [on GitHub](https://github.com/faraixyz/farais-code-graveyard/tree/master/QuickPush).

[^1]: Farai from 2017 speaking. While I still like trap music, montage parodies have become terrible, mainly because of how the creators who defined the medium have left who put a lot of effort into their videos.
[^2]: <dfn>[URI encoding](https://en.wikipedia.org/wiki/Percent-encoding)</dfn> refers to substituting certain reserved characters for a coded equivalent. For example, a space would be converted to `%20`.
[^3]: It's 2017 Farai again. Turns out that that it would have been better to use a `<template>` tag instead of putting the markup in a string because of HTML5 and semantic elements.
[^4]: Technically this was a bug, but I made it a feature. I wouldn't recommend this since it's a good way to reach a `429 Error` from making too many requests to their API.
[^5]: I could have just delayed posting this blog post and spent more time improving it. I really need to proofread.
[^6]: Can someone explain how to version software to me? I feel like I'm just randomly incrementing numbers.
