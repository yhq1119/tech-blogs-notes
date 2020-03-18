### jQuery Tutorial

***jQuery is a framework of JavaScript***
Credit: https://api.jquery.com/
Credit: https://learn.jquery.com/

It makes things like ***HTML document traversal and manipulation***, 
event handling, animation, and Ajax much simpler with an easy-to-use API that works across a multitude of browsers.
 
#### DOM Traversal and Manipulation
Get the <button> element with the class 'continue' and change its HTML to 'Next Step...'
```JavaScript
$( "button.continue" ).html( "Next Step..." )
```

#### Event Handling
Show the #banner-message element that is hidden with display:none in its CSS when any button in #button-container is clicked.
```JavaScript
var hiddenBox = $( "#banner-message" );
$( "#button-container button" ).on( "click", function( event ) {
  hiddenBox.show();
});
```
#### Ajax
Call a local script on the server /api/getWeather with the query parameter zipcode=97201 and replace the element #weather-temp's html with the returned text.
```JavaScript
$.ajax({
  url: "/api/getWeather",
  data: {
    zipcode: 97201
  },
  success: function( result ) {
    $( "#weather-temp" ).html( "<strong>" + result + "</strong> degrees" );
  }
});
```
