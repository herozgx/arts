# what does rsync do when transfering a file.

This artical is not an introduction of rsync userage which can be easily found from the manpage of rsync. 
```
$ man rsync
```
We knew that rsync is an increment transmission tool which is very efficient, and what we care about here is what happens underneath 
when rsync transfer a file, and how does it complete the increment transmission on the background
