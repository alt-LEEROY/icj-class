# Publish the /doc folder to the web

Because we put our web site files inside a `docs` folder, we can take advantage of a special feature in Github called [Github Pages](https://pages.github.com/). It will allow us to publish our site to the Internet.

> Days after recording the in-class assignment video for this assignment, Github added functionality to publish Github Pages from any folder. As such, the video is a little out of sync with reality. See [this page](https://docs.github.com/en/github/working-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site) for the current directions. Use the **master** branch and the **docs** folder.

- Go into your Github repo for this project.
- Click on the Settings link.

![sass-ghpages-settings](../images/sass-ghpages-settings.png)

Go down to the Github Pages section and in the **Source** dropdowns:
- Choose the **master** branch.
- Choose the **/docs** folder.
- Click **Save**.

![sass-ghpages-docs](../images/sass-ghpages-docs.png)

Once the page refreshes, it will give you a link to where you can find your site. It works like this:

`https://YOUR-USER-NAME.github.io/YOUR-REPO-NAME/index.html`

It might take a couple of minutes for your site to publish, and if you first view the site and it isn't there, you may have to break your browser cache (hold down command while you refresh the browser) or use a private browser to see your changes. If that doesn't work, make a change to your html, commit and push the changes to Github again.
