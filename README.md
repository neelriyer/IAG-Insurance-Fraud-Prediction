# IAG Insurance Fraud Prediction
Predicting Insurance fraud using a simulated dataset from Insurance Australia Group.

[Notebook availiable here](DATA3001.ipynb).

# Notebook


```python
log = pd.read_csv('Dataset/data.csv')
log.head(20)
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>message</th>
      <th>timestamp</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>8f70c7577be8483 - mobile_browser - Quote Started for customer: 99ccf1</td>
      <td>1483192800.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1368d40a4f6e455 - mobile_browser - Quote Completed for customer: 99ccf1 with json payload {'name': 'Nicole Berry', 'email': 'Nicole Berry@hotmail.com', 'gender': 'male', 'age': 29, 'home': {'type': 1, 'square_footage': 311.80361967382737, 'number_of_bedrooms': 2, 'number_of_floors': 1}, 'household': [{'name': 'Oscar Berry', 'age': 25, 'gender': 'female'}, {'name': 'Mark Berry', 'age': 10, 'gender': 'female'}, {'name': 'Jacqueline Berry', 'age': 14, 'gender': 'male'}], 'address': '66 Lake Jamieview,PSC '}</td>
      <td>1483193676.51</td>
    </tr>
    <tr>
      <th>2</th>
      <td>90527688b31d445 - mobile_browser - Claim Started for customer: 99ccf1</td>
      <td>1483193794.69</td>
    </tr>
    <tr>
      <th>3</th>
      <td>c4013f44ea6d40c - mobile_browser - Payment Completed for customer: 99ccf1</td>
      <td>1483193794.69</td>
    </tr>
    <tr>
      <th>4</th>
      <td>8045614075e7466 - pc_browser - Quote Started for customer: 9bae09</td>
      <td>1483196400.00</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6859e40fdc3f40d - pc_browser - Quote Completed for customer: 9bae09 with json payload {'name': 'Brandi Harris', 'email': 'Brandi Harris@duncan.com', 'gender': 'male', 'age': 62, 'home': {'type': 1, 'square_footage': 523.4329572865342, 'number_of_bedrooms': 2, 'number_of_floors': 1}, 'household': [{'name': 'Michael Harris', 'age': 12, 'gender': 'male'}, {'name': 'Michael Harris', 'age': 7, 'gender': 'male'}], 'address': '60 West Lisaside, Jamie Port Suite '}</td>
      <td>1483197036.47</td>
    </tr>
    <tr>
      <th>6</th>
      <td>4c9ab2942b484f2 - pc_browser - Claim Started for customer: 9bae09</td>
      <td>1483197184.51</td>
    </tr>
    <tr>
      <th>7</th>
      <td>07ba7defa6444ba - pc_browser - Payment Completed for customer: 9bae09</td>
      <td>1483197184.51</td>
    </tr>
    <tr>
      <th>8</th>
      <td>cb6d5db3f2ce478 - pc_browser - Quote Started for customer: 12fdce</td>
      <td>1483199674.68</td>
    </tr>
    <tr>
      <th>9</th>
      <td>0ddb305e024d49f - pc_browser - Quote Started for customer: b7aab4</td>
      <td>1483200000.00</td>
    </tr>
    <tr>
      <th>10</th>
      <td>be4398c940284fe - pc_browser - Quote Completed for customer: b7aab4 with json payload {'name': 'Christopher Moody', 'email': 'Christopher Moody@green.info', 'gender': 'male', 'age': 40, 'home': {'type': 1, 'square_footage': 221.63326677793447, 'number_of_bedrooms': 3, 'number_of_floors': 1}, 'household': [], 'address': '120 Danielmouth,Unit  Box '}</td>
      <td>1483200799.03</td>
    </tr>
    <tr>
      <th>11</th>
      <td>cf1d5d9af6d54ef - pc_browser - Claim Started for customer: b7aab4</td>
      <td>1483200904.55</td>
    </tr>
    <tr>
      <th>12</th>
      <td>7a1836f6aacf4ec - pc_browser - Payment Completed for customer: b7aab4</td>
      <td>1483200904.55</td>
    </tr>
    <tr>
      <th>13</th>
      <td>697990436eb5484 - pc_browser - Quote Incomplete for customer: 12fdce with json payload {'name': 'Latoya Johnston', 'email': 'Latoya Johnston@peterson.com', 'gender': 'male', 'age': 28, 'home': {'type': 1}, 'household': [], 'address': '136 Jonesberg,Unit  Box '}</td>
      <td>1483203274.68</td>
    </tr>
    <tr>
      <th>14</th>
      <td>e6cd8ce31a1d4d6 - mobile_browser - Claim Denied for customer: 99ccf1 - reason : fraud</td>
      <td>1483203294.05</td>
    </tr>
    <tr>
      <th>15</th>
      <td>f21cd7a34cbc412 - pc_browser - Quote Started for customer: 2bc68b</td>
      <td>1483203600.00</td>
    </tr>
    <tr>
      <th>16</th>
      <td>84618ef8bc28479 - mobile_browser - Claim Started for customer: 983092</td>
      <td>1483203691.28</td>
    </tr>
    <tr>
      <th>17</th>
      <td>e67b69c9b4554c0 - pc_browser - Claim Denied for customer: b7aab4 - reason : fraud</td>
      <td>1483204320.48</td>
    </tr>
    <tr>
      <th>18</th>
      <td>0baaef67fe8a458 - pc_browser - Quote Completed for customer: 2bc68b with json payload {'name': 'Loretta Steele', 'email': 'Loretta Steele@patton-smith.biz', 'gender': 'female', 'age': 48, 'home': {'type': 1, 'square_footage': 301.854949906065, 'number_of_bedrooms': 3, 'number_of_floors': 1}, 'household': [{'name': 'Zachary Steele', 'age': 48, 'gender': 'male'}, {'name': 'Nicholas Steele', 'age': 9, 'gender': 'male'}, {'name': 'Michael Steele', 'age': 12, 'gender': 'female'}], 'address': '73 Edwardfurt, Michelle Crossing Suite '}</td>
      <td>1483204668.62</td>
    </tr>
    <tr>
      <th>19</th>
      <td>a79b052cd8f2480 - pc_browser - Payment Completed for customer: 2bc68b</td>
      <td>1483204804.68</td>
    </tr>
  </tbody>
</table>
</div>




```python
# the log is sorted in icreasing order 
log['timestamp'].is_monotonic 
```




    True



split the message column into multiple columns, transaction_id, action, customer_id, action, message


```python
#%%timeit
start_time = time.time()

