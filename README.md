# manifest-testing
 
A repo meant to help me figure out:
1. How manifests in hammer work
2. How to effectively integrate them into git

Anybody else is free to follow along though if they also want to learn about manifests (they're cool!)

## The manifest bar

There is not much different about manifests and regular maps, you simply have extra courses in the same file that are otherwise completely hidden in the sidebar. Each row has 4 icons on the left and the name of the submap on the right, like so: 
![Manifest Window](/images/ManifestWindow.PNG)

The top left 'eye' icon can be clicked to toggle visibility of the manifest on or off. Most likely you will want this exclusively on for the map you are working on and off for all others, though it may be useful to occasionally check other submaps to make sure you are not building new geometry that overlaps with any of them.

The top right square may contain a red 'X', which indicates the submap file is write-protected and you cannot make any changes to it. You will probably never see this as I believe it is a Perforce thing that Git does not do.

The bottom right square may contain a pencil that indicates that you have unsaved changes in that submap. Simply select the submap and Ctrl+S to save them.

I don't know what the bottom left icon does.

## Setting up Git

Manifests are designed to be used with _version control systems_ that keep track of changes incrementally, allowing for completely accurate changelogs and, most importantly, easier collaborative editing. Valve uses Perforce with all of their games, but Git is cooler so I'm using that instead. Git is mostly used by coders so very few mappers probably know how to use it, but GitHub has a very nice tool that simplifies the process greatly. If you don't want to learn your way around the Git CLI commands, it is a life saver.

- Download it from here: [https://desktop.github.com/](https://desktop.github.com/)

To start, you will have to add a repository by cloning it from a URL (for example, `https://github.com/hexaflexahexagon/manifest-testing`). After that is done, you have all of the map's related files on your computer and can begin to make changes. Any time you make and then save changes you will see them pop up in the GitHub Desktop client separated by file. Green icons mean it is a brand new file that has been added, yellow means it already existed and was modified, and red means that the file was deleted. Once you have made any changes that you wish to share with everybody else, you must make a commit

## Git commits, pushes, and pulls

Some basic Git terms that you'll have to familiarize yourself with:

- Commit: A bundle of changes to files
- Push:   An action where you 'push' the commits on your machine to the central repository
- Pull:   An action where you 'pull' any new commits that others have pushed on to your local version of the repository. This does not happen automatically! You need to click the 'pull' button to get new changes on your computer.
- Origin: Another word for "the GitHub server" in our case. If you push to origin, you are uploading your changes for everyone else to see. If you pull from origin, you are grabbing the latest changes that everybody else has made and pushed from their computers.

In simple terms, whenever somebody else has made changes you will need to 'pull' those changes down from GitHub on to your computer. In the GitHub Desktop client, this is done through a button towards the top of your screen that contains an arrow pointing downwards. 

In order to 'push' your changes, you will need to first gather all of the edits you have made into one or more commits, give them nice titles and descriptions, and then 'push' those commits to origin for others to see. If you commit something but do not push it then others will not be able to see your changes. The button to push looks like so:
![Git Push](/images/GitPush.PNG)

## How to compile the map

Compiling a manifest map works exactly the same as a normal VMF, in theory. You open the .vmm file, make your changes, and then hit compile (or add the .vmm to CompilePal / whatever tool of choice you may use). However, due to a bug [that has been well documented](https://github.com/ValveSoftware/source-sdk-2013/issues/328), the `worldspawn` entity that is responsible for things like setting your skybox is completely broken when compiling a .vmm file. There are a few ways around this, however for the purposes of doing changes to just the course you are responsible for it may not be important that the skybox is broken and compiling the .vmm works fine. If so, I would encourage doing so as directly manipulating the .vmf files can have many strange knock-on effects. 

In order to do a full map compile that does not break, it is necessary to create a new VMF file that includes all of the relevant submaps as separate instances. The first link under the "Useful resources" section explains how to create this better than I ever could so I'll defer to that instead.

## Useful resources
- https://tf2maps.net/threads/guide-using-manifests-to-make-your-life-better.26145/
- https://tf2maps.net/threads/mapping-collaboration-or-using-manifest-and-version-control.24787/ 
