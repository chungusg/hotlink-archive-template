# hotlink archive Template

See the preview here: https://hotlink-archive-template.pages.dev/


**This guide is for an easy way to host files for hotlinking on AO3 or elsewhere, using github and cloudflare pages.**

I've encountered far too many dead links in fanfics and forums simply because a hosting service decided to dump older files, or they decided to change their TOS to no longer allow hotlinking or certain kinds of content (nsfw, fictional graphic content). Currently, both Cloudflare and Github have TOS policies on par with AO3 in terms of content they allow, so it seems like a perfect solution for fandom.

This is an easy, barebones way to permanently host images that you don't want deleted unexpectedly or that you can't host elsewhere. (Emphasis on barebones. This will not be a nice portfolio style site. Unless you decide to code that yourself!)

*It is also EASY to upload and use on mobile devices after initial setup!*


### Tools you will need:

- **Cloudflare Pages/Workers** is a free to use static page hosting service. This will publish your files and make them available online. There are limits to it, but honestly they are so large that you should just pay for proper hosting if you go over them.

- **Github** is a code sharing/storage platform. Your files will go here first before being published on Pages. You can edit and upload files through your browser, or through Github Desktop, a program you install on your computer. There are also limits to Github repositories, but they are also generous (5GB per repo iirc). 

## Basic Setup
1. Create a github account

<img src="https://hotlink-archive-template.pages.dev/rename1/git-signup.gif" alt="sign up for github" height="350">

<br/>

