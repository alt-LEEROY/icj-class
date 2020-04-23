# Your final project

Your goal with this final project is to create a multi-page website using the [icj-project-template](https://github.com/utdata/icj-project-template) that has an index and multiple detail pages. It will be published through Github Pages.

I am supplying you with the idea (a band website for Queen) and assets (images and data). You may add additional content and images, as long as they are public domain material (like from Wikipedia).

Your site should be clean and well-designed. Your code should also be clean, with proper indenting for parent-child related items. Believe me, you will thank me later.

## Some strategies on how to tackle a project

> Read all the directions before you start coding anything.

- Look through the photo and data assests so you know what you have to work with.
- Physically draw out what you want your pages to look like so you have a goal in mind. (There is a first assignment to provide sketches.) Think first how it will look on a phone, then a tablet, then a desktop screen. Draw each version out.
- Work on the structure of the site first. Basically get all the template structure and HTML/Bootstrap elements on the page. Build the structure for mobile first, then consider wider page widths.
- Then work on the loop logic for the member list and discography. Get the loops working first, then make adjustments to make them look the way you want.
- Then work on the logic for the detail layout and pages. Again, get the structure working first so you know you are calling the data correctly, then make it look the way you want.
- Lastly, you can make it all look pretty with CSS adjustments.

Remember: Think mobile first, then adjust for larger screen widths.

## Requirements

### Project structure and helper notes

The project structure should include:

- A base layout that is extended throughout the project.
- A detail layout that is then extended to detail pages for the band members.
- At least one Nunjucks partial that is included into another layout template. (A good project will have several.)
- The project must use the following Bootstrap components and concepts:
  - [Responsive images](https://getbootstrap.com/docs/4.4/content/images/) throughout.
  - A [Jumbotron](https://getbootstrap.com/docs/4.4/components/jumbotron/) for a header.
  - A [Navbar/Navs](https://getbootstrap.com/docs/4.4/components/navbar/) that links to each member.
- You must use at least one scss partial with your Sass code. (A good project would have several.)
- You must use at least one [Google Font](https://fonts.google.com/) somewhere.
- This should all be in its own repo, published through Github Pages.

Everything should look beautiful and be functional. Any additional content beyond that provided in the data can be pulled from Wikipedia, but include a link to the source of the material.

### Index page

The the index should have:

- A short description of the band. You can get this from Wikipedia or other public sources, but please source it properly (i.e. give credit and link back).
- A list of the original members with links to their detail pages. Use a Nunjucks loop using the data provided to write efficient code. One option might be to use the Bootstrap [Cards](https://getbootstrap.com/docs/4.4/components/card/) object with their image, name and url.
- A listing of all of Queen's studio albums built from the the data/images provided. You could do this a number of ways, using cards, the Bootstrap [Media List](https://getbootstrap.com/docs/4.4/layout/media-object/#media-list) or your own HTML design as long as you use the images and data in a Nunjucks "for" loop, similar to the lesson we used in class.

### Detail pages

Each band member page should extend a detail layout.

Be sure to read the **very important note below** about how to filter data to use just one row of an array.

The layout should have:

- Two columns that stack on mobile but become two columns at `sm` and wider. You can adjust widths as the pages gets wider.
- In those two columns, you should have (all from data provided):
  - Photo of the band member
  - Headline of their name
  - All the bio information (birthdate, etc.)
  - Narrative about the member. (See note in Members data below.)

You can design or organize the above however you wish.

## Assets available

To save you time, I've collected a series of images and JSON data about the band members and discography. I've supplied more images than necessary so you can choose ones you like.

Available for you to use:

- A [collection of photos](img.zip) divided into three parts. Band photos, band members, and album covers. Expand the folder, take the images and put these inside your `src/img/` folder. Remember to restart gulp after installing the photos.
- A [queen.json](queen.json?raw=true) file with: A "members" array about band members and a "discography" array for the list of albums. Save this as `src/njk/data/queen.json`.
- A [tour.json](tour.json?raw=true) file for the extra credit option explained below.

### Members data

The data in the "members" collection includes:

- slug: If you name your band member pages the same as this slug, you can use them in loops for the href URLs. For example, `href="{{ members.slug }}.html"` would link to `freddie-mercury.html` and so on.
- name: Full printable name of the member.
- instruments: A list of what instruments/positions they play.
- tenure: When they were in the band.
- birthplace
- birthdate
- image: The filename of a color image of the band member.
- imagebw: the filename of a different, black and white image of the band member.
- text: This is a several paragraph description of the band member, in HTML. You can use the [safe](https://mozilla.github.io/nunjucks/templating.html#safe) tag to use as HTML, like this: `{{ members.text | safe}}`.

Use all of these on the member detail pages.

### Discography

The data in "discography" includes;

- title: The title of the album
- year: The year it was released
- image: The filename of an image of the album

> Side note: To create the `queen.json` file, I organized the information in a [Google spreadsheet](https://drive.google.com/open?id=1rT71c8CXtx3x2ak6nawjpAGukLNLo1lrbLuvjvZ9zFE) and then used this [csvjson](https://www.csvjson.com/csv2json) site to convert to JSON. This is already done for you ... I'm just telling you how I did it.

You can put the discography on the index or it's own page. You DO NOT need individual pages for each album.

## Important notes about using data

### Loops

On your index, you should use a Nunjucks `{% for member in queen.members %}` loop like the books example to create your display of members. You should use a similar loop for the discography.

### Filter for member pages

You can (and should) also use the "members" collection for your band member detail pages to save a lot of extra coding. It works like this:

On your `detail.njk` layout you can build your template to use properties from the "members" collection. You can code the whole page in the layout, and use placeholders for the data like this example:

```html
<h1>{{ members.name }}</h1>
```

`members` is the collection. `.name` is the key value you are using from the array.

Then on the page for a specific band member, you can extend the `detail.njk` layout and then use the Nunjucks [set](https://mozilla.github.io/nunjucks/templating.html#set) tag to filter the data to a single "row" based on its order in the data. Here is the weird thing, the order count starts at zero. So, if you want to use Freddie Mercury's data, and he appears first in the data, you access it using `members[0]`.

Filename `freddie-mercury.njk` would have the following content:

```html
{% extends '_layouts/detail.njk' %}
{% set members = queen.members[0] %}
```

Given the above, now the `{{ members.name }}` value carried over from `detail.njk` will display the text "Freddie Mercury" on his page.

Brian May appears second in the data, but since we count from zero he is position `1`. Create a page `brian-may.njk`, extend the `detail.njk` layout, set members to `queen.members[1]` and you'll get "Brian May" for the `{{ members.name }}` value.

## Deadlines

Canvas is the final word on deadlines, but in general they are in this order:

- A sketch of your index and detail layouts, including mobile, tablet and desktop views.
- A check-in on your HTML templates and data. It's best to get all your logic working before you start styling it. I'll also be checking for responsive design (i.e., different column widths for different screen widths.)
- A check-in on your CSS. You don't have to be finished, but this allows me to offer some feedback.
- On our last class day, you'll show your progress to everyone. You should publish what you have so far to Github Pages so we can review it in class.
- Final deadline for the project when I pull a copy of your repo for grading.

## Extra credit

### Billboard hits chart

For extra credit, you can add a bar chart of Queen's Billboard Hits to your project through [Datawrapper](https://www.datawrapper.de/).

- Click "Start Creating".
- Copy and paste this [csv data](queen-billboard-weeks.csv?raw=true) into Datawrapper.
- Double check that the chart matches the csv data.
- Make a bar chart and customize it. Make sure the chart has a title.
- When it's finished, copy the embed code (make sure it's responsive iframe), and paste the code into your html where you want the chart to appear on your page.

### Tour dates table

Another option is to make a [responsive table](https://www.w3schools.com/bootstrap/bootstrap_tables.asp) or a [data table](https://datatables.net/) of Queen's 2020 tour dates.

- Save the file [tour.json](tour.json?raw=true) into your `src/njk/data/` folder and restart gulp so the data is available.
- Use this data to make a table with Queen's 2020 tour dates, cities and venues. Refer to [loops](#loops) for help.
