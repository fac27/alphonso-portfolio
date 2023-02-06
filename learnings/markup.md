## 1. Structure a site using semantic HTML to aid accessibility
The importance of deliberate use of semantic HTML elements was highlighted in the first project of the bootcamp. Changes that might not have otherwise affected the functionality of the page can greatly impact its accessibility and also the ease in reading for other developers or ourselves in the future.

```js
<div tabindex="0" aria-labelledby="gallery-heading" id="gallery-grid"
            class="grid">
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
                      aria-label="read more about Alphonso" 
                      aria-expanded="false"
                      aria-activedescendant="bio1-description"
                    >
                        Read more
                    </button>
```
*In this example*, the ```<p>``` element and the ```<button>``` are contained within the same element and pressing the ```<button>``` will display the text in the ```<p>``` on the screen. The page was tested by navigating without a mouse and with the screen reader on. This quickly revealed that the purpose of the button was not clear to a user working with a screen reader - without the visual queues displayed on screen, users could not tell what information would be found by clicking the button.

## 3. Ensure our UI has sufficient colour contrast so that everyone can perceive it comfortably

## 4. Use various tools to check that our website meets accessibility criteria

## 5. Use CSS media queries to ensure our content is always presented effectively on screens of different sizes

## 6. Demonstrate a mobile-first approach to building a website

## 7. Use CSS variables to apply repeated colours to HTML elements

## 8. Use CSS Flexbox to style children in a single-direction layout (ie a row or a column)

## 9. Use CSS Grid to style children in two-direction layout

## 10. Ensure our Git commit history tells a coherent story

## 11. Use the appropriate input types in HTML forms for gathering different types of information
