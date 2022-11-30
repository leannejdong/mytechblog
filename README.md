# mytechblog


## Step 1: Create your local Python Dev Environment

```
python -m venv mytechblog-venv
source myblob-venv/bin/activate
```

## Step 2: Install Pelican

```
pip install pelican markdown ghp-import
pip freeze > requirements.txt
```

## Step 3: Set up your blog

```
pelican-quickstart
```
They prompt you a few questions that you must answer:

```
> Where do you want to create your new web site? [.] 
> What will be the title of this web site? MyBlog
> Who will be the author of this web site? 
> What will be the default language of this web site? [en] 
> Do you want to specify a URL prefix? e.g., https://example.com   (Y/n) N
> Do you want to enable article pagination? (Y/n) Y
> How many articles per page do you want? [10] 
> What is your time zone? [Europe/Paris] 
> Do you want to generate a tasks.py/Makefile to automate generation and publishing? (Y/n) 
> Do you want to upload your website using FTP? (y/N) 
> Do you want to upload your website using SSH? (y/N) 
> Do you want to upload your website using Dropbox? (y/N) 
> Do you want to upload your website using S3? (y/N) 
> Do you want to upload your website using Rackspace Cloud Files? (y/N) 
> Do you want to upload your website using GitHub Pages? (y/N) 
Done. Your new project is available at /.../mytechblog
```

Pelican stores the created website in the folder output. However, on the main branch, we usually don't want to commit the generated output. The same is true for the virtual environment.

So, append some entries to the .gitignore file:

```
echo output >> .gitignore
echo myblog-venv >> .gitignore
```

## Step 4: Create a first post and preview

Now generate the whole web site:
```
pelican content
```
and start a development webserver

```
pelican --listen
```
so that we can preview it in the browser at localhost:8000.

## Step 5: Upload your changes

So far, it’s all locally on our machine. But we want to store the data for our blog on GitHub and we want to publish the generated website. To upload the data to our repository:

```
git add .
git commit -m "Sets up the blog"
git push
```
Now the changes have been uploaded to Github. But we still need to publish the changes.

## Step 6: Publish your website
With the ghp-import package installed, this is OK:
```
pelican content
ghp-import output
git push origin gh-pages
```

The first line generates the website (HTML, CSS, Javascript, whatever) and stores it in the output folder. The second line moves the content of the output folder to the gh-pages branch. This is a branch that will automatically trigger deployment actions on GitHub. The third line uploads the content of the gh-pages branch to the corresponding branch on our remote repository on GitHub. When we have done that, a GitHub action is starting. In our GitHub repository, go to the Actions tab. We see that an action called "pages-build-deployment" was executed. 


