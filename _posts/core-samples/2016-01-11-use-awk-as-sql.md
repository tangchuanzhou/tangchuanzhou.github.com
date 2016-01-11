---
layout: post
category : lessons
tagline: "shell"
tags : [shell]
---
{% include JB/setup %}

Awk is a good tool for handling the text.[awk introduction](https://zh.wikipedia.org/wiki/Awk)
This is a simple tutorial use awk like sql, hope you have some basic knowledge of the awk.
the contents I listed should be saved as test.awk and use "awk -f test.awk student.txt"

## Overview

### DataSource We Use

    table1:
    student.txt:
    id     |     name     |     gender     |     course
    123456|allen|male|mathe
    123456|allen|male|english
    234567|jerry|male|mathe
    234567|jerry|male|english
    345678|chelsea|female|mathe
    345678|chelsea|female|english

    table2:
    grades.txt:
    id|grade
    123456|89.8
    234567|78.9
    345678|90.2


### Select id from Student
    ==========test.awk================
    BEGIN{
        FS = "|"
        print "id"
    }
    {
        print $1
    }
    END{
    }
    ==========test.awk================


### Select * from Student
    ==========test.awk================
    BEGIN{
        FS = "|"
        print "id|name|gender|course"
    }
    {
        print $0
    }
    END{
    }
    ==========test.awk================

### select id, count(id) from student group by id?
    ==========test.awk================
    BEGIN{
        FS = "|"
    }
    {
        if ($1 in array)
    {
        array[$1] += 1
    }
    else {
        array[$1] = 1
    }
    }   
    END{
        for(i in array){
        print i,array[i]
    }
    ==========test.awk================

### select distinct id from student
    ==========test.awk================
    BEGIN{
        FS = "|"
    }
    {
        if($1 in array) {
        #array[$1] = $1
    }
    else {
       array[$1] = $1
    }
    END{
        for(i in array) {
        print array[i]
        }
    }
    ==========test.awk================

### select id, name, gender, course, grade from student, grade
    ==========test.awk================
    BEGIN{
        FS = "|"
    }
    {
    if(NR == FNR) {
      if ($1 in array_ids) {

      }
      else {
        array_ids[$1] = $2
        #print $1,array_ids[$1]
      }
      next
    }
    if ($1 in array_ids) {
        #print "test"
         print $1,$2,$3,$4,array_ids[$1]
     }
     else {
         print $1,$2,$3,$4,""""
     }
    }
    END{

    }
    ==========test.awk================

### some summary

for some simple text handling, we could use some simple shell scripts to handle it, it just works.