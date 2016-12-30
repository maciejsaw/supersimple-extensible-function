# Supersimple Extensible Function

## Why?
Instead of having one big function, that gets bigger and bigger with time,
you can chunk it into separate function submodules that can be added separately.
* You can plug into existing functions and enable additional features, but keep the newly added code separately.
* This way you can organise your code per "user story" or per "feature"
* You can disable the "extension" when needed for debugging.

## Demo with annotations
Take a look at this simple scenario when we add a sidebar to a website. This will show you what can happen in several days when you work on your code, and how the extensibleFunction can help you to organise the code
* DAY 1: First, we only add a basic functionality, which is showing and hiding the sidebar 
* DAY 2: Our product onwer asked to add a different feature: popup
* DAY 3: We found out a bug that popup overlaps the menu - We decided that before the menu is opened, all the popups should be hidden
* DAY 4: Our product owner asked to add analytics tracking

[View demo on Codepen](http://codepen.io/maciejsawicki/pen/VmogqW)

Without the extensibleFunction, on DAY 3 you would scatter your code accross different files. After some time a simple function to open a sidebar will become bloated and harder to maintain.  

With extensibleFunction, you can keep the fix for the popups in the same file/folder that is responsible for popups. Consider organising your folders per "user story", for example
* ShowingSidebar
* ShowingPopup
* SidebarAnalytics

## Quick start

1) Download the script and use it in your code

2) Declare the extensible function
```javascript
showSidebar = new extensibleFunction();
```

3) Set its core functionality
```javascript
showSidebar.setCoreFunctionality(function() {
  $('.sidebar').toggleClass('hidden');
});
```

4) Bind the function wherever you want
```javascript
$(document).on('click', '.sidebar-button', function() {
  //this will run the function including all extensions, even if they were added later
  showSidebar.run(); 
});
```

5) In future you can extend the function in different place
```javascript
showSidebar.extendBefore(function() {
  //do something before the core functionality
});
```

## List of methods
Each extensible function has has 5 phases:
- at the beginning
- before core functionality
- core functionality
- after core functionality
- at the end

### Setting up the core functionality
* setCoreFunctionality
Example:


### Running the extensible function
* run

Example:
```javascript
showSidebar.run()
```

### Extending function
* extendAtTheBeginning
* extendBefore
* extendCore
* extendAfter
* extendAtTheEnd

## Need a variable that will be accessible for all the "extensions"?
You can store it in the function object under ```showSidebar.exportedVars```

Just add your var name
```javascript
showSidebar.exportedVars.yourVarName = "Your Var value" 
```

Then this value is accessible in all other functions/extensions
```javascript
console.log(showSidebar.exportedVars.yourVarName);
```

## Disadvantages:
* Security: with the basic simple approach here, the functions are global, though it might be possible to limit their scope by namespacing. Anyway, this is probably not the best security.

## Also see
* For more advanced apps you probably want to see  [JS Module patter](https://toddmotto.com/mastering-the-module-pattern/)


