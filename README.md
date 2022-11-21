# How to build a website with a DataWrapper visualization that automatically updates

We start with a Jupyter notebook and a little bit of HTML, and we turn it into a beautiful auto-updating website.

## 1. Write the code

I wrote a Jupyter notebook called `Pumpkin update script` that saves a file called `pumpkins.csv`. You can name your script whatever you want, and have it save a file named whatever you want.

**Make sure the notebook successfully runs from top to bottom without errors.**

## 2. Point your workflow at the notebook

My GitHub Actions script in [.github/workflows/publish.yml](.github/workflows/publish.yml#L19-L20) is pointing at `Pumpkin update script.ipynb` because that's the name of my notebook.

If you have a different notebook name, change the file name there. It probably needs to be in quotes.

## 3. Create your repository

Send this all on up to GitHub. You can name your repo whatever you want!

## 4. Make sure the workflow runs

Go to the Actions tab and make sure the workflow runs successfully. It should run automatically when you push to GitHub.

You're looking for a **green check mark**. If you see a red X, something went wrong.

## 5. Check your repository

Go to your repository and make sure you see a file called `pumpkins.csv` in the root directory.

## 6. Set up GitHub Pages

Go to the Settings tab and click Pages from on the left-hand menu.

* **Source:** Deploy from a branch
* **Branch:** Use `main` and `/ (root)`

This posts all of your code as a *website* instead of just as a GitHub repo.

## 7. Check that your `pumpkins.csv` file is on the web

The site sometimes takes a few minutes to successfully go online or update, so be patient, but if you refresh the page you're on a few times, you'll see a notice that looks like this:

> **Your site is live at https://jsoma.github.io/auto-update-graph-datawrapper/**
> Last deployed by @github-pages github-pages 2 minutes ago

You can visit the website, but it probably doesn't look great yet. We'll fix that by adding our own chart to it! To do that, we'll need to **get the URL of the CSV file**.

**Take your filename and add it after your website URL.** For example, my process would be:

```
# If this is my site URL
https://jsoma.github.io/auto-update-graph-datawrapper/
# And this is my filename
pumpkins.csv

# Then my full URL to visit is
https://jsoma.github.io/auto-update-graph-datawrapper/pumpkins.csv
```

If it downloads a CSV, it worked! If you got a 404, confirm that you have the right filename and website URL.

## 8. Create a new DataWrapper chart with our data

Go to [DataWrapper](https://www.datawrapper.de/) and create a new chart.

On the first step – **Upload data** – click **Link external dataset** and paste in the URL to your CSV file from the last step. Mine looks like this:

```
https://jsoma.github.io/auto-update-graph-datawrapper/pumpkins.csv
```

After that, I select **Serve data file directly** because I want more than just hourly updates.

## 9. Build our chart/get our embed code

Now that DataWrapper has your data, go through process and create your visualization. At the end you're looking for **Embed code for your visualization**, with **Responsive iframe** version.

Mine looks like this:

```html
<iframe title="The biggest pumpkins, by state" aria-label="Bar Chart" id="datawrapper-chart-rmNfg" src="https://datawrapper.dwcdn.net/rmNfg/1/" scrolling="no" frameborder="0" style="width: 0; min-width: 100% !important; border: none;" height="728" data-external="1"></iframe><script type="text/javascript">!function(){"use strict";window.addEventListener("message",(function(e){if(void 0!==e.data["datawrapper-height"]){var t=document.querySelectorAll("iframe");for(var a in e.data["datawrapper-height"])for(var r=0;r<t.length;r++){if(t[r].contentWindow===e.source)t[r].style.height=e.data["datawrapper-height"][a]+"px"}}}))}();
</script>
```

Copy this code, it adds the chart to your website.

## 9. Add the chart to your `index.html`

The `index.html` sitting in this repository is your actual website. I secretly added it before we started!

Add your embed code to this file. I recommend pasting your embed code inside of the `<div class="content'>` section, but you can put it wherever you want.

## 10. Send your changes back up to GitHub

ToCommit and push your changes to GitHub. It will *probably* yell at you first, that you need to **pull changes from remote**. This means "we updated `pumpkins.csv` on the server, but you haven't updated the copy on your computer yet." If you're using GitHub Desktop, just keep clicking the blue buttons.

## 11. Check your website

Remember when we found that link to our website? My link looks like this:

> **Your site is live at https://jsoma.github.io/auto-update-graph-datawrapper/**
> Last deployed by @github-pages github-pages 2 minutes ago

Go to your website and make sure your chart is there! If it doesn't work, maybe wait a couple minutes and try again. You can also hold down **shift** and click the refresh button to **force refresh**.

## 12. Beautify your website

If you'd like to add more content to your website, you can edit the `index.html` file.

We're using a CSS framework called Bulma that you can [read more about here](https://bulma.io/). By editing your `index.html` and following the guidelines on the Bulma site, you can add navigation, buttons, columns, and lots more.

You might also want to check out my [lazy web basics](https://www.youtube.com/playlist?list=PLewNEVDy7gq1vO4fTJe5fJw4u63qiKt0o) YouTube playlist or  [Customize website with bulma CSS framework](https://youtu.be/iuLPLuxG2pI), which is a little newer and more specific to this project.