```python
# import required library
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```


```python
# load dataset from local file
data = pd.read_csv('C:/Users/denis/PycharmProjects/scientificProject/data/supermarket_sales.csv')
```


```python
data.info() # check data type
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1000 entries, 0 to 999
    Data columns (total 17 columns):
     #   Column                   Non-Null Count  Dtype  
    ---  ------                   --------------  -----  
     0   Invoice ID               1000 non-null   object 
     1   Branch                   1000 non-null   object 
     2   City                     1000 non-null   object 
     3   Customer type            1000 non-null   object 
     4   Gender                   1000 non-null   object 
     5   Product line             1000 non-null   object 
     6   Unit price               1000 non-null   float64
     7   Quantity                 1000 non-null   int64  
     8   Tax 5%                   1000 non-null   float64
     9   Total                    1000 non-null   float64
     10  Date                     1000 non-null   object 
     11  Time                     1000 non-null   object 
     12  Payment                  1000 non-null   object 
     13  cogs                     1000 non-null   float64
     14  gross margin percentage  1000 non-null   float64
     15  gross income             1000 non-null   float64
     16  Rating                   1000 non-null   float64
    dtypes: float64(7), int64(1), object(9)
    memory usage: 132.9+ KB
    


```python
data.head(5) # check first 5 rows
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
      <th>Invoice ID</th>
      <th>Branch</th>
      <th>City</th>
      <th>Customer type</th>
      <th>Gender</th>
      <th>Product line</th>
      <th>Unit price</th>
      <th>Quantity</th>
      <th>Tax 5%</th>
      <th>Total</th>
      <th>Date</th>
      <th>Time</th>
      <th>Payment</th>
      <th>cogs</th>
      <th>gross margin percentage</th>
      <th>gross income</th>
      <th>Rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>750-67-8428</td>
      <td>A</td>
      <td>Yangon</td>
      <td>Member</td>
      <td>Female</td>
      <td>Health and beauty</td>
      <td>74.69</td>
      <td>7</td>
      <td>26.1415</td>
      <td>548.9715</td>
      <td>1/5/2019</td>
      <td>13:08</td>
      <td>Ewallet</td>
      <td>522.83</td>
      <td>4.761905</td>
      <td>26.1415</td>
      <td>9.1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>226-31-3081</td>
      <td>C</td>
      <td>Naypyitaw</td>
      <td>Normal</td>
      <td>Female</td>
      <td>Electronic accessories</td>
      <td>15.28</td>
      <td>5</td>
      <td>3.8200</td>
      <td>80.2200</td>
      <td>3/8/2019</td>
      <td>10:29</td>
      <td>Cash</td>
      <td>76.40</td>
      <td>4.761905</td>
      <td>3.8200</td>
      <td>9.6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>631-41-3108</td>
      <td>A</td>
      <td>Yangon</td>
      <td>Normal</td>
      <td>Male</td>
      <td>Home and lifestyle</td>
      <td>46.33</td>
      <td>7</td>
      <td>16.2155</td>
      <td>340.5255</td>
      <td>3/3/2019</td>
      <td>13:23</td>
      <td>Credit card</td>
      <td>324.31</td>
      <td>4.761905</td>
      <td>16.2155</td>
      <td>7.4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>123-19-1176</td>
      <td>A</td>
      <td>Yangon</td>
      <td>Member</td>
      <td>Male</td>
      <td>Health and beauty</td>
      <td>58.22</td>
      <td>8</td>
      <td>23.2880</td>
      <td>489.0480</td>
      <td>1/27/2019</td>
      <td>20:33</td>
      <td>Ewallet</td>
      <td>465.76</td>
      <td>4.761905</td>
      <td>23.2880</td>
      <td>8.4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>373-73-7910</td>
      <td>A</td>
      <td>Yangon</td>
      <td>Normal</td>
      <td>Male</td>
      <td>Sports and travel</td>
      <td>86.31</td>
      <td>7</td>
      <td>30.2085</td>
      <td>634.3785</td>
      <td>2/8/2019</td>
      <td>10:37</td>
      <td>Ewallet</td>
      <td>604.17</td>
      <td>4.761905</td>
      <td>30.2085</td>
      <td>5.3</td>
    </tr>
  </tbody>
</table>
</div>




```python
# check missing value
print("Check missing value: \n")
print(data.isnull().sum())
```

    Check missing value: 
    
    Invoice ID                 0
    Branch                     0
    City                       0
    Customer type              0
    Gender                     0
    Product line               0
    Unit price                 0
    Quantity                   0
    Tax 5%                     0
    Total                      0
    Date                       0
    Time                       0
    Payment                    0
    cogs                       0
    gross margin percentage    0
    gross income               0
    Rating                     0
    dtype: int64
    