# create msgLog for manipulating message data
msgLog = pd.DataFrame()

#msgLog['message'] = log['message']
msgLog['transaction_id'], msgLog['device'], msgLog['message'] = log['message'].str.split('-',2).str
msgLog['action'], msgLog['message'] = msgLog['message'].str.split(':',1).str
msgLog['customer_id'], msgLog['message'] = msgLog['message'].str.split(n=1).str
msgLog['action'] = msgLog['action'].str.strip()

#msgLog['message'] = msgLog['message'].str.split('json payload',1).str[0]
msgLog['message'], msgLog['json_payload'] = msgLog['message'].str.split('json payload',1).str

msgLog['timestamp'] = log['timestamp']
print("%s seconds" %(time.time() - start_time))
```

    65.64751410484314 seconds



```python
msgLog.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>transaction_id</th>
      <th>device</th>
      <th>message</th>
      <th>action</th>
      <th>customer_id</th>
      <th>json_payload</th>
      <th>timestamp</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>8f70c7577be8483</td>
      <td>mobile_browser</td>
      <td>NaN</td>
      <td>Quote Started for customer</td>
      <td>99ccf1</td>
      <td>NaN</td>
      <td>1483192800.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1368d40a4f6e455</td>
      <td>mobile_browser</td>
      <td>with</td>
      <td>Quote Completed for customer</td>
      <td>99ccf1</td>
      <td>{'name': 'Nicole Berry', 'email': 'Nicole Berry@hotmail.com', 'gender': 'male', 'age': 29, 'home': {'type': 1, 'square_footage': 311.80361967382737, 'number_of_bedrooms': 2, 'number_of_floors': 1}, 'household': [{'name': 'Oscar Berry', 'age': 25, 'gender': 'female'}, {'name': 'Mark Berry', 'age': 10, 'gender': 'female'}, {'name': 'Jacqueline Berry', 'age': 14, 'gender': 'male'}], 'address': '66 Lake Jamieview,PSC '}</td>
      <td>1483193676.51</td>
    </tr>
    <tr>
      <th>2</th>
      <td>90527688b31d445</td>
      <td>mobile_browser</td>
      <td>NaN</td>
      <td>Claim Started for customer</td>
      <td>99ccf1</td>
      <td>NaN</td>
      <td>1483193794.69</td>
    </tr>
    <tr>
      <th>3</th>
      <td>c4013f44ea6d40c</td>
      <td>mobile_browser</td>
      <td>NaN</td>
      <td>Payment Completed for customer</td>
      <td>99ccf1</td>
      <td>NaN</td>
      <td>1483193794.69</td>
    </tr>
    <tr>
      <th>4</th>
      <td>8045614075e7466</td>
      <td>pc_browser</td>
      <td>NaN</td>
      <td>Quote Started for customer</td>
      <td>9bae09</td>
      <td>NaN</td>
      <td>1483196400.00</td>
    </tr>
  </tbody>
