title: 一行命令导入项目到IDEA
author: strongant
tags:
  - IDEA
categories:
  - 工具
date: 2017-11-12 13:11:00
---
## 如何使用一行命令打开一个zip文件并导入项目到IDEA

### 方法如下

首先你得有我上次分享的那个idea打开项目的shell脚本。

```
#!/bin/sh

# check for where the latest version of IDEA is installed
IDEA=`ls -1d /Applications/IntelliJ\ * | tail -n1`
wd=`pwd`

# were we given a directory?
if [ -d "$1" ]; then
#  echo "checking for things in the working dir given"
  wd=`ls -1d "$1" | head -n1`
fi

# were we given a file?
if [ -f "$1" ]; then
#  echo "opening '$1'"
  open -a "$IDEA" "$1"
else
    # let's check for stuff in our working directory.
    pushd $wd > /dev/null

    # does our working dir have an .idea directory?
    if [ -d ".idea" ]; then
#      echo "opening via the .idea dir"
      open -a "$IDEA" .

    # is there an IDEA project file?
    elif [ -f *.ipr ]; then
#      echo "opening via the project file"
      open -a "$IDEA" `ls -1d *.ipr | head -n1`

    # Is there a pom.xml?
    elif [ -f pom.xml ]; then
#      echo "importing from pom"
      open -a "$IDEA" "pom.xml"

    # can't do anything smart; just open IDEA
    else
#      echo 'cbf'
      open "$IDEA"
    fi

    popd > /dev/null
fi

```

然后使用如下脚本即可：

```
fullFileName=$1

suffix=${fullFileName#*.}

if [ "$suffix" != "zip" ];then
  echo "Must be a valid zip file"
else
  filename=${fullFileName%.*}
  echo "filename: $filename"
  echo "now unzip $1 and use idea $1"
  unzip $1 && idea $filename
fi

```

将此脚本另存为uao.sh ， 放在合适的位置，然后建立一个软链，这里我把它放在此处`/usr/local/bin/uao.sh`，建立一个软链接`ln -sf /usr/local/bin/uao.sh /usr/local/bin/uao`。以后如果要将zip文件解压，打开idea，导入项目到idea这三个操作，直接使用这个脚本一行命令一步即可完成。赶快试试吧！