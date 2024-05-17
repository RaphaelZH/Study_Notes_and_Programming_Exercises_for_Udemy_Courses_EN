#

## Flowchart for Jupyter Notebook File Compression and Status Logging

```mermaid
flowchart TB
    A(Start)
    B{Condition 1}
    C[Statement 1]
    D(Stop)

    X[[cleanup]]

    subgraph LOOP_1[Loop 1]
        LOOP_1_A[Loop Entry]
        LOOP_1_B{Loop Condition}
        LOOP_1_C{Condition 2}
        LOOP_1_D[Statement 2]
        LOOP_1_E[Loop Exit]

        LOOP_1_A ~~~ LOOP_1_B ~~~ LOOP_1_C ~~~ LOOP_1_D
        LOOP_1_C ~~~ LOOP_1_E

        direction LR
            LOOP_1_A --> LOOP_1_B -- True --> LOOP_1_C -- True --> LOOP_1_D --> LOOP_1_B
            LOOP_1_C -- False --> LOOP_1_B -- False --> LOOP_1_E
    end

    subgraph LOOP_2[Loop 2]
        LOOP_2_A[Loop Entry]
        LOOP_2_B{Loop Condition}
        LOOP_2_C{Condition 3}
        LOOP_2_D[Statement 3]
        LOOP_2_E{Condition 4}
        LOOP_2_F[Statement 4]
        LOOP_2_G[Statement 5]
        LOOP_2_H[Loop Exit]

        LOOP_2_A ~~~ LOOP_2_B ~~~ LOOP_2_C ~~~ LOOP_2_D ~~~ LOOP_2_E ~~~ LOOP_2_F ~~~ LOOP_2_G
        LOOP_2_F ~~~ LOOP_2_H

        direction LR
            LOOP_2_A --> LOOP_2_B -- True --> LOOP_2_C -- True --> LOOP_2_D --> LOOP_2_G --> LOOP_2_B
            LOOP_2_C -- False--> LOOP_2_E -- True --> LOOP_2_F --> LOOP_2_G
            LOOP_2_E -- False --> LOOP_2_B -- False --> LOOP_2_H
    end
    
    A ==> B == True ==> LOOP_1 ==> LOOP_2 ==> D
    B == False ==> C ==> D

    C ~~~ X
    X -.-> C
    X -.-> LOOP_1
```

> Condition 1: Check whether there exists a record for all Jupyter Notebook files in the current directory.
>
> Statement 1: If Condition 1 is False, create a record for all Jupyter Notebook files in the current directory immediately, while generating the corresponding pre-compressed copy for each file as well as compressing any copies that exceed the preset size limit, and recording relevant information about the copies.
>
> Condition 2: If Condition 1 is True, read this record and check whether there are certain entries in this record for which the corresponding Jupyter Notebook file cannot be found.
>
> Statement 2: If Condition 2 is True, delete these entries and eventually reset the index.
>
> Condition 3: Regardless of whether Condition 2 is True or False, check whether there are any Jupyter Notebook files in the current directory that do not have a corresponding entry in this record.
>
> Statement 3: If condition 3 is True, the information relating to the file will be added to the record as the most recent entry, and its corresponding indexes will be recorded separately in a list of indexes dedicated to recording altered or newly added entries.
>
> Condition 4: If condition 3 is False, check whether the actual modification date of the file is the same as the modification date recorded for the corresponding entry in the record.
>
> Statement 4: If condition 4 is True, update the modification date information and size information of the file to the corresponding entry in the record, and likewise record its corresponding index in the list of indexes dedicated to recording altered or newly added entries.
>
> Statement 5: Generates corresponding pre-compressed copies of the files corresponding to the entries in the records that correspond to all of the indexes in the list of indexes, compresses any copies that exceed the preset size limit, while recording information related to the corresponding copies.
>
> Statement 6: Sorts the updated record and resets its index.