2. Copy this template repository [hotlink-archive-template](https://github.com/chungusg/hotlink-archive-template) or make one from scratch

The template repository uses a python Action to automatically create a "home" page with an index of all the files in the folder every time it is updated. 

<img src="https://hotlink-archive-template.pages.dev/rename1/github-use-template.webp" alt="copy template" height="200">

<br/>

3. Enable Action permissions
In order for the indexing script to work, you need to give Actions permission to read and write in your repository.
Repository settings > Actions > General > Workflow Permissions
![permission setting](https://hotlink-archive-template.pages.dev/rename1/github-permission.png)


4. Create a Cloudflare account
<img src="https://hotlink-archive-template.pages.dev/rename1/pages-signup.gif" alt="signup for cloudflare pages" height="350">
<br/>

5. Create a Pages project and link it to your Github repository
- Be sure to use Pages, not Workers 
- Workers is subsuming Pages on Cloudflare and now has all the same static hosting capabilities, in addition to its original server-side processing services. 
HOWEVER, I still recommend Pages, in the instance that you do not have your own domain AND care about what your URL looks like. 
e.g. For a project "MySite" your URL for Pages = *“MySite.pages.dev”*, while for Workers = *“MySite.username.workers.dev”* 
Very minor, but something that bugs me :)

6. Done with basic setup!
- The default settings for your Pages project should grab the files from your Github repo every time your repository is updated.
- To add files, upload them in your Github repository in the folder you want, and COMMIT the changes.



## More Setup
### Perform site customization/advanced setup with Github Desktop on your PC
Github’s web UI is great, but it has major limitations. I highly recommend that you use Github Desktop during the initial setup, as well as when you want to make major organizational changes to your files/site. Once you have everything set, though, you can be like me and basically only use Github in your browser to upload whatever files you want to hotlink at the moment.

- **Download Github Desktop for an easy to use graphic UI, and “clone” (download a copy of) the repository you made. Once you’re done editing, “push” (upload) all the changes you made to your online Github repository.**

Having some sort of text editor like Notepad++ is useful for editing any code, the automatic color-coding is very helpful. You can edit in plain old Notepad as well, it just won’t look as nice.

### About the Index Page
The template repository uses a python Action to automatically create a "home" page with an index of ALL the files in the folder every time it is updated. 
This is particularly convenient for mobile use, as I can upload a file, and the python action automatically updates the index page without me having to manually update anything.
- If you don’t want this, just disable the “create-index” Action and delete the .py files. You can just type in the file locations to get to each file, or you can manually maintain an home/index page yourself, which isn't hard if you know some basic HTML and can remember to do it consistently.

### Adding/Renaming/Deleting Folders
**Disclaimer:** This is a bit convoluted because I am extremely unqualified to be working with python OR HTML. There’s probably an easy way to do this, but I don’t have the skill to do it, and most of the stuff here is copied from stuff I found around. If you know a better way to do things, please let me know, it’d make my life easier too!
Adding or renaming folders involves some extra steps. 
1. The index.py file inside the folder needs to be edited to match the parent folder name. This is found near the top of the file.

![where to change folder name](https://hotlink-archive-template.pages.dev/change-index-folder.png)


2. Then the outer-most create-index.py file needs to be updated to match the new name as well. If you’ve added a new folder, duplicate and adjust the code to match. 
This is found at the bottom.

![where to edit](https://hotlink-archive-template.pages.dev/create-index.png)

- If you don’t need any folders at all, great! Just delete them and their contents! No need to edit any files. (Don’t delete “index.html” or “create-index.py” or “.github/workflows”!)
- If you would like to have these folders for later use, leave them as-is and simply delete/comment out (using # at the beginning of a line will make it “invisible” to the computer) the relevant lines of code at the bottom of create-index.py like in the previous step for renaming folders.  Also, add the folder’s name to the “exclusions” list at the top of the create-index.py file so that it doesn’t show up on your index page.

![enter the folder you want to exclude](https://hotlink-archive-template.pages.dev/rename1/index-exclude.png)


## Tips/Troubleshooting


### (Re)name your files before uploading
It’s not possible to rename image/media files on Github’s web UI (it is possible with the local Git program). The INDEX action lists out the names of your files exactly, so you will end up with ugly strings of numbers and letters on your index page, which is terrible to look at and also plain old CONFUSING to navigate.
So if you're uploading on mobile or through the Web UI, name your files with easy to remember and distinctive filenames before you go ahead and upload them. This makes everything much easier, and it makes your index look nice :)

### My website isn’t updating when I edit my Github repository!
Check to see if your Pages is retrieving from the correct branch, and if it has automatic deployments enabled. 
![check settings](https://hotlink-archive-template.pages.dev/rename1/pages-branch.png)

### Can’t see your Github repository when trying to link it on Cloudflare?
Check your Github applications Repository Access settings. Go to your ACCOUNT Settings > Integrations - Applications > Cloudflare > Repository Access
![cloudflare access setting](https://hotlink-archive-template.pages.dev/rename1/github-access.png)

### Index action is failing!
Go back to step 3 in **Basic Setup** and check if you’ve given Actions permission to read and write.
If that’s not the issue, check to see if you’ve set up your index.py files correctly. The folder names should correspond to the parent folders, and the create-index.py file in the outer-most folder should have the correct folder names at the VERY BOTTOM.

### How do I rename a folder (or move a file) in Github’s web UI?
It isn’t possible to directly rename a folder in Github’s web UI, doing it using Git on your computer is the most foolproof way to do it. But there is a way (except for media files). 

1. Go into the folder you want to rename and select a file such as “index.html” and enter the “edit” mode. 

2. Go to the file name and backspace until you can edit the parent folder name as well. This will create a new folder with the new name. 

You’ll have to do this to every file in the folder until they’re all in the new folder. 

Unfortunately, *you can’t do this with media files like png/jpg/etc*, because entering the “edit” mode on a photo “breaks” it somehow, and bye-bye image :’)
(Don’t worry if this happens, just don’t commit the change or roll it back in your history).


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

---

Find me on [Bluesky](https://bsky.app/profile/indecisive-fangirl.bsky.social) 

I'll try to answer your questions as best I can! But really, I am the most amateur of amateurs and figured this all out using Google, so I might not be of much help ^^;