Taking into consideration that there are no missing values, we can move on to the next step.




```python
# check duplicate value
print("Check duplicate value")
print(data.duplicated().value_counts())
```

    Check duplicate value
    False    1000
    Name: count, dtype: int64
    

Taking into consideration that there are no duplicate values, we can move on to the next step.


```python
# check outlier
print("Check outlier")
print(data.describe())
```

    Check outlier
            Unit price     Quantity       Tax 5%        Total        cogs  \
    count  1000.000000  1000.000000  1000.000000  1000.000000  1000.00000   
    mean     55.672130     5.510000    15.379369   322.966749   307.58738   
    std      26.494628     2.923431    11.708825   245.885335   234.17651   
    min      10.080000     1.000000     0.508500    10.678500    10.17000   
    25%      32.875000     3.000000     5.924875   124.422375   118.49750   
    50%      55.230000     5.000000    12.088000   253.848000   241.76000   
    75%      77.935000     8.000000    22.445250   471.350250   448.90500   
    max      99.960000    10.000000    49.650000  1042.650000   993.00000   
    
           gross margin percentage  gross income      Rating  
    count              1000.000000   1000.000000  1000.00000  
    mean                  4.761905     15.379369     6.97270  
    std                   0.000000     11.708825     1.71858  
    min                   4.761905      0.508500     4.00000  
    25%                   4.761905      5.924875     5.50000  
    50%                   4.761905     12.088000     7.00000  
    75%                   4.761905     22.445250     8.50000  
    max                   4.761905     49.650000    10.00000  
    

Finding average customer rating


```python
print("Average customer rating: ", data['Rating'].mean())
```

    Average customer rating:  6.9727
    

Finding gender counts


```python
print("Gender counts: ")
gender_counts = data['Gender'].value_counts()
print(gender_counts)
```

    Gender counts: 
    Gender
    Female    501
    Male      499
    Name: count, dtype: int64
    

Plotting the bar chart for gender distribution in the dataset.


```python
sns.countplot(x='Gender', data=data, palette='hls', hue='Gender')
plt.title('Gender distribution in the Supermarket Dataset')
plt.xlabel('Gender')
plt.ylabel('Number of customers')
for index, value in enumerate(gender_counts):
    plt.text(index, value, str(value), ha='center', va='bottom')
plt.show()
```


    
![png](output_15_0.png)
    


We observe that there are more female than male customers in the dataset, but not much difference between them.
We can move on to the next step.

Start determining customer distribution by city in dataset. Also plotting that in pie chart.


```python
city_counts = data['City'].value_counts()
print("City counts: ", city_counts)

palette = sns.color_palette("husl", len(city_counts))
plt.figure(figsize=(8, 6), dpi=100)
plt.pie(city_counts, labels=city_counts.index, autopct='%1.1f%%', colors=palette)
plt.title('Customer distribution by City')
plt.show()
```

    City counts:  City
    Yangon       340
    Mandalay     332
    Naypyitaw    328
    Name: count, dtype: int64
    


    
![png](output_18_1.png)
    


Analyzing total sales by city, and plotting them in bar chart


```python
city_sales = data.groupby('City')['Total'].sum()
print("Total sales by city: ", city_sales)

plt.figure(figsize=(8, 6), dpi=100)
plt.bar(city_sales.index, city_sales.values, color=palette)
plt.title('Total sales by city')
plt.xlabel('City')
plt.ylabel('Total sales')

for index, value in enumerate(city_sales):
    plt.text(index, value, str(round(value, 2)), ha='center', va='bottom')
plt.show()
```

    Total sales by city:  City
    Mandalay     106197.6720
    Naypyitaw    110568.7065
    Yangon       106200.3705
    Name: Total, dtype: float64
    


    
![png](output_20_1.png)
    


Relation between sales and product category! Determining product category distribution in dataset


```python
# product line count
product_line_counts = data['Product line'].value_counts()
print("Product line counts: ", product_line_counts)

# product sales distribution
plt.figure(figsize=(25, 8), dpi=100)
plt.bar(product_line_counts.index, product_line_counts.values, color=palette)
plt.title('Product sales distribution')
plt.xlabel('Product Category')
plt.ylabel('Number of Products')
for index, value in enumerate(product_line_counts):
    plt.text(index, value, str(value), ha='center', va='bottom')
plt.show()
```

    Product line counts:  Product line
    Fashion accessories       178
    Food and beverages        174
    Electronic accessories    170
    Sports and travel         166
    Home and lifestyle        160
    Health and beauty         152
    Name: count, dtype: int64
    


    
