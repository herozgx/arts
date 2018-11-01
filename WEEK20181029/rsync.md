# what does rsync do when transfering a file.

*Please forgive my poor English, any suggestion will be appreciate.*

This artical is not an introduction of rsync userage which can be easily found from the manpage of rsync.

```
$ man rsync
```

We knew that rsync is an increment transmission tool which is very efficient, and what we care about here is what happens underneath 
when rsync transfer a bounth of file, and how does it complete the increment transmission on the background.

There are three mode to transfer files using rsync, such as local transfer,  ssh tunnel to a remote shell and socket to a remote rsync daemon.  Althrough the media protocol is dirrerent, but the priciple is the same underground. so the illustrations are all using local transfer mode for the sake of simple and concentration on the principle. For example:  

```
$ tree
.
├── dst
└── src
    ├── file1
    └── file2

2 directories, 2 files

$ rsync -a src/ dst/
$ tree
.
├── dst
│   ├── file1
│   └── file2
└── src
    ├── file1
    └── file2
```

`src` is the source directory, and `dst` is the destination directory. they are on the same machine.

```
$ cat /dev/random > src/file1
$ cat /dev/random > dst/file1

$ ls -i dst/file1
8597954003 dst/file1

$ rsync -a src/ dst/

$ ls -i dst/file1
8597954222 dst/file1
```

As the rsync command is executing, at the same time , examine the dst directory

```
$ ls -A dst
.file1.HrvKeJ file1         file2
```

we will find a `.file1.HrvKeJ` is generate refer to file1 and the inode number is change after the rsync is complete.

