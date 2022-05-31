---
share: True
---
**notatki**{: #notatki .hash}  
 **blog**{: #blog .hash}  
 **wip**{: #wip .hash}  
 



# Step 1. Create a repository for the blog
## Create a repo
 Go to github.com and create a repo there with the name _username_.github.io, where _username_ is your username (or organization name) on GitHub.
## Add an initial content to the repository
```bash
$ git clone https://github.com/<username>/<username>.github.io
$ cd <username>.github.io
$ echo "Hello World" > index.html
$ git add --all
$ git commit -m "Initial commit"
$ git push -u origin main
```

## Enable the GitHub Pages in the repo. 
Go to the  repository Settings -> Pages and see that the site is published![[Pasted image 20220531100228.png]] 
## Check that the site is working
Go to the `https://<username>.github.io/` and check that you see 'Hello World' there.

# Step 2. Install mkdocs and plugins
```shell
$ yay -S mkdocs mkdocs-bootswatch mkdocs-material-extensions mkdocs-rss-plugin
```


or just

```bash
$ pip install mkdocs mkdocs-bootswatch mkdocs-material-extensions mkdocs-rss-plugin
```


# Step 3. Create a blog structure
## Create a blog
```bash
$ BLOG_PATH=<the path to the cloned github repo>
$ BLOG_NAME=<the name of your blog>
$ cd $BLOG_PATH
$ mkdocs new $BLOG_NAME
```


## Test that it works
```bash
$ cd $BLOG_PATH/$BLOG_NAME
$ mkdocs serve
```


You should be able to see the default starting page
![[Pasted image 20220531093424.png]]

## Customize it
Edit the `mkdocs.yml`: 
```

site_name: <Desired site name>
site_description: <Site description>
site_url: https://<username>.github.io/
```


Add an empty `custom_attributes.css` to the `docs/assets/css`. It is requred for callouts to work. We'll fill it later.

```

$ mkdir -p docs/assets/css
$ touch docs/assets/css/custom_attributes.css
```


# Step 4. Install Obs2MK
```bash
$ poetry init
$ poetry shell
$ poetry add git+https://github.com/Mara-Li/obsidian-mkdocs-publisher-python.git@main
```


# Step 5. Set up Obs2MK
Issue 
```shell
$ obs2mk
```

1. It will ask where the obsidian vault is located. Provide the path. 
2. It will ask for the path to the cloned github repository. Do that as well.
3. Specify an URL of your blog (`https://<username>.github.io/`).
4. Specify the frontmatter key indicating that the note is ready to be published. You can safely leave it as it is.
5. Specify the root for the notes. `/` makes them live in the root of the site's tree.
6. Leave the key for citation as is

!!! WARNING
	I had to patch several files to make it work: 
	1. The file_checking.py:231 in the Obs2MK package, as it didn't have quotes around `docs`
		2. `config.py:468`, IMG = Path(BASEDIR, "/docs/assets/img/")-	IMG = Path(BASEDIR, "docs/assets/img/")
	



https://forum.obsidian.md/t/obsidian-mkdocs-publisher-a-free-publish-alternative/29540

https://github.com/Mara-Li/obsidian-mkdocs-publisher-python/tree/v3.7.1

https://mara-li.github.io/obsidian_mkdocs_publisher_docs/documentation/create%20the%20blog/