![png](output_22_1.png)
    


Due to the biggest sales in the "Fashion accessories" category, we start analyzing the relation between gender and product category.


```python
# Group data by Product line and Gender and sum up Total sales
product_line_gender_sales = data.groupby(['Product line', 'Gender'])['Total'].sum().unstack()

# Plot the relationship between sales, gender, and product line
plt.figure(figsize=(12, 8))
product_line_gender_sales.plot(kind='bar', stacked=False, colormap='viridis', ax=plt.gca())
plt.title('Relationship between Sales, Gender, and Product Line')
plt.xlabel('Product Line')
plt.ylabel('Total Sales')
plt.xticks(rotation=45)
plt.legend(title='Gender', bbox_to_anchor=(1.05, 1), loc='upper left')
plt.show()

```


    
![png](output_24_0.png)
    


We can see than male customers have higher sales than female customers in the "Health and beauty" category. In rest of category's female customers have higher sales than male customers. Minimal difference between male and female customers in the "Electronic accessories" category. We can move on to the next step.

Determining customer profile based on membership status grouping by city


```python
customer_type_counts = data['Customer type'].value_counts()
print("Customer type counts: ", customer_type_counts)

# plotting customer type distribution by city
plt.figure(figsize=(10, 6), dpi=100)
sns.countplot(x='City', hue='Customer type', data=data, palette='hls')
plt.title('Customer type distribution by city')
plt.xlabel('City')
plt.ylabel('Number of customers')
plt.legend(title='Customer type', labels=['Casual', 'Member'], loc='lower right')
plt.show()
```

    Customer type counts:  Customer type
    Member    501
    Normal    499
    Name: count, dtype: int64
    


    
![png](output_27_1.png)
    


In city "Naypyitaw" there are lower member customers than casual customers. Branches in this city have more casual customers and need improve their sales of membership. 
We can move on to the next step.

Interesting to determine the busiest time in market


```python
data['Hour'] = pd.to_datetime(data['Time'], format='%H:%M').dt.hour
holidays_transactions = data.groupby('Hour').size()

all_hours = pd.RangeIndex(start=0, stop=24)
full_day_hourly_transactions = holidays_transactions.reindex(all_hours).fillna(0)
palette = sns.color_palette("bright", 12)

plt.figure(figsize=(12, 7), dpi=100)
plt.bar(full_day_hourly_transactions.index, full_day_hourly_transactions.values, color=palette)
plt.title('Customer Activity by Hour')
plt.xlabel('Hour of the day')
plt.ylabel('Number of Transactions')
for index, value in enumerate(full_day_hourly_transactions):
    plt.text(index, value, str(value), ha='center', va='bottom')
plt.show()
```


    
![png](output_30_0.png)
    


Distribution of busiest time in market is irregular, due to high number of transactions in the 10, 13, 15,18,19 hours. We can move on to the next step. Highest number of transactions are in  19:00-20:00 hour.
Moving on to the next step

Payment method distribution


```python
# Group data by City and Payment and count the number of transactions
payment_types_by_city = data.groupby(['City', 'Payment']).size().unstack(fill_value=0)

# Get the number of cities and set bar width and index for plotting
num_cities = len(payment_types_by_city.index)
bar_width = 0.25
index = np.arange(num_cities)

# Plotting the distribution of payment types by city
plt.figure(figsize=(15, 7), dpi=100)
for i, payment_method in enumerate(payment_types_by_city.columns):
    plt.bar(index + bar_width * i, payment_types_by_city[payment_method], bar_width, label=payment_method)

plt.xlabel('City', fontsize=12)
plt.ylabel('Number of Transactions', fontsize=12)
plt.xticks(index + bar_width, payment_types_by_city.index, fontsize=12, rotation=45)
plt.yticks(fontsize=12)
plt.legend(fontsize=12, loc='lower right')
plt.grid(axis='y', linestyle='--')

# Add text annotations to each bar
for i, payment_method in enumerate(payment_types_by_city.columns):
    for j, value in enumerate(payment_types_by_city[payment_method]):
        plt.text(j + i * bar_width, value, str(value), ha='center', fontsize=10, verticalalignment='bottom')

plt.tight_layout()
plt.show()

```


    
![png](output_33_0.png)
    


