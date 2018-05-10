远程文件拷贝

```shell
rsync -av -e ssh —exclude='.svn' local_dir username@host/home/username/dist_dir
```

