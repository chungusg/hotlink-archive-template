# hotlink archive Template

See the demo site made from this template IN ACTION: https://hotlink-archive-template.pages.dev/


**This guide is for an easy way to host files for hotlinking on AO3 or elsewhere, using github and cloudflare pages.**

I've encountered far too many dead links in fanfics and forums simply because a hosting service decided to dump older files, or they decided to change their TOS to no longer allow hotlinking or certain kinds of content (nsfw, fictional graphic content). See **Optional Steps** for even more options.

This is an easy, barebones way to permanently host images that you don't want deleted unexpectedly or that you can't host elsewhere. (Emphasis on barebones. This will not be a nice portfolio style site. Unless you decide to code that yourself!) You can follow the link above for an example of this type of site.

*It is also EASY to upload and use on mobile devices after initial setup!*


### Tools you will need:

- **Cloudflare Pages/Workers** [link to learn more] is a free to use static page hosting service. This will publish your files and make them available online. There is a limit to the amount (and type?) of data you can upload for free, but you can pay for proper hosting if you want to exceed it.

- **Github** [link to learn more] is a code sharing/storage platform. Your files will go here first before being published on Cloudflare Pages. You can edit and upload files through your browser at github.com, or through Github Desktop, a program you install on your computer. There are limits to Github repositories, but they are generous (a suggested max of 1GB to 5GB per repo). 

## Basic Setup
**1. Create a github account**

<img src="https://hotlink-archive-template.pages.dev/rename1/git-signup.gif" alt="sign up for github" height="350">

[insert brief explination of what a repository is and how to find/use it, with link to a reference to learn more]


<br/>

