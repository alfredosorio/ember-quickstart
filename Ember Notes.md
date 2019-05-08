# Installing Ember
You can install Ember using npm
```
npm install -g ember-cli
```

# Creating a new application
You can use the `ember new` command to create a new application:
```
ember new <appName>
```
This will create a new directory based on your appName and set up a new Ember application inside of it.
Out of the box, your application will include:
- A development server.
- Template compilation.
- JavaScript and CSS minification.
- ES2015 features via Babel.

# Starting the development server
`cd` into the application directory `ember-quickstart` and start the development server by typing:
```
ember serve
```
You should see the following output:
```
Build successful (14382ms) - Serving on http://localhost:4200
```

# Defining a Route
Ember comes with *generators* that automate the boilerplate code for common tasks. This is similar to scaffolding in Rails.
To generate a route, type:
```
ember generate route scientists
```

Output:
```bash
  create app\routes\scientists.js
  create app\templates\scientists.hbs
updating router
  add route scientists
installing route-test
  create tests\unit\routes\scientists-test.js
```

This will have created:
1. A template to be displayed in the /scientists address. Located in `app/templates/scientists.hbs`
2. A `Route` object that fetches the model used by that template.
3. An entry in the application/s router (located in `app/router.js`)
4. A **unit test** for this route.

## Specifying a model for the route

We will now render some data.
We do this by *specifying a model* for that route by editing `app/routes/scientists.js`.

```javascript
// scientists.js

import Route from "@ember/routing/route";

export default Route.extend({
  model() {
    return ["Marie Curie", "Mae Jemison", "Albert Hofmann"];
  }
});
```

In a route's `model()` method, you return whatever data you want to make available to the template.
If you need to fetch data synchronously, the `model()` method supports any library that uses JavaScript Promises.

## Rendering the data

We will now tell Ember to turn that array of strings into HTML:
```javascript
// scientists.hbs

<h2>List of Scientists</h2>

<ul>
  {{#each this.model as |scientist|}}
  <li>{{scientist}}</li>
  {{/each}}
</ul>
```

The `each` helper loops over each item in the array we provided from the `model()` hook.
We then print it inside an `<li>` element.

# Creating a UI Component
Ember makes it easy to refactor your templates into reusable components.

We will create a `people-list` component that we can use in multiple places to show a list of people.

Use the generator `component` to create a new component:
```
ember generate component people-list
```

We copy and paste the `scientists` template into the `people-list` component's template and edit it to look as follows:

```javascript
// people-list.hbs

<h2>{{this.title}}</h2>>

<ul>
  {{#each this.people as |person|}}
  <li>{{person}}</li>
  {{/each}}
</ul>
```

- We have changed the title from a hard-coded string of "List of Scientists" to a dynamic property `{{title}}`.
- We have also renamed `scientist` to a more generic `person`, decreasing the coupling of our component to where it's used.

Revisit the `scientists` template and replace the old code to the new version that uses the `person` component:

```javascript
// scientists.hbs

<PeopleList @title="List of Scientists" @people={{this.model}} />
```

- We have now removed most of the code.
- We use the `title` and `people` attributes to pass the data through from the Scientist template to the people-list component.

The UI should now look identical. The only difference now is that we've componentized our lit into a version that's more reusable and more maintainable.

# Uninstalling Ember add-ons
To uninstall add-ons installed with `ember install "packageName"` type:
```
npm uninstall "packageName"
```

# Removing generated objects
To remove objects generated with `ember generate` type:
```
ember destroy <type> <name>
```

# Sources
- [Ember Guide](https://guides.emberjs.com)
- [Uninstalling Ember add-ons](https://emberigniter.com/uninstall-remove-ember-add-on/)
