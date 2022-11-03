# less -p

-p: find matching patterns. This is useful when looking for a specific word or phrase in a file or to skim data.

` less -pNMDA 1471-2202-2-7.txt`: finds all patterns containing NMDA in the file, use *n* to go to the next pattern and *N* to go to the previous pattern.

![Image](less-p.png)

`less -pDNA *.txt`: finds all patterns containing DNA in all the text files in the directory biomed using *:n* to go to the next file.

![Image](less-*.png)

`less -N presults 1471-2202-2-7.txt`: finds all patterns containing results in this specific file with line numbers.

![Image](lessnumber.png)

#