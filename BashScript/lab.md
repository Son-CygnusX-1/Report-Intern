#!/bin/bash

yum list installed > $HOME/test.txt
rpm -qa > $HOME/test.txt
a=`grep '/^wget\|^curl\|^mtr\|^httpd' test.txt`
b=(curl wget mtr httpd)

echo $a | grep -o -E wget\|curl\|mtr\|httpd > test2.txt

for i in "${b[@]}"
do
        d=`grep $i test2.txt`
        #echo $d
                if [$d=""]
                then
                        echo $d
                        yum install $i
                fi
done
