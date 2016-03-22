## sandjs : fast, light and simple JavaScript module manager
-----------------------------------------------------------
sandjs is a simple library allowing you to manage module in your app.
It is a lot like requirejs except it weighs less than 2kb minified (instead of 16kb for requirejs).
It also allows you to declare and require groups of modules.

### When to use?
You should use a module manager if you start writing serious apps. It will avoid variables conflicts problems and help splitting the different parts of your code. 

### Installing sand
Just include sand.js somewhere in your < body > and you are ready to go!

```html
<script src="sand.min.js"></script>
```

### Usage
#### Declaring a module
We can declare a module in a group. Groups are implicitly declared when your module name contains slashes.
```javascript
sand.define('SouthPark/characters', function() {
  
  return ['Randy Marsh', 'Eric Cartman', 'Kenny McKormick'];

});
```
This example declares a module 'SouthPark/characters', belonging to the group 'SouthPark'. I call inner name of the module the part after the last '/', here 'characters'.

#### Declaring a module requiring another module
```javascript
sand.define('SouthPark/printCharacters', [
  'SouthPark/characters'
], function(requires) {
  
  return function() {
    for (var i = requires.characters.length; i--; ) console.log(requires.characters[i]);
  }
});
```
A required module is accessible within the requiring module by using the first argument of the declaring function (here requires).
The required module is accessible from a key of requires, equal to the inner name of the module (here characters).
#### Using a module
```javascript
sand.require('SouthPark/printCharacters', function(r) {
  r.printCharacters();
});
```
This will log 'Kenny McKormick', 'Eric Cartman', 'Randy Marsh'.

#### Groups of module
With the previous examples, we have implicitly defined a group of module named 'SouthPark'.
We can require a whole group using the '*' character.
```javascript
sand.require('SouthPark/*', function(r) {
  r.SouthPark.printCharacters();
  console.log(r.SouthPark.characters.length);
});
```
This will log 'Kenny McKormick', 'Eric Cartman', 'Randy Marsh', then '3'.

### About

####  Who uses sandjs ?
* [wallDraft](http://walldraft.com) (collaborative real-time whiteboard)

#### Authors 
* [Sam Ton That](https://github.com/KspR)
* [Cyril Agosta](https://github.com/cagosta)
* [Pierre Colle](https://github.com/piercus)
