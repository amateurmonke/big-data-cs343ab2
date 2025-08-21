# 21/08/2025

- Get Hadoop running
    
    ```bash
    cd hadoop-3.3.6/sbin/
    ./start-all.sh
    
    jps # to check if it is running
    ```
    
- Next step is changing that old input.txt file in root dir idk why. If you are a windows user, before doing this install dos2unix or smth like that. Or just buy a Macbook.
    
    ```bash
    cd hadoop-3.3.6/sbin
    cd
    hdfs dfs -mkdir /example
    hdfs dfs -put input.txt /example 
    
    # should give one file exists message
    ```
    
- Make one handson folder in home dir and add mapper.py and reducer.py
    
    ```bash
    cd
    mkdir handson
    touch mapper.py
    ```
    
    ```python
    # mapper.py
    #!/usr/bin/env python3
    
    import sys
    
    for line in sys.stdin:
            words = line.split()
            for word in words:
                    print(f"{word},1")
    ```
    
    ```python
    # reducer.py
    #!usr/bin/env python3
    
    import sys
    
    prev_word = None
    count = 0
    
    for line in sys.stdin:
        curr_word, value = line.split(",")
        value = int(value)
        if (curr_word == prev_word):
            count += value
    
        else:
            if(prev_word):
                print(prev_word, count)
            count = 1
    
        prev_word = curr_word
    print(prev_word, count)
    
    ```
    
- Then, run these commands
    
    ```bash
    hadoop jar $HADOOP_HOME/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.3.6.jar wordcount /example/input.txt /example/output
    ```
    
    ```bash
    hdfs dfs -cat /example/output/part-r-00000
    ```
    
- Above is to understand the working of MapReduce. After this, follow instructions given here https://pesubigdata2024.super.site/assignments/hands-on-1-cw-hadoop-installation-guide-and-hdfs. Steps are similar.