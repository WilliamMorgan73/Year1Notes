mv Moves file
rm removes files
mkdir creates a directory
touch updates most recent access time, if does not exist - Creates folder

1. 

└───home
    └───me
        └───stuff
            ├───admin
            │       todolist.txt
            │
            ├───junk
            └───work
                    coursework1.txt
                    coursework2.txt

2. 
	pwd = print working directory
	home/me/stuff/admin/

## B Dictionary

```
tr '\n' ' ' < 1342.txt.utf-8.txt | tr -dc '[:print:]' | tr -d '0-9_"{}[]()!:#$%&@^*,.-' | tr ' ' '\n' | tr 'A-Z' 'a-z' | sort | uniq
```

## C Shell Scripts

1. 

```
#!/bin/bash

for file in *

do

    count=$(wc -m < "$file")

    echo "There are $count characters in $file"

done
```

2. 

```
#!/bin/bash

if [ $1 -gt 10 ]

then

    echo "This number is bigger than 10"

else

    echo "This number is not bigger than 10"

fi
```

3. 

```
#!/bin/bash

  

# Check if MyTextFiles directory exists, create if it does not

if [ ! -d "MyTextFiles" ]; then

    mkdir MyTextFiles

fi

  

# Copy or move files based on the parameter

if [ "$1" -eq 1 ]; then

    cp *.[tT][xX][tT] MyTextFiles/

else

    if [ -d "MyTextFiles" ]; then

        mv MyTextFiles/*.[tT][xX][tT] .

    else

        echo "Warning: MyTextFiles directory does not exist."

    fi

fi

  

# List files in MyTextFiles directory and save to DirectoryListing.txt

ls MyTextFiles > DirectoryListing.txt

  

# Display the number of lines in DirectoryListing.txt

echo "The number of files listed in DirectoryListing.txt: $(wc -l < DirectoryListing.txt)"

```

# D Text translation

```
tr '\t' ',' < file.txt | tr 'A-Z' 'a-z' | tr "!" "1" | tr "@" "2" | tr "$" "3" | tr "%" "4" > fileOutput.txt
```

# E regular expression


