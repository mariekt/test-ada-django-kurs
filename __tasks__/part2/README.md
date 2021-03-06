# Part 2: Implementing the detail view

## Introduction

In this part, you will get to know the detail page, where one single recipe is displayed. This page is called `detail.html`, and you can access it by typing _/cookbook/\<id>_ in the address bar.

## Task 1: Retrieve recipe from database

Open `views.py` in the code editor. As you can see, the view `detail` renders an HTML template called `detail.html`, and it takes `recipe_id` as a parameter. This recipe id is retrieved from the URL, and is the value after _/cookbook/_. `recipe_id` is a unique identifier for a recipe, and we are going to use this value to retrieve the correct recipe.

Retrieving an objects based on its identifier, also called _primary key_ or _pk_, can be achieved by using the following expression:

```python
item = [MODEL].objects.get(pk=[ID])
```

This command will retrieve the object that matches the given id. However, if we try a primary key that does not exist, the server will send a HTTP response that the item could not be found, and our application will crash. Fortunately, Django has a clever way of handling such an error, where the user receives a warning without having the application crash. This function is called `get_object_or_404`, and handles both the retrieval of the object and error handling if the object does not exist. Here is an example of how it can be used:

```python
item = get_object_or_404([MODEL], pk=[ID])
```

Copy this function to your detail view, import `get_object_or_404` from `django.shortcuts` and switch out `[MODEL]` and `[ID]` with the correct model and identifier. Pass the item on as context to the render function, like we did in the previous part. Once you have completed this, go on to the next task where we will use this retrieved recipe and render it in our application.

Are you uncertain on how to implement the 404-handling, or are you experiencing any issues? Ask an Itera employee for help or check out the `__solutions__` folder.

## Task 2: Display retrieved object in detail.html

In the previous task you passed the recipe on to the template as context, and now it's time to render this object in our template. This is very similar to task 2 in the previous part, so here is a short recap of how you could render your recipe:

```html
<p>{{ item }}</p>
```

Remember that you can also render specific attributes, for instance `title`, with the following syntax:

```python
item.title
```

Open `cookbook/templates/cookbook/detail.html`, and render the recipe as described above. We recommend rendering the attributes `title`, `description` and `ingredients`. Once you have rendered some attributes, take a look at _cookbook/1_. Did the recipe information appear in your application? If yes, great! If no, take a look at the `__solutions__` folder and see if there is something missing.

Once the rendering is in order, you can explore different types of HTML elements and build the detail page the way you want. You could for instance use `<h1>` for the recipe title, `<h2>` as headings for ingredients and description, and `<p>` for rendering of the retrieved ingredients and descriptions.

You might have noticed that the description and ingredients looks a bit strange when rendering them? That's because we have created those elements with linebreaks, but Django does not render these linebreaks by default. To allow linebreaks in a variable to be rendered, you can use the following syntax:

```html
<p>{{ variable | linebreaks }}</p>
```

## Task 3: Display recipe image in detail.html

In addition to titles, descriptions and ingredients, we have also stored an image for each recipe. Now it's time to render these images, so go ahead and open `detail.html`.

Images can be rendered using an image-specific HTML tag called `<img>`. The `<img>` tag has a parameter called `src` (source), which specifies which path Django can use to find the image source. The `<img>` tag can be used like this:

```html
<img src="[PATH]" />
```

In order to find the source of the recipe image, we use the `image` field, and then we use the `url` attribute of that field. The following code will give you a URL (source) for the recipe image:

```
<img src={{ [VARIABLE].image.url }} />
```

Copy this command and switch out `[VARIABLE]` with your own recipe variable. Reload the page. Did it appear? Great! However, the picture is quite big. This can easily be solved by adding a `width` property to the HTML tag:

```
<img src={{ [VARIABLE].image.url }} width="500px" />
```

In this case, the `width` property is set to 500 pixels wide. Explore different sizes and find the one you like.

---

Ready for part 3 of the course? Click [here](/__tasks__/part3) to go to the next tasks.

You can find the solutions for part 2 [here](/__solutions__/part2).
