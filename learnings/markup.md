## 1. Structure a site using semantic HTML to aid accessibility
The importance of deliberate use of semantic HTML elements was highlighted in the first project of the bootcamp. Changes that might not have otherwise affected the functionality of the page can greatly impact its accessibility and also the ease in reading for other developers or ourselves in the future.

```js
            <figure tabindex="0" class="gallery-grid--frame gallery-grid--frame__long">
                <img aria-describedby="fig1-caption" class="gallery-grid--image"
                    src="https://www.nakedlime.com/sites/default/media/image/RS_tube_man.png"
                    alt="classic red tube man model" />
                <figcaption class="gallery-grid--info stack-m">
                    <h3 class="center">Classic Red Tube Man</h3>
                    <p id="fig1-caption" class="center">
                        Everyones favourite arm-flailing tube man is the feature that will
                        turn your business parking lot into a classic.
                    </p>
                </figcaption>
            </figure>
```
*In this example*, using a ```<figure>``` element was a simple change from the initial inclination to use a ```<div>``` element but it creates a clearer understanding of the intended function of this element with its' semantics, specially once considered in conjunction with the nested ```<figcaption>``` element.

## 2. Ensure a web page is readable for screen readers
The code snippet below shows a particular case where a sensible set of aria attributes was needed for an element to be easily understood through a screen reader and possible to interact without the use of a mouse.

```js
     <p id="bio1-description" class="bio-box__description justified">
         After he had disrupted the marble counter-top industry, Alphonso
         became co-founder and main inflatable men engineer at
         ZanyMen.
         His great-great-grandfather also invented the left shoe in 1818.
     </p>
     <button 
        type="button" 
        class="bio-box__button"
        aria-label="read more about Alphonso"      //tells the screen reader what can be found by pressing the button
        aria-expanded="false"                      //tells the screen reader that the button will expand a new section
        aria-activedescendant="bio1-description"   //directs the user to the element revealed once the button is expanded
     >
        Read more
     </button>                    
```
*In this example*, the ```<p>``` element and the ```<button>``` are contained within the same element and pressing the ```<button>``` will display the text in the ```<p>``` on the screen.
The page was tested by navigating without a mouse and with the screen reader on. This quickly revealed that the purpose of the button was not clear to a user working with a screen reader - without the visual queues displayed on screen, users could not tell what information would be found by clicking the button.
To solve this, the ```aria-label```, ```aria-expanded``` and ```aria-activedescendant``` attributes were added. The comments displayed in the snipped above were added for clarity in this document.

## 3. Ensure our UI has sufficient colour contrast so that everyone can perceive it comfortably
At the very start of the project we agreed the page would have a minimal look, with only up three colours for its scheme, and set to work with a basic combination of two complementary colours and one more colour, analogous to the first.

Later, as we developed different sections of the page and started testing its' accessibility, we revisited the colour scheme and updated the values of the variables being used to guarantee good accessibility and a pleasing look to the page.

## 4. Use various tools to check that our website meets accessibility criteria
Besides running regular *lighthouse* reports, we frequently tested the usability of the page by navigating it with screen reader on and by using only the keyboard to interact with it.

![screenshot of the scoring from a lighthouse report on accessibility for the ZanyMen page](/img/screenshot__lighthouse.png)

## 5. Use CSS media queries to ensure our content is always presented effectively on screens of different sizes
*In this example*, media queries are used to define the behaviour of the page in larger screens, since the development of the page was done using a mobile-first approach.

```CSS
@media screen and (min-width: 520px) {

  nav ul a:hover {
    text-decoration: underline;
    color: var(--color-highlight);
  }
  
};
```
*This example* also relates to **learning point #6**

## 6. Demonstrate a mobile-first approach to building a website
Media queries in this project define the behaviour of the page when a screen reaches a set minimum size. In the example below, the behaviour of links in the navigation bar is set in order to let desktop users know they are clickable.

These links behave differently in screens of a smaller size (their original set behaviour) because they assume a mobile device is being used, on which the user will not be hovering a mouse over the links to recognise this behaviour.

## 7. Use CSS variables to apply repeated colours to HTML elements
Using variables to style our page allowed for easier and more effective adjustments to be made as the content changed in response to challenges.

```CSS
:root {
  --color-base: #f5f5f5;            /*basic 'off-white' colour*/
  --color-highlight: #036b8e;       /*complementary colour for highlights*/
  --color-text: #1d3557;            /*used for text when layed out in bright areas*/     
  --color-white: #fff;              /*used for text when layed out in dark areas*/
  --color-black: #0f0f1b;           /*slightly 'off-black' colour to avoid straining the eyes in very high contrast*/
}
```
*This example* also relates to **learning point 3**. Comments displayed were added for clarity in this document.

## 8. Use CSS Flexbox to style children in a single-direction layout (ie a row or a column)
Flexbox was used in different sections of the ZanyMen webpage project.
In this case, it was achieved by setting up CSS fundamentals which we then applied to elements as needed.

```CSS
.flex {
  display: flex;
}

.row {
  flex-direction: row;
}

.column {
  flex-direction: column;
}
```

## 9. Use CSS Grid to style children in two-direction layout

![grid template used for gallery display in ZanyMen webpage project](/img/screenshot__grid.png)
*In this example*, a grid was set up to serve as an image gallery. 
CSS fundamentals were set up so allow some elements to occupy two columns or two rows, instead of one as per their standard behaviour.
This created the layout displayed.

## 10. Ensure our Git commit history tells a coherent story
All commits were connected directly to issues raised within the project. 
A look through the history of commits, or a list of the closed issues, tells us a story of the challenges met while developing the page. 

![screenshot of a list of issues closed in the ZanyMen project](/img/screenshot__commit.png)

## 11. Use the appropriate input types in HTML forms for gathering different types of information

```HTML
            <form id="order-form" class="order__form flex column stack-m"
                aria-label="order form" tabindex="0">
                        
                    <label for="name__order">Name</label>
                    <input type="text" name="name__order" id="name__order"
                        placeholder="e.g James Kirk" required />
                            
                    <label for="email__order">Email</label>
                    <input type="email" name="email__order" id="email__order"
                        placeholder="e.g sulu@starfleet.com" required />

                    <label for="models">Choose a model:</label>
                    <select name="models" id="models">
                        <option value="" disabled selected hidden></option>
                        <option value="red-tube-man">Classic Red Tube Man</option>
                        <option value="red-tube-scarecrow">Red Tube Scarecrow</option>
                        <option value="yellow-destroyer">Yellow Destroyer Man</option>
                        <option value="orange-legged">Orange Legged Man</option>
                        <option value="tiny-desk-man">Tiny Desk Tube Man</option>
                        <option value="red-four-limbed">Red Four Limbed Red Man</option>
                        <option value="living-tube-man">Living Tube Man</option>
                    </select>

                    <label for="amount">Amount</label>
                    <input type="number" min="1" max="1000" name="amount" id="amount"
                        required />

                    <button type="reset">Reset</button>
                    <button type="submit">Submit</button>
            </form>
```
