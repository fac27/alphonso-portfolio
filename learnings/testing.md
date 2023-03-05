## 1. Check that passing a given input into our tests returns the expected output

## 2. Write tests to mimic the behaviour of a user performing different actions
```javascript
test('newItem() renders a new task element on the page', () => {
    newItem();
    let expected = 2; //the new element + an empty one from initialising the page
    let output = document.querySelectorAll('.item__description').length;

    isEqual(expected, output);
    renderTaskList();
});
```
*In this example*, the test shown renders onto the page a new Task List template.
On startup, the page should display the entire task list stored locally and an extra task template element to prompt the user to enter new tasks.
The test is deployed when the storage is empty, so we expect 2 items to be displayed at the end. The item created during the test, and the empty template.
At the end of the test, we render the stored task list again, clearing the output of this test once we have recorded it's result.

This is the message logged at the end of a successful task:
![screenshot of a successful test of the function newItem()](/img/screenshot__successful-test--tUdo.png)
## 3. Write testable, modular functions

## 4. Write functions that add, remove or modify DOM nodes
The layout of the to-do list is defined by the users' input.
To achieve this, our code continuously listens for user behaviour that tells it whether it should:
 - add a new list item, 
 - delete an item, or,
 - change its' status or description.

```javascript
function renderTaskList() {
  canvas.innerHTML = "";
  newItem();
  
  for (let i = 0; i < currentTaskList.length; i++) {
    let { description, completed: done } = currentTaskList[i];

    newItem();                                                                  // this function returns a template element to show the task

    
    let taskDescription = allTaskDescriptions[allTaskDescriptions.length - 1]; //the latest template displayed on the page is populated with
    taskDescription.value = description;                                       //information from the current task object   

    let taskDone = allTasksStatus[allTasksStatus.length - 1];
    taskDone.checked = done;

    let newestTask = allTaskDescriptions[0];                                    //the first template on the page, which was left empty,
    newestTask.focus();                                                         //is focused to prompt new user input
  }                                                                             
}
```
*In this example*, the function renderTaskList clears the DOM and then iterates through all task objects in the localStorage so it can render a new element onto the page and populate it with the object's information.
Comments displayed in the code were added for detail in this document.

## 5. Apply event listeners to HTML form elements

## 6. Use scope to control what variables are accessible inside functions and blocks

## 7. Use CSS grid to create complex layouts

## 8. Use CSS grid to make layouts that adapt to the viewport size
