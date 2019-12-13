---
path: "/post-two"
date: "2019-12-14"
title: "Scripting"
author: "Tom Spencer"
---

# Scripting

Today I did a bit of scripting for replacing several phrases in lots of files. I used the following script:

> for f in $(grep -l "^SECRET_KEY_BASE" ctesius1*)
> do
>  echo ${f}
>  sed -i '/^SECRET_KEY_BASE=.*$/a
> AIRBRAKE_PROJECT_ID=*********\nAIRBRAKE_PROJECT_KEY=************' ${f}
> done

Just to clarify, *for f in.. do... done* is a for loop to encapsulate the tasks within it. The command *$(grep -l "^SECRET_KEY_BASE" ctesius1*)* searches and makes a list of files in the Ctesius1 directory that have the phrase SECRET_KEY_BASE at the beginning of the line.

Here we are using regular expressions. grep is a command-line utility for searching plain-text data sets for lines that match a regular expression. Its name comes from the ed command g/re/p globally search a regular expression and print.

A regular expression (also “regexp”, or just “reg”) consists of a pattern and optional flags. There are two syntaxes that can be used to create a regular expression object. The "long" syntax regexp = new RegExp("pattern", "flags") and the shorter one using slashes ie regexp = /pattern/. Here // means no flags. /pattern/gmi signifies that we are using three flags in this regular expression g, m and i. Regular expressions may have flags that can affect searching. 

So, in the above example we are loop over files in Ctesius1 which have SECRET_KEY_BASE at the beginning of the line and echoing (or printing the file name). We also using the sed command to insert AIRBRAKE_PROJECT_ID and AIRBRAKE_PROJECT_KEY in every instance of the files which contain SECRET_KEY_BASE. The -i flag for sed means that we replace the instances in file. This can be quite dangerous if we don't have a backup. The ${f} at the end of the block means that we replace this phrase in each of the files over which we are looping.

We also grokked over another script that used awk (a very powerful shell script). awk is up there with sed in terms of power. It is an excellent tool for building UNIX/Linux shell scripts. AWK is a programming langauge designed for processing text-based data either in files or data streams. You can combine awk with shell scripts or directly use at the shell prompt. Here is the script for your grokking pleasure:

> #!/bin/bash
> set -ue

> delay=30
> attempts=10

> . /var/secrets/homeflow_migrations-$1.env

> template="${DATABASE_URL_TEMPLATE}"

> nodes=$(echo ${DATABASE_NODES} | awk 'BEGIN { FS = "," } ; { for(i = 1; i <= NF; i++) { print $i } }')

> for node in ${nodes}
> do
>  for ((i=0; i<=${attempts}; i++)) do
>    export healthcheck_host="${node}"
>    response="$(curl -Is --request GET --output /dev/null -w "%{http_code}" "http://${healthcheck_host}:9200" || :)"
>    echo "[${node}] Healthcheck response: ${response}"
>    if [[ ${response} == "200" ]]
>    then
>      echo "[${node}] Running migrations ..."
>      export replacement="${node}"
>      url="$(echo ${template} | sed "s/__HOST__/${replacement}/")"
>      RAILS_ENV="$1" DATABASE_URL="${url}" bundle exec rake db:migrate
>      echo "[${node}] Migrations complete."
>      break
>    else
>      echo "[${node}] Waiting ${delay} seconds before retrying ..."
>      sleep "${delay}"
>    fi
>  done
> done

Here we put #!/bin/bash at the top of the file so that the unix shell knows what kind of interpreter to run. We use set-ue ensures that the file exists if it hits an error. We then set the variables delay and attempts at the top of the file. We also include the .env file in the script at the top of the file. Then we set the template through the environment variable DATABASE_URL_TEMPLATE. We then set the nodes to the environment variable DATABASE_NODES and use awk to iterate over the number of fields in the DATABASE_NODES variable. We then iterate over the nodes and set each node to healthcheck_host and then make a curl request to the healthcheck_host. We then echo the messages relating migrations, url, replacing the host file with the new url and then calling bundle exec rake db:migrate on the url and printing the messages if the response has been successful.

The main shell script commands include grep. A simple grep command could include grep "boo" a_file. This would return every line that contains the word boo. grep -n "boo" a_file also shows the line numbers of occurrences of a string in a file. grep -vn "boo" a_file returns all the lines that don't contain the string "boo". Other tasks include tail to show the end of a file. Head shows the first ten lines of a file. xargs are used to build commands from standard input and find lists every folder and files recursively.


## Extra note:

There are 6 flags for regexes.

### i
This flag is case-insensitive. It means that there is no difference betweene A and a.

### g
This flag means that the searhc looks for all matches, without it only the first match is returned.

### m
Multiline mode means that ^ and $ match not only the beginning and end of the string but the beginning and end of each line.

### s
This flag enables 'dotall' mode. This allows the use of a dot . to match newline character \n.

### u
Enables full unicode support.

### y
Sticky mode means that we search at the exact position in the text.