**2. Copy this template repository [hotlink-archive-template](https://github.com/chungusg/hotlink-archive-template)**

This the template repository you are currently on. It will use an "Action" in python to automatically create a "home" page with an index of all the files in the folder every time it is updated. 

<img src="https://hotlink-archive-template.pages.dev/rename1/github-use-template.webp" alt="copy template" height="200">

> NOTE: You will be prompted to select the privacy features when you copy it. I recommend you **set your repository to Private**. Github's history feature is extensive, so if you have sensitive content or think you might want to delete something later, it will be hard to get rid of it completely once it's been committed and publicly available.

Make sure you give this repository a short descriptive name, as you will need to identify it later.
<br/>

**3. Enable Action permissions**

In order for the script to work, you need to give Actions permission to read and write in your repository.

Within your repository, go to the tab Settings > Actions > General > Workflow Permissions

![permission setting](https://hotlink-archive-template.pages.dev/rename1/github-permission.png)

Make sure to hit Save.

<br/>

**4. Create a Cloudflare account**

<img src="https://hotlink-archive-template.pages.dev/rename1/pages-signup.gif" alt="signup for cloudflare pages" height="350">

<br/>

**5. Create a Pages (or Workers) project and link it to your Github repository**

Your Pages project will create the front end of the site where the images will be displayed. You will be able to link those images to other platforms like AO3. 

You can create either a Workers or Pages project by going to Add > Pages (or Workers).

**Workers vs. Pages**
- Workers is subsuming Pages on Cloudflare and now has all the same static hosting capabilities, in addition to its original server-side processing services. If your curious, you can learn more about the differences [here].
- While Workers has the similar capabilities, I recommend Pages for this project. It has the added bonus of a cleaner URL if you do not have your own domain: *“MySite.pages.dev”* in Pages vs Workers'  *“MySite.username.workers.dev”*.
- However, the differences between them are small enough with regard to what we want them to do today, that either will work.

You will be prompted to import an existing Git repository. (IMAGE) You will need to give it access to your Github to do this. I recommend allowing access to (ANSWER about whetehr to do all repositories or only select ones)

Select the repository on Github which you have previously named, then hit "Begin setup". You do not need to change any settings on the next page, so hit "Save and Deploy". Your image display site will then be live! The URL will be *"repositoryname.pages.dev"*. It may take a few minutes to become accessible.

Now you're done with the basic setup!
<br/>

## Adding files

You will add the files through Github. Open up the repository that you named (it can be found at *github.com/username/repositoryname*). You will see a list of folders and files that are in that repository. Click into the folder "fan-stuff". In the top right, go Add file > Upload files and drag in the images you want added. You will need to name the images BEFORE you upload them, as there is not an easy renaming feature within Github itself.

In the Commit changes box, choose a title for what action you are doing. This will help you backtrack uploads if needed. For example, it could be "Uploaded Batman Week Art". Make sure it's set to "commit directly to the main branch", then commit those changes. This will upload the files. You can do this on mobile, desktop, or the Github desktop program!

Now, if you visit your site, you will see your uploaded image under the "fan-stuff" folder!

> Continue onto **More Setup** to customize your site

<br/>


## More Setup
### Perform site customization/advanced setup with Github Desktop on your PC
Github’s web UI is great, but it has major limitations. I highly recommend that you use Github Desktop during the initial setup, as well as when you want to make major organizational changes to your files/site. Once you have everything set, though, you can be like me and basically only use Github in your browser to upload whatever files you want to hotlink at the moment.

- **Download Github Desktop and “clone” (download a copy of) the repository you made.**
- This is the best time to rename/rearrange folders + files, etc.
	- There are other methods in the **Troubleshooting** section if you need, but Github Desktop is by far the easiest way
	- see **Adding/Renaming Folders** for important info on how to properly rename/add folders
	- see **About the Index Page** for how to customize your index pages
- Once you’re done editing, “push” (upload) all the changes you made to your online Github repository.

Having some sort of text editor like Notepad++ is useful for editing any code, the automatic color-coding is very helpful. You can edit in plain old Notepad as well, it just won’t look as nice.

### About the Index Page
The template repository uses a python Action to automatically create an HTML "home" page with an index of ALL the files in the folder every time it is updated. 

This is particularly convenient for mobile use, as I can upload a file, and the python action automatically updates the index page without me having to manually update anything.

- If you don’t want this, just disable the “create-index” Action and delete the .py files. You can just type in the file locations to get to each file, or you can manually maintain an home/index page yourself, which isn't hard if you know some basic HTML and can remember to do it consistently.
- Also note that if you wish to change any of the content on your index pages, you must edit the "index.py" file, not the "index.html" file as "index.html" gets re-written every time the index Action is run in order to keep the file index up to date.

### Adding/Renaming/Deleting Folders
**Disclaimer:** This is a bit convoluted because I am extremely unqualified to be working with python OR HTML. There’s probably an easy way to do this, but I don’t have the skill to do it, and most of the stuff here is copied from stuff I found around. If you know a better way to do things, please let me know, it’d make my life easier too!

Adding or renaming folders involves some extra steps. 

1. The "index.py" file inside the folder needs to be edited to match the parent folder name. This is found near the top of the file.

![where to change folder name](https://hotlink-archive-template.pages.dev/change-index-folder.png)


2. Then the outer-most "create-index.py" file needs to be updated to match the new name as well. If you’ve added a new folder, duplicate and adjust the code to match. 
This is found at the bottom.

![where to edit](https://hotlink-archive-template.pages.dev/create-index.png)

- If you don’t need any folders at all, great! Just delete them and their contents! No need to edit any files. (Don’t delete “index.html” or “create-index.py” or “.github/workflows”!)
- If you would like to have these folders for later use, leave them as-is and simply delete/comment out (using # at the beginning of a line will make it “invisible” to the computer) the relevant lines of code at the bottom of "create-index.py" like in the previous step for renaming folders.  Also, add the folder’s name to the “exclusions” list at the top of the "create-index.py" file so that it doesn’t show up on your index page.

![enter the folder you want to exclude](https://hotlink-archive-template.pages.dev/rename1/index-exclude.png)

<br/>

## Tips/Troubleshooting


### (Re)name your files before uploading
It’s not possible to rename image/media files on Github’s web UI (it is possible with the local Git program). The INDEX action lists out the names of your files exactly, so you will end up with ugly strings of numbers and letters on your index page, which is terrible to look at and also plain old CONFUSING to navigate.
So if you're uploading on mobile or through the Web UI, name your files with easy to remember and distinctive filenames before you go ahead and upload them. This makes everything much easier, and it makes your index look nice :)

### My website isn’t updating when I edit my Github repository!

Check to see if your Pages is retrieving from the correct branch, and if it has automatic deployments enabled. 

![check settings](https://hotlink-archive-template.pages.dev/rename1/pages-branch.png)

<br/>

### Can’t see your Github repository when trying to link it on Cloudflare?

Check your Github applications Repository Access settings. Go to your ACCOUNT Settings > Integrations - Applications > Cloudflare > Repository Access

![cloudflare access setting](https://hotlink-archive-template.pages.dev/rename1/github-access.png)

<br/>

### Index action is failing!

Go back to step 3 in **Basic Setup** and check if you’ve given Actions permission to read and write.
If that’s not the issue, check to see if you’ve set up your "index.py" files correctly. The folder names should correspond to the parent folders, and the "create-index.py" file in the outer-most folder should have the correct folder names at the VERY BOTTOM.
<br/>

### How do I rename a folder (or move a file) in Github’s web UI?

It isn’t possible to directly rename a folder in Github’s web UI, doing it using Git on your computer is the most foolproof way to do it. But there is a way (except for media files). 

1. Go into the folder you want to rename and select a file such as “index.html” and enter the “edit” mode. 

2. Go to the file name and backspace until you can edit the parent folder name as well. This will create a new folder with the new name. 

You’ll have to do this to every file in the folder until they’re all in the new folder. 

Unfortunately, *you can’t do this with media files like png/jpg/etc*, because entering the “edit” mode on a photo “breaks” it somehow, and bye-bye image :’)
(Don’t worry if this happens, just don’t commit the change or roll it back in your history).

<br/>

## Optional Steps

### Make deployment (fully or semi-)Manual
You can play with cloudflare and github to make deployment of your site completely manual. This is a safeguard in case you accidentally make a change or delete something from your github, it won't affect your website.
#### Semi-Manual
You could do a semi-automatic deployment, with a "Production" branch on your github that is separate from the branch you edit. This creates an extra step before anything is published on Cloudflare. A safeguard against accidental changes/deletion of sorts :)

<img src="https://hotlink-archive-template.pages.dev/rename1/pages-settings.gif" alt="navigate to settings on cloudflare">

1. Go to Settings
2. Choose Production build branch (MAIN or CLOUDFLARE) and enable (or disable) automatic deployments
- If you choose MAIN, every change you commit to MAIN will be published to Pages
- If you choose CLOUDFLARE, you will have to manually pull any changes from MAIN to CLOUDFLARE first before anything is published to Pages
	- Or you can do it the other way, by editing on a side branch and only merging with MAIN when you want to publish.

#### Fully Manual
Or you can create a manual command that you have to enter on github to trigger a deployment on cloudflare. I'd say if you're paranoid about anything happening to your site for any number of reasons, this is the safest choice. Unless you manually trigger the command, your Pages site will be completely untouched.

This can be done in many ways, I think the most straightforward is with [Deploy Hooks](https://developers.cloudflare.com/pages/configuration/deploy-hooks) (maybe in conjunction with Actions if you want to make it mobile-friendly), and might be a bit complicated, but not too hard to figure out with some Google-fu. 

Here’s some links I think will be useful (note: I don’t use this  method, so these haven’t been tested) 

- [Manual trigger action tutorial](https://leonardomontini.dev/github-action-manual-trigger/)

- [How to configure Github webooks](https://magefan.com/blog/configure-webhooks-in-github?srsltid=AfmBOoo4gAHxJdunxkJlQ6ZhVnGVAVEuyRn5hnHBqTdbYmcHWFwIM5s8)

<br/>

### Storing Locally instead of on Github
Although this guide is written with Cloudflare's Github integration in mind, particularly for easy online/mobile access, you can also keep your files locally on your PC and directly upload your assets onto your Pages project. This gives you full control over what happens to your files (keeping backups is a good idea, you can still use Github Desktop, just don't push/pull online).
- Simply clone/download the repository as it is, customize it as you like, and upload everything to Cloudflare in a new **Pages** project (this is not an option for Workers).

One thing that will NOT work the same is the Create-Index Action that only works on Github. 
- I have made a "create-index.exe" that will execute the "create-index.py" files in the exact same way as they would work with the Action. You do not have to install python for this to work (if I did everything right). Simply run "create-index.exe" whenever you make a change and want to update the "index.html" files
- Remember, this is EXACTLY THE SAME as the index Action, meaning you have to edit each "index.py" file when you rename folders, add a folder, want to exclude a file from the index, etc. (See [Adding/Renaming Folders](https://github.com/chungusg/hotlink-archive-template/tree/main#addingrenamingdeleting-folders) for how to do this)

<br/>

---

Find me on [Bluesky](https://bsky.app/profile/indecisive-fangirl.bsky.social). Or if you have a problem, open an [Issue](https://github.com/chungusg/hotlink-archive-template/issues) on this project :)

I'll try to answer your questions as best I can! But really, I am the most amateur of amateurs and figured this all out using Google, so I might not be of much help ^^;

I also recommend [Squidge Images](https://images.squidge.org/) (an offshoot of Squidge.org) as a fairly trustworthy alternative. However, Squidge Images does have some additional rules that Squidge does not, and what crosses the line is at their discretion.