</table>
</div>



Drop the transaction column cos its fucking useless, can count number of transactions by actions


```python
# all transaction id's are unique, not very useful
# msgLog.transaction_id.value_counts()
msgLog = msgLog.drop(columns=['transaction_id'])
```


```python
# 621123 unique ids, note that some customer ids are repeated
len(msgLog.customer_id.value_counts())
```




    621123



Sort values by customer id (thereby grouping by customer id, but not reducing rows)


```python
msgLog = msgLog.sort_values(by=['customer_id', 'timestamp'], kind = 'mergesort')
msgLog = msgLog.reset_index(drop=True)
```


```python
# add paid dataframe to msgLog
paid = pd.DataFrame()
msgLog['message'], msgLog['paid'] = msgLog['message'].str.split('$').str
msgLog['paid'] = pd.to_numeric(msgLog['paid'])
```


```python
msgLog.message.value_counts()
```




    - paid              816301
    with                632998
    - reason : fraud     10494
    Name: message, dtype: int64




```python
print(np.nanmin(msgLog['paid']), np.nanmax(msgLog['paid']), np.nanmean(msgLog['paid']))
```

    2642.61 27097.44 8710.884242638436



```python
# backup good msgLog
#1*
backupMsgLog = msgLog.copy()
```


```python
msgLog.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>device</th>
      <th>message</th>
      <th>action</th>
      <th>customer_id</th>
      <th>json_payload</th>
      <th>timestamp</th>
      <th>paid</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>mobile_app</td>
      <td>NaN</td>
      <td>Quote Started for customer</td>
      <td>000012</td>
      <td>NaN</td>
      <td>1520515553.72</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>1</th>
      <td>mobile_app</td>
      <td>with</td>
      <td>Quote Completed for customer</td>
      <td>000012</td>
      <td>{'name': 'Kimberly Mathews', 'email': 'Kimberly Mathews@hotmail.com', 'gender': 'male', 'age': 53, 'home': {'type': 1, 'square_footage': 346.20595281589794, 'number_of_bedrooms': 5, 'number_of_floors': 1}, 'household': [{'name': 'Kristen Mathews', 'age': 14, 'gender': 'female'}, {'name': 'Randy Mathews', 'age': 9, 'gender': 'male'}], 'address': '16 Reidville, Richard Pine Suite '}</td>
      <td>1520516303.52</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>2</th>
      <td>mobile_app</td>
      <td>NaN</td>
      <td>Quote Started for customer</td>
      <td>000023</td>
      <td>NaN</td>
      <td>1496195647.93</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>3</th>
      <td>mobile_app</td>
      <td>with</td>
      <td>Quote Completed for customer</td>
      <td>000023</td>
      <td>{'name': 'James Terrell', 'email': 'James Terrell@ryan-alvarado.com', 'gender': 'male', 'age': 30, 'home': {'type': 1, 'square_footage': 404.2134657047327, 'number_of_bedrooms': 2, 'number_of_floors': 1}, 'household': [], 'address': '114 Lake Matthewmouth,PSC '}</td>
      <td>1496196488.27</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>4</th>
      <td>phone_call</td>
      <td>NaN</td>
      <td>Quote Started for customer</td>
      <td>00003a</td>
      <td>NaN</td>
      <td>1496494950.52</td>
      <td>nan</td>
    </tr>
  </tbody>
</table>
</div>



[See full code here](DATA3001.ipynb).
