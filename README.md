# jq-repeat

Author William Mantly Jr <wmantly@gmail.com>


A simple, yet highly customizable plugin to handle all of you're client-side repetitive DOM needs. Simple, quick and powerful templating. It is modeled after ng-repeat and shares some basic syntax, but is not a clone.

- To do list [demo](http://jsfiddle.net/wmantly/nLj6nr4q/)
- Reddit JSON feed [demo](http://jsfiddle.net/wmantly/sge3zr28/)

# Requirements

- **jq-repeat requires [jQuery](http://jquery.com/) 1.x/2.x/3.x and [Mustache](https://github.com/janl/mustache.js) 1.x/2.x/3.x/4.x to run**.

## Examples
[examples/](https://github.com/wmantly/jq-repeat/tree/reworked-dev/example)

## Template

To set up a jq-repeat template, write any element tag you wish to repeat once where you want the repeating to start, this will serve as the template and starting point.

Simply add a `jq-repeat` attribute with a unique value for the reference name for that template, in this case `toDo`.

```html
<ul>
	<li jq-repeat="toDo"><span class="item">{{ item }}</span> {{{ done }}}</li>
</ul>
```

Just like mustache, to add variables use double brackets with the name inside.

## Insert

Now that you have a template set up, let's populate the template use $.scope.toDo.push()

```javaScript
$.scope.toDo.push( { item: 'Get milk', done: 'Yes' } )
```

You can add any number of objects as arguments you wish and each will create a new element from the template. Values must be supplied as objects with keys corresponding to the variable names used in the template.

```javaScript
$.scope.toDo.push({
    item: 'Collect underwear',
    done: 'Yes'
}, {
    item: '?',
    done: 'No'
}, {
    item: 'Profit',
    done: 'No'
});
```

## Methods

- `$.scope.toDo.push([object])`
  - **Description**: The method will just insert object with the relevent key and value pair as used in your template.
  - **Parameter**:
    - **Type: object**: Object with key and value in the HTML template.
- `$.scope.toDo.pop()`
  - **Description**: The method will remove and return the last element in the repeat array.
- `$.scope.toDo.reverse()`
  - **Description**: The method will reverse the repeat array and append the array.
- `$.scope.toDo.remove([key] || [index Id])`
  - **Description**: The method would use either the key value of the pair to remove or use the index id to remove an array item.
  - **Parameters**:
    - **key**: The key of the array you wish to remove.
    - **Index Id**: The array Id you wish to remove.
- `$.scope.toDo.shift()`
  - **Description**: The method works the same as regular arrays.
- `$.scope.toDo.loop()`
  - **Description**: The method takes the 0th item of an array and adds it as the last item of the array.
- `$.scope.toDo.loopUp()`
  - **Description**: The method does the opposite of loop(). 
- `$.scope.toDo.indexOf()`
  - **Description**:  The method will return the array index number of the matching element or array id. Mostly used for internals usage.
    - **Parameters**:
    - **key**: The key of the array you wish to get the id of.
    - **Value**: The value of the key pair you wish to get the id of.
- `$.scope.toDo.update([key] || [index Id] , [Object])`
  - **Description**: The method would use either the key value of the pair to update or use the index id to update the object key value pair.
  - **Parameters**:
    - **key**: The key of the array you wish to update.
    - **Index Id**: The array Id you wish to update.
    - **Object**: The object you wish to update the array with.

## Credits

- Written by [William Mantly](https://github.com/wmantly)
- Big thanks to [Derek Hu](https://github.com/derek-dchu) for creating NPM and bower package, and other general house keeping.
- Also, thanks to [Raja Kapur](https://github.com/aonic) for advice and guidance.




- `$.scope.toDo.splice(index [,howMany] [,ToAdd])` functions exactly as a regular array with notable difference. If the index propriety is set a string can be passed as the value of the index.
- **index** _Type: Number or String_
  Index of element you wish to manipulate. If the .index property is set, you may pass a string to match to the index array.
- **howMany** _Type: Number_
  Number of repeat objects that will be removed. If there are non to be removed, it is not required to use this argument.
- **update** _Type: Array_
  This is the array of repeat objects to add. If there are none to this is not required.
- **returns** _Type: Array_
  This function will return an array of deleted elements.

- `$.scope.toDo.__put` is the function that will run when a element is being inserted. This must be a function and must include this.show(), or some other way of un-hiding 'this'.
- `$.scope.toDo.__take` is the function that will run when an element is being removed. This must be a function and include this.remove() or some other way to remove 'this'.
