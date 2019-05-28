# feedback-sofia
This repository is for maintaining the US website associated with the [FEEDBACK SOFIA Legacy Project]( http://feedback.astro.umd.edu) at the University of Maryland.

# Making changes
There are two ways to make changes to the website, the first can be used for simple things like updating html files.  

## The Method for Simple Changes
In the list above, click on the file you want to change.  In the upper right, click on the edit icon (a pencil).  Make the changes and click the green *Commit Changes* button at the bottom of the page (make sure the "commit directly to master branch" radio button is selected).

## The Method For More Extensive Changes
If you are going to make extensive changes to the website, say change the CSS or Javascript files, or modify the layout substantially, you should do it on your own local copy and then commit those changes back to this repository.

Note this updates the <i>master copy</i>.  The website is a copy not the master, and will be auto-updated from the master once per day. If you feel your changes should be immediate send email to Marc Pound to pull in your changes.

### 1) Get a local copy of the website
If you want to make changes to the website, first you need to get a local copy of this repository.  **You only need to do this series of steps once.**
1. Create a login at github.com
2. Create a local copy on the command line by typing
```shell
    git clone https://github.com/mpound/feedback-sofia.git
```
3. You will be prompted for your github login, type your github username and password
4. This will create a directory <tt>feedback-sofia</tt> which has all the files.
5. To make it so you don't have to type your github login every time you make a change, you can set a long timeout for credentials prompting:
```shell
    git config --global credential.helper 'cache --timeout=100000'
```
 
 ### 2) Edit the file(s) you wish to change
 1. Update your local copy with changes others may have made:
 ```shell
    git pull
 ```
 2. Edit your file(s)
 3. Commit those files back to the github repository so others can pick them up.  
 ```shell
    git commit -am "describe your edits here" 
    git push
 ```
 4. If the timeout above has been exceeded you will be prompted again for your user/password.
 
 Note this updates the <i>master copy</i>.  The website is a copy not the master, and will be auto-updated from the master once per day. If you feel your changes should be immediate send email to Marc Pound to pull in your changes.
 
