## 1. Write code that executes asynchronously
In the HTTP project we worked with two separate APIs to create a mashup of information that users could search through according to their specifications.
This meant relying on various fetch calls, often using urls retrieved elsewhere in the users' search.

```javascript
const generateScores = async (url) => {
  let result = await (await fetch(url)).json();
  let scores = await result.categories;
}
```
*In this example* we retrieve a url from a previous user search and await a fetch of the API. Different values returned are stored in variables for later use.

## 2. Use callbacks to access values that aren’t available synchronously
**generateScores**, shown in the point above, is then called within another function to allow the user to see further data if and when their search requires it.

```javascript
const printCityDetails = async (url) => {
  let city = await (await fetch(url)).json();
  canvas.innerHTML = "";
  
  printHTML(`
    <div id='score-card'>
      <h2 class='city__entry--title'>${city["full_name"]}</h2>
      <p class='city__entry--subtitle'>Mayor: ${city.mayor}</p>
    </div>
  `).then((element) => canvas.appendChild(element));
    
  generateScores(`${url}scores`);
}
```

## 3. Use promises to access values that aren’t available synchronously
The initial search in Spot Check may return various cities, but to obtain the data available for any of the search results we need to fetch it from a new url provided in the previous API call.

The function below receives the url provided within the object provided within the object returned form the first fetch and then makes a new API call with it.

```javascript
const printCityDetails = async (url) => {
  let city = await (await fetch(url)).json();

  //further code is omitted in this example
}
```
*This example* is also relevant for **learning point #4**
## 4. Use the fetch method to make HTTP requests and receive responses
The fetch method is called for input provided by the user via callbacks like the one seen below.

