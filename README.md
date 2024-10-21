# Slowly_Changing_Dimensions (SCD)
>The Slowly Changing Dimensions are a crucial concept in data warehousing, allowing you to manage and store historical data effectively. There are several types of SCDs, each suited for different use cases.


**SCD 0** - There are certain attributes of an entity that can never change like the Birth date, Birth place, etc. These attributes fall under SCD 0 category.

**SCD 1** - In some scenarios, the value of an attribute is overwritten, the previous value is not retained. Such attributes where the history is not recorded, fall under SCD 1 category.
Advantage: It is easy to implement as the data needs to be just updated without having to record the previous value.
Disadvantage: The previous value of the attribute is lost while updating as the values are overwritten without capturing the history.

**SCD 2** - This category maintains the complete history of the data changes. For every data update, a new row will be created. It is complex to implement SCD 2 as it involves addition and updation of multiple rows.

**SCD 3** - This category maintains partial history. In this case, instead of a new row creation for updating the data, a new column is maintained in the same row to capture and the previous values of the updated attribute.
Easy to implement but has limited history, only one previous value is captured as history.

**Note:**
- SCD 1 implementation would be a good fit if the data is not crucial, for which the history is required to be maintained.
- Based on the business requirement the respective SCD implementations can be adopted. It is always a good approach to maintain the complete history of the data as the business requirements can change over time and if the history is not captured, then it will not be possible to share the accurate data for analysis.

# Dataset
- **[customers1.csv](https://github.com/nk3099/Slowly_Changing_Dimensions/blob/main/customers1.csv)** : the original file. 
- **[customers2.csv](https://github.com/nk3099/Slowly_Changing_Dimensions/blob/main/customers2.csv)** : the data getting changed over the time.

\
```Source Location:``` \
dbutils.fs.mkdirs("/FileStore/SCD/source/") \
<img width="542" alt="source" src="https://github.com/user-attachments/assets/7f57b687-1cd6-4967-80a7-0b70f2152f4c">

```Target Location: ``` \
dbutils.fs.mkdirs("/FileStore/SCD/target/") \
<img width="541" alt="target" src="https://github.com/user-attachments/assets/806e634f-d680-47c2-863c-738823ae04fe"> \

# SCD-Type2_Implementation
**The changes in data over the time** (from customers1.csv to customers2.csv):
```
* In 1st row, the Email address updated from email.com to gmail.com
* In 2nd row, we have changed Phone number from "555-5678" to "555-5679"
* In 3rd row, we have updated city,state,zipcode
* Inserted two new records ie. row 11 and row12
* Deleted 10th record, ie. row 10
```
```
-updates(row 1,2,3) 
-insert(row 11,12) 
-delete(row 10) 
-unchanged(all other records)
```

<img width="847" alt="slowly_changed_dimensions" src="https://github.com/user-attachments/assets/25ef5e51-6db1-477b-b4db-ee663edee80d">