Also, we can see that the number of transactions with cash in Naypyitaw is higher than other cities. We can move on to the next step for determining sales distribution by payment type group by city.


```python
# Group data by City and Payment, summing up Total sales
sales_by_city_payment = data.groupby(['City', 'Payment'])['Total'].sum().unstack(fill_value=0)

# Get the number of cities and set bar width and index for plotting
num_cities = len(sales_by_city_payment.index)
bar_width = 0.25
index = np.arange(num_cities)

# Plotting the distribution of sales by payment type and city
plt.figure(figsize=(15, 7), dpi=100)
for i, payment_method in enumerate(sales_by_city_payment.columns):
    plt.bar(index + bar_width * i, sales_by_city_payment[payment_method], bar_width, label=payment_method)

plt.xlabel('City', fontsize=12)
plt.ylabel('Total Sales', fontsize=12)
plt.xticks(index + bar_width, sales_by_city_payment.index, fontsize=12, rotation=45)
plt.yticks(fontsize=12)
plt.legend(fontsize=12, loc='upper right')
plt.grid(axis='y', linestyle='--')

# Add text annotations to each bar
for i, payment_method in enumerate(sales_by_city_payment.columns):
    for j, value in enumerate(sales_by_city_payment[payment_method]):
        plt.text(j + i * bar_width, value, str(round(value, 2)), ha='center', fontsize=10, verticalalignment='bottom')

plt.tight_layout()
plt.show()

```


    
![png](output_35_0.png)
    


As next step we will determine mean payment for one transaction by city. 


```python
# Calculate the mean payment for one transaction by city
mean_payment_by_city = data.groupby('City')['Total'].mean()

# Plot the mean payment for one transaction by city
plt.figure(figsize=(10, 6))
mean_payment_by_city.plot(kind='bar', color=palette)
plt.title('Mean Payment for One Transaction by City')
plt.xlabel('City')
plt.ylabel('Mean Payment')
plt.xticks(rotation=45)
plt.grid(axis='y', linestyle='--')
plt.show()

```


    
![png](output_37_0.png)
    


As next step we will determine city wise gross income (income before deduction). 


```python
gross_income_total = data.groupby('City')['gross income'].sum()

total_gross_income = gross_income_total.sum()

plt.figure(figsize=(8, 6), dpi=100)
bars = plt.bar(gross_income_total.index, gross_income_total.values, color=palette)

for bar in bars:
    height = bar.get_height()
    plt.text(bar.get_x() + bar.get_width() / 2, height, f'{height:.2f}', ha='center', va='bottom')

plt.title('Branch wise gross income distribution (Total Income:' + f' {total_gross_income:.2f})')
plt.xlabel('City')
plt.ylabel('Total Gross Income (Before Tax)')
plt.xticks(rotation=0)
plt.show()


print("gross margin percentage analysis: ")
print("min gross margin percentage: ", data['gross margin percentage'].min())
print("max gross margin percentage: ", data['gross margin percentage'].max())
print("average gross margin percentage: ", data['gross margin percentage'].mean())

```


    
![png](output_39_0.png)
    


    gross margin percentage analysis: 
    min gross margin percentage:  4.761904762
    max gross margin percentage:  4.761904762
    average gross margin percentage:  4.761904762
    

Distributions of product line sales in every branch.


```python
product_line_sales = data.groupby(['Branch', 'Product line'])['Total'].sum().unstack()
total_sales_per_product_line = product_line_sales.sum()
sorted_columns = total_sales_per_product_line.sort_values(ascending=False).index
product_line_sales_sorted = product_line_sales[sorted_columns]

# Separate plots for each branch
for branch in ['A', 'B', 'C']:
    ax = product_line_sales_sorted.loc[[branch]].plot(kind='barh', figsize=(25, 10), legend=True, colormap='viridis')
    ax.set_title(f'Sales by Product Line in Branch {branch}', fontsize=20)
    ax.set_xlabel('Sales', fontsize=20)
    ax.set_ylabel('Branch', fontsize=20)
    ax.tick_params(axis='y', labelsize=20)
    ax.tick_params(axis='x', labelsize=20)

    # Adding annotations next to each bar for better visibility
    for p in ax.patches:
        ax.annotate(f'{p.get_width():,.2f}', (p.get_width(), p.get_y() + p.get_height() / 2.),
                    ha='left', va='center', fontsize=14, color='black', xytext=(5, 0), textcoords='offset points')

    plt.tight_layout()
    plt.show()
```


    
![png](output_41_0.png)
    



    
![png](output_41_1.png)
    



    
![png](output_41_2.png)
    

