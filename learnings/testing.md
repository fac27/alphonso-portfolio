# Project Goal
For this project we were tasked with building a functional To-do list using a TDD approach.<br>
[tUdo](https://github.com/fac27/tUdo) is a dynamic task tracker that facilitates simple navigation using clear keyboard commands to add, edit and delete tasks.
We built our own testing library while developing this page.

## 1. Check that passing a given input into our tests returns the expected output
```javascript
 test('typing "/delete" into an item will remove the associated task from storage', () => {
    let expected = 0;

    let testTask = document.querySelector('.test-task');
    testTask.value += ' /delete';
    testTask.dispatchEvent(pressEnter);

    let output = document.querySelectorAll('.test-task').length;

    isEqual(expected,output, 'deleted a test task');
};
```
*In this example*, the test targets a test item (created during a previous test) and adds the input '/delete' to it's text content before pressing 'Enter'.
We expect this to delete the item.

At this point, the test task should be the only task on the page, so we expect the length of the html element list captured at the end to be 0, which is the fixed value assigned to the variable 'expected'.

A separate test tracks whether the number of items shown on the page matches the number of items in storage, but this test is only checking whether an item is removed from the page when we type '/delete'.

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
![screenshot of a successful test of the function newItem()](/img/screenshot__pass-test--tUdo.png)
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
When a new task is created or edited by the user, tUdo will update the stored task list and render its updated version onto the page.
Specific event listeners are added to the newly rendered items to allow the user to continue interacting with their task list.

```javascript
function listenForKeyStrokes() {
 let tasksOnPage = Array.from(
    document.querySelectorAll(".item__description")
  ).splice(1);
        
 let typeToDelete = new RegExp(/(\/delete)$/);
 let typeToComplete = new RegExp(/(\/done)$/);
 let typeToUntick = new RegExp(/(\/pending)$/);
        
 tasksOnPage.forEach((task) => {
  task.addEventListener("keyup", (e) => {
   if (e.key !== "Enter") return;
   if (typeToDelete.test(task.value)) return deleteItem(task);
   if (typeToComplete.test(task.value)) return tickItem(task);
   if (typeToUntick.test(task.value)) return untickItem(task);
   editItem(task);
  });
 });
};
```
*In this example*, the function ```listenForKeyStrokes()``` iterates through all tasks displayed on the page and adds an event listener to allow the user to enter new changes with different text entries.
This is function is then called when the list is rendered onto the page.

## 6. Use scope to control what variables are accessible inside functions and blocks

## 7. Use CSS grid to create complex layouts

## 8. Use CSS grid to make layouts that adapt to the viewport size