```javascript
const fetchTeleport = async (city) => {
  let result = await (
    await fetch(`https://api.teleport.org/api/cities/?search=${city}`)
  ).json();
  
  let matches = await result._embedded["city:search-results"];
  
  return matches;
};
```

## 5. Configure the options argument of the fetch method to make GET and POST requests

## 6. Use the map array method to create a new array containing new values
```javascript
let scores = result.map(score => `{field: ${score.name}, Score: ${score.score_out_of_10}}`);
```
*In this example*, the variable 'scores' stores a mapped version of the array of objects returned in a previous ```.fetch()``` call.
The shortened objects, with their keys renamed for ease of read, are later used to print data onto the page, similarly to what is shown in the learning outcomes #2 and #9.
## 7. Use the filter array method to create a new array with certain values removed
Searching a city may return several results. For example, searching for 'London' would return data for 'London, United Kingdom' and 'London, Ontario, Canada'.

We filter the list of results to include only cities within the UK, since the Police API only has information relevant to the United Kingdom.

```javascript
fetchTeleport(searchInput).then((matches) => {
  let ukRegex = new RegExp(/(United Kingdom)/);
  let filteredMatches = Object.values(matches).filter(match => ukRegex.test(match.matching_full_name));

  filteredMatches.forEach(match => {
    if (ukRegex.test(match["matching_full_name"])) {
      printSearchResults(match);
    }
  });
}
```
## 8. Access DOM nodes using a variety of selectors

```javascript
const canvas = document.querySelector("#canvas");
const crimeOccurrences = document.querySelector("#crime-occurrences");
const gifFig = document.querySelector("#gif-load");
```
*In this example*, three different elements are stored into variables using ```.querySelector()```. These elements are unique in our page so they are accessed through their ID attribute. 

Other ways to access elements would be:
- ```.getElementById()```, which would give us the same result for this case,
- ```.getElementsByClassName()```, which would produce an array of all elements with the same class and could easily be used to iterate through them
- ```.querySelectorAll()```, which would produce an array, but would allow us to target a type of element rather than their class attribute 
  - i.e.: ```document.querySelectorAll('input[type=text]')``` would access all text input fields

## 9. Add and remove DOM nodes to change the content on the page
The base HTML for this project is very bare and most elements are added, adapted or removed from the page via our javascript.
For this, we used two different methods.

```javascript
    let crimeScoreCard = document.createElement("div");
    crimeScoreCard.classList.add("canvas__score-card", 'canvas__score-card--crime');
    canvas.appendChild(crimeScoreCard);
```
*In this example*, an element is created using typical DOM manipulation. In this particular instance the function goes on to iterate through the data points handed to it asynchronously before collecting them to populate different elements on the page. We only needed to create the *crimeScoreCard* element so that other elements could later on be appended to it.

But sometimes we create a higher number of elements, potentially with intricate structures connecting them. For that, we use the second method.

```javascript
const printHTML = async (data) => {
  const template = document.createElement("template");
  template.innerHTML = data.trim();
  return template.content.firstChild;
};
```
*This function* allows us to feed a string into it that will be returned as a template element, which we can then populate and append to the page as needed. When used in conjunction with template literals, this becomes quite powerful.

```javascript
printHTML(`
    <div class='canvas__search-header'>
      <h2 class='city__search-header--title'>
        ${city["full_name"]}
      </h2>
      <p class='city__search-header--subtitle'>
        Mayor: ${city.mayor}
      </p>
    </div>
`).then((element) => canvas.appendChild(element));
```
*In this example*, the printHTML() function show above was used to create a ```<div>``` that will display on the page the name of the city searched and the name of its Mayor. The use of template literals lets us type the html elements directly into our code, making it easier to read and allowing us to append all elements as one, since the ```<h2>``` and ```<p>``` are nested within a ```<div>```, which is the template returned to us.
## 10. Toggle the classes applied to DOM nodes to change their CSS properties
When displaying the results of the user's search we created a header that shows the city's safety rating.
To bring this rating to life, we added a function that dictates the color of the rating for the user.

```javascript
    let safetySpan = document.querySelector('.canvas__city-safety-score');
    let safetySpanScore = Math.floor(score.score_out_of_10);
        
    if(safetySpanScore >= 0 && safetySpanScore <= 4){
      safetySpan.classList.add('canvas__city-safety-score--red');
    } else if(safetySpanScore >= 5 && safetySpanScore <= 7) {
      safetySpan.classList.add('canvas__city-safety-score--yellow');
      } else {
        safetySpan.classList.add('canvas__city-safety-score--green');
      }
```
This was achieved by applying a different modifier class to the relevant ```<span>``` element, dependent on the value contained within.

This was the final result:

![screenshot of safety rating display in Spot Check](/img/screenshot__safety-display--spotcheck.png)
## 11. Use consistent layout and spacing
Throughout Spot Check, css fundamentals are used to create a consistent layout and spacing in the page.

![screenshot of the layout of Spot Check as search results are displayed](/img/screenshot__layout--spotcheck.png)
*In this example*, three boxes display the results for a city search. They are coloured using variables in css where the colourscheme for the page has been saved and the spaces between them and between the elements inside each box is dictated using css fundamentals. For example, both boxes on the bottom have the class ```.stack-sm``` to ensure the information stored inside is shown in pleasing symmetry.
## 13. Debug client side JS in our web browser
The use of ```console.log()``` and other console actions is covered in learning point #14, but in order to investigate and solve more intricate issues we can insert break points in the browser.

![screenshot of the sources tool in google chrome with the code stopped at a break point](/img/screenshot__debugging--spotcheck.png)
*In this example*, we can see the code for Spot Check stopped where ```printCityDetails()``` was called. The code we can see here displayed has been timestamped to when the break point was reached. That means that, by hovering on the variables declared in our code, we can see the values those variables have received at that point.

In this case, we can see that the variables 'lat' and 'lon' have been assigned values from a previous ```.fetch()``` call, as intended. Here there is no bug, but if the information we expected were not being returned this would be a powerful way to explore the reasons for it and pinpoint at what point our logic was failing.
## 14. Use console.log() to help us debug our code
```javascript
try {
    callPolice(lat, lon).then(printPoliceResults);
} catch {
    console.error(`callPolice did not find a reference for this city. the following url was fed into the call ${url}`);
    window.alert('No data available for that city');
}
```
*In this example*, we incorporated debugging and feedback for the user into our error handling. Since the function relies on multiple fetch calls being made, which could all fail for different reasons, we alert the user in this ```catch``` that *'no data is available for that city'* but ```console.error()``` more detail on which call failed to help us review and debug any errors.
