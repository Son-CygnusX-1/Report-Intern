#!/bin/bash

a=(httpd curl wget mtr)

for i in "${a[@]}"
do
        if [ `rpm -qa $i` ]
        then
                echo "$i installed"
        else
                echo "$i don't install"
                echo $i >> test2.txt
        fi
done

for i in `cat $HOME/test2.txt`
do
        yum install -y $i
done

