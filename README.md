#### Module by closure pattern
An example of the module by closure pattern. 
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
