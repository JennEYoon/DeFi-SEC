# Guide for editing Github History after the fact.   

Source:  https://codewithhugo.com/change-the-date-of-a-git-commit/  

One of the greatest and worst things with git is that you can rewrite the history. Here’s a sneaky way of abusing that, I can’t think of a legitimate reason to do this.  As with anything, thanks StackOverflow for all the options I can pick from 👍.  

#### Set the date of the last commit to the current date  
>GIT_COMMITTER_DATE="$(date)" git commit --amend --no-edit --date "$(date)"  

#### Set the date of the last commit to an arbitrary date  
>GIT_COMMITTER_DATE="Mon 20 Aug 2018 20:19:19 BST" git commit --amend --no-edit --date "Mon 20 Aug 2018 20:19:19 BST"  
  
  ***Woohoo! Worked!***
>GIT_COMMITTER_DATE="Sep 14, 2019 1:00 PM EST" git commit --amend --no-edit --date "Sep 14, 2019 1:00 PM EST"    
> (output)
>[master a78163c] Create git-test-hist1.txt                                                     
>A>uthor: Jennifer E. Yoon <jenneyoon@gmail.com>                                                
>Date: Sat Sep 14 13:00:00 2019 -0500                                                          
>1 file changed, 7 insertions(+)                                                              
>create mode 100644 git-test-hist1.txt 

 * Then git add . , git commit -m "", git pull to merge two histories, git push to change history on Github.  

#### Set the date of an arbitrary commit to an arbitrary or current date  
>Rebase to before said commit and stop for amendment:  
>
>git rebase <commit-hash>^ -i  (Copy commit long-hash number)  
>Replace **pick** with **e** (edit) on the line with that commit (the first one)  
>quit the editor (ESC followed by :wq in VIM)  

Either:
>GIT_COMMITTER_DATE="$(date)" git commit --amend --no-edit --date "$(date)"  
>GIT_COMMITTER_DATE="Mon 20 Aug 2018 20:19:19 BST" git commit --amend --no-edit --date "Mon 20 Aug 2018 20:19:19 BST"  

See here for more information around rebasing and editing in git:  
Split an existing git commit. https://codewithhugo.com/split-an-existing-git-commit/  

Following any of these 3 options, you will want to run:  
>git rebase --continue  
