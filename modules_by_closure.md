# Module by closure pattern

I've used this pattern introduce much-needed encapusulation and modularity into larger scripts and applications in the Google Apps Script environment, which is inherently non-modular and does not have suport for anything like ES modules or CommonJS modules. Fun fact the following pattern is acutally how CommonJS works under the hood. 

### A working example of the module by closure pattern. 

Copy and paste this boilerplate to play with things and see how they work. Each key concept is illustrated with at least one example, demonstrated through console logs. 
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
## Source

"Functional Programming in JavaScript" by Luis Attencio pointed to a [this post](http://www.adequatelygood.com/JavaScript-Module-Pattern-In-Depth.html) from Ben Cherry's blog,  "Adequately Good: Decent Programming Advice".
