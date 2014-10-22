---
layout: post
title: "Wiring up a back-end to your AngularJS app using Firebase"
description: "Simple CRUD app using AngularJS + Firebase with the help of Yeoman"
date: 2014-06-21 09:25:00 +0800
comments: true
categories: [angularjs, firebase, yeoman]
---
<img src="/images/angularfirebase/angularjs.jpg" style="width:100%" />
<img src="/images/angularfirebase/firebase_logo.png" style="width:100%" />

In this post, I will teach you how to create a simple CRUD app using AngularJS and Firebase, and of course, with the help of Yeoman. Let's get started!

### Generating our AngularJS app using Yeoman
<img src="/images/angularfirebase/yeoman_toolset_k50sok.png" style="width: 100%;" />
[Yeoman](http://yeoman.io) is a scaffolding tool. What it does is it kickstart your project, providing coding best practices and tools to help you out on the project. Yeoman provides different generators. So in our case, we will be using the AngularJS generator. Let's now start generating our app by making a folder then summon Yeoman and ask to generate our AngularJS app in it:

{% codeblock %}
mkdir angularfirebase && cd angularfirebase
yo angular
{% endcodeblock %}

When you ask Yeoman to generate your app for you, it will also ask you some questions like, if you need Twitter Bootstrap ready installed, and other things. It will be up to you on what do you need.

<img src="/images/angularfirebase/yo_angular.png" style="width: 100%" />

Once you have already answered Yeoman's question, it will now proceed on generating the files needed, getting all the dependencies through Bower, and conducting a pre-build test using Grunt for your app.

<img src="/images/angularfirebase/yo_generate.png" style="width: 100%" />

Once Yeoman is done, you can now check the project through your browser by running `grunt serve` on your command line. This will automatically open the app page for you and the good thing with this is, once you have edited a file within your project, Grunt will automatically refresh the page for you. Which means, you don't need to hit the refresh button or pressing `F5` or `Ctrl + R` every time you make changes.

<img src="/images/angularfirebase/hello_yo.png" style="width: 100%" />

### Installing Firebase to our app
To install Firebase to our app, we will ask Bower to install for us by running `bower install --save angularfire` on our command line. What this does is it will download the `firebase.js`, `firebase-simple-login.js`, and `angularfire.js`. Once this done, we will now include the javascript files we have to our `index.html`.

{% codeblock app/index.html %}
<!-- bower:js -->
---

<script src="bower_components/firebase/firebase.js"></script>
<script src="bower_components/angularfire/dist/angularfire.min.js"></script>

---
<!-- endbower-->
{% endcodeblock %}

After this, we can now add Firebase to our AngularJS modules

{% codeblock app/scripts/app.js %}
---

angular
  .module('angularfirebaseApp', [
  ---
  
  'firebase'
  
  ---
  ])
  .value('fbURL', 'https://angularifictest.firebaseio.com/')
  .factory('Person', function (fbURL, $firebase) {
    return $firebase(new Firebase(fbURL)).$asArray();
  })

---
{% endcodeblock %}

### Adding data to Firebase

Of course, before you can save data to Firebase, you must first create an account and your app there.

<img src="/images/angularfirebase/firebase.png" style="width: 100%" />

Once you have your Firebase app, it will have its own URL which we will use on development. In my case, I have created an app with a URL  `angularifictest.firebaseio.com`.

Let's now proceed on developing of creating a data and saving it to Firebase. By default, we have already a controller named as `MainCtrl` on the `app/scripts/controllers/main.js` file. We'll just use that to contain our function for saving data to Firebase.

{% codeblock /app/scripts/controllers/main.js %}
---

angular.module('angularfirebaseApp')
  .controller('MainCtrl', function ($scope, Person) {
    $scope.add = function() {
     var save = Person.$add({
      firstName: $scope.firstName,
      lastName: $scope.lastName
     });

     $scope.firstName = '';
     $scope.lastName = '';

     if(save) {
      alert('saved successfully');
     } else {
      alert('something went wrong');
     }
    });

---
{% endcodeblock %}

What we've done here is, we created a function called `add()` function which then passed to the `$scope` object so we can use it on our view. Inside the `add()` function, we used the `$add` function from  the Firebase object  we created on the `Person` factory to save the data to our Firebase. Inside the `$add` function, it accepts an array of data which will be saved to our Firebase.

And let's edit `/app/views/main.html` to create our form for creating data.

{% codeblock /app/views/main.html  %}
<form ng-submit="add()">
  <div class="form-group">
    <label>First Name:</label>
    <input type="text" ng-model="firstName" class="form-control">
  </div>
  <div class="form-group">
    <label>Last Name:</label>
    <input type="text" ng-model="lastName" class="form-conrol">
  </div>
  <div class="form-group">
    <input type="submit" value="Save" class="btn btn-primary">
  </div>
</form>
{% endcodeblock %}

On our form, we've added the `add()` function we have created which will be triggered once the form is submitted with the help of the `ng-submit` directive.

Once you're done with this, you'll have a form like this:

<img src="/images/angularfirebase/create_form.png" style="width: 100%" />

And if you tried to submit a data, you can check on you Firebase Graphical Debugger if the data is saved. 

<img src="/images/angularfirebase/firebasedash.png" style="width: 100%" />

### Listing the Data

Listing the data from Firebase is very simple. Just add this line of code on our `MainCtrl` in `app/scipts/controllers/main.js` file:

{% codeblock  app/scripts/controllers/main.js %}
$scope.person = Person;
{% endcodeblock %}

And on our `app/views/main.html`, let's add this code:

{% codeblock app/views/main.html %}
<table class="table">
  <thead>
    <th>First Name</th>
    <th>Last Name</th>
    <th>&nbsp;</th>
    <th>&nbsp;</th>
  </thead>
  <tbody>
    <tr ng-repeat="(id, name) in pesron">
      <td>{{ name.firstName }}</td>
      <td>{{name.lastName }}</td>
      <td>
        <a href="#">Edit</a>
      </t>
      <td>
        <a href="#">Remove</a>
      </td>
    </tr>
  </tbody>
</table>
{% endcodeblock %}
<small>Note: Inside the first `<td>` tag, add &#123;&#123; name.firstName &#125;&#125; inside. And on the second `<td>` tag, add &#123;&#123; name.lastName &#125;&#125; inside. It's not just showing on the codeblock plugin :)</small>

In here, we just used the `ng-repeat` directive to loop through the data from Firebase and display them using AngularJS's data binding. You should be seeing something like this:

<img src="/images/angularfirebase/firebaselist.png" style="width: 100%" />

### Editing a Data
On editing a data, we will create a different controller. So, we will edit the `app/scripts/controllers/main.js` file and add this code

{% codeblock app/scripts/controllers/main.js %}
  .controller('EditCtrl', function ($scope, $location, $routeParams, $firebase, fbURL) {
    var personURL = new Firebase(fbURL + $routeParams.id);
    $scope.person = $firebase(personURL).$asObject();

    $scope.edit = function() {
      $scope.person.$save();
      $location.path('/');
    }
  });
{% endcodeblock %}

In here, we declared a variable containing the Firebase object using the URL of the person we will edit. Then we made a function called `edit()` which saves the changes from the form we will create.

We don't have yet the view file for our edit page so we will create one. 

{% codeblock app/views/edit.html %}
<form ng-controller="EditCtrl" ng-submit="edit()">
  <div class="form-group">
    <label>First Name:</label>
    <input type="text" ng-model="person.firstName" class="form-control">
  </div>
  <div class="form-group">
    <label>Last Name:</label>
    <input type="text" ng-model="person.lastName" class="form-control">
  </div>
  <div class="form-group">
    <input type="submit" value="Save" class="btn btn-primary">
  </div>
</form>
{% endcodeblock %}

On our view file, it's almost the same with the form we created for creating data except that we only changed the function called by the `ng-submit` directive and the controller we're using. Next, we will add the route for our `EditCtrl`

{% codeblock app/scripts/app.js %}
---
  .config(function ($routeProvider) {
    $routeProvider
      ---
      .when('/edit/:id', {
        templateUrl: 'views/edit.html',
        controller: 'EditCtrl'
      })
      ---
  });
---
{% endcodeblock %}

And now, we will add the link of our Edit page from the Edit link on our list of data

{% codeblock app/views/main.html %}
---
  <a href="#/edit/{{ name.$id }}">Edit</a>
---
{% endcodeblock %}
<small>Note: The `href` value should be <i>#/edit/&#123;&#123; name.$id &#125;&#125;</i></small>

### Deleting Data
Deleting of data is just simple too, we'll just add this line to our `MainCtrl` in `app/scripts/controllers/main.js` file:

{% codeblock app/scripts/controllers/main.js %}
  $scope.remove = function (id) {
    Person.$remove(id);
  }
{% endcodeblock %}

Here, we just created a function called `remove()` which accepts an ID parameter and used the `$remove` function to delete that specific ID from our Firebase. We can now use this function on our view by editing the Remove link in our `app/views/main.html' file.

{% codeblock app/views/main.html %}
  <a href="#" ng-click="remove(id)">Remove</a>
{% endcodeblock %}

So, if you'll click the Remove link beside the data, it should delete that specific data.

### Conclusion
I like how AngularJS works well with Firebase. There's more than just creating a CRUD app with AngularJS and Firebase. And also, maximize the real-timeness of Firebase.

If you wish to see a demo, just click [here](http://junereycasuga.github.io/angularfirebase/). You can also see the source code on [Github](https://github.com/junereycasuga/angularfirebase).

Cheerio!
