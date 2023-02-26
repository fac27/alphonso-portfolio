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

## 9. Add and remove DOM nodes to change the content on the page

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

## 12. Follow a spacing guideline to give our app a consistent feel

## 13. Debug client side JS in our web browser

## 14. Use console.log() to help us debug our code
