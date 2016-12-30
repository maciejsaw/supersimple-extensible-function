# Supersimple Extensible Function

## Why?
Instead of having one big function, that gets bigger and bigger with time,
you can chunk it into separate function submodules that can be added separately.
* You can plug into existing functions and enable additional features, but keep the newly added code separately.
* This way you can organise your code per "user story" or per "feature"
* You can disable the "extension" when needed for debugging.

## Demo with annotations

## Quick start

1. Download the script and use it in your code

2. Declare the extensible function
```javascript
showSidebar = new extensibleFunction();
```

3. Set its core functionality
```javascript
showSidebar.setCoreFunctionality(function() {
  $('.sidebar').toggleClass('hidden');
});
```

4. Bind the function wherever you want
```javascript
$(document).on('click', '.sidebar-button', function() {
  //this will run the function including all extensions, even if they were added later
  showSidebar.run(); 
});
```

5. In future you can extend the function in different place
```javascript
showSidebar.extendBefore(function() {
  //do something before the core functionality
});
```

## List of methods
