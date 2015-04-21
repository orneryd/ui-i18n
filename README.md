# ui-i18n
Lightweight and fast localization library for angular.js

```
bower install angular-ui-i18n --save
```
Then include the angular-ui-i18n.min.js file in your project

# Description
due to the verbose nature of a couple of the i18n libraries out there and working on ng-grid 3.0 and wanting a lightweight version of i18n support I created a module that seems to be fairly lightweight and performant.

you can compare the performance of thousands of bindings against angular-translate here:

[angular-translate 11K rows of bindings](http://jsfiddle.net/eUGWJ/70/)

[ui-i18n 14K rows of bindings](http://jsfiddle.net/mc66U/5/)

# setup:
```javascript
//inject via the provider in a config block or service in anything else.
.config(function(i18nServiceProvider, i18nService /*this is the same as i18nServiceProvider.api*/) {
  i18nServiceProvider.api.add(["en", "en-us"],{
    groupPanel: {
      otherText: 'some other group property text'
    },
    anotherExample: "I speak A Different Language"
  });
  i18nServiceProvider.api.add("de",{
    groupPanel:{
        description:'Ziehen Sie eine Spaltenüberschrift hierhin um nach dieser Spalte zu gruppieren.'
    },
    example: "I speak Something Else"
  });
}

```
NOTE: you can lazy load strings and it will extend the current set of strings with the new ones

```javascript
var uiI18n = angular.module('ui.i18n');

//calling this later:
uiI18n.add(["en", "en-us"],{
    groupPanel: {
        otherText: 'some other group property text'
    },
    anotherExample: "I speak A Different Language"
});
// results in 
"en"/"en-us": {
    groupPanel:{
        otherText: 'some other group property text',
        description:'Drag a column header here and drop it to group by that column.'
    },
    example: "I speak English",
    anotherExample: "I speak A Different Language"
}
```
You can set the language via directive 
```html
<!-- directly-->
<body ui-i18n="en">
<!-- or via bindable $scope property-->
<body ui-i18n="bindableProperty">
```
Or, through a module method:
```javascript
angular.module('ui.i18n').set("en-us");
```

Usage:
You can use it as an attribute, element, or filter, see all the different possibilities below 
```html
 <h3>Using attribute:</h3>
    <p ui-t="groupPanel.description"></p>
    
    <p ui-t="example"></p>
    
    <p ui-t>groupPanel.description</p>
    
    <p ui-t>example</p>
    
    <p ui-t="invalid.translation.path"></p>
    
    <p ui-t>invalid.path</p>
    
    <p ui-t>invalid.translation.again</p>
    
    
    <h3>Using element:</h3>
    <ui-t>example</ui-t>
    <br/>
    <ui-translate>groupPanel.description</ui-translate>
    <br/>
    <ui-t>invalid.path</ui-t>
    <br/>
    <ui-t>invalid.translation.again</ui-t>
    
    <h3>Using Translate Filters:</h3>

    <p>{{"groupPanel.description" | t}}</p>
    
    <p>{{"example" | t}}</p>
    <p>{{"invalid.path" | t}}</p>
    
    <p>{{"invalid.translation.again" | translate}}</p>
```

Bonus:
{{}} expressions work in the directive syntax also.
Caveat, this does impact performance a little bit.. even using this syntax its still about 2-3x faster than angular-translate with a similar amount of rows but you should know.
```html
 <p ui-t="groupPanel.{{desc}}"></p>
```

it will alert you to missing translations with "[MISSING]: invalid.path" in place of where the translations should be.

All feedback is greatly appreciated.
