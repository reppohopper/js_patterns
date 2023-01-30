# Module by closure pattern

## Origin

I originally learned about this pattern from, 
"Functional Programming in JavaScript" by Luis Attencio (maybe this product listing works?)[https://www.amazon.com/gp/product/1617292826/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1], which pointed to a (brilliant post)[http://www.adequatelygood.com/JavaScript-Module-Pattern-In-Depth.html] on the subject by Ben Cherry in a blog called "Adequately Good: Decent Programming Advice". 

The post is from 2010, but the patterns and structures demonstrated there, even in their pre-ES6 syntax, retain their relevance. The patterns is no less powerful now, as we can implement it in ES6+ and carry over their incredible ability to create modules with private state on the fly, even in environments like Google Apps Script which are particularly hostile to code modularity. 


## Examples

### A working example of the module by closure pattern. 
```
const my_module = (function my_module_loader () {
   let exports = {}; // The one object to be returned. 
   let sth = 123; // Private, encapsulated data! 
   let print_count = 1;
   
   // Some private function. 
   const complaining_log = function (text) {
       console.log(text);
       console.log(`Aww, I've had to print ${print_count} things now...`);
       print_count += 1;
   }   
   
   // Some exported function with ongoing access to the 
   // private variables and private functions. 
   exports.print_something = function (text) { 
       complaining_log (text); 
   }
   return exports; // Expose only these exports.
}()); // invoke immediately, to evaluate to the object 'my_module'

// Exported functions have ongoing access to the modules 
// private variables and private functions. 
my_module.print_something("hello");
// prints --> "hello", "Aww, I've had to print 1 things now..."
my_module.print_something("oh, sorry.");
// prints --> "oh sorry.", "Aww, I've had to print 2 things now..."

// These private variables and functions cannot otherwise be accessed. 
my_module.complaining_log("complain for me!");  // --> Error. 
my_modele.print_count // --> undefined


```
