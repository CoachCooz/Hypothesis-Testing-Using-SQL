
# Mod 3 Final Project

## Student Info

- Name: Acusio Bivona
- Cohort: Part-Time Online 10/07/19
- Instructor: James Irving




<img src="https://raw.githubusercontent.com/jirvingphd/dsc-mod-3-project-online-ds-ft-100719/master/Northwind_ERD_updated.png">


```python
!pip install -U fsds_100719
from fsds_100719.imports import *
```

    fsds_1007219  v0.7.16 loaded.  Read the docs: https://fsds.readthedocs.io/en/latest/ 



<style  type="text/css" >
</style><table id="T_b8e2d052_63dd_11ea_8104_a683e7b2e65e" ><caption>Loaded Packages and Handles</caption><thead>    <tr>        <th class="col_heading level0 col0" >Handle</th>        <th class="col_heading level0 col1" >Package</th>        <th class="col_heading level0 col2" >Description</th>    </tr></thead><tbody>
                <tr>
                                <td id="T_b8e2d052_63dd_11ea_8104_a683e7b2e65erow0_col0" class="data row0 col0" >dp</td>
                        <td id="T_b8e2d052_63dd_11ea_8104_a683e7b2e65erow0_col1" class="data row0 col1" >IPython.display</td>
                        <td id="T_b8e2d052_63dd_11ea_8104_a683e7b2e65erow0_col2" class="data row0 col2" >Display modules with helpful display and clearing commands.</td>
            </tr>
            <tr>
                                <td id="T_b8e2d052_63dd_11ea_8104_a683e7b2e65erow1_col0" class="data row1 col0" >fs</td>
                        <td id="T_b8e2d052_63dd_11ea_8104_a683e7b2e65erow1_col1" class="data row1 col1" >fsds_100719</td>
                        <td id="T_b8e2d052_63dd_11ea_8104_a683e7b2e65erow1_col2" class="data row1 col2" >Custom data science bootcamp student package</td>
            </tr>
            <tr>
                                <td id="T_b8e2d052_63dd_11ea_8104_a683e7b2e65erow2_col0" class="data row2 col0" >mpl</td>
                        <td id="T_b8e2d052_63dd_11ea_8104_a683e7b2e65erow2_col1" class="data row2 col1" >matplotlib</td>
                        <td id="T_b8e2d052_63dd_11ea_8104_a683e7b2e65erow2_col2" class="data row2 col2" >Matplotlib's base OOP module with formatting artists</td>
            </tr>
            <tr>
                                <td id="T_b8e2d052_63dd_11ea_8104_a683e7b2e65erow3_col0" class="data row3 col0" >plt</td>
                        <td id="T_b8e2d052_63dd_11ea_8104_a683e7b2e65erow3_col1" class="data row3 col1" >matplotlib.pyplot</td>
                        <td id="T_b8e2d052_63dd_11ea_8104_a683e7b2e65erow3_col2" class="data row3 col2" >Matplotlib's matlab-like plotting module</td>
            </tr>
            <tr>
                                <td id="T_b8e2d052_63dd_11ea_8104_a683e7b2e65erow4_col0" class="data row4 col0" >np</td>
                        <td id="T_b8e2d052_63dd_11ea_8104_a683e7b2e65erow4_col1" class="data row4 col1" >numpy</td>
                        <td id="T_b8e2d052_63dd_11ea_8104_a683e7b2e65erow4_col2" class="data row4 col2" >scientific computing with Python</td>
            </tr>
            <tr>
                                <td id="T_b8e2d052_63dd_11ea_8104_a683e7b2e65erow5_col0" class="data row5 col0" >pd</td>
                        <td id="T_b8e2d052_63dd_11ea_8104_a683e7b2e65erow5_col1" class="data row5 col1" >pandas</td>
                        <td id="T_b8e2d052_63dd_11ea_8104_a683e7b2e65erow5_col2" class="data row5 col2" >High performance data structures and tools</td>
            </tr>
            <tr>
                                <td id="T_b8e2d052_63dd_11ea_8104_a683e7b2e65erow6_col0" class="data row6 col0" >sns</td>
                        <td id="T_b8e2d052_63dd_11ea_8104_a683e7b2e65erow6_col1" class="data row6 col1" >seaborn</td>
                        <td id="T_b8e2d052_63dd_11ea_8104_a683e7b2e65erow6_col2" class="data row6 col2" >High-level data visualization library based on matplotlib</td>
            </tr>
    </tbody></table>



        <script type="text/javascript">
        window.PlotlyConfig = {MathJaxConfig: 'local'};
        if (window.MathJax) {MathJax.Hub.Config({SVG: {font: "STIX-Web"}});}
        if (typeof require !== 'undefined') {
        require.undef("plotly");
        requirejs.config({
            paths: {
                'plotly': ['https://cdn.plot.ly/plotly-latest.min']
            }
        });
        require(['plotly'], function(Plotly) {
            window._Plotly = Plotly;
        });
        }
        </script>
        


    [i] Pandas .iplot() method activated.



```python
from functions import Cohen_d, find_outliers_IQR,find_outliers_Z

## Uncomment the line below to see the source code for the imported functions
##fs.ihelp(Cohen_d,False),fs.ihelp(find_outliers_IQR,False), fs.ihelp(find_outliers_Z,False)
```


```python
import sqlite3
connect = sqlite3.connect('Northwind_small.sqlite')
cur = connect.cursor()
```


```python
cur.execute("""SELECT name FROM sqlite_master WHERE type='table';""")
df_tables = pd.DataFrame(cur.fetchall(), columns=['Table'])
df_tables
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
      <th>Table</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Employee</td>
    </tr>
    <tr>
      <td>1</td>
      <td>Category</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Customer</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Shipper</td>
    </tr>
    <tr>
      <td>4</td>
      <td>Supplier</td>
    </tr>
    <tr>
      <td>5</td>
      <td>Order</td>
    </tr>
    <tr>
      <td>6</td>
      <td>Product</td>
    </tr>
    <tr>
      <td>7</td>
      <td>OrderDetail</td>
    </tr>
    <tr>
      <td>8</td>
      <td>CustomerCustomerDemo</td>
    </tr>
    <tr>
      <td>9</td>
      <td>CustomerDemographic</td>
    </tr>
    <tr>
      <td>10</td>
      <td>Region</td>
    </tr>
    <tr>
      <td>11</td>
      <td>Territory</td>
    </tr>
    <tr>
      <td>12</td>
      <td>EmployeeTerritory</td>
    </tr>
  </tbody>
</table>
</div>



# HYPOTHESIS 1

> ***Does discount amount have a statistically significant effect on the quantity of a product in an order? If so, at what level(s) of discount?***

- $H_0$: Discounts will not produce a statistically significant effect on the quantity of products sold.
- $H_1$: Including a discount on products will create a statistically significant effect on the quantity of those products sold.

## Create DataFrame


```python
cur.execute("""SELECT * 
            FROM OrderDetail;""")
df_od = pd.DataFrame(cur.fetchall(), columns = [x[0] for x in cur.description])
df_od.head()
#Use dictionaries & GroupBy Statements
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
      <th>Id</th>
      <th>OrderId</th>
      <th>ProductId</th>
      <th>UnitPrice</th>
      <th>Quantity</th>
      <th>Discount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>10248/11</td>
      <td>10248</td>
      <td>11</td>
      <td>14.0</td>
      <td>12</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>10248/42</td>
      <td>10248</td>
      <td>42</td>
      <td>9.8</td>
      <td>10</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>2</td>
      <td>10248/72</td>
      <td>10248</td>
      <td>72</td>
      <td>34.8</td>
      <td>5</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>3</td>
      <td>10249/14</td>
      <td>10249</td>
      <td>14</td>
      <td>18.6</td>
      <td>9</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>4</td>
      <td>10249/51</td>
      <td>10249</td>
      <td>51</td>
      <td>42.4</td>
      <td>40</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>



## Create Dictionaries for Each Discount Offered


```python
data = {}
for discount in df_od['Discount'].unique():
    print(discount)
    data[discount] = df_od.groupby('Discount').get_group(discount)['Quantity']
    
data
```

    0.0
    0.15
    0.05
    0.2
    0.25
    0.1
    0.02
    0.03
    0.04
    0.06
    0.01





    {0.0: 0       12
     1       10
     2        5
     3        9
     4       40
             ..
     2147     2
     2148     2
     2151     1
     2153     4
     2154     2
     Name: Quantity, Length: 1317, dtype: int64, 0.15: 6       35
     7       15
     17      15
     18      21
     48      25
             ..
     2112    20
     2113    30
     2124    10
     2125    30
     2126     2
     Name: Quantity, Length: 157, dtype: int64, 0.05: 8        6
     9       15
     11      40
     12      25
     51      12
             ..
     2116    10
     2123    14
     2134     1
     2137     2
     2144     2
     Name: Quantity, Length: 185, dtype: int64, 0.2: 29      50
     30      65
     31       6
     40      12
     99      45
             ..
     2069    35
     2071    25
     2091    10
     2092    12
     2130    24
     Name: Quantity, Length: 161, dtype: int64, 0.25: 34      16
     36      15
     37      21
     43      60
     45      60
             ..
     2101     4
     2102    20
     2127    20
     2128    20
     2129    10
     Name: Quantity, Length: 154, dtype: int64, 0.1: 107     10
     108      3
     115     20
     116     24
     117      2
             ..
     2095    30
     2096    77
     2098    25
     2099     4
     2135     2
     Name: Quantity, Length: 173, dtype: int64, 0.02: 2133    1
     2146    3
     Name: Quantity, dtype: int64, 0.03: 2139    1
     2140    2
     2150    2
     Name: Quantity, dtype: int64, 0.04: 2141    1
     Name: Quantity, dtype: int64, 0.06: 2149    2
     Name: Quantity, dtype: int64, 0.01: 2152    2
     Name: Quantity, dtype: int64}



## Outlier Removal & Normality Test


```python
#Outlier Removal
#Can run normality test & equal variance test (if applicable)
from scipy import stats
clean_data = {}
for k, v in data.items():
    
    idx_outs = find_outliers_Z(v)
    dat_clean = v[~idx_outs].copy()
    if len(dat_clean) < 4:
        print(f"{k} only has {len(dat_clean)} rows. Removing group from dataset.")
    else: 
        stat, p = stats.shapiro(dat_clean)
        print(f"For {k} normal test, p = {round(p, 4)}, n = {len(dat_clean)}")
        clean_data[k] = dat_clean
```

    For 0.0 normal test, p = 0.0, n = 1297
    For 0.15 normal test, p = 0.0, n = 155
    For 0.05 normal test, p = 0.0, n = 182
    For 0.2 normal test, p = 0.0, n = 159
    For 0.25 normal test, p = 0.0, n = 151
    For 0.1 normal test, p = 0.0, n = 170
    0.02 only has 2 rows. Removing group from dataset.
    0.03 only has 3 rows. Removing group from dataset.
    0.04 only has 1 rows. Removing group from dataset.
    0.06 only has 1 rows. Removing group from dataset.
    0.01 only has 1 rows. Removing group from dataset.


    /Users/acusiobivona/opt/anaconda3/envs/learn-env/lib/python3.6/site-packages/scipy/stats/stats.py:2315: RuntimeWarning:
    
    invalid value encountered in true_divide
    


### After running the normality test, it is evident the data is not normally distributed in each group. However, due to the large sample sizes in each group, we can safely ignore this assumption and move forward into the equal variance test.

## Equal Variance Test


```python
empty_list = []
for k,v in clean_data.items():
    empty_list.append(v)
```


```python
stats.levene(*empty_list)
```




    LeveneResult(statistic=4.7429850894071715, pvalue=0.0002591859866634427)



### After running the test, we can conclude that this data does not have equal variance. Given this result along with the number of sample groups (6 groups), we will have to run a non-parametric ANOVA hypothesis test.

## Hypothesis Test - Non-Parametric ANOVA (Alpha = 0.05)


```python
stats.kruskal(*empty_list)
```




    KruskalResult(statistic=53.65085902244109, pvalue=2.472284921686678e-10)



### After running the hypothesis test, a very small (and thus signficant) p-value was recorded. Therefore, we can confidently reject the null hypothesis and perform a Tukey's Comparison test to see which groups are different.

## Tukey's Comparison Test


```python
def prep_data_for_tukeys(data):
    """Accepts a dictionary with group names as the keys 
    and pandas series as the values. 
    
    Returns a dataframe ready for tukeys test:
    - with a 'data' column and a 'group' column for sms.stats.multicomp.pairwise_tukeyhsd 
    
    Example Use:
    df_tukey = prep_data_for_tukeys(grp_data)
    tukey = sms.stats.multicomp.pairwise_tukeyhsd(df_tukey['data'], df_tukey['group'])
    tukey.summary()
    """
    df_tukey = pd.DataFrame(columns=['data','group'])
    for k,v in  data.items():
        grp_df = v.rename('data').to_frame() 
        grp_df['group'] = k
        df_tukey=pd.concat([df_tukey, grp_df],axis=0)
        
    df_tukey['group'] = df_tukey['group'].astype('str')
    df_tukey['data'] = df_tukey['data'].astype('float')
    return df_tukey
```


```python
best_data_ever = prep_data_for_tukeys(clean_data)
best_data_ever
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
      <th>data</th>
      <th>group</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>12.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>10.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>2</td>
      <td>5.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>3</td>
      <td>9.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>4</td>
      <td>40.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>2095</td>
      <td>30.0</td>
      <td>0.1</td>
    </tr>
    <tr>
      <td>2096</td>
      <td>77.0</td>
      <td>0.1</td>
    </tr>
    <tr>
      <td>2098</td>
      <td>25.0</td>
      <td>0.1</td>
    </tr>
    <tr>
      <td>2099</td>
      <td>4.0</td>
      <td>0.1</td>
    </tr>
    <tr>
      <td>2135</td>
      <td>2.0</td>
      <td>0.1</td>
    </tr>
  </tbody>
</table>
<p>2114 rows × 2 columns</p>
</div>




```python
from statsmodels.stats.multicomp import pairwise_tukeyhsd
print(pairwise_tukeyhsd(best_data_ever['data'].values, best_data_ever['group'].values))
```

    Multiple Comparison of Means - Tukey HSD, FWER=0.05 
    ====================================================
    group1 group2 meandiff p-adj   lower   upper  reject
    ----------------------------------------------------
       0.0   0.05   6.0639  0.001  2.4368   9.691   True
       0.0    0.1   2.9654 0.2098 -0.7723  6.7031  False
       0.0   0.15   6.9176  0.001  3.0233 10.8119   True
       0.0    0.2   5.6293  0.001  1.7791  9.4796   True
       0.0   0.25   6.1416  0.001  2.2016 10.0817   True
      0.05    0.1  -3.0985 0.4621 -7.9861   1.789  False
      0.05   0.15   0.8537    0.9 -4.1547   5.862  False
      0.05    0.2  -0.4346    0.9 -5.4088  4.5396  False
      0.05   0.25   0.0777    0.9 -4.9663  5.1218  False
       0.1   0.15   3.9522 0.2311 -1.1368  9.0412  False
       0.1    0.2   2.6639 0.6409 -2.3915  7.7193  False
       0.1   0.25   3.1762 0.4872 -1.9479  8.3004  False
      0.15    0.2  -1.2883    0.9 -6.4605   3.884  False
      0.15   0.25  -0.7759    0.9 -6.0154  4.4635  False
       0.2   0.25   0.5123    0.9 -4.6945  5.7191  False
    ----------------------------------------------------


### Based on the results of Tukey's Test, there is a clear & significant effect on product sales when a product includes a discount. Significant p-values were recorded for products sold when comparing the '0.0' discount group with every other discount group, except for the '0.1' group.

### As for comapring discounts against each other, there were no statistically significant effects. The strongest relationship was present between the '0.1' and '0.15' groups.


```python
import seaborn as sns
fig, ax = plt.subplots(figsize=(6,4))
sns.barplot(data=best_data_ever, x='group', y='data', ci=68, ax=ax)
ax.grid()
ax.get_figure().set_size_inches(6,4)

ax.set(xlabel='Discount', ylabel='Quantity')
```




    [Text(0, 0.5, 'Quantity'), Text(0.5, 0, 'Discount')]




![png](output_30_1.png)


### Recommendation: Based on the results, we have about the same number of products sold for both the 5% and 25% groups. But when we offer a 25% discount, we are losing more money. Therefore, I would suggest no longer offering 25% discounts.

# HYPOTHESIS 2

- $H_0$: There will be no statistically significant effect on units sold based on shipping region.
- $H_1$: Shipping Region will have a statistically significant effect on product units sold.

## Query Data


```python
cur.execute("""SELECT *
            FROM OrderDetail""")
cur.description
df_order_detail = pd.DataFrame(cur.fetchall(), columns = [x[0] for x in cur.description])
df_order_detail
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
      <th>Id</th>
      <th>OrderId</th>
      <th>ProductId</th>
      <th>UnitPrice</th>
      <th>Quantity</th>
      <th>Discount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>10248/11</td>
      <td>10248</td>
      <td>11</td>
      <td>14.00</td>
      <td>12</td>
      <td>0.00</td>
    </tr>
    <tr>
      <td>1</td>
      <td>10248/42</td>
      <td>10248</td>
      <td>42</td>
      <td>9.80</td>
      <td>10</td>
      <td>0.00</td>
    </tr>
    <tr>
      <td>2</td>
      <td>10248/72</td>
      <td>10248</td>
      <td>72</td>
      <td>34.80</td>
      <td>5</td>
      <td>0.00</td>
    </tr>
    <tr>
      <td>3</td>
      <td>10249/14</td>
      <td>10249</td>
      <td>14</td>
      <td>18.60</td>
      <td>9</td>
      <td>0.00</td>
    </tr>
    <tr>
      <td>4</td>
      <td>10249/51</td>
      <td>10249</td>
      <td>51</td>
      <td>42.40</td>
      <td>40</td>
      <td>0.00</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>2150</td>
      <td>11077/64</td>
      <td>11077</td>
      <td>64</td>
      <td>33.25</td>
      <td>2</td>
      <td>0.03</td>
    </tr>
    <tr>
      <td>2151</td>
      <td>11077/66</td>
      <td>11077</td>
      <td>66</td>
      <td>17.00</td>
      <td>1</td>
      <td>0.00</td>
    </tr>
    <tr>
      <td>2152</td>
      <td>11077/73</td>
      <td>11077</td>
      <td>73</td>
      <td>15.00</td>
      <td>2</td>
      <td>0.01</td>
    </tr>
    <tr>
      <td>2153</td>
      <td>11077/75</td>
      <td>11077</td>
      <td>75</td>
      <td>7.75</td>
      <td>4</td>
      <td>0.00</td>
    </tr>
    <tr>
      <td>2154</td>
      <td>11077/77</td>
      <td>11077</td>
      <td>77</td>
      <td>13.00</td>
      <td>2</td>
      <td>0.00</td>
    </tr>
  </tbody>
</table>
<p>2155 rows × 6 columns</p>
</div>




```python
cur.execute("""SELECT *
            FROM 'Order'""")
cur.description
df_order = pd.DataFrame(cur.fetchall(), columns = [x[0] for x in cur.description])
df_order
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
      <th>Id</th>
      <th>CustomerId</th>
      <th>EmployeeId</th>
      <th>OrderDate</th>
      <th>RequiredDate</th>
      <th>ShippedDate</th>
      <th>ShipVia</th>
      <th>Freight</th>
      <th>ShipName</th>
      <th>ShipAddress</th>
      <th>ShipCity</th>
      <th>ShipRegion</th>
      <th>ShipPostalCode</th>
      <th>ShipCountry</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>10248</td>
      <td>VINET</td>
      <td>5</td>
      <td>2012-07-04</td>
      <td>2012-08-01</td>
      <td>2012-07-16</td>
      <td>3</td>
      <td>32.38</td>
      <td>Vins et alcools Chevalier</td>
      <td>59 rue de l'Abbaye</td>
      <td>Reims</td>
      <td>Western Europe</td>
      <td>51100</td>
      <td>France</td>
    </tr>
    <tr>
      <td>1</td>
      <td>10249</td>
      <td>TOMSP</td>
      <td>6</td>
      <td>2012-07-05</td>
      <td>2012-08-16</td>
      <td>2012-07-10</td>
      <td>1</td>
      <td>11.61</td>
      <td>Toms Spezialitäten</td>
      <td>Luisenstr. 48</td>
      <td>Münster</td>
      <td>Western Europe</td>
      <td>44087</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>2</td>
      <td>10250</td>
      <td>HANAR</td>
      <td>4</td>
      <td>2012-07-08</td>
      <td>2012-08-05</td>
      <td>2012-07-12</td>
      <td>2</td>
      <td>65.83</td>
      <td>Hanari Carnes</td>
      <td>Rua do Paço, 67</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>05454-876</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>3</td>
      <td>10251</td>
      <td>VICTE</td>
      <td>3</td>
      <td>2012-07-08</td>
      <td>2012-08-05</td>
      <td>2012-07-15</td>
      <td>1</td>
      <td>41.34</td>
      <td>Victuailles en stock</td>
      <td>2, rue du Commerce</td>
      <td>Lyon</td>
      <td>Western Europe</td>
      <td>69004</td>
      <td>France</td>
    </tr>
    <tr>
      <td>4</td>
      <td>10252</td>
      <td>SUPRD</td>
      <td>4</td>
      <td>2012-07-09</td>
      <td>2012-08-06</td>
      <td>2012-07-11</td>
      <td>2</td>
      <td>51.30</td>
      <td>Suprêmes délices</td>
      <td>Boulevard Tirou, 255</td>
      <td>Charleroi</td>
      <td>Western Europe</td>
      <td>B-6000</td>
      <td>Belgium</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>825</td>
      <td>11073</td>
      <td>PERIC</td>
      <td>2</td>
      <td>2014-05-05</td>
      <td>2014-06-02</td>
      <td>None</td>
      <td>2</td>
      <td>24.95</td>
      <td>Pericles Comidas clásicas</td>
      <td>Calle Dr. Jorge Cash 321</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05033</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>826</td>
      <td>11074</td>
      <td>SIMOB</td>
      <td>7</td>
      <td>2014-05-06</td>
      <td>2014-06-03</td>
      <td>None</td>
      <td>2</td>
      <td>18.44</td>
      <td>Simons bistro</td>
      <td>Vinbæltet 34</td>
      <td>Kobenhavn</td>
      <td>Northern Europe</td>
      <td>1734</td>
      <td>Denmark</td>
    </tr>
    <tr>
      <td>827</td>
      <td>11075</td>
      <td>RICSU</td>
      <td>8</td>
      <td>2014-05-06</td>
      <td>2014-06-03</td>
      <td>None</td>
      <td>2</td>
      <td>6.19</td>
      <td>Richter Supermarkt</td>
      <td>Starenweg 5</td>
      <td>Genève</td>
      <td>Western Europe</td>
      <td>1204</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <td>828</td>
      <td>11076</td>
      <td>BONAP</td>
      <td>4</td>
      <td>2014-05-06</td>
      <td>2014-06-03</td>
      <td>None</td>
      <td>2</td>
      <td>38.28</td>
      <td>Bon app'</td>
      <td>12, rue des Bouchers</td>
      <td>Marseille</td>
      <td>Western Europe</td>
      <td>13008</td>
      <td>France</td>
    </tr>
    <tr>
      <td>829</td>
      <td>11077</td>
      <td>RATTC</td>
      <td>1</td>
      <td>2014-05-06</td>
      <td>2014-06-03</td>
      <td>None</td>
      <td>2</td>
      <td>8.53</td>
      <td>Rattlesnake Canyon Grocery</td>
      <td>2817 Milton Dr.</td>
      <td>Albuquerque</td>
      <td>North America</td>
      <td>87110</td>
      <td>USA</td>
    </tr>
  </tbody>
</table>
<p>830 rows × 14 columns</p>
</div>



## Merge Tables


```python
df_region_use = pd.merge(df_order, df_order_detail, left_on='Id', right_on='OrderId')
df_region_use.head()
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
      <th>Id_x</th>
      <th>CustomerId</th>
      <th>EmployeeId</th>
      <th>OrderDate</th>
      <th>RequiredDate</th>
      <th>ShippedDate</th>
      <th>ShipVia</th>
      <th>Freight</th>
      <th>ShipName</th>
      <th>ShipAddress</th>
      <th>ShipCity</th>
      <th>ShipRegion</th>
      <th>ShipPostalCode</th>
      <th>ShipCountry</th>
      <th>Id_y</th>
      <th>OrderId</th>
      <th>ProductId</th>
      <th>UnitPrice</th>
      <th>Quantity</th>
      <th>Discount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>10248</td>
      <td>VINET</td>
      <td>5</td>
      <td>2012-07-04</td>
      <td>2012-08-01</td>
      <td>2012-07-16</td>
      <td>3</td>
      <td>32.38</td>
      <td>Vins et alcools Chevalier</td>
      <td>59 rue de l'Abbaye</td>
      <td>Reims</td>
      <td>Western Europe</td>
      <td>51100</td>
      <td>France</td>
      <td>10248/11</td>
      <td>10248</td>
      <td>11</td>
      <td>14.0</td>
      <td>12</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>10248</td>
      <td>VINET</td>
      <td>5</td>
      <td>2012-07-04</td>
      <td>2012-08-01</td>
      <td>2012-07-16</td>
      <td>3</td>
      <td>32.38</td>
      <td>Vins et alcools Chevalier</td>
      <td>59 rue de l'Abbaye</td>
      <td>Reims</td>
      <td>Western Europe</td>
      <td>51100</td>
      <td>France</td>
      <td>10248/42</td>
      <td>10248</td>
      <td>42</td>
      <td>9.8</td>
      <td>10</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>2</td>
      <td>10248</td>
      <td>VINET</td>
      <td>5</td>
      <td>2012-07-04</td>
      <td>2012-08-01</td>
      <td>2012-07-16</td>
      <td>3</td>
      <td>32.38</td>
      <td>Vins et alcools Chevalier</td>
      <td>59 rue de l'Abbaye</td>
      <td>Reims</td>
      <td>Western Europe</td>
      <td>51100</td>
      <td>France</td>
      <td>10248/72</td>
      <td>10248</td>
      <td>72</td>
      <td>34.8</td>
      <td>5</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>3</td>
      <td>10249</td>
      <td>TOMSP</td>
      <td>6</td>
      <td>2012-07-05</td>
      <td>2012-08-16</td>
      <td>2012-07-10</td>
      <td>1</td>
      <td>11.61</td>
      <td>Toms Spezialitäten</td>
      <td>Luisenstr. 48</td>
      <td>Münster</td>
      <td>Western Europe</td>
      <td>44087</td>
      <td>Germany</td>
      <td>10249/14</td>
      <td>10249</td>
      <td>14</td>
      <td>18.6</td>
      <td>9</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>4</td>
      <td>10249</td>
      <td>TOMSP</td>
      <td>6</td>
      <td>2012-07-05</td>
      <td>2012-08-16</td>
      <td>2012-07-10</td>
      <td>1</td>
      <td>11.61</td>
      <td>Toms Spezialitäten</td>
      <td>Luisenstr. 48</td>
      <td>Münster</td>
      <td>Western Europe</td>
      <td>44087</td>
      <td>Germany</td>
      <td>10249/51</td>
      <td>10249</td>
      <td>51</td>
      <td>42.4</td>
      <td>40</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>



## Create Dictionaries for Shipping Regions


```python
data_region_products = {}
for region in df_region_use['ShipRegion'].unique():
    print(region)
    data_region_products[region] = df_region_use.groupby('ShipRegion').get_group(region)['Quantity']
    
data_region_products
```

    Western Europe
    South America
    Central America
    North America
    Northern Europe
    Scandinavia
    Southern Europe
    British Isles
    Eastern Europe





    {'Western Europe': 0       12
     1       10
     2        5
     3        9
     4       40
             ..
     2125    30
     2126     2
     2127    20
     2128    20
     2129    10
     Name: Quantity, Length: 745, dtype: int64, 'South America': 5       10
     6       35
     7       15
     14      20
     15      42
             ..
     2107     8
     2108    36
     2109    28
     2115    15
     2116    10
     Name: Quantity, Length: 355, dtype: int64, 'Central America': 32      10
     33       1
     74      15
     75      10
     119     12
             ..
     1927    20
     1928     4
     2110    20
     2121    10
     2122    20
     Name: Quantity, Length: 72, dtype: int64, 'North America': 40      12
     41      15
     42       2
     57      60
     58      20
             ..
     2150     2
     2151     1
     2152     2
     2153     4
     2154     2
     Name: Quantity, Length: 427, dtype: int64, 'Northern Europe': 47      35
     48      25
     78      16
     79      15
     80       8
             ..
     1944    25
     1945    25
     1946     6
     2065    50
     2123    14
     Name: Quantity, Length: 143, dtype: int64, 'Scandinavia': 51      12
     59      30
     60      25
     190     30
     226     10
             ..
     1957    10
     1981    15
     1982    18
     2007    10
     2008    20
     Name: Quantity, Length: 70, dtype: int64, 'Southern Europe': 72      12
     73       6
     86       1
     87       6
     88       4
             ..
     2040     4
     2088     4
     2089    10
     2091    10
     2092    12
     Name: Quantity, Length: 137, dtype: int64, 'British Isles': 109     30
     110      9
     134     40
     135     40
     136     30
             ..
     2080    50
     2081     3
     2093    30
     2094    40
     2095    30
     Name: Quantity, Length: 190, dtype: int64, 'Eastern Europe': 336     30
     337     15
     957      6
     958     10
     959     15
     1424    10
     1425     3
     1426    15
     1633     3
     1634     2
     1713    15
     1933    12
     1934     7
     1935    20
     1936    30
     2054    12
     Name: Quantity, dtype: int64}



## Outlier Removal & Normality Test


```python
clean_data_region_prod = {}
clean_list_region_prod = []
for k, v in data_region_products.items():
    
    idx_outs = find_outliers_Z(v)
    data_clean = v[~idx_outs].copy()
    clean_list_region_prod.append(data_clean)
    stat, p = stats.shapiro(data_clean)
    print(f"For {k} normal test, p = {round(p, 4)}, n = {len(data_clean)}")
    clean_data_region_prod[k] = data_clean
```

    For Western Europe normal test, p = 0.0, n = 731
    For South America normal test, p = 0.0, n = 350
    For Central America normal test, p = 0.0007, n = 71
    For North America normal test, p = 0.0, n = 417
    For Northern Europe normal test, p = 0.0, n = 143
    For Scandinavia normal test, p = 0.0001, n = 69
    For Southern Europe normal test, p = 0.0, n = 136
    For British Isles normal test, p = 0.0, n = 185
    For Eastern Europe normal test, p = 0.084, n = 16


### After testing for normality, we can conclude that this data is not normally distributed. We will now test for equal variance because our groups have large enough samples.

## Test for Equal Variance


```python
empty_list_reg = []
for k,v in clean_data_region_prod.items():
    empty_list_reg.append(v)
```


```python
stats.levene(*empty_list_reg)
```




    LeveneResult(statistic=10.413760942601051, pvalue=2.0992306280336536e-14)



### This test result shows that our data does not have equal variance. Therefore, we will test this data using the Non-Parametric ANOVA test.

## Hypothesis Test: Non-Parametric ANOVA (Alpha = .05)


```python
stats.kruskal(*clean_list_region_prod)
```




    KruskalResult(statistic=111.8182551112351, pvalue=1.6098142288244464e-20)



### We were able to achieve a significant p-value from this hypothesis test. Therefore, we can reject our null hypothesis and accept that shipping region has a statistically significant effect on product units sold. Next, we will run a Tukey's Test to see if any region has signficant effects when compared to another region.

## Tukey's Test


```python
df_reg_product_tukey = prep_data_for_tukeys(clean_data_region_prod)
```


```python
results = pairwise_tukeyhsd(df_reg_product_tukey['data'].values, df_reg_product_tukey['group'].values)
results.summary()
```




<table class="simpletable">
<caption>Multiple Comparison of Means - Tukey HSD, FWER=0.05</caption>
<tr>
      <th>group1</th>          <th>group2</th>      <th>meandiff</th>  <th>p-adj</th>   <th>lower</th>   <th>upper</th>  <th>reject</th>
</tr>
<tr>
   <td>British Isles</td>  <td>Central America</td>  <td>-8.0298</td> <td>0.0096</td> <td>-14.9408</td> <td>-1.1188</td>  <td>True</td> 
</tr>
<tr>
   <td>British Isles</td>  <td>Eastern Europe</td>   <td>-8.9497</td> <td>0.4395</td> <td>-21.8496</td> <td>3.9503</td>   <td>False</td>
</tr>
<tr>
   <td>British Isles</td>   <td>North America</td>   <td>2.7558</td>  <td>0.5634</td>  <td>-1.6172</td> <td>7.1288</td>   <td>False</td>
</tr>
<tr>
   <td>British Isles</td>  <td>Northern Europe</td>   <td>2.049</td>    <td>0.9</td>   <td>-3.4631</td> <td>7.5612</td>   <td>False</td>
</tr>
<tr>
   <td>British Isles</td>    <td>Scandinavia</td>    <td>-7.3274</td> <td>0.0313</td> <td>-14.3104</td> <td>-0.3444</td>  <td>True</td> 
</tr>
<tr>
   <td>British Isles</td>   <td>South America</td>   <td>-1.2707</td>   <td>0.9</td>   <td>-5.7705</td> <td>3.2291</td>   <td>False</td>
</tr>
<tr>
   <td>British Isles</td>  <td>Southern Europe</td>  <td>-6.8872</td> <td>0.0043</td> <td>-12.4787</td> <td>-1.2956</td>  <td>True</td> 
</tr>
<tr>
   <td>British Isles</td>  <td>Western Europe</td>   <td>3.8876</td>  <td>0.0755</td>  <td>-0.1865</td> <td>7.9618</td>   <td>False</td>
</tr>
<tr>
  <td>Central America</td> <td>Eastern Europe</td>   <td>-0.9199</td>   <td>0.9</td>  <td>-14.6195</td> <td>12.7797</td>  <td>False</td>
</tr>
<tr>
  <td>Central America</td>  <td>North America</td>   <td>10.7856</td>  <td>0.001</td>  <td>4.4301</td>  <td>17.1411</td>  <td>True</td> 
</tr>
<tr>
  <td>Central America</td> <td>Northern Europe</td>  <td>10.0788</td>  <td>0.001</td>  <td>2.8918</td>  <td>17.2658</td>  <td>True</td> 
</tr>
<tr>
  <td>Central America</td>   <td>Scandinavia</td>    <td>0.7024</td>    <td>0.9</td>   <td>-7.6661</td> <td>9.0709</td>   <td>False</td>
</tr>
<tr>
  <td>Central America</td>  <td>South America</td>    <td>6.759</td>  <td>0.0314</td>  <td>0.3156</td>  <td>13.2024</td>  <td>True</td> 
</tr>
<tr>
  <td>Central America</td> <td>Southern Europe</td>  <td>1.1426</td>    <td>0.9</td>   <td>-6.1055</td> <td>8.3907</td>   <td>False</td>
</tr>
<tr>
  <td>Central America</td> <td>Western Europe</td>   <td>11.9174</td>  <td>0.001</td>  <td>5.7637</td>  <td>18.0711</td>  <td>True</td> 
</tr>
<tr>
  <td>Eastern Europe</td>   <td>North America</td>   <td>11.7055</td> <td>0.0934</td>  <td>-0.9056</td> <td>24.3166</td>  <td>False</td>
</tr>
<tr>
  <td>Eastern Europe</td>  <td>Northern Europe</td>  <td>10.9987</td> <td>0.1797</td>  <td>-2.0512</td> <td>24.0486</td>  <td>False</td>
</tr>
<tr>
  <td>Eastern Europe</td>    <td>Scandinavia</td>    <td>1.6223</td>    <td>0.9</td>  <td>-12.1137</td> <td>15.3583</td>  <td>False</td>
</tr>
<tr>
  <td>Eastern Europe</td>   <td>South America</td>   <td>7.6789</td>  <td>0.6075</td>  <td>-4.9767</td> <td>20.3345</td>  <td>False</td>
</tr>
<tr>
  <td>Eastern Europe</td>  <td>Southern Europe</td>  <td>2.0625</td>    <td>0.9</td>  <td>-11.0211</td> <td>15.1461</td>  <td>False</td>
</tr>
<tr>
  <td>Eastern Europe</td>  <td>Western Europe</td>   <td>12.8373</td> <td>0.0392</td>  <td>0.3267</td>  <td>25.3479</td>  <td>True</td> 
</tr>
<tr>
   <td>North America</td>  <td>Northern Europe</td>  <td>-0.7068</td>   <td>0.9</td>   <td>-5.5041</td> <td>4.0905</td>   <td>False</td>
</tr>
<tr>
   <td>North America</td>    <td>Scandinavia</td>   <td>-10.0832</td>  <td>0.001</td> <td>-16.5169</td> <td>-3.6495</td>  <td>True</td> 
</tr>
<tr>
   <td>North America</td>   <td>South America</td>   <td>-4.0266</td> <td>0.0148</td>  <td>-7.6152</td> <td>-0.4379</td>  <td>True</td> 
</tr>
<tr>
   <td>North America</td>  <td>Southern Europe</td>  <td>-9.643</td>   <td>0.001</td> <td>-14.5313</td> <td>-4.7546</td>  <td>True</td> 
</tr>
<tr>
   <td>North America</td>  <td>Western Europe</td>   <td>1.1318</td>    <td>0.9</td>   <td>-1.9061</td> <td>4.1698</td>   <td>False</td>
</tr>
<tr>
  <td>Northern Europe</td>   <td>Scandinavia</td>    <td>-9.3764</td>  <td>0.002</td> <td>-16.6326</td> <td>-2.1202</td>  <td>True</td> 
</tr>
<tr>
  <td>Northern Europe</td>  <td>South America</td>   <td>-3.3198</td> <td>0.4766</td>  <td>-8.2329</td> <td>1.5934</td>   <td>False</td>
</tr>
<tr>
  <td>Northern Europe</td> <td>Southern Europe</td>  <td>-8.9362</td>  <td>0.001</td> <td>-14.8655</td> <td>-3.0069</td>  <td>True</td> 
</tr>
<tr>
  <td>Northern Europe</td> <td>Western Europe</td>   <td>1.8386</td>    <td>0.9</td>   <td>-2.6879</td> <td>6.3651</td>   <td>False</td>
</tr>
<tr>
    <td>Scandinavia</td>    <td>South America</td>   <td>6.0566</td>  <td>0.0929</td>  <td>-0.4639</td> <td>12.5772</td>  <td>False</td>
</tr>
<tr>
    <td>Scandinavia</td>   <td>Southern Europe</td>  <td>0.4402</td>    <td>0.9</td>   <td>-6.8765</td>  <td>7.757</td>   <td>False</td>
</tr>
<tr>
    <td>Scandinavia</td>   <td>Western Europe</td>   <td>11.215</td>   <td>0.001</td>  <td>4.9806</td>  <td>17.4495</td>  <td>True</td> 
</tr>
<tr>
   <td>South America</td>  <td>Southern Europe</td>  <td>-5.6164</td> <td>0.0147</td> <td>-10.6185</td> <td>-0.6143</td>  <td>True</td> 
</tr>
<tr>
   <td>South America</td>  <td>Western Europe</td>   <td>5.1584</td>   <td>0.001</td>  <td>1.9406</td>  <td>8.3761</td>   <td>True</td> 
</tr>
<tr>
  <td>Southern Europe</td> <td>Western Europe</td>   <td>10.7748</td>  <td>0.001</td>  <td>6.1519</td>  <td>15.3977</td>  <td>True</td> 
</tr>
</table>




```python
df_reg_prod_final = pd.DataFrame(data=results._results_table.data[1:], columns=results._results_table.data[0])
pd.set_option('display.max_rows', 999)
df_reg_prod_final.loc[df_reg_prod_final['reject'] == True]
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
      <th>group1</th>
      <th>group2</th>
      <th>meandiff</th>
      <th>p-adj</th>
      <th>lower</th>
      <th>upper</th>
      <th>reject</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>British Isles</td>
      <td>Central America</td>
      <td>-8.0298</td>
      <td>0.0096</td>
      <td>-14.9408</td>
      <td>-1.1188</td>
      <td>True</td>
    </tr>
    <tr>
      <td>4</td>
      <td>British Isles</td>
      <td>Scandinavia</td>
      <td>-7.3274</td>
      <td>0.0313</td>
      <td>-14.3104</td>
      <td>-0.3444</td>
      <td>True</td>
    </tr>
    <tr>
      <td>6</td>
      <td>British Isles</td>
      <td>Southern Europe</td>
      <td>-6.8872</td>
      <td>0.0043</td>
      <td>-12.4787</td>
      <td>-1.2956</td>
      <td>True</td>
    </tr>
    <tr>
      <td>9</td>
      <td>Central America</td>
      <td>North America</td>
      <td>10.7856</td>
      <td>0.0010</td>
      <td>4.4301</td>
      <td>17.1411</td>
      <td>True</td>
    </tr>
    <tr>
      <td>10</td>
      <td>Central America</td>
      <td>Northern Europe</td>
      <td>10.0788</td>
      <td>0.0010</td>
      <td>2.8918</td>
      <td>17.2658</td>
      <td>True</td>
    </tr>
    <tr>
      <td>12</td>
      <td>Central America</td>
      <td>South America</td>
      <td>6.7590</td>
      <td>0.0314</td>
      <td>0.3156</td>
      <td>13.2024</td>
      <td>True</td>
    </tr>
    <tr>
      <td>14</td>
      <td>Central America</td>
      <td>Western Europe</td>
      <td>11.9174</td>
      <td>0.0010</td>
      <td>5.7637</td>
      <td>18.0711</td>
      <td>True</td>
    </tr>
    <tr>
      <td>20</td>
      <td>Eastern Europe</td>
      <td>Western Europe</td>
      <td>12.8373</td>
      <td>0.0392</td>
      <td>0.3267</td>
      <td>25.3479</td>
      <td>True</td>
    </tr>
    <tr>
      <td>22</td>
      <td>North America</td>
      <td>Scandinavia</td>
      <td>-10.0832</td>
      <td>0.0010</td>
      <td>-16.5169</td>
      <td>-3.6495</td>
      <td>True</td>
    </tr>
    <tr>
      <td>23</td>
      <td>North America</td>
      <td>South America</td>
      <td>-4.0266</td>
      <td>0.0148</td>
      <td>-7.6152</td>
      <td>-0.4379</td>
      <td>True</td>
    </tr>
    <tr>
      <td>24</td>
      <td>North America</td>
      <td>Southern Europe</td>
      <td>-9.6430</td>
      <td>0.0010</td>
      <td>-14.5313</td>
      <td>-4.7546</td>
      <td>True</td>
    </tr>
    <tr>
      <td>26</td>
      <td>Northern Europe</td>
      <td>Scandinavia</td>
      <td>-9.3764</td>
      <td>0.0020</td>
      <td>-16.6326</td>
      <td>-2.1202</td>
      <td>True</td>
    </tr>
    <tr>
      <td>28</td>
      <td>Northern Europe</td>
      <td>Southern Europe</td>
      <td>-8.9362</td>
      <td>0.0010</td>
      <td>-14.8655</td>
      <td>-3.0069</td>
      <td>True</td>
    </tr>
    <tr>
      <td>32</td>
      <td>Scandinavia</td>
      <td>Western Europe</td>
      <td>11.2150</td>
      <td>0.0010</td>
      <td>4.9806</td>
      <td>17.4495</td>
      <td>True</td>
    </tr>
    <tr>
      <td>33</td>
      <td>South America</td>
      <td>Southern Europe</td>
      <td>-5.6164</td>
      <td>0.0147</td>
      <td>-10.6185</td>
      <td>-0.6143</td>
      <td>True</td>
    </tr>
    <tr>
      <td>34</td>
      <td>South America</td>
      <td>Western Europe</td>
      <td>5.1584</td>
      <td>0.0010</td>
      <td>1.9406</td>
      <td>8.3761</td>
      <td>True</td>
    </tr>
    <tr>
      <td>35</td>
      <td>Southern Europe</td>
      <td>Western Europe</td>
      <td>10.7748</td>
      <td>0.0010</td>
      <td>6.1519</td>
      <td>15.3977</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



### The Tukey's Test clearly shows that certain shipping regions have statistical significance when compared with another region. The strongest relationships are as follows:

### - Central America & North America
### - Central America & Northern Europe
### - Central America & Western Europe
### - North America & Scandinavia
### - North America & Southern Europe
### - Northern Europe & Southern Europe
### - Scandinavia & Western Europe
### - South America & Western Europe
### - Southern Europe & Western Europe


```python
fig, ax = plt.subplots(figsize=(7,4))
sns.barplot(data=df_reg_product_tukey, x='group', y='data', ci=68, ax=ax)
ax.grid()
ax.set_xticklabels(ax.get_xticklabels(), rotation=45, ha='right')
ax.set(xlabel='Shipping Region', ylabel='Quantity')
```




    [Text(0, 0.5, 'Quantity'), Text(0.5, 0, 'Shipping Region')]




![png](output_56_1.png)


### Recommendation: After analyzing these results, my primary recommendation would be to try and increase sales where products are shipped in Western Europe, North America, and Northern Europe. These 3 regions seem to be our biggest players and I believe the best decision would be to further invest marketing into those three regions so that we can further improve sales and increase revenue.

# HYPOTHESIS 3

- $H_0$: Revenue will not be statistically affected by applying discounts to each product.
- $H_1$: For each product, discounts will result in a statistically significant effect on revenue. 

## Create Function to Calculate Revenue


```python
def revenue(x,y):
    """This function will be used to calculate the revenue generated for each product sold.
    x = UnitPrice
    y = Quantity"""
    return x*y
```

## Query Data


```python
cur.execute("""SELECT * 
            FROM OrderDetail
            ORDER BY ProductID ASC;""")
df_revenue = pd.DataFrame(cur.fetchall(), columns = [x[0] for x in cur.description])
df_revenue.head()
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
      <th>Id</th>
      <th>OrderId</th>
      <th>ProductId</th>
      <th>UnitPrice</th>
      <th>Quantity</th>
      <th>Discount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>10285/1</td>
      <td>10285</td>
      <td>1</td>
      <td>14.4</td>
      <td>45</td>
      <td>0.20</td>
    </tr>
    <tr>
      <td>1</td>
      <td>10294/1</td>
      <td>10294</td>
      <td>1</td>
      <td>14.4</td>
      <td>18</td>
      <td>0.00</td>
    </tr>
    <tr>
      <td>2</td>
      <td>10317/1</td>
      <td>10317</td>
      <td>1</td>
      <td>14.4</td>
      <td>20</td>
      <td>0.00</td>
    </tr>
    <tr>
      <td>3</td>
      <td>10348/1</td>
      <td>10348</td>
      <td>1</td>
      <td>14.4</td>
      <td>15</td>
      <td>0.15</td>
    </tr>
    <tr>
      <td>4</td>
      <td>10354/1</td>
      <td>10354</td>
      <td>1</td>
      <td>14.4</td>
      <td>12</td>
      <td>0.00</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_revenue['Revenue'] = revenue(df_revenue['UnitPrice'], df_revenue['Quantity'])
df_revenue.head()
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
      <th>Id</th>
      <th>OrderId</th>
      <th>ProductId</th>
      <th>UnitPrice</th>
      <th>Quantity</th>
      <th>Discount</th>
      <th>Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>10285/1</td>
      <td>10285</td>
      <td>1</td>
      <td>14.4</td>
      <td>45</td>
      <td>0.20</td>
      <td>648.0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>10294/1</td>
      <td>10294</td>
      <td>1</td>
      <td>14.4</td>
      <td>18</td>
      <td>0.00</td>
      <td>259.2</td>
    </tr>
    <tr>
      <td>2</td>
      <td>10317/1</td>
      <td>10317</td>
      <td>1</td>
      <td>14.4</td>
      <td>20</td>
      <td>0.00</td>
      <td>288.0</td>
    </tr>
    <tr>
      <td>3</td>
      <td>10348/1</td>
      <td>10348</td>
      <td>1</td>
      <td>14.4</td>
      <td>15</td>
      <td>0.15</td>
      <td>216.0</td>
    </tr>
    <tr>
      <td>4</td>
      <td>10354/1</td>
      <td>10354</td>
      <td>1</td>
      <td>14.4</td>
      <td>12</td>
      <td>0.00</td>
      <td>172.8</td>
    </tr>
  </tbody>
</table>
</div>



## Create Dictionaries for each Product


```python
data_2 = {}
for product in df_revenue['ProductId'].unique():
    print(product)
    data_2[product] = df_revenue.groupby('ProductId').get_group(product)['Revenue']
    
data_2
```

    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20
    21
    22
    23
    24
    25
    26
    27
    28
    29
    30
    31
    32
    33
    34
    35
    36
    37
    38
    39
    40
    41
    42
    43
    44
    45
    46
    47
    48
    49
    50
    51
    52
    53
    54
    55
    56
    57
    58
    59
    60
    61
    62
    63
    64
    65
    66
    67
    68
    69
    70
    71
    72
    73
    74
    75
    76
    77





    {1: 0      648.0
     1      259.2
     2      288.0
     3      216.0
     4      172.8
     5      216.0
     6      144.0
     7      345.6
     8      216.0
     9      720.0
     10     144.0
     11     180.0
     12     360.0
     13      54.0
     14     108.0
     15     450.0
     16     270.0
     17     630.0
     18     540.0
     19      90.0
     20     900.0
     21     144.0
     22      72.0
     23    1440.0
     24     360.0
     25     720.0
     26     360.0
     27     180.0
     28    1080.0
     29     378.0
     30      72.0
     31      36.0
     32     144.0
     33     180.0
     34     810.0
     35     180.0
     36     450.0
     37     720.0
     Name: Revenue, dtype: float64, 2: 38     304.0
     39     760.0
     40     532.0
     41     608.0
     42     380.0
     43     106.4
     44     364.8
     45     380.0
     46     912.0
     47     152.0
     48     684.0
     49     608.0
     50     304.0
     51     228.0
     52     190.0
     53     380.0
     54     570.0
     55     950.0
     56      95.0
     57     570.0
     58      57.0
     59     285.0
     60     760.0
     61     285.0
     62     190.0
     63     380.0
     64     228.0
     65     190.0
     66      95.0
     67     285.0
     68     380.0
     69     399.0
     70     380.0
     71     380.0
     72     190.0
     73     950.0
     74     209.0
     75    1900.0
     76     570.0
     77     190.0
     78     380.0
     79     152.0
     80     190.0
     81     456.0
     Name: Revenue, dtype: float64, 3: 82    240.0
     83    400.0
     84    160.0
     85    600.0
     86    140.0
     87     60.0
     88    200.0
     89    200.0
     90    490.0
     91    300.0
     92    250.0
     93     40.0
     Name: Revenue, dtype: float64, 4: 94      352.0
     95      422.4
     96      316.8
     97      176.0
     98      616.0
     99      281.6
     100    1100.0
     101    1100.0
     102    1100.0
     103     440.0
     104     220.0
     105     550.0
     106     264.0
     107     132.0
     108     550.0
     109     462.0
     110     660.0
     111     110.0
     112     550.0
     113      22.0
     Name: Revenue, dtype: float64, 5: 114    1105.00
     115     204.00
     116     340.00
     117     544.00
     118     320.25
     119      85.40
     120     640.50
     121     427.00
     122    1494.50
     123     640.50
     Name: Revenue, dtype: float64, 6: 124     600.0
     125     120.0
     126    1750.0
     127     750.0
     128     150.0
     129    1250.0
     130     500.0
     131     300.0
     132     400.0
     133    1000.0
     134     500.0
     135      25.0
     Name: Revenue, dtype: float64, 7: 136     360.0
     137     240.0
     138     384.0
     139     720.0
     140    1500.0
     141     300.0
     142     300.0
     143    1350.0
     144    1050.0
     145    2700.0
     146    1050.0
     147      90.0
     148     600.0
     149     150.0
     150     600.0
     151     360.0
     152     240.0
     153     180.0
     154    1350.0
     155     540.0
     156     600.0
     157    1800.0
     158    1800.0
     159    1800.0
     160     600.0
     161     120.0
     162    1200.0
     163     450.0
     164      30.0
     Name: Revenue, dtype: float64, 8: 165    2240.0
     166    2240.0
     167     400.0
     168     960.0
     169     400.0
     170    1600.0
     171    1200.0
     172     800.0
     173    1200.0
     174     640.0
     175     800.0
     176    1200.0
     177      80.0
     Name: Revenue, dtype: float64, 9: 178    1552.0
     179    1552.0
     180    4850.0
     181     582.0
     182     291.0
     Name: Revenue, dtype: float64, 10: 183     595.2
     184     372.0
     185     744.0
     186     396.8
     187     347.2
     188     496.0
     189     496.0
     190     496.0
     191      62.0
     192     155.0
     193     310.0
     194    2170.0
     195     558.0
     196     744.0
     197      62.0
     198     620.0
     199     558.0
     200     558.0
     201     651.0
     202     496.0
     203     186.0
     204     310.0
     205    1116.0
     206     465.0
     207     496.0
     208    3100.0
     209     310.0
     210    2170.0
     211     620.0
     212     775.0
     213     930.0
     214     744.0
     215      31.0
     Name: Revenue, dtype: float64, 11: 216     168.0
     217     201.6
     218     840.0
     219     201.6
     220     403.2
     221     504.0
     222     100.8
     223     504.0
     224     100.8
     225     168.0
     226      84.0
     227     252.0
     228      63.0
     229    1050.0
     230     315.0
     231     210.0
     232     315.0
     233     735.0
     234     315.0
     235     294.0
     236     210.0
     237     315.0
     238     105.0
     239     315.0
     240     420.0
     241    1050.0
     242     420.0
     243     315.0
     244     525.0
     245     210.0
     246     840.0
     247     840.0
     248      42.0
     249     105.0
     250     630.0
     251     315.0
     252     210.0
     253     210.0
     Name: Revenue, dtype: float64, 12: 254     364.8
     255     456.0
     256     570.0
     257    1140.0
     258    1368.0
     259    3800.0
     260     152.0
     261    1368.0
     262    1140.0
     263     760.0
     264     760.0
     265     760.0
     266     152.0
     267      76.0
     Name: Revenue, dtype: float64, 13: 268     48.0
     269     96.0
     270     57.6
     271     96.0
     272     86.4
     273     48.0
     274      9.6
     275      4.8
     276     60.0
     277     60.0
     278     48.0
     279    360.0
     280     48.0
     281     78.0
     282     24.0
     283     36.0
     284    120.0
     285     42.0
     286     60.0
     287     18.0
     288     36.0
     289    390.0
     290    168.0
     291     30.0
     292    240.0
     293     60.0
     294    252.0
     295    120.0
     296    120.0
     297     90.0
     298    120.0
     299    462.0
     300    504.0
     301    336.0
     302    120.0
     303    480.0
     304     42.0
     305    180.0
     306     60.0
     307     24.0
     Name: Revenue, dtype: float64, 14: 308     167.40
     309     167.40
     310     186.00
     311     279.00
     312     781.20
     313     223.20
     314     372.00
     315     651.00
     316     223.20
     317    1627.50
     318     697.50
     319     255.75
     320     348.75
     321     488.25
     322      69.75
     323      69.75
     324     697.50
     325     372.00
     326     116.25
     327     348.75
     328     465.00
     329      23.25
     Name: Revenue, dtype: float64, 15: 330    248.0
     331     62.0
     332    186.0
     333    155.0
     334    387.5
     335    775.0
     Name: Revenue, dtype: float64, 16: 336     486.50
     337     834.00
     338     556.00
     339     417.00
     340     139.00
     341     291.90
     342     778.40
     343     291.90
     344     222.40
     345     681.10
     346     278.00
     347     486.50
     348     250.20
     349     872.50
     350     698.00
     351     244.30
     352     523.50
     353     209.40
     354     523.50
     355     523.50
     356     174.50
     357      52.35
     358     872.50
     359     349.00
     360     349.00
     361     261.75
     362      52.35
     363     349.00
     364    1134.25
     365     872.50
     366     209.40
     367     523.50
     368     261.75
     369     104.70
     370     418.80
     371     523.50
     372     488.60
     373     959.75
     374     628.20
     375      52.35
     376     523.50
     377     244.30
     378      34.90
     Name: Revenue, dtype: float64, 17: 379     936.0
     380     468.0
     381     468.0
     382    1248.0
     383     249.6
     384     624.0
     385    2184.0
     386    1123.2
     387      62.4
     388    1404.0
     389    1560.0
     390     312.0
     391     975.0
     392    1560.0
     393     312.0
     394     624.0
     395     702.0
     396    3900.0
     397    1170.0
     398     780.0
     399     312.0
     400    1053.0
     401     780.0
     402    1287.0
     403    1365.0
     404    1560.0
     405     234.0
     406    1638.0
     407     624.0
     408     585.0
     409     468.0
     410     390.0
     411     585.0
     412     234.0
     413     234.0
     414     468.0
     415    3003.0
     Name: Revenue, dtype: float64, 18: 416     600.0
     417    1250.0
     418    2000.0
     419    1000.0
     420     450.0
     421    1500.0
     422    1562.5
     423    1125.0
     424    2500.0
     425    3125.0
     426     500.0
     427     250.0
     428    1250.0
     429     750.0
     430    1500.0
     431    1312.5
     432    1875.0
     433    1562.5
     434     625.0
     435    1250.0
     436    1562.5
     437     250.0
     438     375.0
     439     500.0
     440     625.0
     441     500.0
     442    2187.5
     Name: Revenue, dtype: float64, 19: 443      7.3
     444    131.4
     445    109.5
     446     73.0
     447    584.0
     448    131.4
     449    146.0
     450     29.2
     451    109.5
     452     87.6
     453    292.0
     454    153.3
     455     36.5
     456     92.0
     457    322.0
     458     46.0
     459    138.0
     460    276.0
     461    110.4
     462     64.4
     463    276.0
     464     64.4
     465     46.0
     466    110.4
     467    460.0
     468    220.8
     469    138.0
     470     18.4
     471    110.4
     472    230.0
     473    110.4
     474     64.4
     475    110.4
     476    460.0
     477    322.0
     478    386.4
     479     92.0
     Name: Revenue, dtype: float64, 20: 480    2592.0
     481     388.8
     482    1296.0
     483     777.6
     484    1814.4
     485    3159.0
     486    1215.0
     487    1701.0
     488    1701.0
     489     405.0
     490    1620.0
     491     405.0
     492    4050.0
     493    1215.0
     494    1215.0
     495      81.0
     Name: Revenue, dtype: float64, 21: 496     80.0
     497    160.0
     498     80.0
     499     40.0
     500     80.0
     501    240.0
     502     96.0
     503    400.0
     504    320.0
     505    320.0
     506    168.0
     507    112.0
     508    120.0
     509    400.0
     510    150.0
     511     60.0
     512     60.0
     513     80.0
     514    420.0
     515    250.0
     516    300.0
     517    600.0
     518    120.0
     519     50.0
     520    320.0
     521    300.0
     522    400.0
     523    400.0
     524    400.0
     525    200.0
     526    400.0
     527    600.0
     528    360.0
     529    120.0
     530    400.0
     531    650.0
     532    150.0
     533    200.0
     534     30.0
     Name: Revenue, dtype: float64, 22: 535     100.8
     536     201.6
     537     504.0
     538    1008.0
     539     840.0
     540     840.0
     541     315.0
     542     420.0
     543     126.0
     544      84.0
     545    1092.0
     546     735.0
     547     441.0
     548     525.0
     Name: Revenue, dtype: float64, 23: 549    288.0
     550    180.0
     551    288.0
     552    432.0
     553    151.2
     554    108.0
     555     72.0
     556    630.0
     557    180.0
     558     90.0
     559    288.0
     560     45.0
     561    396.0
     562    162.0
     563    630.0
     564    450.0
     565    270.0
     566     72.0
     567     90.0
     568     18.0
     Name: Revenue, dtype: float64, 24: 569     54.0
     570    100.8
     571     43.2
     572     43.2
     573     21.6
     574     36.0
     575     36.0
     576     90.0
     577     36.0
     578     54.0
     579     54.0
     580     72.0
     581     90.0
     582    100.8
     583    288.0
     584     63.0
     585     45.0
     586     22.5
     587     36.0
     588    157.5
     589     81.0
     590    112.5
     591    157.5
     592     22.5
     593     13.5
     594     67.5
     595     90.0
     596    157.5
     597     90.0
     598     90.0
     599    180.0
     600     27.0
     601     36.0
     602     54.0
     603     45.0
     604    495.0
     605    157.5
     606    112.5
     607     45.0
     608    135.0
     609    360.0
     610     90.0
     611     54.0
     612    135.0
     613     54.0
     614     45.0
     615    135.0
     616     94.5
     617     45.0
     618     67.5
     619     90.0
     Name: Revenue, dtype: float64, 25: 620     44.8
     621    112.0
     622    560.0
     623     78.4
     624    134.4
     625    672.0
     626    252.0
     627    168.0
     628    490.0
     629    210.0
     630     70.0
     631    140.0
     632     84.0
     633    280.0
     634    140.0
     635     70.0
     636    336.0
     637    210.0
     Name: Revenue, dtype: float64, 26: 638    1245.00
     639     597.60
     640     398.40
     641    1743.00
     642     747.00
     643     747.00
     644      49.80
     645     249.00
     646     373.50
     647     149.40
     648     747.00
     649     747.00
     650    1249.20
     651     187.38
     652     156.15
     653    1093.05
     654     936.90
     655     468.45
     656     936.90
     657     468.45
     658     374.76
     659     624.60
     660     655.83
     661    1249.20
     662     374.76
     663     562.14
     664    1093.05
     665     624.60
     666     156.15
     667     187.38
     668    1967.49
     669     374.76
     Name: Revenue, dtype: float64, 27: 670     877.5
     671     526.5
     672    1755.0
     673    5268.0
     674    2195.0
     675    1756.0
     676     439.0
     677    1097.5
     678    1317.0
     Name: Revenue, dtype: float64, 28: 679     728.0
     680    1019.2
     681     145.6
     682     509.6
     683    1092.0
     684     473.2
     685     728.0
     686     218.4
     687    1528.8
     688     436.8
     689     546.0
     690    1092.0
     691     655.2
     692     912.0
     693     364.8
     694     136.8
     695    1596.0
     696     319.2
     697     456.0
     698     684.0
     699     912.0
     700    2736.0
     701     912.0
     702     228.0
     703    1094.4
     704     136.8
     705    1368.0
     706     364.8
     707      91.2
     708     912.0
     709    3192.0
     710     912.0
     711     364.8
     Name: Revenue, dtype: float64, 29: 712     990.00
     713    1485.00
     714    2475.00
     715     396.00
     716    3465.00
     717    1980.00
     718    1386.00
     719    2079.00
     720    2376.00
     721    1782.00
     722    4456.44
     723    1237.90
     724     742.74
     725    2475.80
     726    4456.44
     727    1237.90
     728    4951.60
     729    1485.48
     730    2228.22
     731    2475.80
     732    1733.06
     733    2475.80
     734     990.32
     735    1237.90
     736    2970.96
     737    9903.20
     738    7427.40
     739    1733.06
     740    6189.50
     741     247.58
     742    1237.90
     743    7427.40
     Name: Revenue, dtype: float64, 30: 744    1242.00
     745     124.20
     746     207.00
     747     724.50
     748     165.60
     749     310.50
     750     372.60
     751     372.60
     752     579.60
     753     165.60
     754     517.80
     755     258.90
     756     388.35
     757     258.90
     758     517.80
     759     776.70
     760      51.78
     761      77.67
     762     388.35
     763     388.35
     764     776.70
     765     388.35
     766     647.25
     767     517.80
     768    1035.60
     769     388.35
     770     906.15
     771     932.04
     772      25.89
     773     776.70
     774     388.35
     775     103.56
     Name: Revenue, dtype: float64, 31: 776    200.0
     777    400.0
     778    150.0
     779     40.0
     780    250.0
     781    560.0
     782    300.0
     783    700.0
     784    200.0
     785    300.0
     786    420.0
     787    600.0
     788    320.0
     789    140.0
     790     30.0
     791    350.0
     792    200.0
     793    250.0
     794    375.0
     795    687.5
     796    375.0
     797     75.0
     798    750.0
     799    437.5
     800    250.0
     801    625.0
     802    250.0
     803    100.0
     804    250.0
     805    250.0
     806    625.0
     807     37.5
     808    100.0
     809    625.0
     810    875.0
     811     25.0
     812    200.0
     813     12.5
     814    125.0
     815    200.0
     816    437.5
     817    112.5
     818    175.0
     819    437.5
     820    550.0
     821    125.0
     822    625.0
     823    312.5
     824    300.0
     825    187.5
     826    250.0
     Name: Revenue, dtype: float64, 32: 827     153.6
     828    1024.0
     829     153.6
     830    1600.0
     831     768.0
     832     320.0
     833     128.0
     834     320.0
     835     640.0
     836     192.0
     837    1120.0
     838    1600.0
     839     480.0
     840     640.0
     841      32.0
     Name: Revenue, dtype: float64, 33: 842     50.0
     843    120.0
     844     48.0
     845     40.0
     846     16.0
     847    120.0
     848     98.0
     849    100.0
     850     40.0
     851     40.0
     852     24.0
     853     40.0
     854     20.0
     855     75.0
     856     37.5
     857     50.0
     858     35.0
     859     35.0
     860     50.0
     861     20.0
     862     75.0
     863     75.0
     864     40.0
     865     10.0
     866     87.5
     867    100.0
     868     75.0
     869     37.5
     870     17.5
     871     75.0
     872     37.5
     873     25.0
     Name: Revenue, dtype: float64, 34: 874     224.0
     875     156.8
     876     112.0
     877     403.2
     878     112.0
     879     224.0
     880     392.0
     881     140.0
     882     560.0
     883     196.0
     884     168.0
     885     420.0
     886     140.0
     887     140.0
     888     280.0
     889     840.0
     890    1260.0
     891     420.0
     892     490.0
     Name: Revenue, dtype: float64, 35: 893     288.0
     894      57.6
     895    1440.0
     896     144.0
     897    1008.0
     898     576.0
     899     432.0
     900     504.0
     901     864.0
     902     115.2
     903      54.0
     904     540.0
     905     360.0
     906     108.0
     907     360.0
     908     360.0
     909      72.0
     910     540.0
     911     540.0
     912     162.0
     913     378.0
     914     630.0
     915     270.0
     916     360.0
     917     144.0
     918     108.0
     919     450.0
     920      72.0
     921     540.0
     922      54.0
     923     180.0
     924     720.0
     925     270.0
     926    1080.0
     927     432.0
     928     324.0
     Name: Revenue, dtype: float64, 36: 929     380.0
     930     456.0
     931     608.0
     932     182.4
     933     304.0
     934     608.0
     935     304.0
     936      91.2
     937      76.0
     938     570.0
     939     570.0
     940    1140.0
     941     475.0
     942     399.0
     943    1045.0
     944     285.0
     945     570.0
     946     114.0
     947      95.0
     948     760.0
     949     114.0
     950     380.0
     951     570.0
     952     950.0
     953     380.0
     954     475.0
     955     570.0
     956     760.0
     957     342.0
     958     304.0
     959     665.0
     Name: Revenue, dtype: float64, 37: 960      20.8
     961     582.4
     962     208.0
     963     468.0
     964    1560.0
     965     208.0
     Name: Revenue, dtype: float64, 38: 966     4216.0
     967     4216.0
     968    10540.0
     969     2108.0
     970     8432.0
     971    10540.0
     972    10329.2
     973     6324.0
     974     3952.5
     975     7905.0
     976     1054.0
     977     3952.5
     978     3952.5
     979     1317.5
     980     2635.0
     981     7905.0
     982     7905.0
     983      527.0
     984     2108.0
     985    15810.0
     986    10540.0
     987     1317.5
     988    15810.0
     989     6587.5
     Name: Revenue, dtype: float64, 39: 990      604.8
     991       86.4
     992      864.0
     993      432.0
     994       57.6
     995      720.0
     996      777.6
     997      288.0
     998       86.4
     999      288.0
     1000     288.0
     1001     180.0
     1002     180.0
     1003      90.0
     1004     378.0
     1005     360.0
     1006     360.0
     1007      54.0
     1008     288.0
     1009    2340.0
     1010      36.0
     1011     378.0
     1012     504.0
     1013     180.0
     1014    1440.0
     1015     810.0
     1016     144.0
     1017     540.0
     1018     360.0
     1019      36.0
     Name: Revenue, dtype: float64, 40: 1020     735.0
     1021     882.0
     1022     588.0
     1023     147.0
     1024     588.0
     1025      58.8
     1026      29.4
     1027     735.0
     1028     294.0
     1029     294.0
     1030     308.7
     1031     147.0
     1032     147.0
     1033      92.0
     1034     460.0
     1035     276.0
     1036     184.0
     1037     184.0
     1038     920.0
     1039      36.8
     1040     772.8
     1041    1104.0
     1042    1288.0
     1043     441.6
     1044     552.0
     1045     368.0
     1046     110.4
     1047     920.0
     1048     736.0
     1049      55.2
     1050      18.4
     1051     552.0
     1052    1104.0
     1053     460.0
     1054     220.8
     1055    1674.4
     1056     368.0
     1057     184.0
     1058     184.0
     1059      92.0
     1060     736.0
     Name: Revenue, dtype: float64, 41: 1061      77.00
     1062     123.20
     1063     192.50
     1064      77.00
     1065     154.00
     1066      92.40
     1067     100.10
     1068      61.60
     1069     192.50
     1070     231.00
     1071     154.00
     1072     772.00
     1073      96.50
     1074      57.90
     1075     135.10
     1076     115.80
     1077      86.85
     1078     193.00
     1079     231.60
     1080    1158.00
     1081      38.60
     1082     405.30
     1083     115.80
     1084     115.80
     1085     337.75
     1086     289.50
     1087      96.50
     1088     193.00
     1089     135.10
     1090     193.00
     1091     193.00
     1092     115.80
     1093     135.10
     1094     289.50
     1095      48.25
     1096      57.90
     1097     231.60
     1098      57.90
     1099      38.60
     1100     337.75
     1101     193.00
     1102     270.20
     1103     289.50
     1104     115.80
     1105      86.85
     1106     386.00
     1107      28.95
     Name: Revenue, dtype: float64, 42: 1108      98.0
     1109      22.4
     1110      67.2
     1111     112.0
     1112     100.8
     1113     448.0
     1114     560.0
     1115     224.0
     1116     420.0
     1117     280.0
     1118     392.0
     1119    1400.0
     1120      70.0
     1121     280.0
     1122     420.0
     1123      84.0
     1124     560.0
     1125     392.0
     1126      28.0
     1127     168.0
     1128     280.0
     1129     588.0
     1130     280.0
     1131     350.0
     1132     140.0
     1133     560.0
     1134     336.0
     1135     196.0
     1136      56.0
     1137     420.0
     Name: Revenue, dtype: float64, 43: 1138     920.0
     1139     552.0
     1140     441.6
     1141     736.0
     1142     883.2
     1143    1472.0
     1144     736.0
     1145     110.4
     1146     552.0
     1147     690.0
     1148    2760.0
     1149    1150.0
     1150     920.0
     1151     276.0
     1152    1840.0
     1153    1104.0
     1154    1380.0
     1155     920.0
     1156     322.0
     1157     414.0
     1158     230.0
     1159     460.0
     1160    1104.0
     1161     414.0
     1162     276.0
     1163    1380.0
     1164    1380.0
     1165    1656.0
     Name: Revenue, dtype: float64, 44: 1166     248.00
     1167     325.50
     1168     372.00
     1169    1193.50
     1170     620.00
     1171    1550.00
     1172      31.00
     1173     232.50
     1174     175.05
     1175     778.00
     1176     194.50
     1177     408.45
     1178     194.50
     1179     544.60
     1180     408.45
     1181     466.80
     1182     972.50
     1183     311.20
     1184     194.50
     1185     311.20
     1186     350.10
     1187     116.70
     1188     233.40
     1189     291.75
     Name: Revenue, dtype: float64, 45: 1190     114.0
     1191     228.0
     1192     199.5
     1193     950.0
     1194     190.0
     1195    1045.0
     1196     380.0
     1197     380.0
     1198      38.0
     1199     256.5
     1200     342.0
     1201     142.5
     1202     285.0
     1203     190.0
     Name: Revenue, dtype: float64, 46: 1204    144.0
     1205    288.0
     1206    432.0
     1207    268.8
     1208     19.2
     1209    192.0
     1210     48.0
     1211     96.0
     1212    192.0
     1213     48.0
     1214    108.0
     1215     24.0
     1216    252.0
     1217    540.0
     1218    720.0
     1219    216.0
     1220    288.0
     1221    336.0
     1222    420.0
     1223    252.0
     1224    180.0
     1225    108.0
     1226    240.0
     1227    300.0
     1228     36.0
     1229    360.0
     1230     36.0
     Name: Revenue, dtype: float64, 47: 1231    121.6
     1232    418.0
     1233    228.0
     1234    228.0
     1235     57.0
     1236    237.5
     1237    142.5
     1238     57.0
     1239     95.0
     1240    380.0
     1241    142.5
     1242    114.0
     1243     47.5
     1244    475.0
     1245    285.0
     1246    285.0
     1247    380.0
     1248    199.5
     1249     47.5
     1250    133.0
     1251    285.0
     Name: Revenue, dtype: float64, 48: 1252    714.00
     1253    153.00
     1254    191.25
     1255     76.50
     1256    306.00
     1257    102.00
     Name: Revenue, dtype: float64, 49: 1258     640.0
     1259     240.0
     1260     480.0
     1261     560.0
     1262     480.0
     1263     480.0
     1264     336.0
     1265     384.0
     1266     500.0
     1267     120.0
     1268     500.0
     1269     360.0
     1270      80.0
     1271     840.0
     1272     300.0
     1273     400.0
     1274     200.0
     1275     560.0
     1276     800.0
     1277      40.0
     1278    1200.0
     Name: Revenue, dtype: float64, 50: 1279    195.00
     1280    195.00
     1281    520.00
     1282    325.00
     1283    406.25
     1284    650.00
     1285    325.00
     1286    390.00
     1287    146.25
     1288    357.50
     Name: Revenue, dtype: float64, 51: 1289    1696.0
     1290    1484.0
     1291      84.8
     1292    2035.2
     1293     848.0
     1294     763.2
     1295     763.2
     1296     127.2
     1297    1060.0
     1298     318.0
     1299    2544.0
     1300    1060.0
     1301    1060.0
     1302    2650.0
     1303     159.0
     1304     795.0
     1305    1060.0
     1306    1060.0
     1307    1484.0
     1308     371.0
     1309    1590.0
     1310    1484.0
     1311    6360.0
     1312     530.0
     1313    1590.0
     1314     318.0
     1315     212.0
     1316     159.0
     1317     106.0
     1318    2120.0
     1319     424.0
     1320     848.0
     1321     530.0
     1322    1060.0
     1323     795.0
     1324    2332.0
     1325     530.0
     1326    1272.0
     1327    1060.0
     Name: Revenue, dtype: float64, 52: 1328    112.0
     1329     44.8
     1330    112.0
     1331     84.0
     1332    112.0
     1333     42.0
     1334    210.0
     1335    490.0
     1336     28.0
     1337    168.0
     1338     35.0
     1339     63.0
     1340     28.0
     1341    175.0
     1342    126.0
     1343    420.0
     1344    105.0
     1345     56.0
     1346    140.0
     1347     56.0
     1348     98.0
     1349     84.0
     1350     35.0
     1351     42.0
     1352    280.0
     1353    140.0
     1354     70.0
     1355     14.0
     1356     14.0
     Name: Revenue, dtype: float64, 53: 1357     393.0
     1358     943.2
     1359     262.0
     1360     524.0
     1361     524.0
     1362    1048.0
     1363    1834.0
     1364     262.0
     1365     393.0
     1366     393.0
     1367    1310.0
     1368     733.6
     1369     196.8
     1370     328.0
     1371     164.0
     1372     590.4
     1373     820.0
     1374     393.6
     1375     820.0
     1376     328.0
     1377    3936.0
     1378      98.4
     1379     656.0
     1380     295.2
     1381      98.4
     1382      65.6
     1383     656.0
     1384    2296.0
     1385     328.0
     1386     820.0
     Name: Revenue, dtype: float64, 54: 1387     59.00
     1388     29.50
     1389     88.50
     1390    141.60
     1391    118.00
     1392    165.20
     1393    141.60
     1394    106.20
     1395     59.00
     1396     35.40
     1397    236.00
     1398    472.00
     1399     88.50
     1400     35.40
     1401    141.60
     1402    149.00
     1403    111.75
     1404     74.50
     1405    178.80
     1406    372.50
     1407     29.80
     1408    223.50
     1409     44.70
     1410    223.50
     1411    447.00
     1412    111.75
     1413    298.00
     1414     22.35
     1415     22.35
     1416     44.70
     1417     52.15
     1418    260.75
     1419    238.40
     1420     74.50
     1421     74.50
     1422    149.00
     Name: Revenue, dtype: float64, 55: 1423     403.2
     1424     384.0
     1425     768.0
     1426     230.4
     1427     288.0
     1428    2304.0
     1429     192.0
     1430    2304.0
     1431    1152.0
     1432      38.4
     1433     576.0
     1434     336.0
     1435     432.0
     1436     600.0
     1437     480.0
     1438     120.0
     1439     288.0
     1440      96.0
     1441     504.0
     1442     144.0
     1443     288.0
     1444    1440.0
     1445     240.0
     1446     720.0
     1447     600.0
     1448      96.0
     1449    1560.0
     1450     144.0
     1451     960.0
     1452     840.0
     1453     840.0
     1454      96.0
     1455      48.0
     Name: Revenue, dtype: float64, 56: 1456      60.8
     1457     121.6
     1458     608.0
     1459     364.8
     1460     608.0
     1461     547.2
     1462     608.0
     1463    2128.0
     1464     152.0
     1465     912.0
     1466     851.2
     1467    1216.0
     1468     456.0
     1469     912.0
     1470     608.0
     1471     912.0
     1472     425.6
     1473    2660.0
     1474    1520.0
     1475    1140.0
     1476    1520.0
     1477    2280.0
     1478     190.0
     1479    1064.0
     1480     532.0
     1481     760.0
     1482    2280.0
     1483    1710.0
     1484     456.0
     1485     760.0
     1486    1140.0
     1487     684.0
     1488     380.0
     1489     532.0
     1490    1064.0
     1491     570.0
     1492    1140.0
     1493    2280.0
     1494     760.0
     1495     760.0
     1496     760.0
     1497    1140.0
     1498    1140.0
     1499     912.0
     1500     798.0
     1501     608.0
     1502     684.0
     1503     456.0
     1504     190.0
     1505     760.0
     Name: Revenue, dtype: float64, 57: 1506    234.0
     1507    780.0
     1508     31.2
     1509    249.6
     1510    390.0
     1511    390.0
     1512    312.0
     1513    234.0
     1514     97.5
     1515    117.0
     1516     78.0
     1517    390.0
     1518    780.0
     1519    273.0
     1520    292.5
     1521    292.5
     1522    468.0
     1523    195.0
     1524    390.0
     1525    585.0
     1526    292.5
     1527    546.0
     1528    390.0
     Name: Revenue, dtype: float64, 58: 1529    318.00
     1530    318.00
     1531    848.00
     1532    159.00
     1533    265.00
     1534    397.50
     1535     79.50
     1536    649.25
     1537    397.50
     1538    397.50
     1539    159.00
     1540    397.50
     1541    795.00
     1542    159.00
     1543    198.75
     1544    198.75
     1545    397.50
     1546    530.00
     Name: Revenue, dtype: float64, 59: 1547    1320.0
     1548    3080.0
     1549     264.0
     1550     660.0
     1551    1320.0
     1552     440.0
     1553    1760.0
     1554     396.0
     1555     396.0
     1556     528.0
     1557     704.0
     1558     396.0
     1559     880.0
     1560    3080.0
     1561    1584.0
     1562    2640.0
     1563     528.0
     1564    1320.0
     1565    2640.0
     1566     220.0
     1567     110.0
     1568     825.0
     1569    2200.0
     1570     660.0
     1571    1925.0
     1572    1100.0
     1573    1650.0
     1574      55.0
     1575     660.0
     1576    1375.0
     1577    2310.0
     1578    1925.0
     1579     440.0
     1580     550.0
     1581    2475.0
     1582     330.0
     1583    1375.0
     1584     385.0
     1585    1375.0
     1586    1375.0
     1587     825.0
     1588    2200.0
     1589     825.0
     1590    2750.0
     1591    2310.0
     1592    2200.0
     1593     220.0
     1594     990.0
     1595     550.0
     1596    6050.0
     1597    1320.0
     1598    5500.0
     1599    1650.0
     1600    1650.0
     Name: Revenue, dtype: float64, 60: 1601    1088.0
     1602     952.0
     1603     544.0
     1604     571.2
     1605     217.6
     1606    2176.0
     1607    1496.0
     1608    1904.0
     1609     163.2
     1610     408.0
     1611     544.0
     1612    1632.0
     1613     544.0
     1614    1088.0
     1615     408.0
     1616    2856.0
     1617     340.0
     1618    1190.0
     1619     816.0
     1620    2380.0
     1621     510.0
     1622    1360.0
     1623     340.0
     1624     680.0
     1625     680.0
     1626    1020.0
     1627    1870.0
     1628    1020.0
     1629     340.0
     1630     510.0
     1631    1700.0
     1632     510.0
     1633     714.0
     1634    1020.0
     1635    2040.0
     1636    1530.0
     1637    3400.0
     1638     340.0
     1639     850.0
     1640    1666.0
     1641     816.0
     1642      68.0
     1643     136.0
     1644     306.0
     1645    1224.0
     1646    1700.0
     1647     714.0
     1648    1190.0
     1649     136.0
     1650     510.0
     1651      68.0
     Name: Revenue, dtype: float64, 61: 1652     364.8
     1653    2052.0
     1654     570.0
     1655     712.5
     1656     427.5
     1657     570.0
     1658     285.0
     1659    3420.0
     1660     570.0
     1661     285.0
     1662     142.5
     1663     570.0
     1664     570.0
     1665     855.0
     1666     855.0
     1667     427.5
     1668     142.5
     1669     855.0
     1670    1881.0
     1671     199.5
     1672     171.0
     1673     114.0
     1674     285.0
     1675     114.0
     Name: Revenue, dtype: float64, 62: 1676     591.0
     1677     472.8
     1678    1576.0
     1679     591.0
     1680     394.0
     1681     197.0
     1682     985.0
     1683    2758.0
     1684    1103.2
     1685     788.0
     1686     394.0
     1687    1379.0
     1688    1576.0
     1689    1379.0
     1690     147.9
     1691    1972.0
     1692     986.0
     1693     739.5
     1694     493.0
     1695     493.0
     1696     493.0
     1697     493.0
     1698     739.5
     1699    3944.0
     1700     493.0
     1701    2366.4
     1702     986.0
     1703     443.7
     1704    1479.0
     1705     739.5
     1706     986.0
     1707      98.6
     1708     246.5
     1709     986.0
     1710    1232.5
     1711     147.9
     1712    2465.0
     1713     147.9
     1714     986.0
     1715     295.8
     1716    1725.5
     1717     690.2
     1718    1479.0
     1719    2958.0
     1720     591.6
     1721    1972.0
     1722    1035.3
     1723     591.6
     Name: Revenue, dtype: float64, 63: 1724     280.8
     1725     175.5
     1726    2808.0
     1727     561.6
     1728    2281.5
     1729    1228.5
     1730     263.4
     1731    1053.6
     1732     878.0
     1733     395.1
     1734    1317.0
     1735    1756.0
     1736     439.0
     1737     878.0
     1738    1536.5
     1739     526.8
     1740    1317.0
     Name: Revenue, dtype: float64, 64: 1741     239.40
     1742    1330.00
     1743     931.00
     1744     798.00
     1745     186.20
     1746     798.00
     1747     159.60
     1748     931.00
     1749     212.80
     1750     798.00
     1751     997.50
     1752     598.50
     1753     199.50
     1754     299.25
     1755     498.75
     1756     931.00
     1757     798.00
     1758    1163.75
     1759      99.75
     1760     997.50
     1761    1596.00
     1762     997.50
     1763     498.75
     1764     665.00
     1765     266.00
     1766     133.00
     1767     665.00
     1768     831.25
     1769    4322.50
     1770      66.50
     Name: Revenue, dtype: float64, 65: 1771     252.00
     1772     336.00
     1773     504.00
     1774     672.00
     1775     168.00
     1776      84.00
     1777     252.00
     1778     336.00
     1779     336.00
     1780     588.00
     1781     470.40
     1782     252.00
     1783     421.00
     1784     820.95
     1785     757.80
     1786     631.50
     1787     252.60
     1788     442.05
     1789     315.75
     1790     210.50
     1791     252.60
     1792    1368.25
     1793     210.50
     1794     842.00
     1795    1684.00
     1796      42.10
     1797     315.75
     1798     442.05
     1799     210.50
     1800     252.60
     1801     442.05
     1802     442.05
     Name: Revenue, dtype: float64, 66: 1803    408.0
     1804    816.0
     1805    816.0
     1806    136.0
     1807    408.0
     1808     68.0
     1809    850.0
     1810     17.0
     Name: Revenue, dtype: float64, 67: 1811     56.0
     1812    420.0
     1813     98.0
     1814    350.0
     1815     42.0
     1816    210.0
     1817    210.0
     1818    336.0
     1819    560.0
     1820    280.0
     Name: Revenue, dtype: float64, 68: 1821      30.0
     1822     200.0
     1823     150.0
     1824      30.0
     1825     100.0
     1826     100.0
     1827      40.0
     1828      80.0
     1829     600.0
     1830     360.0
     1831     300.0
     1832     210.0
     1833     300.0
     1834      75.0
     1835     250.0
     1836     437.5
     1837     187.5
     1838     225.0
     1839     125.0
     1840     500.0
     1841     562.5
     1842      75.0
     1843     500.0
     1844     225.0
     1845     187.5
     1846     300.0
     1847     250.0
     1848     250.0
     1849     225.0
     1850     250.0
     1851    1000.0
     1852      25.0
     1853     525.0
     1854     687.5
     Name: Revenue, dtype: float64, 69: 1855     432.0
     1856      28.8
     1857     201.6
     1858     518.4
     1859     576.0
     1860     864.0
     1861    1440.0
     1862     230.4
     1863     432.0
     1864     576.0
     1865     288.0
     1866     360.0
     1867     648.0
     1868     360.0
     1869     720.0
     1870    2340.0
     1871     720.0
     1872    1620.0
     1873    1080.0
     1874     900.0
     1875    1440.0
     1876    1080.0
     1877     108.0
     1878     900.0
     1879     720.0
     1880     864.0
     1881    1800.0
     1882     324.0
     1883     360.0
     1884    1080.0
     1885    1296.0
     Name: Revenue, dtype: float64, 70: 1886    252.0
     1887    240.0
     1888    240.0
     1889     60.0
     1890    360.0
     1891    360.0
     1892    360.0
     1893     96.0
     1894    300.0
     1895    144.0
     1896    720.0
     1897    210.0
     1898     90.0
     1899    105.0
     1900    225.0
     1901    300.0
     1902    225.0
     1903    600.0
     1904    750.0
     1905    450.0
     1906    120.0
     1907    420.0
     1908    600.0
     1909    525.0
     1910     75.0
     1911     90.0
     1912    135.0
     1913    180.0
     1914    450.0
     1915    450.0
     1916     60.0
     1917    750.0
     1918    450.0
     1919     45.0
     1920    300.0
     1921    450.0
     1922     60.0
     1923     45.0
     1924    180.0
     Name: Revenue, dtype: float64, 71: 1925     344.0
     1926      34.4
     1927      51.6
     1928     516.0
     1929     688.0
     1930      86.0
     1931     860.0
     1932     103.2
     1933     258.0
     1934    1032.0
     1935     516.0
     1936    1032.0
     1937     258.0
     1938      34.4
     1939     516.0
     1940     860.0
     1941     206.4
     1942     193.5
     1943     193.5
     1944     322.5
     1945     322.5
     1946     322.5
     1947     430.0
     1948     645.0
     1949     301.0
     1950     258.0
     1951    1290.0
     1952     430.0
     1953     645.0
     1954     172.0
     1955     258.0
     1956     344.0
     1957    1182.5
     1958     645.0
     1959     537.5
     1960     752.5
     1961     451.5
     1962     430.0
     1963    1290.0
     1964    1075.0
     1965     344.0
     1966     645.0
     Name: Revenue, dtype: float64, 72: 1967     174.0
     1968     111.2
     1969     556.0
     1970     667.2
     1971     194.6
     1972      83.4
     1973     556.0
     1974    1112.0
     1975     695.0
     1976     695.0
     1977    1167.6
     1978     667.2
     1979     583.8
     1980     278.0
     1981    1112.0
     1982     695.0
     1983     313.2
     1984     835.2
     1985     730.8
     1986      34.8
     1987     835.2
     1988    1044.0
     1989     417.6
     1990    2088.0
     1991     522.0
     1992    1218.0
     1993     243.6
     1994    1044.0
     1995     348.0
     1996    1392.0
     1997     522.0
     1998     348.0
     1999     556.8
     2000    1740.0
     2001     174.0
     2002     696.0
     2003      69.6
     2004    1218.0
     Name: Revenue, dtype: float64, 73: 2005    300.0
     2006    240.0
     2007    240.0
     2008    360.0
     2009    135.0
     2010     45.0
     2011    450.0
     2012    525.0
     2013    750.0
     2014    225.0
     2015    525.0
     2016    225.0
     2017    150.0
     2018     30.0
     Name: Revenue, dtype: float64, 74: 2019    168.0
     2020    288.0
     2021    160.0
     2022    112.0
     2023    400.0
     2024    120.0
     2025    240.0
     2026    128.0
     2027     50.0
     2028    350.0
     2029    150.0
     2030    200.0
     2031    200.0
     Name: Revenue, dtype: float64, 75: 2032    186.00
     2033     37.20
     2034     37.20
     2035     62.00
     2036    310.00
     2037     37.20
     2038     74.40
     2039    148.80
     2040     24.80
     2041     62.00
     2042    223.20
     2043    279.00
     2044    387.50
     2045    232.50
     2046    155.00
     2047    116.25
     2048    155.00
     2049    162.75
     2050    387.50
     2051    232.50
     2052    310.00
     2053     62.00
     2054     15.50
     2055    193.75
     2056    232.50
     2057    325.50
     2058    155.00
     2059    139.50
     2060     54.25
     2061     77.50
     2062    325.50
     2063    310.00
     2064    155.00
     2065    930.00
     2066    108.50
     2067     46.50
     2068    379.75
     2069    155.00
     2070    387.50
     2071     93.00
     2072    155.00
     2073     77.50
     2074     77.50
     2075    310.00
     2076    232.50
     2077     31.00
     Name: Revenue, dtype: float64, 76: 2078     216.0
     2079     475.2
     2080      86.4
     2081     432.0
     2082     216.0
     2083     172.8
     2084     504.0
     2085     201.6
     2086     288.0
     2087     259.2
     2088     604.8
     2089     900.0
     2090     180.0
     2091     540.0
     2092     180.0
     2093     252.0
     2094      72.0
     2095     180.0
     2096    1440.0
     2097     630.0
     2098     180.0
     2099     630.0
     2100     270.0
     2101     360.0
     2102     360.0
     2103     180.0
     2104     900.0
     2105     378.0
     2106     360.0
     2107     180.0
     2108     360.0
     2109      90.0
     2110    1080.0
     2111     792.0
     2112     180.0
     2113    1620.0
     2114     108.0
     2115     900.0
     2116      36.0
     Name: Revenue, dtype: float64, 77: 2117    124.8
     2118    156.0
     2119    104.0
     2120     52.0
     2121     72.8
     2122    145.6
     2123    364.0
     2124    104.0
     2125    572.0
     2126    312.0
     2127     72.8
     2128     52.0
     2129    260.0
     2130    130.0
     2131    234.0
     2132    260.0
     2133    780.0
     2134     65.0
     2135    455.0
     2136    910.0
     2137    390.0
     2138     26.0
     2139    195.0
     2140    260.0
     2141    195.0
     2142     26.0
     2143    195.0
     2144    325.0
     2145    520.0
     2146    195.0
     2147    520.0
     2148    195.0
     2149    273.0
     2150    390.0
     2151    234.0
     2152    130.0
     2153    364.0
     2154     26.0
     Name: Revenue, dtype: float64}



## Outlier Removal & Normality Test


```python
clean_data_revenue = {}
clean_list = []
for k, v in data_2.items():
    
    idx_outs = find_outliers_Z(v)
    data_clean = v[~idx_outs].copy()
    clean_list.append(data_clean)
    stat, p = stats.shapiro(data_clean)
    print(f"For {k} normal test, p = {round(p, 4)}, n = {len(data_clean)}")
    clean_data_revenue[k] = data_clean
```

    For 1 normal test, p = 0.001, n = 37
    For 2 normal test, p = 0.0029, n = 43
    For 3 normal test, p = 0.4441, n = 12
    For 4 normal test, p = 0.0331, n = 20
    For 5 normal test, p = 0.1788, n = 10
    For 6 normal test, p = 0.2286, n = 12
    For 7 normal test, p = 0.0023, n = 29
    For 8 normal test, p = 0.3593, n = 13
    For 9 normal test, p = 0.0947, n = 5
    For 10 normal test, p = 0.0, n = 32
    For 11 normal test, p = 0.0003, n = 38
    For 12 normal test, p = 0.2891, n = 13
    For 13 normal test, p = 0.0, n = 40
    For 14 normal test, p = 0.1238, n = 21
    For 15 normal test, p = 0.1803, n = 6
    For 16 normal test, p = 0.0587, n = 43
    For 17 normal test, p = 0.0018, n = 36
    For 18 normal test, p = 0.067, n = 27
    For 19 normal test, p = 0.0003, n = 36
    For 20 normal test, p = 0.1326, n = 16
    For 21 normal test, p = 0.0051, n = 39
    For 22 normal test, p = 0.3411, n = 14
    For 23 normal test, p = 0.0355, n = 20
    For 24 normal test, p = 0.0001, n = 49
    For 25 normal test, p = 0.0049, n = 18
    For 26 normal test, p = 0.017, n = 32
    For 27 normal test, p = 0.0081, n = 9
    For 28 normal test, p = 0.001, n = 32
    For 29 normal test, p = 0.0003, n = 31
    For 30 normal test, p = 0.0978, n = 32
    For 31 normal test, p = 0.0091, n = 51
    For 32 normal test, p = 0.0468, n = 15
    For 33 normal test, p = 0.0114, n = 32
    For 34 normal test, p = 0.0087, n = 18
    For 35 normal test, p = 0.0103, n = 35
    For 36 normal test, p = 0.1241, n = 31
    For 37 normal test, p = 0.0813, n = 6
    For 38 normal test, p = 0.0553, n = 24
    For 39 normal test, p = 0.0013, n = 29
    For 40 normal test, p = 0.0053, n = 40
    For 41 normal test, p = 0.0045, n = 45
    For 42 normal test, p = 0.0581, n = 29
    For 43 normal test, p = 0.2501, n = 27
    For 44 normal test, p = 0.0024, n = 23
    For 45 normal test, p = 0.0013, n = 14
    For 46 normal test, p = 0.0417, n = 27
    For 47 normal test, p = 0.1369, n = 21
    For 48 normal test, p = 0.0405, n = 6
    For 49 normal test, p = 0.2175, n = 21
    For 50 normal test, p = 0.6215, n = 10
    For 51 normal test, p = 0.0271, n = 38
    For 52 normal test, p = 0.0002, n = 28
    For 53 normal test, p = 0.0002, n = 29
    For 54 normal test, p = 0.0003, n = 36
    For 55 normal test, p = 0.0, n = 33
    For 56 normal test, p = 0.0001, n = 50
    For 57 normal test, p = 0.1337, n = 23
    For 58 normal test, p = 0.0614, n = 18
    For 59 normal test, p = 0.0056, n = 52
    For 60 normal test, p = 0.0046, n = 50
    For 61 normal test, p = 0.0001, n = 23
    For 62 normal test, p = 0.0006, n = 47
    For 63 normal test, p = 0.116, n = 17
    For 64 normal test, p = 0.1032, n = 29
    For 65 normal test, p = 0.001, n = 31
    For 66 normal test, p = 0.1114, n = 8
    For 67 normal test, p = 0.7502, n = 10
    For 68 normal test, p = 0.0161, n = 33
    For 69 normal test, p = 0.0416, n = 31
    For 70 normal test, p = 0.0061, n = 39
    For 71 normal test, p = 0.006, n = 42
    For 72 normal test, p = 0.1319, n = 37
    For 73 normal test, p = 0.4079, n = 14
    For 74 normal test, p = 0.4518, n = 13
    For 75 normal test, p = 0.0043, n = 45
    For 76 normal test, p = 0.0001, n = 38
    For 77 normal test, p = 0.0073, n = 37


### After running this normality test, we received a mixed bag of results in terms of significant or insignificant p-values for each product. Also, there are a few groups that have a small number of samples (<20). Therefore we will move past testing for equal variance and perform the non-parametric version of an ANOVA test.

## Hypothesis Test: Non-Parametric ANOVA (Alpha = .05)


```python
stats.kruskal(*clean_list)
```




    KruskalResult(statistic=947.2946660406544, pvalue=1.5343308499647505e-150)



### With a very significant p-value being recorded, we can confidently reject our null hypothesis and state that discounts have a signifcant statistical effect on revenue. Now, we will run another Tukey's test to compare the signficance of revenue changes between products.

## Tukey's Test


```python
df_rev_tukey = prep_data_for_tukeys(clean_data_revenue)
```


```python
results = pairwise_tukeyhsd(df_rev_tukey['data'].values, df_rev_tukey['group'].values)
results.summary()
```




<table class="simpletable">
<caption>Multiple Comparison of Means - Tukey HSD, FWER=0.05</caption>
<tr>
  <th>group1</th> <th>group2</th>  <th>meandiff</th>   <th>p-adj</th>    <th>lower</th>      <th>upper</th>   <th>reject</th>
</tr>
<tr>
     <td>1</td>     <td>10</td>    <td>248.0441</td>    <td>0.9</td>   <td>-431.6704</td>  <td>927.7585</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>11</td>     <td>18.8799</td>    <td>0.9</td>   <td>-631.4231</td>   <td>669.183</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>12</td>     <td>350.484</td>    <td>0.9</td>   <td>-557.3162</td>  <td>1258.2842</td>  <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>13</td>    <td>-216.1022</td>   <td>0.9</td>   <td>-858.3347</td>  <td>426.1304</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>14</td>    <td>-13.4907</td>    <td>0.9</td>   <td>-782.7652</td>  <td>755.7837</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>15</td>    <td>-44.7122</td>    <td>0.9</td>  <td>-1283.8954</td>  <td>1194.4711</td>  <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>16</td>     <td>89.039</td>     <td>0.9</td>   <td>-542.3365</td>  <td>720.4145</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>17</td>    <td>530.3212</td>  <td>0.5024</td>  <td>-128.8332</td>  <td>1189.4755</td>  <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>18</td>    <td>837.7601</td>  <td>0.0022</td>  <td>125.0957</td>   <td>1550.4244</td>  <td>True</td> 
</tr>
<tr>
     <td>1</td>     <td>19</td>    <td>-192.0872</td>   <td>0.9</td>   <td>-851.2415</td>  <td>467.0672</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>      <td>2</td>     <td>40.4611</td>    <td>0.9</td>   <td>-590.9144</td>  <td>671.8366</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>20</td>    <td>1130.2753</td>  <td>0.001</td>  <td>287.8045</td>   <td>1972.7462</td>  <td>True</td> 
</tr>
<tr>
     <td>1</td>     <td>21</td>    <td>-99.8852</td>    <td>0.9</td>   <td>-746.0621</td>  <td>546.2917</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>22</td>    <td>169.6378</td>    <td>0.9</td>   <td>-713.8448</td>  <td>1053.1205</td>  <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>23</td>    <td>-104.9522</td>   <td>0.9</td>   <td>-886.3989</td>  <td>676.4946</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>24</td>    <td>-266.8071</td>   <td>0.9</td>   <td>-880.0437</td>  <td>346.4296</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>25</td>    <td>-121.8733</td>   <td>0.9</td>   <td>-931.0102</td>  <td>687.2637</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>26</td>    <td>326.0035</td>    <td>0.9</td>   <td>-353.711</td>   <td>1005.7179</td>  <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>27</td>    <td>1345.4267</td>  <td>0.001</td>  <td>298.9379</td>   <td>2391.9156</td>  <td>True</td> 
</tr>
<tr>
     <td>1</td>     <td>28</td>    <td>392.8378</td>    <td>0.9</td>   <td>-286.8766</td>  <td>1072.5523</td>  <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>29</td>    <td>2163.7862</td>  <td>0.001</td>  <td>1478.2182</td>  <td>2849.3542</td>  <td>True</td> 
</tr>
<tr>
     <td>1</td>      <td>3</td>    <td>-90.2955</td>    <td>0.9</td>  <td>-1025.6675</td>  <td>845.0765</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>30</td>    <td>114.7735</td>    <td>0.9</td>   <td>-564.941</td>   <td>794.4879</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>31</td>    <td>-29.8543</td>    <td>0.9</td>   <td>-637.8958</td>  <td>578.1871</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>32</td>    <td>264.4512</td>    <td>0.9</td>   <td>-597.4014</td>  <td>1126.3037</td>  <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>33</td>    <td>-293.4153</td>   <td>0.9</td>   <td>-973.1297</td>  <td>386.2992</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>34</td>    <td>-45.9622</td>    <td>0.9</td>   <td>-855.0991</td>  <td>763.1748</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>35</td>     <td>27.2321</td>    <td>0.9</td>   <td>-636.6778</td>  <td>691.1421</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>36</td>     <td>122.154</td>    <td>0.9</td>   <td>-563.4141</td>   <td>807.722</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>37</td>    <td>160.9045</td>    <td>0.9</td>  <td>-1078.2788</td>  <td>1400.0878</td>  <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>38</td>    <td>5902.3795</td>  <td>0.001</td>  <td>5164.4137</td>  <td>6640.3453</td>  <td>True</td> 
</tr>
<tr>
     <td>1</td>     <td>39</td>     <td>25.824</td>     <td>0.9</td>   <td>-672.4886</td>  <td>724.1367</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>      <td>4</td>    <td>124.2778</td>    <td>0.9</td>   <td>-657.1689</td>  <td>905.7246</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>40</td>     <td>87.3853</td>    <td>0.9</td>   <td>-554.8472</td>  <td>729.6179</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>41</td>    <td>-187.6711</td>   <td>0.9</td>   <td>-812.5237</td>  <td>437.1816</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>42</td>    <td>-73.4311</td>    <td>0.9</td>   <td>-771.7438</td>  <td>624.8815</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>43</td>    <td>479.6749</td>    <td>0.9</td>   <td>-232.9895</td>  <td>1192.3392</td>  <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>44</td>     <td>43.2204</td>    <td>0.9</td>   <td>-704.4129</td>  <td>790.8538</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>45</td>     <td>-8.355</td>     <td>0.9</td>   <td>-891.8376</td>  <td>875.1276</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>46</td>    <td>-119.4066</td>   <td>0.9</td>   <td>-832.071</td>   <td>593.2578</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>47</td>    <td>-139.4098</td>   <td>0.9</td>   <td>-908.6842</td>  <td>629.8646</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>48</td>    <td>-89.8372</td>    <td>0.9</td>  <td>-1329.0204</td>  <td>1149.3461</td>  <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>49</td>    <td>105.4188</td>    <td>0.9</td>   <td>-663.8556</td>  <td>874.6932</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>      <td>5</td>    <td>233.1528</td>    <td>0.9</td>   <td>-770.3668</td>  <td>1236.6725</td>  <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>50</td>     <td>4.0378</td>     <td>0.9</td>   <td>-999.4818</td>  <td>1007.5575</td>  <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>51</td>    <td>663.1063</td>  <td>0.0369</td>   <td>12.8032</td>   <td>1313.4093</td>  <td>True</td> 
</tr>
<tr>
     <td>1</td>     <td>52</td>    <td>-243.6122</td>   <td>0.9</td>   <td>-948.8809</td>  <td>461.6565</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>53</td>    <td>259.0447</td>    <td>0.9</td>   <td>-439.2679</td>  <td>957.3574</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>54</td>    <td>-204.7122</td>   <td>0.9</td>   <td>-863.8665</td>  <td>454.4422</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>55</td>    <td>244.3106</td>    <td>0.9</td>   <td>-429.8588</td>  <td>918.4799</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>56</td>    <td>555.4618</td>   <td>0.175</td>  <td>-55.1308</td>   <td>1166.0545</td>  <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>57</td>     <td>-7.4926</td>    <td>0.9</td>   <td>-755.1259</td>  <td>740.1407</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>58</td>     <td>23.3017</td>    <td>0.9</td>   <td>-785.8352</td>  <td>832.4387</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>59</td>    <td>898.1532</td>   <td>0.001</td>   <td>292.575</td>   <td>1503.7315</td>  <td>True</td> 
</tr>
<tr>
     <td>1</td>      <td>6</td>    <td>265.1212</td>    <td>0.9</td>   <td>-670.2508</td>  <td>1200.4932</td>  <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>60</td>    <td>590.7578</td>  <td>0.0823</td>  <td>-19.8348</td>   <td>1201.3505</td>  <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>61</td>    <td>219.0726</td>    <td>0.9</td>   <td>-528.5607</td>  <td>966.7059</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>62</td>     <td>629.291</td>  <td>0.0386</td>   <td>10.4663</td>   <td>1248.1158</td>  <td>True</td> 
</tr>
<tr>
     <td>1</td>     <td>63</td>    <td>693.9967</td>   <td>0.373</td>  <td>-130.9946</td>  <td>1518.9879</td>  <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>64</td>    <td>297.3999</td>    <td>0.9</td>   <td>-400.9127</td>  <td>995.7126</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>65</td>     <td>69.9088</td>    <td>0.9</td>   <td>-615.6592</td>  <td>755.4768</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>66</td>     <td>92.9128</td>    <td>0.9</td>   <td>-1004.925</td>  <td>1190.7507</td>  <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>67</td>    <td>-90.7622</td>    <td>0.9</td>  <td>-1094.2818</td>  <td>912.7575</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>68</td>    <td>-93.5531</td>    <td>0.9</td>   <td>-767.7224</td>  <td>580.6163</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>69</td>    <td>437.1411</td>    <td>0.9</td>   <td>-248.427</td>   <td>1122.7091</td>  <td>False</td>
</tr>
<tr>
     <td>1</td>      <td>7</td>    <td>427.6585</td>    <td>0.9</td>   <td>-270.6541</td>  <td>1125.9712</td>  <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>70</td>    <td>-52.8083</td>    <td>0.9</td>   <td>-698.9852</td>  <td>593.3686</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>71</td>    <td>150.0974</td>    <td>0.9</td>   <td>-484.7449</td>  <td>784.9396</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>72</td>    <td>292.2486</td>    <td>0.9</td>   <td>-362.3754</td>  <td>946.8727</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>73</td>    <td>-46.9622</td>    <td>0.9</td>   <td>-930.4448</td>  <td>836.5205</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>74</td>    <td>-149.5775</td>   <td>0.9</td>  <td>-1057.3777</td>  <td>758.2226</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>75</td>    <td>-175.3944</td>   <td>0.9</td>   <td>-800.247</td>   <td>449.4583</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>76</td>     <td>52.3536</td>    <td>0.9</td>   <td>-597.9494</td>  <td>702.6567</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>     <td>77</td>     <td>-109.8</td>     <td>0.9</td>   <td>-764.424</td>    <td>544.824</td>   <td>False</td>
</tr>
<tr>
     <td>1</td>      <td>8</td>    <td>711.4994</td>  <td>0.5661</td>  <td>-196.3008</td>  <td>1619.2996</td>  <td>False</td>
</tr>
<tr>
     <td>1</td>      <td>9</td>    <td>1418.4378</td> <td>0.0197</td>   <td>76.8578</td>   <td>2760.0179</td>  <td>True</td> 
</tr>
<tr>
    <td>10</td>     <td>11</td>    <td>-229.1641</td>   <td>0.9</td>   <td>-904.7181</td>  <td>446.3898</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>12</td>    <td>102.4399</td>    <td>0.9</td>   <td>-823.6164</td>  <td>1028.4962</td>  <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>13</td>    <td>-464.1462</td> <td>0.8379</td>  <td>-1131.935</td>  <td>203.6425</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>14</td>    <td>-261.5348</td>   <td>0.9</td>  <td>-1052.2701</td>  <td>529.2004</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>15</td>    <td>-292.7562</td>   <td>0.9</td>  <td>-1545.3752</td>  <td>959.8627</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>16</td>    <td>-159.0051</td>   <td>0.9</td>   <td>-816.3589</td>  <td>498.3488</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>17</td>    <td>282.2771</td>    <td>0.9</td>   <td>-401.8015</td>  <td>966.3557</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>18</td>     <td>589.716</td>  <td>0.5118</td>  <td>-146.0623</td>  <td>1325.4942</td>  <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>19</td>    <td>-440.1312</td>   <td>0.9</td>  <td>-1124.2099</td>  <td>243.9474</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>      <td>2</td>    <td>-207.583</td>    <td>0.9</td>   <td>-864.9369</td>  <td>449.7709</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>20</td>    <td>882.2312</td>  <td>0.0348</td>   <td>20.1197</td>   <td>1744.3428</td>  <td>True</td> 
</tr>
<tr>
    <td>10</td>     <td>21</td>    <td>-347.9293</td>   <td>0.9</td>  <td>-1019.5123</td>  <td>323.6537</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>22</td>    <td>-78.4062</td>    <td>0.9</td>   <td>-980.6372</td>  <td>823.8247</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>23</td>    <td>-352.9963</td>   <td>0.9</td>  <td>-1155.5784</td>  <td>449.5859</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>24</td>    <td>-514.8511</td> <td>0.5025</td>  <td>-1154.803</td>  <td>125.1007</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>25</td>    <td>-369.9174</td>   <td>0.9</td>  <td>-1199.4845</td>  <td>459.6498</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>26</td>     <td>77.9594</td>    <td>0.9</td>   <td>-625.9517</td>  <td>781.8705</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>27</td>    <td>1097.3826</td> <td>0.0297</td>   <td>35.0183</td>   <td>2159.747</td>   <td>True</td> 
</tr>
<tr>
    <td>10</td>     <td>28</td>    <td>144.7937</td>    <td>0.9</td>   <td>-559.1173</td>  <td>848.7048</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>29</td>    <td>1915.7421</td>  <td>0.001</td>  <td>1206.177</td>   <td>2625.3072</td>  <td>True</td> 
</tr>
<tr>
    <td>10</td>      <td>3</td>    <td>-338.3396</td>   <td>0.9</td>  <td>-1291.4397</td>  <td>614.7605</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>30</td>    <td>-133.2706</td>   <td>0.9</td>   <td>-837.1817</td>  <td>570.6405</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>31</td>    <td>-277.8984</td>   <td>0.9</td>   <td>-912.8736</td>  <td>357.0768</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>32</td>     <td>16.4071</td>    <td>0.9</td>   <td>-864.6542</td>  <td>897.4684</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>33</td>    <td>-541.4594</td> <td>0.6107</td> <td>-1245.3705</td>  <td>162.4517</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>34</td>    <td>-294.0062</td>   <td>0.9</td>  <td>-1123.5734</td>  <td>535.5609</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>35</td>    <td>-220.812</td>    <td>0.9</td>   <td>-909.4741</td>  <td>467.8502</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>36</td>    <td>-125.8901</td>   <td>0.9</td>   <td>-835.4552</td>   <td>583.675</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>37</td>    <td>-87.1396</td>    <td>0.9</td>  <td>-1339.7586</td>  <td>1165.4794</td>  <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>38</td>    <td>5654.3354</td>  <td>0.001</td>  <td>4894.0245</td>  <td>6414.6463</td>  <td>True</td> 
</tr>
<tr>
    <td>10</td>     <td>39</td>     <td>-222.22</td>    <td>0.9</td>   <td>-944.1062</td>  <td>499.6661</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>      <td>4</td>    <td>-123.7663</td>   <td>0.9</td>   <td>-926.3484</td>  <td>678.8159</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>40</td>    <td>-160.6588</td>   <td>0.9</td>   <td>-828.4475</td>   <td>507.13</td>    <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>41</td>    <td>-435.7151</td>   <td>0.9</td>  <td>-1086.8065</td>  <td>215.3762</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>42</td>    <td>-321.4752</td>   <td>0.9</td>  <td>-1043.3614</td>   <td>400.411</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>43</td>    <td>231.6308</td>    <td>0.9</td>   <td>-504.1475</td>   <td>967.409</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>44</td>    <td>-204.8236</td>   <td>0.9</td>   <td>-974.5214</td>  <td>564.8742</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>45</td>    <td>-256.3991</td>   <td>0.9</td>   <td>-1158.63</td>   <td>645.8318</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>46</td>    <td>-367.4507</td>   <td>0.9</td>  <td>-1103.2289</td>  <td>368.3275</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>47</td>    <td>-387.4539</td>   <td>0.9</td>  <td>-1178.1891</td>  <td>403.2814</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>48</td>    <td>-337.8812</td>   <td>0.9</td>  <td>-1590.5002</td>  <td>914.7377</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>49</td>    <td>-142.6253</td>   <td>0.9</td>   <td>-933.3606</td>   <td>648.11</td>    <td>False</td>
</tr>
<tr>
    <td>10</td>      <td>5</td>    <td>-14.8913</td>    <td>0.9</td>  <td>-1034.9553</td>  <td>1005.1728</td>  <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>50</td>    <td>-244.0062</td>   <td>0.9</td>  <td>-1264.0703</td>  <td>776.0578</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>51</td>    <td>415.0622</td>    <td>0.9</td>   <td>-260.4918</td>  <td>1090.6161</td>  <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>52</td>    <td>-491.6562</td>   <td>0.9</td>  <td>-1220.2735</td>   <td>236.961</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>53</td>     <td>11.0006</td>    <td>0.9</td>   <td>-710.8855</td>  <td>732.8868</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>54</td>    <td>-452.7562</td>   <td>0.9</td>  <td>-1136.8349</td>  <td>231.3224</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>55</td>     <td>-3.7335</td>    <td>0.9</td>   <td>-702.2916</td>  <td>694.8246</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>56</td>    <td>307.4177</td>    <td>0.9</td>   <td>-330.0009</td>  <td>944.8364</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>57</td>    <td>-255.5367</td>   <td>0.9</td>  <td>-1025.2345</td>  <td>514.1611</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>58</td>    <td>-224.7424</td>   <td>0.9</td>  <td>-1054.3095</td>  <td>604.8248</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>59</td>    <td>650.1091</td>  <td>0.0324</td>   <td>17.4922</td>   <td>1282.726</td>   <td>True</td> 
</tr>
<tr>
    <td>10</td>      <td>6</td>     <td>17.0771</td>    <td>0.9</td>   <td>-936.023</td>   <td>970.1772</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>60</td>    <td>342.7138</td>    <td>0.9</td>   <td>-294.7049</td>  <td>980.1324</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>61</td>    <td>-28.9715</td>    <td>0.9</td>   <td>-798.6693</td>  <td>740.7263</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>62</td>    <td>381.2469</td>    <td>0.9</td>   <td>-264.0616</td>  <td>1026.5555</td>  <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>63</td>    <td>445.9526</td>    <td>0.9</td>   <td>-399.0857</td>  <td>1290.9909</td>  <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>64</td>     <td>49.3558</td>    <td>0.9</td>   <td>-672.5304</td>   <td>771.242</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>65</td>    <td>-178.1353</td>   <td>0.9</td>   <td>-887.7004</td>  <td>531.4298</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>66</td>    <td>-155.1313</td>   <td>0.9</td>  <td>-1268.1124</td>  <td>957.8499</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>67</td>    <td>-338.8063</td>   <td>0.9</td>  <td>-1358.8703</td>  <td>681.2578</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>68</td>    <td>-341.5972</td>   <td>0.9</td>  <td>-1040.1552</td>  <td>356.9609</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>69</td>     <td>189.097</td>    <td>0.9</td>   <td>-520.4681</td>  <td>898.6621</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>      <td>7</td>    <td>179.6144</td>    <td>0.9</td>   <td>-542.2717</td>  <td>901.5006</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>70</td>    <td>-300.8524</td>   <td>0.9</td>   <td>-972.4354</td>  <td>370.7306</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>71</td>    <td>-97.9467</td>    <td>0.9</td>   <td>-758.6311</td>  <td>562.7376</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>72</td>     <td>44.2046</td>    <td>0.9</td>   <td>-635.5099</td>   <td>723.919</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>73</td>    <td>-295.0062</td>   <td>0.9</td>  <td>-1197.2372</td>  <td>607.2247</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>74</td>    <td>-397.6216</td>   <td>0.9</td>  <td>-1323.6779</td>  <td>528.4347</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>75</td>    <td>-423.4385</td>   <td>0.9</td>  <td>-1074.5298</td>  <td>227.6529</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>76</td>    <td>-195.6905</td>   <td>0.9</td>   <td>-871.2444</td>  <td>479.8635</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>     <td>77</td>    <td>-357.8441</td>   <td>0.9</td>  <td>-1037.5585</td>  <td>321.8704</td>   <td>False</td>
</tr>
<tr>
    <td>10</td>      <td>8</td>    <td>463.4553</td>    <td>0.9</td>   <td>-462.601</td>   <td>1389.5116</td>  <td>False</td>
</tr>
<tr>
    <td>10</td>      <td>9</td>    <td>1170.3938</td> <td>0.2939</td>  <td>-183.6063</td>  <td>2524.3938</td>  <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>12</td>     <td>331.604</td>    <td>0.9</td>   <td>-573.0852</td>  <td>1236.2933</td>  <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>13</td>    <td>-234.9821</td>   <td>0.9</td>   <td>-872.8097</td>  <td>402.8455</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>14</td>    <td>-32.3707</td>    <td>0.9</td>   <td>-797.9715</td>  <td>733.2301</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>15</td>    <td>-63.5921</td>    <td>0.9</td>  <td>-1300.4982</td>  <td>1173.314</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>16</td>     <td>70.1591</td>    <td>0.9</td>   <td>-556.7352</td>  <td>697.0533</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>17</td>    <td>511.4412</td>  <td>0.5746</td>  <td>-143.422</td>   <td>1166.3045</td>  <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>18</td>    <td>818.8801</td>  <td>0.0032</td>  <td>110.1828</td>   <td>1527.5775</td>  <td>True</td> 
</tr>
<tr>
    <td>11</td>     <td>19</td>    <td>-210.9671</td>   <td>0.9</td>   <td>-865.8303</td>  <td>443.8961</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>      <td>2</td>     <td>21.5812</td>    <td>0.9</td>   <td>-605.3131</td>  <td>648.4754</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>20</td>    <td>1111.3954</td>  <td>0.001</td>  <td>272.2777</td>   <td>1950.5131</td>  <td>True</td> 
</tr>
<tr>
    <td>11</td>     <td>21</td>    <td>-118.7652</td>   <td>0.9</td>   <td>-760.5642</td>  <td>523.0339</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>22</td>    <td>150.7579</td>    <td>0.9</td>   <td>-729.5278</td>  <td>1031.0436</td>  <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>23</td>    <td>-123.8321</td>   <td>0.9</td>   <td>-901.6627</td>  <td>653.9985</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>24</td>    <td>-285.687</td>    <td>0.9</td>   <td>-894.3089</td>  <td>322.9349</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>25</td>    <td>-140.7532</td>   <td>0.9</td>   <td>-946.3983</td>  <td>664.8919</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>26</td>    <td>307.1235</td>    <td>0.9</td>   <td>-368.4304</td>  <td>982.6775</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>27</td>    <td>1326.5468</td>  <td>0.001</td>  <td>282.7555</td>   <td>2370.3381</td>  <td>True</td> 
</tr>
<tr>
    <td>11</td>     <td>28</td>    <td>373.9579</td>    <td>0.9</td>   <td>-301.5961</td>  <td>1049.5118</td>  <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>29</td>    <td>2144.9063</td>  <td>0.001</td>  <td>1463.463</td>   <td>2826.3495</td>  <td>True</td> 
</tr>
<tr>
    <td>11</td>      <td>3</td>    <td>-109.1754</td>   <td>0.9</td>  <td>-1041.5285</td>  <td>823.1776</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>30</td>     <td>95.8935</td>    <td>0.9</td>   <td>-579.6604</td>  <td>771.4475</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>31</td>    <td>-48.7343</td>    <td>0.9</td>   <td>-652.1212</td>  <td>554.6527</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>32</td>    <td>245.5712</td>    <td>0.9</td>   <td>-613.0039</td>  <td>1104.1464</td>  <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>33</td>    <td>-312.2952</td>   <td>0.9</td>   <td>-987.8492</td>  <td>363.2587</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>34</td>    <td>-64.8421</td>    <td>0.9</td>   <td>-870.4872</td>   <td>740.803</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>35</td>     <td>8.3522</td>     <td>0.9</td>   <td>-651.2976</td>  <td>668.0019</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>36</td>     <td>103.274</td>    <td>0.9</td>   <td>-578.1692</td>  <td>784.7173</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>37</td>    <td>142.0246</td>    <td>0.9</td>  <td>-1094.8815</td>  <td>1378.9306</td>  <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>38</td>    <td>5883.4996</td>  <td>0.001</td>  <td>5149.3641</td>  <td>6617.6351</td>  <td>True</td> 
</tr>
<tr>
    <td>11</td>     <td>39</td>     <td>6.9441</td>     <td>0.9</td>   <td>-687.3195</td>  <td>701.2077</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>      <td>4</td>    <td>105.3979</td>    <td>0.9</td>   <td>-672.4327</td>  <td>883.2285</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>40</td>     <td>68.5054</td>    <td>0.9</td>   <td>-569.3222</td>   <td>706.333</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>41</td>    <td>-206.551</td>    <td>0.9</td>   <td>-826.8753</td>  <td>413.7733</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>42</td>    <td>-92.3111</td>    <td>0.9</td>   <td>-786.5747</td>  <td>601.9525</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>43</td>    <td>460.7949</td>    <td>0.9</td>   <td>-247.9024</td>  <td>1169.4923</td>  <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>44</td>     <td>24.3405</td>    <td>0.9</td>   <td>-719.5123</td>  <td>768.1933</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>45</td>     <td>-27.235</td>    <td>0.9</td>   <td>-907.5207</td>  <td>853.0508</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>46</td>    <td>-138.2865</td>   <td>0.9</td>   <td>-846.9839</td>  <td>570.4108</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>47</td>    <td>-158.2897</td>   <td>0.9</td>   <td>-923.8905</td>   <td>607.311</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>48</td>    <td>-108.7171</td>   <td>0.9</td>  <td>-1345.6232</td>  <td>1128.189</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>49</td>     <td>86.5388</td>    <td>0.9</td>   <td>-679.0619</td>  <td>852.1396</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>      <td>5</td>    <td>214.2729</td>    <td>0.9</td>   <td>-786.4334</td>  <td>1214.9792</td>  <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>50</td>    <td>-14.8421</td>    <td>0.9</td>  <td>-1015.5484</td>  <td>985.8642</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>51</td>    <td>644.2263</td>  <td>0.0522</td>   <td>-1.7268</td>   <td>1290.1794</td>  <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>52</td>    <td>-262.4921</td>   <td>0.9</td>   <td>-963.7519</td>  <td>438.7677</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>53</td>    <td>240.1648</td>    <td>0.9</td>   <td>-454.0988</td>  <td>934.4284</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>54</td>    <td>-223.5921</td>   <td>0.9</td>   <td>-878.4553</td>  <td>431.2711</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>55</td>    <td>225.4306</td>    <td>0.9</td>   <td>-444.5438</td>   <td>895.405</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>56</td>    <td>536.5819</td>  <td>0.2336</td>  <td>-69.3758</td>   <td>1142.5396</td>  <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>57</td>    <td>-26.3725</td>    <td>0.9</td>   <td>-770.2253</td>  <td>717.4803</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>58</td>     <td>4.4218</td>     <td>0.9</td>   <td>-801.2233</td>  <td>810.0669</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>59</td>    <td>879.2733</td>   <td>0.001</td>  <td>278.3686</td>   <td>1480.178</td>   <td>True</td> 
</tr>
<tr>
    <td>11</td>      <td>6</td>    <td>246.2412</td>    <td>0.9</td>   <td>-686.1118</td>  <td>1178.5943</td>  <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>60</td>    <td>571.8779</td>   <td>0.114</td>  <td>-34.0798</td>   <td>1177.8356</td>  <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>61</td>    <td>200.1927</td>    <td>0.9</td>   <td>-543.6601</td>  <td>944.0455</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>62</td>    <td>610.4111</td>  <td>0.0553</td>   <td>-3.8409</td>   <td>1224.663</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>63</td>    <td>675.1167</td>  <td>0.4465</td>  <td>-146.4501</td>  <td>1496.6835</td>  <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>64</td>     <td>278.52</td>     <td>0.9</td>   <td>-415.7437</td>  <td>972.7836</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>65</td>     <td>51.0289</td>    <td>0.9</td>   <td>-630.4144</td>  <td>732.4721</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>66</td>     <td>74.0329</td>    <td>0.9</td>  <td>-1021.2339</td>  <td>1169.2997</td>  <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>67</td>    <td>-109.6421</td>   <td>0.9</td>  <td>-1110.3484</td>  <td>891.0642</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>68</td>    <td>-112.433</td>    <td>0.9</td>   <td>-782.4074</td>  <td>557.5414</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>69</td>    <td>418.2611</td>    <td>0.9</td>   <td>-263.1821</td>  <td>1099.7044</td>  <td>False</td>
</tr>
<tr>
    <td>11</td>      <td>7</td>    <td>408.7786</td>    <td>0.9</td>   <td>-285.485</td>   <td>1103.0422</td>  <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>70</td>    <td>-71.6883</td>    <td>0.9</td>   <td>-713.4873</td>  <td>570.1108</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>71</td>    <td>131.2174</td>    <td>0.9</td>   <td>-499.1683</td>  <td>761.6031</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>72</td>    <td>273.3687</td>    <td>0.9</td>   <td>-376.9343</td>  <td>923.6717</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>73</td>    <td>-65.8421</td>    <td>0.9</td>   <td>-946.1278</td>  <td>814.4436</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>74</td>    <td>-168.4575</td>   <td>0.9</td>  <td>-1073.1467</td>  <td>736.2317</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>75</td>    <td>-194.2743</td>   <td>0.9</td>   <td>-814.5986</td>   <td>426.05</td>    <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>76</td>     <td>33.4737</td>    <td>0.9</td>   <td>-612.4794</td>  <td>679.4268</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>     <td>77</td>    <td>-128.6799</td>   <td>0.9</td>   <td>-778.983</td>   <td>521.6231</td>   <td>False</td>
</tr>
<tr>
    <td>11</td>      <td>8</td>    <td>692.6194</td>  <td>0.6218</td>  <td>-212.0698</td>  <td>1597.3087</td>  <td>False</td>
</tr>
<tr>
    <td>11</td>      <td>9</td>    <td>1399.5579</td> <td>0.0243</td>   <td>60.081</td>    <td>2739.0348</td>  <td>True</td> 
</tr>
<tr>
    <td>12</td>     <td>13</td>    <td>-566.5862</td>   <td>0.9</td>  <td>-1465.4917</td>  <td>332.3194</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>14</td>    <td>-363.9747</td>   <td>0.9</td>  <td>-1357.6304</td>   <td>629.681</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>15</td>    <td>-395.1962</td>   <td>0.9</td>  <td>-1784.8521</td>  <td>994.4598</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>16</td>    <td>-261.445</td>    <td>0.9</td>   <td>-1152.626</td>   <td>629.736</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>17</td>    <td>179.8372</td>    <td>0.9</td>   <td>-731.2353</td>  <td>1090.9096</td>  <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>18</td>    <td>487.2761</td>    <td>0.9</td>   <td>-463.2286</td>  <td>1437.7807</td>  <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>19</td>    <td>-542.5712</td>   <td>0.9</td>  <td>-1453.6436</td>  <td>368.5013</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>      <td>2</td>    <td>-310.0229</td>   <td>0.9</td>  <td>-1201.2039</td>  <td>581.1581</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>20</td>    <td>779.7913</td>   <td>0.695</td>  <td>-271.5534</td>  <td>1831.1361</td>  <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>21</td>    <td>-450.3692</td>   <td>0.9</td>  <td>-1352.0971</td>  <td>451.3586</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>22</td>    <td>-180.8462</td>   <td>0.9</td>  <td>-1265.3323</td>   <td>903.64</td>    <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>23</td>    <td>-455.4362</td>   <td>0.9</td>  <td>-1458.5451</td>  <td>547.6728</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>24</td>    <td>-617.2911</td> <td>0.8144</td> <td>-1495.7145</td>  <td>261.1324</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>25</td>    <td>-472.3573</td>   <td>0.9</td>  <td>-1497.1846</td>  <td>552.4701</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>26</td>    <td>-24.4805</td>    <td>0.9</td>   <td>-950.5368</td>  <td>901.5758</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>27</td>    <td>994.9427</td>   <td>0.47</td>   <td>-226.0026</td>  <td>2215.8881</td>  <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>28</td>     <td>42.3538</td>    <td>0.9</td>   <td>-883.7025</td>  <td>968.4102</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>29</td>    <td>1813.3022</td>  <td>0.001</td>   <td>882.941</td>   <td>2743.6635</td>  <td>True</td> 
</tr>
<tr>
    <td>12</td>      <td>3</td>    <td>-440.7795</td>   <td>0.9</td>  <td>-1567.9393</td>  <td>686.3804</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>30</td>    <td>-235.7105</td>   <td>0.9</td>  <td>-1161.7668</td>  <td>690.3458</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>31</td>    <td>-380.3383</td>   <td>0.9</td>  <td>-1255.1428</td>  <td>494.4662</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>32</td>    <td>-86.0328</td>    <td>0.9</td>  <td>-1152.9716</td>   <td>980.906</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>33</td>    <td>-643.8993</td> <td>0.8371</td> <td>-1569.9556</td>   <td>282.157</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>34</td>    <td>-396.4462</td>   <td>0.9</td>  <td>-1421.2735</td>  <td>628.3812</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>35</td>    <td>-323.2519</td>   <td>0.9</td>  <td>-1237.7708</td>  <td>591.2671</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>36</td>     <td>-228.33</td>    <td>0.9</td>  <td>-1158.6913</td>  <td>702.0312</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>37</td>    <td>-189.5795</td>   <td>0.9</td>  <td>-1579.2355</td>  <td>1200.0765</td>  <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>38</td>    <td>5551.8955</td>  <td>0.001</td>  <td>4582.276</td>   <td>6521.5151</td>  <td>True</td> 
</tr>
<tr>
    <td>12</td>     <td>39</td>    <td>-324.6599</td>   <td>0.9</td>   <td>-1264.452</td>  <td>615.1321</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>      <td>4</td>    <td>-226.2062</td>   <td>0.9</td>  <td>-1229.3151</td>  <td>776.9028</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>40</td>    <td>-263.0987</td>   <td>0.9</td>  <td>-1162.0042</td>  <td>635.8069</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>41</td>    <td>-538.155</td>    <td>0.9</td>  <td>-1424.7267</td>  <td>348.4167</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>42</td>    <td>-423.9151</td>   <td>0.9</td>  <td>-1363.7072</td>  <td>515.8769</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>43</td>    <td>129.1909</td>    <td>0.9</td>   <td>-821.3138</td>  <td>1079.6955</td>  <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>44</td>    <td>-307.2635</td>   <td>0.9</td>  <td>-1284.2611</td>   <td>669.734</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>45</td>    <td>-358.839</td>    <td>0.9</td>  <td>-1443.3251</td>  <td>725.6471</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>46</td>    <td>-469.8906</td>   <td>0.9</td>  <td>-1420.3952</td>   <td>480.614</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>47</td>    <td>-489.8938</td>   <td>0.9</td>  <td>-1483.5495</td>   <td>503.762</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>48</td>    <td>-440.3212</td>   <td>0.9</td>  <td>-1829.9771</td>  <td>949.3348</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>49</td>    <td>-245.0652</td>   <td>0.9</td>  <td>-1238.7209</td>  <td>748.5905</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>      <td>5</td>    <td>-117.3312</td>   <td>0.9</td>  <td>-1301.6538</td>  <td>1066.9915</td>  <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>50</td>    <td>-346.4462</td>   <td>0.9</td>  <td>-1530.7688</td>  <td>837.8765</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>51</td>    <td>312.6223</td>    <td>0.9</td>   <td>-592.067</td>   <td>1217.3115</td>  <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>52</td>    <td>-594.0962</td>   <td>0.9</td>  <td>-1539.0684</td>  <td>350.8761</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>53</td>    <td>-91.4393</td>    <td>0.9</td>  <td>-1031.2313</td>  <td>848.3528</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>54</td>    <td>-555.1962</td>   <td>0.9</td>  <td>-1466.2686</td>  <td>355.8763</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>55</td>    <td>-106.1734</td>   <td>0.9</td>  <td>-1028.1674</td>  <td>815.8205</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>56</td>    <td>204.9778</td>    <td>0.9</td>   <td>-671.6018</td>  <td>1081.5575</td>  <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>57</td>    <td>-357.9766</td>   <td>0.9</td>  <td>-1334.9741</td>  <td>619.0209</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>58</td>    <td>-327.1823</td>   <td>0.9</td>  <td>-1352.0096</td>  <td>697.6451</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>59</td>    <td>547.6692</td>    <td>0.9</td>   <td>-325.425</td>   <td>1420.7635</td>  <td>False</td>
</tr>
<tr>
    <td>12</td>      <td>6</td>    <td>-85.3628</td>    <td>0.9</td>  <td>-1212.5227</td>  <td>1041.797</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>60</td>    <td>240.2738</td>    <td>0.9</td>   <td>-636.3058</td>  <td>1116.8535</td>  <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>61</td>    <td>-131.4114</td>   <td>0.9</td>  <td>-1108.4089</td>  <td>845.5861</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>62</td>     <td>278.807</td>    <td>0.9</td>   <td>-603.5266</td>  <td>1161.1406</td>  <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>63</td>    <td>343.5127</td>    <td>0.9</td>   <td>-693.8779</td>  <td>1380.9032</td>  <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>64</td>    <td>-53.0841</td>    <td>0.9</td>   <td>-992.8761</td>   <td>886.708</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>65</td>    <td>-280.5752</td>   <td>0.9</td>  <td>-1210.9364</td>  <td>649.7861</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>66</td>    <td>-257.5712</td>   <td>0.9</td>  <td>-1522.8049</td>  <td>1007.6626</td>  <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>67</td>    <td>-441.2462</td>   <td>0.9</td>  <td>-1625.5688</td>  <td>743.0765</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>68</td>    <td>-444.0371</td>   <td>0.9</td>   <td>-1366.031</td>  <td>477.9569</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>69</td>     <td>86.6571</td>    <td>0.9</td>   <td>-843.7042</td>  <td>1017.0183</td>  <td>False</td>
</tr>
<tr>
    <td>12</td>      <td>7</td>     <td>77.1745</td>    <td>0.9</td>   <td>-862.6175</td>  <td>1016.9666</td>  <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>70</td>    <td>-403.2923</td>   <td>0.9</td>  <td>-1305.0202</td>  <td>498.4356</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>71</td>    <td>-200.3866</td>   <td>0.9</td>  <td>-1094.0271</td>  <td>693.2538</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>72</td>    <td>-58.2353</td>    <td>0.9</td>   <td>-966.0355</td>  <td>849.5648</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>73</td>    <td>-397.4462</td>   <td>0.9</td>  <td>-1481.9323</td>   <td>687.04</td>    <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>74</td>    <td>-500.0615</td>   <td>0.9</td>  <td>-1604.4481</td>  <td>604.3251</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>75</td>    <td>-525.8784</td>   <td>0.9</td>  <td>-1412.4501</td>  <td>360.6933</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>76</td>    <td>-298.1304</td>   <td>0.9</td>  <td>-1202.8196</td>  <td>606.5589</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>     <td>77</td>    <td>-460.284</td>    <td>0.9</td>  <td>-1368.0842</td>  <td>447.5162</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>      <td>8</td>    <td>361.0154</td>    <td>0.9</td>   <td>-743.3712</td>  <td>1465.402</td>   <td>False</td>
</tr>
<tr>
    <td>12</td>      <td>9</td>    <td>1067.9538</td> <td>0.7591</td>  <td>-413.7362</td>  <td>2549.6439</td>  <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>14</td>    <td>202.6114</td>    <td>0.9</td>   <td>-556.1462</td>  <td>961.3691</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>15</td>     <td>171.39</td>     <td>0.9</td>  <td>-1061.2921</td>  <td>1404.0721</td>  <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>16</td>    <td>305.1412</td>    <td>0.9</td>   <td>-313.3772</td>  <td>923.6596</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>17</td>    <td>746.4233</td>  <td>0.0033</td>   <td>99.5737</td>   <td>1393.273</td>   <td>True</td> 
</tr>
<tr>
    <td>13</td>     <td>18</td>    <td>1053.8622</td>  <td>0.001</td>   <td>352.563</td>   <td>1755.1614</td>  <td>True</td> 
</tr>
<tr>
    <td>13</td>     <td>19</td>     <td>24.015</td>     <td>0.9</td>   <td>-622.8347</td>  <td>670.8647</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>      <td>2</td>    <td>256.5633</td>    <td>0.9</td>   <td>-361.9551</td>  <td>875.0817</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>20</td>    <td>1346.3775</td>  <td>0.001</td>  <td>513.4987</td>   <td>2179.2563</td>  <td>True</td> 
</tr>
<tr>
    <td>13</td>     <td>21</td>    <td>116.2169</td>    <td>0.9</td>   <td>-517.4033</td>  <td>749.8372</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>22</td>     <td>385.74</td>     <td>0.9</td>   <td>-488.6006</td>  <td>1260.0806</td>  <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>23</td>     <td>111.15</td>     <td>0.9</td>   <td>-659.946</td>    <td>882.246</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>24</td>    <td>-50.7049</td>    <td>0.9</td>   <td>-650.6959</td>  <td>549.2862</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>25</td>     <td>94.2289</td>    <td>0.9</td>   <td>-704.916</td>   <td>893.3738</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>26</td>    <td>542.1056</td>  <td>0.4801</td>  <td>-125.6831</td>  <td>1209.8943</td>  <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>27</td>    <td>1561.5289</td>  <td>0.001</td>  <td>522.7465</td>   <td>2600.3113</td>  <td>True</td> 
</tr>
<tr>
    <td>13</td>     <td>28</td>     <td>608.94</td>   <td>0.1716</td>  <td>-58.8487</td>   <td>1276.7287</td>  <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>29</td>    <td>2379.8884</td>  <td>0.001</td>  <td>1706.1425</td>  <td>3053.6343</td>  <td>True</td> 
</tr>
<tr>
    <td>13</td>      <td>3</td>    <td>125.8067</td>    <td>0.9</td>   <td>-800.9354</td>  <td>1052.5487</td>  <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>30</td>    <td>330.8756</td>    <td>0.9</td>   <td>-336.9131</td>  <td>998.6643</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>31</td>    <td>186.2478</td>    <td>0.9</td>   <td>-408.4323</td>   <td>780.928</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>32</td>    <td>480.5533</td>    <td>0.9</td>   <td>-371.9253</td>  <td>1333.032</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>33</td>    <td>-77.3131</td>    <td>0.9</td>   <td>-745.1018</td>  <td>590.4756</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>34</td>     <td>170.14</td>     <td>0.9</td>   <td>-629.0049</td>  <td>969.2849</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>35</td>    <td>243.3343</td>    <td>0.9</td>   <td>-408.3608</td>  <td>895.0293</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>36</td>    <td>338.2561</td>    <td>0.9</td>   <td>-335.4898</td>  <td>1012.002</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>37</td>    <td>377.0067</td>    <td>0.9</td>   <td>-855.6755</td>  <td>1609.6888</td>  <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>38</td>    <td>6118.4817</td>  <td>0.001</td>  <td>5391.4854</td>  <td>6845.4779</td>  <td>True</td> 
</tr>
<tr>
    <td>13</td>     <td>39</td>    <td>241.9262</td>    <td>0.9</td>   <td>-444.7838</td>  <td>928.6362</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>      <td>4</td>     <td>340.38</td>     <td>0.9</td>   <td>-430.716</td>   <td>1111.476</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>40</td>    <td>303.4875</td>    <td>0.9</td>   <td>-326.1097</td>  <td>933.0847</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>41</td>     <td>28.4311</td>    <td>0.9</td>   <td>-583.4274</td>  <td>640.2896</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>42</td>     <td>142.671</td>    <td>0.9</td>   <td>-544.0389</td>   <td>829.381</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>43</td>     <td>695.777</td>  <td>0.0567</td>   <td>-5.5221</td>   <td>1397.0762</td>  <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>44</td>    <td>259.3226</td>    <td>0.9</td>   <td>-477.4851</td>  <td>996.1303</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>45</td>    <td>207.7471</td>    <td>0.9</td>   <td>-666.5935</td>  <td>1082.0878</td>  <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>46</td>     <td>96.6956</td>    <td>0.9</td>   <td>-604.6036</td>  <td>797.9947</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>47</td>     <td>76.6924</td>    <td>0.9</td>   <td>-682.0653</td>   <td>835.45</td>    <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>48</td>     <td>126.265</td>    <td>0.9</td>  <td>-1106.4171</td>  <td>1358.9471</td>  <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>49</td>     <td>321.521</td>    <td>0.9</td>   <td>-437.2367</td>  <td>1080.2786</td>  <td>False</td>
</tr>
<tr>
    <td>13</td>      <td>5</td>     <td>449.255</td>    <td>0.9</td>   <td>-546.2256</td>  <td>1444.7356</td>  <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>50</td>     <td>220.14</td>     <td>0.9</td>   <td>-775.3406</td>  <td>1215.6206</td>  <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>51</td>    <td>879.2084</td>   <td>0.001</td>  <td>241.3808</td>   <td>1517.036</td>   <td>True</td> 
</tr>
<tr>
    <td>13</td>     <td>52</td>     <td>-27.51</td>     <td>0.9</td>   <td>-721.2924</td>  <td>666.2724</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>53</td>    <td>475.1469</td>  <td>0.8475</td>  <td>-211.5631</td>  <td>1161.8569</td>  <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>54</td>      <td>11.39</td>     <td>0.9</td>   <td>-635.4597</td>  <td>658.2397</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>55</td>    <td>460.4127</td>   <td>0.837</td>  <td>-201.731</td>   <td>1122.5565</td>  <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>56</td>     <td>771.564</td>   <td>0.001</td>  <td>174.2756</td>   <td>1368.8524</td>  <td>True</td> 
</tr>
<tr>
    <td>13</td>     <td>57</td>    <td>208.6096</td>    <td>0.9</td>   <td>-528.1981</td>  <td>945.4173</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>58</td>    <td>239.4039</td>    <td>0.9</td>   <td>-559.741</td>   <td>1038.5488</td>  <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>59</td>    <td>1114.2554</td>  <td>0.001</td>   <td>522.094</td>   <td>1706.4167</td>  <td>True</td> 
</tr>
<tr>
    <td>13</td>      <td>6</td>    <td>481.2233</td>    <td>0.9</td>   <td>-445.5187</td>  <td>1407.9654</td>  <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>60</td>     <td>806.86</td>    <td>0.001</td>  <td>209.5716</td>   <td>1404.1484</td>  <td>True</td> 
</tr>
<tr>
    <td>13</td>     <td>61</td>    <td>435.1748</td>    <td>0.9</td>   <td>-301.6329</td>  <td>1171.9825</td>  <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>62</td>    <td>845.3932</td>   <td>0.001</td>  <td>239.6919</td>   <td>1451.0945</td>  <td>True</td> 
</tr>
<tr>
    <td>13</td>     <td>63</td>    <td>910.0988</td>  <td>0.0068</td>   <td>94.9052</td>   <td>1725.2924</td>  <td>True</td> 
</tr>
<tr>
    <td>13</td>     <td>64</td>    <td>513.5021</td>  <td>0.6764</td>  <td>-173.2079</td>  <td>1200.212</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>65</td>     <td>286.011</td>    <td>0.9</td>   <td>-387.7349</td>  <td>959.7569</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>66</td>     <td>309.015</td>    <td>0.9</td>   <td>-781.4794</td>  <td>1399.5094</td>  <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>67</td>     <td>125.34</td>     <td>0.9</td>   <td>-870.1406</td>  <td>1120.8206</td>  <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>68</td>    <td>122.5491</td>    <td>0.9</td>   <td>-539.5946</td>  <td>784.6928</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>69</td>    <td>653.2432</td>   <td>0.08</td>   <td>-20.5027</td>   <td>1326.9891</td>  <td>False</td>
</tr>
<tr>
    <td>13</td>      <td>7</td>    <td>643.7607</td>  <td>0.1245</td>  <td>-42.9493</td>   <td>1330.4707</td>  <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>70</td>    <td>163.2938</td>    <td>0.9</td>   <td>-470.3264</td>  <td>796.9141</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>71</td>    <td>366.1995</td>    <td>0.9</td>   <td>-255.8573</td>  <td>988.2564</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>72</td>    <td>508.3508</td>  <td>0.5423</td>  <td>-133.8817</td>  <td>1150.5834</td>  <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>73</td>     <td>169.14</td>     <td>0.9</td>   <td>-705.2006</td>  <td>1043.4806</td>  <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>74</td>     <td>66.5246</td>    <td>0.9</td>   <td>-832.3809</td>  <td>965.4302</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>75</td>     <td>40.7078</td>    <td>0.9</td>   <td>-571.1507</td>  <td>652.5663</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>76</td>    <td>268.4558</td>    <td>0.9</td>   <td>-369.3718</td>  <td>906.2834</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>     <td>77</td>    <td>106.3022</td>    <td>0.9</td>   <td>-535.9304</td>  <td>748.5347</td>   <td>False</td>
</tr>
<tr>
    <td>13</td>      <td>8</td>    <td>927.6015</td>  <td>0.0302</td>   <td>28.696</td>    <td>1826.5071</td>  <td>True</td> 
</tr>
<tr>
    <td>13</td>      <td>9</td>     <td>1634.54</td>   <td>0.001</td>  <td>298.9626</td>   <td>2970.1174</td>  <td>True</td> 
</tr>
<tr>
    <td>14</td>     <td>15</td>    <td>-31.2214</td>    <td>0.9</td>  <td>-1334.6115</td>  <td>1272.1687</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>16</td>    <td>102.5297</td>    <td>0.9</td>   <td>-647.0605</td>   <td>852.12</td>    <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>17</td>    <td>543.8119</td>  <td>0.8124</td>  <td>-229.3213</td>  <td>1316.9451</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>18</td>    <td>851.2508</td>  <td>0.0268</td>   <td>32.0188</td>   <td>1670.4828</td>  <td>True</td> 
</tr>
<tr>
    <td>14</td>     <td>19</td>    <td>-178.5964</td>   <td>0.9</td>   <td>-951.7296</td>  <td>594.5368</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>      <td>2</td>     <td>53.9518</td>    <td>0.9</td>   <td>-695.6384</td>  <td>803.5421</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>20</td>    <td>1143.7661</td>  <td>0.001</td>  <td>209.4173</td>   <td>2078.1149</td>  <td>True</td> 
</tr>
<tr>
    <td>14</td>     <td>21</td>    <td>-86.3945</td>    <td>0.9</td>   <td>-848.4937</td>  <td>675.7046</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>22</td>    <td>183.1286</td>    <td>0.9</td>   <td>-788.361</td>   <td>1154.6182</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>23</td>    <td>-91.4614</td>    <td>0.9</td>   <td>-971.1827</td>  <td>788.2598</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>24</td>    <td>-253.3163</td>   <td>0.9</td>   <td>-987.6934</td>  <td>481.0608</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>25</td>    <td>-108.3825</td>   <td>0.9</td>  <td>-1012.7901</td>  <td>796.0251</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>26</td>    <td>339.4942</td>    <td>0.9</td>   <td>-451.2411</td>  <td>1130.2295</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>27</td>    <td>1358.9175</td>  <td>0.001</td>  <td>237.1379</td>   <td>2480.697</td>   <td>True</td> 
</tr>
<tr>
    <td>14</td>     <td>28</td>    <td>406.3286</td>    <td>0.9</td>   <td>-384.4067</td>  <td>1197.0638</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>29</td>    <td>2177.277</td>   <td>0.001</td>  <td>1381.5044</td>  <td>2973.0496</td>  <td>True</td> 
</tr>
<tr>
    <td>14</td>      <td>3</td>    <td>-76.8048</td>    <td>0.9</td>  <td>-1095.7117</td>  <td>942.1021</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>30</td>    <td>128.2642</td>    <td>0.9</td>   <td>-662.4711</td>  <td>918.9995</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>31</td>    <td>-16.3636</td>    <td>0.9</td>   <td>-746.4081</td>  <td>713.6809</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>32</td>    <td>277.9419</td>    <td>0.9</td>   <td>-673.9196</td>  <td>1229.8034</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>33</td>    <td>-279.9246</td>   <td>0.9</td>  <td>-1070.6598</td>  <td>510.8107</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>34</td>    <td>-32.4714</td>    <td>0.9</td>   <td>-936.879</td>   <td>871.9362</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>35</td>     <td>40.7229</td>    <td>0.9</td>   <td>-736.4688</td>  <td>817.9145</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>36</td>    <td>135.6447</td>    <td>0.9</td>   <td>-660.1279</td>  <td>931.4173</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>37</td>    <td>174.3952</td>    <td>0.9</td>  <td>-1128.9948</td>  <td>1477.7853</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>38</td>    <td>5915.8702</td>  <td>0.001</td>  <td>5074.5356</td>  <td>6757.2049</td>  <td>True</td> 
</tr>
<tr>
    <td>14</td>     <td>39</td>     <td>39.3148</td>    <td>0.9</td>   <td>-767.4634</td>   <td>846.093</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>      <td>4</td>    <td>137.7686</td>    <td>0.9</td>   <td>-741.9527</td>  <td>1017.4898</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>40</td>    <td>100.8761</td>    <td>0.9</td>   <td>-657.8816</td>  <td>859.6337</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>41</td>    <td>-174.1803</td>   <td>0.9</td>   <td>-918.2847</td>  <td>569.9241</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>42</td>    <td>-59.9404</td>    <td>0.9</td>   <td>-866.7186</td>  <td>746.8378</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>43</td>    <td>493.1656</td>    <td>0.9</td>   <td>-326.0664</td>  <td>1312.3976</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>44</td>     <td>56.7112</td>    <td>0.9</td>   <td>-793.1159</td>  <td>906.5383</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>45</td>     <td>5.1357</td>     <td>0.9</td>   <td>-966.3539</td>  <td>976.6253</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>46</td>    <td>-105.9159</td>   <td>0.9</td>   <td>-925.1478</td>  <td>713.3161</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>47</td>    <td>-125.919</td>    <td>0.9</td>   <td>-994.8458</td>  <td>743.0077</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>48</td>    <td>-76.3464</td>    <td>0.9</td>  <td>-1379.7365</td>  <td>1227.0437</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>49</td>    <td>118.9095</td>    <td>0.9</td>   <td>-750.0172</td>  <td>987.8362</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>      <td>5</td>    <td>246.6436</td>    <td>0.9</td>   <td>-835.1615</td>  <td>1328.4486</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>50</td>     <td>17.5286</td>    <td>0.9</td>  <td>-1064.2765</td>  <td>1099.3336</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>51</td>     <td>676.597</td>  <td>0.2375</td>  <td>-89.0038</td>   <td>1442.1978</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>52</td>    <td>-230.1214</td>   <td>0.9</td>   <td>-1042.928</td>  <td>582.6851</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>53</td>    <td>272.5355</td>    <td>0.9</td>   <td>-534.2427</td>  <td>1079.3137</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>54</td>    <td>-191.2214</td>   <td>0.9</td>   <td>-964.3546</td>  <td>581.9118</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>55</td>    <td>257.8013</td>    <td>0.9</td>   <td>-528.1725</td>  <td>1043.7751</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>56</td>    <td>568.9526</td>  <td>0.5866</td>  <td>-163.2181</td>  <td>1301.1232</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>57</td>     <td>5.9981</td>     <td>0.9</td>   <td>-843.829</td>   <td>855.8252</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>58</td>     <td>36.7925</td>    <td>0.9</td>   <td>-867.6151</td>  <td>941.2001</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>59</td>     <td>911.644</td>   <td>0.001</td>  <td>183.6498</td>   <td>1639.6381</td>  <td>True</td> 
</tr>
<tr>
    <td>14</td>      <td>6</td>    <td>278.6119</td>    <td>0.9</td>   <td>-740.295</td>   <td>1297.5188</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>60</td>    <td>604.2486</td>  <td>0.4336</td>  <td>-127.9221</td>  <td>1336.4192</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>61</td>    <td>232.5634</td>    <td>0.9</td>   <td>-617.2637</td>  <td>1082.3905</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>62</td>    <td>642.7818</td>  <td>0.2778</td>   <td>-96.268</td>   <td>1381.8315</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>63</td>    <td>707.4874</td>  <td>0.6078</td>  <td>-211.1318</td>  <td>1626.1065</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>64</td>    <td>310.8906</td>    <td>0.9</td>   <td>-495.8876</td>  <td>1117.6688</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>65</td>     <td>83.3995</td>    <td>0.9</td>   <td>-712.3731</td>  <td>879.1721</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>66</td>    <td>106.4036</td>    <td>0.9</td>  <td>-1063.4248</td>  <td>1276.232</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>67</td>    <td>-77.2714</td>    <td>0.9</td>  <td>-1159.0765</td>  <td>1004.5336</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>68</td>    <td>-80.0623</td>    <td>0.9</td>   <td>-866.0361</td>  <td>705.9115</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>69</td>    <td>450.6318</td>    <td>0.9</td>   <td>-345.1408</td>  <td>1246.4044</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>      <td>7</td>    <td>441.1493</td>    <td>0.9</td>   <td>-365.6289</td>  <td>1247.9275</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>70</td>    <td>-39.3176</td>    <td>0.9</td>   <td>-801.4167</td>  <td>722.7816</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>71</td>    <td>163.5881</td>    <td>0.9</td>   <td>-588.9245</td>  <td>916.1007</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>72</td>    <td>305.7394</td>    <td>0.9</td>   <td>-463.535</td>   <td>1075.0138</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>73</td>    <td>-33.4714</td>    <td>0.9</td>   <td>-1004.961</td>  <td>938.0182</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>74</td>    <td>-136.0868</td>   <td>0.9</td>  <td>-1129.7425</td>  <td>857.5689</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>75</td>    <td>-161.9037</td>   <td>0.9</td>   <td>-906.008</td>   <td>582.2007</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>76</td>     <td>65.8444</td>    <td>0.9</td>   <td>-699.7564</td>  <td>831.4451</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>     <td>77</td>    <td>-96.3093</td>    <td>0.9</td>   <td>-865.5837</td>  <td>672.9652</td>   <td>False</td>
</tr>
<tr>
    <td>14</td>      <td>8</td>    <td>724.9901</td>   <td>0.732</td>  <td>-268.6656</td>  <td>1718.6458</td>  <td>False</td>
</tr>
<tr>
    <td>14</td>      <td>9</td>    <td>1431.9286</td> <td>0.0355</td>   <td>30.8263</td>   <td>2833.0308</td>  <td>True</td> 
</tr>
<tr>
    <td>15</td>     <td>16</td>    <td>133.7512</td>    <td>0.9</td>  <td>-1093.3094</td>  <td>1360.8117</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>17</td>    <td>575.0333</td>    <td>0.9</td>   <td>-666.5491</td>  <td>1816.6158</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>18</td>    <td>882.4722</td>  <td>0.8398</td>  <td>-388.328</td>   <td>2153.2724</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>19</td>    <td>-147.375</td>    <td>0.9</td>  <td>-1388.9575</td>  <td>1094.2075</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>      <td>2</td>     <td>85.1733</td>    <td>0.9</td>  <td>-1141.8873</td>  <td>1312.2338</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>20</td>    <td>1174.9875</td> <td>0.2718</td>  <td>-172.8996</td>  <td>2522.8746</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>21</td>    <td>-55.1731</td>    <td>0.9</td>  <td>-1289.9148</td>  <td>1179.5687</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>22</td>     <td>214.35</td>     <td>0.9</td>  <td>-1159.5438</td>  <td>1588.2438</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>23</td>     <td>-60.24</td>     <td>0.9</td>  <td>-1370.8511</td>  <td>1250.3711</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>24</td>    <td>-222.0949</td>   <td>0.9</td>  <td>-1439.9216</td>  <td>995.7318</td>   <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>25</td>    <td>-77.1611</td>    <td>0.9</td>  <td>-1404.4686</td>  <td>1250.1464</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>26</td>    <td>370.7156</td>    <td>0.9</td>   <td>-881.9034</td>  <td>1623.3346</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>27</td>    <td>1390.1389</td>  <td>0.125</td>   <td>-93.836</td>   <td>2874.1138</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>28</td>     <td>437.55</td>     <td>0.9</td>   <td>-815.069</td>   <td>1690.169</td>   <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>29</td>    <td>2208.4984</td>  <td>0.001</td>  <td>952.6934</td>   <td>3464.3033</td>  <td>True</td> 
</tr>
<tr>
    <td>15</td>      <td>3</td>    <td>-45.5833</td>    <td>0.9</td>  <td>-1453.4055</td>  <td>1362.2389</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>30</td>    <td>159.4856</td>    <td>0.9</td>  <td>-1093.1334</td>  <td>1412.1046</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>31</td>     <td>14.8578</td>    <td>0.9</td>  <td>-1200.3611</td>  <td>1230.0768</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>32</td>    <td>309.1633</td>    <td>0.9</td>  <td>-1050.9221</td>  <td>1669.2488</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>33</td>    <td>-248.7031</td>   <td>0.9</td>  <td>-1501.3221</td>  <td>1003.9159</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>34</td>      <td>-1.25</td>     <td>0.9</td>  <td>-1328.5575</td>  <td>1326.0575</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>35</td>     <td>71.9443</td>    <td>0.9</td>  <td>-1172.1694</td>  <td>1316.058</td>   <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>36</td>    <td>166.8661</td>    <td>0.9</td>  <td>-1088.9388</td>  <td>1422.6711</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>37</td>    <td>205.6167</td>    <td>0.9</td>  <td>-1419.9964</td>  <td>1831.2297</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>38</td>    <td>5947.0917</td>  <td>0.001</td>  <td>4661.9317</td>  <td>7232.2516</td>  <td>True</td> 
</tr>
<tr>
    <td>15</td>     <td>39</td>     <td>70.5362</td>    <td>0.9</td>  <td>-1192.2714</td>  <td>1333.3438</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>      <td>4</td>     <td>168.99</td>     <td>0.9</td>  <td>-1141.6211</td>  <td>1479.6011</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>40</td>    <td>132.0975</td>    <td>0.9</td>  <td>-1100.5846</td>  <td>1364.7796</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>41</td>    <td>-142.9589</td>   <td>0.9</td>  <td>-1366.6759</td>  <td>1080.7582</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>42</td>     <td>-28.719</td>    <td>0.9</td>  <td>-1291.5266</td>  <td>1234.0887</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>43</td>     <td>524.387</td>    <td>0.9</td>   <td>-746.4131</td>  <td>1795.1872</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>44</td>     <td>87.9326</td>    <td>0.9</td>  <td>-1202.8029</td>  <td>1378.6681</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>45</td>     <td>36.3571</td>    <td>0.9</td>  <td>-1337.5366</td>  <td>1410.2509</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>46</td>    <td>-74.6944</td>    <td>0.9</td>  <td>-1345.4946</td>  <td>1196.1057</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>47</td>    <td>-94.6976</td>    <td>0.9</td>  <td>-1398.0877</td>  <td>1208.6925</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>48</td>     <td>-45.125</td>    <td>0.9</td>   <td>-1670.738</td>  <td>1580.488</td>   <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>49</td>     <td>150.131</td>    <td>0.9</td>  <td>-1153.2591</td>  <td>1453.521</td>   <td>False</td>
</tr>
<tr>
    <td>15</td>      <td>5</td>     <td>277.865</td>    <td>0.9</td>  <td>-1176.1275</td>  <td>1731.8575</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>50</td>      <td>48.75</td>     <td>0.9</td>  <td>-1405.2425</td>  <td>1502.7425</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>51</td>    <td>707.8184</td>    <td>0.9</td>   <td>-529.0876</td>  <td>1944.7245</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>52</td>     <td>-198.9</td>     <td>0.9</td>  <td>-1465.5675</td>  <td>1067.7675</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>53</td>    <td>303.7569</td>    <td>0.9</td>   <td>-959.0507</td>  <td>1566.5645</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>54</td>     <td>-160.0</td>     <td>0.9</td>  <td>-1401.5825</td>  <td>1081.5825</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>55</td>    <td>289.0227</td>    <td>0.9</td>   <td>-960.596</td>   <td>1538.6414</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>56</td>     <td>600.174</td>    <td>0.9</td>   <td>-616.3234</td>  <td>1816.6714</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>57</td>     <td>37.2196</td>    <td>0.9</td>  <td>-1253.5159</td>  <td>1327.9551</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>58</td>     <td>68.0139</td>    <td>0.9</td>  <td>-1259.2936</td>  <td>1395.3214</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>59</td>    <td>942.8654</td>  <td>0.5879</td>  <td>-271.1229</td>  <td>2156.8537</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>      <td>6</td>    <td>309.8333</td>    <td>0.9</td>  <td>-1097.9889</td>  <td>1717.6555</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>60</td>     <td>635.47</td>     <td>0.9</td>   <td>-581.0274</td>  <td>1851.9674</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>61</td>    <td>263.7848</td>    <td>0.9</td>  <td>-1026.9507</td>  <td>1554.5203</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>62</td>    <td>674.0032</td>    <td>0.9</td>   <td>-546.6469</td>  <td>1894.6533</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>63</td>    <td>738.7088</td>    <td>0.9</td>   <td>-598.3227</td>  <td>2075.7403</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>64</td>    <td>342.1121</td>    <td>0.9</td>   <td>-920.6956</td>  <td>1604.9197</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>65</td>     <td>114.621</td>    <td>0.9</td>   <td>-1141.184</td>  <td>1370.4259</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>66</td>     <td>137.625</td>    <td>0.9</td>  <td>-1382.9968</td>  <td>1658.2468</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>67</td>     <td>-46.05</td>     <td>0.9</td>  <td>-1500.0425</td>  <td>1407.9425</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>68</td>    <td>-48.8409</td>    <td>0.9</td>  <td>-1298.4596</td>  <td>1200.7778</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>69</td>    <td>481.8532</td>    <td>0.9</td>   <td>-773.9517</td>  <td>1737.6582</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>      <td>7</td>    <td>472.3707</td>    <td>0.9</td>   <td>-790.437</td>   <td>1735.1783</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>70</td>     <td>-8.0962</td>    <td>0.9</td>  <td>-1242.8379</td>  <td>1226.6456</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>71</td>    <td>194.8095</td>    <td>0.9</td>  <td>-1034.0384</td>  <td>1423.6575</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>72</td>    <td>336.9608</td>    <td>0.9</td>   <td>-902.2225</td>  <td>1576.1441</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>73</td>      <td>-2.25</td>     <td>0.9</td>  <td>-1376.1438</td>  <td>1371.6438</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>74</td>    <td>-104.8654</td>   <td>0.9</td>  <td>-1494.5214</td>  <td>1284.7906</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>75</td>    <td>-130.6822</td>   <td>0.9</td>  <td>-1354.3993</td>  <td>1093.0348</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>76</td>     <td>97.0658</td>    <td>0.9</td>  <td>-1139.8403</td>  <td>1333.9719</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>     <td>77</td>    <td>-65.0878</td>    <td>0.9</td>  <td>-1304.2711</td>  <td>1174.0954</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>      <td>8</td>    <td>756.2115</td>    <td>0.9</td>   <td>-633.4444</td>  <td>2145.8675</td>  <td>False</td>
</tr>
<tr>
    <td>15</td>      <td>9</td>     <td>1463.15</td>  <td>0.3129</td>  <td>-241.8073</td>  <td>3168.1073</td>  <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>17</td>    <td>441.2822</td>  <td>0.8419</td>  <td>-194.7892</td>  <td>1077.3536</td>  <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>18</td>    <td>748.7211</td>  <td>0.0126</td>   <td>57.3508</td>   <td>1440.0914</td>  <td>True</td> 
</tr>
<tr>
    <td>16</td>     <td>19</td>    <td>-281.1262</td>   <td>0.9</td>   <td>-917.1976</td>  <td>354.9452</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>      <td>2</td>    <td>-48.5779</td>    <td>0.9</td>   <td>-655.8154</td>  <td>558.6596</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>20</td>    <td>1041.2363</td>  <td>0.001</td>  <td>216.7004</td>   <td>1865.7723</td>  <td>True</td> 
</tr>
<tr>
    <td>16</td>     <td>21</td>    <td>-188.9242</td>   <td>0.9</td>   <td>-811.5373</td>  <td>433.6888</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>22</td>     <td>80.5988</td>    <td>0.9</td>   <td>-785.7983</td>  <td>946.9959</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>23</td>    <td>-193.9912</td>   <td>0.9</td>   <td>-956.0682</td>  <td>568.0858</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>24</td>    <td>-355.8461</td>   <td>0.9</td>   <td>-944.2011</td>  <td>232.5089</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>25</td>    <td>-210.9123</td>   <td>0.9</td>  <td>-1001.3583</td>  <td>579.5338</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>26</td>    <td>236.9645</td>    <td>0.9</td>   <td>-420.3894</td>  <td>894.3183</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>27</td>    <td>1256.3877</td>  <td>0.001</td>  <td>224.2825</td>   <td>2288.493</td>   <td>True</td> 
</tr>
<tr>
    <td>16</td>     <td>28</td>    <td>303.7988</td>    <td>0.9</td>   <td>-353.555</td>   <td>961.1527</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>29</td>    <td>2074.7472</td>  <td>0.001</td>  <td>1411.3425</td>  <td>2738.152</td>   <td>True</td> 
</tr>
<tr>
    <td>16</td>      <td>3</td>    <td>-179.3345</td>   <td>0.9</td>  <td>-1098.5859</td>  <td>739.9169</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>30</td>     <td>25.7345</td>    <td>0.9</td>   <td>-631.6194</td>  <td>683.0883</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>31</td>    <td>-118.8933</td>   <td>0.9</td>   <td>-701.8314</td>  <td>464.0447</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>32</td>    <td>175.4122</td>    <td>0.9</td>   <td>-668.9173</td>  <td>1019.7416</td>  <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>33</td>    <td>-382.4543</td>   <td>0.9</td>  <td>-1039.8081</td>  <td>274.8996</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>34</td>    <td>-135.0012</td>   <td>0.9</td>   <td>-925.4472</td>  <td>655.4449</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>35</td>    <td>-61.8069</td>    <td>0.9</td>   <td>-702.8051</td>  <td>579.1914</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>36</td>     <td>33.115</td>     <td>0.9</td>   <td>-630.2898</td>  <td>696.5197</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>37</td>     <td>71.8655</td>    <td>0.9</td>   <td>-1155.195</td>  <td>1298.926</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>38</td>    <td>5813.3405</td>  <td>0.001</td>  <td>5095.9174</td>  <td>6530.7636</td>  <td>True</td> 
</tr>
<tr>
    <td>16</td>     <td>39</td>     <td>-63.215</td>    <td>0.9</td>   <td>-739.782</td>   <td>613.3521</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>      <td>4</td>     <td>35.2388</td>    <td>0.9</td>   <td>-726.8382</td>  <td>797.3158</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>40</td>     <td>-1.6537</td>    <td>0.9</td>   <td>-620.1721</td>  <td>616.8647</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>41</td>    <td>-276.7101</td>   <td>0.9</td>   <td>-877.1625</td>  <td>323.7424</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>42</td>    <td>-162.4701</td>   <td>0.9</td>   <td>-839.0372</td>  <td>514.0969</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>43</td>    <td>390.6359</td>    <td>0.9</td>   <td>-300.7344</td>  <td>1082.0062</td>  <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>44</td>    <td>-45.8186</td>    <td>0.9</td>   <td>-773.1823</td>  <td>681.5451</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>45</td>     <td>-97.394</td>    <td>0.9</td>   <td>-963.7911</td>  <td>769.0031</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>46</td>    <td>-208.4456</td>   <td>0.9</td>   <td>-899.8159</td>  <td>482.9247</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>47</td>    <td>-228.4488</td>   <td>0.9</td>   <td>-978.039</td>   <td>521.1414</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>48</td>    <td>-178.8762</td>   <td>0.9</td>  <td>-1405.9367</td>  <td>1048.1844</td>  <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>49</td>     <td>16.3798</td>    <td>0.9</td>   <td>-733.2104</td>   <td>765.97</td>    <td>False</td>
</tr>
<tr>
    <td>16</td>      <td>5</td>    <td>144.1138</td>    <td>0.9</td>   <td>-844.3972</td>  <td>1132.6248</td>  <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>50</td>    <td>-85.0012</td>    <td>0.9</td>  <td>-1073.5122</td>  <td>903.5098</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>51</td>    <td>574.0673</td>  <td>0.1633</td>   <td>-52.827</td>   <td>1200.9615</td>  <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>52</td>    <td>-332.6512</td>   <td>0.9</td>  <td>-1016.3955</td>  <td>351.0932</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>53</td>    <td>170.0057</td>    <td>0.9</td>   <td>-506.5613</td>  <td>846.5728</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>54</td>    <td>-293.7512</td>   <td>0.9</td>   <td>-929.8226</td>  <td>342.3202</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>55</td>    <td>155.2716</td>    <td>0.9</td>   <td>-496.3469</td>  <td>806.8901</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>56</td>    <td>466.4228</td>  <td>0.5271</td>  <td>-119.1758</td>  <td>1052.0215</td>  <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>57</td>    <td>-96.5316</td>    <td>0.9</td>   <td>-823.8953</td>  <td>630.8321</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>58</td>    <td>-65.7373</td>    <td>0.9</td>   <td>-856.1833</td>  <td>724.7088</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>59</td>    <td>809.1142</td>   <td>0.001</td>  <td>228.7459</td>   <td>1389.4826</td>  <td>True</td> 
</tr>
<tr>
    <td>16</td>      <td>6</td>    <td>176.0822</td>    <td>0.9</td>   <td>-743.1692</td>  <td>1095.3336</td>  <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>60</td>    <td>501.7188</td>  <td>0.3172</td>  <td>-83.8798</td>   <td>1087.3175</td>  <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>61</td>    <td>130.0336</td>    <td>0.9</td>   <td>-597.3301</td>  <td>857.3973</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>62</td>     <td>540.252</td>  <td>0.1758</td>  <td>-53.9251</td>   <td>1134.4291</td>  <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>63</td>    <td>604.9577</td>  <td>0.6697</td>  <td>-201.7102</td>  <td>1411.6255</td>  <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>64</td>    <td>208.3609</td>    <td>0.9</td>   <td>-468.2061</td>  <td>884.9279</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>65</td>    <td>-19.1302</td>    <td>0.9</td>   <td>-682.535</td>   <td>644.2746</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>66</td>     <td>3.8738</td>     <td>0.9</td>  <td>-1080.2619</td>  <td>1088.0096</td>  <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>67</td>    <td>-179.8012</td>   <td>0.9</td>  <td>-1168.3122</td>  <td>808.7098</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>68</td>    <td>-182.5921</td>   <td>0.9</td>   <td>-834.2106</td>  <td>469.0264</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>69</td>    <td>348.1021</td>    <td>0.9</td>   <td>-315.3027</td>  <td>1011.5068</td>  <td>False</td>
</tr>
<tr>
    <td>16</td>      <td>7</td>    <td>338.6195</td>    <td>0.9</td>   <td>-337.9475</td>  <td>1015.1865</td>  <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>70</td>    <td>-141.8473</td>   <td>0.9</td>   <td>-764.4603</td>  <td>480.7657</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>71</td>     <td>61.0584</td>    <td>0.9</td>   <td>-549.7829</td>  <td>671.8997</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>72</td>    <td>203.2096</td>    <td>0.9</td>   <td>-428.1658</td>  <td>834.5851</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>73</td>    <td>-136.0012</td>   <td>0.9</td>  <td>-1002.3983</td>  <td>730.3959</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>74</td>    <td>-238.6165</td>   <td>0.9</td>  <td>-1129.7975</td>  <td>652.5644</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>75</td>    <td>-264.4334</td>   <td>0.9</td>   <td>-864.8859</td>  <td>336.0191</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>76</td>    <td>-36.6854</td>    <td>0.9</td>   <td>-663.5796</td>  <td>590.2089</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>     <td>77</td>    <td>-198.839</td>    <td>0.9</td>   <td>-830.2145</td>  <td>432.5365</td>   <td>False</td>
</tr>
<tr>
    <td>16</td>      <td>8</td>    <td>622.4604</td>  <td>0.8274</td>  <td>-268.7206</td>  <td>1513.6414</td>  <td>False</td>
</tr>
<tr>
    <td>16</td>      <td>9</td>    <td>1329.3988</td> <td>0.0506</td>   <td>-0.9918</td>   <td>2659.7895</td>  <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>18</td>    <td>307.4389</td>    <td>0.9</td>   <td>-409.3891</td>  <td>1024.2669</td>  <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>19</td>    <td>-722.4083</td> <td>0.0114</td> <td>-1386.0621</td>  <td>-58.7546</td>   <td>True</td> 
</tr>
<tr>
    <td>17</td>      <td>2</td>    <td>-489.8601</td> <td>0.6079</td> <td>-1125.9315</td>  <td>146.2113</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>20</td>    <td>599.9542</td>  <td>0.7946</td>  <td>-246.0417</td>   <td>1445.95</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>21</td>    <td>-630.2064</td> <td>0.0813</td> <td>-1280.9725</td>   <td>20.5596</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>22</td>    <td>-360.6833</td>   <td>0.9</td>   <td>-1247.528</td>  <td>526.1613</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>23</td>    <td>-635.2733</td> <td>0.4889</td>  <td>-1420.519</td>  <td>149.9724</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>24</td>    <td>-797.1282</td>  <td>0.001</td> <td>-1415.1987</td>  <td>-179.0578</td>  <td>True</td> 
</tr>
<tr>
    <td>17</td>     <td>25</td>    <td>-652.1944</td>  <td>0.509</td>  <td>-1465.001</td>  <td>160.6121</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>26</td>    <td>-204.3177</td>   <td>0.9</td>   <td>-888.3963</td>  <td>479.7609</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>27</td>    <td>815.1056</td>  <td>0.5875</td>  <td>-234.2232</td>  <td>1864.4343</td>  <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>28</td>    <td>-137.4833</td>   <td>0.9</td>   <td>-821.562</td>   <td>546.5953</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>29</td>    <td>1633.4651</td>  <td>0.001</td>  <td>943.5699</td>   <td>2323.3602</td>  <td>True</td> 
</tr>
<tr>
    <td>17</td>      <td>3</td>    <td>-620.6167</td>   <td>0.9</td>  <td>-1559.1648</td>  <td>317.9315</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>30</td>    <td>-415.5477</td>   <td>0.9</td>  <td>-1099.6263</td>  <td>268.5309</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>31</td>    <td>-560.1755</td> <td>0.1671</td> <td>-1173.0917</td>   <td>52.7407</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>32</td>     <td>-265.87</td>    <td>0.9</td>  <td>-1131.1686</td>  <td>599.4286</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>33</td>    <td>-823.7365</td> <td>0.0012</td> <td>-1507.8151</td>  <td>-139.6578</td>  <td>True</td> 
</tr>
<tr>
    <td>17</td>     <td>34</td>    <td>-576.2833</td> <td>0.7952</td> <td>-1389.0899</td>  <td>236.5232</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>35</td>    <td>-503.089</td>  <td>0.6613</td> <td>-1171.4664</td>  <td>165.2883</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>36</td>    <td>-408.1672</td>   <td>0.9</td>  <td>-1098.0624</td>   <td>281.728</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>37</td>    <td>-369.4167</td>   <td>0.9</td>  <td>-1610.9991</td>  <td>872.1658</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>38</td>    <td>5372.0583</td>  <td>0.001</td>  <td>4630.0709</td>  <td>6114.0458</td>  <td>True</td> 
</tr>
<tr>
    <td>17</td>     <td>39</td>    <td>-504.4971</td> <td>0.7673</td> <td>-1207.0584</td>  <td>198.0642</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>      <td>4</td>    <td>-406.0433</td>   <td>0.9</td>   <td>-1191.289</td>  <td>379.2024</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>40</td>    <td>-442.9358</td> <td>0.8694</td> <td>-1089.7855</td>  <td>203.9138</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>41</td>    <td>-717.9922</td> <td>0.0043</td> <td>-1347.5894</td>   <td>-88.395</td>   <td>True</td> 
</tr>
<tr>
    <td>17</td>     <td>42</td>    <td>-603.7523</td> <td>0.3093</td> <td>-1306.3136</td>   <td>98.809</td>    <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>43</td>    <td>-50.6463</td>    <td>0.9</td>   <td>-767.4743</td>  <td>666.1817</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>44</td>    <td>-487.1007</td>   <td>0.9</td>   <td>-1238.704</td>  <td>264.5025</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>45</td>    <td>-538.6762</td>   <td>0.9</td>  <td>-1425.5208</td>  <td>348.1684</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>46</td>    <td>-649.7278</td> <td>0.1821</td> <td>-1366.5558</td>   <td>67.1002</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>47</td>    <td>-669.731</td>  <td>0.2883</td> <td>-1442.8642</td>  <td>103.4023</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>48</td>    <td>-620.1583</td>   <td>0.9</td>  <td>-1861.7408</td>  <td>621.4241</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>49</td>    <td>-424.9024</td>   <td>0.9</td>  <td>-1198.0356</td>  <td>348.2308</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>      <td>5</td>    <td>-297.1683</td>   <td>0.9</td>  <td>-1303.6491</td>  <td>709.3124</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>50</td>    <td>-526.2833</td>   <td>0.9</td>  <td>-1532.7641</td>  <td>480.1974</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>51</td>    <td>132.7851</td>    <td>0.9</td>   <td>-522.0782</td>  <td>787.6483</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>52</td>    <td>-773.9333</td> <td>0.0109</td>  <td>-1483.409</td>  <td>-64.4576</td>   <td>True</td> 
</tr>
<tr>
    <td>17</td>     <td>53</td>    <td>-271.2764</td>   <td>0.9</td>   <td>-973.8378</td>  <td>431.2849</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>54</td>    <td>-735.0333</td>  <td>0.008</td> <td>-1398.6871</td>  <td>-71.3796</td>   <td>True</td> 
</tr>
<tr>
    <td>17</td>     <td>55</td>    <td>-286.0106</td>   <td>0.9</td>   <td>-964.5798</td>  <td>392.5586</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>56</td>     <td>25.1407</td>    <td>0.9</td>   <td>-590.3065</td>  <td>640.5878</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>57</td>    <td>-537.8138</td> <td>0.7751</td>  <td>-1289.417</td>  <td>213.7895</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>58</td>    <td>-507.0194</td>   <td>0.9</td>   <td>-1319.826</td>  <td>305.7871</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>59</td>    <td>367.8321</td>    <td>0.9</td>   <td>-242.6406</td>  <td>978.3047</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>      <td>6</td>     <td>-265.2</td>     <td>0.9</td>  <td>-1203.7481</td>  <td>673.3481</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>60</td>     <td>60.4367</td>    <td>0.9</td>   <td>-555.0105</td>  <td>675.8838</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>61</td>    <td>-311.2486</td>   <td>0.9</td>  <td>-1062.8518</td>  <td>440.3547</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>62</td>     <td>98.9699</td>    <td>0.9</td>   <td>-524.6453</td>   <td>722.585</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>63</td>    <td>163.6755</td>    <td>0.9</td>   <td>-664.9152</td>  <td>992.2661</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>64</td>    <td>-232.9213</td>   <td>0.9</td>   <td>-935.4826</td>  <td>469.6401</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>65</td>    <td>-460.4124</td>   <td>0.9</td>  <td>-1150.3075</td>  <td>229.4828</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>66</td>    <td>-437.4083</td>   <td>0.9</td>  <td>-1537.9536</td>  <td>663.1369</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>67</td>    <td>-621.0833</td>   <td>0.9</td>  <td>-1627.5641</td>  <td>385.3974</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>68</td>    <td>-623.8742</td> <td>0.1557</td> <td>-1302.4434</td>   <td>54.6949</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>69</td>    <td>-93.1801</td>    <td>0.9</td>   <td>-783.0753</td>  <td>596.7151</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>      <td>7</td>    <td>-102.6626</td>   <td>0.9</td>   <td>-805.224</td>   <td>599.8987</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>70</td>    <td>-583.1295</td> <td>0.2066</td> <td>-1233.8955</td>   <td>67.6366</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>71</td>    <td>-380.2238</td>   <td>0.9</td>  <td>-1019.7366</td>  <td>259.2889</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>72</td>    <td>-238.0725</td>   <td>0.9</td>   <td>-897.2269</td>  <td>421.0818</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>73</td>    <td>-577.2833</td>   <td>0.9</td>   <td>-1464.128</td>  <td>309.5613</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>74</td>    <td>-679.8987</td>  <td>0.681</td> <td>-1590.9712</td>  <td>231.1737</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>75</td>    <td>-705.7156</td> <td>0.0063</td> <td>-1335.3128</td>  <td>-76.1183</td>   <td>True</td> 
</tr>
<tr>
    <td>17</td>     <td>76</td>    <td>-477.9675</td> <td>0.7312</td> <td>-1132.8308</td>  <td>176.8957</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>     <td>77</td>    <td>-640.1212</td> <td>0.0782</td> <td>-1299.2755</td>   <td>19.0332</td>   <td>False</td>
</tr>
<tr>
    <td>17</td>      <td>8</td>    <td>181.1782</td>    <td>0.9</td>   <td>-729.8943</td>  <td>1092.2507</td>  <td>False</td>
</tr>
<tr>
    <td>17</td>      <td>9</td>    <td>888.1167</td>    <td>0.9</td>   <td>-455.6798</td>  <td>2231.9131</td>  <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>19</td>   <td>-1029.8472</td>  <td>0.001</td> <td>-1746.6752</td>  <td>-313.0192</td>  <td>True</td> 
</tr>
<tr>
    <td>18</td>      <td>2</td>    <td>-797.299</td>  <td>0.0034</td> <td>-1488.6693</td>  <td>-105.9287</td>  <td>True</td> 
</tr>
<tr>
    <td>18</td>     <td>20</td>    <td>292.5153</td>    <td>0.9</td>   <td>-595.8062</td>  <td>1180.8367</td>  <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>21</td>    <td>-937.6453</td>  <td>0.001</td> <td>-1642.5584</td>  <td>-232.7322</td>  <td>True</td> 
</tr>
<tr>
    <td>18</td>     <td>22</td>    <td>-668.1222</td> <td>0.7599</td> <td>-1595.4298</td>  <td>259.1854</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>23</td>    <td>-942.7122</td> <td>0.0048</td> <td>-1773.3848</td>  <td>-112.0397</td>  <td>True</td> 
</tr>
<tr>
    <td>18</td>     <td>24</td>   <td>-1104.5671</td>  <td>0.001</td> <td>-1779.4131</td>  <td>-429.7211</td>  <td>True</td> 
</tr>
<tr>
    <td>18</td>     <td>25</td>    <td>-959.6333</td> <td>0.0064</td> <td>-1816.4066</td>   <td>-102.86</td>   <td>True</td> 
</tr>
<tr>
    <td>18</td>     <td>26</td>    <td>-511.7566</td> <td>0.8364</td> <td>-1247.5348</td>  <td>224.0216</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>27</td>    <td>507.6667</td>    <td>0.9</td>   <td>-576.0754</td>  <td>1591.4087</td>  <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>28</td>    <td>-444.9222</td>   <td>0.9</td>  <td>-1180.7005</td>   <td>290.856</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>29</td>    <td>1326.0262</td>  <td>0.001</td>   <td>584.837</td>   <td>2067.2153</td>  <td>True</td> 
</tr>
<tr>
    <td>18</td>      <td>3</td>    <td>-928.0556</td>  <td>0.104</td> <td>-1904.9274</td>   <td>48.8163</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>30</td>    <td>-722.9866</td> <td>0.0658</td> <td>-1458.7648</td>   <td>12.7916</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>31</td>    <td>-867.6144</td>  <td>0.001</td>  <td>-1537.743</td>  <td>-197.4858</td>  <td>True</td> 
</tr>
<tr>
    <td>18</td>     <td>32</td>    <td>-573.3089</td>   <td>0.9</td>  <td>-1480.0325</td>  <td>333.4147</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>33</td>   <td>-1131.1753</td>  <td>0.001</td> <td>-1866.9536</td>  <td>-395.3971</td>  <td>True</td> 
</tr>
<tr>
    <td>18</td>     <td>34</td>    <td>-883.7222</td> <td>0.0304</td> <td>-1740.4955</td>  <td>-26.9489</td>   <td>True</td> 
</tr>
<tr>
    <td>18</td>     <td>35</td>    <td>-810.5279</td> <td>0.0059</td> <td>-1531.7313</td>  <td>-89.3246</td>   <td>True</td> 
</tr>
<tr>
    <td>18</td>     <td>36</td>    <td>-715.6061</td> <td>0.0847</td> <td>-1456.7953</td>   <td>25.5831</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>37</td>    <td>-676.8556</td>   <td>0.9</td>  <td>-1947.6557</td>  <td>593.9446</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>38</td>    <td>5064.6194</td>  <td>0.001</td>  <td>4274.7135</td>  <td>5854.5254</td>  <td>True</td> 
</tr>
<tr>
    <td>18</td>     <td>39</td>    <td>-811.936</td>  <td>0.0137</td>  <td>-1564.929</td>   <td>-58.943</td>   <td>True</td> 
</tr>
<tr>
    <td>18</td>      <td>4</td>    <td>-713.4822</td> <td>0.3106</td> <td>-1544.1548</td>  <td>117.1903</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>40</td>    <td>-750.3747</td> <td>0.0158</td> <td>-1451.6739</td>  <td>-49.0755</td>   <td>True</td> 
</tr>
<tr>
    <td>18</td>     <td>41</td>   <td>-1025.4311</td>  <td>0.001</td> <td>-1710.8498</td>  <td>-340.0125</td>  <td>True</td> 
</tr>
<tr>
    <td>18</td>     <td>42</td>    <td>-911.1912</td> <td>0.0011</td> <td>-1664.1842</td>  <td>-158.1982</td>  <td>True</td> 
</tr>
<tr>
    <td>18</td>     <td>43</td>    <td>-358.0852</td>   <td>0.9</td>  <td>-1124.4065</td>  <td>408.2362</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>44</td>    <td>-794.5396</td> <td>0.0546</td> <td>-1593.4848</td>   <td>4.4056</td>    <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>45</td>    <td>-846.1151</td> <td>0.1703</td> <td>-1773.4227</td>   <td>81.1925</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>46</td>    <td>-957.1667</td>  <td>0.001</td>  <td>-1723.488</td>  <td>-190.8453</td>  <td>True</td> 
</tr>
<tr>
    <td>18</td>     <td>47</td>    <td>-977.1698</td> <td>0.0015</td> <td>-1796.4018</td>  <td>-157.9379</td>  <td>True</td> 
</tr>
<tr>
    <td>18</td>     <td>48</td>    <td>-927.5972</td>  <td>0.731</td> <td>-2198.3974</td>   <td>343.203</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>49</td>    <td>-732.3413</td>  <td>0.212</td> <td>-1551.5732</td>   <td>86.8907</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>      <td>5</td>    <td>-604.6072</td>   <td>0.9</td>  <td>-1646.9169</td>  <td>437.7025</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>50</td>    <td>-833.7222</td> <td>0.5167</td> <td>-1876.0319</td>  <td>208.5875</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>51</td>    <td>-174.6538</td>   <td>0.9</td>   <td>-883.3511</td>  <td>534.0435</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>52</td>   <td>-1081.3722</td>  <td>0.001</td> <td>-1840.8206</td>  <td>-321.9239</td>  <td>True</td> 
</tr>
<tr>
    <td>18</td>     <td>53</td>    <td>-578.7153</td> <td>0.6127</td> <td>-1331.7083</td>  <td>174.2777</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>54</td>   <td>-1042.4722</td>  <td>0.001</td> <td>-1759.3002</td>  <td>-325.6442</td>  <td>True</td> 
</tr>
<tr>
    <td>18</td>     <td>55</td>    <td>-593.4495</td> <td>0.4788</td> <td>-1324.1082</td>  <td>137.2092</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>56</td>    <td>-282.2982</td>   <td>0.9</td>   <td>-954.7425</td>   <td>390.146</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>57</td>    <td>-845.2527</td> <td>0.0195</td> <td>-1644.1979</td>  <td>-46.3074</td>   <td>True</td> 
</tr>
<tr>
    <td>18</td>     <td>58</td>    <td>-814.4583</td> <td>0.1031</td> <td>-1671.2316</td>   <td>42.315</td>    <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>59</td>     <td>60.3932</td>    <td>0.9</td>   <td>-607.5012</td>  <td>728.2876</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>      <td>6</td>    <td>-572.6389</td>   <td>0.9</td>  <td>-1549.5108</td>   <td>404.233</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>60</td>    <td>-247.0022</td>   <td>0.9</td>   <td>-919.4465</td>   <td>425.442</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>61</td>    <td>-618.6874</td> <td>0.5949</td> <td>-1417.6327</td>  <td>180.2578</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>62</td>    <td>-208.469</td>    <td>0.9</td>   <td>-888.3969</td>  <td>471.4589</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>63</td>    <td>-143.7634</td>   <td>0.9</td>  <td>-1015.5251</td>  <td>727.9983</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>64</td>    <td>-540.3602</td> <td>0.7688</td> <td>-1293.3531</td>  <td>212.6328</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>65</td>    <td>-767.8513</td> <td>0.0282</td> <td>-1509.0404</td>  <td>-26.6621</td>   <td>True</td> 
</tr>
<tr>
    <td>18</td>     <td>66</td>    <td>-744.8472</td>   <td>0.9</td>  <td>-1878.2518</td>  <td>388.5573</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>67</td>    <td>-928.5222</td> <td>0.2198</td> <td>-1970.8319</td>  <td>113.7875</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>68</td>    <td>-931.3131</td>  <td>0.001</td> <td>-1661.9719</td>  <td>-200.6544</td>  <td>True</td> 
</tr>
<tr>
    <td>18</td>     <td>69</td>    <td>-400.619</td>    <td>0.9</td>  <td>-1141.8082</td>  <td>340.5702</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>      <td>7</td>    <td>-410.1015</td>   <td>0.9</td>  <td>-1163.0945</td>  <td>342.8915</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>70</td>    <td>-890.5684</td>  <td>0.001</td> <td>-1595.4815</td>  <td>-185.6553</td>  <td>True</td> 
</tr>
<tr>
    <td>18</td>     <td>71</td>    <td>-687.6627</td> <td>0.0585</td> <td>-1382.2004</td>    <td>6.875</td>    <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>72</td>    <td>-545.5114</td> <td>0.6222</td> <td>-1258.1758</td>   <td>167.153</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>73</td>    <td>-884.7222</td> <td>0.0979</td> <td>-1812.0298</td>   <td>42.5854</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>     <td>74</td>    <td>-987.3376</td> <td>0.0269</td> <td>-1937.8422</td>   <td>-36.833</td>   <td>True</td> 
</tr>
<tr>
    <td>18</td>     <td>75</td>   <td>-1013.1544</td>  <td>0.001</td> <td>-1698.5731</td>  <td>-327.7358</td>  <td>True</td> 
</tr>
<tr>
    <td>18</td>     <td>76</td>    <td>-785.4064</td> <td>0.0079</td> <td>-1494.1038</td>  <td>-76.7091</td>   <td>True</td> 
</tr>
<tr>
    <td>18</td>     <td>77</td>    <td>-947.5601</td>  <td>0.001</td> <td>-1660.2244</td>  <td>-234.8957</td>  <td>True</td> 
</tr>
<tr>
    <td>18</td>      <td>8</td>    <td>-126.2607</td>   <td>0.9</td>  <td>-1076.7653</td>   <td>824.244</td>   <td>False</td>
</tr>
<tr>
    <td>18</td>      <td>9</td>    <td>580.6778</td>    <td>0.9</td>   <td>-790.1595</td>  <td>1951.5151</td>  <td>False</td>
</tr>
<tr>
    <td>19</td>      <td>2</td>    <td>232.5483</td>    <td>0.9</td>   <td>-403.5231</td>  <td>868.6197</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>20</td>    <td>1322.3625</td>  <td>0.001</td>  <td>476.3666</td>   <td>2168.3584</td>  <td>True</td> 
</tr>
<tr>
    <td>19</td>     <td>21</td>     <td>92.2019</td>    <td>0.9</td>   <td>-558.5641</td>   <td>742.968</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>22</td>     <td>361.725</td>    <td>0.9</td>   <td>-525.1196</td>  <td>1248.5696</td>  <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>23</td>     <td>87.135</td>     <td>0.9</td>   <td>-698.1107</td>  <td>872.3807</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>24</td>    <td>-74.7199</td>    <td>0.9</td>   <td>-692.7903</td>  <td>543.3505</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>25</td>     <td>70.2139</td>    <td>0.9</td>   <td>-742.5926</td>  <td>883.0204</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>26</td>    <td>518.0906</td>   <td>0.647</td>  <td>-165.988</td>   <td>1202.1692</td>  <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>27</td>    <td>1537.5139</td>  <td>0.001</td>  <td>488.1852</td>   <td>2586.8426</td>  <td>True</td> 
</tr>
<tr>
    <td>19</td>     <td>28</td>     <td>584.925</td>  <td>0.3224</td>  <td>-99.1536</td>   <td>1269.0036</td>  <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>29</td>    <td>2355.8734</td>  <td>0.001</td>  <td>1665.9782</td>  <td>3045.7686</td>  <td>True</td> 
</tr>
<tr>
    <td>19</td>      <td>3</td>    <td>101.7917</td>    <td>0.9</td>   <td>-836.7565</td>  <td>1040.3398</td>  <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>30</td>    <td>306.8606</td>    <td>0.9</td>   <td>-377.218</td>   <td>990.9392</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>31</td>    <td>162.2328</td>    <td>0.9</td>   <td>-450.6833</td>   <td>775.149</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>32</td>    <td>456.5383</td>    <td>0.9</td>   <td>-408.7603</td>  <td>1321.837</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>33</td>    <td>-101.3281</td>   <td>0.9</td>   <td>-785.4067</td>  <td>582.7505</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>34</td>     <td>146.125</td>    <td>0.9</td>   <td>-666.6815</td>  <td>958.9315</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>35</td>    <td>219.3193</td>    <td>0.9</td>   <td>-449.058</td>   <td>887.6966</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>36</td>    <td>314.2411</td>    <td>0.9</td>   <td>-375.654</td>   <td>1004.1363</td>  <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>37</td>    <td>352.9917</td>    <td>0.9</td>   <td>-888.5908</td>  <td>1594.5741</td>  <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>38</td>    <td>6094.4667</td>  <td>0.001</td>  <td>5352.4792</td>  <td>6836.4541</td>  <td>True</td> 
</tr>
<tr>
    <td>19</td>     <td>39</td>    <td>217.9112</td>    <td>0.9</td>   <td>-484.6501</td>  <td>920.4725</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>      <td>4</td>     <td>316.365</td>    <td>0.9</td>   <td>-468.8807</td>  <td>1101.6107</td>  <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>40</td>    <td>279.4725</td>    <td>0.9</td>   <td>-367.3772</td>  <td>926.3222</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>41</td>     <td>4.4161</td>     <td>0.9</td>   <td>-625.1811</td>  <td>634.0133</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>42</td>     <td>118.656</td>    <td>0.9</td>   <td>-583.9053</td>  <td>821.2173</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>43</td>     <td>671.762</td>   <td>0.125</td>  <td>-45.0659</td>    <td>1388.59</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>44</td>    <td>235.3076</td>    <td>0.9</td>   <td>-516.2956</td>  <td>986.9108</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>45</td>    <td>183.7321</td>    <td>0.9</td>   <td>-703.1125</td>  <td>1070.5768</td>  <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>46</td>     <td>72.6806</td>    <td>0.9</td>   <td>-644.1474</td>  <td>789.5085</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>47</td>     <td>52.6774</td>    <td>0.9</td>   <td>-720.4558</td>  <td>825.8106</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>48</td>     <td>102.25</td>     <td>0.9</td>  <td>-1139.3325</td>  <td>1343.8325</td>  <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>49</td>     <td>297.506</td>    <td>0.9</td>   <td>-475.6273</td>  <td>1070.6392</td>  <td>False</td>
</tr>
<tr>
    <td>19</td>      <td>5</td>     <td>425.24</td>     <td>0.9</td>   <td>-581.2407</td>  <td>1431.7207</td>  <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>50</td>     <td>196.125</td>    <td>0.9</td>   <td>-810.3557</td>  <td>1202.6057</td>  <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>51</td>    <td>855.1934</td>   <td>0.001</td>  <td>200.3302</td>   <td>1510.0567</td>  <td>True</td> 
</tr>
<tr>
    <td>19</td>     <td>52</td>     <td>-51.525</td>    <td>0.9</td>   <td>-761.0007</td>  <td>657.9507</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>53</td>    <td>451.1319</td>    <td>0.9</td>   <td>-251.4294</td>  <td>1153.6932</td>  <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>54</td>     <td>-12.625</td>    <td>0.9</td>   <td>-676.2787</td>  <td>651.0287</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>55</td>    <td>436.3977</td>    <td>0.9</td>   <td>-242.1714</td>  <td>1114.9669</td>  <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>56</td>     <td>747.549</td>   <td>0.001</td>  <td>132.1018</td>   <td>1362.9962</td>  <td>True</td> 
</tr>
<tr>
    <td>19</td>     <td>57</td>    <td>184.5946</td>    <td>0.9</td>   <td>-567.0087</td>  <td>936.1978</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>58</td>    <td>215.3889</td>    <td>0.9</td>   <td>-597.4176</td>  <td>1028.1954</td>  <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>59</td>    <td>1090.2404</td>  <td>0.001</td>  <td>479.7677</td>   <td>1700.713</td>   <td>True</td> 
</tr>
<tr>
    <td>19</td>      <td>6</td>    <td>457.2083</td>    <td>0.9</td>   <td>-481.3398</td>  <td>1395.7565</td>  <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>60</td>     <td>782.845</td>   <td>0.001</td>  <td>167.3978</td>   <td>1398.2922</td>  <td>True</td> 
</tr>
<tr>
    <td>19</td>     <td>61</td>    <td>411.1598</td>    <td>0.9</td>   <td>-340.4435</td>  <td>1162.763</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>62</td>    <td>821.3782</td>   <td>0.001</td>   <td>197.763</td>   <td>1444.9934</td>  <td>True</td> 
</tr>
<tr>
    <td>19</td>     <td>63</td>    <td>886.0838</td>   <td>0.016</td>   <td>57.4932</td>   <td>1714.6745</td>  <td>True</td> 
</tr>
<tr>
    <td>19</td>     <td>64</td>    <td>489.4871</td>  <td>0.8328</td>  <td>-213.0742</td>  <td>1192.0484</td>  <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>65</td>     <td>261.996</td>    <td>0.9</td>   <td>-427.8992</td>  <td>951.8911</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>66</td>      <td>285.0</td>     <td>0.9</td>   <td>-815.5452</td>  <td>1385.5452</td>  <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>67</td>     <td>101.325</td>    <td>0.9</td>   <td>-905.1557</td>  <td>1107.8057</td>  <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>68</td>     <td>98.5341</td>    <td>0.9</td>   <td>-580.0351</td>  <td>777.1033</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>69</td>    <td>629.2282</td>  <td>0.1712</td>  <td>-60.6669</td>   <td>1319.1234</td>  <td>False</td>
</tr>
<tr>
    <td>19</td>      <td>7</td>    <td>619.7457</td>  <td>0.2419</td>  <td>-82.8156</td>   <td>1322.307</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>70</td>    <td>139.2788</td>    <td>0.9</td>   <td>-511.4872</td>  <td>790.0449</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>71</td>    <td>342.1845</td>    <td>0.9</td>   <td>-297.3282</td>  <td>981.6973</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>72</td>    <td>484.3358</td>  <td>0.7162</td>  <td>-174.8185</td>  <td>1143.4902</td>  <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>73</td>     <td>145.125</td>    <td>0.9</td>   <td>-741.7196</td>  <td>1031.9696</td>  <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>74</td>     <td>42.5096</td>    <td>0.9</td>   <td>-868.5628</td>  <td>953.5821</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>75</td>     <td>16.6928</td>    <td>0.9</td>   <td>-612.9044</td>   <td>646.29</td>    <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>76</td>    <td>244.4408</td>    <td>0.9</td>   <td>-410.4225</td>   <td>899.304</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>     <td>77</td>     <td>82.2872</td>    <td>0.9</td>   <td>-576.8672</td>  <td>741.4415</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>      <td>8</td>    <td>903.5865</td>   <td>0.057</td>   <td>-7.4859</td>   <td>1814.659</td>   <td>False</td>
</tr>
<tr>
    <td>19</td>      <td>9</td>    <td>1610.525</td>  <td>0.0014</td>  <td>266.7286</td>   <td>2954.3214</td>  <td>True</td> 
</tr>
<tr>
     <td>2</td>     <td>20</td>    <td>1089.8142</td>  <td>0.001</td>  <td>265.2783</td>   <td>1914.3502</td>  <td>True</td> 
</tr>
<tr>
     <td>2</td>     <td>21</td>    <td>-140.3463</td>   <td>0.9</td>   <td>-762.9594</td>  <td>482.2667</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>22</td>    <td>129.1767</td>    <td>0.9</td>   <td>-737.2203</td>  <td>995.5738</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>23</td>    <td>-145.4133</td>   <td>0.9</td>   <td>-907.4903</td>  <td>616.6637</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>24</td>    <td>-307.2682</td>   <td>0.9</td>   <td>-895.6232</td>  <td>281.0868</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>25</td>    <td>-162.3344</td>   <td>0.9</td>   <td>-952.7804</td>  <td>628.1117</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>26</td>    <td>285.5424</td>    <td>0.9</td>   <td>-371.8115</td>  <td>942.8962</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>27</td>    <td>1304.9656</td>  <td>0.001</td>  <td>272.8604</td>   <td>2337.0709</td>  <td>True</td> 
</tr>
<tr>
     <td>2</td>     <td>28</td>    <td>352.3767</td>    <td>0.9</td>   <td>-304.9771</td>  <td>1009.7306</td>  <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>29</td>    <td>2123.3251</td>  <td>0.001</td>  <td>1459.9204</td>  <td>2786.7299</td>  <td>True</td> 
</tr>
<tr>
     <td>2</td>      <td>3</td>    <td>-130.7566</td>   <td>0.9</td>   <td>-1050.008</td>  <td>788.4948</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>30</td>     <td>74.3124</td>    <td>0.9</td>   <td>-583.0415</td>  <td>731.6662</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>31</td>    <td>-70.3154</td>    <td>0.9</td>   <td>-653.2535</td>  <td>512.6227</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>32</td>    <td>223.9901</td>    <td>0.9</td>   <td>-620.3394</td>  <td>1068.3195</td>  <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>33</td>    <td>-333.8764</td>   <td>0.9</td>   <td>-991.2302</td>  <td>323.4775</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>34</td>    <td>-86.4233</td>    <td>0.9</td>   <td>-876.8693</td>  <td>704.0228</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>35</td>     <td>-13.229</td>    <td>0.9</td>   <td>-654.2272</td>  <td>627.7693</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>36</td>     <td>81.6929</td>    <td>0.9</td>   <td>-581.7119</td>  <td>745.0976</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>37</td>    <td>120.4434</td>    <td>0.9</td>  <td>-1106.6171</td>  <td>1347.504</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>38</td>    <td>5861.9184</td>  <td>0.001</td>  <td>5144.4953</td>  <td>6579.3415</td>  <td>True</td> 
</tr>
<tr>
     <td>2</td>     <td>39</td>     <td>-14.637</td>    <td>0.9</td>   <td>-691.2041</td>   <td>661.93</td>    <td>False</td>
</tr>
<tr>
     <td>2</td>      <td>4</td>     <td>83.8167</td>    <td>0.9</td>   <td>-678.2603</td>  <td>845.8937</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>40</td>     <td>46.9242</td>    <td>0.9</td>   <td>-571.5942</td>  <td>665.4426</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>41</td>    <td>-228.1321</td>   <td>0.9</td>   <td>-828.5846</td>  <td>372.3204</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>42</td>    <td>-113.8922</td>   <td>0.9</td>   <td>-790.4592</td>  <td>562.6748</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>43</td>    <td>439.2138</td>    <td>0.9</td>   <td>-252.1565</td>  <td>1130.5841</td>  <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>44</td>     <td>2.7594</td>     <td>0.9</td>   <td>-724.6044</td>  <td>730.1231</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>45</td>    <td>-48.8161</td>    <td>0.9</td>   <td>-915.2132</td>   <td>817.581</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>46</td>    <td>-159.8677</td>   <td>0.9</td>   <td>-851.238</td>   <td>531.5026</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>47</td>    <td>-179.8709</td>   <td>0.9</td>   <td>-929.4611</td>  <td>569.7194</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>48</td>    <td>-130.2983</td>   <td>0.9</td>  <td>-1357.3588</td>  <td>1096.7623</td>  <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>49</td>     <td>64.9577</td>    <td>0.9</td>   <td>-684.6325</td>  <td>814.5479</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>      <td>5</td>    <td>192.6917</td>    <td>0.9</td>   <td>-795.8193</td>  <td>1181.2028</td>  <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>50</td>    <td>-36.4233</td>    <td>0.9</td>  <td>-1024.9343</td>  <td>952.0878</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>51</td>    <td>622.6452</td>  <td>0.0557</td>   <td>-4.2491</td>   <td>1249.5394</td>  <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>52</td>    <td>-284.0733</td>   <td>0.9</td>   <td>-967.8176</td>  <td>399.6711</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>53</td>    <td>218.5836</td>    <td>0.9</td>   <td>-457.9834</td>  <td>895.1507</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>54</td>    <td>-245.1733</td>   <td>0.9</td>   <td>-881.2447</td>  <td>390.8981</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>55</td>    <td>203.8495</td>    <td>0.9</td>   <td>-447.769</td>    <td>855.468</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>56</td>    <td>515.0007</td>  <td>0.2494</td>  <td>-70.5979</td>   <td>1100.5994</td>  <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>57</td>    <td>-47.9537</td>    <td>0.9</td>   <td>-775.3174</td>   <td>679.41</td>    <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>58</td>    <td>-17.1594</td>    <td>0.9</td>   <td>-807.6054</td>  <td>773.2867</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>59</td>    <td>857.6921</td>   <td>0.001</td>  <td>277.3238</td>   <td>1438.0605</td>  <td>True</td> 
</tr>
<tr>
     <td>2</td>      <td>6</td>    <td>224.6601</td>    <td>0.9</td>   <td>-694.5913</td>  <td>1143.9115</td>  <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>60</td>    <td>550.2967</td>  <td>0.1207</td>  <td>-35.3019</td>   <td>1135.8954</td>  <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>61</td>    <td>178.6115</td>    <td>0.9</td>   <td>-548.7522</td>  <td>905.9752</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>62</td>    <td>588.8299</td>  <td>0.0577</td>   <td>-5.3472</td>   <td>1183.007</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>63</td>    <td>653.5356</td>  <td>0.4853</td>  <td>-153.1323</td>  <td>1460.2034</td>  <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>64</td>    <td>256.9388</td>    <td>0.9</td>   <td>-419.6282</td>  <td>933.5058</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>65</td>     <td>29.4477</td>    <td>0.9</td>   <td>-633.9571</td>  <td>692.8525</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>66</td>     <td>52.4517</td>    <td>0.9</td>   <td>-1031.684</td>  <td>1136.5875</td>  <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>67</td>    <td>-131.2233</td>   <td>0.9</td>  <td>-1119.7343</td>  <td>857.2878</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>68</td>    <td>-134.0142</td>   <td>0.9</td>   <td>-785.6327</td>  <td>517.6043</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>69</td>     <td>396.68</td>     <td>0.9</td>   <td>-266.7248</td>  <td>1060.0847</td>  <td>False</td>
</tr>
<tr>
     <td>2</td>      <td>7</td>    <td>387.1974</td>    <td>0.9</td>   <td>-289.3696</td>  <td>1063.7645</td>  <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>70</td>    <td>-93.2694</td>    <td>0.9</td>   <td>-715.8824</td>  <td>529.3436</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>71</td>    <td>109.6363</td>    <td>0.9</td>   <td>-501.205</td>   <td>720.4776</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>72</td>    <td>251.7876</td>    <td>0.9</td>   <td>-379.5879</td>   <td>883.163</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>73</td>    <td>-87.4233</td>    <td>0.9</td>   <td>-953.8203</td>  <td>778.9738</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>74</td>    <td>-190.0386</td>   <td>0.9</td>  <td>-1081.2196</td>  <td>701.1423</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>75</td>    <td>-215.8555</td>   <td>0.9</td>   <td>-816.308</td>    <td>384.597</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>76</td>     <td>11.8925</td>    <td>0.9</td>   <td>-615.0017</td>  <td>638.7868</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>     <td>77</td>    <td>-150.2611</td>   <td>0.9</td>   <td>-781.6366</td>  <td>481.1144</td>   <td>False</td>
</tr>
<tr>
     <td>2</td>      <td>8</td>    <td>671.0383</td>  <td>0.6604</td>  <td>-220.1427</td>  <td>1562.2193</td>  <td>False</td>
</tr>
<tr>
     <td>2</td>      <td>9</td>    <td>1377.9767</td> <td>0.0283</td>   <td>47.5861</td>   <td>2708.3674</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>21</td>   <td>-1230.1606</td>  <td>0.001</td> <td>-2066.0847</td>  <td>-394.2365</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>22</td>    <td>-960.6375</td> <td>0.1305</td> <td>-1991.0578</td>   <td>69.7828</td>   <td>False</td>
</tr>
<tr>
    <td>20</td>     <td>23</td>   <td>-1235.2275</td>  <td>0.001</td> <td>-2179.6233</td>  <td>-290.8317</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>24</td>   <td>-1397.0824</td>  <td>0.001</td> <td>-2207.8128</td>  <td>-586.352</td>   <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>25</td>   <td>-1252.1486</td>  <td>0.001</td> <td>-2219.5819</td>  <td>-284.7153</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>26</td>    <td>-804.2719</td> <td>0.1294</td> <td>-1666.3834</td>   <td>57.8396</td>   <td>False</td>
</tr>
<tr>
    <td>20</td>     <td>27</td>    <td>215.1514</td>    <td>0.9</td>   <td>-958.0338</td>  <td>1388.3366</td>  <td>False</td>
</tr>
<tr>
    <td>20</td>     <td>28</td>    <td>-737.4375</td> <td>0.3214</td>  <td>-1599.549</td>   <td>124.674</td>   <td>False</td>
</tr>
<tr>
    <td>20</td>     <td>29</td>    <td>1033.5109</td> <td>0.0015</td>  <td>166.7768</td>   <td>1900.245</td>   <td>True</td> 
</tr>
<tr>
    <td>20</td>      <td>3</td>   <td>-1220.5708</td> <td>0.0048</td> <td>-2295.8128</td>  <td>-145.3289</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>30</td>   <td>-1015.5019</td> <td>0.0021</td> <td>-1877.6134</td>  <td>-153.3904</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>31</td>   <td>-1160.1297</td>  <td>0.001</td> <td>-1966.9375</td>  <td>-353.3218</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>32</td>    <td>-865.8242</td> <td>0.3207</td> <td>-1877.7601</td>  <td>146.1118</td>   <td>False</td>
</tr>
<tr>
    <td>20</td>     <td>33</td>   <td>-1423.6906</td>  <td>0.001</td> <td>-2285.8021</td>  <td>-561.5791</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>34</td>   <td>-1176.2375</td>  <td>0.001</td> <td>-2143.6708</td>  <td>-208.8042</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>35</td>   <td>-1103.0432</td>  <td>0.001</td> <td>-1952.7496</td>  <td>-253.3368</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>36</td>   <td>-1008.1214</td> <td>0.0028</td> <td>-1874.8555</td>  <td>-141.3872</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>37</td>    <td>-969.3708</td>  <td>0.764</td>  <td>-2317.258</td>  <td>378.5163</td>   <td>False</td>
</tr>
<tr>
    <td>20</td>     <td>38</td>    <td>4772.1042</td>  <td>0.001</td>  <td>3863.3588</td>  <td>5680.8495</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>39</td>   <td>-1104.4513</td>  <td>0.001</td> <td>-1981.3008</td>  <td>-227.6018</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>      <td>4</td>   <td>-1005.9975</td> <td>0.0172</td> <td>-1950.3933</td>  <td>-61.6017</td>   <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>40</td>    <td>-1042.89</td>   <td>0.001</td> <td>-1875.7688</td>  <td>-210.0112</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>41</td>   <td>-1317.9464</td>  <td>0.001</td> <td>-2137.4983</td>  <td>-498.3945</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>42</td>   <td>-1203.7065</td>  <td>0.001</td>  <td>-2080.556</td>  <td>-326.8569</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>43</td>    <td>-650.6005</td> <td>0.7235</td> <td>-1538.9219</td>   <td>237.721</td>   <td>False</td>
</tr>
<tr>
    <td>20</td>     <td>44</td>   <td>-1087.0549</td> <td>0.0017</td> <td>-2003.6683</td>  <td>-170.4415</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>45</td>   <td>-1138.6304</td> <td>0.0084</td> <td>-2169.0507</td>   <td>-108.21</td>   <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>46</td>   <td>-1249.6819</td>  <td>0.001</td> <td>-2138.0034</td>  <td>-361.3605</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>47</td>   <td>-1269.6851</td>  <td>0.001</td> <td>-2204.0339</td>  <td>-335.3363</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>48</td>   <td>-1220.1125</td> <td>0.1848</td> <td>-2567.9996</td>  <td>127.7746</td>   <td>False</td>
</tr>
<tr>
    <td>20</td>     <td>49</td>   <td>-1024.8565</td> <td>0.0098</td> <td>-1959.2053</td>  <td>-90.5078</td>   <td>True</td> 
</tr>
<tr>
    <td>20</td>      <td>5</td>    <td>-897.1225</td> <td>0.5458</td>  <td>-2032.145</td>    <td>237.9</td>    <td>False</td>
</tr>
<tr>
    <td>20</td>     <td>50</td>   <td>-1126.2375</td> <td>0.0566</td>  <td>-2261.26</td>     <td>8.785</td>    <td>False</td>
</tr>
<tr>
    <td>20</td>     <td>51</td>    <td>-467.1691</td>   <td>0.9</td>  <td>-1306.2868</td>  <td>371.9486</td>   <td>False</td>
</tr>
<tr>
    <td>20</td>     <td>52</td>   <td>-1373.8875</td>  <td>0.001</td> <td>-2256.2868</td>  <td>-491.4882</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>53</td>    <td>-871.2306</td> <td>0.0554</td> <td>-1748.0801</td>   <td>5.6189</td>    <td>False</td>
</tr>
<tr>
    <td>20</td>     <td>54</td>   <td>-1334.9875</td>  <td>0.001</td> <td>-2180.9834</td>  <td>-488.9916</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>55</td>    <td>-885.9648</td> <td>0.0297</td> <td>-1743.7111</td>  <td>-28.2184</td>   <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>56</td>    <td>-574.8135</td> <td>0.7898</td> <td>-1383.5458</td>  <td>233.9188</td>   <td>False</td>
</tr>
<tr>
    <td>20</td>     <td>57</td>   <td>-1137.7679</td>  <td>0.001</td> <td>-2054.3813</td>  <td>-221.1545</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>58</td>   <td>-1106.9736</td>  <td>0.004</td> <td>-2074.4069</td>  <td>-139.5403</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>59</td>    <td>-232.1221</td>   <td>0.9</td>  <td>-1037.0753</td>   <td>572.831</td>   <td>False</td>
</tr>
<tr>
    <td>20</td>      <td>6</td>    <td>-865.1542</td> <td>0.5022</td> <td>-1940.3961</td>  <td>210.0878</td>   <td>False</td>
</tr>
<tr>
    <td>20</td>     <td>60</td>    <td>-539.5175</td>   <td>0.9</td>  <td>-1348.2498</td>  <td>269.2148</td>   <td>False</td>
</tr>
<tr>
    <td>20</td>     <td>61</td>    <td>-911.2027</td> <td>0.0549</td> <td>-1827.8161</td>   <td>5.4107</td>    <td>False</td>
</tr>
<tr>
    <td>20</td>     <td>62</td>    <td>-500.9843</td>   <td>0.9</td>  <td>-1315.9497</td>  <td>313.9811</td>   <td>False</td>
</tr>
<tr>
    <td>20</td>     <td>63</td>    <td>-436.2787</td>   <td>0.9</td>  <td>-1417.0106</td>  <td>544.4533</td>   <td>False</td>
</tr>
<tr>
    <td>20</td>     <td>64</td>    <td>-832.8754</td> <td>0.1042</td>  <td>-1709.725</td>   <td>43.9741</td>   <td>False</td>
</tr>
<tr>
    <td>20</td>     <td>65</td>   <td>-1060.3665</td>  <td>0.001</td> <td>-1927.1007</td>  <td>-193.6324</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>66</td>   <td>-1037.3625</td> <td>0.3369</td> <td>-2256.5723</td>  <td>181.8473</td>   <td>False</td>
</tr>
<tr>
    <td>20</td>     <td>67</td>   <td>-1221.0375</td> <td>0.0143</td>  <td>-2356.06</td>    <td>-86.015</td>   <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>68</td>   <td>-1223.8284</td>  <td>0.001</td> <td>-2081.5748</td>  <td>-366.0821</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>69</td>    <td>-693.1343</td> <td>0.5173</td> <td>-1559.8684</td>  <td>173.5998</td>   <td>False</td>
</tr>
<tr>
    <td>20</td>      <td>7</td>    <td>-702.6168</td> <td>0.5124</td> <td>-1579.4663</td>  <td>174.2327</td>   <td>False</td>
</tr>
<tr>
    <td>20</td>     <td>70</td>   <td>-1183.0837</td>  <td>0.001</td> <td>-2019.0078</td>  <td>-347.1595</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>71</td>    <td>-980.178</td>  <td>0.0018</td> <td>-1807.3716</td>  <td>-152.9844</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>72</td>    <td>-838.0267</td> <td>0.0544</td> <td>-1680.4975</td>   <td>4.4442</td>    <td>False</td>
</tr>
<tr>
    <td>20</td>     <td>73</td>   <td>-1177.2375</td> <td>0.0042</td> <td>-2207.6578</td>  <td>-146.8172</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>74</td>   <td>-1279.8529</td>  <td>0.001</td> <td>-2331.1976</td>  <td>-228.5082</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>75</td>   <td>-1305.6697</td>  <td>0.001</td> <td>-2125.2216</td>  <td>-486.1178</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>76</td>   <td>-1077.9217</td>  <td>0.001</td> <td>-1917.0394</td>  <td>-238.804</td>   <td>True</td> 
</tr>
<tr>
    <td>20</td>     <td>77</td>   <td>-1240.0753</td>  <td>0.001</td> <td>-2082.5462</td>  <td>-397.6045</td>  <td>True</td> 
</tr>
<tr>
    <td>20</td>      <td>8</td>    <td>-418.776</td>    <td>0.9</td>  <td>-1470.1207</td>  <td>632.5688</td>   <td>False</td>
</tr>
<tr>
    <td>20</td>      <td>9</td>    <td>288.1625</td>    <td>0.9</td>   <td>-1154.426</td>  <td>1730.751</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>22</td>    <td>269.5231</td>    <td>0.9</td>   <td>-607.7189</td>  <td>1146.7651</td>  <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>23</td>     <td>-5.0669</td>    <td>0.9</td>   <td>-779.4512</td>  <td>769.3173</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>24</td>    <td>-166.9218</td>   <td>0.9</td>   <td>-771.1331</td>  <td>437.2894</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>25</td>     <td>-21.988</td>    <td>0.9</td>   <td>-824.3063</td>  <td>780.3302</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>26</td>    <td>425.8887</td>    <td>0.9</td>   <td>-245.6943</td>  <td>1097.4717</td>  <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>27</td>    <td>1445.312</td>   <td>0.001</td>  <td>404.0863</td>   <td>2486.5376</td>  <td>True</td> 
</tr>
<tr>
    <td>21</td>     <td>28</td>    <td>492.7231</td>  <td>0.7196</td>  <td>-178.8599</td>  <td>1164.3061</td>  <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>29</td>    <td>2263.6715</td>  <td>0.001</td>  <td>1586.1646</td>  <td>2941.1783</td>  <td>True</td> 
</tr>
<tr>
    <td>21</td>      <td>3</td>     <td>9.5897</td>     <td>0.9</td>   <td>-919.8901</td>  <td>939.0696</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>30</td>    <td>214.6587</td>    <td>0.9</td>   <td>-456.9243</td>  <td>886.2417</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>31</td>     <td>70.0309</td>    <td>0.9</td>   <td>-528.9068</td>  <td>668.9686</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>32</td>    <td>364.3364</td>    <td>0.9</td>   <td>-491.1178</td>  <td>1219.7906</td>  <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>33</td>     <td>-193.53</td>    <td>0.9</td>   <td>-865.113</td>   <td>478.0529</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>34</td>     <td>53.9231</td>    <td>0.9</td>   <td>-748.3952</td>  <td>856.2413</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>35</td>    <td>127.1174</td>    <td>0.9</td>   <td>-528.4651</td>  <td>782.6998</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>36</td>    <td>222.0392</td>    <td>0.9</td>   <td>-455.4676</td>   <td>899.546</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>37</td>    <td>260.7897</td>    <td>0.9</td>   <td>-973.952</td>   <td>1495.5315</td>  <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>38</td>    <td>6002.2647</td>  <td>0.001</td>  <td>5271.7817</td>  <td>6732.7478</td>  <td>True</td> 
</tr>
<tr>
    <td>21</td>     <td>39</td>    <td>125.7093</td>    <td>0.9</td>   <td>-564.691</td>   <td>816.1096</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>      <td>4</td>    <td>224.1631</td>    <td>0.9</td>   <td>-550.2212</td>  <td>998.5473</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>40</td>    <td>187.2706</td>    <td>0.9</td>   <td>-446.3497</td>  <td>820.8908</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>41</td>    <td>-87.7858</td>    <td>0.9</td>   <td>-703.7832</td>  <td>528.2116</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>42</td>     <td>26.4541</td>    <td>0.9</td>   <td>-663.9462</td>  <td>716.8544</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>43</td>    <td>579.5601</td>  <td>0.4449</td>  <td>-125.353</td>   <td>1284.4732</td>  <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>44</td>    <td>143.1057</td>    <td>0.9</td>   <td>-597.1426</td>   <td>883.354</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>45</td>     <td>91.5302</td>    <td>0.9</td>   <td>-785.7118</td>  <td>968.7722</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>46</td>    <td>-19.5214</td>    <td>0.9</td>   <td>-724.4345</td>  <td>685.3917</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>47</td>    <td>-39.5245</td>    <td>0.9</td>   <td>-801.6237</td>  <td>722.5746</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>48</td>     <td>10.0481</td>    <td>0.9</td>  <td>-1224.6937</td>  <td>1244.7898</td>  <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>49</td>     <td>205.304</td>    <td>0.9</td>   <td>-556.7951</td>  <td>967.4032</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>      <td>5</td>    <td>333.0381</td>    <td>0.9</td>   <td>-664.9918</td>  <td>1331.0679</td>  <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>50</td>    <td>103.9231</td>    <td>0.9</td>   <td>-894.1068</td>  <td>1101.9529</td>  <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>51</td>    <td>762.9915</td>  <td>0.0016</td>  <td>121.1925</td>   <td>1404.7905</td>  <td>True</td> 
</tr>
<tr>
    <td>21</td>     <td>52</td>    <td>-143.7269</td>   <td>0.9</td>   <td>-841.1622</td>  <td>553.7083</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>53</td>     <td>358.93</td>     <td>0.9</td>   <td>-331.4703</td>  <td>1049.3303</td>  <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>54</td>    <td>-104.8269</td>   <td>0.9</td>   <td>-755.593</td>   <td>545.9391</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>55</td>    <td>344.1958</td>    <td>0.9</td>   <td>-321.7744</td>  <td>1010.166</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>56</td>    <td>655.3471</td>  <td>0.0112</td>   <td>53.8196</td>   <td>1256.8746</td>  <td>True</td> 
</tr>
<tr>
    <td>21</td>     <td>57</td>     <td>92.3926</td>    <td>0.9</td>   <td>-647.8557</td>   <td>832.641</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>58</td>     <td>123.187</td>    <td>0.9</td>   <td>-679.1313</td>  <td>925.5052</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>59</td>    <td>998.0385</td>   <td>0.001</td>  <td>401.6015</td>   <td>1594.4754</td>  <td>True</td> 
</tr>
<tr>
    <td>21</td>      <td>6</td>    <td>365.0064</td>    <td>0.9</td>   <td>-564.4734</td>  <td>1294.4862</td>  <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>60</td>    <td>690.6431</td>  <td>0.0037</td>   <td>89.1156</td>   <td>1292.1706</td>  <td>True</td> 
</tr>
<tr>
    <td>21</td>     <td>61</td>    <td>318.9579</td>    <td>0.9</td>   <td>-421.2905</td>  <td>1059.2062</td>  <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>62</td>    <td>729.1763</td>  <td>0.0014</td>  <td>119.2943</td>   <td>1339.0582</td>  <td>True</td> 
</tr>
<tr>
    <td>21</td>     <td>63</td>    <td>793.8819</td>  <td>0.0793</td>  <td>-24.4228</td>   <td>1612.1866</td>  <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>64</td>    <td>397.2851</td>    <td>0.9</td>   <td>-293.1151</td>  <td>1087.6854</td>  <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>65</td>     <td>169.794</td>    <td>0.9</td>   <td>-507.7128</td>  <td>847.3009</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>66</td>    <td>192.7981</td>    <td>0.9</td>   <td>-900.0239</td>  <td>1285.6201</td>  <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>67</td>     <td>9.1231</td>     <td>0.9</td>   <td>-988.9068</td>  <td>1007.1529</td>  <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>68</td>     <td>6.3322</td>     <td>0.9</td>   <td>-659.638</td>   <td>672.3023</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>69</td>    <td>537.0263</td>  <td>0.5389</td>  <td>-140.4805</td>  <td>1214.5331</td>  <td>False</td>
</tr>
<tr>
    <td>21</td>      <td>7</td>    <td>527.5438</td>  <td>0.6263</td>  <td>-162.8565</td>  <td>1217.944</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>70</td>     <td>47.0769</td>    <td>0.9</td>   <td>-590.541</td>   <td>684.6948</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>71</td>    <td>249.9826</td>    <td>0.9</td>   <td>-376.1457</td>  <td>876.1109</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>72</td>    <td>392.1339</td>    <td>0.9</td>   <td>-254.043</td>   <td>1038.3108</td>  <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>73</td>     <td>52.9231</td>    <td>0.9</td>   <td>-824.3189</td>  <td>930.1651</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>74</td>    <td>-49.6923</td>    <td>0.9</td>   <td>-951.4202</td>  <td>852.0356</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>75</td>    <td>-75.5091</td>    <td>0.9</td>   <td>-691.5066</td>  <td>540.4883</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>76</td>    <td>152.2389</td>    <td>0.9</td>   <td>-489.5602</td>  <td>794.0379</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>     <td>77</td>     <td>-9.9148</td>    <td>0.9</td>   <td>-656.0917</td>  <td>636.2621</td>   <td>False</td>
</tr>
<tr>
    <td>21</td>      <td>8</td>    <td>811.3846</td>  <td>0.1975</td>  <td>-90.3433</td>   <td>1713.1125</td>  <td>False</td>
</tr>
<tr>
    <td>21</td>      <td>9</td>    <td>1518.3231</td> <td>0.0048</td>  <td>180.8445</td>   <td>2855.8017</td>  <td>True</td> 
</tr>
<tr>
    <td>22</td>     <td>23</td>     <td>-274.59</td>    <td>0.9</td>  <td>-1255.7464</td>  <td>706.5664</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>24</td>    <td>-436.4449</td>   <td>0.9</td>   <td>-1289.714</td>  <td>416.8242</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>25</td>    <td>-291.5111</td>   <td>0.9</td>  <td>-1294.8613</td>   <td>711.839</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>26</td>    <td>156.3656</td>    <td>0.9</td>   <td>-745.8653</td>  <td>1058.5966</td>  <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>27</td>    <td>1175.7889</td> <td>0.0713</td>  <td>-27.1857</td>   <td>2378.7635</td>  <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>28</td>      <td>223.2</td>     <td>0.9</td>   <td>-679.0309</td>  <td>1125.4309</td>  <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>29</td>    <td>1994.1484</td>  <td>0.001</td>  <td>1087.4994</td>  <td>2900.7974</td>  <td>True</td> 
</tr>
<tr>
    <td>22</td>      <td>3</td>    <td>-259.9333</td>   <td>0.9</td>  <td>-1367.6019</td>  <td>847.7352</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>30</td>    <td>-54.8644</td>    <td>0.9</td>   <td>-957.0953</td>  <td>847.3666</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>31</td>    <td>-199.4922</td>   <td>0.9</td>  <td>-1049.0352</td>  <td>650.0509</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>32</td>     <td>94.8133</td>    <td>0.9</td>   <td>-951.513</td>   <td>1141.1397</td>  <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>33</td>    <td>-463.0531</td>   <td>0.9</td>  <td>-1365.2841</td>  <td>439.1778</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>34</td>     <td>-215.6</td>     <td>0.9</td>  <td>-1218.9502</td>  <td>787.7502</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>35</td>    <td>-142.4057</td>   <td>0.9</td>  <td>-1032.7907</td>  <td>747.9792</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>36</td>    <td>-47.4839</td>    <td>0.9</td>   <td>-954.1329</td>  <td>859.1651</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>37</td>     <td>-8.7333</td>    <td>0.9</td>  <td>-1382.6271</td>  <td>1365.1605</td>  <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>38</td>    <td>5732.7417</td>  <td>0.001</td>  <td>4785.8507</td>  <td>6679.6326</td>  <td>True</td> 
</tr>
<tr>
    <td>22</td>     <td>39</td>    <td>-143.8138</td>   <td>0.9</td>  <td>-1060.1377</td>  <td>772.5101</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>      <td>4</td>     <td>-45.36</td>     <td>0.9</td>  <td>-1026.5164</td>  <td>935.7964</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>40</td>    <td>-82.2525</td>    <td>0.9</td>   <td>-956.5931</td>  <td>792.0881</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>41</td>    <td>-357.3089</td>   <td>0.9</td>  <td>-1218.9641</td>  <td>504.3464</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>42</td>    <td>-243.069</td>    <td>0.9</td>  <td>-1159.3929</td>  <td>673.2549</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>43</td>     <td>310.037</td>    <td>0.9</td>   <td>-617.2706</td>  <td>1237.3447</td>  <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>44</td>    <td>-126.4174</td>   <td>0.9</td>   <td>-1080.862</td>  <td>828.0272</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>45</td>    <td>-177.9929</td>   <td>0.9</td>  <td>-1242.2064</td>  <td>886.2207</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>46</td>    <td>-289.0444</td>   <td>0.9</td>  <td>-1216.3521</td>  <td>638.2632</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>47</td>    <td>-309.0476</td>   <td>0.9</td>  <td>-1280.5372</td>   <td>662.442</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>48</td>    <td>-259.475</td>    <td>0.9</td>  <td>-1633.3688</td>  <td>1114.4188</td>  <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>49</td>     <td>-64.219</td>    <td>0.9</td>  <td>-1035.7087</td>  <td>907.2706</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>      <td>5</td>     <td>63.515</td>     <td>0.9</td>  <td>-1102.2725</td>  <td>1229.3025</td>  <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>50</td>     <td>-165.6</td>     <td>0.9</td>  <td>-1331.3875</td>  <td>1000.1875</td>  <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>51</td>    <td>493.4684</td>    <td>0.9</td>   <td>-386.8173</td>  <td>1373.7541</td>  <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>52</td>     <td>-413.25</td>    <td>0.9</td>   <td>-1334.886</td>   <td>508.386</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>53</td>     <td>89.4069</td>    <td>0.9</td>   <td>-826.917</td>   <td>1005.7308</td>  <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>54</td>     <td>-374.35</td>    <td>0.9</td>  <td>-1261.1946</td>  <td>512.4946</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>55</td>     <td>74.6727</td>    <td>0.9</td>   <td>-823.3881</td>  <td>972.7335</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>56</td>     <td>385.824</td>    <td>0.9</td>   <td>-465.5468</td>  <td>1237.1948</td>  <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>57</td>    <td>-177.1304</td>   <td>0.9</td>   <td>-1131.575</td>  <td>777.3142</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>58</td>    <td>-146.3361</td>   <td>0.9</td>  <td>-1149.6863</td>   <td>857.014</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>59</td>    <td>728.5154</td>  <td>0.3094</td>  <td>-119.2664</td>  <td>1576.2972</td>  <td>False</td>
</tr>
<tr>
    <td>22</td>      <td>6</td>     <td>95.4833</td>    <td>0.9</td>  <td>-1012.1852</td>  <td>1203.1519</td>  <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>60</td>     <td>421.12</td>     <td>0.9</td>   <td>-430.2508</td>  <td>1272.4908</td>  <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>61</td>     <td>49.4348</td>    <td>0.9</td>   <td>-905.0098</td>  <td>1003.8794</td>  <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>62</td>    <td>459.6532</td>    <td>0.9</td>   <td>-397.6408</td>  <td>1316.9472</td>  <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>63</td>    <td>524.3588</td>    <td>0.9</td>   <td>-491.8201</td>  <td>1540.5377</td>  <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>64</td>    <td>127.7621</td>    <td>0.9</td>   <td>-788.5618</td>  <td>1044.086</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>65</td>     <td>-99.729</td>    <td>0.9</td>  <td>-1006.3781</td>   <td>806.92</td>    <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>66</td>     <td>-76.725</td>    <td>0.9</td>   <td>-1324.626</td>  <td>1171.176</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>67</td>     <td>-260.4</td>     <td>0.9</td>  <td>-1426.1875</td>  <td>905.3875</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>68</td>    <td>-263.1909</td>   <td>0.9</td>  <td>-1161.2517</td>  <td>634.8699</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>69</td>    <td>267.5032</td>    <td>0.9</td>   <td>-639.1458</td>  <td>1174.1522</td>  <td>False</td>
</tr>
<tr>
    <td>22</td>      <td>7</td>    <td>258.0207</td>    <td>0.9</td>   <td>-658.3032</td>  <td>1174.3446</td>  <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>70</td>    <td>-222.4462</td>   <td>0.9</td>  <td>-1099.6882</td>  <td>654.7958</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>71</td>    <td>-19.5405</td>    <td>0.9</td>   <td>-888.4672</td>  <td>849.3862</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>72</td>    <td>122.6108</td>    <td>0.9</td>   <td>-760.8718</td>  <td>1006.0934</td>  <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>73</td>     <td>-216.6</td>     <td>0.9</td>  <td>-1280.8135</td>  <td>847.6135</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>74</td>    <td>-319.2154</td>   <td>0.9</td>  <td>-1403.7015</td>  <td>765.2707</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>75</td>    <td>-345.0322</td>   <td>0.9</td>  <td>-1206.6875</td>   <td>516.623</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>76</td>    <td>-117.2842</td>   <td>0.9</td>   <td>-997.5699</td>  <td>763.0015</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>     <td>77</td>    <td>-279.4378</td>   <td>0.9</td>  <td>-1162.9205</td>  <td>604.0448</td>   <td>False</td>
</tr>
<tr>
    <td>22</td>      <td>8</td>    <td>541.8615</td>    <td>0.9</td>   <td>-542.6246</td>  <td>1626.3476</td>  <td>False</td>
</tr>
<tr>
    <td>22</td>      <td>9</td>     <td>1248.8</td>   <td>0.3352</td>  <td>-218.1171</td>  <td>2715.7171</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>24</td>    <td>-161.8549</td>   <td>0.9</td>   <td>-908.9731</td>  <td>585.2633</td>   <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>25</td>    <td>-16.9211</td>    <td>0.9</td>   <td>-931.7047</td>  <td>897.8624</td>   <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>26</td>    <td>430.9556</td>    <td>0.9</td>   <td>-371.6265</td>  <td>1233.5378</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>27</td>    <td>1450.3789</td>  <td>0.001</td>  <td>320.2173</td>   <td>2580.5405</td>  <td>True</td> 
</tr>
<tr>
    <td>23</td>     <td>28</td>     <td>497.79</td>     <td>0.9</td>   <td>-304.7921</td>  <td>1300.3721</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>29</td>    <td>2268.7384</td>  <td>0.001</td>  <td>1461.1928</td>  <td>3076.284</td>   <td>True</td> 
</tr>
<tr>
    <td>23</td>      <td>3</td>     <td>14.6567</td>    <td>0.9</td>  <td>-1013.4713</td>  <td>1042.7846</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>30</td>    <td>219.7256</td>    <td>0.9</td>   <td>-582.8565</td>  <td>1022.3078</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>31</td>     <td>75.0978</td>    <td>0.9</td>   <td>-667.762</td>   <td>817.9577</td>   <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>32</td>    <td>369.4033</td>    <td>0.9</td>   <td>-592.3223</td>  <td>1331.129</td>   <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>33</td>    <td>-188.4631</td>   <td>0.9</td>   <td>-991.0453</td>   <td>614.119</td>   <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>34</td>      <td>58.99</td>     <td>0.9</td>   <td>-855.7936</td>  <td>973.7736</td>   <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>35</td>    <td>132.1843</td>    <td>0.9</td>   <td>-657.0576</td>  <td>921.4262</td>   <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>36</td>    <td>227.1061</td>    <td>0.9</td>   <td>-580.4395</td>  <td>1034.6517</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>37</td>    <td>265.8567</td>    <td>0.9</td>  <td>-1044.7545</td>  <td>1576.4678</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>38</td>    <td>6007.3317</td>  <td>0.001</td>  <td>5154.853</td>   <td>6859.8103</td>  <td>True</td> 
</tr>
<tr>
    <td>23</td>     <td>39</td>    <td>130.7762</td>    <td>0.9</td>   <td>-687.6167</td>  <td>949.1691</td>   <td>False</td>
</tr>
<tr>
    <td>23</td>      <td>4</td>     <td>229.23</td>     <td>0.9</td>   <td>-661.1549</td>  <td>1119.6149</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>40</td>    <td>192.3375</td>    <td>0.9</td>   <td>-578.7585</td>  <td>963.4335</td>   <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>41</td>    <td>-82.7189</td>    <td>0.9</td>   <td>-839.4006</td>  <td>673.9628</td>   <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>42</td>     <td>31.521</td>     <td>0.9</td>   <td>-786.8719</td>  <td>849.9139</td>   <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>43</td>     <td>584.627</td>  <td>0.8111</td>  <td>-246.0455</td>  <td>1415.2996</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>44</td>    <td>148.1726</td>    <td>0.9</td>   <td>-712.6886</td>  <td>1009.0338</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>45</td>     <td>96.5971</td>    <td>0.9</td>   <td>-884.5593</td>  <td>1077.7536</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>46</td>    <td>-14.4544</td>    <td>0.9</td>   <td>-845.127</td>   <td>816.2181</td>   <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>47</td>    <td>-34.4576</td>    <td>0.9</td>   <td>-914.1789</td>  <td>845.2636</td>   <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>48</td>     <td>15.115</td>     <td>0.9</td>  <td>-1295.4961</td>  <td>1325.7261</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>49</td>     <td>210.371</td>    <td>0.9</td>   <td>-669.3503</td>  <td>1090.0922</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>      <td>5</td>     <td>338.105</td>    <td>0.9</td>   <td>-752.3894</td>  <td>1428.5994</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>50</td>     <td>108.99</td>     <td>0.9</td>   <td>-981.5044</td>  <td>1199.4844</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>51</td>    <td>768.0584</td>  <td>0.0611</td>   <td>-9.7721</td>   <td>1545.889</td>   <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>52</td>     <td>-138.66</td>    <td>0.9</td>   <td>-962.9963</td>  <td>685.6763</td>   <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>53</td>    <td>363.9969</td>    <td>0.9</td>   <td>-454.396</td>   <td>1182.3898</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>54</td>     <td>-99.76</td>     <td>0.9</td>   <td>-885.0057</td>  <td>685.4857</td>   <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>55</td>    <td>349.2627</td>    <td>0.9</td>   <td>-448.6286</td>  <td>1147.1541</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>56</td>     <td>660.414</td>   <td>0.231</td>  <td>-84.5355</td>   <td>1405.3635</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>57</td>     <td>97.4596</td>    <td>0.9</td>   <td>-763.4016</td>  <td>958.3207</td>   <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>58</td>    <td>128.2539</td>    <td>0.9</td>   <td>-786.5297</td>  <td>1043.0374</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>59</td>    <td>1003.1054</td>  <td>0.001</td>  <td>262.2603</td>   <td>1743.9504</td>  <td>True</td> 
</tr>
<tr>
    <td>23</td>      <td>6</td>    <td>370.0733</td>    <td>0.9</td>   <td>-658.0546</td>  <td>1398.2013</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>60</td>     <td>695.71</td>   <td>0.1276</td>  <td>-49.2395</td>   <td>1440.6595</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>61</td>    <td>324.0248</td>    <td>0.9</td>   <td>-536.8364</td>  <td>1184.8859</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>62</td>    <td>734.2432</td>   <td>0.072</td>  <td>-17.4685</td>   <td>1485.9548</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>63</td>    <td>798.9488</td>  <td>0.3069</td>  <td>-129.8875</td>  <td>1727.7852</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>64</td>    <td>402.3521</td>    <td>0.9</td>   <td>-416.0408</td>  <td>1220.745</td>   <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>65</td>     <td>174.861</td>    <td>0.9</td>   <td>-632.6846</td>  <td>982.4066</td>   <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>66</td>     <td>197.865</td>    <td>0.9</td>   <td>-980.0036</td>  <td>1375.7336</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>67</td>      <td>14.19</td>     <td>0.9</td>  <td>-1076.3044</td>  <td>1104.6844</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>68</td>     <td>11.3991</td>    <td>0.9</td>   <td>-786.4923</td>  <td>809.2905</td>   <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>69</td>    <td>542.0932</td>    <td>0.9</td>   <td>-265.4524</td>  <td>1349.6388</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>      <td>7</td>    <td>532.6107</td>    <td>0.9</td>   <td>-285.7822</td>  <td>1351.0036</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>70</td>     <td>52.1438</td>    <td>0.9</td>   <td>-722.2404</td>  <td>826.5281</td>   <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>71</td>    <td>255.0495</td>    <td>0.9</td>   <td>-509.9022</td>  <td>1020.0012</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>72</td>    <td>397.2008</td>    <td>0.9</td>   <td>-384.2459</td>  <td>1178.6475</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>73</td>      <td>57.99</td>     <td>0.9</td>   <td>-923.1664</td>  <td>1039.1464</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>74</td>    <td>-44.6254</td>    <td>0.9</td>  <td>-1047.7343</td>  <td>958.4836</td>   <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>75</td>    <td>-70.4422</td>    <td>0.9</td>   <td>-827.1239</td>  <td>686.2395</td>   <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>76</td>    <td>157.3058</td>    <td>0.9</td>   <td>-620.5248</td>  <td>935.1364</td>   <td>False</td>
</tr>
<tr>
    <td>23</td>     <td>77</td>     <td>-4.8478</td>    <td>0.9</td>   <td>-786.2946</td>  <td>776.5989</td>   <td>False</td>
</tr>
<tr>
    <td>23</td>      <td>8</td>    <td>816.4515</td>  <td>0.4732</td>  <td>-186.6574</td>  <td>1819.5605</td>  <td>False</td>
</tr>
<tr>
    <td>23</td>      <td>9</td>     <td>1523.39</td>  <td>0.0128</td>  <td>115.5678</td>   <td>2931.2122</td>  <td>True</td> 
</tr>
<tr>
    <td>24</td>     <td>25</td>    <td>144.9338</td>    <td>0.9</td>   <td>-631.1005</td>  <td>920.9681</td>   <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>26</td>    <td>592.8105</td>  <td>0.1416</td>  <td>-47.1413</td>   <td>1232.7624</td>  <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>27</td>    <td>1612.2338</td>  <td>0.001</td>  <td>591.1238</td>   <td>2633.3437</td>  <td>True</td> 
</tr>
<tr>
    <td>24</td>     <td>28</td>    <td>659.6449</td>  <td>0.0308</td>   <td>19.6931</td>   <td>1299.5967</td>  <td>True</td> 
</tr>
<tr>
    <td>24</td>     <td>29</td>    <td>2430.5933</td>  <td>0.001</td>  <td>1784.4276</td>  <td>3076.759</td>   <td>True</td> 
</tr>
<tr>
    <td>24</td>      <td>3</td>    <td>176.5116</td>    <td>0.9</td>   <td>-730.3773</td>  <td>1083.4004</td>  <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>30</td>    <td>381.5805</td>    <td>0.9</td>   <td>-258.3713</td>  <td>1021.5324</td>  <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>31</td>    <td>236.9527</td>    <td>0.9</td>   <td>-326.2888</td>  <td>800.1943</td>   <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>32</td>    <td>531.2582</td>    <td>0.9</td>   <td>-299.5946</td>  <td>1362.1111</td>  <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>33</td>    <td>-26.6082</td>    <td>0.9</td>   <td>-666.5601</td>  <td>613.3436</td>   <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>34</td>    <td>220.8449</td>    <td>0.9</td>   <td>-555.1894</td>  <td>996.8792</td>   <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>35</td>    <td>294.0392</td>    <td>0.9</td>   <td>-329.1005</td>  <td>917.1788</td>   <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>36</td>     <td>388.961</td>    <td>0.9</td>   <td>-257.2047</td>  <td>1035.1267</td>  <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>37</td>    <td>427.7116</td>    <td>0.9</td>   <td>-790.1151</td>  <td>1645.5382</td>  <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>38</td>    <td>6169.1866</td>  <td>0.001</td>  <td>5467.6738</td>  <td>6870.6993</td>  <td>True</td> 
</tr>
<tr>
    <td>24</td>     <td>39</td>    <td>292.6311</td>    <td>0.9</td>   <td>-367.0409</td>  <td>952.3031</td>   <td>False</td>
</tr>
<tr>
    <td>24</td>      <td>4</td>    <td>391.0849</td>    <td>0.9</td>   <td>-356.0333</td>  <td>1138.2031</td>  <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>40</td>    <td>354.1924</td>    <td>0.9</td>   <td>-245.7987</td>  <td>954.1834</td>   <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>41</td>     <td>79.136</td>     <td>0.9</td>   <td>-502.2137</td>  <td>660.4857</td>   <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>42</td>    <td>193.3759</td>    <td>0.9</td>   <td>-466.2961</td>   <td>853.048</td>   <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>43</td>    <td>746.4819</td>  <td>0.0083</td>   <td>71.6359</td>   <td>1421.3279</td>  <td>True</td> 
</tr>
<tr>
    <td>24</td>     <td>44</td>    <td>310.0275</td>    <td>0.9</td>   <td>-401.6481</td>  <td>1021.7031</td>  <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>45</td>     <td>258.452</td>    <td>0.9</td>   <td>-594.8171</td>  <td>1111.7211</td>  <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>46</td>    <td>147.4005</td>    <td>0.9</td>   <td>-527.4455</td>  <td>822.2465</td>   <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>47</td>    <td>127.3973</td>    <td>0.9</td>   <td>-606.9798</td>  <td>861.7744</td>   <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>48</td>    <td>176.9699</td>    <td>0.9</td>  <td>-1040.8568</td>  <td>1394.7966</td>  <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>49</td>    <td>372.2259</td>    <td>0.9</td>   <td>-362.1513</td>  <td>1106.603</td>   <td>False</td>
</tr>
<tr>
    <td>24</td>      <td>5</td>    <td>499.9599</td>    <td>0.9</td>   <td>-477.0653</td>  <td>1476.9851</td>  <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>50</td>    <td>270.8449</td>    <td>0.9</td>   <td>-706.1803</td>  <td>1247.8701</td>  <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>51</td>    <td>929.9133</td>   <td>0.001</td>  <td>321.2914</td>   <td>1538.5352</td>  <td>True</td> 
</tr>
<tr>
    <td>24</td>     <td>52</td>     <td>23.1949</td>    <td>0.9</td>   <td>-643.8362</td>   <td>690.226</td>   <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>53</td>    <td>525.8518</td>  <td>0.5251</td>  <td>-133.8202</td>  <td>1185.5238</td>  <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>54</td>     <td>62.0949</td>    <td>0.9</td>   <td>-555.9755</td>  <td>680.1653</td>   <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>55</td>    <td>511.1176</td>  <td>0.4977</td>  <td>-122.9414</td>  <td>1145.1767</td>  <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>56</td>    <td>822.2689</td>   <td>0.001</td>  <td>256.2742</td>   <td>1388.2636</td>  <td>True</td> 
</tr>
<tr>
    <td>24</td>     <td>57</td>    <td>259.3145</td>    <td>0.9</td>   <td>-452.3612</td>  <td>970.9901</td>   <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>58</td>    <td>290.1088</td>    <td>0.9</td>   <td>-485.9255</td>  <td>1066.1431</td>  <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>59</td>    <td>1164.9603</td>  <td>0.001</td>  <td>604.3788</td>   <td>1725.5418</td>  <td>True</td> 
</tr>
<tr>
    <td>24</td>      <td>6</td>    <td>531.9282</td>    <td>0.9</td>   <td>-374.9606</td>  <td>1438.8171</td>  <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>60</td>    <td>857.5649</td>   <td>0.001</td>  <td>291.5702</td>   <td>1423.5596</td>  <td>True</td> 
</tr>
<tr>
    <td>24</td>     <td>61</td>    <td>485.8797</td>  <td>0.8757</td>  <td>-225.7959</td>  <td>1197.5553</td>  <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>62</td>    <td>896.0981</td>   <td>0.001</td>  <td>321.2323</td>   <td>1470.9639</td>  <td>True</td> 
</tr>
<tr>
    <td>24</td>     <td>63</td>    <td>960.8037</td>   <td>0.001</td>  <td>168.2526</td>   <td>1753.3548</td>  <td>True</td> 
</tr>
<tr>
    <td>24</td>     <td>64</td>     <td>564.207</td>  <td>0.3217</td>  <td>-95.4651</td>   <td>1223.879</td>   <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>65</td>    <td>336.7159</td>    <td>0.9</td>   <td>-309.4498</td>  <td>982.8816</td>   <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>66</td>    <td>359.7199</td>    <td>0.9</td>   <td>-713.9535</td>  <td>1433.3933</td>  <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>67</td>    <td>176.0449</td>    <td>0.9</td>   <td>-800.9803</td>  <td>1153.0701</td>  <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>68</td>     <td>173.254</td>    <td>0.9</td>   <td>-460.8051</td>  <td>807.3131</td>   <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>69</td>    <td>703.9481</td>  <td>0.0112</td>   <td>57.7824</td>   <td>1350.1138</td>  <td>True</td> 
</tr>
<tr>
    <td>24</td>      <td>7</td>    <td>694.4656</td>  <td>0.0213</td>   <td>34.7936</td>   <td>1354.1376</td>  <td>True</td> 
</tr>
<tr>
    <td>24</td>     <td>70</td>    <td>213.9987</td>    <td>0.9</td>   <td>-390.2125</td>   <td>818.21</td>    <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>71</td>    <td>416.9044</td>   <td>0.81</td>   <td>-175.1693</td>  <td>1008.9782</td>  <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>72</td>    <td>559.0557</td>  <td>0.1721</td>   <td>-54.181</td>   <td>1172.2924</td>  <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>73</td>    <td>219.8449</td>    <td>0.9</td>   <td>-633.4242</td>  <td>1073.114</td>   <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>74</td>    <td>117.2295</td>    <td>0.9</td>   <td>-761.194</td>    <td>995.653</td>   <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>75</td>     <td>91.4127</td>    <td>0.9</td>   <td>-489.937</td>   <td>672.7624</td>   <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>76</td>    <td>319.1607</td>    <td>0.9</td>   <td>-289.4612</td>  <td>927.7826</td>   <td>False</td>
</tr>
<tr>
    <td>24</td>     <td>77</td>    <td>157.0071</td>    <td>0.9</td>   <td>-456.2296</td>  <td>770.2437</td>   <td>False</td>
</tr>
<tr>
    <td>24</td>      <td>8</td>    <td>978.3064</td>  <td>0.0072</td>   <td>99.883</td>    <td>1856.7299</td>  <td>True</td> 
</tr>
<tr>
    <td>24</td>      <td>9</td>    <td>1685.2449</td>  <td>0.001</td>  <td>363.3661</td>   <td>3007.1237</td>  <td>True</td> 
</tr>
<tr>
    <td>25</td>     <td>26</td>    <td>447.8767</td>    <td>0.9</td>   <td>-381.6904</td>  <td>1277.4439</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>27</td>     <td>1467.3</td>    <td>0.001</td>   <td>317.818</td>   <td>2616.782</td>   <td>True</td> 
</tr>
<tr>
    <td>25</td>     <td>28</td>    <td>514.7111</td>    <td>0.9</td>   <td>-314.8561</td>  <td>1344.2783</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>29</td>    <td>2285.6595</td>  <td>0.001</td>  <td>1451.2894</td>  <td>3120.0296</td>  <td>True</td> 
</tr>
<tr>
    <td>25</td>      <td>3</td>     <td>31.5778</td>    <td>0.9</td>  <td>-1017.7509</td>  <td>1080.9065</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>30</td>    <td>236.6467</td>    <td>0.9</td>   <td>-592.9204</td>  <td>1066.2139</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>31</td>     <td>92.019</td>     <td>0.9</td>   <td>-679.9165</td>  <td>863.9544</td>   <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>32</td>    <td>386.3244</td>    <td>0.9</td>   <td>-598.0331</td>  <td>1370.682</td>   <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>33</td>    <td>-171.542</td>    <td>0.9</td>  <td>-1001.1092</td>  <td>658.0252</td>   <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>34</td>     <td>75.9111</td>    <td>0.9</td>   <td>-862.637</td>   <td>1014.4592</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>35</td>    <td>149.1054</td>    <td>0.9</td>   <td>-667.5625</td>  <td>965.7733</td>   <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>36</td>    <td>244.0272</td>    <td>0.9</td>   <td>-590.3429</td>  <td>1078.3974</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>37</td>    <td>282.7778</td>    <td>0.9</td>  <td>-1044.5297</td>  <td>1610.0853</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>38</td>    <td>6024.2528</td>  <td>0.001</td>  <td>5146.3214</td>  <td>6902.1842</td>  <td>True</td> 
</tr>
<tr>
    <td>25</td>     <td>39</td>    <td>147.6973</td>    <td>0.9</td>   <td>-697.1758</td>  <td>992.5704</td>   <td>False</td>
</tr>
<tr>
    <td>25</td>      <td>4</td>    <td>246.1511</td>    <td>0.9</td>   <td>-668.6324</td>  <td>1160.9347</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>40</td>    <td>209.2586</td>    <td>0.9</td>   <td>-589.8863</td>  <td>1008.4035</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>41</td>    <td>-65.7978</td>    <td>0.9</td>   <td>-851.0435</td>  <td>719.4479</td>   <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>42</td>     <td>48.4421</td>    <td>0.9</td>   <td>-796.431</td>   <td>893.3152</td>   <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>43</td>    <td>601.5481</td>  <td>0.8163</td>  <td>-255.2252</td>  <td>1458.3215</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>44</td>    <td>165.0937</td>    <td>0.9</td>   <td>-720.9794</td>  <td>1051.1668</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>45</td>    <td>113.5183</td>    <td>0.9</td>   <td>-889.8319</td>  <td>1116.8684</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>46</td>     <td>2.4667</td>     <td>0.9</td>   <td>-854.3066</td>   <td>859.24</td>    <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>47</td>    <td>-17.5365</td>    <td>0.9</td>   <td>-921.9441</td>  <td>886.8711</td>   <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>48</td>     <td>32.0361</td>    <td>0.9</td>  <td>-1295.2714</td>  <td>1359.3436</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>49</td>    <td>227.2921</td>    <td>0.9</td>   <td>-677.1155</td>  <td>1131.6997</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>      <td>5</td>    <td>355.0261</td>    <td>0.9</td>   <td>-755.479</td>   <td>1465.5312</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>50</td>    <td>125.9111</td>    <td>0.9</td>   <td>-984.594</td>   <td>1236.4162</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>51</td>    <td>784.9795</td>  <td>0.0746</td>  <td>-20.6656</td>   <td>1590.6246</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>52</td>    <td>-121.7389</td>   <td>0.9</td>   <td>-972.3704</td>  <td>728.8926</td>   <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>53</td>     <td>380.918</td>    <td>0.9</td>   <td>-463.9551</td>  <td>1225.7911</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>54</td>    <td>-82.8389</td>    <td>0.9</td>   <td>-895.6454</td>  <td>729.9676</td>   <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>55</td>    <td>366.1838</td>    <td>0.9</td>   <td>-458.846</td>   <td>1191.2137</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>56</td>    <td>677.3351</td>  <td>0.2617</td>  <td>-96.6115</td>   <td>1451.2817</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>57</td>    <td>114.3807</td>    <td>0.9</td>   <td>-771.6924</td>  <td>1000.4538</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>58</td>     <td>145.175</td>    <td>0.9</td>   <td>-793.3731</td>  <td>1083.7231</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>59</td>    <td>1020.0265</td>  <td>0.001</td>  <td>250.0297</td>   <td>1790.0233</td>  <td>True</td> 
</tr>
<tr>
    <td>25</td>      <td>6</td>    <td>386.9944</td>    <td>0.9</td>   <td>-662.3343</td>  <td>1436.3232</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>60</td>    <td>712.6311</td>  <td>0.1529</td>  <td>-61.3155</td>   <td>1486.5777</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>61</td>    <td>340.9459</td>    <td>0.9</td>   <td>-545.1272</td>  <td>1227.019</td>   <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>62</td>    <td>751.1643</td>  <td>0.0875</td>  <td>-29.2933</td>   <td>1531.6219</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>63</td>    <td>815.8699</td>  <td>0.3171</td>  <td>-136.3804</td>  <td>1768.1202</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>64</td>    <td>419.2732</td>    <td>0.9</td>   <td>-425.5999</td>  <td>1264.1463</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>65</td>    <td>191.7821</td>    <td>0.9</td>   <td>-642.588</td>   <td>1026.1522</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>66</td>    <td>214.7861</td>    <td>0.9</td>   <td>-981.6327</td>  <td>1411.2049</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>67</td>     <td>31.1111</td>    <td>0.9</td>   <td>-1079.394</td>  <td>1141.6162</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>68</td>     <td>28.3202</td>    <td>0.9</td>   <td>-796.7097</td>  <td>853.3501</td>   <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>69</td>    <td>559.0143</td>    <td>0.9</td>   <td>-275.3558</td>  <td>1393.3845</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>      <td>7</td>    <td>549.5318</td>    <td>0.9</td>   <td>-295.3413</td>  <td>1394.4049</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>70</td>     <td>69.065</td>     <td>0.9</td>   <td>-733.2533</td>  <td>871.3832</td>   <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>71</td>    <td>271.9706</td>    <td>0.9</td>   <td>-521.2473</td>  <td>1065.1886</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>72</td>    <td>414.1219</td>    <td>0.9</td>   <td>-395.015</td>   <td>1223.2589</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>73</td>     <td>74.9111</td>    <td>0.9</td>   <td>-928.439</td>   <td>1078.2613</td>  <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>74</td>    <td>-27.7043</td>    <td>0.9</td>  <td>-1052.5317</td>  <td>997.1231</td>   <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>75</td>    <td>-53.5211</td>    <td>0.9</td>   <td>-838.7668</td>  <td>731.7246</td>   <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>76</td>    <td>174.2269</td>    <td>0.9</td>   <td>-631.4182</td>   <td>979.872</td>   <td>False</td>
</tr>
<tr>
    <td>25</td>     <td>77</td>     <td>12.0733</td>    <td>0.9</td>   <td>-797.0637</td>  <td>821.2102</td>   <td>False</td>
</tr>
<tr>
    <td>25</td>      <td>8</td>    <td>833.3726</td>  <td>0.4757</td>  <td>-191.4547</td>   <td>1858.2</td>    <td>False</td>
</tr>
<tr>
    <td>25</td>      <td>9</td>    <td>1540.3111</td> <td>0.0128</td>  <td>116.9324</td>   <td>2963.6898</td>  <td>True</td> 
</tr>
<tr>
    <td>26</td>     <td>27</td>    <td>1019.4233</td> <td>0.0901</td>  <td>-42.9411</td>   <td>2081.7876</td>  <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>28</td>     <td>66.8344</td>    <td>0.9</td>   <td>-637.0767</td>  <td>770.7455</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>29</td>    <td>1837.7828</td>  <td>0.001</td>  <td>1128.2177</td>  <td>2547.3479</td>  <td>True</td> 
</tr>
<tr>
    <td>26</td>      <td>3</td>    <td>-416.299</td>    <td>0.9</td>  <td>-1369.3991</td>  <td>536.8012</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>30</td>     <td>-211.23</td>    <td>0.9</td>   <td>-915.1411</td>  <td>492.6811</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>31</td>    <td>-355.8578</td>   <td>0.9</td>   <td>-990.833</td>   <td>279.1174</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>32</td>    <td>-61.5523</td>    <td>0.9</td>   <td>-942.6136</td>   <td>819.509</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>33</td>    <td>-619.4187</td> <td>0.2479</td> <td>-1323.3298</td>   <td>84.4923</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>34</td>    <td>-371.9656</td>   <td>0.9</td>  <td>-1201.5328</td>  <td>457.6016</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>35</td>    <td>-298.7713</td>   <td>0.9</td>   <td>-987.4335</td>  <td>389.8908</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>36</td>    <td>-203.8495</td>   <td>0.9</td>   <td>-913.4146</td>  <td>505.7156</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>37</td>    <td>-165.099</td>    <td>0.9</td>  <td>-1417.7179</td>   <td>1087.52</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>38</td>    <td>5576.376</td>   <td>0.001</td>  <td>4816.0652</td>  <td>6336.6869</td>  <td>True</td> 
</tr>
<tr>
    <td>26</td>     <td>39</td>    <td>-300.1794</td>   <td>0.9</td>  <td>-1022.0656</td>  <td>421.7068</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>      <td>4</td>    <td>-201.7256</td>   <td>0.9</td>  <td>-1004.3078</td>  <td>600.8565</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>40</td>    <td>-238.6181</td>   <td>0.9</td>   <td>-906.4068</td>  <td>429.1706</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>41</td>    <td>-513.6745</td> <td>0.5502</td> <td>-1164.7659</td>  <td>137.4168</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>42</td>    <td>-399.4346</td>   <td>0.9</td>  <td>-1121.3208</td>  <td>322.4516</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>43</td>    <td>153.6714</td>    <td>0.9</td>   <td>-582.1068</td>  <td>889.4496</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>44</td>    <td>-282.783</td>    <td>0.9</td>  <td>-1052.4808</td>  <td>486.9148</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>45</td>    <td>-334.3585</td>   <td>0.9</td>  <td>-1236.5894</td>  <td>567.8725</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>46</td>    <td>-445.4101</td>   <td>0.9</td>  <td>-1181.1883</td>  <td>290.3682</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>47</td>    <td>-465.4132</td>   <td>0.9</td>  <td>-1256.1485</td>   <td>325.322</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>48</td>    <td>-415.8406</td>   <td>0.9</td>  <td>-1668.4596</td>  <td>836.7784</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>49</td>    <td>-220.5847</td>   <td>0.9</td>  <td>-1011.3199</td>  <td>570.1506</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>      <td>5</td>    <td>-92.8506</td>    <td>0.9</td>  <td>-1112.9147</td>  <td>927.2135</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>50</td>    <td>-321.9656</td>   <td>0.9</td>  <td>-1342.0297</td>  <td>698.0985</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>51</td>    <td>337.1028</td>    <td>0.9</td>   <td>-338.4512</td>  <td>1012.6567</td>  <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>52</td>    <td>-569.6156</td> <td>0.5722</td> <td>-1298.2328</td>  <td>159.0016</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>53</td>    <td>-66.9587</td>    <td>0.9</td>   <td>-788.8449</td>  <td>654.9275</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>54</td>    <td>-530.7156</td> <td>0.5905</td> <td>-1214.7942</td>   <td>153.363</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>55</td>    <td>-81.6929</td>    <td>0.9</td>   <td>-780.251</td>   <td>616.8652</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>56</td>    <td>229.4584</td>    <td>0.9</td>   <td>-407.9602</td>   <td>866.877</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>57</td>    <td>-333.4961</td>   <td>0.9</td>  <td>-1103.1939</td>  <td>436.2017</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>58</td>    <td>-302.7017</td>   <td>0.9</td>  <td>-1132.2689</td>  <td>526.8654</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>59</td>    <td>572.1498</td>  <td>0.1866</td>  <td>-60.4671</td>   <td>1204.7667</td>  <td>False</td>
</tr>
<tr>
    <td>26</td>      <td>6</td>    <td>-60.8823</td>    <td>0.9</td>  <td>-1013.9824</td>  <td>892.2178</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>60</td>    <td>264.7544</td>    <td>0.9</td>   <td>-372.6642</td>   <td>902.173</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>61</td>    <td>-106.9308</td>   <td>0.9</td>   <td>-876.6286</td>   <td>662.767</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>62</td>    <td>303.2876</td>    <td>0.9</td>   <td>-342.021</td>   <td>948.5961</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>63</td>    <td>367.9932</td>    <td>0.9</td>   <td>-477.0451</td>  <td>1213.0315</td>  <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>64</td>    <td>-28.6036</td>    <td>0.9</td>   <td>-750.4897</td>  <td>693.2826</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>65</td>    <td>-256.0947</td>   <td>0.9</td>   <td>-965.6598</td>  <td>453.4704</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>66</td>    <td>-233.0906</td>   <td>0.9</td>  <td>-1346.0718</td>  <td>879.8905</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>67</td>    <td>-416.7656</td>   <td>0.9</td>  <td>-1436.8297</td>  <td>603.2985</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>68</td>    <td>-419.5565</td>   <td>0.9</td>  <td>-1118.1146</td>  <td>279.0015</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>69</td>    <td>111.1376</td>    <td>0.9</td>   <td>-598.4275</td>  <td>820.7027</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>      <td>7</td>    <td>101.6551</td>    <td>0.9</td>   <td>-620.2311</td>  <td>823.5413</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>70</td>    <td>-378.8118</td>   <td>0.9</td>  <td>-1050.3948</td>  <td>292.7712</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>71</td>    <td>-175.9061</td>   <td>0.9</td>   <td>-836.5905</td>  <td>484.7783</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>72</td>    <td>-33.7548</td>    <td>0.9</td>   <td>-713.4693</td>  <td>645.9596</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>73</td>    <td>-372.9656</td>   <td>0.9</td>  <td>-1275.1966</td>  <td>529.2653</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>74</td>    <td>-475.581</td>    <td>0.9</td>  <td>-1401.6373</td>  <td>450.4753</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>75</td>    <td>-501.3978</td>  <td>0.608</td> <td>-1152.4892</td>  <td>149.6935</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>76</td>    <td>-273.6498</td>   <td>0.9</td>   <td>-949.2038</td>  <td>401.9041</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>     <td>77</td>    <td>-435.8035</td>   <td>0.9</td>  <td>-1115.5179</td>   <td>243.911</td>   <td>False</td>
</tr>
<tr>
    <td>26</td>      <td>8</td>    <td>385.4959</td>    <td>0.9</td>   <td>-540.5604</td>  <td>1311.5522</td>  <td>False</td>
</tr>
<tr>
    <td>26</td>      <td>9</td>    <td>1092.4344</td> <td>0.4956</td>  <td>-261.5657</td>  <td>2446.4344</td>  <td>False</td>
</tr>
<tr>
    <td>27</td>     <td>28</td>    <td>-952.5889</td> <td>0.2051</td> <td>-2014.9532</td>  <td>109.7755</td>   <td>False</td>
</tr>
<tr>
    <td>27</td>     <td>29</td>    <td>818.3595</td>  <td>0.6156</td>  <td>-247.7595</td>  <td>1884.4785</td>  <td>False</td>
</tr>
<tr>
    <td>27</td>      <td>3</td>   <td>-1435.7222</td> <td>0.0032</td> <td>-2677.3047</td>  <td>-194.1397</td>  <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>30</td>   <td>-1230.6533</td>  <td>0.003</td> <td>-2293.0176</td>  <td>-168.2889</td>  <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>31</td>    <td>-1375.281</td>  <td>0.001</td> <td>-2393.2794</td>  <td>-357.2827</td>  <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>32</td>   <td>-1080.9756</td> <td>0.1744</td> <td>-2268.1555</td>  <td>106.2044</td>   <td>False</td>
</tr>
<tr>
    <td>27</td>     <td>33</td>    <td>-1638.842</td>  <td>0.001</td> <td>-2701.2064</td>  <td>-576.4777</td>  <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>34</td>   <td>-1391.3889</td> <td>0.0011</td> <td>-2540.8709</td>  <td>-241.9069</td>  <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>35</td>   <td>-1318.1946</td>  <td>0.001</td> <td>-2370.5171</td>  <td>-265.8721</td>  <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>36</td>   <td>-1223.2728</td> <td>0.0038</td> <td>-2289.3918</td>  <td>-157.1537</td>  <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>37</td>   <td>-1184.5222</td> <td>0.5219</td> <td>-2668.4971</td>  <td>299.4527</td>   <td>False</td>
</tr>
<tr>
    <td>27</td>     <td>38</td>    <td>4556.9528</td>  <td>0.001</td>  <td>3456.4075</td>  <td>5657.498</td>   <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>39</td>   <td>-1319.6027</td>  <td>0.001</td> <td>-2393.9615</td>  <td>-245.2439</td>  <td>True</td> 
</tr>
<tr>
    <td>27</td>      <td>4</td>   <td>-1221.1489</td> <td>0.0131</td> <td>-2351.3105</td>  <td>-90.9873</td>   <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>40</td>   <td>-1258.0414</td>  <td>0.001</td> <td>-2296.8238</td>  <td>-219.259</td>   <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>41</td>   <td>-1533.0978</td>  <td>0.001</td> <td>-2561.2257</td>  <td>-504.9698</td>  <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>42</td>   <td>-1418.8579</td>  <td>0.001</td> <td>-2493.2167</td>  <td>-344.499</td>   <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>43</td>    <td>-865.7519</td> <td>0.5199</td> <td>-1949.4939</td>  <td>217.9902</td>   <td>False</td>
</tr>
<tr>
    <td>27</td>     <td>44</td>   <td>-1302.2063</td> <td>0.0021</td> <td>-2409.2573</td>  <td>-195.1553</td>  <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>45</td>   <td>-1353.7817</td> <td>0.0058</td> <td>-2556.7563</td>  <td>-150.8072</td>  <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>46</td>   <td>-1464.8333</td>  <td>0.001</td> <td>-2548.5754</td>  <td>-381.0913</td>  <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>47</td>   <td>-1484.8365</td>  <td>0.001</td> <td>-2606.6161</td>  <td>-363.0569</td>  <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>48</td>   <td>-1435.2639</td> <td>0.0827</td> <td>-2919.2388</td>   <td>48.711</td>    <td>False</td>
</tr>
<tr>
    <td>27</td>     <td>49</td>   <td>-1240.0079</td> <td>0.0084</td> <td>-2361.7875</td>  <td>-118.2284</td>  <td>True</td> 
</tr>
<tr>
    <td>27</td>      <td>5</td>   <td>-1112.2739</td> <td>0.3081</td> <td>-2405.9732</td>  <td>181.4254</td>   <td>False</td>
</tr>
<tr>
    <td>27</td>     <td>50</td>   <td>-1341.3889</td> <td>0.0278</td> <td>-2635.0882</td>  <td>-47.6896</td>   <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>51</td>    <td>-682.3205</td>   <td>0.9</td>  <td>-1726.1118</td>  <td>361.4708</td>   <td>False</td>
</tr>
<tr>
    <td>27</td>     <td>52</td>   <td>-1589.0389</td>  <td>0.001</td> <td>-2667.9319</td>  <td>-510.1458</td>  <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>53</td>    <td>-1086.382</td> <td>0.0422</td> <td>-2160.7408</td>  <td>-12.0232</td>   <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>54</td>   <td>-1550.1389</td>  <td>0.001</td> <td>-2599.4676</td>  <td>-500.8102</td>  <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>55</td>   <td>-1101.1162</td> <td>0.0264</td> <td>-2159.9413</td>  <td>-42.2911</td>   <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>56</td>    <td>-789.9649</td> <td>0.5935</td> <td>-1809.4891</td>  <td>229.5593</td>   <td>False</td>
</tr>
<tr>
    <td>27</td>     <td>57</td>   <td>-1352.9193</td>  <td>0.001</td> <td>-2459.9703</td>  <td>-245.8683</td>  <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>58</td>    <td>-1322.125</td> <td>0.0036</td>  <td>-2471.607</td>  <td>-172.643</td>   <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>59</td>    <td>-447.2735</td>   <td>0.9</td>  <td>-1463.8026</td>  <td>569.2555</td>   <td>False</td>
</tr>
<tr>
    <td>27</td>      <td>6</td>   <td>-1080.3056</td> <td>0.2767</td>  <td>-2321.888</td>  <td>161.2769</td>   <td>False</td>
</tr>
<tr>
    <td>27</td>     <td>60</td>    <td>-754.6689</td> <td>0.6995</td> <td>-1774.1931</td>  <td>264.8553</td>   <td>False</td>
</tr>
<tr>
    <td>27</td>     <td>61</td>   <td>-1126.3541</td> <td>0.0382</td> <td>-2233.4051</td>  <td>-19.3031</td>   <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>62</td>    <td>-716.1357</td> <td>0.8257</td> <td>-1740.6113</td>  <td>308.3399</td>   <td>False</td>
</tr>
<tr>
    <td>27</td>     <td>63</td>    <td>-651.4301</td>   <td>0.9</td>  <td>-1812.1268</td>  <td>509.2667</td>   <td>False</td>
</tr>
<tr>
    <td>27</td>     <td>64</td>   <td>-1048.0268</td> <td>0.0733</td> <td>-2122.3856</td>   <td>26.332</td>    <td>False</td>
</tr>
<tr>
    <td>27</td>     <td>65</td>   <td>-1275.5179</td> <td>0.0014</td>  <td>-2341.637</td>  <td>-209.3989</td>  <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>66</td>   <td>-1252.5139</td> <td>0.1639</td> <td>-2620.6711</td>  <td>115.6434</td>   <td>False</td>
</tr>
<tr>
    <td>27</td>     <td>67</td>   <td>-1436.1889</td> <td>0.0077</td> <td>-2729.8882</td>  <td>-142.4896</td>  <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>68</td>   <td>-1438.9798</td>  <td>0.001</td> <td>-2497.8049</td>  <td>-380.1547</td>  <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>69</td>    <td>-908.2857</td> <td>0.3329</td> <td>-1974.4047</td>  <td>157.8334</td>   <td>False</td>
</tr>
<tr>
    <td>27</td>      <td>7</td>    <td>-917.7682</td> <td>0.3248</td>  <td>-1992.127</td>  <td>156.5906</td>   <td>False</td>
</tr>
<tr>
    <td>27</td>     <td>70</td>    <td>-1398.235</td>  <td>0.001</td> <td>-2439.4607</td>  <td>-357.0094</td>  <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>71</td>   <td>-1195.3294</td> <td>0.0032</td>  <td>-2229.559</td>  <td>-161.0997</td>  <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>72</td>   <td>-1053.1781</td> <td>0.0454</td> <td>-2099.6669</td>   <td>-6.6892</td>   <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>73</td>   <td>-1392.3889</td> <td>0.0031</td> <td>-2595.3635</td>  <td>-189.4143</td>  <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>74</td>   <td>-1495.0043</td>  <td>0.001</td> <td>-2715.9496</td>  <td>-274.059</td>   <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>75</td>   <td>-1520.8211</td>  <td>0.001</td> <td>-2548.9491</td>  <td>-492.6931</td>  <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>76</td>   <td>-1293.0731</td>  <td>0.001</td> <td>-2336.8644</td>  <td>-249.2818</td>  <td>True</td> 
</tr>
<tr>
    <td>27</td>     <td>77</td>   <td>-1455.2267</td>  <td>0.001</td> <td>-2501.7156</td>  <td>-408.7379</td>  <td>True</td> 
</tr>
<tr>
    <td>27</td>      <td>8</td>    <td>-633.9274</td>   <td>0.9</td>  <td>-1854.8727</td>   <td>587.018</td>   <td>False</td>
</tr>
<tr>
    <td>27</td>      <td>9</td>     <td>73.0111</td>    <td>0.9</td>  <td>-1497.4803</td>  <td>1643.5025</td>  <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>29</td>    <td>1770.9484</td>  <td>0.001</td>  <td>1061.3833</td>  <td>2480.5135</td>  <td>True</td> 
</tr>
<tr>
    <td>28</td>      <td>3</td>    <td>-483.1333</td>   <td>0.9</td>  <td>-1436.2335</td>  <td>469.9668</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>30</td>    <td>-278.0644</td>   <td>0.9</td>   <td>-981.9755</td>  <td>425.8467</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>31</td>    <td>-422.6922</td>   <td>0.9</td>  <td>-1057.6674</td>  <td>212.2831</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>32</td>    <td>-128.3867</td>   <td>0.9</td>  <td>-1009.4479</td>  <td>752.6746</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>33</td>    <td>-686.2531</td>  <td>0.074</td> <td>-1390.1642</td>   <td>17.658</td>    <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>34</td>     <td>-438.8</td>     <td>0.9</td>  <td>-1268.3672</td>  <td>390.7672</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>35</td>    <td>-365.6057</td>   <td>0.9</td>  <td>-1054.2678</td>  <td>323.0564</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>36</td>    <td>-270.6839</td>   <td>0.9</td>   <td>-980.249</td>   <td>438.8812</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>37</td>    <td>-231.9333</td>   <td>0.9</td>  <td>-1484.5523</td>  <td>1020.6856</td>  <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>38</td>    <td>5509.5417</td>  <td>0.001</td>  <td>4749.2308</td>  <td>6269.8525</td>  <td>True</td> 
</tr>
<tr>
    <td>28</td>     <td>39</td>    <td>-367.0138</td>   <td>0.9</td>    <td>-1088.9</td>   <td>354.8724</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>      <td>4</td>     <td>-268.56</td>    <td>0.9</td>  <td>-1071.1421</td>  <td>534.0221</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>40</td>    <td>-305.4525</td>   <td>0.9</td>   <td>-973.2412</td>  <td>362.3362</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>41</td>    <td>-580.5089</td> <td>0.2179</td> <td>-1231.6002</td>   <td>70.5825</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>42</td>    <td>-466.269</td>    <td>0.9</td>  <td>-1188.1552</td>  <td>255.6172</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>43</td>     <td>86.837</td>     <td>0.9</td>   <td>-648.9412</td>  <td>822.6153</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>44</td>    <td>-349.6174</td>   <td>0.9</td>  <td>-1119.3152</td>  <td>420.0804</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>45</td>    <td>-401.1929</td>   <td>0.9</td>  <td>-1303.4238</td>  <td>501.0381</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>46</td>    <td>-512.2444</td> <td>0.8344</td> <td>-1248.0227</td>  <td>223.5338</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>47</td>    <td>-532.2476</td>   <td>0.9</td>  <td>-1322.9829</td>  <td>258.4876</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>48</td>    <td>-482.675</td>    <td>0.9</td>   <td>-1735.294</td>   <td>769.944</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>49</td>    <td>-287.419</td>    <td>0.9</td>  <td>-1078.1543</td>  <td>503.3162</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>      <td>5</td>    <td>-159.685</td>    <td>0.9</td>  <td>-1179.7491</td>  <td>860.3791</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>50</td>     <td>-388.8</td>     <td>0.9</td>  <td>-1408.8641</td>  <td>631.2641</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>51</td>    <td>270.2684</td>    <td>0.9</td>   <td>-405.2855</td>  <td>945.8224</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>52</td>     <td>-636.45</td>  <td>0.2666</td> <td>-1365.0672</td>   <td>92.1672</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>53</td>    <td>-133.7931</td>   <td>0.9</td>   <td>-855.6793</td>  <td>588.0931</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>54</td>     <td>-597.55</td>  <td>0.2665</td> <td>-1281.6286</td>   <td>86.5286</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>55</td>    <td>-148.5273</td>   <td>0.9</td>   <td>-847.0854</td>  <td>550.0308</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>56</td>     <td>162.624</td>    <td>0.9</td>   <td>-474.7946</td>  <td>800.0426</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>57</td>    <td>-400.3304</td>   <td>0.9</td>  <td>-1170.0282</td>  <td>369.3674</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>58</td>    <td>-369.5361</td>   <td>0.9</td>  <td>-1199.1033</td>  <td>460.0311</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>59</td>    <td>505.3154</td>  <td>0.5201</td>  <td>-127.3015</td>  <td>1137.9323</td>  <td>False</td>
</tr>
<tr>
    <td>28</td>      <td>6</td>    <td>-127.7167</td>   <td>0.9</td>  <td>-1080.8168</td>  <td>825.3835</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>60</td>     <td>197.92</td>     <td>0.9</td>   <td>-439.4986</td>  <td>835.3386</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>61</td>    <td>-173.7652</td>   <td>0.9</td>   <td>-943.463</td>   <td>595.9326</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>62</td>    <td>236.4532</td>    <td>0.9</td>   <td>-408.8554</td>  <td>881.7618</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>63</td>    <td>301.1588</td>    <td>0.9</td>   <td>-543.8795</td>  <td>1146.1971</td>  <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>64</td>    <td>-95.4379</td>    <td>0.9</td>   <td>-817.3241</td>  <td>626.4483</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>65</td>    <td>-322.929</td>    <td>0.9</td>  <td>-1032.4941</td>  <td>386.6361</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>66</td>    <td>-299.925</td>    <td>0.9</td>  <td>-1412.9062</td>  <td>813.0562</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>67</td>     <td>-483.6</td>     <td>0.9</td>  <td>-1503.6641</td>  <td>536.4641</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>68</td>    <td>-486.3909</td> <td>0.8341</td>  <td>-1184.949</td>  <td>212.1672</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>69</td>     <td>44.3032</td>    <td>0.9</td>   <td>-665.2619</td>  <td>753.8683</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>      <td>7</td>     <td>34.8207</td>    <td>0.9</td>   <td>-687.0655</td>  <td>756.7069</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>70</td>    <td>-445.6462</td>   <td>0.9</td>  <td>-1117.2291</td>  <td>225.9368</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>71</td>    <td>-242.7405</td>   <td>0.9</td>   <td>-903.4248</td>  <td>417.9439</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>72</td>    <td>-100.5892</td>   <td>0.9</td>   <td>-780.3036</td>  <td>579.1253</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>73</td>     <td>-439.8</td>     <td>0.9</td>  <td>-1342.0309</td>  <td>462.4309</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>74</td>    <td>-542.4154</td>   <td>0.9</td>  <td>-1468.4717</td>  <td>383.6409</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>75</td>    <td>-568.2322</td> <td>0.2688</td> <td>-1219.3236</td>   <td>82.8591</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>76</td>    <td>-340.4842</td>   <td>0.9</td>  <td>-1016.0382</td>  <td>335.0697</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>     <td>77</td>    <td>-502.6378</td> <td>0.7018</td> <td>-1182.3523</td>  <td>177.0766</td>   <td>False</td>
</tr>
<tr>
    <td>28</td>      <td>8</td>    <td>318.6615</td>    <td>0.9</td>   <td>-607.3948</td>  <td>1244.7178</td>  <td>False</td>
</tr>
<tr>
    <td>28</td>      <td>9</td>     <td>1025.6</td>   <td>0.6467</td>   <td>-328.4</td>     <td>2379.6</td>    <td>False</td>
</tr>
<tr>
    <td>29</td>      <td>3</td>   <td>-2254.0817</td>  <td>0.001</td> <td>-3211.3652</td> <td>-1296.7982</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>30</td>   <td>-2049.0128</td>  <td>0.001</td> <td>-2758.5779</td> <td>-1339.4477</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>31</td>   <td>-2193.6405</td>  <td>0.001</td> <td>-2834.8779</td> <td>-1552.4032</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>32</td>   <td>-1899.3351</td>  <td>0.001</td>  <td>-2784.92</td>  <td>-1013.7501</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>33</td>   <td>-2457.2015</td>  <td>0.001</td> <td>-3166.7666</td> <td>-1747.6364</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>34</td>   <td>-2209.7484</td>  <td>0.001</td> <td>-3044.1185</td> <td>-1375.3783</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>35</td>   <td>-2136.5541</td>  <td>0.001</td> <td>-2830.9944</td> <td>-1442.1138</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>36</td>   <td>-2041.6323</td>  <td>0.001</td> <td>-2756.8066</td> <td>-1326.4579</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>37</td>   <td>-2002.8817</td>  <td>0.001</td> <td>-3258.6867</td>  <td>-747.0768</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>38</td>    <td>3738.5933</td>  <td>0.001</td>  <td>2973.0448</td>  <td>4504.1417</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>39</td>   <td>-2137.9622</td>  <td>0.001</td> <td>-2865.3627</td> <td>-1410.5617</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>      <td>4</td>   <td>-2039.5084</td>  <td>0.001</td>  <td>-2847.054</td> <td>-1231.9628</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>40</td>   <td>-2076.4009</td>  <td>0.001</td> <td>-2750.1468</td>  <td>-1402.655</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>41</td>   <td>-2351.4573</td>  <td>0.001</td> <td>-3008.6572</td> <td>-1694.2574</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>42</td>   <td>-2237.2174</td>  <td>0.001</td> <td>-2964.6178</td> <td>-1509.8169</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>43</td>   <td>-1684.1114</td>  <td>0.001</td> <td>-2425.3005</td>  <td>-942.9222</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>44</td>   <td>-2120.5658</td>  <td>0.001</td> <td>-2895.4377</td> <td>-1345.6939</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>45</td>   <td>-2172.1412</td>  <td>0.001</td> <td>-3078.7903</td> <td>-1265.4922</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>46</td>   <td>-2283.1928</td>  <td>0.001</td>  <td>-3024.382</td> <td>-1542.0037</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>47</td>    <td>-2303.196</td>  <td>0.001</td> <td>-3098.9686</td> <td>-1507.4234</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>48</td>   <td>-2253.6234</td>  <td>0.001</td> <td>-3509.4283</td>  <td>-997.8184</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>49</td>   <td>-2058.3674</td>  <td>0.001</td>  <td>-2854.14</td>  <td>-1262.5948</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>      <td>5</td>   <td>-1930.6334</td>  <td>0.001</td> <td>-2954.6073</td>  <td>-906.6595</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>50</td>   <td>-2159.7484</td>  <td>0.001</td> <td>-3183.7223</td> <td>-1135.7745</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>51</td>    <td>-1500.68</td>   <td>0.001</td> <td>-2182.1232</td>  <td>-819.2367</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>52</td>   <td>-2407.3984</td>  <td>0.001</td> <td>-3141.4793</td> <td>-1673.3174</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>53</td>   <td>-1904.7415</td>  <td>0.001</td>  <td>-2632.142</td>  <td>-1177.341</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>54</td>   <td>-2368.4984</td>  <td>0.001</td> <td>-3058.3936</td> <td>-1678.6032</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>55</td>   <td>-1919.4757</td>  <td>0.001</td> <td>-2623.7307</td> <td>-1215.2206</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>56</td>   <td>-1608.3244</td>  <td>0.001</td> <td>-2251.9813</td>  <td>-964.6674</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>57</td>   <td>-2171.2788</td>  <td>0.001</td> <td>-2946.1507</td> <td>-1396.4069</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>58</td>   <td>-2140.4845</td>  <td>0.001</td> <td>-2974.8546</td> <td>-1306.1144</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>59</td>    <td>-1265.633</td>  <td>0.001</td> <td>-1904.5351</td>  <td>-626.7309</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>      <td>6</td>   <td>-1898.6651</td>  <td>0.001</td> <td>-2855.9485</td>  <td>-941.3816</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>60</td>   <td>-1573.0284</td>  <td>0.001</td> <td>-2216.6853</td>  <td>-929.3714</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>61</td>   <td>-1944.7136</td>  <td>0.001</td> <td>-2719.5855</td> <td>-1169.8417</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>62</td>   <td>-1534.4952</td>  <td>0.001</td> <td>-2185.9666</td>  <td>-883.0238</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>63</td>   <td>-1469.7896</td>  <td>0.001</td> <td>-2319.5434</td>  <td>-620.0358</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>64</td>   <td>-1866.3863</td>  <td>0.001</td> <td>-2593.7868</td> <td>-1138.9858</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>65</td>   <td>-2093.8774</td>  <td>0.001</td> <td>-2809.0518</td>  <td>-1378.703</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>66</td>   <td>-2070.8734</td>  <td>0.001</td>  <td>-3187.439</td>  <td>-954.3077</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>67</td>   <td>-2254.5484</td>  <td>0.001</td> <td>-3278.5223</td> <td>-1230.5745</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>68</td>   <td>-2257.3393</td>  <td>0.001</td> <td>-2961.5944</td> <td>-1553.0842</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>69</td>   <td>-1726.6452</td>  <td>0.001</td> <td>-2441.8196</td> <td>-1011.4708</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>      <td>7</td>   <td>-1736.1277</td>  <td>0.001</td> <td>-2463.5282</td> <td>-1008.7272</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>70</td>   <td>-2216.5945</td>  <td>0.001</td> <td>-2894.1014</td> <td>-1539.0877</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>71</td>   <td>-2013.6889</td>  <td>0.001</td> <td>-2680.3939</td> <td>-1346.9838</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>72</td>   <td>-1871.5376</td>  <td>0.001</td> <td>-2557.1056</td> <td>-1185.9696</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>73</td>   <td>-2210.7484</td>  <td>0.001</td> <td>-3117.3974</td> <td>-1304.0994</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>74</td>   <td>-2313.3638</td>  <td>0.001</td>  <td>-3243.725</td> <td>-1383.0025</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>75</td>   <td>-2339.1806</td>  <td>0.001</td> <td>-2996.3805</td> <td>-1681.9807</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>76</td>   <td>-2111.4326</td>  <td>0.001</td> <td>-2792.8759</td> <td>-1429.9893</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>     <td>77</td>   <td>-2273.5862</td>  <td>0.001</td> <td>-2959.1542</td> <td>-1588.0182</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>      <td>8</td>   <td>-1452.2868</td>  <td>0.001</td> <td>-2382.6481</td>  <td>-521.9256</td>  <td>True</td> 
</tr>
<tr>
    <td>29</td>      <td>9</td>    <td>-745.3484</td>   <td>0.9</td>  <td>-2102.2964</td>  <td>611.5996</td>   <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>30</td>     <td>205.069</td>    <td>0.9</td>   <td>-748.0312</td>  <td>1158.1691</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>31</td>     <td>60.4412</td>    <td>0.9</td>   <td>-842.9428</td>  <td>963.8251</td>   <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>32</td>    <td>354.7467</td>    <td>0.9</td>   <td>-735.7477</td>  <td>1445.2411</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>33</td>    <td>-203.1198</td>   <td>0.9</td>  <td>-1156.2199</td>  <td>749.9803</td>   <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>34</td>     <td>44.3333</td>    <td>0.9</td>  <td>-1004.9954</td>  <td>1093.662</td>   <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>35</td>    <td>117.5276</td>    <td>0.9</td>   <td>-824.3665</td>  <td>1059.4217</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>36</td>    <td>212.4495</td>    <td>0.9</td>   <td>-744.834</td>   <td>1169.7329</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>37</td>      <td>251.2</td>     <td>0.9</td>  <td>-1156.6222</td>  <td>1659.0222</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>38</td>    <td>5992.675</td>   <td>0.001</td>  <td>4997.1944</td>  <td>6988.1556</td>  <td>True</td> 
</tr>
<tr>
     <td>3</td>     <td>39</td>    <td>116.1195</td>    <td>0.9</td>   <td>-850.3321</td>  <td>1082.5711</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>      <td>4</td>    <td>214.5733</td>    <td>0.9</td>   <td>-813.5546</td>  <td>1242.7013</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>40</td>    <td>177.6808</td>    <td>0.9</td>   <td>-749.0612</td>  <td>1104.4229</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>41</td>    <td>-97.3756</td>    <td>0.9</td>  <td>-1012.1591</td>   <td>817.408</td>   <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>42</td>     <td>16.8644</td>    <td>0.9</td>   <td>-949.5872</td>   <td>983.316</td>   <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>43</td>    <td>569.9704</td>    <td>0.9</td>   <td>-406.9015</td>  <td>1546.8422</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>44</td>    <td>133.5159</td>    <td>0.9</td>   <td>-869.1524</td>  <td>1136.1842</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>45</td>     <td>81.9405</td>    <td>0.9</td>  <td>-1025.7281</td>  <td>1189.6091</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>46</td>    <td>-29.1111</td>    <td>0.9</td>   <td>-1005.983</td>  <td>947.7608</td>   <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>47</td>    <td>-49.1143</td>    <td>0.9</td>  <td>-1068.0212</td>  <td>969.7926</td>   <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>48</td>     <td>0.4583</td>     <td>0.9</td>  <td>-1407.3639</td>  <td>1408.2805</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>49</td>    <td>195.7143</td>    <td>0.9</td>   <td>-823.1926</td>  <td>1214.6212</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>      <td>5</td>    <td>323.4483</td>    <td>0.9</td>   <td>-882.1386</td>  <td>1529.0352</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>50</td>     <td>94.3333</td>    <td>0.9</td>  <td>-1111.2536</td>  <td>1299.9202</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>51</td>    <td>753.4018</td>  <td>0.4918</td>  <td>-178.9513</td>  <td>1685.7548</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>52</td>    <td>-153.3167</td>   <td>0.9</td>  <td>-1124.8063</td>  <td>818.1729</td>   <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>53</td>    <td>349.3402</td>    <td>0.9</td>   <td>-617.1114</td>  <td>1315.7918</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>54</td>    <td>-114.4167</td>   <td>0.9</td>  <td>-1052.9648</td>  <td>824.1315</td>   <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>55</td>    <td>334.6061</td>    <td>0.9</td>   <td>-614.5475</td>  <td>1283.7596</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>56</td>    <td>645.7573</td>  <td>0.7815</td>  <td>-259.3457</td>  <td>1550.8604</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>57</td>     <td>82.8029</td>    <td>0.9</td>   <td>-919.8654</td>  <td>1085.4712</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>58</td>    <td>113.5972</td>    <td>0.9</td>   <td>-935.7315</td>  <td>1162.9259</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>59</td>    <td>988.4487</td>  <td>0.0099</td>   <td>86.7208</td>   <td>1890.1766</td>  <td>True</td> 
</tr>
<tr>
     <td>3</td>      <td>6</td>    <td>355.4167</td>    <td>0.9</td>   <td>-794.0653</td>  <td>1504.8987</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>60</td>    <td>681.0533</td>   <td>0.662</td>  <td>-224.0497</td>  <td>1586.1564</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>61</td>    <td>309.3681</td>    <td>0.9</td>   <td>-693.3002</td>  <td>1312.0364</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>62</td>    <td>719.5865</td>  <td>0.5465</td>  <td>-191.0902</td>  <td>1630.2633</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>63</td>    <td>784.2922</td>  <td>0.7039</td>  <td>-277.3098</td>  <td>1845.8941</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>64</td>    <td>387.6954</td>    <td>0.9</td>   <td>-578.7562</td>  <td>1354.147</td>   <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>65</td>    <td>160.2043</td>    <td>0.9</td>   <td>-797.0792</td>  <td>1117.4878</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>66</td>    <td>183.2083</td>    <td>0.9</td>  <td>-1101.9516</td>  <td>1468.3683</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>67</td>     <td>-0.4667</td>    <td>0.9</td>  <td>-1206.0536</td>  <td>1205.1202</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>68</td>     <td>-3.2576</td>    <td>0.9</td>   <td>-952.4111</td>   <td>945.896</td>   <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>69</td>    <td>527.4366</td>    <td>0.9</td>   <td>-429.8469</td>   <td>1484.72</td>   <td>False</td>
</tr>
<tr>
     <td>3</td>      <td>7</td>     <td>517.954</td>    <td>0.9</td>   <td>-448.4976</td>  <td>1484.4056</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>70</td>     <td>37.4872</td>    <td>0.9</td>   <td>-891.9926</td>   <td>966.967</td>   <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>71</td>    <td>240.3929</td>    <td>0.9</td>   <td>-681.2431</td>  <td>1162.0288</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>72</td>    <td>382.5441</td>    <td>0.9</td>   <td>-552.8278</td>  <td>1317.9161</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>73</td>     <td>43.3333</td>    <td>0.9</td>  <td>-1064.3352</td>  <td>1151.0019</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>74</td>    <td>-59.2821</td>    <td>0.9</td>  <td>-1186.4419</td>  <td>1067.8778</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>75</td>    <td>-85.0989</td>    <td>0.9</td>   <td>-999.8824</td>  <td>829.6847</td>   <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>76</td>    <td>142.6491</td>    <td>0.9</td>   <td>-789.7039</td>  <td>1075.0021</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>     <td>77</td>    <td>-19.5045</td>    <td>0.9</td>   <td>-954.8765</td>  <td>915.8675</td>   <td>False</td>
</tr>
<tr>
     <td>3</td>      <td>8</td>    <td>801.7949</td>   <td>0.788</td>  <td>-325.365</td>   <td>1928.9547</td>  <td>False</td>
</tr>
<tr>
     <td>3</td>      <td>9</td>    <td>1508.7333</td> <td>0.0453</td>   <td>9.9922</td>    <td>3007.4745</td>  <td>True</td> 
</tr>
<tr>
    <td>30</td>     <td>31</td>    <td>-144.6278</td>   <td>0.9</td>   <td>-779.603</td>   <td>490.3474</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>32</td>    <td>149.6777</td>    <td>0.9</td>   <td>-731.3836</td>  <td>1030.739</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>33</td>    <td>-408.1888</td>   <td>0.9</td>  <td>-1112.0998</td>  <td>295.7223</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>34</td>    <td>-160.7356</td>   <td>0.9</td>   <td>-990.3028</td>  <td>668.8316</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>35</td>    <td>-87.5413</td>    <td>0.9</td>   <td>-776.2035</td>  <td>601.1208</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>36</td>     <td>7.3805</td>     <td>0.9</td>   <td>-702.1846</td>  <td>716.9456</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>37</td>     <td>46.131</td>     <td>0.9</td>  <td>-1206.4879</td>   <td>1298.75</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>38</td>    <td>5787.606</td>   <td>0.001</td>  <td>5027.2952</td>  <td>6547.9169</td>  <td>True</td> 
</tr>
<tr>
    <td>30</td>     <td>39</td>    <td>-88.9494</td>    <td>0.9</td>   <td>-810.8356</td>  <td>632.9368</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>      <td>4</td>     <td>9.5044</td>     <td>0.9</td>   <td>-793.0778</td>  <td>812.0865</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>40</td>    <td>-27.3881</td>    <td>0.9</td>   <td>-695.1768</td>  <td>640.4006</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>41</td>    <td>-302.4445</td>   <td>0.9</td>   <td>-953.5359</td>  <td>348.6468</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>42</td>    <td>-188.2046</td>   <td>0.9</td>   <td>-910.0908</td>  <td>533.6816</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>43</td>    <td>364.9014</td>    <td>0.9</td>   <td>-370.8768</td>  <td>1100.6796</td>  <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>44</td>     <td>-71.553</td>    <td>0.9</td>   <td>-841.2508</td>  <td>698.1448</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>45</td>    <td>-123.1285</td>   <td>0.9</td>  <td>-1025.3594</td>  <td>779.1025</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>46</td>    <td>-234.1801</td>   <td>0.9</td>   <td>-969.9583</td>  <td>501.5982</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>47</td>    <td>-254.1832</td>   <td>0.9</td>  <td>-1044.9185</td>   <td>536.552</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>48</td>    <td>-204.6106</td>   <td>0.9</td>  <td>-1457.2296</td>  <td>1048.0084</td>  <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>49</td>     <td>-9.3547</td>    <td>0.9</td>   <td>-800.0899</td>  <td>781.3806</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>      <td>5</td>    <td>118.3794</td>    <td>0.9</td>   <td>-901.6847</td>  <td>1138.4435</td>  <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>50</td>    <td>-110.7356</td>   <td>0.9</td>  <td>-1130.7997</td>  <td>909.3285</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>51</td>    <td>548.3328</td>  <td>0.4805</td>  <td>-127.2212</td>  <td>1223.8867</td>  <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>52</td>    <td>-358.3856</td>   <td>0.9</td>  <td>-1087.0028</td>  <td>370.2316</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>53</td>    <td>144.2713</td>    <td>0.9</td>   <td>-577.6149</td>  <td>866.1575</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>54</td>    <td>-319.4856</td>   <td>0.9</td>  <td>-1003.5642</td>   <td>364.593</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>55</td>    <td>129.5371</td>    <td>0.9</td>   <td>-569.021</td>   <td>828.0952</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>56</td>    <td>440.6884</td>  <td>0.8492</td>  <td>-196.7302</td>  <td>1078.107</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>57</td>    <td>-122.2661</td>   <td>0.9</td>   <td>-891.9639</td>  <td>647.4317</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>58</td>    <td>-91.4717</td>    <td>0.9</td>   <td>-921.0389</td>  <td>738.0954</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>59</td>    <td>783.3798</td>   <td>0.001</td>  <td>150.7629</td>   <td>1415.9967</td>  <td>True</td> 
</tr>
<tr>
    <td>30</td>      <td>6</td>    <td>150.3477</td>    <td>0.9</td>   <td>-802.7524</td>  <td>1103.4478</td>  <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>60</td>    <td>475.9844</td>  <td>0.6796</td>  <td>-161.4342</td>  <td>1113.403</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>61</td>    <td>104.2992</td>    <td>0.9</td>   <td>-665.3986</td>   <td>873.997</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>62</td>    <td>514.5176</td>  <td>0.5246</td>  <td>-130.791</td>   <td>1159.8261</td>  <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>63</td>    <td>579.2232</td>  <td>0.8674</td>  <td>-265.8151</td>  <td>1424.2615</td>  <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>64</td>    <td>182.6264</td>    <td>0.9</td>   <td>-539.2597</td>  <td>904.5126</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>65</td>    <td>-44.8647</td>    <td>0.9</td>   <td>-754.4298</td>  <td>664.7004</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>66</td>    <td>-21.8606</td>    <td>0.9</td>  <td>-1134.8418</td>  <td>1091.1205</td>  <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>67</td>    <td>-205.5356</td>   <td>0.9</td>  <td>-1225.5997</td>  <td>814.5285</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>68</td>    <td>-208.3265</td>   <td>0.9</td>   <td>-906.8846</td>  <td>490.2315</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>69</td>    <td>322.3676</td>    <td>0.9</td>   <td>-387.1975</td>  <td>1031.9327</td>  <td>False</td>
</tr>
<tr>
    <td>30</td>      <td>7</td>    <td>312.8851</td>    <td>0.9</td>   <td>-409.0011</td>  <td>1034.7713</td>  <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>70</td>    <td>-167.5818</td>   <td>0.9</td>   <td>-839.1648</td>  <td>504.0012</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>71</td>     <td>35.3239</td>    <td>0.9</td>   <td>-625.3605</td>  <td>696.0083</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>72</td>    <td>177.4752</td>    <td>0.9</td>   <td>-502.2393</td>  <td>857.1896</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>73</td>    <td>-161.7356</td>   <td>0.9</td>  <td>-1063.9666</td>  <td>740.4953</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>74</td>    <td>-264.351</td>    <td>0.9</td>  <td>-1190.4073</td>  <td>661.7053</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>75</td>    <td>-290.1678</td>   <td>0.9</td>   <td>-941.2592</td>  <td>360.9235</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>76</td>    <td>-62.4198</td>    <td>0.9</td>   <td>-737.9738</td>  <td>613.1341</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>     <td>77</td>    <td>-224.5735</td>   <td>0.9</td>   <td>-904.2879</td>   <td>455.141</td>   <td>False</td>
</tr>
<tr>
    <td>30</td>      <td>8</td>    <td>596.7259</td>    <td>0.9</td>   <td>-329.3304</td>  <td>1522.7822</td>  <td>False</td>
</tr>
<tr>
    <td>30</td>      <td>9</td>    <td>1303.6644</td> <td>0.0875</td>  <td>-50.3357</td>   <td>2657.6644</td>  <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>32</td>    <td>294.3055</td>    <td>0.9</td>   <td>-532.7203</td>  <td>1121.3313</td>  <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>33</td>    <td>-263.561</td>    <td>0.9</td>   <td>-898.5362</td>  <td>371.4142</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>34</td>    <td>-16.1078</td>    <td>0.9</td>   <td>-788.0433</td>  <td>755.8276</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>35</td>     <td>57.0864</td>    <td>0.9</td>   <td>-560.9412</td>  <td>675.1141</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>36</td>    <td>152.0083</td>    <td>0.9</td>   <td>-489.229</td>   <td>793.2456</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>37</td>    <td>190.7588</td>    <td>0.9</td>  <td>-1024.4601</td>  <td>1405.9777</td>  <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>38</td>    <td>5932.2338</td>  <td>0.001</td>  <td>5235.258</td>   <td>6629.2097</td>  <td>True</td> 
</tr>
<tr>
    <td>31</td>     <td>39</td>     <td>55.6784</td>    <td>0.9</td>   <td>-599.1669</td>  <td>710.5237</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>      <td>4</td>    <td>154.1322</td>    <td>0.9</td>   <td>-588.7277</td>   <td>896.992</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>40</td>    <td>117.2397</td>    <td>0.9</td>   <td>-477.4405</td>  <td>711.9198</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>41</td>    <td>-157.8167</td>   <td>0.9</td>   <td>-733.6836</td>  <td>418.0501</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>42</td>    <td>-43.5768</td>    <td>0.9</td>   <td>-698.4221</td>  <td>611.2685</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>43</td>    <td>509.5292</td>  <td>0.6379</td>  <td>-160.5994</td>  <td>1179.6578</td>  <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>44</td>     <td>73.0748</td>    <td>0.9</td>   <td>-634.1292</td>  <td>780.2787</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>45</td>     <td>21.4993</td>    <td>0.9</td>   <td>-828.0437</td>  <td>871.0423</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>46</td>    <td>-89.5523</td>    <td>0.9</td>   <td>-759.6809</td>  <td>580.5763</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>47</td>    <td>-109.5555</td>   <td>0.9</td>   <td>-839.5999</td>   <td>620.489</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>48</td>    <td>-59.9828</td>    <td>0.9</td>  <td>-1275.2018</td>  <td>1155.2361</td>  <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>49</td>    <td>135.2731</td>    <td>0.9</td>   <td>-594.7714</td>  <td>865.3176</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>      <td>5</td>    <td>263.0072</td>    <td>0.9</td>   <td>-710.7656</td>  <td>1236.7799</td>  <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>50</td>     <td>33.8922</td>    <td>0.9</td>   <td>-939.8806</td>  <td>1007.6649</td>  <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>51</td>    <td>692.9606</td>  <td>0.0037</td>   <td>89.5736</td>   <td>1296.3475</td>  <td>True</td> 
</tr>
<tr>
    <td>31</td>     <td>52</td>    <td>-213.7578</td>   <td>0.9</td>   <td>-876.0159</td>  <td>448.5002</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>53</td>    <td>288.8991</td>    <td>0.9</td>   <td>-365.9462</td>  <td>943.7443</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>54</td>    <td>-174.8578</td>   <td>0.9</td>   <td>-787.774</td>   <td>438.0583</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>55</td>    <td>274.1649</td>    <td>0.9</td>   <td>-354.871</td>   <td>903.2007</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>56</td>    <td>585.3162</td>  <td>0.0244</td>   <td>24.9545</td>   <td>1145.6778</td>  <td>True</td> 
</tr>
<tr>
    <td>31</td>     <td>57</td>     <td>22.3617</td>    <td>0.9</td>   <td>-684.8422</td>  <td>729.5656</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>58</td>     <td>53.156</td>     <td>0.9</td>   <td>-718.7794</td>  <td>825.0915</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>59</td>    <td>928.0075</td>   <td>0.001</td>   <td>373.114</td>   <td>1482.9011</td>  <td>True</td> 
</tr>
<tr>
    <td>31</td>      <td>6</td>    <td>294.9755</td>    <td>0.9</td>   <td>-608.4085</td>  <td>1198.3594</td>  <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>60</td>    <td>620.6122</td>  <td>0.0081</td>   <td>60.2505</td>   <td>1180.9738</td>  <td>True</td> 
</tr>
<tr>
    <td>31</td>     <td>61</td>    <td>248.9269</td>    <td>0.9</td>   <td>-458.277</td>   <td>956.1309</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>62</td>    <td>659.1453</td>  <td>0.0031</td>   <td>89.8248</td>   <td>1228.4659</td>  <td>True</td> 
</tr>
<tr>
    <td>31</td>     <td>63</td>     <td>723.851</td>  <td>0.1586</td>  <td>-64.6872</td>   <td>1512.3891</td>  <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>64</td>    <td>327.2542</td>    <td>0.9</td>   <td>-327.5911</td>  <td>982.0995</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>65</td>     <td>99.7631</td>    <td>0.9</td>   <td>-541.4742</td>  <td>741.0005</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>66</td>    <td>122.7672</td>    <td>0.9</td>   <td>-947.9475</td>  <td>1193.4818</td>  <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>67</td>    <td>-60.9078</td>    <td>0.9</td>  <td>-1034.6806</td>  <td>912.8649</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>68</td>    <td>-63.6988</td>    <td>0.9</td>   <td>-692.7346</td>  <td>565.3371</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>69</td>    <td>466.9954</td>  <td>0.7361</td>  <td>-174.2419</td>  <td>1108.2327</td>  <td>False</td>
</tr>
<tr>
    <td>31</td>      <td>7</td>    <td>457.5128</td>  <td>0.8269</td>  <td>-197.3324</td>  <td>1112.3581</td>  <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>70</td>     <td>-22.954</td>    <td>0.9</td>   <td>-621.8917</td>  <td>575.9837</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>71</td>    <td>179.9517</td>    <td>0.9</td>   <td>-406.7395</td>  <td>766.6428</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>72</td>     <td>322.103</td>    <td>0.9</td>   <td>-285.9385</td>  <td>930.1444</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>73</td>    <td>-17.1078</td>    <td>0.9</td>   <td>-866.6509</td>  <td>832.4352</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>74</td>    <td>-119.7232</td>   <td>0.9</td>   <td>-994.5278</td>  <td>755.0813</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>75</td>    <td>-145.5401</td>   <td>0.9</td>   <td>-721.4069</td>  <td>430.3268</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>76</td>     <td>82.2079</td>    <td>0.9</td>   <td>-521.179</td>   <td>685.5949</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>     <td>77</td>    <td>-79.9457</td>    <td>0.9</td>   <td>-687.9871</td>  <td>528.0958</td>   <td>False</td>
</tr>
<tr>
    <td>31</td>      <td>8</td>    <td>741.3537</td>  <td>0.3494</td>  <td>-133.4508</td>  <td>1616.1582</td>  <td>False</td>
</tr>
<tr>
    <td>31</td>      <td>9</td>    <td>1448.2922</td> <td>0.0096</td>  <td>128.8155</td>   <td>2767.7689</td>  <td>True</td> 
</tr>
<tr>
    <td>32</td>     <td>33</td>    <td>-557.8665</td>   <td>0.9</td>  <td>-1438.9277</td>  <td>323.1948</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>34</td>    <td>-310.4133</td>   <td>0.9</td>  <td>-1294.7709</td>  <td>673.9443</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>35</td>    <td>-237.219</td>    <td>0.9</td>  <td>-1106.1458</td>  <td>631.7077</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>36</td>    <td>-142.2972</td>   <td>0.9</td>  <td>-1027.8822</td>  <td>743.2878</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>37</td>    <td>-103.5467</td>   <td>0.9</td>  <td>-1463.6321</td>  <td>1256.5388</td>  <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>38</td>    <td>5637.9283</td>  <td>0.001</td>  <td>4711.1863</td>  <td>6564.6704</td>  <td>True</td> 
</tr>
<tr>
    <td>32</td>     <td>39</td>    <td>-238.6271</td>   <td>0.9</td>  <td>-1134.1146</td>  <td>656.8603</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>      <td>4</td>    <td>-140.1733</td>   <td>0.9</td>   <td>-1101.899</td>  <td>821.5523</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>40</td>    <td>-177.0658</td>   <td>0.9</td>  <td>-1029.5445</td>  <td>675.4128</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>41</td>    <td>-452.1222</td>   <td>0.9</td>  <td>-1291.5852</td>  <td>387.3407</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>42</td>    <td>-337.8823</td>   <td>0.9</td>  <td>-1233.3698</td>  <td>557.6052</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>43</td>    <td>215.2237</td>    <td>0.9</td>   <td>-691.4999</td>  <td>1121.9473</td>  <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>44</td>    <td>-221.2307</td>   <td>0.9</td>  <td>-1155.6893</td>  <td>713.2279</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>45</td>    <td>-272.8062</td>   <td>0.9</td>  <td>-1319.1325</td>  <td>773.5201</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>46</td>    <td>-383.8578</td>   <td>0.9</td>  <td>-1290.5814</td>  <td>522.8659</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>47</td>    <td>-403.861</td>    <td>0.9</td>  <td>-1355.7225</td>  <td>548.0006</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>48</td>    <td>-354.2883</td>   <td>0.9</td>  <td>-1714.3738</td>  <td>1005.7971</td>  <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>49</td>    <td>-159.0324</td>   <td>0.9</td>  <td>-1110.8939</td>  <td>792.8292</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>      <td>5</td>    <td>-31.2983</td>    <td>0.9</td>  <td>-1180.7803</td>  <td>1118.1837</td>  <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>50</td>    <td>-260.4133</td>   <td>0.9</td>  <td>-1409.8953</td>  <td>889.0687</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>51</td>    <td>398.6551</td>    <td>0.9</td>   <td>-459.9201</td>  <td>1257.2302</td>  <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>52</td>    <td>-508.0633</td>   <td>0.9</td>  <td>-1408.9857</td>  <td>392.8591</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>53</td>     <td>-5.4064</td>    <td>0.9</td>   <td>-900.8939</td>   <td>890.081</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>54</td>    <td>-469.1633</td>   <td>0.9</td>   <td>-1334.462</td>  <td>396.1353</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>55</td>    <td>-20.1406</td>    <td>0.9</td>   <td>-896.9311</td>  <td>856.6499</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>56</td>    <td>291.0107</td>    <td>0.9</td>   <td>-537.8926</td>  <td>1119.9139</td>  <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>57</td>    <td>-271.9438</td>   <td>0.9</td>  <td>-1206.4023</td>  <td>662.5148</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>58</td>    <td>-241.1494</td>   <td>0.9</td>   <td>-1225.507</td>  <td>743.2081</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>59</td>    <td>633.7021</td>  <td>0.6146</td>  <td>-191.5144</td>  <td>1458.9186</td>  <td>False</td>
</tr>
<tr>
    <td>32</td>      <td>6</td>      <td>0.67</td>      <td>0.9</td>  <td>-1089.8244</td>  <td>1091.1644</td>  <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>60</td>    <td>326.3067</td>    <td>0.9</td>   <td>-502.5966</td>  <td>1155.2099</td>  <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>61</td>    <td>-45.3786</td>    <td>0.9</td>   <td>-979.8371</td>   <td>889.08</td>    <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>62</td>    <td>364.8399</td>    <td>0.9</td>   <td>-470.1459</td>  <td>1199.8257</td>  <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>63</td>    <td>429.5455</td>    <td>0.9</td>   <td>-567.8851</td>  <td>1426.9761</td>  <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>64</td>     <td>32.9487</td>    <td>0.9</td>   <td>-862.5387</td>  <td>928.4362</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>65</td>    <td>-194.5424</td>   <td>0.9</td>  <td>-1080.1273</td>  <td>691.0426</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>66</td>    <td>-171.5383</td>   <td>0.9</td>  <td>-1404.2205</td>  <td>1061.1438</td>  <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>67</td>    <td>-355.2133</td>   <td>0.9</td>  <td>-1504.6953</td>  <td>794.2687</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>68</td>    <td>-358.0042</td>   <td>0.9</td>  <td>-1234.7947</td>  <td>518.7862</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>69</td>    <td>172.6899</td>    <td>0.9</td>   <td>-712.8951</td>  <td>1058.2749</td>  <td>False</td>
</tr>
<tr>
    <td>32</td>      <td>7</td>    <td>163.2074</td>    <td>0.9</td>   <td>-732.2801</td>  <td>1058.6948</td>  <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>70</td>    <td>-317.2595</td>   <td>0.9</td>  <td>-1172.7137</td>  <td>538.1947</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>71</td>    <td>-114.3538</td>   <td>0.9</td>   <td>-961.2788</td>  <td>732.5712</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>72</td>     <td>27.7975</td>    <td>0.9</td>   <td>-834.0551</td>  <td>889.6501</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>73</td>    <td>-311.4133</td>   <td>0.9</td>  <td>-1357.7397</td>   <td>734.913</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>74</td>    <td>-414.0287</td>   <td>0.9</td>  <td>-1480.9675</td>  <td>652.9101</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>75</td>    <td>-439.8456</td>   <td>0.9</td>  <td>-1279.3085</td>  <td>399.6174</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>76</td>    <td>-212.0975</td>   <td>0.9</td>  <td>-1070.6727</td>  <td>646.4776</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>     <td>77</td>    <td>-374.2512</td>   <td>0.9</td>  <td>-1236.1037</td>  <td>487.6014</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>      <td>8</td>    <td>447.0482</td>    <td>0.9</td>   <td>-619.8906</td>  <td>1513.987</td>   <td>False</td>
</tr>
<tr>
    <td>32</td>      <td>9</td>    <td>1153.9867</td> <td>0.5358</td>  <td>-300.0058</td>  <td>2607.9792</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>34</td>    <td>247.4531</td>    <td>0.9</td>   <td>-582.1141</td>  <td>1077.0203</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>35</td>    <td>320.6474</td>    <td>0.9</td>   <td>-368.0147</td>  <td>1009.3095</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>36</td>    <td>415.5693</td>    <td>0.9</td>   <td>-293.9958</td>  <td>1125.1343</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>37</td>    <td>454.3198</td>    <td>0.9</td>   <td>-798.2992</td>  <td>1706.9388</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>38</td>    <td>6195.7948</td>  <td>0.001</td>  <td>5435.4839</td>  <td>6956.1057</td>  <td>True</td> 
</tr>
<tr>
    <td>33</td>     <td>39</td>    <td>319.2393</td>    <td>0.9</td>   <td>-402.6469</td>  <td>1041.1255</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>      <td>4</td>    <td>417.6931</td>    <td>0.9</td>   <td>-384.889</td>   <td>1220.2753</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>40</td>    <td>380.8006</td>    <td>0.9</td>   <td>-286.9881</td>  <td>1048.5893</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>41</td>    <td>105.7442</td>    <td>0.9</td>   <td>-545.3471</td>  <td>756.8356</td>   <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>42</td>    <td>219.9842</td>    <td>0.9</td>   <td>-501.902</td>   <td>941.8703</td>   <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>43</td>    <td>773.0902</td>   <td>0.022</td>   <td>37.3119</td>   <td>1508.8684</td>  <td>True</td> 
</tr>
<tr>
    <td>33</td>     <td>44</td>    <td>336.6357</td>    <td>0.9</td>   <td>-433.0621</td>  <td>1106.3335</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>45</td>    <td>285.0603</td>    <td>0.9</td>   <td>-617.1707</td>  <td>1187.2912</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>46</td>    <td>174.0087</td>    <td>0.9</td>   <td>-561.7696</td>  <td>909.7869</td>   <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>47</td>    <td>154.0055</td>    <td>0.9</td>   <td>-636.7297</td>  <td>944.7408</td>   <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>48</td>    <td>203.5781</td>    <td>0.9</td>  <td>-1049.0409</td>  <td>1456.1971</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>49</td>    <td>398.8341</td>    <td>0.9</td>   <td>-391.9012</td>  <td>1189.5693</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>      <td>5</td>    <td>526.5681</td>    <td>0.9</td>   <td>-493.496</td>   <td>1546.6322</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>50</td>    <td>297.4531</td>    <td>0.9</td>   <td>-722.611</td>   <td>1317.5172</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>51</td>    <td>956.5215</td>   <td>0.001</td>  <td>280.9676</td>   <td>1632.0755</td>  <td>True</td> 
</tr>
<tr>
    <td>33</td>     <td>52</td>     <td>49.8031</td>    <td>0.9</td>   <td>-678.8141</td>  <td>778.4203</td>   <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>53</td>     <td>552.46</td>   <td>0.6227</td>  <td>-169.4262</td>  <td>1274.3462</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>54</td>     <td>88.7031</td>    <td>0.9</td>   <td>-595.3755</td>  <td>772.7817</td>   <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>55</td>    <td>537.7259</td>   <td>0.609</td>  <td>-160.8322</td>  <td>1236.2839</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>56</td>    <td>848.8771</td>   <td>0.001</td>  <td>211.4585</td>   <td>1486.2957</td>  <td>True</td> 
</tr>
<tr>
    <td>33</td>     <td>57</td>    <td>285.9227</td>    <td>0.9</td>   <td>-483.7751</td>  <td>1055.6205</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>58</td>     <td>316.717</td>    <td>0.9</td>   <td>-512.8502</td>  <td>1146.2842</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>59</td>    <td>1191.5685</td>  <td>0.001</td>  <td>558.9516</td>   <td>1824.1854</td>  <td>True</td> 
</tr>
<tr>
    <td>33</td>      <td>6</td>    <td>558.5365</td>    <td>0.9</td>   <td>-394.5637</td>  <td>1511.6366</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>60</td>    <td>884.1731</td>   <td>0.001</td>  <td>246.7545</td>   <td>1521.5917</td>  <td>True</td> 
</tr>
<tr>
    <td>33</td>     <td>61</td>    <td>512.4879</td>    <td>0.9</td>   <td>-257.2099</td>  <td>1282.1857</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>62</td>    <td>922.7063</td>   <td>0.001</td>  <td>277.3977</td>   <td>1568.0149</td>  <td>True</td> 
</tr>
<tr>
    <td>33</td>     <td>63</td>    <td>987.4119</td>  <td>0.0025</td>  <td>142.3736</td>   <td>1832.4502</td>  <td>True</td> 
</tr>
<tr>
    <td>33</td>     <td>64</td>    <td>590.8152</td>  <td>0.4581</td>  <td>-131.071</td>   <td>1312.7014</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>65</td>    <td>363.3241</td>    <td>0.9</td>   <td>-346.241</td>   <td>1072.8892</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>66</td>    <td>386.3281</td>    <td>0.9</td>   <td>-726.653</td>   <td>1499.3093</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>67</td>    <td>202.6531</td>    <td>0.9</td>   <td>-817.411</td>   <td>1222.7172</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>68</td>    <td>199.8622</td>    <td>0.9</td>   <td>-498.6959</td>  <td>898.4203</td>   <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>69</td>    <td>730.5564</td>  <td>0.0314</td>   <td>20.9913</td>   <td>1440.1214</td>  <td>True</td> 
</tr>
<tr>
    <td>33</td>      <td>7</td>    <td>721.0738</td>  <td>0.0509</td>   <td>-0.8124</td>    <td>1442.96</td>   <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>70</td>     <td>240.607</td>    <td>0.9</td>   <td>-430.976</td>    <td>912.19</td>    <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>71</td>    <td>443.5126</td>    <td>0.9</td>   <td>-217.1717</td>  <td>1104.197</td>   <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>72</td>    <td>585.6639</td>  <td>0.3024</td>  <td>-94.0505</td>   <td>1265.3784</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>73</td>    <td>246.4531</td>    <td>0.9</td>   <td>-655.7778</td>  <td>1148.6841</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>74</td>    <td>143.8377</td>    <td>0.9</td>   <td>-782.2186</td>  <td>1069.8941</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>75</td>    <td>118.0209</td>    <td>0.9</td>   <td>-533.0704</td>  <td>769.1122</td>   <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>76</td>    <td>345.7689</td>    <td>0.9</td>   <td>-329.785</td>   <td>1021.3229</td>  <td>False</td>
</tr>
<tr>
    <td>33</td>     <td>77</td>    <td>183.6153</td>    <td>0.9</td>   <td>-496.0992</td>  <td>863.3297</td>   <td>False</td>
</tr>
<tr>
    <td>33</td>      <td>8</td>    <td>1004.9147</td> <td>0.0121</td>   <td>78.8584</td>   <td>1930.971</td>   <td>True</td> 
</tr>
<tr>
    <td>33</td>      <td>9</td>    <td>1711.8531</td>  <td>0.001</td>  <td>357.8531</td>   <td>3065.8532</td>  <td>True</td> 
</tr>
<tr>
    <td>34</td>     <td>35</td>     <td>73.1943</td>    <td>0.9</td>   <td>-743.4736</td>  <td>889.8621</td>   <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>36</td>    <td>168.1161</td>    <td>0.9</td>   <td>-666.254</td>   <td>1002.4863</td>  <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>37</td>    <td>206.8667</td>    <td>0.9</td>  <td>-1120.4408</td>  <td>1534.1742</td>  <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>38</td>    <td>5948.3417</td>  <td>0.001</td>  <td>5070.4103</td>  <td>6826.2731</td>  <td>True</td> 
</tr>
<tr>
    <td>34</td>     <td>39</td>     <td>71.7862</td>    <td>0.9</td>   <td>-773.0869</td>  <td>916.6593</td>   <td>False</td>
</tr>
<tr>
    <td>34</td>      <td>4</td>     <td>170.24</td>     <td>0.9</td>   <td>-744.5436</td>  <td>1085.0236</td>  <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>40</td>    <td>133.3475</td>    <td>0.9</td>   <td>-665.7974</td>  <td>932.4924</td>   <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>41</td>    <td>-141.7089</td>   <td>0.9</td>   <td>-926.9546</td>  <td>643.5368</td>   <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>42</td>     <td>-27.469</td>    <td>0.9</td>   <td>-872.3421</td>  <td>817.4041</td>   <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>43</td>     <td>525.637</td>    <td>0.9</td>   <td>-331.1363</td>  <td>1382.4103</td>  <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>44</td>     <td>89.1826</td>    <td>0.9</td>   <td>-796.8905</td>  <td>975.2557</td>   <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>45</td>     <td>37.6071</td>    <td>0.9</td>   <td>-965.743</td>   <td>1040.9573</td>  <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>46</td>    <td>-73.4444</td>    <td>0.9</td>   <td>-930.2177</td>  <td>783.3289</td>   <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>47</td>    <td>-93.4476</td>    <td>0.9</td>   <td>-997.8552</td>   <td>810.96</td>    <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>48</td>     <td>-43.875</td>    <td>0.9</td>  <td>-1371.1825</td>  <td>1283.4325</td>  <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>49</td>     <td>151.381</td>    <td>0.9</td>   <td>-753.0267</td>  <td>1055.7886</td>  <td>False</td>
</tr>
<tr>
    <td>34</td>      <td>5</td>     <td>279.115</td>    <td>0.9</td>   <td>-831.3901</td>  <td>1389.6201</td>  <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>50</td>      <td>50.0</td>      <td>0.9</td>  <td>-1060.5051</td>  <td>1160.5051</td>  <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>51</td>    <td>709.0684</td>  <td>0.2475</td>  <td>-96.5767</td>   <td>1514.7135</td>  <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>52</td>     <td>-197.65</td>    <td>0.9</td>  <td>-1048.2815</td>  <td>652.9815</td>   <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>53</td>    <td>305.0069</td>    <td>0.9</td>   <td>-539.8662</td>   <td>1149.88</td>   <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>54</td>     <td>-158.75</td>    <td>0.9</td>   <td>-971.5565</td>  <td>654.0565</td>   <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>55</td>    <td>290.2727</td>    <td>0.9</td>   <td>-534.7571</td>  <td>1115.3026</td>  <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>56</td>     <td>601.424</td>  <td>0.5866</td>  <td>-172.5226</td>  <td>1375.3706</td>  <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>57</td>     <td>38.4696</td>    <td>0.9</td>   <td>-847.6036</td>  <td>924.5427</td>   <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>58</td>     <td>69.2639</td>    <td>0.9</td>   <td>-869.2842</td>  <td>1007.812</td>   <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>59</td>    <td>944.1154</td>   <td>0.001</td>  <td>174.1186</td>   <td>1714.1121</td>  <td>True</td> 
</tr>
<tr>
    <td>34</td>      <td>6</td>    <td>311.0833</td>    <td>0.9</td>   <td>-738.2454</td>  <td>1360.412</td>   <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>60</td>     <td>636.72</td>   <td>0.4431</td>  <td>-137.2266</td>  <td>1410.6666</td>  <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>61</td>    <td>265.0348</td>    <td>0.9</td>   <td>-621.0383</td>  <td>1151.1079</td>  <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>62</td>    <td>675.2532</td>  <td>0.2915</td>  <td>-105.2044</td>  <td>1455.7108</td>  <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>63</td>    <td>739.9588</td>  <td>0.5866</td>  <td>-212.2915</td>  <td>1692.2091</td>  <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>64</td>    <td>343.3621</td>    <td>0.9</td>   <td>-501.511</td>   <td>1188.2352</td>  <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>65</td>     <td>115.871</td>    <td>0.9</td>   <td>-718.4992</td>  <td>950.2411</td>   <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>66</td>     <td>138.875</td>    <td>0.9</td>  <td>-1057.5438</td>  <td>1335.2938</td>  <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>67</td>      <td>-44.8</td>     <td>0.9</td>  <td>-1155.3051</td>  <td>1065.7051</td>  <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>68</td>    <td>-47.5909</td>    <td>0.9</td>   <td>-872.6208</td>   <td>777.439</td>   <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>69</td>    <td>483.1032</td>    <td>0.9</td>   <td>-351.2669</td>  <td>1317.4733</td>  <td>False</td>
</tr>
<tr>
    <td>34</td>      <td>7</td>    <td>473.6207</td>    <td>0.9</td>   <td>-371.2524</td>  <td>1318.4938</td>  <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>70</td>     <td>-6.8462</td>    <td>0.9</td>   <td>-809.1644</td>  <td>795.4721</td>   <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>71</td>    <td>196.0595</td>    <td>0.9</td>   <td>-597.1584</td>  <td>989.2775</td>   <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>72</td>    <td>338.2108</td>    <td>0.9</td>   <td>-470.9261</td>  <td>1147.3478</td>  <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>73</td>      <td>-1.0</td>      <td>0.9</td>  <td>-1004.3502</td>  <td>1002.3502</td>  <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>74</td>    <td>-103.6154</td>   <td>0.9</td>  <td>-1128.4428</td>   <td>921.212</td>   <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>75</td>    <td>-129.4322</td>   <td>0.9</td>   <td>-914.6779</td>  <td>655.8135</td>   <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>76</td>     <td>98.3158</td>    <td>0.9</td>   <td>-707.3293</td>  <td>903.9609</td>   <td>False</td>
</tr>
<tr>
    <td>34</td>     <td>77</td>    <td>-63.8378</td>    <td>0.9</td>   <td>-872.9748</td>  <td>745.2991</td>   <td>False</td>
</tr>
<tr>
    <td>34</td>      <td>8</td>    <td>757.4615</td>  <td>0.7029</td>  <td>-267.3658</td>  <td>1782.2889</td>  <td>False</td>
</tr>
<tr>
    <td>34</td>      <td>9</td>     <td>1464.4</td>   <td>0.0318</td>   <td>41.0213</td>   <td>2887.7787</td>  <td>True</td> 
</tr>
<tr>
    <td>35</td>     <td>36</td>     <td>94.9218</td>    <td>0.9</td>   <td>-599.5184</td>  <td>789.3621</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>37</td>    <td>133.6724</td>    <td>0.9</td>  <td>-1110.4414</td>  <td>1377.7861</td>  <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>38</td>    <td>5875.1474</td>  <td>0.001</td>  <td>5128.9321</td>  <td>6621.3627</td>  <td>True</td> 
</tr>
<tr>
    <td>35</td>     <td>39</td>     <td>-1.4081</td>    <td>0.9</td>   <td>-708.4331</td>  <td>705.6169</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>      <td>4</td>     <td>97.0457</td>    <td>0.9</td>   <td>-692.1962</td>  <td>886.2876</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>40</td>     <td>60.1532</td>    <td>0.9</td>   <td>-591.5418</td>  <td>711.8483</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>41</td>    <td>-214.9032</td>   <td>0.9</td>   <td>-849.4775</td>  <td>419.6712</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>42</td>    <td>-100.6633</td>   <td>0.9</td>   <td>-807.6882</td>  <td>606.3617</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>43</td>    <td>452.4428</td>    <td>0.9</td>   <td>-268.7606</td>  <td>1173.6461</td>  <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>44</td>     <td>15.9883</td>    <td>0.9</td>   <td>-739.789</td>   <td>771.7657</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>45</td>    <td>-35.5871</td>    <td>0.9</td>   <td>-925.9721</td>  <td>854.7978</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>46</td>    <td>-146.6387</td>   <td>0.9</td>   <td>-867.8421</td>  <td>574.5646</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>47</td>    <td>-166.6419</td>   <td>0.9</td>   <td>-943.8336</td>  <td>610.5498</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>48</td>    <td>-117.0693</td>   <td>0.9</td>   <td>-1361.183</td>  <td>1127.0444</td>  <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>49</td>     <td>78.1867</td>    <td>0.9</td>   <td>-699.005</td>   <td>855.3784</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>      <td>5</td>    <td>205.9207</td>    <td>0.9</td>   <td>-803.6809</td>  <td>1215.5223</td>  <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>50</td>    <td>-23.1943</td>    <td>0.9</td>  <td>-1032.7959</td>  <td>986.4073</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>51</td>    <td>635.8741</td>  <td>0.0865</td>  <td>-23.7756</td>   <td>1295.5239</td>  <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>52</td>    <td>-270.8443</td>   <td>0.9</td>   <td>-984.7404</td>  <td>443.0519</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>53</td>    <td>231.8126</td>    <td>0.9</td>   <td>-475.2124</td>  <td>938.8376</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>54</td>    <td>-231.9443</td>   <td>0.9</td>   <td>-900.3216</td>   <td>436.433</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>55</td>    <td>217.0784</td>    <td>0.9</td>   <td>-466.1112</td>  <td>900.2681</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>56</td>    <td>528.2297</td>  <td>0.3355</td>  <td>-92.3081</td>   <td>1148.7675</td>  <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>57</td>    <td>-34.7247</td>    <td>0.9</td>   <td>-790.502</td>   <td>721.0526</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>58</td>     <td>-3.9304</td>    <td>0.9</td>   <td>-820.5983</td>  <td>812.7375</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>59</td>    <td>870.9211</td>   <td>0.001</td>  <td>255.3167</td>   <td>1486.5255</td>  <td>True</td> 
</tr>
<tr>
    <td>35</td>      <td>6</td>     <td>237.889</td>    <td>0.9</td>   <td>-704.0051</td>  <td>1179.7832</td>  <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>60</td>    <td>563.5257</td>  <td>0.1783</td>  <td>-57.0121</td>   <td>1184.0635</td>  <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>61</td>    <td>191.8405</td>    <td>0.9</td>   <td>-563.9368</td>  <td>947.6178</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>62</td>    <td>602.0589</td>  <td>0.0927</td>  <td>-26.5808</td>   <td>1230.6986</td>  <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>63</td>    <td>666.7645</td>  <td>0.5132</td>  <td>-165.6142</td>  <td>1499.1433</td>  <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>64</td>    <td>270.1678</td>    <td>0.9</td>   <td>-436.8572</td>  <td>977.1928</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>65</td>     <td>42.6767</td>    <td>0.9</td>   <td>-651.7636</td>   <td>737.117</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>66</td>     <td>65.6807</td>    <td>0.9</td>  <td>-1037.7194</td>  <td>1169.0808</td>  <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>67</td>    <td>-117.9943</td>   <td>0.9</td>  <td>-1127.5959</td>  <td>891.6073</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>68</td>    <td>-120.7852</td>   <td>0.9</td>   <td>-803.9748</td>  <td>562.4044</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>69</td>    <td>409.9089</td>    <td>0.9</td>   <td>-284.5313</td>  <td>1104.3492</td>  <td>False</td>
</tr>
<tr>
    <td>35</td>      <td>7</td>    <td>400.4264</td>    <td>0.9</td>   <td>-306.5986</td>  <td>1107.4514</td>  <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>70</td>    <td>-80.0404</td>    <td>0.9</td>   <td>-735.6229</td>   <td>575.542</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>71</td>    <td>122.8652</td>    <td>0.9</td>   <td>-521.5481</td>  <td>767.2785</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>72</td>    <td>265.0165</td>    <td>0.9</td>   <td>-398.8934</td>  <td>928.9265</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>73</td>    <td>-74.1943</td>    <td>0.9</td>   <td>-964.5792</td>  <td>816.1907</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>74</td>    <td>-176.8097</td>   <td>0.9</td>  <td>-1091.3287</td>  <td>737.7093</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>75</td>    <td>-202.6265</td>   <td>0.9</td>   <td>-837.2009</td>  <td>431.9478</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>76</td>     <td>25.1215</td>    <td>0.9</td>   <td>-634.5283</td>  <td>684.7713</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>     <td>77</td>    <td>-137.0321</td>   <td>0.9</td>   <td>-800.9421</td>  <td>526.8778</td>   <td>False</td>
</tr>
<tr>
    <td>35</td>      <td>8</td>    <td>684.2673</td>   <td>0.675</td>  <td>-230.2517</td>  <td>1598.7862</td>  <td>False</td>
</tr>
<tr>
    <td>35</td>      <td>9</td>    <td>1391.2057</td> <td>0.0294</td>   <td>45.0702</td>   <td>2737.3412</td>  <td>True</td> 
</tr>
<tr>
    <td>36</td>     <td>37</td>     <td>38.7505</td>    <td>0.9</td>  <td>-1217.0544</td>  <td>1294.5555</td>  <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>38</td>    <td>5780.2255</td>  <td>0.001</td>  <td>5014.6771</td>  <td>6545.774</td>   <td>True</td> 
</tr>
<tr>
    <td>36</td>     <td>39</td>    <td>-96.3299</td>    <td>0.9</td>   <td>-823.7304</td>  <td>631.0706</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>      <td>4</td>     <td>2.1239</td>     <td>0.9</td>   <td>-805.4217</td>  <td>809.6695</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>40</td>    <td>-34.7686</td>    <td>0.9</td>   <td>-708.5145</td>  <td>638.9773</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>41</td>    <td>-309.825</td>    <td>0.9</td>   <td>-967.0249</td>  <td>347.3749</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>42</td>    <td>-195.5851</td>   <td>0.9</td>   <td>-922.9856</td>  <td>531.8154</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>43</td>    <td>357.5209</td>    <td>0.9</td>   <td>-383.6683</td>  <td>1098.7101</td>  <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>44</td>    <td>-78.9335</td>    <td>0.9</td>   <td>-853.8054</td>  <td>695.9384</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>45</td>    <td>-130.509</td>    <td>0.9</td>   <td>-1037.158</td>   <td>776.14</td>    <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>46</td>    <td>-241.5606</td>   <td>0.9</td>   <td>-982.7498</td>  <td>499.6286</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>47</td>    <td>-261.5637</td>   <td>0.9</td>  <td>-1057.3363</td>  <td>534.2089</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>48</td>    <td>-211.9911</td>   <td>0.9</td>  <td>-1467.7961</td>  <td>1043.8138</td>  <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>49</td>    <td>-16.7352</td>    <td>0.9</td>   <td>-812.5078</td>  <td>779.0374</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>      <td>5</td>    <td>110.9989</td>    <td>0.9</td>   <td>-912.975</td>   <td>1134.9728</td>  <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>50</td>    <td>-118.1161</td>   <td>0.9</td>   <td>-1142.09</td>   <td>905.8578</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>51</td>    <td>540.9523</td>  <td>0.5353</td>  <td>-140.491</td>   <td>1222.3956</td>  <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>52</td>    <td>-365.7661</td>   <td>0.9</td>  <td>-1099.8471</td>  <td>368.3148</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>53</td>    <td>136.8908</td>    <td>0.9</td>   <td>-590.5097</td>  <td>864.2912</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>54</td>    <td>-326.8661</td>   <td>0.9</td>  <td>-1016.7613</td>   <td>363.029</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>55</td>    <td>122.1566</td>    <td>0.9</td>   <td>-582.0985</td>  <td>826.4117</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>56</td>    <td>433.3079</td>    <td>0.9</td>   <td>-210.3491</td>  <td>1076.9648</td>  <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>57</td>    <td>-129.6466</td>   <td>0.9</td>   <td>-904.5185</td>  <td>645.2253</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>58</td>    <td>-98.8522</td>    <td>0.9</td>   <td>-933.2224</td>  <td>735.5179</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>59</td>    <td>775.9993</td>   <td>0.001</td>  <td>137.0971</td>   <td>1414.9014</td>  <td>True</td> 
</tr>
<tr>
    <td>36</td>      <td>6</td>    <td>142.9672</td>    <td>0.9</td>   <td>-814.3163</td>  <td>1100.2507</td>  <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>60</td>    <td>468.6039</td>  <td>0.7369</td>  <td>-175.0531</td>  <td>1112.2608</td>  <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>61</td>     <td>96.9187</td>    <td>0.9</td>   <td>-677.9533</td>  <td>871.7906</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>62</td>    <td>507.1371</td>  <td>0.5824</td>  <td>-144.3343</td>  <td>1158.6084</td>  <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>63</td>    <td>571.8427</td>    <td>0.9</td>   <td>-277.9111</td>  <td>1421.5965</td>  <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>64</td>    <td>175.2459</td>    <td>0.9</td>   <td>-552.1545</td>  <td>902.6464</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>65</td>    <td>-52.2452</td>    <td>0.9</td>   <td>-767.4196</td>  <td>662.9292</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>66</td>    <td>-29.2411</td>    <td>0.9</td>  <td>-1145.8068</td>  <td>1087.3245</td>  <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>67</td>    <td>-212.9161</td>   <td>0.9</td>   <td>-1236.89</td>   <td>811.0578</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>68</td>    <td>-215.707</td>    <td>0.9</td>   <td>-919.9621</td>   <td>488.548</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>69</td>    <td>314.9871</td>    <td>0.9</td>   <td>-400.1873</td>  <td>1030.1615</td>  <td>False</td>
</tr>
<tr>
    <td>36</td>      <td>7</td>    <td>305.5046</td>    <td>0.9</td>   <td>-421.8959</td>  <td>1032.905</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>70</td>    <td>-174.9623</td>   <td>0.9</td>   <td>-852.4691</td>  <td>502.5445</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>71</td>     <td>27.9434</td>    <td>0.9</td>   <td>-638.7617</td>  <td>694.6484</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>72</td>    <td>170.0947</td>    <td>0.9</td>   <td>-515.4733</td>  <td>855.6627</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>73</td>    <td>-169.1161</td>   <td>0.9</td>  <td>-1075.7651</td>  <td>737.5329</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>74</td>    <td>-271.7315</td>   <td>0.9</td>  <td>-1202.0928</td>  <td>658.6297</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>75</td>    <td>-297.5484</td>   <td>0.9</td>   <td>-954.7483</td>  <td>359.6516</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>76</td>    <td>-69.8003</td>    <td>0.9</td>   <td>-751.2436</td>  <td>611.6429</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>     <td>77</td>    <td>-231.954</td>    <td>0.9</td>   <td>-917.522</td>   <td>453.6141</td>   <td>False</td>
</tr>
<tr>
    <td>36</td>      <td>8</td>    <td>589.3454</td>    <td>0.9</td>   <td>-341.0159</td>  <td>1519.7067</td>  <td>False</td>
</tr>
<tr>
    <td>36</td>      <td>9</td>    <td>1296.2839</td> <td>0.0961</td>  <td>-60.6641</td>   <td>2653.2319</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>38</td>    <td>5741.475</td>   <td>0.001</td>  <td>4456.315</td>   <td>7026.635</td>   <td>True</td> 
</tr>
<tr>
    <td>37</td>     <td>39</td>    <td>-135.0805</td>   <td>0.9</td>  <td>-1397.8881</td>  <td>1127.7272</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>      <td>4</td>    <td>-36.6267</td>    <td>0.9</td>  <td>-1347.2378</td>  <td>1273.9845</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>40</td>    <td>-73.5192</td>    <td>0.9</td>  <td>-1306.2013</td>  <td>1159.163</td>   <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>41</td>    <td>-348.5756</td>   <td>0.9</td>  <td>-1572.2926</td>  <td>875.1415</td>   <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>42</td>    <td>-234.3356</td>   <td>0.9</td>  <td>-1497.1433</td>  <td>1028.472</td>   <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>43</td>    <td>318.7704</td>    <td>0.9</td>   <td>-952.0298</td>  <td>1589.5705</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>44</td>    <td>-117.6841</td>   <td>0.9</td>  <td>-1408.4196</td>  <td>1173.0515</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>45</td>    <td>-169.2595</td>   <td>0.9</td>  <td>-1543.1533</td>  <td>1204.6343</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>46</td>    <td>-280.3111</td>   <td>0.9</td>  <td>-1551.1113</td>  <td>990.4891</td>   <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>47</td>    <td>-300.3143</td>   <td>0.9</td>  <td>-1603.7044</td>  <td>1003.0758</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>48</td>    <td>-250.7417</td>   <td>0.9</td>  <td>-1876.3547</td>  <td>1374.8714</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>49</td>    <td>-55.4857</td>    <td>0.9</td>  <td>-1358.8758</td>  <td>1247.9044</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>      <td>5</td>     <td>72.2483</td>    <td>0.9</td>  <td>-1381.7442</td>  <td>1526.2408</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>50</td>    <td>-156.8667</td>   <td>0.9</td>  <td>-1610.8592</td>  <td>1297.1258</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>51</td>    <td>502.2018</td>    <td>0.9</td>   <td>-734.7043</td>  <td>1739.1078</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>52</td>    <td>-404.5167</td>   <td>0.9</td>  <td>-1671.1841</td>  <td>862.1508</td>   <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>53</td>     <td>98.1402</td>    <td>0.9</td>  <td>-1164.6674</td>  <td>1360.9479</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>54</td>    <td>-365.6167</td>   <td>0.9</td>  <td>-1607.1991</td>  <td>875.9658</td>   <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>55</td>     <td>83.4061</td>    <td>0.9</td>  <td>-1166.2126</td>  <td>1333.0248</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>56</td>    <td>394.5573</td>    <td>0.9</td>   <td>-821.9401</td>  <td>1611.0547</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>57</td>    <td>-168.3971</td>   <td>0.9</td>  <td>-1459.1326</td>  <td>1122.3384</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>58</td>    <td>-137.6028</td>   <td>0.9</td>  <td>-1464.9103</td>  <td>1189.7047</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>59</td>    <td>737.2487</td>    <td>0.9</td>   <td>-476.7396</td>  <td>1951.237</td>   <td>False</td>
</tr>
<tr>
    <td>37</td>      <td>6</td>    <td>104.2167</td>    <td>0.9</td>  <td>-1303.6055</td>  <td>1512.0389</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>60</td>    <td>429.8533</td>    <td>0.9</td>   <td>-786.6441</td>  <td>1646.3507</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>61</td>     <td>58.1681</td>    <td>0.9</td>  <td>-1232.5674</td>  <td>1348.9036</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>62</td>    <td>468.3865</td>    <td>0.9</td>   <td>-752.2636</td>  <td>1689.0366</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>63</td>    <td>533.0922</td>    <td>0.9</td>   <td>-803.9393</td>  <td>1870.1236</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>64</td>    <td>136.4954</td>    <td>0.9</td>  <td>-1126.3122</td>  <td>1399.303</td>   <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>65</td>    <td>-90.9957</td>    <td>0.9</td>  <td>-1346.8007</td>  <td>1164.8093</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>66</td>    <td>-67.9917</td>    <td>0.9</td>  <td>-1588.6134</td>  <td>1452.6301</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>67</td>    <td>-251.6667</td>   <td>0.9</td>  <td>-1705.6592</td>  <td>1202.3258</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>68</td>    <td>-254.4576</td>   <td>0.9</td>  <td>-1504.0763</td>  <td>995.1611</td>   <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>69</td>    <td>276.2366</td>    <td>0.9</td>   <td>-979.5684</td>  <td>1532.0415</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>      <td>7</td>     <td>266.754</td>    <td>0.9</td>   <td>-996.0536</td>  <td>1529.5617</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>70</td>    <td>-213.7128</td>   <td>0.9</td>  <td>-1448.4546</td>  <td>1021.0289</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>71</td>    <td>-10.8071</td>    <td>0.9</td>  <td>-1239.6551</td>  <td>1218.0408</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>72</td>    <td>131.3441</td>    <td>0.9</td>  <td>-1107.8391</td>  <td>1370.5274</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>73</td>    <td>-207.8667</td>   <td>0.9</td>  <td>-1581.7605</td>  <td>1166.0271</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>74</td>    <td>-310.4821</td>   <td>0.9</td>   <td>-1700.138</td>  <td>1079.1739</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>75</td>    <td>-336.2989</td>   <td>0.9</td>  <td>-1560.0159</td>  <td>887.4182</td>   <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>76</td>    <td>-108.5509</td>   <td>0.9</td>  <td>-1345.4569</td>  <td>1128.3552</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>     <td>77</td>    <td>-270.7045</td>   <td>0.9</td>  <td>-1509.8878</td>  <td>968.4788</td>   <td>False</td>
</tr>
<tr>
    <td>37</td>      <td>8</td>    <td>550.5949</td>    <td>0.9</td>   <td>-839.0611</td>  <td>1940.2509</td>  <td>False</td>
</tr>
<tr>
    <td>37</td>      <td>9</td>    <td>1257.5333</td> <td>0.7076</td>  <td>-447.424</td>   <td>2962.4907</td>  <td>False</td>
</tr>
<tr>
    <td>38</td>     <td>39</td>   <td>-5876.5555</td>  <td>0.001</td> <td>-6653.5377</td> <td>-5099.5732</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>      <td>4</td>   <td>-5778.1017</td>  <td>0.001</td> <td>-6630.5803</td>  <td>-4925.623</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>40</td>   <td>-5814.9942</td>  <td>0.001</td> <td>-6541.9904</td> <td>-5087.9979</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>41</td>   <td>-6090.0506</td>  <td>0.001</td> <td>-6801.7399</td> <td>-5378.3612</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>42</td>   <td>-5975.8106</td>  <td>0.001</td> <td>-6752.7929</td> <td>-5198.8283</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>43</td>   <td>-5422.7046</td>  <td>0.001</td> <td>-6212.6106</td> <td>-4632.7987</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>44</td>   <td>-5859.1591</td>  <td>0.001</td> <td>-6680.7529</td> <td>-5037.5652</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>45</td>   <td>-5910.7345</td>  <td>0.001</td> <td>-6857.6255</td> <td>-4963.8436</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>46</td>   <td>-6021.7861</td>  <td>0.001</td> <td>-6811.6921</td> <td>-5231.8802</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>47</td>   <td>-6041.7893</td>  <td>0.001</td>  <td>-6883.124</td> <td>-5200.4546</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>48</td>   <td>-5992.2167</td>  <td>0.001</td> <td>-7277.3766</td> <td>-4707.0567</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>49</td>   <td>-5796.9607</td>  <td>0.001</td> <td>-6638.2954</td>  <td>-4955.626</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>      <td>5</td>   <td>-5669.2267</td>  <td>0.001</td> <td>-6728.9967</td> <td>-4609.4566</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>50</td>   <td>-5898.3417</td>  <td>0.001</td> <td>-6958.1117</td> <td>-4838.5716</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>51</td>   <td>-5239.2732</td>  <td>0.001</td> <td>-5973.4088</td> <td>-4505.1377</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>52</td>   <td>-6145.9917</td>  <td>0.001</td> <td>-6929.2316</td> <td>-5362.7517</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>53</td>   <td>-5643.3348</td>  <td>0.001</td> <td>-6420.3171</td> <td>-4866.3525</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>54</td>   <td>-6107.0917</td>  <td>0.001</td> <td>-6849.0791</td> <td>-5365.1042</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>55</td>   <td>-5658.0689</td>  <td>0.001</td> <td>-6413.4266</td> <td>-4902.7113</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>56</td>   <td>-5346.9177</td>  <td>0.001</td> <td>-6046.1203</td> <td>-4647.7151</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>57</td>   <td>-5909.8721</td>  <td>0.001</td>  <td>-6731.466</td> <td>-5088.2782</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>58</td>   <td>-5879.0778</td>  <td>0.001</td> <td>-6757.0092</td> <td>-5001.1464</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>59</td>   <td>-5004.2263</td>  <td>0.001</td> <td>-5699.0543</td> <td>-4309.3983</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>      <td>6</td>   <td>-5637.2583</td>  <td>0.001</td>  <td>-6632.739</td> <td>-4641.7777</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>60</td>   <td>-5311.6217</td>  <td>0.001</td> <td>-6010.8243</td> <td>-4612.4191</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>61</td>   <td>-5683.3069</td>  <td>0.001</td> <td>-6504.9008</td>  <td>-4861.713</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>62</td>   <td>-5273.0885</td>  <td>0.001</td> <td>-5979.4913</td> <td>-4566.6856</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>63</td>   <td>-5208.3828</td>  <td>0.001</td> <td>-6100.9474</td> <td>-4315.8183</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>64</td>   <td>-5604.9796</td>  <td>0.001</td> <td>-6381.9619</td> <td>-4827.9973</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>65</td>   <td>-5832.4707</td>  <td>0.001</td> <td>-6598.0191</td> <td>-5066.9223</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>66</td>   <td>-5809.4667</td>  <td>0.001</td> <td>-6958.9487</td> <td>-4659.9847</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>67</td>   <td>-5993.1417</td>  <td>0.001</td> <td>-7052.9117</td> <td>-4933.3716</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>68</td>   <td>-5995.9326</td>  <td>0.001</td> <td>-6751.2902</td> <td>-5240.5749</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>69</td>   <td>-5465.2384</td>  <td>0.001</td> <td>-6230.7869</td>  <td>-4699.69</td>   <td>True</td> 
</tr>
<tr>
    <td>38</td>      <td>7</td>    <td>-5474.721</td>  <td>0.001</td> <td>-6251.7033</td> <td>-4697.7387</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>70</td>   <td>-5955.1878</td>  <td>0.001</td> <td>-6685.6709</td> <td>-5224.7048</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>71</td>   <td>-5752.2821</td>  <td>0.001</td> <td>-6472.7581</td> <td>-5031.8062</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>72</td>   <td>-5610.1309</td>  <td>0.001</td> <td>-6348.0967</td> <td>-4872.1651</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>73</td>   <td>-5949.3417</td>  <td>0.001</td> <td>-6896.2326</td> <td>-5002.4507</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>74</td>   <td>-6051.9571</td>  <td>0.001</td> <td>-7021.5766</td> <td>-5082.3375</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>75</td>   <td>-6077.7739</td>  <td>0.001</td> <td>-6789.4632</td> <td>-5366.0845</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>76</td>   <td>-5850.0259</td>  <td>0.001</td> <td>-6584.1614</td> <td>-5115.8904</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>     <td>77</td>   <td>-6012.1795</td>  <td>0.001</td> <td>-6750.1453</td> <td>-5274.2137</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>      <td>8</td>   <td>-5190.8801</td>  <td>0.001</td> <td>-6160.4997</td> <td>-4221.2606</td>  <td>True</td> 
</tr>
<tr>
    <td>38</td>      <td>9</td>   <td>-4483.9417</td>  <td>0.001</td> <td>-5868.1013</td>  <td>-3099.782</td>  <td>True</td> 
</tr>
<tr>
    <td>39</td>      <td>4</td>     <td>98.4538</td>    <td>0.9</td>   <td>-719.9391</td>  <td>916.8467</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>40</td>     <td>61.5613</td>    <td>0.9</td>   <td>-625.1487</td>  <td>748.2713</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>41</td>    <td>-213.4951</td>   <td>0.9</td>   <td>-883.9791</td>  <td>456.9889</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>42</td>    <td>-99.2552</td>    <td>0.9</td>   <td>-838.6796</td>  <td>640.1693</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>43</td>    <td>453.8508</td>    <td>0.9</td>   <td>-299.1422</td>  <td>1206.8438</td>  <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>44</td>     <td>17.3964</td>    <td>0.9</td>   <td>-768.7738</td>  <td>803.5666</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>45</td>    <td>-34.1791</td>    <td>0.9</td>   <td>-950.503</td>   <td>882.1448</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>46</td>    <td>-145.2307</td>   <td>0.9</td>   <td>-898.2236</td>  <td>607.7623</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>47</td>    <td>-165.2338</td>   <td>0.9</td>   <td>-972.012</td>   <td>641.5444</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>48</td>    <td>-115.6612</td>   <td>0.9</td>  <td>-1378.4688</td>  <td>1147.1464</td>  <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>49</td>     <td>79.5947</td>    <td>0.9</td>   <td>-727.1835</td>   <td>886.373</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>      <td>5</td>    <td>207.3288</td>    <td>0.9</td>   <td>-825.2212</td>  <td>1239.8788</td>  <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>50</td>    <td>-21.7862</td>    <td>0.9</td>  <td>-1054.3362</td>  <td>1010.7638</td>  <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>51</td>    <td>637.2822</td>  <td>0.1587</td>  <td>-56.9814</td>   <td>1331.5458</td>  <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>52</td>    <td>-269.4362</td>   <td>0.9</td>  <td>-1015.4334</td>   <td>476.561</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>53</td>    <td>233.2207</td>    <td>0.9</td>   <td>-506.2038</td>  <td>972.6451</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>54</td>    <td>-230.5362</td>   <td>0.9</td>   <td>-933.0975</td>  <td>472.0251</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>55</td>    <td>218.4865</td>    <td>0.9</td>   <td>-498.1809</td>   <td>935.154</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>56</td>    <td>529.6378</td>  <td>0.4984</td>  <td>-127.577</td>   <td>1186.8526</td>  <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>57</td>    <td>-33.3166</td>    <td>0.9</td>   <td>-819.4868</td>  <td>752.8535</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>58</td>     <td>-2.5223</td>    <td>0.9</td>   <td>-847.3954</td>  <td>842.3508</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>59</td>    <td>872.3292</td>   <td>0.001</td>  <td>219.7704</td>   <td>1524.888</td>   <td>True</td> 
</tr>
<tr>
    <td>39</td>      <td>6</td>    <td>239.2971</td>    <td>0.9</td>   <td>-727.1545</td>  <td>1205.7487</td>  <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>60</td>    <td>564.9338</td>  <td>0.3086</td>   <td>-92.281</td>   <td>1222.1486</td>  <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>61</td>    <td>193.2486</td>    <td>0.9</td>   <td>-592.9216</td>  <td>979.4187</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>62</td>     <td>603.467</td>  <td>0.1793</td>  <td>-61.4029</td>   <td>1268.3369</td>  <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>63</td>    <td>668.1726</td>  <td>0.5872</td>  <td>-191.8963</td>  <td>1528.2415</td>  <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>64</td>    <td>271.5759</td>    <td>0.9</td>   <td>-467.8486</td>  <td>1011.0003</td>  <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>65</td>     <td>44.0848</td>    <td>0.9</td>   <td>-683.3157</td>  <td>771.4852</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>66</td>     <td>67.0888</td>    <td>0.9</td>   <td>-1057.347</td>  <td>1191.5246</td>  <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>67</td>    <td>-116.5862</td>   <td>0.9</td>  <td>-1149.1362</td>  <td>915.9638</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>68</td>    <td>-119.3771</td>   <td>0.9</td>   <td>-836.0446</td>  <td>597.2903</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>69</td>     <td>411.317</td>    <td>0.9</td>   <td>-316.0835</td>  <td>1138.7175</td>  <td>False</td>
</tr>
<tr>
    <td>39</td>      <td>7</td>    <td>401.8345</td>    <td>0.9</td>    <td>-337.59</td>   <td>1141.2589</td>  <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>70</td>    <td>-78.6324</td>    <td>0.9</td>   <td>-769.0326</td>  <td>611.7679</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>71</td>    <td>124.2733</td>    <td>0.9</td>   <td>-555.5301</td>  <td>804.0767</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>72</td>    <td>266.4246</td>    <td>0.9</td>   <td>-431.888</td>   <td>964.7373</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>73</td>    <td>-72.7862</td>    <td>0.9</td>   <td>-989.1101</td>  <td>843.5377</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>74</td>    <td>-175.4016</td>   <td>0.9</td>  <td>-1115.1937</td>  <td>764.3905</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>75</td>    <td>-201.2184</td>   <td>0.9</td>   <td>-871.7024</td>  <td>469.2656</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>76</td>     <td>26.5296</td>    <td>0.9</td>   <td>-667.734</td>   <td>720.7932</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>     <td>77</td>    <td>-135.624</td>    <td>0.9</td>   <td>-833.9367</td>  <td>562.6886</td>   <td>False</td>
</tr>
<tr>
    <td>39</td>      <td>8</td>    <td>685.6753</td>   <td>0.732</td>  <td>-254.1167</td>  <td>1625.4674</td>  <td>False</td>
</tr>
<tr>
    <td>39</td>      <td>9</td>    <td>1392.6138</td> <td>0.0359</td>   <td>29.1825</td>   <td>2756.0451</td>  <td>True</td> 
</tr>
<tr>
     <td>4</td>     <td>40</td>    <td>-36.8925</td>    <td>0.9</td>   <td>-807.9885</td>  <td>734.2035</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>41</td>    <td>-311.9489</td>   <td>0.9</td>  <td>-1068.6306</td>  <td>444.7328</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>42</td>    <td>-197.709</td>    <td>0.9</td>  <td>-1016.1019</td>  <td>620.6839</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>43</td>     <td>355.397</td>    <td>0.9</td>   <td>-475.2755</td>  <td>1186.0696</td>  <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>44</td>    <td>-81.0574</td>    <td>0.9</td>   <td>-941.9186</td>  <td>779.8038</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>45</td>    <td>-132.6329</td>   <td>0.9</td>  <td>-1113.7893</td>  <td>848.5236</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>46</td>    <td>-243.6844</td>   <td>0.9</td>   <td>-1074.357</td>  <td>586.9881</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>47</td>    <td>-263.6876</td>   <td>0.9</td>  <td>-1143.4089</td>  <td>616.0336</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>48</td>    <td>-214.115</td>    <td>0.9</td>  <td>-1524.7261</td>  <td>1096.4961</td>  <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>49</td>     <td>-18.859</td>    <td>0.9</td>   <td>-898.5803</td>  <td>860.8622</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>      <td>5</td>     <td>108.875</td>    <td>0.9</td>   <td>-981.6194</td>  <td>1199.3694</td>  <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>50</td>     <td>-120.24</td>    <td>0.9</td>  <td>-1210.7344</td>  <td>970.2544</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>51</td>    <td>538.8284</td>   <td>0.845</td>  <td>-239.0021</td>  <td>1316.659</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>52</td>     <td>-367.89</td>    <td>0.9</td>  <td>-1192.2263</td>  <td>456.4463</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>53</td>    <td>134.7669</td>    <td>0.9</td>   <td>-683.626</td>   <td>953.1598</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>54</td>     <td>-328.99</td>    <td>0.9</td>  <td>-1114.2357</td>  <td>456.2557</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>55</td>    <td>120.0327</td>    <td>0.9</td>   <td>-677.8586</td>  <td>917.9241</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>56</td>     <td>431.184</td>    <td>0.9</td>   <td>-313.7655</td>  <td>1176.1335</td>  <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>57</td>    <td>-131.7704</td>   <td>0.9</td>   <td>-992.6316</td>  <td>729.0907</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>58</td>    <td>-100.9761</td>   <td>0.9</td>  <td>-1015.7597</td>  <td>813.8074</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>59</td>    <td>773.8754</td>  <td>0.0244</td>   <td>33.0303</td>   <td>1514.7204</td>  <td>True</td> 
</tr>
<tr>
     <td>4</td>      <td>6</td>    <td>140.8433</td>    <td>0.9</td>   <td>-887.2846</td>  <td>1168.9713</td>  <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>60</td>     <td>466.48</td>     <td>0.9</td>   <td>-278.4695</td>  <td>1211.4295</td>  <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>61</td>     <td>94.7948</td>    <td>0.9</td>   <td>-766.0664</td>  <td>955.6559</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>62</td>    <td>505.0132</td>    <td>0.9</td>   <td>-246.6985</td>  <td>1256.7248</td>  <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>63</td>    <td>569.7188</td>    <td>0.9</td>   <td>-359.1175</td>  <td>1498.5552</td>  <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>64</td>    <td>173.1221</td>    <td>0.9</td>   <td>-645.2708</td>   <td>991.515</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>65</td>     <td>-54.369</td>    <td>0.9</td>   <td>-861.9146</td>  <td>753.1766</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>66</td>     <td>-31.365</td>    <td>0.9</td>  <td>-1209.2336</td>  <td>1146.5036</td>  <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>67</td>     <td>-215.04</td>    <td>0.9</td>  <td>-1305.5344</td>  <td>875.4544</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>68</td>    <td>-217.8309</td>   <td>0.9</td>  <td>-1015.7223</td>  <td>580.0605</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>69</td>    <td>312.8632</td>    <td>0.9</td>   <td>-494.6824</td>  <td>1120.4088</td>  <td>False</td>
</tr>
<tr>
     <td>4</td>      <td>7</td>    <td>303.3807</td>    <td>0.9</td>   <td>-515.0122</td>  <td>1121.7736</td>  <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>70</td>    <td>-177.0862</td>   <td>0.9</td>   <td>-951.4704</td>  <td>597.2981</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>71</td>     <td>25.8195</td>    <td>0.9</td>   <td>-739.1322</td>  <td>790.7712</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>72</td>    <td>167.9708</td>    <td>0.9</td>   <td>-613.4759</td>  <td>949.4175</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>73</td>     <td>-171.24</td>    <td>0.9</td>  <td>-1152.3964</td>  <td>809.9164</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>74</td>    <td>-273.8554</td>   <td>0.9</td>  <td>-1276.9643</td>  <td>729.2536</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>75</td>    <td>-299.6722</td>   <td>0.9</td>  <td>-1056.3539</td>  <td>457.0095</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>76</td>    <td>-71.9242</td>    <td>0.9</td>   <td>-849.7548</td>  <td>705.9064</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>     <td>77</td>    <td>-234.0778</td>   <td>0.9</td>  <td>-1015.5246</td>  <td>547.3689</td>   <td>False</td>
</tr>
<tr>
     <td>4</td>      <td>8</td>    <td>587.2215</td>    <td>0.9</td>   <td>-415.8874</td>  <td>1590.3305</td>  <td>False</td>
</tr>
<tr>
     <td>4</td>      <td>9</td>     <td>1294.16</td>   <td>0.156</td>  <td>-113.6622</td>  <td>2701.9822</td>  <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>41</td>    <td>-275.0564</td>   <td>0.9</td>   <td>-886.9149</td>  <td>336.8021</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>42</td>    <td>-160.8165</td>   <td>0.9</td>   <td>-847.5264</td>  <td>525.8935</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>43</td>    <td>392.2895</td>    <td>0.9</td>   <td>-309.0096</td>  <td>1093.5887</td>  <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>44</td>    <td>-44.1649</td>    <td>0.9</td>   <td>-780.9726</td>  <td>692.6428</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>45</td>    <td>-95.7404</td>    <td>0.9</td>   <td>-970.081</td>   <td>778.6003</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>46</td>    <td>-206.7919</td>   <td>0.9</td>   <td>-908.0911</td>  <td>494.5072</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>47</td>    <td>-226.7951</td>   <td>0.9</td>   <td>-985.5528</td>  <td>531.9625</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>48</td>    <td>-177.2225</td>   <td>0.9</td>  <td>-1409.9046</td>  <td>1055.4596</td>  <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>49</td>     <td>18.0335</td>    <td>0.9</td>   <td>-740.7242</td>  <td>776.7911</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>      <td>5</td>    <td>145.7675</td>    <td>0.9</td>   <td>-849.7131</td>  <td>1141.2481</td>  <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>50</td>    <td>-83.3475</td>    <td>0.9</td>  <td>-1078.8281</td>  <td>912.1331</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>51</td>    <td>575.7209</td>  <td>0.1908</td>  <td>-62.1067</td>   <td>1213.5485</td>  <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>52</td>    <td>-330.9975</td>   <td>0.9</td>  <td>-1024.7799</td>  <td>362.7849</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>53</td>    <td>171.6594</td>    <td>0.9</td>   <td>-515.0506</td>  <td>858.3694</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>54</td>    <td>-292.0975</td>   <td>0.9</td>   <td>-938.9472</td>  <td>354.7522</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>55</td>    <td>156.9252</td>    <td>0.9</td>   <td>-505.2185</td>   <td>819.069</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>56</td>    <td>468.0765</td>  <td>0.5664</td>  <td>-129.2119</td>  <td>1065.3649</td>  <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>57</td>    <td>-94.8779</td>    <td>0.9</td>   <td>-831.6856</td>  <td>641.9298</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>58</td>    <td>-64.0836</td>    <td>0.9</td>   <td>-863.2285</td>  <td>735.0613</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>59</td>    <td>810.7679</td>   <td>0.001</td>  <td>218.6065</td>   <td>1402.9292</td>  <td>True</td> 
</tr>
<tr>
    <td>40</td>      <td>6</td>    <td>177.7358</td>    <td>0.9</td>   <td>-749.0062</td>  <td>1104.4779</td>  <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>60</td>    <td>503.3725</td>  <td>0.3671</td>  <td>-93.9159</td>   <td>1100.6609</td>  <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>61</td>    <td>131.6873</td>    <td>0.9</td>   <td>-605.1204</td>   <td>868.495</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>62</td>    <td>541.9057</td>  <td>0.2101</td>  <td>-63.7956</td>   <td>1147.607</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>63</td>    <td>606.6113</td>  <td>0.6875</td>  <td>-208.5823</td>  <td>1421.8049</td>  <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>64</td>    <td>210.0146</td>    <td>0.9</td>   <td>-476.6954</td>  <td>896.7245</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>65</td>    <td>-17.4765</td>    <td>0.9</td>   <td>-691.2224</td>  <td>656.2694</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>66</td>     <td>5.5275</td>     <td>0.9</td>  <td>-1084.9669</td>  <td>1096.0219</td>  <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>67</td>    <td>-178.1475</td>   <td>0.9</td>  <td>-1173.6281</td>  <td>817.3331</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>68</td>    <td>-180.9384</td>   <td>0.9</td>   <td>-843.0821</td>  <td>481.2053</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>69</td>    <td>349.7557</td>    <td>0.9</td>   <td>-323.9902</td>  <td>1023.5016</td>  <td>False</td>
</tr>
<tr>
    <td>40</td>      <td>7</td>    <td>340.2732</td>    <td>0.9</td>   <td>-346.4368</td>  <td>1026.9832</td>  <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>70</td>    <td>-140.1937</td>   <td>0.9</td>   <td>-773.8139</td>  <td>493.4266</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>71</td>     <td>62.712</td>     <td>0.9</td>   <td>-559.3448</td>  <td>684.7689</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>72</td>    <td>204.8633</td>    <td>0.9</td>   <td>-437.3692</td>  <td>847.0959</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>73</td>    <td>-134.3475</td>   <td>0.9</td>  <td>-1008.6881</td>  <td>739.9931</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>74</td>    <td>-236.9629</td>   <td>0.9</td>  <td>-1135.8684</td>  <td>661.9427</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>75</td>    <td>-262.7797</td>   <td>0.9</td>   <td>-874.6382</td>  <td>349.0788</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>76</td>    <td>-35.0317</td>    <td>0.9</td>   <td>-672.8593</td>  <td>602.7959</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>     <td>77</td>    <td>-197.1853</td>   <td>0.9</td>   <td>-839.4179</td>  <td>445.0472</td>   <td>False</td>
</tr>
<tr>
    <td>40</td>      <td>8</td>     <td>624.114</td>  <td>0.8402</td>  <td>-274.7915</td>  <td>1523.0196</td>  <td>False</td>
</tr>
<tr>
    <td>40</td>      <td>9</td>    <td>1331.0525</td> <td>0.0528</td>   <td>-4.5249</td>   <td>2666.6299</td>  <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>42</td>    <td>114.2399</td>    <td>0.9</td>   <td>-556.2441</td>  <td>784.7239</td>   <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>43</td>    <td>667.3459</td>  <td>0.0754</td>  <td>-18.0727</td>   <td>1352.7646</td>  <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>44</td>    <td>230.8915</td>    <td>0.9</td>   <td>-490.8174</td>  <td>952.6004</td>   <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>45</td>     <td>179.316</td>    <td>0.9</td>   <td>-682.3392</td>  <td>1040.9713</td>  <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>46</td>     <td>68.2644</td>    <td>0.9</td>   <td>-617.1542</td>  <td>753.6831</td>   <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>47</td>     <td>48.2613</td>    <td>0.9</td>   <td>-695.8431</td>  <td>792.3657</td>   <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>48</td>     <td>97.8339</td>    <td>0.9</td>  <td>-1125.8832</td>  <td>1321.5509</td>  <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>49</td>    <td>293.0898</td>    <td>0.9</td>   <td>-451.0145</td>  <td>1037.1942</td>  <td>False</td>
</tr>
<tr>
    <td>41</td>      <td>5</td>    <td>420.8239</td>    <td>0.9</td>   <td>-563.5337</td>  <td>1405.1815</td>  <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>50</td>    <td>191.7089</td>    <td>0.9</td>   <td>-792.6487</td>  <td>1176.0665</td>  <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>51</td>    <td>850.7773</td>   <td>0.001</td>   <td>230.453</td>   <td>1471.1016</td>  <td>True</td> 
</tr>
<tr>
    <td>41</td>     <td>52</td>    <td>-55.9411</td>    <td>0.9</td>   <td>-733.6668</td>  <td>621.7846</td>   <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>53</td>    <td>446.7158</td>    <td>0.9</td>   <td>-223.7682</td>  <td>1117.1998</td>  <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>54</td>    <td>-17.0411</td>    <td>0.9</td>   <td>-646.6383</td>  <td>612.5561</td>   <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>55</td>    <td>431.9816</td>    <td>0.9</td>   <td>-213.3187</td>  <td>1077.2819</td>  <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>56</td>    <td>743.1329</td>   <td>0.001</td>   <td>164.573</td>   <td>1321.6928</td>  <td>True</td> 
</tr>
<tr>
    <td>41</td>     <td>57</td>    <td>180.1785</td>    <td>0.9</td>   <td>-541.5305</td>  <td>901.8874</td>   <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>58</td>    <td>210.9728</td>    <td>0.9</td>   <td>-574.2729</td>  <td>996.2185</td>   <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>59</td>    <td>1085.8243</td>  <td>0.001</td>  <td>512.5589</td>   <td>1659.0897</td>  <td>True</td> 
</tr>
<tr>
    <td>41</td>      <td>6</td>    <td>452.7922</td>    <td>0.9</td>   <td>-461.9913</td>  <td>1367.5758</td>  <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>60</td>    <td>778.4289</td>   <td>0.001</td>   <td>199.869</td>   <td>1356.9888</td>  <td>True</td> 
</tr>
<tr>
    <td>41</td>     <td>61</td>    <td>406.7437</td>    <td>0.9</td>   <td>-314.9653</td>  <td>1128.4526</td>  <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>62</td>    <td>816.9621</td>   <td>0.001</td>  <td>229.7209</td>   <td>1404.2033</td>  <td>True</td> 
</tr>
<tr>
    <td>41</td>     <td>63</td>    <td>881.6677</td>  <td>0.0093</td>   <td>80.095</td>    <td>1683.2404</td>  <td>True</td> 
</tr>
<tr>
    <td>41</td>     <td>64</td>     <td>485.071</td>  <td>0.7509</td>  <td>-185.413</td>   <td>1155.5549</td>  <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>65</td>    <td>257.5799</td>    <td>0.9</td>   <td>-399.6201</td>  <td>914.7798</td>   <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>66</td>    <td>280.5839</td>    <td>0.9</td>   <td>-799.7661</td>  <td>1360.9339</td>  <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>67</td>     <td>96.9089</td>    <td>0.9</td>   <td>-887.4487</td>  <td>1081.2665</td>  <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>68</td>     <td>94.118</td>     <td>0.9</td>   <td>-551.1823</td>  <td>739.4183</td>   <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>69</td>    <td>624.8121</td>  <td>0.1029</td>  <td>-32.3878</td>   <td>1282.012</td>   <td>False</td>
</tr>
<tr>
    <td>41</td>      <td>7</td>    <td>615.3296</td>  <td>0.1591</td>  <td>-55.1544</td>   <td>1285.8136</td>  <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>70</td>    <td>134.8627</td>    <td>0.9</td>   <td>-481.1347</td>  <td>750.8601</td>   <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>71</td>    <td>337.7684</td>    <td>0.9</td>   <td>-266.3284</td>  <td>941.8652</td>   <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>72</td>    <td>479.9197</td>  <td>0.6142</td>  <td>-144.9329</td>  <td>1104.7723</td>  <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>73</td>    <td>140.7089</td>    <td>0.9</td>   <td>-720.9464</td>  <td>1002.3641</td>  <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>74</td>     <td>38.0935</td>    <td>0.9</td>   <td>-848.4782</td>  <td>924.6652</td>   <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>75</td>     <td>12.2767</td>    <td>0.9</td>   <td>-581.3133</td>  <td>605.8666</td>   <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>76</td>    <td>240.0247</td>    <td>0.9</td>   <td>-380.2996</td>   <td>860.349</td>   <td>False</td>
</tr>
<tr>
    <td>41</td>     <td>77</td>     <td>77.8711</td>    <td>0.9</td>   <td>-546.9816</td>  <td>702.7237</td>   <td>False</td>
</tr>
<tr>
    <td>41</td>      <td>8</td>    <td>899.1704</td>  <td>0.0403</td>   <td>12.5987</td>   <td>1785.7421</td>  <td>True</td> 
</tr>
<tr>
    <td>41</td>      <td>9</td>    <td>1606.1089</td> <td>0.0011</td>  <td>278.8014</td>   <td>2933.4164</td>  <td>True</td> 
</tr>
<tr>
    <td>42</td>     <td>43</td>     <td>553.106</td>  <td>0.7169</td>  <td>-199.887</td>   <td>1306.099</td>   <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>44</td>    <td>116.6516</td>    <td>0.9</td>   <td>-669.5186</td>  <td>902.8217</td>   <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>45</td>     <td>65.0761</td>    <td>0.9</td>   <td>-851.2478</td>    <td>981.4</td>    <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>46</td>    <td>-45.9755</td>    <td>0.9</td>   <td>-798.9685</td>  <td>707.0175</td>   <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>47</td>    <td>-65.9787</td>    <td>0.9</td>   <td>-872.7569</td>  <td>740.7996</td>   <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>48</td>     <td>-16.406</td>    <td>0.9</td>  <td>-1279.2137</td>  <td>1246.4016</td>  <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>49</td>    <td>178.8499</td>    <td>0.9</td>   <td>-627.9283</td>  <td>985.6281</td>   <td>False</td>
</tr>
<tr>
    <td>42</td>      <td>5</td>     <td>306.584</td>    <td>0.9</td>   <td>-725.9661</td>  <td>1339.134</td>   <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>50</td>     <td>77.469</td>     <td>0.9</td>   <td>-955.0811</td>  <td>1110.019</td>   <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>51</td>    <td>736.5374</td>  <td>0.0186</td>   <td>42.2738</td>   <td>1430.801</td>   <td>True</td> 
</tr>
<tr>
    <td>42</td>     <td>52</td>    <td>-170.181</td>    <td>0.9</td>   <td>-916.1783</td>  <td>575.8162</td>   <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>53</td>    <td>332.4759</td>    <td>0.9</td>   <td>-406.9486</td>  <td>1071.9003</td>  <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>54</td>    <td>-131.281</td>    <td>0.9</td>   <td>-833.8423</td>  <td>571.2803</td>   <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>55</td>    <td>317.7417</td>    <td>0.9</td>   <td>-398.9258</td>  <td>1034.4091</td>  <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>56</td>     <td>628.893</td>  <td>0.0938</td>  <td>-28.3219</td>   <td>1286.1078</td>  <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>57</td>     <td>65.9385</td>    <td>0.9</td>   <td>-720.2316</td>  <td>852.1087</td>   <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>58</td>     <td>96.7329</td>    <td>0.9</td>   <td>-748.1402</td>   <td>941.606</td>   <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>59</td>    <td>971.5844</td>   <td>0.001</td>  <td>319.0256</td>   <td>1624.1431</td>  <td>True</td> 
</tr>
<tr>
    <td>42</td>      <td>6</td>    <td>338.5523</td>    <td>0.9</td>   <td>-627.8993</td>  <td>1305.0039</td>  <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>60</td>     <td>664.189</td>  <td>0.0426</td>   <td>6.9741</td>    <td>1321.4038</td>  <td>True</td> 
</tr>
<tr>
    <td>42</td>     <td>61</td>    <td>292.5037</td>    <td>0.9</td>   <td>-493.6664</td>  <td>1078.6739</td>  <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>62</td>    <td>702.7222</td>  <td>0.0198</td>   <td>37.8523</td>   <td>1367.5921</td>  <td>True</td> 
</tr>
<tr>
    <td>42</td>     <td>63</td>    <td>767.4278</td>  <td>0.2161</td>  <td>-92.6411</td>   <td>1627.4967</td>  <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>64</td>     <td>370.831</td>    <td>0.9</td>   <td>-368.5934</td>  <td>1110.2555</td>  <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>65</td>    <td>143.3399</td>    <td>0.9</td>   <td>-584.0605</td>  <td>870.7404</td>   <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>66</td>     <td>166.344</td>    <td>0.9</td>   <td>-958.0919</td>  <td>1290.7798</td>  <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>67</td>     <td>-17.331</td>    <td>0.9</td>  <td>-1049.8811</td>  <td>1015.219</td>   <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>68</td>    <td>-20.1219</td>    <td>0.9</td>   <td>-736.7894</td>  <td>696.5455</td>   <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>69</td>    <td>510.5722</td>  <td>0.8169</td>  <td>-216.8283</td>  <td>1237.9727</td>  <td>False</td>
</tr>
<tr>
    <td>42</td>      <td>7</td>    <td>501.0897</td>  <td>0.8911</td>  <td>-238.3348</td>  <td>1240.5141</td>  <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>70</td>     <td>20.6228</td>    <td>0.9</td>   <td>-669.7775</td>  <td>711.0231</td>   <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>71</td>    <td>223.5285</td>    <td>0.9</td>   <td>-456.2749</td>  <td>903.3319</td>   <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>72</td>    <td>365.6798</td>    <td>0.9</td>   <td>-332.6329</td>  <td>1063.9924</td>  <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>73</td>     <td>26.469</td>     <td>0.9</td>   <td>-889.8549</td>  <td>942.7929</td>   <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>74</td>    <td>-76.1464</td>    <td>0.9</td>  <td>-1015.9385</td>  <td>863.6456</td>   <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>75</td>    <td>-101.9633</td>   <td>0.9</td>   <td>-772.4472</td>  <td>568.5207</td>   <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>76</td>    <td>125.7848</td>    <td>0.9</td>   <td>-568.4789</td>  <td>820.0484</td>   <td>False</td>
</tr>
<tr>
    <td>42</td>     <td>77</td>    <td>-36.3689</td>    <td>0.9</td>   <td>-734.6815</td>  <td>661.9438</td>   <td>False</td>
</tr>
<tr>
    <td>42</td>      <td>8</td>    <td>784.9305</td>  <td>0.3961</td>  <td>-154.8616</td>  <td>1724.7226</td>  <td>False</td>
</tr>
<tr>
    <td>42</td>      <td>9</td>    <td>1491.869</td>  <td>0.0103</td>  <td>128.4377</td>   <td>2855.3003</td>  <td>True</td> 
</tr>
<tr>
    <td>43</td>     <td>44</td>    <td>-436.4544</td>   <td>0.9</td>  <td>-1235.3997</td>  <td>362.4908</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>45</td>    <td>-488.0299</td>   <td>0.9</td>  <td>-1415.3375</td>  <td>439.2777</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>46</td>    <td>-599.0815</td> <td>0.5722</td> <td>-1365.4028</td>  <td>167.2399</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>47</td>    <td>-619.0847</td> <td>0.6521</td> <td>-1438.3166</td>  <td>200.1473</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>48</td>    <td>-569.512</td>    <td>0.9</td>  <td>-1840.3122</td>  <td>701.2881</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>49</td>    <td>-374.2561</td>   <td>0.9</td>  <td>-1193.4881</td>  <td>444.9759</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>      <td>5</td>    <td>-246.522</td>    <td>0.9</td>  <td>-1288.8317</td>  <td>795.7877</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>50</td>    <td>-475.637</td>    <td>0.9</td>  <td>-1517.9467</td>  <td>566.6727</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>51</td>    <td>183.4314</td>    <td>0.9</td>   <td>-525.266</td>   <td>892.1287</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>52</td>    <td>-723.287</td>  <td>0.1004</td> <td>-1482.7354</td>   <td>36.1613</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>53</td>    <td>-220.6301</td>   <td>0.9</td>   <td>-973.6231</td>  <td>532.3629</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>54</td>    <td>-684.387</td>  <td>0.0969</td>  <td>-1401.215</td>   <td>32.4409</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>55</td>    <td>-235.3643</td>   <td>0.9</td>   <td>-966.023</td>   <td>495.2944</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>56</td>     <td>75.787</td>     <td>0.9</td>   <td>-596.6573</td>  <td>748.2312</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>57</td>    <td>-487.1675</td>   <td>0.9</td>  <td>-1286.1127</td>  <td>311.7778</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>58</td>    <td>-456.3731</td>   <td>0.9</td>  <td>-1313.1465</td>  <td>400.4002</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>59</td>    <td>418.4783</td>    <td>0.9</td>   <td>-249.416</td>   <td>1086.3727</td>  <td>False</td>
</tr>
<tr>
    <td>43</td>      <td>6</td>    <td>-214.5537</td>   <td>0.9</td>  <td>-1191.4256</td>  <td>762.3182</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>60</td>     <td>111.083</td>    <td>0.9</td>   <td>-561.3613</td>  <td>783.5272</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>61</td>    <td>-260.6023</td>   <td>0.9</td>  <td>-1059.5475</td>   <td>538.343</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>62</td>    <td>149.6162</td>    <td>0.9</td>   <td>-530.3117</td>   <td>829.544</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>63</td>    <td>214.3218</td>    <td>0.9</td>   <td>-657.4399</td>  <td>1086.0835</td>  <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>64</td>    <td>-182.275</td>    <td>0.9</td>   <td>-935.268</td>    <td>570.718</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>65</td>    <td>-409.7661</td>   <td>0.9</td>  <td>-1150.9553</td>  <td>331.4231</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>66</td>    <td>-386.762</td>    <td>0.9</td>  <td>-1520.1666</td>  <td>746.6425</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>67</td>    <td>-570.437</td>    <td>0.9</td>  <td>-1612.7467</td>  <td>471.8727</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>68</td>    <td>-573.2279</td> <td>0.5637</td> <td>-1303.8867</td>  <td>157.4308</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>69</td>    <td>-42.5338</td>    <td>0.9</td>   <td>-783.723</td>   <td>698.6554</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>      <td>7</td>    <td>-52.0163</td>    <td>0.9</td>   <td>-805.0093</td>  <td>700.9766</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>70</td>    <td>-532.4832</td>  <td>0.653</td> <td>-1237.3963</td>  <td>172.4299</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>71</td>    <td>-329.5775</td>   <td>0.9</td>  <td>-1024.1152</td>  <td>364.9602</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>72</td>    <td>-187.4262</td>   <td>0.9</td>   <td>-900.0906</td>  <td>525.2381</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>73</td>    <td>-526.637</td>    <td>0.9</td>  <td>-1453.9447</td>  <td>400.6706</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>74</td>    <td>-629.2524</td>   <td>0.9</td>  <td>-1579.7571</td>  <td>321.2522</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>75</td>    <td>-655.0693</td> <td>0.0955</td> <td>-1340.4879</td>   <td>30.3494</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>76</td>    <td>-427.3212</td>   <td>0.9</td>  <td>-1136.0186</td>  <td>281.3761</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>     <td>77</td>    <td>-589.4749</td> <td>0.4268</td> <td>-1302.1392</td>  <td>123.1895</td>   <td>False</td>
</tr>
<tr>
    <td>43</td>      <td>8</td>    <td>231.8245</td>    <td>0.9</td>   <td>-718.6801</td>  <td>1182.3291</td>  <td>False</td>
</tr>
<tr>
    <td>43</td>      <td>9</td>     <td>938.763</td>  <td>0.8693</td>  <td>-432.0743</td>  <td>2309.6002</td>  <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>45</td>    <td>-51.5755</td>    <td>0.9</td>  <td>-1006.0201</td>  <td>902.8691</td>   <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>46</td>    <td>-162.6271</td>   <td>0.9</td>   <td>-961.5723</td>  <td>636.3182</td>   <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>47</td>    <td>-182.6302</td>   <td>0.9</td>  <td>-1032.4573</td>  <td>667.1969</td>   <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>48</td>    <td>-133.0576</td>   <td>0.9</td>  <td>-1423.7931</td>  <td>1157.6779</td>  <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>49</td>     <td>62.1983</td>    <td>0.9</td>   <td>-787.6288</td>  <td>912.0254</td>   <td>False</td>
</tr>
<tr>
    <td>44</td>      <td>5</td>    <td>189.9324</td>    <td>0.9</td>   <td>-876.5922</td>  <td>1256.4569</td>  <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>50</td>    <td>-39.1826</td>    <td>0.9</td>  <td>-1105.7072</td>  <td>1027.3419</td>  <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>51</td>    <td>619.8858</td>  <td>0.4033</td>  <td>-123.967</td>   <td>1363.7386</td>  <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>52</td>    <td>-286.8326</td>   <td>0.9</td>  <td>-1079.1879</td>  <td>505.5227</td>   <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>53</td>    <td>215.8243</td>    <td>0.9</td>   <td>-570.3459</td>  <td>1001.9945</td>  <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>54</td>    <td>-247.9326</td>   <td>0.9</td>   <td>-999.5358</td>  <td>503.6706</td>   <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>55</td>    <td>201.0901</td>    <td>0.9</td>   <td>-563.7153</td>  <td>965.8955</td>   <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>56</td>    <td>512.2414</td>  <td>0.7551</td>  <td>-197.1572</td>   <td>1221.64</td>   <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>57</td>     <td>-50.713</td>    <td>0.9</td>   <td>-881.0013</td>  <td>779.5752</td>   <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>58</td>    <td>-19.9187</td>    <td>0.9</td>   <td>-905.9918</td>  <td>866.1544</td>   <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>59</td>    <td>854.9328</td>   <td>0.001</td>  <td>149.8456</td>    <td>1560.02</td>   <td>True</td> 
</tr>
<tr>
    <td>44</td>      <td>6</td>    <td>221.9007</td>    <td>0.9</td>   <td>-780.7676</td>  <td>1224.569</td>   <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>60</td>    <td>547.5374</td>  <td>0.6027</td>  <td>-161.8612</td>  <td>1256.936</td>   <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>61</td>    <td>175.8522</td>    <td>0.9</td>   <td>-654.4361</td>  <td>1006.1404</td>  <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>62</td>    <td>586.0706</td>  <td>0.4597</td>  <td>-130.4258</td>  <td>1302.5669</td>  <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>63</td>    <td>650.7762</td>  <td>0.7534</td>  <td>-249.7978</td>  <td>1551.3502</td>  <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>64</td>    <td>254.1795</td>    <td>0.9</td>   <td>-531.9907</td>  <td>1040.3496</td>  <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>65</td>     <td>26.6884</td>    <td>0.9</td>   <td>-748.1836</td>  <td>801.5603</td>   <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>66</td>     <td>49.6924</td>    <td>0.9</td>  <td>-1106.0199</td>  <td>1205.4047</td>  <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>67</td>    <td>-133.9826</td>   <td>0.9</td>  <td>-1200.5072</td>  <td>932.5419</td>   <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>68</td>    <td>-136.7735</td>   <td>0.9</td>   <td>-901.5789</td>  <td>628.0319</td>   <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>69</td>    <td>393.9206</td>    <td>0.9</td>   <td>-380.9513</td>  <td>1168.7925</td>  <td>False</td>
</tr>
<tr>
    <td>44</td>      <td>7</td>    <td>384.4381</td>    <td>0.9</td>   <td>-401.7321</td>  <td>1170.6082</td>  <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>70</td>    <td>-96.0288</td>    <td>0.9</td>   <td>-836.2771</td>  <td>644.2196</td>   <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>71</td>    <td>106.8769</td>    <td>0.9</td>   <td>-623.4981</td>  <td>837.2519</td>   <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>72</td>    <td>249.0282</td>    <td>0.9</td>   <td>-498.6051</td>  <td>996.6615</td>   <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>73</td>    <td>-90.1826</td>    <td>0.9</td>  <td>-1044.6272</td>   <td>864.262</td>   <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>74</td>    <td>-192.798</td>    <td>0.9</td>  <td>-1169.7955</td>  <td>784.1995</td>   <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>75</td>    <td>-218.6148</td>   <td>0.9</td>   <td>-940.3238</td>  <td>503.0941</td>   <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>76</td>     <td>9.1332</td>     <td>0.9</td>   <td>-734.7196</td>   <td>752.986</td>   <td>False</td>
</tr>
<tr>
    <td>44</td>     <td>77</td>    <td>-153.0204</td>   <td>0.9</td>   <td>-900.6538</td>  <td>594.6129</td>   <td>False</td>
</tr>
<tr>
    <td>44</td>      <td>8</td>    <td>668.2789</td>  <td>0.8717</td>  <td>-308.7186</td>  <td>1645.2764</td>  <td>False</td>
</tr>
<tr>
    <td>44</td>      <td>9</td>    <td>1375.2174</td> <td>0.0588</td>  <td>-14.1206</td>   <td>2764.5553</td>  <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>46</td>    <td>-111.0516</td>   <td>0.9</td>  <td>-1038.3592</td>   <td>816.256</td>   <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>47</td>    <td>-131.0548</td>   <td>0.9</td>  <td>-1102.5444</td>  <td>840.4348</td>   <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>48</td>    <td>-81.4821</td>    <td>0.9</td>  <td>-1455.3759</td>  <td>1292.4116</td>  <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>49</td>    <td>113.7738</td>    <td>0.9</td>   <td>-857.7158</td>  <td>1085.2634</td>  <td>False</td>
</tr>
<tr>
    <td>45</td>      <td>5</td>    <td>241.5079</td>    <td>0.9</td>   <td>-924.2797</td>  <td>1407.2954</td>  <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>50</td>     <td>12.3929</td>    <td>0.9</td>  <td>-1153.3947</td>  <td>1178.1804</td>  <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>51</td>    <td>671.4613</td>  <td>0.6304</td>  <td>-208.8244</td>  <td>1551.747</td>   <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>52</td>    <td>-235.2571</td>   <td>0.9</td>  <td>-1156.8931</td>  <td>686.3788</td>   <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>53</td>    <td>267.3998</td>    <td>0.9</td>   <td>-648.9241</td>  <td>1183.7237</td>  <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>54</td>    <td>-196.3571</td>   <td>0.9</td>  <td>-1083.2018</td>  <td>690.4875</td>   <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>55</td>    <td>252.6656</td>    <td>0.9</td>   <td>-645.3952</td>  <td>1150.7264</td>  <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>56</td>    <td>563.8169</td>    <td>0.9</td>   <td>-287.554</td>   <td>1415.1877</td>  <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>57</td>     <td>0.8624</td>     <td>0.9</td>   <td>-953.5822</td>   <td>955.307</td>   <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>58</td>     <td>31.6567</td>    <td>0.9</td>   <td>-971.6934</td>  <td>1035.0069</td>  <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>59</td>    <td>906.5082</td>   <td>0.016</td>   <td>58.7265</td>    <td>1754.29</td>   <td>True</td> 
</tr>
<tr>
    <td>45</td>      <td>6</td>    <td>273.4762</td>    <td>0.9</td>   <td>-834.1924</td>  <td>1381.1448</td>  <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>60</td>    <td>599.1129</td>  <td>0.8114</td>  <td>-252.258</td>   <td>1450.4837</td>  <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>61</td>    <td>227.4276</td>    <td>0.9</td>   <td>-727.017</td>   <td>1181.8723</td>  <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>62</td>     <td>637.646</td>  <td>0.6886</td>  <td>-219.6479</td>   <td>1494.94</td>   <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>63</td>    <td>702.3517</td>  <td>0.8498</td>  <td>-313.8272</td>  <td>1718.5306</td>  <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>64</td>    <td>305.7549</td>    <td>0.9</td>   <td>-610.569</td>   <td>1222.0788</td>  <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>65</td>     <td>78.2638</td>    <td>0.9</td>   <td>-828.3852</td>  <td>984.9128</td>   <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>66</td>    <td>101.2679</td>    <td>0.9</td>  <td>-1146.6331</td>  <td>1349.1689</td>  <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>67</td>    <td>-82.4071</td>    <td>0.9</td>  <td>-1248.1947</td>  <td>1083.3804</td>  <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>68</td>    <td>-85.1981</td>    <td>0.9</td>   <td>-983.2589</td>  <td>812.8628</td>   <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>69</td>    <td>445.4961</td>    <td>0.9</td>   <td>-461.1529</td>  <td>1352.1451</td>  <td>False</td>
</tr>
<tr>
    <td>45</td>      <td>7</td>    <td>436.0135</td>    <td>0.9</td>   <td>-480.3104</td>  <td>1352.3374</td>  <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>70</td>    <td>-44.4533</td>    <td>0.9</td>   <td>-921.6953</td>  <td>832.7887</td>   <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>71</td>    <td>158.4524</td>    <td>0.9</td>   <td>-710.4743</td>  <td>1027.3791</td>  <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>72</td>    <td>300.6037</td>    <td>0.9</td>   <td>-582.879</td>   <td>1184.0863</td>  <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>73</td>    <td>-38.6071</td>    <td>0.9</td>  <td>-1102.8207</td>  <td>1025.6064</td>  <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>74</td>    <td>-141.2225</td>   <td>0.9</td>  <td>-1225.7086</td>  <td>943.2636</td>   <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>75</td>    <td>-167.0394</td>   <td>0.9</td>  <td>-1028.6946</td>  <td>694.6159</td>   <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>76</td>     <td>60.7086</td>    <td>0.9</td>   <td>-819.5771</td>  <td>940.9944</td>   <td>False</td>
</tr>
<tr>
    <td>45</td>     <td>77</td>    <td>-101.445</td>    <td>0.9</td>   <td>-984.9276</td>  <td>782.0376</td>   <td>False</td>
</tr>
<tr>
    <td>45</td>      <td>8</td>    <td>719.8544</td>    <td>0.9</td>   <td>-364.6317</td>  <td>1804.3405</td>  <td>False</td>
</tr>
<tr>
    <td>45</td>      <td>9</td>    <td>1426.7929</td> <td>0.0765</td>  <td>-40.1243</td>    <td>2893.71</td>   <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>47</td>    <td>-20.0032</td>    <td>0.9</td>   <td>-839.2351</td>  <td>799.2288</td>   <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>48</td>     <td>29.5694</td>    <td>0.9</td>  <td>-1241.2307</td>  <td>1300.3696</td>  <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>49</td>    <td>224.8254</td>    <td>0.9</td>   <td>-594.4066</td>  <td>1044.0574</td>  <td>False</td>
</tr>
<tr>
    <td>46</td>      <td>5</td>    <td>352.5594</td>    <td>0.9</td>   <td>-689.7503</td>  <td>1394.8692</td>  <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>50</td>    <td>123.4444</td>    <td>0.9</td>   <td>-918.8653</td>  <td>1165.7542</td>  <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>51</td>    <td>782.5129</td>  <td>0.0086</td>   <td>73.8155</td>   <td>1491.2102</td>  <td>True</td> 
</tr>
<tr>
    <td>46</td>     <td>52</td>    <td>-124.2056</td>   <td>0.9</td>   <td>-883.6539</td>  <td>635.2428</td>   <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>53</td>    <td>378.4513</td>    <td>0.9</td>   <td>-374.5417</td>  <td>1131.4443</td>  <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>54</td>    <td>-85.3056</td>    <td>0.9</td>   <td>-802.1335</td>  <td>631.5224</td>   <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>55</td>    <td>363.7172</td>    <td>0.9</td>   <td>-366.9416</td>  <td>1094.3759</td>  <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>56</td>    <td>674.8684</td>  <td>0.0474</td>   <td>2.4242</td>    <td>1347.3127</td>  <td>True</td> 
</tr>
<tr>
    <td>46</td>     <td>57</td>     <td>111.914</td>    <td>0.9</td>   <td>-687.0312</td>  <td>910.8592</td>   <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>58</td>    <td>142.7083</td>    <td>0.9</td>   <td>-714.065</td>   <td>999.4816</td>   <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>59</td>    <td>1017.5598</td>  <td>0.001</td>  <td>349.6654</td>   <td>1685.4542</td>  <td>True</td> 
</tr>
<tr>
    <td>46</td>      <td>6</td>    <td>384.5278</td>    <td>0.9</td>   <td>-592.3441</td>  <td>1361.3996</td>  <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>60</td>    <td>710.1644</td>  <td>0.0201</td>   <td>37.7202</td>   <td>1382.6087</td>  <td>True</td> 
</tr>
<tr>
    <td>46</td>     <td>61</td>    <td>338.4792</td>    <td>0.9</td>   <td>-460.466</td>   <td>1137.4245</td>  <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>62</td>    <td>748.6976</td>   <td>0.009</td>   <td>68.7698</td>   <td>1428.6255</td>  <td>True</td> 
</tr>
<tr>
    <td>46</td>     <td>63</td>    <td>813.4033</td>  <td>0.1291</td>  <td>-58.3585</td>   <td>1685.165</td>   <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>64</td>    <td>416.8065</td>    <td>0.9</td>   <td>-336.1865</td>  <td>1169.7995</td>  <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>65</td>    <td>189.3154</td>    <td>0.9</td>   <td>-551.8738</td>  <td>930.5046</td>   <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>66</td>    <td>212.3194</td>    <td>0.9</td>   <td>-921.0851</td>  <td>1345.724</td>   <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>67</td>     <td>28.6444</td>    <td>0.9</td>  <td>-1013.6653</td>  <td>1070.9542</td>  <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>68</td>     <td>25.8535</td>    <td>0.9</td>   <td>-704.8052</td>  <td>756.5123</td>   <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>69</td>    <td>556.5477</td>  <td>0.6668</td>  <td>-184.6415</td>  <td>1297.7369</td>  <td>False</td>
</tr>
<tr>
    <td>46</td>      <td>7</td>    <td>547.0651</td>  <td>0.7415</td>  <td>-205.9279</td>  <td>1300.0581</td>  <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>70</td>     <td>66.5983</td>    <td>0.9</td>   <td>-638.3148</td>  <td>771.5114</td>   <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>71</td>     <td>269.504</td>    <td>0.9</td>   <td>-425.0337</td>  <td>964.0417</td>   <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>72</td>    <td>411.6553</td>    <td>0.9</td>   <td>-301.0091</td>  <td>1124.3196</td>  <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>73</td>     <td>72.4444</td>    <td>0.9</td>   <td>-854.8632</td>  <td>999.7521</td>   <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>74</td>    <td>-30.1709</td>    <td>0.9</td>   <td>-980.6756</td>  <td>920.3337</td>   <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>75</td>    <td>-55.9878</td>    <td>0.9</td>   <td>-741.4064</td>  <td>629.4309</td>   <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>76</td>    <td>171.7602</td>    <td>0.9</td>   <td>-536.9371</td>  <td>880.4576</td>   <td>False</td>
</tr>
<tr>
    <td>46</td>     <td>77</td>     <td>9.6066</td>     <td>0.9</td>   <td>-703.0578</td>   <td>722.271</td>   <td>False</td>
</tr>
<tr>
    <td>46</td>      <td>8</td>     <td>830.906</td>  <td>0.2646</td>  <td>-119.5987</td>  <td>1781.4106</td>  <td>False</td>
</tr>
<tr>
    <td>46</td>      <td>9</td>    <td>1537.8444</td> <td>0.0062</td>  <td>167.0072</td>   <td>2908.6817</td>  <td>True</td> 
</tr>
<tr>
    <td>47</td>     <td>48</td>     <td>49.5726</td>    <td>0.9</td>  <td>-1253.8175</td>  <td>1352.9627</td>  <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>49</td>    <td>244.8286</td>    <td>0.9</td>   <td>-624.0982</td>  <td>1113.7553</td>  <td>False</td>
</tr>
<tr>
    <td>47</td>      <td>5</td>    <td>372.5626</td>    <td>0.9</td>   <td>-709.2424</td>  <td>1454.3677</td>  <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>50</td>    <td>143.4476</td>    <td>0.9</td>   <td>-938.3574</td>  <td>1225.2527</td>  <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>51</td>     <td>802.516</td>   <td>0.023</td>   <td>36.9153</td>   <td>1568.1168</td>  <td>True</td> 
</tr>
<tr>
    <td>47</td>     <td>52</td>    <td>-104.2024</td>   <td>0.9</td>   <td>-917.0089</td>  <td>708.6041</td>   <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>53</td>    <td>398.4545</td>    <td>0.9</td>   <td>-408.3237</td>  <td>1205.2327</td>  <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>54</td>    <td>-65.3024</td>    <td>0.9</td>   <td>-838.4356</td>  <td>707.8308</td>   <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>55</td>    <td>383.7203</td>    <td>0.9</td>   <td>-402.2534</td>  <td>1169.6941</td>  <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>56</td>    <td>694.8716</td>  <td>0.1055</td>  <td>-37.2991</td>   <td>1427.0423</td>  <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>57</td>    <td>131.9172</td>    <td>0.9</td>   <td>-717.9099</td>  <td>981.7443</td>   <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>58</td>    <td>162.7115</td>    <td>0.9</td>   <td>-741.6961</td>  <td>1067.1191</td>  <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>59</td>    <td>1037.563</td>   <td>0.001</td>  <td>309.5688</td>   <td>1765.5572</td>  <td>True</td> 
</tr>
<tr>
    <td>47</td>      <td>6</td>     <td>404.531</td>    <td>0.9</td>   <td>-614.3759</td>  <td>1423.4379</td>  <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>60</td>    <td>730.1676</td>  <td>0.0522</td>   <td>-2.0031</td>   <td>1462.3383</td>  <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>61</td>    <td>358.4824</td>    <td>0.9</td>   <td>-491.3447</td>  <td>1208.3095</td>  <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>62</td>    <td>768.7008</td>  <td>0.0263</td>   <td>29.651</td>    <td>1507.7506</td>  <td>True</td> 
</tr>
<tr>
    <td>47</td>     <td>63</td>    <td>833.4064</td>  <td>0.1802</td>  <td>-85.2127</td>   <td>1752.0256</td>  <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>64</td>    <td>436.8097</td>    <td>0.9</td>   <td>-369.9685</td>  <td>1243.5879</td>  <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>65</td>    <td>209.3186</td>    <td>0.9</td>   <td>-586.454</td>   <td>1005.0912</td>  <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>66</td>    <td>232.3226</td>    <td>0.9</td>   <td>-937.5058</td>  <td>1402.151</td>   <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>67</td>     <td>48.6476</td>    <td>0.9</td>  <td>-1033.1574</td>  <td>1130.4527</td>  <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>68</td>     <td>45.8567</td>    <td>0.9</td>   <td>-740.1171</td>  <td>831.8305</td>   <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>69</td>    <td>576.5508</td>  <td>0.7476</td>  <td>-219.2218</td>  <td>1372.3234</td>  <td>False</td>
</tr>
<tr>
    <td>47</td>      <td>7</td>    <td>567.0683</td>  <td>0.8139</td>  <td>-239.7099</td>  <td>1373.8465</td>  <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>70</td>     <td>86.6015</td>    <td>0.9</td>   <td>-675.4977</td>  <td>848.7006</td>   <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>71</td>    <td>289.5071</td>    <td>0.9</td>   <td>-463.0055</td>  <td>1042.0198</td>  <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>72</td>    <td>431.6584</td>    <td>0.9</td>   <td>-337.616</td>   <td>1200.9328</td>  <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>73</td>     <td>92.4476</td>    <td>0.9</td>   <td>-879.042</td>   <td>1063.9372</td>  <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>74</td>    <td>-10.1678</td>    <td>0.9</td>  <td>-1003.8235</td>   <td>983.488</td>   <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>75</td>    <td>-35.9846</td>    <td>0.9</td>   <td>-780.089</td>   <td>708.1198</td>   <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>76</td>    <td>191.7634</td>    <td>0.9</td>   <td>-573.8374</td>  <td>957.3642</td>   <td>False</td>
</tr>
<tr>
    <td>47</td>     <td>77</td>     <td>29.6098</td>    <td>0.9</td>   <td>-739.6646</td>  <td>798.8842</td>   <td>False</td>
</tr>
<tr>
    <td>47</td>      <td>8</td>    <td>850.9092</td>  <td>0.3185</td>  <td>-142.7466</td>  <td>1844.5649</td>  <td>False</td>
</tr>
<tr>
    <td>47</td>      <td>9</td>    <td>1557.8476</td> <td>0.0074</td>  <td>156.7454</td>   <td>2958.9499</td>  <td>True</td> 
</tr>
<tr>
    <td>48</td>     <td>49</td>     <td>195.256</td>    <td>0.9</td>  <td>-1108.1341</td>  <td>1498.646</td>   <td>False</td>
</tr>
<tr>
    <td>48</td>      <td>5</td>     <td>322.99</td>     <td>0.9</td>  <td>-1131.0025</td>  <td>1776.9825</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>50</td>     <td>93.875</td>     <td>0.9</td>  <td>-1360.1175</td>  <td>1547.8675</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>51</td>    <td>752.9434</td>    <td>0.9</td>   <td>-483.9626</td>  <td>1989.8495</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>52</td>    <td>-153.775</td>    <td>0.9</td>  <td>-1420.4425</td>  <td>1112.8925</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>53</td>    <td>348.8819</td>    <td>0.9</td>   <td>-913.9257</td>  <td>1611.6895</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>54</td>    <td>-114.875</td>    <td>0.9</td>  <td>-1356.4575</td>  <td>1126.7075</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>55</td>    <td>334.1477</td>    <td>0.9</td>   <td>-915.471</td>   <td>1583.7664</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>56</td>     <td>645.299</td>    <td>0.9</td>   <td>-571.1984</td>  <td>1861.7964</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>57</td>     <td>82.3446</td>    <td>0.9</td>  <td>-1208.3909</td>  <td>1373.0801</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>58</td>    <td>113.1389</td>    <td>0.9</td>  <td>-1214.1686</td>  <td>1440.4464</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>59</td>    <td>987.9904</td>  <td>0.4735</td>  <td>-225.9979</td>  <td>2201.9787</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>      <td>6</td>    <td>354.9583</td>    <td>0.9</td>  <td>-1052.8639</td>  <td>1762.7805</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>60</td>     <td>680.595</td>    <td>0.9</td>   <td>-535.9024</td>  <td>1897.0924</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>61</td>    <td>308.9098</td>    <td>0.9</td>   <td>-981.8257</td>  <td>1599.6453</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>62</td>    <td>719.1282</td>    <td>0.9</td>   <td>-501.5219</td>  <td>1939.7783</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>63</td>    <td>783.8338</td>    <td>0.9</td>   <td>-553.1977</td>  <td>2120.8653</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>64</td>    <td>387.2371</td>    <td>0.9</td>   <td>-875.5706</td>  <td>1650.0447</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>65</td>     <td>159.746</td>    <td>0.9</td>   <td>-1096.059</td>  <td>1415.5509</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>66</td>     <td>182.75</td>     <td>0.9</td>  <td>-1337.8718</td>  <td>1703.3718</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>67</td>     <td>-0.925</td>     <td>0.9</td>  <td>-1454.9175</td>  <td>1453.0675</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>68</td>     <td>-3.7159</td>    <td>0.9</td>  <td>-1253.3346</td>  <td>1245.9028</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>69</td>    <td>526.9782</td>    <td>0.9</td>   <td>-728.8267</td>  <td>1782.7832</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>      <td>7</td>    <td>517.4957</td>    <td>0.9</td>   <td>-745.312</td>   <td>1780.3033</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>70</td>     <td>37.0288</td>    <td>0.9</td>  <td>-1197.7129</td>  <td>1271.7706</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>71</td>    <td>239.9345</td>    <td>0.9</td>   <td>-988.9134</td>  <td>1468.7825</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>72</td>    <td>382.0858</td>    <td>0.9</td>   <td>-857.0975</td>  <td>1621.2691</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>73</td>     <td>42.875</td>     <td>0.9</td>  <td>-1331.0188</td>  <td>1416.7688</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>74</td>    <td>-59.7404</td>    <td>0.9</td>  <td>-1449.3964</td>  <td>1329.9156</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>75</td>    <td>-85.5572</td>    <td>0.9</td>  <td>-1309.2743</td>  <td>1138.1598</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>76</td>    <td>142.1908</td>    <td>0.9</td>  <td>-1094.7153</td>  <td>1379.0969</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>     <td>77</td>    <td>-19.9628</td>    <td>0.9</td>  <td>-1259.1461</td>  <td>1219.2204</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>      <td>8</td>    <td>801.3365</td>    <td>0.9</td>   <td>-588.3194</td>  <td>2190.9925</td>  <td>False</td>
</tr>
<tr>
    <td>48</td>      <td>9</td>    <td>1508.275</td>  <td>0.2359</td>  <td>-196.6823</td>  <td>3213.2323</td>  <td>False</td>
</tr>
<tr>
    <td>49</td>      <td>5</td>     <td>127.734</td>    <td>0.9</td>   <td>-954.071</td>   <td>1209.5391</td>  <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>50</td>    <td>-101.381</td>    <td>0.9</td>   <td>-1183.186</td>  <td>980.4241</td>   <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>51</td>    <td>557.6875</td>  <td>0.7356</td>  <td>-207.9133</td>  <td>1323.2882</td>  <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>52</td>    <td>-349.031</td>    <td>0.9</td>  <td>-1161.8375</td>  <td>463.7756</td>   <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>53</td>    <td>153.6259</td>    <td>0.9</td>   <td>-653.1523</td>  <td>960.4042</td>   <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>54</td>    <td>-310.131</td>    <td>0.9</td>  <td>-1083.2642</td>  <td>463.0023</td>   <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>55</td>    <td>138.8918</td>    <td>0.9</td>   <td>-647.082</td>   <td>924.8656</td>   <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>56</td>     <td>450.043</td>    <td>0.9</td>   <td>-282.1276</td>  <td>1182.2137</td>  <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>57</td>    <td>-112.9114</td>   <td>0.9</td>   <td>-962.7385</td>  <td>736.9157</td>   <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>58</td>    <td>-82.1171</td>    <td>0.9</td>   <td>-986.5247</td>  <td>822.2905</td>   <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>59</td>    <td>792.7344</td>  <td>0.0113</td>   <td>64.7402</td>   <td>1520.7286</td>  <td>True</td> 
</tr>
<tr>
    <td>49</td>      <td>6</td>    <td>159.7024</td>    <td>0.9</td>   <td>-859.2045</td>  <td>1178.6093</td>  <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>60</td>     <td>485.339</td>    <td>0.9</td>   <td>-246.8316</td>  <td>1217.5097</td>  <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>61</td>    <td>113.6538</td>    <td>0.9</td>   <td>-736.1733</td>  <td>963.4809</td>   <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>62</td>    <td>523.8722</td>  <td>0.7956</td>  <td>-215.1775</td>  <td>1262.922</td>   <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>63</td>    <td>588.5779</td>    <td>0.9</td>   <td>-330.0413</td>  <td>1507.197</td>   <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>64</td>    <td>191.9811</td>    <td>0.9</td>   <td>-614.7971</td>  <td>998.7593</td>   <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>65</td>     <td>-35.51</td>     <td>0.9</td>   <td>-831.2826</td>  <td>760.2626</td>   <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>66</td>     <td>-12.506</td>    <td>0.9</td>  <td>-1182.3344</td>  <td>1157.3225</td>  <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>67</td>    <td>-196.181</td>    <td>0.9</td>   <td>-1277.986</td>  <td>885.6241</td>   <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>68</td>    <td>-198.9719</td>   <td>0.9</td>   <td>-984.9457</td>  <td>587.0019</td>   <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>69</td>    <td>331.7223</td>    <td>0.9</td>   <td>-464.0503</td>  <td>1127.4949</td>  <td>False</td>
</tr>
<tr>
    <td>49</td>      <td>7</td>    <td>322.2397</td>    <td>0.9</td>   <td>-484.5385</td>  <td>1129.0179</td>  <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>70</td>    <td>-158.2271</td>   <td>0.9</td>   <td>-920.3263</td>   <td>603.872</td>   <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>71</td>     <td>44.6786</td>    <td>0.9</td>   <td>-707.834</td>   <td>797.1912</td>   <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>72</td>    <td>186.8299</td>    <td>0.9</td>   <td>-582.4446</td>  <td>956.1043</td>   <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>73</td>    <td>-152.381</td>    <td>0.9</td>  <td>-1123.8706</td>  <td>819.1087</td>   <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>74</td>    <td>-254.9963</td>   <td>0.9</td>  <td>-1248.6521</td>  <td>738.6594</td>   <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>75</td>    <td>-280.8132</td>   <td>0.9</td>  <td>-1024.9176</td>  <td>463.2912</td>   <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>76</td>    <td>-53.0652</td>    <td>0.9</td>   <td>-818.6659</td>  <td>712.5356</td>   <td>False</td>
</tr>
<tr>
    <td>49</td>     <td>77</td>    <td>-215.2188</td>   <td>0.9</td>   <td>-984.4932</td>  <td>554.0556</td>   <td>False</td>
</tr>
<tr>
    <td>49</td>      <td>8</td>    <td>606.0806</td>    <td>0.9</td>   <td>-387.5751</td>  <td>1599.7363</td>  <td>False</td>
</tr>
<tr>
    <td>49</td>      <td>9</td>    <td>1313.019</td>   <td>0.125</td>  <td>-88.0832</td>   <td>2714.1213</td>  <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>50</td>    <td>-229.115</td>    <td>0.9</td>  <td>-1488.3095</td>  <td>1030.0795</td>  <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>51</td>    <td>429.9534</td>    <td>0.9</td>   <td>-570.7529</td>  <td>1430.6597</td>  <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>52</td>    <td>-476.765</td>    <td>0.9</td>  <td>-1514.0321</td>  <td>560.5021</td>   <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>53</td>     <td>25.8919</td>    <td>0.9</td>  <td>-1006.6581</td>  <td>1058.4419</td>  <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>54</td>    <td>-437.865</td>    <td>0.9</td>  <td>-1444.3457</td>  <td>568.6157</td>   <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>55</td>     <td>11.1577</td>    <td>0.9</td>  <td>-1005.2198</td>  <td>1027.5353</td>  <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>56</td>     <td>322.309</td>    <td>0.9</td>   <td>-653.0588</td>  <td>1297.6768</td>  <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>57</td>    <td>-240.6454</td>   <td>0.9</td>   <td>-1307.17</td>   <td>825.8791</td>   <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>58</td>    <td>-209.8511</td>   <td>0.9</td>  <td>-1320.3562</td>   <td>900.654</td>   <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>59</td>    <td>665.0004</td>  <td>0.8718</td>  <td>-307.2362</td>  <td>1637.237</td>   <td>False</td>
</tr>
<tr>
     <td>5</td>      <td>6</td>     <td>31.9683</td>    <td>0.9</td>  <td>-1173.6186</td>  <td>1237.5552</td>  <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>60</td>     <td>357.605</td>    <td>0.9</td>   <td>-617.7628</td>  <td>1332.9728</td>  <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>61</td>    <td>-14.0802</td>    <td>0.9</td>  <td>-1080.6048</td>  <td>1052.4443</td>  <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>62</td>    <td>396.1382</td>    <td>0.9</td>   <td>-584.404</td>   <td>1376.6804</td>  <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>63</td>    <td>460.8438</td>    <td>0.9</td>   <td>-661.2656</td>  <td>1582.9533</td>  <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>64</td>     <td>64.2471</td>    <td>0.9</td>   <td>-968.303</td>   <td>1096.7971</td>  <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>65</td>    <td>-163.244</td>    <td>0.9</td>  <td>-1187.2179</td>  <td>860.7299</td>   <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>66</td>     <td>-140.24</td>    <td>0.9</td>  <td>-1475.8174</td>  <td>1195.3374</td>  <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>67</td>    <td>-323.915</td>    <td>0.9</td>  <td>-1583.1095</td>  <td>935.2795</td>   <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>68</td>    <td>-326.7059</td>   <td>0.9</td>  <td>-1343.0835</td>  <td>689.6716</td>   <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>69</td>    <td>203.9882</td>    <td>0.9</td>   <td>-819.9857</td>  <td>1227.9621</td>  <td>False</td>
</tr>
<tr>
     <td>5</td>      <td>7</td>    <td>194.5057</td>    <td>0.9</td>   <td>-838.0444</td>  <td>1227.0557</td>  <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>70</td>    <td>-285.9612</td>   <td>0.9</td>   <td>-1283.991</td>  <td>712.0687</td>   <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>71</td>    <td>-83.0555</td>    <td>0.9</td>  <td>-1073.7844</td>  <td>907.6734</td>   <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>72</td>     <td>59.0958</td>    <td>0.9</td>   <td>-944.4238</td>  <td>1062.6154</td>  <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>73</td>    <td>-280.115</td>    <td>0.9</td>  <td>-1445.9025</td>  <td>885.6725</td>   <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>74</td>    <td>-382.7304</td>   <td>0.9</td>  <td>-1567.0531</td>  <td>801.5923</td>   <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>75</td>    <td>-408.5472</td>   <td>0.9</td>  <td>-1392.9048</td>  <td>575.8104</td>   <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>76</td>    <td>-180.7992</td>   <td>0.9</td>  <td>-1181.5055</td>  <td>819.9071</td>   <td>False</td>
</tr>
<tr>
     <td>5</td>     <td>77</td>    <td>-342.9528</td>   <td>0.9</td>  <td>-1346.4725</td>  <td>660.5668</td>   <td>False</td>
</tr>
<tr>
     <td>5</td>      <td>8</td>    <td>478.3465</td>    <td>0.9</td>   <td>-705.9761</td>  <td>1662.6692</td>  <td>False</td>
</tr>
<tr>
     <td>5</td>      <td>9</td>    <td>1185.285</td>  <td>0.6127</td>  <td>-356.9069</td>  <td>2727.4769</td>  <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>51</td>    <td>659.0684</td>    <td>0.9</td>   <td>-341.6379</td>  <td>1659.7747</td>  <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>52</td>     <td>-247.65</td>    <td>0.9</td>  <td>-1284.9171</td>  <td>789.6171</td>   <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>53</td>    <td>255.0069</td>    <td>0.9</td>   <td>-777.5431</td>  <td>1287.5569</td>  <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>54</td>     <td>-208.75</td>    <td>0.9</td>  <td>-1215.2307</td>  <td>797.7307</td>   <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>55</td>    <td>240.2727</td>    <td>0.9</td>   <td>-776.1048</td>  <td>1256.6503</td>  <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>56</td>     <td>551.424</td>    <td>0.9</td>   <td>-423.9438</td>  <td>1526.7918</td>  <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>57</td>    <td>-11.5304</td>    <td>0.9</td>   <td>-1078.055</td>  <td>1054.9941</td>  <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>58</td>     <td>19.2639</td>    <td>0.9</td>  <td>-1091.2412</td>  <td>1129.769</td>   <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>59</td>    <td>894.1154</td>  <td>0.1552</td>  <td>-78.1212</td>   <td>1866.352</td>   <td>False</td>
</tr>
<tr>
    <td>50</td>      <td>6</td>    <td>261.0833</td>    <td>0.9</td>   <td>-944.5036</td>  <td>1466.6702</td>  <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>60</td>     <td>586.72</td>     <td>0.9</td>   <td>-388.6478</td>  <td>1562.0878</td>  <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>61</td>    <td>215.0348</td>    <td>0.9</td>   <td>-851.4898</td>  <td>1281.5593</td>  <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>62</td>    <td>625.2532</td>    <td>0.9</td>   <td>-355.289</td>   <td>1605.7954</td>  <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>63</td>    <td>689.9588</td>    <td>0.9</td>   <td>-432.1506</td>  <td>1812.0683</td>  <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>64</td>    <td>293.3621</td>    <td>0.9</td>   <td>-739.188</td>   <td>1325.9121</td>  <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>65</td>     <td>65.871</td>     <td>0.9</td>   <td>-958.1029</td>  <td>1089.8449</td>  <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>66</td>     <td>88.875</td>     <td>0.9</td>  <td>-1246.7024</td>  <td>1424.4524</td>  <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>67</td>      <td>-94.8</td>     <td>0.9</td>  <td>-1353.9945</td>  <td>1164.3945</td>  <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>68</td>    <td>-97.5909</td>    <td>0.9</td>  <td>-1113.9685</td>  <td>918.7866</td>   <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>69</td>    <td>433.1032</td>    <td>0.9</td>   <td>-590.8707</td>  <td>1457.0771</td>  <td>False</td>
</tr>
<tr>
    <td>50</td>      <td>7</td>    <td>423.6207</td>    <td>0.9</td>   <td>-608.9294</td>  <td>1456.1707</td>  <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>70</td>    <td>-56.8462</td>    <td>0.9</td>   <td>-1054.876</td>  <td>941.1837</td>   <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>71</td>    <td>146.0595</td>    <td>0.9</td>   <td>-844.6694</td>  <td>1136.7884</td>  <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>72</td>    <td>288.2108</td>    <td>0.9</td>   <td>-715.3088</td>  <td>1291.7304</td>  <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>73</td>      <td>-51.0</td>     <td>0.9</td>  <td>-1216.7875</td>  <td>1114.7875</td>  <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>74</td>    <td>-153.6154</td>   <td>0.9</td>  <td>-1337.9381</td>  <td>1030.7073</td>  <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>75</td>    <td>-179.4322</td>   <td>0.9</td>  <td>-1163.7898</td>  <td>804.9254</td>   <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>76</td>     <td>48.3158</td>    <td>0.9</td>   <td>-952.3905</td>  <td>1049.0221</td>  <td>False</td>
</tr>
<tr>
    <td>50</td>     <td>77</td>    <td>-113.8378</td>   <td>0.9</td>  <td>-1117.3575</td>  <td>889.6818</td>   <td>False</td>
</tr>
<tr>
    <td>50</td>      <td>8</td>    <td>707.4615</td>    <td>0.9</td>   <td>-476.8611</td>  <td>1891.7842</td>  <td>False</td>
</tr>
<tr>
    <td>50</td>      <td>9</td>     <td>1414.4</td>   <td>0.1604</td>  <td>-127.7919</td>  <td>2956.5919</td>  <td>False</td>
</tr>
<tr>
    <td>51</td>     <td>52</td>    <td>-906.7184</td>  <td>0.001</td> <td>-1607.9782</td>  <td>-205.4586</td>  <td>True</td> 
</tr>
<tr>
    <td>51</td>     <td>53</td>    <td>-404.0615</td>   <td>0.9</td>  <td>-1098.3251</td>  <td>290.2021</td>   <td>False</td>
</tr>
<tr>
    <td>51</td>     <td>54</td>    <td>-867.8184</td>  <td>0.001</td> <td>-1522.6817</td>  <td>-212.9552</td>  <td>True</td> 
</tr>
<tr>
    <td>51</td>     <td>55</td>    <td>-418.7957</td>   <td>0.9</td>  <td>-1088.7701</td>  <td>251.1787</td>   <td>False</td>
</tr>
<tr>
    <td>51</td>     <td>56</td>    <td>-107.6444</td>   <td>0.9</td>   <td>-713.6022</td>  <td>498.3133</td>   <td>False</td>
</tr>
<tr>
    <td>51</td>     <td>57</td>    <td>-670.5989</td> <td>0.1934</td> <td>-1414.4517</td>   <td>73.2539</td>   <td>False</td>
</tr>
<tr>
    <td>51</td>     <td>58</td>    <td>-639.8045</td> <td>0.5343</td> <td>-1445.4496</td>  <td>165.8406</td>   <td>False</td>
</tr>
<tr>
    <td>51</td>     <td>59</td>     <td>235.047</td>    <td>0.9</td>   <td>-365.8577</td>  <td>835.9516</td>   <td>False</td>
</tr>
<tr>
    <td>51</td>      <td>6</td>    <td>-397.9851</td>   <td>0.9</td>  <td>-1330.3381</td>  <td>534.3679</td>   <td>False</td>
</tr>
<tr>
    <td>51</td>     <td>60</td>    <td>-72.3484</td>    <td>0.9</td>   <td>-678.3062</td>  <td>533.6093</td>   <td>False</td>
</tr>
<tr>
    <td>51</td>     <td>61</td>    <td>-444.0336</td>   <td>0.9</td>  <td>-1187.8864</td>  <td>299.8192</td>   <td>False</td>
</tr>
<tr>
    <td>51</td>     <td>62</td>    <td>-33.8152</td>    <td>0.9</td>   <td>-648.0672</td>  <td>580.4367</td>   <td>False</td>
</tr>
<tr>
    <td>51</td>     <td>63</td>     <td>30.8904</td>    <td>0.9</td>   <td>-790.6764</td>  <td>852.4572</td>   <td>False</td>
</tr>
<tr>
    <td>51</td>     <td>64</td>    <td>-365.7064</td>   <td>0.9</td>   <td>-1059.97</td>   <td>328.5573</td>   <td>False</td>
</tr>
<tr>
    <td>51</td>     <td>65</td>    <td>-593.1975</td> <td>0.2755</td> <td>-1274.6407</td>   <td>88.2458</td>   <td>False</td>
</tr>
<tr>
    <td>51</td>     <td>66</td>    <td>-570.1934</td>   <td>0.9</td>  <td>-1665.4602</td>  <td>525.0734</td>   <td>False</td>
</tr>
<tr>
    <td>51</td>     <td>67</td>    <td>-753.8684</td> <td>0.6593</td> <td>-1754.5747</td>  <td>246.8379</td>   <td>False</td>
</tr>
<tr>
    <td>51</td>     <td>68</td>    <td>-756.6593</td> <td>0.0053</td> <td>-1426.6337</td>  <td>-86.6849</td>   <td>True</td> 
</tr>
<tr>
    <td>51</td>     <td>69</td>    <td>-225.9652</td>   <td>0.9</td>   <td>-907.4085</td>  <td>455.4781</td>   <td>False</td>
</tr>
<tr>
    <td>51</td>      <td>7</td>    <td>-235.4477</td>   <td>0.9</td>   <td>-929.7114</td>  <td>458.8159</td>   <td>False</td>
</tr>
<tr>
    <td>51</td>     <td>70</td>    <td>-715.9146</td> <td>0.0069</td> <td>-1357.7136</td>  <td>-74.1155</td>   <td>True</td> 
</tr>
<tr>
    <td>51</td>     <td>71</td>    <td>-513.0089</td> <td>0.4736</td> <td>-1143.3946</td>  <td>117.3768</td>   <td>False</td>
</tr>
<tr>
    <td>51</td>     <td>72</td>    <td>-370.8576</td>   <td>0.9</td>  <td>-1021.1606</td>  <td>279.4454</td>   <td>False</td>
</tr>
<tr>
    <td>51</td>     <td>73</td>    <td>-710.0684</td> <td>0.4961</td> <td>-1590.3541</td>  <td>170.2173</td>   <td>False</td>
</tr>
<tr>
    <td>51</td>     <td>74</td>    <td>-812.6838</td> <td>0.2011</td>  <td>-1717.373</td>   <td>92.0054</td>   <td>False</td>
</tr>
<tr>
    <td>51</td>     <td>75</td>    <td>-838.5006</td>  <td>0.001</td> <td>-1458.8249</td>  <td>-218.1763</td>  <td>True</td> 
</tr>
<tr>
    <td>51</td>     <td>76</td>    <td>-610.7526</td> <td>0.1111</td> <td>-1256.7058</td>   <td>35.2005</td>   <td>False</td>
</tr>
<tr>
    <td>51</td>     <td>77</td>    <td>-772.9063</td> <td>0.0017</td> <td>-1423.2093</td>  <td>-122.6032</td>  <td>True</td> 
</tr>
<tr>
    <td>51</td>      <td>8</td>     <td>48.3931</td>    <td>0.9</td>   <td>-856.2961</td>  <td>953.0823</td>   <td>False</td>
</tr>
<tr>
    <td>51</td>      <td>9</td>    <td>755.3316</td>    <td>0.9</td>   <td>-584.1453</td>  <td>2094.8085</td>  <td>False</td>
</tr>
<tr>
    <td>52</td>     <td>53</td>    <td>502.6569</td>    <td>0.9</td>   <td>-243.3403</td>  <td>1248.6541</td>  <td>False</td>
</tr>
<tr>
    <td>52</td>     <td>54</td>      <td>38.9</td>      <td>0.9</td>   <td>-670.5757</td>  <td>748.3757</td>   <td>False</td>
</tr>
<tr>
    <td>52</td>     <td>55</td>    <td>487.9227</td>    <td>0.9</td>   <td>-235.5243</td>  <td>1211.3698</td>  <td>False</td>
</tr>
<tr>
    <td>52</td>     <td>56</td>     <td>799.074</td>  <td>0.0013</td>  <td>134.4729</td>   <td>1463.6751</td>  <td>True</td> 
</tr>
<tr>
    <td>52</td>     <td>57</td>    <td>236.1196</td>    <td>0.9</td>   <td>-556.2357</td>  <td>1028.4748</td>  <td>False</td>
</tr>
<tr>
    <td>52</td>     <td>58</td>    <td>266.9139</td>    <td>0.9</td>   <td>-583.7176</td>  <td>1117.5454</td>  <td>False</td>
</tr>
<tr>
    <td>52</td>     <td>59</td>    <td>1141.7654</td>  <td>0.001</td>  <td>481.7682</td>   <td>1801.7626</td>  <td>True</td> 
</tr>
<tr>
    <td>52</td>      <td>6</td>    <td>508.7333</td>    <td>0.9</td>   <td>-462.7563</td>  <td>1480.2229</td>  <td>False</td>
</tr>
<tr>
    <td>52</td>     <td>60</td>     <td>834.37</td>    <td>0.001</td>  <td>169.7689</td>   <td>1498.9711</td>  <td>True</td> 
</tr>
<tr>
    <td>52</td>     <td>61</td>    <td>462.6848</td>    <td>0.9</td>   <td>-329.6705</td>  <td>1255.0401</td>  <td>False</td>
</tr>
<tr>
    <td>52</td>     <td>62</td>    <td>872.9032</td>   <td>0.001</td>  <td>200.7311</td>   <td>1545.0753</td>  <td>True</td> 
</tr>
<tr>
    <td>52</td>     <td>63</td>    <td>937.6088</td>  <td>0.0126</td>   <td>71.8826</td>   <td>1803.3351</td>  <td>True</td> 
</tr>
<tr>
    <td>52</td>     <td>64</td>    <td>541.0121</td>  <td>0.7455</td>  <td>-204.9852</td>  <td>1287.0093</td>  <td>False</td>
</tr>
<tr>
    <td>52</td>     <td>65</td>     <td>313.521</td>    <td>0.9</td>    <td>-420.56</td>   <td>1047.6019</td>  <td>False</td>
</tr>
<tr>
    <td>52</td>     <td>66</td>     <td>336.525</td>    <td>0.9</td>   <td>-792.2439</td>  <td>1465.2939</td>  <td>False</td>
</tr>
<tr>
    <td>52</td>     <td>67</td>     <td>152.85</td>     <td>0.9</td>   <td>-884.4171</td>  <td>1190.1171</td>  <td>False</td>
</tr>
<tr>
    <td>52</td>     <td>68</td>    <td>150.0591</td>    <td>0.9</td>   <td>-573.3879</td>  <td>873.5061</td>   <td>False</td>
</tr>
<tr>
    <td>52</td>     <td>69</td>    <td>680.7532</td>  <td>0.1396</td>  <td>-53.3277</td>   <td>1414.8342</td>  <td>False</td>
</tr>
<tr>
    <td>52</td>      <td>7</td>    <td>671.2707</td>  <td>0.1974</td>  <td>-74.7265</td>   <td>1417.2679</td>  <td>False</td>
</tr>
<tr>
    <td>52</td>     <td>70</td>    <td>190.8038</td>    <td>0.9</td>   <td>-506.6314</td>  <td>888.2391</td>   <td>False</td>
</tr>
<tr>
    <td>52</td>     <td>71</td>    <td>393.7095</td>    <td>0.9</td>   <td>-293.2374</td>  <td>1080.6564</td>  <td>False</td>
</tr>
<tr>
    <td>52</td>     <td>72</td>    <td>535.8608</td>  <td>0.6395</td>  <td>-169.4079</td>  <td>1241.1295</td>  <td>False</td>
</tr>
<tr>
    <td>52</td>     <td>73</td>     <td>196.65</td>     <td>0.9</td>   <td>-724.986</td>   <td>1118.286</td>   <td>False</td>
</tr>
<tr>
    <td>52</td>     <td>74</td>     <td>94.0346</td>    <td>0.9</td>   <td>-850.9376</td>  <td>1039.0068</td>  <td>False</td>
</tr>
<tr>
    <td>52</td>     <td>75</td>     <td>68.2178</td>    <td>0.9</td>   <td>-609.5079</td>  <td>745.9435</td>   <td>False</td>
</tr>
<tr>
    <td>52</td>     <td>76</td>    <td>295.9658</td>    <td>0.9</td>   <td>-405.294</td>   <td>997.2256</td>   <td>False</td>
</tr>
<tr>
    <td>52</td>     <td>77</td>    <td>133.8122</td>    <td>0.9</td>   <td>-571.4565</td>  <td>839.0809</td>   <td>False</td>
</tr>
<tr>
    <td>52</td>      <td>8</td>    <td>955.1115</td>  <td>0.0425</td>   <td>10.1393</td>   <td>1900.0838</td>  <td>True</td> 
</tr>
<tr>
    <td>52</td>      <td>9</td>     <td>1662.05</td>   <td>0.001</td>  <td>295.0429</td>   <td>3029.0571</td>  <td>True</td> 
</tr>
<tr>
    <td>53</td>     <td>54</td>    <td>-463.7569</td>   <td>0.9</td>  <td>-1166.3182</td>  <td>238.8044</td>   <td>False</td>
</tr>
<tr>
    <td>53</td>     <td>55</td>    <td>-14.7342</td>    <td>0.9</td>   <td>-731.4016</td>  <td>701.9333</td>   <td>False</td>
</tr>
<tr>
    <td>53</td>     <td>56</td>    <td>296.4171</td>    <td>0.9</td>   <td>-360.7977</td>  <td>953.6319</td>   <td>False</td>
</tr>
<tr>
    <td>53</td>     <td>57</td>    <td>-266.5373</td>   <td>0.9</td>  <td>-1052.7075</td>  <td>519.6328</td>   <td>False</td>
</tr>
<tr>
    <td>53</td>     <td>58</td>    <td>-235.743</td>    <td>0.9</td>  <td>-1080.6161</td>  <td>609.1301</td>   <td>False</td>
</tr>
<tr>
    <td>53</td>     <td>59</td>    <td>639.1085</td>  <td>0.0692</td>  <td>-13.4503</td>   <td>1291.6673</td>  <td>False</td>
</tr>
<tr>
    <td>53</td>      <td>6</td>     <td>6.0764</td>     <td>0.9</td>   <td>-960.3752</td>   <td>972.528</td>   <td>False</td>
</tr>
<tr>
    <td>53</td>     <td>60</td>    <td>331.7131</td>    <td>0.9</td>   <td>-325.5017</td>  <td>988.9279</td>   <td>False</td>
</tr>
<tr>
    <td>53</td>     <td>61</td>    <td>-39.9721</td>    <td>0.9</td>   <td>-826.1423</td>  <td>746.1981</td>   <td>False</td>
</tr>
<tr>
    <td>53</td>     <td>62</td>    <td>370.2463</td>    <td>0.9</td>   <td>-294.6236</td>  <td>1035.1162</td>  <td>False</td>
</tr>
<tr>
    <td>53</td>     <td>63</td>    <td>434.9519</td>    <td>0.9</td>   <td>-425.117</td>   <td>1295.0209</td>  <td>False</td>
</tr>
<tr>
    <td>53</td>     <td>64</td>     <td>38.3552</td>    <td>0.9</td>   <td>-701.0693</td>  <td>777.7796</td>   <td>False</td>
</tr>
<tr>
    <td>53</td>     <td>65</td>    <td>-189.1359</td>   <td>0.9</td>   <td>-916.5364</td>  <td>538.2646</td>   <td>False</td>
</tr>
<tr>
    <td>53</td>     <td>66</td>    <td>-166.1319</td>   <td>0.9</td>  <td>-1290.5677</td>  <td>958.3039</td>   <td>False</td>
</tr>
<tr>
    <td>53</td>     <td>67</td>    <td>-349.8069</td>   <td>0.9</td>  <td>-1382.3569</td>  <td>682.7431</td>   <td>False</td>
</tr>
<tr>
    <td>53</td>     <td>68</td>    <td>-352.5978</td>   <td>0.9</td>  <td>-1069.2653</td>  <td>364.0696</td>   <td>False</td>
</tr>
<tr>
    <td>53</td>     <td>69</td>    <td>178.0963</td>    <td>0.9</td>   <td>-549.3042</td>  <td>905.4968</td>   <td>False</td>
</tr>
<tr>
    <td>53</td>      <td>7</td>    <td>168.6138</td>    <td>0.9</td>   <td>-570.8106</td>  <td>908.0382</td>   <td>False</td>
</tr>
<tr>
    <td>53</td>     <td>70</td>    <td>-311.8531</td>   <td>0.9</td>  <td>-1002.2533</td>  <td>378.5472</td>   <td>False</td>
</tr>
<tr>
    <td>53</td>     <td>71</td>    <td>-108.9474</td>   <td>0.9</td>   <td>-788.7508</td>   <td>570.856</td>   <td>False</td>
</tr>
<tr>
    <td>53</td>     <td>72</td>     <td>33.2039</td>    <td>0.9</td>   <td>-665.1087</td>  <td>731.5166</td>   <td>False</td>
</tr>
<tr>
    <td>53</td>     <td>73</td>    <td>-306.0069</td>   <td>0.9</td>  <td>-1222.3308</td>   <td>610.317</td>   <td>False</td>
</tr>
<tr>
    <td>53</td>     <td>74</td>    <td>-408.6223</td>   <td>0.9</td>  <td>-1348.4143</td>  <td>531.1698</td>   <td>False</td>
</tr>
<tr>
    <td>53</td>     <td>75</td>    <td>-434.4391</td>   <td>0.9</td>  <td>-1104.9231</td>  <td>236.0449</td>   <td>False</td>
</tr>
<tr>
    <td>53</td>     <td>76</td>    <td>-206.6911</td>   <td>0.9</td>   <td>-900.9547</td>  <td>487.5725</td>   <td>False</td>
</tr>
<tr>
    <td>53</td>     <td>77</td>    <td>-368.8447</td>   <td>0.9</td>  <td>-1067.1574</td>  <td>329.4679</td>   <td>False</td>
</tr>
<tr>
    <td>53</td>      <td>8</td>    <td>452.4546</td>    <td>0.9</td>   <td>-487.3374</td>  <td>1392.2467</td>  <td>False</td>
</tr>
<tr>
    <td>53</td>      <td>9</td>    <td>1159.3931</td> <td>0.3387</td>  <td>-204.0382</td>  <td>2522.8244</td>  <td>False</td>
</tr>
<tr>
    <td>54</td>     <td>55</td>    <td>449.0227</td>    <td>0.9</td>   <td>-229.5464</td>  <td>1127.5919</td>  <td>False</td>
</tr>
<tr>
    <td>54</td>     <td>56</td>     <td>760.174</td>   <td>0.001</td>  <td>144.7268</td>   <td>1375.6212</td>  <td>True</td> 
</tr>
<tr>
    <td>54</td>     <td>57</td>    <td>197.2196</td>    <td>0.9</td>   <td>-554.3837</td>  <td>948.8228</td>   <td>False</td>
</tr>
<tr>
    <td>54</td>     <td>58</td>    <td>228.0139</td>    <td>0.9</td>   <td>-584.7926</td>  <td>1040.8204</td>  <td>False</td>
</tr>
<tr>
    <td>54</td>     <td>59</td>    <td>1102.8654</td>  <td>0.001</td>  <td>492.3927</td>   <td>1713.338</td>   <td>True</td> 
</tr>
<tr>
    <td>54</td>      <td>6</td>    <td>469.8333</td>    <td>0.9</td>   <td>-468.7148</td>  <td>1408.3815</td>  <td>False</td>
</tr>
<tr>
    <td>54</td>     <td>60</td>     <td>795.47</td>    <td>0.001</td>  <td>180.0228</td>   <td>1410.9172</td>  <td>True</td> 
</tr>
<tr>
    <td>54</td>     <td>61</td>    <td>423.7848</td>    <td>0.9</td>   <td>-327.8185</td>  <td>1175.388</td>   <td>False</td>
</tr>
<tr>
    <td>54</td>     <td>62</td>    <td>834.0032</td>   <td>0.001</td>   <td>210.388</td>   <td>1457.6184</td>  <td>True</td> 
</tr>
<tr>
    <td>54</td>     <td>63</td>    <td>898.7088</td>  <td>0.0122</td>   <td>70.1182</td>   <td>1727.2995</td>  <td>True</td> 
</tr>
<tr>
    <td>54</td>     <td>64</td>    <td>502.1121</td>  <td>0.7777</td>  <td>-200.4492</td>  <td>1204.6734</td>  <td>False</td>
</tr>
<tr>
    <td>54</td>     <td>65</td>     <td>274.621</td>    <td>0.9</td>   <td>-415.2742</td>  <td>964.5161</td>   <td>False</td>
</tr>
<tr>
    <td>54</td>     <td>66</td>     <td>297.625</td>    <td>0.9</td>   <td>-802.9202</td>  <td>1398.1702</td>  <td>False</td>
</tr>
<tr>
    <td>54</td>     <td>67</td>     <td>113.95</td>     <td>0.9</td>   <td>-892.5307</td>  <td>1120.4307</td>  <td>False</td>
</tr>
<tr>
    <td>54</td>     <td>68</td>    <td>111.1591</td>    <td>0.9</td>   <td>-567.4101</td>  <td>789.7283</td>   <td>False</td>
</tr>
<tr>
    <td>54</td>     <td>69</td>    <td>641.8532</td>   <td>0.134</td>  <td>-48.0419</td>   <td>1331.7484</td>  <td>False</td>
</tr>
<tr>
    <td>54</td>      <td>7</td>    <td>632.3707</td>  <td>0.1968</td>  <td>-70.1906</td>   <td>1334.932</td>   <td>False</td>
</tr>
<tr>
    <td>54</td>     <td>70</td>    <td>151.9038</td>    <td>0.9</td>   <td>-498.8622</td>  <td>802.6699</td>   <td>False</td>
</tr>
<tr>
    <td>54</td>     <td>71</td>    <td>354.8095</td>    <td>0.9</td>   <td>-284.7032</td>  <td>994.3223</td>   <td>False</td>
</tr>
<tr>
    <td>54</td>     <td>72</td>    <td>496.9608</td>  <td>0.6575</td>  <td>-162.1935</td>  <td>1156.1152</td>  <td>False</td>
</tr>
<tr>
    <td>54</td>     <td>73</td>     <td>157.75</td>     <td>0.9</td>   <td>-729.0946</td>  <td>1044.5946</td>  <td>False</td>
</tr>
<tr>
    <td>54</td>     <td>74</td>     <td>55.1346</td>    <td>0.9</td>   <td>-855.9378</td>  <td>966.2071</td>   <td>False</td>
</tr>
<tr>
    <td>54</td>     <td>75</td>     <td>29.3178</td>    <td>0.9</td>   <td>-600.2794</td>   <td>658.915</td>   <td>False</td>
</tr>
<tr>
    <td>54</td>     <td>76</td>    <td>257.0658</td>    <td>0.9</td>   <td>-397.7975</td>   <td>911.929</td>   <td>False</td>
</tr>
<tr>
    <td>54</td>     <td>77</td>     <td>94.9122</td>    <td>0.9</td>   <td>-564.2422</td>  <td>754.0665</td>   <td>False</td>
</tr>
<tr>
    <td>54</td>      <td>8</td>    <td>916.2115</td>   <td>0.046</td>   <td>5.1391</td>    <td>1827.284</td>   <td>True</td> 
</tr>
<tr>
    <td>54</td>      <td>9</td>     <td>1623.15</td>  <td>0.0011</td>  <td>279.3536</td>   <td>2966.9464</td>  <td>True</td> 
</tr>
<tr>
    <td>55</td>     <td>56</td>    <td>311.1513</td>    <td>0.9</td>   <td>-320.3509</td>  <td>942.6535</td>   <td>False</td>
</tr>
<tr>
    <td>55</td>     <td>57</td>    <td>-251.8032</td>   <td>0.9</td>  <td>-1016.6085</td>  <td>513.0022</td>   <td>False</td>
</tr>
<tr>
    <td>55</td>     <td>58</td>    <td>-221.0088</td>   <td>0.9</td>  <td>-1046.0387</td>   <td>604.021</td>   <td>False</td>
</tr>
<tr>
    <td>55</td>     <td>59</td>    <td>653.8427</td>  <td>0.0249</td>   <td>27.1875</td>   <td>1280.4978</td>  <td>True</td> 
</tr>
<tr>
    <td>55</td>      <td>6</td>     <td>20.8106</td>    <td>0.9</td>   <td>-928.3429</td>  <td>969.9641</td>   <td>False</td>
</tr>
<tr>
    <td>55</td>     <td>60</td>    <td>346.4473</td>    <td>0.9</td>   <td>-285.0549</td>  <td>977.9495</td>   <td>False</td>
</tr>
<tr>
    <td>55</td>     <td>61</td>    <td>-25.2379</td>    <td>0.9</td>   <td>-790.0433</td>  <td>739.5674</td>   <td>False</td>
</tr>
<tr>
    <td>55</td>     <td>62</td>    <td>384.9805</td>    <td>0.9</td>   <td>-254.4847</td>  <td>1024.4456</td>  <td>False</td>
</tr>
<tr>
    <td>55</td>     <td>63</td>    <td>449.6861</td>    <td>0.9</td>   <td>-390.8984</td>  <td>1290.2706</td>  <td>False</td>
</tr>
<tr>
    <td>55</td>     <td>64</td>     <td>53.0893</td>    <td>0.9</td>   <td>-663.5781</td>  <td>769.7568</td>   <td>False</td>
</tr>
<tr>
    <td>55</td>     <td>65</td>    <td>-174.4018</td>   <td>0.9</td>   <td>-878.6568</td>  <td>529.8533</td>   <td>False</td>
</tr>
<tr>
    <td>55</td>     <td>66</td>    <td>-151.3977</td>   <td>0.9</td>  <td>-1261.0011</td>  <td>958.2056</td>   <td>False</td>
</tr>
<tr>
    <td>55</td>     <td>67</td>    <td>-335.0727</td>   <td>0.9</td>  <td>-1351.4503</td>  <td>681.3048</td>   <td>False</td>
</tr>
<tr>
    <td>55</td>     <td>68</td>    <td>-337.8636</td>   <td>0.9</td>  <td>-1031.0274</td>  <td>355.3001</td>   <td>False</td>
</tr>
<tr>
    <td>55</td>     <td>69</td>    <td>192.8305</td>    <td>0.9</td>   <td>-511.4246</td>  <td>897.0856</td>   <td>False</td>
</tr>
<tr>
    <td>55</td>      <td>7</td>     <td>183.348</td>    <td>0.9</td>   <td>-533.3195</td>  <td>900.0154</td>   <td>False</td>
</tr>
<tr>
    <td>55</td>     <td>70</td>    <td>-297.1189</td>   <td>0.9</td>   <td>-963.0891</td>  <td>368.8513</td>   <td>False</td>
</tr>
<tr>
    <td>55</td>     <td>71</td>    <td>-94.2132</td>    <td>0.9</td>   <td>-749.1914</td>   <td>560.765</td>   <td>False</td>
</tr>
<tr>
    <td>55</td>     <td>72</td>     <td>47.9381</td>    <td>0.9</td>   <td>-626.2312</td>  <td>722.1074</td>   <td>False</td>
</tr>
<tr>
    <td>55</td>     <td>73</td>    <td>-291.2727</td>   <td>0.9</td>  <td>-1189.3335</td>  <td>606.7881</td>   <td>False</td>
</tr>
<tr>
    <td>55</td>     <td>74</td>    <td>-393.8881</td>   <td>0.9</td>  <td>-1315.8821</td>  <td>528.1058</td>   <td>False</td>
</tr>
<tr>
    <td>55</td>     <td>75</td>    <td>-419.7049</td>   <td>0.9</td>  <td>-1065.0053</td>  <td>225.5954</td>   <td>False</td>
</tr>
<tr>
    <td>55</td>     <td>76</td>    <td>-191.9569</td>   <td>0.9</td>   <td>-861.9313</td>  <td>478.0175</td>   <td>False</td>
</tr>
<tr>
    <td>55</td>     <td>77</td>    <td>-354.1106</td>   <td>0.9</td>  <td>-1028.2799</td>  <td>320.0588</td>   <td>False</td>
</tr>
<tr>
    <td>55</td>      <td>8</td>    <td>467.1888</td>    <td>0.9</td>   <td>-454.8051</td>  <td>1389.1828</td>  <td>False</td>
</tr>
<tr>
    <td>55</td>      <td>9</td>    <td>1174.1273</td> <td>0.2802</td>  <td>-177.0976</td>  <td>2525.3521</td>  <td>False</td>
</tr>
<tr>
    <td>56</td>     <td>57</td>    <td>-562.9544</td> <td>0.5361</td>  <td>-1272.353</td>  <td>146.4441</td>   <td>False</td>
</tr>
<tr>
    <td>56</td>     <td>58</td>    <td>-532.1601</td> <td>0.8608</td> <td>-1306.1067</td>  <td>241.7865</td>   <td>False</td>
</tr>
<tr>
    <td>56</td>     <td>59</td>    <td>342.6914</td>    <td>0.9</td>   <td>-214.9965</td>  <td>900.3793</td>   <td>False</td>
</tr>
<tr>
    <td>56</td>      <td>6</td>    <td>-290.3407</td>   <td>0.9</td>  <td>-1195.4437</td>  <td>614.7624</td>   <td>False</td>
</tr>
<tr>
    <td>56</td>     <td>60</td>     <td>35.296</td>     <td>0.9</td>   <td>-527.8329</td>  <td>598.4249</td>   <td>False</td>
</tr>
<tr>
    <td>56</td>     <td>61</td>    <td>-336.3892</td>   <td>0.9</td>  <td>-1045.7878</td>  <td>373.0094</td>   <td>False</td>
</tr>
<tr>
    <td>56</td>     <td>62</td>     <td>73.8292</td>    <td>0.9</td>   <td>-498.2152</td>  <td>645.8736</td>   <td>False</td>
</tr>
<tr>
    <td>56</td>     <td>63</td>    <td>138.5348</td>    <td>0.9</td>   <td>-651.9722</td>  <td>929.0419</td>   <td>False</td>
</tr>
<tr>
    <td>56</td>     <td>64</td>    <td>-258.0619</td>   <td>0.9</td>   <td>-915.2768</td>  <td>399.1529</td>   <td>False</td>
</tr>
<tr>
    <td>56</td>     <td>65</td>    <td>-485.553</td>  <td>0.6562</td>  <td>-1129.21</td>   <td>158.1039</td>   <td>False</td>
</tr>
<tr>
    <td>56</td>     <td>66</td>    <td>-462.549</td>    <td>0.9</td>  <td>-1534.7144</td>  <td>609.6164</td>   <td>False</td>
</tr>
<tr>
    <td>56</td>     <td>67</td>    <td>-646.224</td>    <td>0.9</td>  <td>-1621.5918</td>  <td>329.1438</td>   <td>False</td>
</tr>
<tr>
    <td>56</td>     <td>68</td>    <td>-649.0149</td> <td>0.0323</td> <td>-1280.5171</td>  <td>-17.5127</td>   <td>True</td> 
</tr>
<tr>
    <td>56</td>     <td>69</td>    <td>-118.3208</td>   <td>0.9</td>   <td>-761.9777</td>  <td>525.3362</td>   <td>False</td>
</tr>
<tr>
    <td>56</td>      <td>7</td>    <td>-127.8033</td>   <td>0.9</td>   <td>-785.0181</td>  <td>529.4115</td>   <td>False</td>
</tr>
<tr>
    <td>56</td>     <td>70</td>    <td>-608.2702</td> <td>0.0422</td> <td>-1209.7977</td>   <td>-6.7426</td>   <td>True</td> 
</tr>
<tr>
    <td>56</td>     <td>71</td>    <td>-405.3645</td>  <td>0.86</td>   <td>-994.6993</td>  <td>183.9703</td>   <td>False</td>
</tr>
<tr>
    <td>56</td>     <td>72</td>    <td>-263.2132</td>   <td>0.9</td>   <td>-873.8058</td>  <td>347.3795</td>   <td>False</td>
</tr>
<tr>
    <td>56</td>     <td>73</td>    <td>-602.424</td>  <td>0.7995</td> <td>-1453.7948</td>  <td>248.9468</td>   <td>False</td>
</tr>
<tr>
    <td>56</td>     <td>74</td>    <td>-705.0394</td> <td>0.5032</td> <td>-1581.6191</td>  <td>171.5403</td>   <td>False</td>
</tr>
<tr>
    <td>56</td>     <td>75</td>    <td>-730.8562</td>  <td>0.001</td> <td>-1309.4161</td>  <td>-152.2963</td>  <td>True</td> 
</tr>
<tr>
    <td>56</td>     <td>76</td>    <td>-503.1082</td>  <td>0.415</td>  <td>-1109.066</td>  <td>102.8495</td>   <td>False</td>
</tr>
<tr>
    <td>56</td>     <td>77</td>    <td>-665.2618</td> <td>0.0112</td> <td>-1275.8545</td>  <td>-54.6692</td>   <td>True</td> 
</tr>
<tr>
    <td>56</td>      <td>8</td>    <td>156.0375</td>    <td>0.9</td>   <td>-720.5421</td>  <td>1032.6172</td>  <td>False</td>
</tr>
<tr>
    <td>56</td>      <td>9</td>     <td>862.976</td>    <td>0.9</td>   <td>-457.6783</td>  <td>2183.6303</td>  <td>False</td>
</tr>
<tr>
    <td>57</td>     <td>58</td>     <td>30.7943</td>    <td>0.9</td>   <td>-855.2788</td>  <td>916.8674</td>   <td>False</td>
</tr>
<tr>
    <td>57</td>     <td>59</td>    <td>905.6458</td>   <td>0.001</td>  <td>200.5586</td>   <td>1610.733</td>   <td>True</td> 
</tr>
<tr>
    <td>57</td>      <td>6</td>    <td>272.6138</td>    <td>0.9</td>   <td>-730.0545</td>  <td>1275.2821</td>  <td>False</td>
</tr>
<tr>
    <td>57</td>     <td>60</td>    <td>598.2504</td>  <td>0.3649</td>  <td>-111.1481</td>  <td>1307.649</td>   <td>False</td>
</tr>
<tr>
    <td>57</td>     <td>61</td>    <td>226.5652</td>    <td>0.9</td>   <td>-603.723</td>   <td>1056.8535</td>  <td>False</td>
</tr>
<tr>
    <td>57</td>     <td>62</td>    <td>636.7836</td>  <td>0.2252</td>  <td>-79.7127</td>    <td>1353.28</td>   <td>False</td>
</tr>
<tr>
    <td>57</td>     <td>63</td>    <td>701.4893</td>  <td>0.5809</td>  <td>-199.0848</td>  <td>1602.0633</td>  <td>False</td>
</tr>
<tr>
    <td>57</td>     <td>64</td>    <td>304.8925</td>    <td>0.9</td>   <td>-481.2777</td>  <td>1091.0627</td>  <td>False</td>
</tr>
<tr>
    <td>57</td>     <td>65</td>     <td>77.4014</td>    <td>0.9</td>   <td>-697.4705</td>  <td>852.2733</td>   <td>False</td>
</tr>
<tr>
    <td>57</td>     <td>66</td>    <td>100.4054</td>    <td>0.9</td>  <td>-1055.3069</td>  <td>1256.1177</td>  <td>False</td>
</tr>
<tr>
    <td>57</td>     <td>67</td>    <td>-83.2696</td>    <td>0.9</td>  <td>-1149.7941</td>   <td>983.255</td>   <td>False</td>
</tr>
<tr>
    <td>57</td>     <td>68</td>    <td>-86.0605</td>    <td>0.9</td>   <td>-850.8658</td>  <td>678.7449</td>   <td>False</td>
</tr>
<tr>
    <td>57</td>     <td>69</td>    <td>444.6337</td>    <td>0.9</td>   <td>-330.2383</td>  <td>1219.5056</td>  <td>False</td>
</tr>
<tr>
    <td>57</td>      <td>7</td>    <td>435.1511</td>    <td>0.9</td>   <td>-351.019</td>   <td>1221.3213</td>  <td>False</td>
</tr>
<tr>
    <td>57</td>     <td>70</td>    <td>-45.3157</td>    <td>0.9</td>   <td>-785.564</td>   <td>694.9326</td>   <td>False</td>
</tr>
<tr>
    <td>57</td>     <td>71</td>     <td>157.59</td>     <td>0.9</td>   <td>-572.7851</td>   <td>887.965</td>   <td>False</td>
</tr>
<tr>
    <td>57</td>     <td>72</td>    <td>299.7412</td>    <td>0.9</td>   <td>-447.8921</td>  <td>1047.3746</td>  <td>False</td>
</tr>
<tr>
    <td>57</td>     <td>73</td>    <td>-39.4696</td>    <td>0.9</td>   <td>-993.9142</td>   <td>914.975</td>   <td>False</td>
</tr>
<tr>
    <td>57</td>     <td>74</td>    <td>-142.0849</td>   <td>0.9</td>  <td>-1119.0825</td>  <td>834.9126</td>   <td>False</td>
</tr>
<tr>
    <td>57</td>     <td>75</td>    <td>-167.9018</td>   <td>0.9</td>   <td>-889.6107</td>  <td>553.8072</td>   <td>False</td>
</tr>
<tr>
    <td>57</td>     <td>76</td>     <td>59.8462</td>    <td>0.9</td>   <td>-684.0066</td>   <td>803.699</td>   <td>False</td>
</tr>
<tr>
    <td>57</td>     <td>77</td>    <td>-102.3074</td>   <td>0.9</td>   <td>-849.9407</td>  <td>645.3259</td>   <td>False</td>
</tr>
<tr>
    <td>57</td>      <td>8</td>     <td>718.992</td>  <td>0.7127</td>  <td>-258.0055</td>  <td>1695.9895</td>  <td>False</td>
</tr>
<tr>
    <td>57</td>      <td>9</td>    <td>1425.9304</td> <td>0.0331</td>   <td>36.5925</td>   <td>2815.2684</td>  <td>True</td> 
</tr>
<tr>
    <td>58</td>     <td>59</td>    <td>874.8515</td>  <td>0.0047</td>  <td>104.8547</td>   <td>1644.8483</td>  <td>True</td> 
</tr>
<tr>
    <td>58</td>      <td>6</td>    <td>241.8194</td>    <td>0.9</td>   <td>-807.5093</td>  <td>1291.1482</td>  <td>False</td>
</tr>
<tr>
    <td>58</td>     <td>60</td>    <td>567.4561</td>   <td>0.721</td>  <td>-206.4905</td>  <td>1341.4027</td>  <td>False</td>
</tr>
<tr>
    <td>58</td>     <td>61</td>    <td>195.7709</td>    <td>0.9</td>   <td>-690.3022</td>  <td>1081.844</td>   <td>False</td>
</tr>
<tr>
    <td>58</td>     <td>62</td>    <td>605.9893</td>  <td>0.5885</td>  <td>-174.4683</td>  <td>1386.4469</td>  <td>False</td>
</tr>
<tr>
    <td>58</td>     <td>63</td>    <td>670.6949</td>  <td>0.8095</td>  <td>-281.5554</td>  <td>1622.9452</td>  <td>False</td>
</tr>
<tr>
    <td>58</td>     <td>64</td>    <td>274.0982</td>    <td>0.9</td>   <td>-570.7749</td>  <td>1118.9713</td>  <td>False</td>
</tr>
<tr>
    <td>58</td>     <td>65</td>     <td>46.6071</td>    <td>0.9</td>   <td>-787.763</td>   <td>880.9772</td>   <td>False</td>
</tr>
<tr>
    <td>58</td>     <td>66</td>     <td>69.6111</td>    <td>0.9</td>  <td>-1126.8077</td>  <td>1266.0299</td>  <td>False</td>
</tr>
<tr>
    <td>58</td>     <td>67</td>    <td>-114.0639</td>   <td>0.9</td>   <td>-1224.569</td>  <td>996.4412</td>   <td>False</td>
</tr>
<tr>
    <td>58</td>     <td>68</td>    <td>-116.8548</td>   <td>0.9</td>   <td>-941.8847</td>  <td>708.1751</td>   <td>False</td>
</tr>
<tr>
    <td>58</td>     <td>69</td>    <td>413.8393</td>    <td>0.9</td>   <td>-420.5308</td>  <td>1248.2095</td>  <td>False</td>
</tr>
<tr>
    <td>58</td>      <td>7</td>    <td>404.3568</td>    <td>0.9</td>   <td>-440.5163</td>  <td>1249.2299</td>  <td>False</td>
</tr>
<tr>
    <td>58</td>     <td>70</td>     <td>-76.11</td>     <td>0.9</td>   <td>-878.4283</td>  <td>726.2082</td>   <td>False</td>
</tr>
<tr>
    <td>58</td>     <td>71</td>    <td>126.7956</td>    <td>0.9</td>   <td>-666.4223</td>  <td>920.0136</td>   <td>False</td>
</tr>
<tr>
    <td>58</td>     <td>72</td>    <td>268.9469</td>    <td>0.9</td>    <td>-540.19</td>   <td>1078.0839</td>  <td>False</td>
</tr>
<tr>
    <td>58</td>     <td>73</td>    <td>-70.2639</td>    <td>0.9</td>   <td>-1073.614</td>  <td>933.0863</td>   <td>False</td>
</tr>
<tr>
    <td>58</td>     <td>74</td>    <td>-172.8793</td>   <td>0.9</td>  <td>-1197.7067</td>  <td>851.9481</td>   <td>False</td>
</tr>
<tr>
    <td>58</td>     <td>75</td>    <td>-198.6961</td>   <td>0.9</td>   <td>-983.9418</td>  <td>586.5496</td>   <td>False</td>
</tr>
<tr>
    <td>58</td>     <td>76</td>     <td>29.0519</td>    <td>0.9</td>   <td>-776.5932</td>   <td>834.697</td>   <td>False</td>
</tr>
<tr>
    <td>58</td>     <td>77</td>    <td>-133.1017</td>   <td>0.9</td>   <td>-942.2387</td>  <td>676.0352</td>   <td>False</td>
</tr>
<tr>
    <td>58</td>      <td>8</td>    <td>688.1976</td>    <td>0.9</td>   <td>-336.6297</td>  <td>1713.025</td>   <td>False</td>
</tr>
<tr>
    <td>58</td>      <td>9</td>    <td>1395.1361</td> <td>0.0683</td>  <td>-28.2426</td>   <td>2818.5148</td>  <td>False</td>
</tr>
<tr>
    <td>59</td>      <td>6</td>    <td>-633.0321</td> <td>0.8165</td> <td>-1534.7599</td>  <td>268.6958</td>   <td>False</td>
</tr>
<tr>
    <td>59</td>     <td>60</td>    <td>-307.3954</td>   <td>0.9</td>   <td>-865.0833</td>  <td>250.2925</td>   <td>False</td>
</tr>
<tr>
    <td>59</td>     <td>61</td>    <td>-679.0806</td> <td>0.0875</td> <td>-1384.1678</td>   <td>26.0066</td>   <td>False</td>
</tr>
<tr>
    <td>59</td>     <td>62</td>    <td>-268.8622</td>   <td>0.9</td>   <td>-835.5512</td>  <td>297.8268</td>   <td>False</td>
</tr>
<tr>
    <td>59</td>     <td>63</td>    <td>-204.1566</td>   <td>0.9</td>   <td>-990.7969</td>  <td>582.4838</td>   <td>False</td>
</tr>
<tr>
    <td>59</td>     <td>64</td>    <td>-600.7533</td> <td>0.1532</td> <td>-1253.3121</td>   <td>51.8055</td>   <td>False</td>
</tr>
<tr>
    <td>59</td>     <td>65</td>    <td>-828.2444</td>  <td>0.001</td> <td>-1467.1465</td>  <td>-189.3423</td>  <td>True</td> 
</tr>
<tr>
    <td>59</td>     <td>66</td>    <td>-805.2404</td> <td>0.6602</td> <td>-1874.5581</td>  <td>264.0773</td>   <td>False</td>
</tr>
<tr>
    <td>59</td>     <td>67</td>    <td>-988.9154</td> <td>0.0384</td>  <td>-1961.152</td>  <td>-16.6788</td>   <td>True</td> 
</tr>
<tr>
    <td>59</td>     <td>68</td>    <td>-991.7063</td>  <td>0.001</td> <td>-1618.3615</td>  <td>-365.0511</td>  <td>True</td> 
</tr>
<tr>
    <td>59</td>     <td>69</td>    <td>-461.0122</td> <td>0.7567</td> <td>-1099.9143</td>   <td>177.89</td>    <td>False</td>
</tr>
<tr>
    <td>59</td>      <td>7</td>    <td>-470.4947</td> <td>0.7584</td> <td>-1123.0535</td>  <td>182.0641</td>   <td>False</td>
</tr>
<tr>
    <td>59</td>     <td>70</td>    <td>-950.9615</td>  <td>0.001</td> <td>-1547.3985</td>  <td>-354.5246</td>  <td>True</td> 
</tr>
<tr>
    <td>59</td>     <td>71</td>    <td>-748.0559</td>  <td>0.001</td> <td>-1332.1938</td>  <td>-163.9179</td>  <td>True</td> 
</tr>
<tr>
    <td>59</td>     <td>72</td>    <td>-605.9046</td> <td>0.0496</td> <td>-1211.4828</td>   <td>-0.3263</td>   <td>True</td> 
</tr>
<tr>
    <td>59</td>     <td>73</td>    <td>-945.1154</td>  <td>0.007</td> <td>-1792.8972</td>  <td>-97.3336</td>   <td>True</td> 
</tr>
<tr>
    <td>59</td>     <td>74</td>   <td>-1047.7308</td> <td>0.0013</td>  <td>-1920.825</td>  <td>-174.6365</td>  <td>True</td> 
</tr>
<tr>
    <td>59</td>     <td>75</td>   <td>-1073.5476</td>  <td>0.001</td>  <td>-1646.813</td>  <td>-500.2822</td>  <td>True</td> 
</tr>
<tr>
    <td>59</td>     <td>76</td>    <td>-845.7996</td>  <td>0.001</td> <td>-1446.7043</td>  <td>-244.8949</td>  <td>True</td> 
</tr>
<tr>
    <td>59</td>     <td>77</td>   <td>-1007.9532</td>  <td>0.001</td> <td>-1613.5315</td>  <td>-402.375</td>   <td>True</td> 
</tr>
<tr>
    <td>59</td>      <td>8</td>    <td>-186.6538</td>   <td>0.9</td>  <td>-1059.7481</td>  <td>686.4404</td>   <td>False</td>
</tr>
<tr>
    <td>59</td>      <td>9</td>    <td>520.2846</td>    <td>0.9</td>   <td>-798.0588</td>  <td>1838.628</td>   <td>False</td>
</tr>
<tr>
     <td>6</td>     <td>60</td>    <td>325.6367</td>    <td>0.9</td>   <td>-579.4664</td>  <td>1230.7397</td>  <td>False</td>
</tr>
<tr>
     <td>6</td>     <td>61</td>    <td>-46.0486</td>    <td>0.9</td>  <td>-1048.7169</td>  <td>956.6197</td>   <td>False</td>
</tr>
<tr>
     <td>6</td>     <td>62</td>    <td>364.1699</td>    <td>0.9</td>   <td>-546.5069</td>  <td>1274.8466</td>  <td>False</td>
</tr>
<tr>
     <td>6</td>     <td>63</td>    <td>428.8755</td>    <td>0.9</td>   <td>-632.7265</td>  <td>1490.4775</td>  <td>False</td>
</tr>
<tr>
     <td>6</td>     <td>64</td>     <td>32.2787</td>    <td>0.9</td>   <td>-934.1729</td>  <td>998.7303</td>   <td>False</td>
</tr>
<tr>
     <td>6</td>     <td>65</td>    <td>-195.2124</td>   <td>0.9</td>  <td>-1152.4958</td>  <td>762.0711</td>   <td>False</td>
</tr>
<tr>
     <td>6</td>     <td>66</td>    <td>-172.2083</td>   <td>0.9</td>  <td>-1457.3683</td>  <td>1112.9516</td>  <td>False</td>
</tr>
<tr>
     <td>6</td>     <td>67</td>    <td>-355.8833</td>   <td>0.9</td>  <td>-1561.4702</td>  <td>849.7036</td>   <td>False</td>
</tr>
<tr>
     <td>6</td>     <td>68</td>    <td>-358.6742</td>   <td>0.9</td>  <td>-1307.8278</td>  <td>590.4793</td>   <td>False</td>
</tr>
<tr>
     <td>6</td>     <td>69</td>    <td>172.0199</td>    <td>0.9</td>   <td>-785.2636</td>  <td>1129.3034</td>  <td>False</td>
</tr>
<tr>
     <td>6</td>      <td>7</td>    <td>162.5374</td>    <td>0.9</td>   <td>-803.9142</td>  <td>1128.989</td>   <td>False</td>
</tr>
<tr>
     <td>6</td>     <td>70</td>    <td>-317.9295</td>   <td>0.9</td>  <td>-1247.4093</td>  <td>611.5503</td>   <td>False</td>
</tr>
<tr>
     <td>6</td>     <td>71</td>    <td>-115.0238</td>   <td>0.9</td>  <td>-1036.6598</td>  <td>806.6122</td>   <td>False</td>
</tr>
<tr>
     <td>6</td>     <td>72</td>     <td>27.1275</td>    <td>0.9</td>   <td>-908.2445</td>  <td>962.4995</td>   <td>False</td>
</tr>
<tr>
     <td>6</td>     <td>73</td>    <td>-312.0833</td>   <td>0.9</td>  <td>-1419.7519</td>  <td>795.5852</td>   <td>False</td>
</tr>
<tr>
     <td>6</td>     <td>74</td>    <td>-414.6987</td>   <td>0.9</td>  <td>-1541.8586</td>  <td>712.4611</td>   <td>False</td>
</tr>
<tr>
     <td>6</td>     <td>75</td>    <td>-440.5156</td>   <td>0.9</td>  <td>-1355.2991</td>   <td>474.268</td>   <td>False</td>
</tr>
<tr>
     <td>6</td>     <td>76</td>    <td>-212.7675</td>   <td>0.9</td>  <td>-1145.1206</td>  <td>719.5855</td>   <td>False</td>
</tr>
<tr>
     <td>6</td>     <td>77</td>    <td>-374.9212</td>   <td>0.9</td>  <td>-1310.2932</td>  <td>560.4508</td>   <td>False</td>
</tr>
<tr>
     <td>6</td>      <td>8</td>    <td>446.3782</td>    <td>0.9</td>   <td>-680.7816</td>  <td>1573.5381</td>  <td>False</td>
</tr>
<tr>
     <td>6</td>      <td>9</td>    <td>1153.3167</td> <td>0.6097</td>  <td>-345.4245</td>  <td>2652.0578</td>  <td>False</td>
</tr>
<tr>
    <td>60</td>     <td>61</td>    <td>-371.6852</td>   <td>0.9</td>  <td>-1081.0838</td>  <td>337.7134</td>   <td>False</td>
</tr>
<tr>
    <td>60</td>     <td>62</td>     <td>38.5332</td>    <td>0.9</td>   <td>-533.5112</td>  <td>610.5776</td>   <td>False</td>
</tr>
<tr>
    <td>60</td>     <td>63</td>    <td>103.2388</td>    <td>0.9</td>   <td>-687.2682</td>  <td>893.7459</td>   <td>False</td>
</tr>
<tr>
    <td>60</td>     <td>64</td>    <td>-293.3579</td>   <td>0.9</td>   <td>-950.5728</td>  <td>363.8569</td>   <td>False</td>
</tr>
<tr>
    <td>60</td>     <td>65</td>    <td>-520.849</td>  <td>0.4883</td>  <td>-1164.506</td>  <td>122.8079</td>   <td>False</td>
</tr>
<tr>
    <td>60</td>     <td>66</td>    <td>-497.845</td>    <td>0.9</td>  <td>-1570.0104</td>  <td>574.3204</td>   <td>False</td>
</tr>
<tr>
    <td>60</td>     <td>67</td>     <td>-681.52</td>  <td>0.8266</td> <td>-1656.8878</td>  <td>293.8478</td>   <td>False</td>
</tr>
<tr>
    <td>60</td>     <td>68</td>    <td>-684.3109</td> <td>0.0124</td> <td>-1315.8131</td>  <td>-52.8087</td>   <td>True</td> 
</tr>
<tr>
    <td>60</td>     <td>69</td>    <td>-153.6168</td>   <td>0.9</td>   <td>-797.2737</td>  <td>490.0402</td>   <td>False</td>
</tr>
<tr>
    <td>60</td>      <td>7</td>    <td>-163.0993</td>   <td>0.9</td>   <td>-820.3141</td>  <td>494.1155</td>   <td>False</td>
</tr>
<tr>
    <td>60</td>     <td>70</td>    <td>-643.5662</td> <td>0.0159</td> <td>-1245.0937</td>  <td>-42.0386</td>   <td>True</td> 
</tr>
<tr>
    <td>60</td>     <td>71</td>    <td>-440.6605</td> <td>0.6765</td> <td>-1029.9953</td>  <td>148.6743</td>   <td>False</td>
</tr>
<tr>
    <td>60</td>     <td>72</td>    <td>-298.5092</td>   <td>0.9</td>   <td>-909.1018</td>  <td>312.0835</td>   <td>False</td>
</tr>
<tr>
    <td>60</td>     <td>73</td>     <td>-637.72</td>  <td>0.6725</td> <td>-1489.0908</td>  <td>213.6508</td>   <td>False</td>
</tr>
<tr>
    <td>60</td>     <td>74</td>    <td>-740.3354</td> <td>0.3602</td> <td>-1616.9151</td>  <td>136.2443</td>   <td>False</td>
</tr>
<tr>
    <td>60</td>     <td>75</td>    <td>-766.1522</td>  <td>0.001</td> <td>-1344.7121</td>  <td>-187.5923</td>  <td>True</td> 
</tr>
<tr>
    <td>60</td>     <td>76</td>    <td>-538.4042</td> <td>0.2258</td>  <td>-1144.362</td>   <td>67.5535</td>   <td>False</td>
</tr>
<tr>
    <td>60</td>     <td>77</td>    <td>-700.5578</td> <td>0.0038</td> <td>-1311.1505</td>  <td>-89.9652</td>   <td>True</td> 
</tr>
<tr>
    <td>60</td>      <td>8</td>    <td>120.7415</td>    <td>0.9</td>   <td>-755.8381</td>  <td>997.3212</td>   <td>False</td>
</tr>
<tr>
    <td>60</td>      <td>9</td>     <td>827.68</td>     <td>0.9</td>   <td>-492.9743</td>  <td>2148.3343</td>  <td>False</td>
</tr>
<tr>
    <td>61</td>     <td>62</td>    <td>410.2184</td>    <td>0.9</td>   <td>-306.2779</td>  <td>1126.7147</td>  <td>False</td>
</tr>
<tr>
    <td>61</td>     <td>63</td>     <td>474.924</td>    <td>0.9</td>    <td>-425.65</td>   <td>1375.4981</td>  <td>False</td>
</tr>
<tr>
    <td>61</td>     <td>64</td>     <td>78.3273</td>    <td>0.9</td>   <td>-707.8429</td>  <td>864.4975</td>   <td>False</td>
</tr>
<tr>
    <td>61</td>     <td>65</td>    <td>-149.1638</td>   <td>0.9</td>   <td>-924.0357</td>  <td>625.7081</td>   <td>False</td>
</tr>
<tr>
    <td>61</td>     <td>66</td>    <td>-126.1598</td>   <td>0.9</td>  <td>-1281.8721</td>  <td>1029.5525</td>  <td>False</td>
</tr>
<tr>
    <td>61</td>     <td>67</td>    <td>-309.8348</td>   <td>0.9</td>  <td>-1376.3593</td>  <td>756.6898</td>   <td>False</td>
</tr>
<tr>
    <td>61</td>     <td>68</td>    <td>-312.6257</td>   <td>0.9</td>  <td>-1077.4311</td>  <td>452.1797</td>   <td>False</td>
</tr>
<tr>
    <td>61</td>     <td>69</td>    <td>218.0684</td>    <td>0.9</td>   <td>-556.8035</td>  <td>992.9404</td>   <td>False</td>
</tr>
<tr>
    <td>61</td>      <td>7</td>    <td>208.5859</td>    <td>0.9</td>   <td>-577.5843</td>  <td>994.7561</td>   <td>False</td>
</tr>
<tr>
    <td>61</td>     <td>70</td>    <td>-271.8809</td>   <td>0.9</td>  <td>-1012.1293</td>  <td>468.3674</td>   <td>False</td>
</tr>
<tr>
    <td>61</td>     <td>71</td>    <td>-68.9753</td>    <td>0.9</td>   <td>-799.3503</td>  <td>661.3998</td>   <td>False</td>
</tr>
<tr>
    <td>61</td>     <td>72</td>     <td>73.176</td>     <td>0.9</td>   <td>-674.4573</td>  <td>820.8093</td>   <td>False</td>
</tr>
<tr>
    <td>61</td>     <td>73</td>    <td>-266.0348</td>   <td>0.9</td>  <td>-1220.4794</td>  <td>688.4098</td>   <td>False</td>
</tr>
<tr>
    <td>61</td>     <td>74</td>    <td>-368.6502</td>   <td>0.9</td>  <td>-1345.6477</td>  <td>608.3473</td>   <td>False</td>
</tr>
<tr>
    <td>61</td>     <td>75</td>    <td>-394.467</td>    <td>0.9</td>  <td>-1116.1759</td>  <td>327.2419</td>   <td>False</td>
</tr>
<tr>
    <td>61</td>     <td>76</td>    <td>-166.719</td>    <td>0.9</td>   <td>-910.5718</td>  <td>577.1338</td>   <td>False</td>
</tr>
<tr>
    <td>61</td>     <td>77</td>    <td>-328.8726</td>   <td>0.9</td>  <td>-1076.5059</td>  <td>418.7607</td>   <td>False</td>
</tr>
<tr>
    <td>61</td>      <td>8</td>    <td>492.4268</td>    <td>0.9</td>   <td>-484.5708</td>  <td>1469.4243</td>  <td>False</td>
</tr>
<tr>
    <td>61</td>      <td>9</td>    <td>1199.3652</td> <td>0.2974</td>  <td>-189.9727</td>  <td>2588.7032</td>  <td>False</td>
</tr>
<tr>
    <td>62</td>     <td>63</td>     <td>64.7056</td>    <td>0.9</td>   <td>-732.1771</td>  <td>861.5883</td>   <td>False</td>
</tr>
<tr>
    <td>62</td>     <td>64</td>    <td>-331.8911</td>   <td>0.9</td>   <td>-996.761</td>   <td>332.9788</td>   <td>False</td>
</tr>
<tr>
    <td>62</td>     <td>65</td>    <td>-559.3822</td> <td>0.3115</td> <td>-1210.8536</td>   <td>92.0891</td>   <td>False</td>
</tr>
<tr>
    <td>62</td>     <td>66</td>    <td>-536.3782</td>   <td>0.9</td>   <td>-1613.253</td>  <td>540.4966</td>   <td>False</td>
</tr>
<tr>
    <td>62</td>     <td>67</td>    <td>-720.0532</td> <td>0.7175</td> <td>-1700.5954</td>   <td>260.489</td>   <td>False</td>
</tr>
<tr>
    <td>62</td>     <td>68</td>    <td>-722.8441</td> <td>0.0052</td> <td>-1362.3093</td>  <td>-83.3789</td>   <td>True</td> 
</tr>
<tr>
    <td>62</td>     <td>69</td>     <td>-192.15</td>    <td>0.9</td>   <td>-843.6213</td>  <td>459.3214</td>   <td>False</td>
</tr>
<tr>
    <td>62</td>      <td>7</td>    <td>-201.6325</td>   <td>0.9</td>   <td>-866.5024</td>  <td>463.2374</td>   <td>False</td>
</tr>
<tr>
    <td>62</td>     <td>70</td>    <td>-682.0993</td> <td>0.0066</td> <td>-1291.9813</td>  <td>-72.2174</td>   <td>True</td> 
</tr>
<tr>
    <td>62</td>     <td>71</td>    <td>-479.1937</td> <td>0.5117</td> <td>-1077.0533</td>   <td>118.666</td>   <td>False</td>
</tr>
<tr>
    <td>62</td>     <td>72</td>    <td>-337.0424</td>   <td>0.9</td>   <td>-955.8671</td>  <td>281.7823</td>   <td>False</td>
</tr>
<tr>
    <td>62</td>     <td>73</td>    <td>-676.2532</td> <td>0.5506</td> <td>-1533.5472</td>  <td>181.0408</td>   <td>False</td>
</tr>
<tr>
    <td>62</td>     <td>74</td>    <td>-778.8686</td> <td>0.2402</td> <td>-1661.2022</td>   <td>103.465</td>   <td>False</td>
</tr>
<tr>
    <td>62</td>     <td>75</td>    <td>-804.6854</td>  <td>0.001</td> <td>-1391.9266</td>  <td>-217.4442</td>  <td>True</td> 
</tr>
<tr>
    <td>62</td>     <td>76</td>    <td>-576.9374</td> <td>0.1215</td> <td>-1191.1893</td>   <td>37.3145</td>   <td>False</td>
</tr>
<tr>
    <td>62</td>     <td>77</td>    <td>-739.091</td>  <td>0.0015</td> <td>-1357.9158</td>  <td>-120.2663</td>  <td>True</td> 
</tr>
<tr>
    <td>62</td>      <td>8</td>     <td>82.2083</td>    <td>0.9</td>   <td>-800.1253</td>   <td>964.542</td>   <td>False</td>
</tr>
<tr>
    <td>62</td>      <td>9</td>    <td>789.1468</td>    <td>0.9</td>   <td>-535.3336</td>  <td>2113.6272</td>  <td>False</td>
</tr>
<tr>
    <td>63</td>     <td>64</td>    <td>-396.5968</td>   <td>0.9</td>  <td>-1256.6657</td>  <td>463.4722</td>   <td>False</td>
</tr>
<tr>
    <td>63</td>     <td>65</td>    <td>-624.0879</td> <td>0.7172</td> <td>-1473.8417</td>  <td>225.6659</td>   <td>False</td>
</tr>
<tr>
    <td>63</td>     <td>66</td>    <td>-601.0838</td>   <td>0.9</td>  <td>-1808.2814</td>  <td>606.1137</td>   <td>False</td>
</tr>
<tr>
    <td>63</td>     <td>67</td>    <td>-784.7588</td> <td>0.8247</td> <td>-1906.8683</td>  <td>337.3506</td>   <td>False</td>
</tr>
<tr>
    <td>63</td>     <td>68</td>    <td>-787.5497</td>  <td>0.125</td> <td>-1628.1342</td>   <td>53.0348</td>   <td>False</td>
</tr>
<tr>
    <td>63</td>     <td>69</td>    <td>-256.8556</td>   <td>0.9</td>  <td>-1106.6094</td>  <td>592.8982</td>   <td>False</td>
</tr>
<tr>
    <td>63</td>      <td>7</td>    <td>-266.3381</td>   <td>0.9</td>  <td>-1126.4071</td>  <td>593.7308</td>   <td>False</td>
</tr>
<tr>
    <td>63</td>     <td>70</td>    <td>-746.805</td>   <td>0.17</td>  <td>-1565.1097</td>   <td>71.4997</td>   <td>False</td>
</tr>
<tr>
    <td>63</td>     <td>71</td>    <td>-543.8993</td>   <td>0.9</td>  <td>-1353.2835</td>  <td>265.4849</td>   <td>False</td>
</tr>
<tr>
    <td>63</td>     <td>72</td>    <td>-401.748</td>    <td>0.9</td>  <td>-1226.7393</td>  <td>423.2433</td>   <td>False</td>
</tr>
<tr>
    <td>63</td>     <td>73</td>    <td>-740.9588</td> <td>0.7334</td> <td>-1757.1377</td>  <td>275.2201</td>   <td>False</td>
</tr>
<tr>
    <td>63</td>     <td>74</td>    <td>-843.5742</td> <td>0.4757</td> <td>-1880.9648</td>  <td>193.8164</td>   <td>False</td>
</tr>
<tr>
    <td>63</td>     <td>75</td>    <td>-869.391</td>  <td>0.0122</td> <td>-1670.9638</td>  <td>-67.8183</td>   <td>True</td> 
</tr>
<tr>
    <td>63</td>     <td>76</td>    <td>-641.643</td>  <td>0.5746</td> <td>-1463.2099</td>  <td>179.9238</td>   <td>False</td>
</tr>
<tr>
    <td>63</td>     <td>77</td>    <td>-803.7967</td> <td>0.0746</td> <td>-1628.7879</td>   <td>21.1946</td>   <td>False</td>
</tr>
<tr>
    <td>63</td>      <td>8</td>     <td>17.5027</td>    <td>0.9</td>  <td>-1019.8879</td>  <td>1054.8933</td>  <td>False</td>
</tr>
<tr>
    <td>63</td>      <td>9</td>    <td>724.4412</td>    <td>0.9</td>   <td>-708.0095</td>  <td>2156.8919</td>  <td>False</td>
</tr>
<tr>
    <td>64</td>     <td>65</td>    <td>-227.4911</td>   <td>0.9</td>   <td>-954.8916</td>  <td>499.9094</td>   <td>False</td>
</tr>
<tr>
    <td>64</td>     <td>66</td>    <td>-204.4871</td>   <td>0.9</td>  <td>-1328.9229</td>  <td>919.9488</td>   <td>False</td>
</tr>
<tr>
    <td>64</td>     <td>67</td>    <td>-388.1621</td>   <td>0.9</td>  <td>-1420.7121</td>   <td>644.388</td>   <td>False</td>
</tr>
<tr>
    <td>64</td>     <td>68</td>    <td>-390.953</td>    <td>0.9</td>  <td>-1107.6204</td>  <td>325.7145</td>   <td>False</td>
</tr>
<tr>
    <td>64</td>     <td>69</td>    <td>139.7412</td>    <td>0.9</td>   <td>-587.6593</td>  <td>867.1416</td>   <td>False</td>
</tr>
<tr>
    <td>64</td>      <td>7</td>    <td>130.2586</td>    <td>0.9</td>   <td>-609.1658</td>  <td>869.6831</td>   <td>False</td>
</tr>
<tr>
    <td>64</td>     <td>70</td>    <td>-350.2082</td>   <td>0.9</td>  <td>-1040.6085</td>  <td>340.1921</td>   <td>False</td>
</tr>
<tr>
    <td>64</td>     <td>71</td>    <td>-147.3025</td>   <td>0.9</td>   <td>-827.1059</td>  <td>532.5009</td>   <td>False</td>
</tr>
<tr>
    <td>64</td>     <td>72</td>     <td>-5.1513</td>    <td>0.9</td>   <td>-703.4639</td>  <td>693.1614</td>   <td>False</td>
</tr>
<tr>
    <td>64</td>     <td>73</td>    <td>-344.3621</td>   <td>0.9</td>   <td>-1260.686</td>  <td>571.9618</td>   <td>False</td>
</tr>
<tr>
    <td>64</td>     <td>74</td>    <td>-446.9775</td>   <td>0.9</td>  <td>-1386.7695</td>  <td>492.8146</td>   <td>False</td>
</tr>
<tr>
    <td>64</td>     <td>75</td>    <td>-472.7943</td>  <td>0.807</td> <td>-1143.2783</td>  <td>197.6897</td>   <td>False</td>
</tr>
<tr>
    <td>64</td>     <td>76</td>    <td>-245.0463</td>   <td>0.9</td>   <td>-939.3099</td>  <td>449.2173</td>   <td>False</td>
</tr>
<tr>
    <td>64</td>     <td>77</td>    <td>-407.1999</td>   <td>0.9</td>  <td>-1105.5126</td>  <td>291.1127</td>   <td>False</td>
</tr>
<tr>
    <td>64</td>      <td>8</td>    <td>414.0995</td>    <td>0.9</td>   <td>-525.6926</td>  <td>1353.8915</td>  <td>False</td>
</tr>
<tr>
    <td>64</td>      <td>9</td>    <td>1121.0379</td> <td>0.4448</td>  <td>-242.3934</td>  <td>2484.4692</td>  <td>False</td>
</tr>
<tr>
    <td>65</td>     <td>66</td>     <td>23.004</td>     <td>0.9</td>  <td>-1093.5616</td>  <td>1139.5697</td>  <td>False</td>
</tr>
<tr>
    <td>65</td>     <td>67</td>    <td>-160.671</td>    <td>0.9</td>  <td>-1184.6449</td>  <td>863.3029</td>   <td>False</td>
</tr>
<tr>
    <td>65</td>     <td>68</td>    <td>-163.4619</td>   <td>0.9</td>   <td>-867.7169</td>  <td>540.7932</td>   <td>False</td>
</tr>
<tr>
    <td>65</td>     <td>69</td>    <td>367.2323</td>    <td>0.9</td>   <td>-347.9421</td>  <td>1082.4066</td>  <td>False</td>
</tr>
<tr>
    <td>65</td>      <td>7</td>    <td>357.7497</td>    <td>0.9</td>   <td>-369.6508</td>  <td>1085.1502</td>  <td>False</td>
</tr>
<tr>
    <td>65</td>     <td>70</td>    <td>-122.7171</td>   <td>0.9</td>   <td>-800.2239</td>  <td>554.7897</td>   <td>False</td>
</tr>
<tr>
    <td>65</td>     <td>71</td>     <td>80.1886</td>    <td>0.9</td>   <td>-586.5165</td>  <td>746.8936</td>   <td>False</td>
</tr>
<tr>
    <td>65</td>     <td>72</td>    <td>222.3398</td>    <td>0.9</td>   <td>-463.2282</td>  <td>907.9079</td>   <td>False</td>
</tr>
<tr>
    <td>65</td>     <td>73</td>    <td>-116.871</td>    <td>0.9</td>   <td>-1023.52</td>   <td>789.7781</td>   <td>False</td>
</tr>
<tr>
    <td>65</td>     <td>74</td>    <td>-219.4864</td>   <td>0.9</td>  <td>-1149.8476</td>  <td>710.8749</td>   <td>False</td>
</tr>
<tr>
    <td>65</td>     <td>75</td>    <td>-245.3032</td>   <td>0.9</td>   <td>-902.5031</td>  <td>411.8967</td>   <td>False</td>
</tr>
<tr>
    <td>65</td>     <td>76</td>    <td>-17.5552</td>    <td>0.9</td>   <td>-698.9984</td>  <td>663.8881</td>   <td>False</td>
</tr>
<tr>
    <td>65</td>     <td>77</td>    <td>-179.7088</td>   <td>0.9</td>   <td>-865.2768</td>  <td>505.8592</td>   <td>False</td>
</tr>
<tr>
    <td>65</td>      <td>8</td>    <td>641.5906</td>  <td>0.8546</td>  <td>-288.7707</td>  <td>1571.9518</td>  <td>False</td>
</tr>
<tr>
    <td>65</td>      <td>9</td>    <td>1348.529</td>  <td>0.0552</td>   <td>-8.419</td>    <td>2705.477</td>   <td>False</td>
</tr>
<tr>
    <td>66</td>     <td>67</td>    <td>-183.675</td>    <td>0.9</td>  <td>-1519.2524</td>  <td>1151.9024</td>  <td>False</td>
</tr>
<tr>
    <td>66</td>     <td>68</td>    <td>-186.4659</td>   <td>0.9</td>  <td>-1296.0693</td>  <td>923.1375</td>   <td>False</td>
</tr>
<tr>
    <td>66</td>     <td>69</td>    <td>344.2282</td>    <td>0.9</td>   <td>-772.3374</td>  <td>1460.7939</td>  <td>False</td>
</tr>
<tr>
    <td>66</td>      <td>7</td>    <td>334.7457</td>    <td>0.9</td>   <td>-789.6901</td>  <td>1459.1815</td>  <td>False</td>
</tr>
<tr>
    <td>66</td>     <td>70</td>    <td>-145.7212</td>   <td>0.9</td>  <td>-1238.5432</td>  <td>947.1009</td>   <td>False</td>
</tr>
<tr>
    <td>66</td>     <td>71</td>     <td>57.1845</td>    <td>0.9</td>  <td>-1028.9739</td>  <td>1143.3429</td>  <td>False</td>
</tr>
<tr>
    <td>66</td>     <td>72</td>    <td>199.3358</td>    <td>0.9</td>   <td>-898.5021</td>  <td>1297.1737</td>  <td>False</td>
</tr>
<tr>
    <td>66</td>     <td>73</td>    <td>-139.875</td>    <td>0.9</td>   <td>-1387.776</td>  <td>1108.026</td>   <td>False</td>
</tr>
<tr>
    <td>66</td>     <td>74</td>    <td>-242.4904</td>   <td>0.9</td>  <td>-1507.7242</td>  <td>1022.7434</td>  <td>False</td>
</tr>
<tr>
    <td>66</td>     <td>75</td>    <td>-268.3072</td>   <td>0.9</td>  <td>-1348.6573</td>  <td>812.0428</td>   <td>False</td>
</tr>
<tr>
    <td>66</td>     <td>76</td>    <td>-40.5592</td>    <td>0.9</td>   <td>-1135.826</td>  <td>1054.7076</td>  <td>False</td>
</tr>
<tr>
    <td>66</td>     <td>77</td>    <td>-202.7128</td>   <td>0.9</td>  <td>-1300.5507</td>   <td>895.125</td>   <td>False</td>
</tr>
<tr>
    <td>66</td>      <td>8</td>    <td>618.5865</td>    <td>0.9</td>   <td>-646.6473</td>  <td>1883.8203</td>  <td>False</td>
</tr>
<tr>
    <td>66</td>      <td>9</td>    <td>1325.525</td>  <td>0.4318</td>  <td>-279.6393</td>  <td>2930.6893</td>  <td>False</td>
</tr>
<tr>
    <td>67</td>     <td>68</td>     <td>-2.7909</td>    <td>0.9</td>  <td>-1019.1685</td>  <td>1013.5866</td>  <td>False</td>
</tr>
<tr>
    <td>67</td>     <td>69</td>    <td>527.9032</td>    <td>0.9</td>   <td>-496.0707</td>  <td>1551.8771</td>  <td>False</td>
</tr>
<tr>
    <td>67</td>      <td>7</td>    <td>518.4207</td>    <td>0.9</td>   <td>-514.1294</td>  <td>1550.9707</td>  <td>False</td>
</tr>
<tr>
    <td>67</td>     <td>70</td>     <td>37.9538</td>    <td>0.9</td>   <td>-960.076</td>   <td>1035.9837</td>  <td>False</td>
</tr>
<tr>
    <td>67</td>     <td>71</td>    <td>240.8595</td>    <td>0.9</td>   <td>-749.8694</td>  <td>1231.5884</td>  <td>False</td>
</tr>
<tr>
    <td>67</td>     <td>72</td>    <td>383.0108</td>    <td>0.9</td>   <td>-620.5088</td>  <td>1386.5304</td>  <td>False</td>
</tr>
<tr>
    <td>67</td>     <td>73</td>      <td>43.8</td>      <td>0.9</td>  <td>-1121.9875</td>  <td>1209.5875</td>  <td>False</td>
</tr>
<tr>
    <td>67</td>     <td>74</td>    <td>-58.8154</td>    <td>0.9</td>  <td>-1243.1381</td>  <td>1125.5073</td>  <td>False</td>
</tr>
<tr>
    <td>67</td>     <td>75</td>    <td>-84.6322</td>    <td>0.9</td>  <td>-1068.9898</td>  <td>899.7254</td>   <td>False</td>
</tr>
<tr>
    <td>67</td>     <td>76</td>    <td>143.1158</td>    <td>0.9</td>   <td>-857.5905</td>  <td>1143.8221</td>  <td>False</td>
</tr>
<tr>
    <td>67</td>     <td>77</td>    <td>-19.0378</td>    <td>0.9</td>  <td>-1022.5575</td>  <td>984.4818</td>   <td>False</td>
</tr>
<tr>
    <td>67</td>      <td>8</td>    <td>802.2615</td>   <td>0.892</td>  <td>-382.0611</td>  <td>1986.5842</td>  <td>False</td>
</tr>
<tr>
    <td>67</td>      <td>9</td>     <td>1509.2</td>    <td>0.07</td>   <td>-32.9919</td>   <td>3051.3919</td>  <td>False</td>
</tr>
<tr>
    <td>68</td>     <td>69</td>    <td>530.6941</td>  <td>0.6587</td>  <td>-173.5609</td>  <td>1234.9492</td>  <td>False</td>
</tr>
<tr>
    <td>68</td>      <td>7</td>    <td>521.2116</td>  <td>0.7392</td>  <td>-195.4559</td>  <td>1237.879</td>   <td>False</td>
</tr>
<tr>
    <td>68</td>     <td>70</td>     <td>40.7448</td>    <td>0.9</td>   <td>-625.2254</td>  <td>706.7149</td>   <td>False</td>
</tr>
<tr>
    <td>68</td>     <td>71</td>    <td>243.6504</td>    <td>0.9</td>   <td>-411.3277</td>  <td>898.6286</td>   <td>False</td>
</tr>
<tr>
    <td>68</td>     <td>72</td>    <td>385.8017</td>    <td>0.9</td>   <td>-288.3676</td>  <td>1059.9711</td>  <td>False</td>
</tr>
<tr>
    <td>68</td>     <td>73</td>     <td>46.5909</td>    <td>0.9</td>   <td>-851.4699</td>  <td>944.6517</td>   <td>False</td>
</tr>
<tr>
    <td>68</td>     <td>74</td>    <td>-56.0245</td>    <td>0.9</td>   <td>-978.0184</td>  <td>865.9695</td>   <td>False</td>
</tr>
<tr>
    <td>68</td>     <td>75</td>    <td>-81.8413</td>    <td>0.9</td>   <td>-727.1416</td>   <td>563.459</td>   <td>False</td>
</tr>
<tr>
    <td>68</td>     <td>76</td>    <td>145.9067</td>    <td>0.9</td>   <td>-524.0677</td>  <td>815.8811</td>   <td>False</td>
</tr>
<tr>
    <td>68</td>     <td>77</td>    <td>-16.2469</td>    <td>0.9</td>   <td>-690.4163</td>  <td>657.9224</td>   <td>False</td>
</tr>
<tr>
    <td>68</td>      <td>8</td>    <td>805.0524</td>  <td>0.2676</td>  <td>-116.9415</td>  <td>1727.0464</td>  <td>False</td>
</tr>
<tr>
    <td>68</td>      <td>9</td>    <td>1511.9909</td> <td>0.0065</td>   <td>160.766</td>   <td>2863.2158</td>  <td>True</td> 
</tr>
<tr>
    <td>69</td>      <td>7</td>     <td>-9.4825</td>    <td>0.9</td>   <td>-736.883</td>   <td>717.9179</td>   <td>False</td>
</tr>
<tr>
    <td>69</td>     <td>70</td>    <td>-489.9494</td> <td>0.7518</td> <td>-1167.4562</td>  <td>187.5574</td>   <td>False</td>
</tr>
<tr>
    <td>69</td>     <td>71</td>    <td>-287.0437</td>   <td>0.9</td>   <td>-953.7487</td>  <td>379.6613</td>   <td>False</td>
</tr>
<tr>
    <td>69</td>     <td>72</td>    <td>-144.8924</td>   <td>0.9</td>   <td>-830.4604</td>  <td>540.6756</td>   <td>False</td>
</tr>
<tr>
    <td>69</td>     <td>73</td>    <td>-484.1032</td>   <td>0.9</td>  <td>-1390.7522</td>  <td>422.5458</td>   <td>False</td>
</tr>
<tr>
    <td>69</td>     <td>74</td>    <td>-586.7186</td>   <td>0.9</td>  <td>-1517.0799</td>  <td>343.6427</td>   <td>False</td>
</tr>
<tr>
    <td>69</td>     <td>75</td>    <td>-612.5354</td> <td>0.1309</td> <td>-1269.7354</td>   <td>44.6645</td>   <td>False</td>
</tr>
<tr>
    <td>69</td>     <td>76</td>    <td>-384.7874</td>   <td>0.9</td>  <td>-1066.2307</td>  <td>296.6558</td>   <td>False</td>
</tr>
<tr>
    <td>69</td>     <td>77</td>    <td>-546.9411</td> <td>0.5231</td> <td>-1232.5091</td>   <td>138.627</td>   <td>False</td>
</tr>
<tr>
    <td>69</td>      <td>8</td>    <td>274.3583</td>    <td>0.9</td>   <td>-656.0029</td>  <td>1204.7196</td>  <td>False</td>
</tr>
<tr>
    <td>69</td>      <td>9</td>    <td>981.2968</td>  <td>0.7518</td>  <td>-375.6512</td>  <td>2338.2448</td>  <td>False</td>
</tr>
<tr>
     <td>7</td>     <td>70</td>    <td>-480.4668</td> <td>0.8352</td> <td>-1170.8671</td>  <td>209.9334</td>   <td>False</td>
</tr>
<tr>
     <td>7</td>     <td>71</td>    <td>-277.5612</td>   <td>0.9</td>   <td>-957.3646</td>  <td>402.2422</td>   <td>False</td>
</tr>
<tr>
     <td>7</td>     <td>72</td>    <td>-135.4099</td>   <td>0.9</td>   <td>-833.7225</td>  <td>562.9028</td>   <td>False</td>
</tr>
<tr>
     <td>7</td>     <td>73</td>    <td>-474.6207</td>   <td>0.9</td>  <td>-1390.9446</td>  <td>441.7032</td>   <td>False</td>
</tr>
<tr>
     <td>7</td>     <td>74</td>    <td>-577.2361</td>   <td>0.9</td>  <td>-1517.0281</td>   <td>362.556</td>   <td>False</td>
</tr>
<tr>
     <td>7</td>     <td>75</td>    <td>-603.0529</td> <td>0.1984</td> <td>-1273.5369</td>   <td>67.4311</td>   <td>False</td>
</tr>
<tr>
     <td>7</td>     <td>76</td>    <td>-375.3049</td>   <td>0.9</td>  <td>-1069.5685</td>  <td>318.9587</td>   <td>False</td>
</tr>
<tr>
     <td>7</td>     <td>77</td>    <td>-537.4585</td> <td>0.6093</td> <td>-1235.7712</td>  <td>160.8541</td>   <td>False</td>
</tr>
<tr>
     <td>7</td>      <td>8</td>    <td>283.8408</td>    <td>0.9</td>   <td>-655.9512</td>  <td>1223.6329</td>  <td>False</td>
</tr>
<tr>
     <td>7</td>      <td>9</td>    <td>990.7793</td>   <td>0.741</td>  <td>-372.652</td>   <td>2354.2106</td>  <td>False</td>
</tr>
<tr>
    <td>70</td>     <td>71</td>    <td>202.9057</td>    <td>0.9</td>   <td>-423.2227</td>   <td>829.034</td>   <td>False</td>
</tr>
<tr>
    <td>70</td>     <td>72</td>     <td>345.057</td>    <td>0.9</td>   <td>-301.1199</td>  <td>991.2339</td>   <td>False</td>
</tr>
<tr>
    <td>70</td>     <td>73</td>     <td>5.8462</td>     <td>0.9</td>   <td>-871.3958</td>  <td>883.0882</td>   <td>False</td>
</tr>
<tr>
    <td>70</td>     <td>74</td>    <td>-96.7692</td>    <td>0.9</td>   <td>-998.4971</td>  <td>804.9586</td>   <td>False</td>
</tr>
<tr>
    <td>70</td>     <td>75</td>    <td>-122.5861</td>   <td>0.9</td>   <td>-738.5835</td>  <td>493.4113</td>   <td>False</td>
</tr>
<tr>
    <td>70</td>     <td>76</td>    <td>105.1619</td>    <td>0.9</td>   <td>-536.6371</td>   <td>746.961</td>   <td>False</td>
</tr>
<tr>
    <td>70</td>     <td>77</td>    <td>-56.9917</td>    <td>0.9</td>   <td>-703.1686</td>  <td>589.1852</td>   <td>False</td>
</tr>
<tr>
    <td>70</td>      <td>8</td>    <td>764.3077</td>  <td>0.3488</td>  <td>-137.4202</td>  <td>1666.0356</td>  <td>False</td>
</tr>
<tr>
    <td>70</td>      <td>9</td>    <td>1471.2462</td> <td>0.0092</td>  <td>133.7676</td>   <td>2808.7247</td>  <td>True</td> 
</tr>
<tr>
    <td>71</td>     <td>72</td>    <td>142.1513</td>    <td>0.9</td>   <td>-492.691</td>   <td>776.9936</td>   <td>False</td>
</tr>
<tr>
    <td>71</td>     <td>73</td>    <td>-197.0595</td>   <td>0.9</td>  <td>-1065.9862</td>  <td>671.8672</td>   <td>False</td>
</tr>
<tr>
    <td>71</td>     <td>74</td>    <td>-299.6749</td>   <td>0.9</td>  <td>-1193.3154</td>  <td>593.9656</td>   <td>False</td>
</tr>
<tr>
    <td>71</td>     <td>75</td>    <td>-325.4917</td>   <td>0.9</td>   <td>-929.5885</td>   <td>278.605</td>   <td>False</td>
</tr>
<tr>
    <td>71</td>     <td>76</td>    <td>-97.7437</td>    <td>0.9</td>   <td>-728.1294</td>   <td>532.642</td>   <td>False</td>
</tr>
<tr>
    <td>71</td>     <td>77</td>    <td>-259.8974</td>   <td>0.9</td>   <td>-894.7396</td>  <td>374.9449</td>   <td>False</td>
</tr>
<tr>
    <td>71</td>      <td>8</td>     <td>561.402</td>    <td>0.9</td>   <td>-332.2385</td>  <td>1455.0425</td>  <td>False</td>
</tr>
<tr>
    <td>71</td>      <td>9</td>    <td>1268.3405</td> <td>0.1007</td>   <td>-63.699</td>   <td>2600.3799</td>  <td>False</td>
</tr>
<tr>
    <td>72</td>     <td>73</td>    <td>-339.2108</td>   <td>0.9</td>  <td>-1222.6934</td>  <td>544.2718</td>   <td>False</td>
</tr>
<tr>
    <td>72</td>     <td>74</td>    <td>-441.8262</td>   <td>0.9</td>  <td>-1349.6264</td>   <td>465.974</td>   <td>False</td>
</tr>
<tr>
    <td>72</td>     <td>75</td>    <td>-467.643</td>  <td>0.6744</td> <td>-1092.4957</td>  <td>157.2096</td>   <td>False</td>
</tr>
<tr>
    <td>72</td>     <td>76</td>    <td>-239.895</td>    <td>0.9</td>   <td>-890.198</td>    <td>410.408</td>   <td>False</td>
</tr>
<tr>
    <td>72</td>     <td>77</td>    <td>-402.0486</td>   <td>0.9</td>  <td>-1056.6727</td>  <td>252.5754</td>   <td>False</td>
</tr>
<tr>
    <td>72</td>      <td>8</td>    <td>419.2507</td>    <td>0.9</td>   <td>-488.5495</td>  <td>1327.0509</td>  <td>False</td>
</tr>
<tr>
    <td>72</td>      <td>9</td>    <td>1126.1892</td> <td>0.3798</td>  <td>-215.3908</td>  <td>2467.7692</td>  <td>False</td>
</tr>
<tr>
    <td>73</td>     <td>74</td>    <td>-102.6154</td>   <td>0.9</td>  <td>-1187.1015</td>  <td>981.8707</td>   <td>False</td>
</tr>
<tr>
    <td>73</td>     <td>75</td>    <td>-128.4322</td>   <td>0.9</td>   <td>-990.0875</td>   <td>733.223</td>   <td>False</td>
</tr>
<tr>
    <td>73</td>     <td>76</td>     <td>99.3158</td>    <td>0.9</td>   <td>-780.9699</td>  <td>979.6015</td>   <td>False</td>
</tr>
<tr>
    <td>73</td>     <td>77</td>    <td>-62.8378</td>    <td>0.9</td>   <td>-946.3205</td>  <td>820.6448</td>   <td>False</td>
</tr>
<tr>
    <td>73</td>      <td>8</td>    <td>758.4615</td>  <td>0.8247</td>  <td>-326.0246</td>  <td>1842.9476</td>  <td>False</td>
</tr>
<tr>
    <td>73</td>      <td>9</td>     <td>1465.4</td>   <td>0.0508</td>   <td>-1.5171</td>   <td>2932.3171</td>  <td>False</td>
</tr>
<tr>
    <td>74</td>     <td>75</td>    <td>-25.8168</td>    <td>0.9</td>   <td>-912.3885</td>  <td>860.7549</td>   <td>False</td>
</tr>
<tr>
    <td>74</td>     <td>76</td>    <td>201.9312</td>    <td>0.9</td>   <td>-702.758</td>   <td>1106.6204</td>  <td>False</td>
</tr>
<tr>
    <td>74</td>     <td>77</td>     <td>39.7775</td>    <td>0.9</td>   <td>-868.0226</td>  <td>947.5777</td>   <td>False</td>
</tr>
<tr>
    <td>74</td>      <td>8</td>    <td>861.0769</td>  <td>0.5786</td>  <td>-243.3097</td>  <td>1965.4635</td>  <td>False</td>
</tr>
<tr>
    <td>74</td>      <td>9</td>    <td>1568.0154</td> <td>0.0194</td>   <td>86.3253</td>   <td>3049.7055</td>  <td>True</td> 
</tr>
<tr>
    <td>75</td>     <td>76</td>     <td>227.748</td>    <td>0.9</td>   <td>-392.5763</td>  <td>848.0723</td>   <td>False</td>
</tr>
<tr>
    <td>75</td>     <td>77</td>     <td>65.5944</td>    <td>0.9</td>   <td>-559.2583</td>   <td>690.447</td>   <td>False</td>
</tr>
<tr>
    <td>75</td>      <td>8</td>    <td>886.8938</td>  <td>0.0497</td>   <td>0.3221</td>    <td>1773.4655</td>  <td>True</td> 
</tr>
<tr>
    <td>75</td>      <td>9</td>    <td>1593.8322</td> <td>0.0013</td>  <td>266.5247</td>   <td>2921.1397</td>  <td>True</td> 
</tr>
<tr>
    <td>76</td>     <td>77</td>    <td>-162.1536</td>   <td>0.9</td>   <td>-812.4567</td>  <td>488.1494</td>   <td>False</td>
</tr>
<tr>
    <td>76</td>      <td>8</td>    <td>659.1457</td>  <td>0.7352</td>  <td>-245.5435</td>  <td>1563.835</td>   <td>False</td>
</tr>
<tr>
    <td>76</td>      <td>9</td>    <td>1366.0842</td> <td>0.0368</td>   <td>26.6073</td>   <td>2705.5611</td>  <td>True</td> 
</tr>
<tr>
    <td>77</td>      <td>8</td>    <td>821.2994</td>  <td>0.1859</td>  <td>-86.5008</td>   <td>1729.0996</td>  <td>False</td>
</tr>
<tr>
    <td>77</td>      <td>9</td>    <td>1528.2378</td> <td>0.0044</td>  <td>186.6578</td>   <td>2869.8179</td>  <td>True</td> 
</tr>
<tr>
     <td>8</td>      <td>9</td>    <td>706.9385</td>    <td>0.9</td>   <td>-774.7516</td>  <td>2188.6286</td>  <td>False</td>
</tr>
</table>




```python
cool_df = pd.DataFrame(data=results._results_table.data[1:], columns=results._results_table.data[0])
pd.set_option('display.max_rows', 999)
cool_df.loc[cool_df['reject'] == True]
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
      <th>group1</th>
      <th>group2</th>
      <th>meandiff</th>
      <th>p-adj</th>
      <th>lower</th>
      <th>upper</th>
      <th>reject</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>8</td>
      <td>1</td>
      <td>18</td>
      <td>837.7601</td>
      <td>0.0022</td>
      <td>125.0957</td>
      <td>1550.4244</td>
      <td>True</td>
    </tr>
    <tr>
      <td>11</td>
      <td>1</td>
      <td>20</td>
      <td>1130.2753</td>
      <td>0.0010</td>
      <td>287.8045</td>
      <td>1972.7462</td>
      <td>True</td>
    </tr>
    <tr>
      <td>18</td>
      <td>1</td>
      <td>27</td>
      <td>1345.4267</td>
      <td>0.0010</td>
      <td>298.9379</td>
      <td>2391.9156</td>
      <td>True</td>
    </tr>
    <tr>
      <td>20</td>
      <td>1</td>
      <td>29</td>
      <td>2163.7862</td>
      <td>0.0010</td>
      <td>1478.2182</td>
      <td>2849.3542</td>
      <td>True</td>
    </tr>
    <tr>
      <td>30</td>
      <td>1</td>
      <td>38</td>
      <td>5902.3795</td>
      <td>0.0010</td>
      <td>5164.4137</td>
      <td>6640.3453</td>
      <td>True</td>
    </tr>
    <tr>
      <td>45</td>
      <td>1</td>
      <td>51</td>
      <td>663.1063</td>
      <td>0.0369</td>
      <td>12.8032</td>
      <td>1313.4093</td>
      <td>True</td>
    </tr>
    <tr>
      <td>53</td>
      <td>1</td>
      <td>59</td>
      <td>898.1532</td>
      <td>0.0010</td>
      <td>292.5750</td>
      <td>1503.7315</td>
      <td>True</td>
    </tr>
    <tr>
      <td>57</td>
      <td>1</td>
      <td>62</td>
      <td>629.2910</td>
      <td>0.0386</td>
      <td>10.4663</td>
      <td>1248.1158</td>
      <td>True</td>
    </tr>
    <tr>
      <td>75</td>
      <td>1</td>
      <td>9</td>
      <td>1418.4378</td>
      <td>0.0197</td>
      <td>76.8578</td>
      <td>2760.0179</td>
      <td>True</td>
    </tr>
    <tr>
      <td>86</td>
      <td>10</td>
      <td>20</td>
      <td>882.2312</td>
      <td>0.0348</td>
      <td>20.1197</td>
      <td>1744.3428</td>
      <td>True</td>
    </tr>
    <tr>
      <td>93</td>
      <td>10</td>
      <td>27</td>
      <td>1097.3826</td>
      <td>0.0297</td>
      <td>35.0183</td>
      <td>2159.7470</td>
      <td>True</td>
    </tr>
    <tr>
      <td>95</td>
      <td>10</td>
      <td>29</td>
      <td>1915.7421</td>
      <td>0.0010</td>
      <td>1206.1770</td>
      <td>2625.3072</td>
      <td>True</td>
    </tr>
    <tr>
      <td>105</td>
      <td>10</td>
      <td>38</td>
      <td>5654.3354</td>
      <td>0.0010</td>
      <td>4894.0245</td>
      <td>6414.6463</td>
      <td>True</td>
    </tr>
    <tr>
      <td>128</td>
      <td>10</td>
      <td>59</td>
      <td>650.1091</td>
      <td>0.0324</td>
      <td>17.4922</td>
      <td>1282.7260</td>
      <td>True</td>
    </tr>
    <tr>
      <td>157</td>
      <td>11</td>
      <td>18</td>
      <td>818.8801</td>
      <td>0.0032</td>
      <td>110.1828</td>
      <td>1527.5775</td>
      <td>True</td>
    </tr>
    <tr>
      <td>160</td>
      <td>11</td>
      <td>20</td>
      <td>1111.3954</td>
      <td>0.0010</td>
      <td>272.2777</td>
      <td>1950.5131</td>
      <td>True</td>
    </tr>
    <tr>
      <td>167</td>
      <td>11</td>
      <td>27</td>
      <td>1326.5468</td>
      <td>0.0010</td>
      <td>282.7555</td>
      <td>2370.3381</td>
      <td>True</td>
    </tr>
    <tr>
      <td>169</td>
      <td>11</td>
      <td>29</td>
      <td>2144.9063</td>
      <td>0.0010</td>
      <td>1463.4630</td>
      <td>2826.3495</td>
      <td>True</td>
    </tr>
    <tr>
      <td>179</td>
      <td>11</td>
      <td>38</td>
      <td>5883.4996</td>
      <td>0.0010</td>
      <td>5149.3641</td>
      <td>6617.6351</td>
      <td>True</td>
    </tr>
    <tr>
      <td>202</td>
      <td>11</td>
      <td>59</td>
      <td>879.2733</td>
      <td>0.0010</td>
      <td>278.3686</td>
      <td>1480.1780</td>
      <td>True</td>
    </tr>
    <tr>
      <td>224</td>
      <td>11</td>
      <td>9</td>
      <td>1399.5579</td>
      <td>0.0243</td>
      <td>60.0810</td>
      <td>2739.0348</td>
      <td>True</td>
    </tr>
    <tr>
      <td>242</td>
      <td>12</td>
      <td>29</td>
      <td>1813.3022</td>
      <td>0.0010</td>
      <td>882.9410</td>
      <td>2743.6635</td>
      <td>True</td>
    </tr>
    <tr>
      <td>252</td>
      <td>12</td>
      <td>38</td>
      <td>5551.8955</td>
      <td>0.0010</td>
      <td>4582.2760</td>
      <td>6521.5151</td>
      <td>True</td>
    </tr>
    <tr>
      <td>301</td>
      <td>13</td>
      <td>17</td>
      <td>746.4233</td>
      <td>0.0033</td>
      <td>99.5737</td>
      <td>1393.2730</td>
      <td>True</td>
    </tr>
    <tr>
      <td>302</td>
      <td>13</td>
      <td>18</td>
      <td>1053.8622</td>
      <td>0.0010</td>
      <td>352.5630</td>
      <td>1755.1614</td>
      <td>True</td>
    </tr>
    <tr>
      <td>305</td>
      <td>13</td>
      <td>20</td>
      <td>1346.3775</td>
      <td>0.0010</td>
      <td>513.4987</td>
      <td>2179.2563</td>
      <td>True</td>
    </tr>
    <tr>
      <td>312</td>
      <td>13</td>
      <td>27</td>
      <td>1561.5289</td>
      <td>0.0010</td>
      <td>522.7465</td>
      <td>2600.3113</td>
      <td>True</td>
    </tr>
    <tr>
      <td>314</td>
      <td>13</td>
      <td>29</td>
      <td>2379.8884</td>
      <td>0.0010</td>
      <td>1706.1425</td>
      <td>3053.6343</td>
      <td>True</td>
    </tr>
    <tr>
      <td>324</td>
      <td>13</td>
      <td>38</td>
      <td>6118.4817</td>
      <td>0.0010</td>
      <td>5391.4854</td>
      <td>6845.4779</td>
      <td>True</td>
    </tr>
    <tr>
      <td>339</td>
      <td>13</td>
      <td>51</td>
      <td>879.2084</td>
      <td>0.0010</td>
      <td>241.3808</td>
      <td>1517.0360</td>
      <td>True</td>
    </tr>
    <tr>
      <td>344</td>
      <td>13</td>
      <td>56</td>
      <td>771.5640</td>
      <td>0.0010</td>
      <td>174.2756</td>
      <td>1368.8524</td>
      <td>True</td>
    </tr>
    <tr>
      <td>347</td>
      <td>13</td>
      <td>59</td>
      <td>1114.2554</td>
      <td>0.0010</td>
      <td>522.0940</td>
      <td>1706.4167</td>
      <td>True</td>
    </tr>
    <tr>
      <td>349</td>
      <td>13</td>
      <td>60</td>
      <td>806.8600</td>
      <td>0.0010</td>
      <td>209.5716</td>
      <td>1404.1484</td>
      <td>True</td>
    </tr>
    <tr>
      <td>351</td>
      <td>13</td>
      <td>62</td>
      <td>845.3932</td>
      <td>0.0010</td>
      <td>239.6919</td>
      <td>1451.0945</td>
      <td>True</td>
    </tr>
    <tr>
      <td>352</td>
      <td>13</td>
      <td>63</td>
      <td>910.0988</td>
      <td>0.0068</td>
      <td>94.9052</td>
      <td>1725.2924</td>
      <td>True</td>
    </tr>
    <tr>
      <td>368</td>
      <td>13</td>
      <td>8</td>
      <td>927.6015</td>
      <td>0.0302</td>
      <td>28.6960</td>
      <td>1826.5071</td>
      <td>True</td>
    </tr>
    <tr>
      <td>369</td>
      <td>13</td>
      <td>9</td>
      <td>1634.5400</td>
      <td>0.0010</td>
      <td>298.9626</td>
      <td>2970.1174</td>
      <td>True</td>
    </tr>
    <tr>
      <td>373</td>
      <td>14</td>
      <td>18</td>
      <td>851.2508</td>
      <td>0.0268</td>
      <td>32.0188</td>
      <td>1670.4828</td>
      <td>True</td>
    </tr>
    <tr>
      <td>376</td>
      <td>14</td>
      <td>20</td>
      <td>1143.7661</td>
      <td>0.0010</td>
      <td>209.4173</td>
      <td>2078.1149</td>
      <td>True</td>
    </tr>
    <tr>
      <td>383</td>
      <td>14</td>
      <td>27</td>
      <td>1358.9175</td>
      <td>0.0010</td>
      <td>237.1379</td>
      <td>2480.6970</td>
      <td>True</td>
    </tr>
    <tr>
      <td>385</td>
      <td>14</td>
      <td>29</td>
      <td>2177.2770</td>
      <td>0.0010</td>
      <td>1381.5044</td>
      <td>2973.0496</td>
      <td>True</td>
    </tr>
    <tr>
      <td>395</td>
      <td>14</td>
      <td>38</td>
      <td>5915.8702</td>
      <td>0.0010</td>
      <td>5074.5356</td>
      <td>6757.2049</td>
      <td>True</td>
    </tr>
    <tr>
      <td>418</td>
      <td>14</td>
      <td>59</td>
      <td>911.6440</td>
      <td>0.0010</td>
      <td>183.6498</td>
      <td>1639.6381</td>
      <td>True</td>
    </tr>
    <tr>
      <td>440</td>
      <td>14</td>
      <td>9</td>
      <td>1431.9286</td>
      <td>0.0355</td>
      <td>30.8263</td>
      <td>2833.0308</td>
      <td>True</td>
    </tr>
    <tr>
      <td>455</td>
      <td>15</td>
      <td>29</td>
      <td>2208.4984</td>
      <td>0.0010</td>
      <td>952.6934</td>
      <td>3464.3033</td>
      <td>True</td>
    </tr>
    <tr>
      <td>465</td>
      <td>15</td>
      <td>38</td>
      <td>5947.0917</td>
      <td>0.0010</td>
      <td>4661.9317</td>
      <td>7232.2516</td>
      <td>True</td>
    </tr>
    <tr>
      <td>512</td>
      <td>16</td>
      <td>18</td>
      <td>748.7211</td>
      <td>0.0126</td>
      <td>57.3508</td>
      <td>1440.0914</td>
      <td>True</td>
    </tr>
    <tr>
      <td>515</td>
      <td>16</td>
      <td>20</td>
      <td>1041.2363</td>
      <td>0.0010</td>
      <td>216.7004</td>
      <td>1865.7723</td>
      <td>True</td>
    </tr>
    <tr>
      <td>522</td>
      <td>16</td>
      <td>27</td>
      <td>1256.3877</td>
      <td>0.0010</td>
      <td>224.2825</td>
      <td>2288.4930</td>
      <td>True</td>
    </tr>
    <tr>
      <td>524</td>
      <td>16</td>
      <td>29</td>
      <td>2074.7472</td>
      <td>0.0010</td>
      <td>1411.3425</td>
      <td>2738.1520</td>
      <td>True</td>
    </tr>
    <tr>
      <td>534</td>
      <td>16</td>
      <td>38</td>
      <td>5813.3405</td>
      <td>0.0010</td>
      <td>5095.9174</td>
      <td>6530.7636</td>
      <td>True</td>
    </tr>
    <tr>
      <td>557</td>
      <td>16</td>
      <td>59</td>
      <td>809.1142</td>
      <td>0.0010</td>
      <td>228.7459</td>
      <td>1389.4826</td>
      <td>True</td>
    </tr>
    <tr>
      <td>581</td>
      <td>17</td>
      <td>19</td>
      <td>-722.4083</td>
      <td>0.0114</td>
      <td>-1386.0621</td>
      <td>-58.7546</td>
      <td>True</td>
    </tr>
    <tr>
      <td>587</td>
      <td>17</td>
      <td>24</td>
      <td>-797.1282</td>
      <td>0.0010</td>
      <td>-1415.1987</td>
      <td>-179.0578</td>
      <td>True</td>
    </tr>
    <tr>
      <td>592</td>
      <td>17</td>
      <td>29</td>
      <td>1633.4651</td>
      <td>0.0010</td>
      <td>943.5699</td>
      <td>2323.3602</td>
      <td>True</td>
    </tr>
    <tr>
      <td>597</td>
      <td>17</td>
      <td>33</td>
      <td>-823.7365</td>
      <td>0.0012</td>
      <td>-1507.8151</td>
      <td>-139.6578</td>
      <td>True</td>
    </tr>
    <tr>
      <td>602</td>
      <td>17</td>
      <td>38</td>
      <td>5372.0583</td>
      <td>0.0010</td>
      <td>4630.0709</td>
      <td>6114.0458</td>
      <td>True</td>
    </tr>
    <tr>
      <td>606</td>
      <td>17</td>
      <td>41</td>
      <td>-717.9922</td>
      <td>0.0043</td>
      <td>-1347.5894</td>
      <td>-88.3950</td>
      <td>True</td>
    </tr>
    <tr>
      <td>618</td>
      <td>17</td>
      <td>52</td>
      <td>-773.9333</td>
      <td>0.0109</td>
      <td>-1483.4090</td>
      <td>-64.4576</td>
      <td>True</td>
    </tr>
    <tr>
      <td>620</td>
      <td>17</td>
      <td>54</td>
      <td>-735.0333</td>
      <td>0.0080</td>
      <td>-1398.6871</td>
      <td>-71.3796</td>
      <td>True</td>
    </tr>
    <tr>
      <td>643</td>
      <td>17</td>
      <td>75</td>
      <td>-705.7156</td>
      <td>0.0063</td>
      <td>-1335.3128</td>
      <td>-76.1183</td>
      <td>True</td>
    </tr>
    <tr>
      <td>648</td>
      <td>18</td>
      <td>19</td>
      <td>-1029.8472</td>
      <td>0.0010</td>
      <td>-1746.6752</td>
      <td>-313.0192</td>
      <td>True</td>
    </tr>
    <tr>
      <td>649</td>
      <td>18</td>
      <td>2</td>
      <td>-797.2990</td>
      <td>0.0034</td>
      <td>-1488.6693</td>
      <td>-105.9287</td>
      <td>True</td>
    </tr>
    <tr>
      <td>651</td>
      <td>18</td>
      <td>21</td>
      <td>-937.6453</td>
      <td>0.0010</td>
      <td>-1642.5584</td>
      <td>-232.7322</td>
      <td>True</td>
    </tr>
    <tr>
      <td>653</td>
      <td>18</td>
      <td>23</td>
      <td>-942.7122</td>
      <td>0.0048</td>
      <td>-1773.3848</td>
      <td>-112.0397</td>
      <td>True</td>
    </tr>
    <tr>
      <td>654</td>
      <td>18</td>
      <td>24</td>
      <td>-1104.5671</td>
      <td>0.0010</td>
      <td>-1779.4131</td>
      <td>-429.7211</td>
      <td>True</td>
    </tr>
    <tr>
      <td>655</td>
      <td>18</td>
      <td>25</td>
      <td>-959.6333</td>
      <td>0.0064</td>
      <td>-1816.4066</td>
      <td>-102.8600</td>
      <td>True</td>
    </tr>
    <tr>
      <td>659</td>
      <td>18</td>
      <td>29</td>
      <td>1326.0262</td>
      <td>0.0010</td>
      <td>584.8370</td>
      <td>2067.2153</td>
      <td>True</td>
    </tr>
    <tr>
      <td>662</td>
      <td>18</td>
      <td>31</td>
      <td>-867.6144</td>
      <td>0.0010</td>
      <td>-1537.7430</td>
      <td>-197.4858</td>
      <td>True</td>
    </tr>
    <tr>
      <td>664</td>
      <td>18</td>
      <td>33</td>
      <td>-1131.1753</td>
      <td>0.0010</td>
      <td>-1866.9536</td>
      <td>-395.3971</td>
      <td>True</td>
    </tr>
    <tr>
      <td>665</td>
      <td>18</td>
      <td>34</td>
      <td>-883.7222</td>
      <td>0.0304</td>
      <td>-1740.4955</td>
      <td>-26.9489</td>
      <td>True</td>
    </tr>
    <tr>
      <td>666</td>
      <td>18</td>
      <td>35</td>
      <td>-810.5279</td>
      <td>0.0059</td>
      <td>-1531.7313</td>
      <td>-89.3246</td>
      <td>True</td>
    </tr>
    <tr>
      <td>669</td>
      <td>18</td>
      <td>38</td>
      <td>5064.6194</td>
      <td>0.0010</td>
      <td>4274.7135</td>
      <td>5854.5254</td>
      <td>True</td>
    </tr>
    <tr>
      <td>670</td>
      <td>18</td>
      <td>39</td>
      <td>-811.9360</td>
      <td>0.0137</td>
      <td>-1564.9290</td>
      <td>-58.9430</td>
      <td>True</td>
    </tr>
    <tr>
      <td>672</td>
      <td>18</td>
      <td>40</td>
      <td>-750.3747</td>
      <td>0.0158</td>
      <td>-1451.6739</td>
      <td>-49.0755</td>
      <td>True</td>
    </tr>
    <tr>
      <td>673</td>
      <td>18</td>
      <td>41</td>
      <td>-1025.4311</td>
      <td>0.0010</td>
      <td>-1710.8498</td>
      <td>-340.0125</td>
      <td>True</td>
    </tr>
    <tr>
      <td>674</td>
      <td>18</td>
      <td>42</td>
      <td>-911.1912</td>
      <td>0.0011</td>
      <td>-1664.1842</td>
      <td>-158.1982</td>
      <td>True</td>
    </tr>
    <tr>
      <td>678</td>
      <td>18</td>
      <td>46</td>
      <td>-957.1667</td>
      <td>0.0010</td>
      <td>-1723.4880</td>
      <td>-190.8453</td>
      <td>True</td>
    </tr>
    <tr>
      <td>679</td>
      <td>18</td>
      <td>47</td>
      <td>-977.1698</td>
      <td>0.0015</td>
      <td>-1796.4018</td>
      <td>-157.9379</td>
      <td>True</td>
    </tr>
    <tr>
      <td>685</td>
      <td>18</td>
      <td>52</td>
      <td>-1081.3722</td>
      <td>0.0010</td>
      <td>-1840.8206</td>
      <td>-321.9239</td>
      <td>True</td>
    </tr>
    <tr>
      <td>687</td>
      <td>18</td>
      <td>54</td>
      <td>-1042.4722</td>
      <td>0.0010</td>
      <td>-1759.3002</td>
      <td>-325.6442</td>
      <td>True</td>
    </tr>
    <tr>
      <td>690</td>
      <td>18</td>
      <td>57</td>
      <td>-845.2527</td>
      <td>0.0195</td>
      <td>-1644.1979</td>
      <td>-46.3074</td>
      <td>True</td>
    </tr>
    <tr>
      <td>699</td>
      <td>18</td>
      <td>65</td>
      <td>-767.8513</td>
      <td>0.0282</td>
      <td>-1509.0404</td>
      <td>-26.6621</td>
      <td>True</td>
    </tr>
    <tr>
      <td>702</td>
      <td>18</td>
      <td>68</td>
      <td>-931.3131</td>
      <td>0.0010</td>
      <td>-1661.9719</td>
      <td>-200.6544</td>
      <td>True</td>
    </tr>
    <tr>
      <td>705</td>
      <td>18</td>
      <td>70</td>
      <td>-890.5684</td>
      <td>0.0010</td>
      <td>-1595.4815</td>
      <td>-185.6553</td>
      <td>True</td>
    </tr>
    <tr>
      <td>709</td>
      <td>18</td>
      <td>74</td>
      <td>-987.3376</td>
      <td>0.0269</td>
      <td>-1937.8422</td>
      <td>-36.8330</td>
      <td>True</td>
    </tr>
    <tr>
      <td>710</td>
      <td>18</td>
      <td>75</td>
      <td>-1013.1544</td>
      <td>0.0010</td>
      <td>-1698.5731</td>
      <td>-327.7358</td>
      <td>True</td>
    </tr>
    <tr>
      <td>711</td>
      <td>18</td>
      <td>76</td>
      <td>-785.4064</td>
      <td>0.0079</td>
      <td>-1494.1038</td>
      <td>-76.7091</td>
      <td>True</td>
    </tr>
    <tr>
      <td>712</td>
      <td>18</td>
      <td>77</td>
      <td>-947.5601</td>
      <td>0.0010</td>
      <td>-1660.2244</td>
      <td>-234.8957</td>
      <td>True</td>
    </tr>
    <tr>
      <td>716</td>
      <td>19</td>
      <td>20</td>
      <td>1322.3625</td>
      <td>0.0010</td>
      <td>476.3666</td>
      <td>2168.3584</td>
      <td>True</td>
    </tr>
    <tr>
      <td>723</td>
      <td>19</td>
      <td>27</td>
      <td>1537.5139</td>
      <td>0.0010</td>
      <td>488.1852</td>
      <td>2586.8426</td>
      <td>True</td>
    </tr>
    <tr>
      <td>725</td>
      <td>19</td>
      <td>29</td>
      <td>2355.8734</td>
      <td>0.0010</td>
      <td>1665.9782</td>
      <td>3045.7686</td>
      <td>True</td>
    </tr>
    <tr>
      <td>735</td>
      <td>19</td>
      <td>38</td>
      <td>6094.4667</td>
      <td>0.0010</td>
      <td>5352.4792</td>
      <td>6836.4541</td>
      <td>True</td>
    </tr>
    <tr>
      <td>750</td>
      <td>19</td>
      <td>51</td>
      <td>855.1934</td>
      <td>0.0010</td>
      <td>200.3302</td>
      <td>1510.0567</td>
      <td>True</td>
    </tr>
    <tr>
      <td>755</td>
      <td>19</td>
      <td>56</td>
      <td>747.5490</td>
      <td>0.0010</td>
      <td>132.1018</td>
      <td>1362.9962</td>
      <td>True</td>
    </tr>
    <tr>
      <td>758</td>
      <td>19</td>
      <td>59</td>
      <td>1090.2404</td>
      <td>0.0010</td>
      <td>479.7677</td>
      <td>1700.7130</td>
      <td>True</td>
    </tr>
    <tr>
      <td>760</td>
      <td>19</td>
      <td>60</td>
      <td>782.8450</td>
      <td>0.0010</td>
      <td>167.3978</td>
      <td>1398.2922</td>
      <td>True</td>
    </tr>
    <tr>
      <td>762</td>
      <td>19</td>
      <td>62</td>
      <td>821.3782</td>
      <td>0.0010</td>
      <td>197.7630</td>
      <td>1444.9934</td>
      <td>True</td>
    </tr>
    <tr>
      <td>763</td>
      <td>19</td>
      <td>63</td>
      <td>886.0838</td>
      <td>0.0160</td>
      <td>57.4932</td>
      <td>1714.6745</td>
      <td>True</td>
    </tr>
    <tr>
      <td>780</td>
      <td>19</td>
      <td>9</td>
      <td>1610.5250</td>
      <td>0.0014</td>
      <td>266.7286</td>
      <td>2954.3214</td>
      <td>True</td>
    </tr>
    <tr>
      <td>781</td>
      <td>2</td>
      <td>20</td>
      <td>1089.8142</td>
      <td>0.0010</td>
      <td>265.2783</td>
      <td>1914.3502</td>
      <td>True</td>
    </tr>
    <tr>
      <td>788</td>
      <td>2</td>
      <td>27</td>
      <td>1304.9656</td>
      <td>0.0010</td>
      <td>272.8604</td>
      <td>2337.0709</td>
      <td>True</td>
    </tr>
    <tr>
      <td>790</td>
      <td>2</td>
      <td>29</td>
      <td>2123.3251</td>
      <td>0.0010</td>
      <td>1459.9204</td>
      <td>2786.7299</td>
      <td>True</td>
    </tr>
    <tr>
      <td>800</td>
      <td>2</td>
      <td>38</td>
      <td>5861.9184</td>
      <td>0.0010</td>
      <td>5144.4953</td>
      <td>6579.3415</td>
      <td>True</td>
    </tr>
    <tr>
      <td>823</td>
      <td>2</td>
      <td>59</td>
      <td>857.6921</td>
      <td>0.0010</td>
      <td>277.3238</td>
      <td>1438.0605</td>
      <td>True</td>
    </tr>
    <tr>
      <td>845</td>
      <td>2</td>
      <td>9</td>
      <td>1377.9767</td>
      <td>0.0283</td>
      <td>47.5861</td>
      <td>2708.3674</td>
      <td>True</td>
    </tr>
    <tr>
      <td>846</td>
      <td>20</td>
      <td>21</td>
      <td>-1230.1606</td>
      <td>0.0010</td>
      <td>-2066.0847</td>
      <td>-394.2365</td>
      <td>True</td>
    </tr>
    <tr>
      <td>848</td>
      <td>20</td>
      <td>23</td>
      <td>-1235.2275</td>
      <td>0.0010</td>
      <td>-2179.6233</td>
      <td>-290.8317</td>
      <td>True</td>
    </tr>
    <tr>
      <td>849</td>
      <td>20</td>
      <td>24</td>
      <td>-1397.0824</td>
      <td>0.0010</td>
      <td>-2207.8128</td>
      <td>-586.3520</td>
      <td>True</td>
    </tr>
    <tr>
      <td>850</td>
      <td>20</td>
      <td>25</td>
      <td>-1252.1486</td>
      <td>0.0010</td>
      <td>-2219.5819</td>
      <td>-284.7153</td>
      <td>True</td>
    </tr>
    <tr>
      <td>854</td>
      <td>20</td>
      <td>29</td>
      <td>1033.5109</td>
      <td>0.0015</td>
      <td>166.7768</td>
      <td>1900.2450</td>
      <td>True</td>
    </tr>
    <tr>
      <td>855</td>
      <td>20</td>
      <td>3</td>
      <td>-1220.5708</td>
      <td>0.0048</td>
      <td>-2295.8128</td>
      <td>-145.3289</td>
      <td>True</td>
    </tr>
    <tr>
      <td>856</td>
      <td>20</td>
      <td>30</td>
      <td>-1015.5019</td>
      <td>0.0021</td>
      <td>-1877.6134</td>
      <td>-153.3904</td>
      <td>True</td>
    </tr>
    <tr>
      <td>857</td>
      <td>20</td>
      <td>31</td>
      <td>-1160.1297</td>
      <td>0.0010</td>
      <td>-1966.9375</td>
      <td>-353.3218</td>
      <td>True</td>
    </tr>
    <tr>
      <td>859</td>
      <td>20</td>
      <td>33</td>
      <td>-1423.6906</td>
      <td>0.0010</td>
      <td>-2285.8021</td>
      <td>-561.5791</td>
      <td>True</td>
    </tr>
    <tr>
      <td>860</td>
      <td>20</td>
      <td>34</td>
      <td>-1176.2375</td>
      <td>0.0010</td>
      <td>-2143.6708</td>
      <td>-208.8042</td>
      <td>True</td>
    </tr>
    <tr>
      <td>861</td>
      <td>20</td>
      <td>35</td>
      <td>-1103.0432</td>
      <td>0.0010</td>
      <td>-1952.7496</td>
      <td>-253.3368</td>
      <td>True</td>
    </tr>
    <tr>
      <td>862</td>
      <td>20</td>
      <td>36</td>
      <td>-1008.1214</td>
      <td>0.0028</td>
      <td>-1874.8555</td>
      <td>-141.3872</td>
      <td>True</td>
    </tr>
    <tr>
      <td>864</td>
      <td>20</td>
      <td>38</td>
      <td>4772.1042</td>
      <td>0.0010</td>
      <td>3863.3588</td>
      <td>5680.8495</td>
      <td>True</td>
    </tr>
    <tr>
      <td>865</td>
      <td>20</td>
      <td>39</td>
      <td>-1104.4513</td>
      <td>0.0010</td>
      <td>-1981.3008</td>
      <td>-227.6018</td>
      <td>True</td>
    </tr>
    <tr>
      <td>866</td>
      <td>20</td>
      <td>4</td>
      <td>-1005.9975</td>
      <td>0.0172</td>
      <td>-1950.3933</td>
      <td>-61.6017</td>
      <td>True</td>
    </tr>
    <tr>
      <td>867</td>
      <td>20</td>
      <td>40</td>
      <td>-1042.8900</td>
      <td>0.0010</td>
      <td>-1875.7688</td>
      <td>-210.0112</td>
      <td>True</td>
    </tr>
    <tr>
      <td>868</td>
      <td>20</td>
      <td>41</td>
      <td>-1317.9464</td>
      <td>0.0010</td>
      <td>-2137.4983</td>
      <td>-498.3945</td>
      <td>True</td>
    </tr>
    <tr>
      <td>869</td>
      <td>20</td>
      <td>42</td>
      <td>-1203.7065</td>
      <td>0.0010</td>
      <td>-2080.5560</td>
      <td>-326.8569</td>
      <td>True</td>
    </tr>
    <tr>
      <td>871</td>
      <td>20</td>
      <td>44</td>
      <td>-1087.0549</td>
      <td>0.0017</td>
      <td>-2003.6683</td>
      <td>-170.4415</td>
      <td>True</td>
    </tr>
    <tr>
      <td>872</td>
      <td>20</td>
      <td>45</td>
      <td>-1138.6304</td>
      <td>0.0084</td>
      <td>-2169.0507</td>
      <td>-108.2100</td>
      <td>True</td>
    </tr>
    <tr>
      <td>873</td>
      <td>20</td>
      <td>46</td>
      <td>-1249.6819</td>
      <td>0.0010</td>
      <td>-2138.0034</td>
      <td>-361.3605</td>
      <td>True</td>
    </tr>
    <tr>
      <td>874</td>
      <td>20</td>
      <td>47</td>
      <td>-1269.6851</td>
      <td>0.0010</td>
      <td>-2204.0339</td>
      <td>-335.3363</td>
      <td>True</td>
    </tr>
    <tr>
      <td>876</td>
      <td>20</td>
      <td>49</td>
      <td>-1024.8565</td>
      <td>0.0098</td>
      <td>-1959.2053</td>
      <td>-90.5078</td>
      <td>True</td>
    </tr>
    <tr>
      <td>880</td>
      <td>20</td>
      <td>52</td>
      <td>-1373.8875</td>
      <td>0.0010</td>
      <td>-2256.2868</td>
      <td>-491.4882</td>
      <td>True</td>
    </tr>
    <tr>
      <td>882</td>
      <td>20</td>
      <td>54</td>
      <td>-1334.9875</td>
      <td>0.0010</td>
      <td>-2180.9834</td>
      <td>-488.9916</td>
      <td>True</td>
    </tr>
    <tr>
      <td>883</td>
      <td>20</td>
      <td>55</td>
      <td>-885.9648</td>
      <td>0.0297</td>
      <td>-1743.7111</td>
      <td>-28.2184</td>
      <td>True</td>
    </tr>
    <tr>
      <td>885</td>
      <td>20</td>
      <td>57</td>
      <td>-1137.7679</td>
      <td>0.0010</td>
      <td>-2054.3813</td>
      <td>-221.1545</td>
      <td>True</td>
    </tr>
    <tr>
      <td>886</td>
      <td>20</td>
      <td>58</td>
      <td>-1106.9736</td>
      <td>0.0040</td>
      <td>-2074.4069</td>
      <td>-139.5403</td>
      <td>True</td>
    </tr>
    <tr>
      <td>894</td>
      <td>20</td>
      <td>65</td>
      <td>-1060.3665</td>
      <td>0.0010</td>
      <td>-1927.1007</td>
      <td>-193.6324</td>
      <td>True</td>
    </tr>
    <tr>
      <td>896</td>
      <td>20</td>
      <td>67</td>
      <td>-1221.0375</td>
      <td>0.0143</td>
      <td>-2356.0600</td>
      <td>-86.0150</td>
      <td>True</td>
    </tr>
    <tr>
      <td>897</td>
      <td>20</td>
      <td>68</td>
      <td>-1223.8284</td>
      <td>0.0010</td>
      <td>-2081.5748</td>
      <td>-366.0821</td>
      <td>True</td>
    </tr>
    <tr>
      <td>900</td>
      <td>20</td>
      <td>70</td>
      <td>-1183.0837</td>
      <td>0.0010</td>
      <td>-2019.0078</td>
      <td>-347.1595</td>
      <td>True</td>
    </tr>
    <tr>
      <td>901</td>
      <td>20</td>
      <td>71</td>
      <td>-980.1780</td>
      <td>0.0018</td>
      <td>-1807.3716</td>
      <td>-152.9844</td>
      <td>True</td>
    </tr>
    <tr>
      <td>903</td>
      <td>20</td>
      <td>73</td>
      <td>-1177.2375</td>
      <td>0.0042</td>
      <td>-2207.6578</td>
      <td>-146.8172</td>
      <td>True</td>
    </tr>
    <tr>
      <td>904</td>
      <td>20</td>
      <td>74</td>
      <td>-1279.8529</td>
      <td>0.0010</td>
      <td>-2331.1976</td>
      <td>-228.5082</td>
      <td>True</td>
    </tr>
    <tr>
      <td>905</td>
      <td>20</td>
      <td>75</td>
      <td>-1305.6697</td>
      <td>0.0010</td>
      <td>-2125.2216</td>
      <td>-486.1178</td>
      <td>True</td>
    </tr>
    <tr>
      <td>906</td>
      <td>20</td>
      <td>76</td>
      <td>-1077.9217</td>
      <td>0.0010</td>
      <td>-1917.0394</td>
      <td>-238.8040</td>
      <td>True</td>
    </tr>
    <tr>
      <td>907</td>
      <td>20</td>
      <td>77</td>
      <td>-1240.0753</td>
      <td>0.0010</td>
      <td>-2082.5462</td>
      <td>-397.6045</td>
      <td>True</td>
    </tr>
    <tr>
      <td>915</td>
      <td>21</td>
      <td>27</td>
      <td>1445.3120</td>
      <td>0.0010</td>
      <td>404.0863</td>
      <td>2486.5376</td>
      <td>True</td>
    </tr>
    <tr>
      <td>917</td>
      <td>21</td>
      <td>29</td>
      <td>2263.6715</td>
      <td>0.0010</td>
      <td>1586.1646</td>
      <td>2941.1783</td>
      <td>True</td>
    </tr>
    <tr>
      <td>927</td>
      <td>21</td>
      <td>38</td>
      <td>6002.2647</td>
      <td>0.0010</td>
      <td>5271.7817</td>
      <td>6732.7478</td>
      <td>True</td>
    </tr>
    <tr>
      <td>942</td>
      <td>21</td>
      <td>51</td>
      <td>762.9915</td>
      <td>0.0016</td>
      <td>121.1925</td>
      <td>1404.7905</td>
      <td>True</td>
    </tr>
    <tr>
      <td>947</td>
      <td>21</td>
      <td>56</td>
      <td>655.3471</td>
      <td>0.0112</td>
      <td>53.8196</td>
      <td>1256.8746</td>
      <td>True</td>
    </tr>
    <tr>
      <td>950</td>
      <td>21</td>
      <td>59</td>
      <td>998.0385</td>
      <td>0.0010</td>
      <td>401.6015</td>
      <td>1594.4754</td>
      <td>True</td>
    </tr>
    <tr>
      <td>952</td>
      <td>21</td>
      <td>60</td>
      <td>690.6431</td>
      <td>0.0037</td>
      <td>89.1156</td>
      <td>1292.1706</td>
      <td>True</td>
    </tr>
    <tr>
      <td>954</td>
      <td>21</td>
      <td>62</td>
      <td>729.1763</td>
      <td>0.0014</td>
      <td>119.2943</td>
      <td>1339.0582</td>
      <td>True</td>
    </tr>
    <tr>
      <td>972</td>
      <td>21</td>
      <td>9</td>
      <td>1518.3231</td>
      <td>0.0048</td>
      <td>180.8445</td>
      <td>2855.8017</td>
      <td>True</td>
    </tr>
    <tr>
      <td>979</td>
      <td>22</td>
      <td>29</td>
      <td>1994.1484</td>
      <td>0.0010</td>
      <td>1087.4994</td>
      <td>2900.7974</td>
      <td>True</td>
    </tr>
    <tr>
      <td>989</td>
      <td>22</td>
      <td>38</td>
      <td>5732.7417</td>
      <td>0.0010</td>
      <td>4785.8507</td>
      <td>6679.6326</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1038</td>
      <td>23</td>
      <td>27</td>
      <td>1450.3789</td>
      <td>0.0010</td>
      <td>320.2173</td>
      <td>2580.5405</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1040</td>
      <td>23</td>
      <td>29</td>
      <td>2268.7384</td>
      <td>0.0010</td>
      <td>1461.1928</td>
      <td>3076.2840</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1050</td>
      <td>23</td>
      <td>38</td>
      <td>6007.3317</td>
      <td>0.0010</td>
      <td>5154.8530</td>
      <td>6859.8103</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1073</td>
      <td>23</td>
      <td>59</td>
      <td>1003.1054</td>
      <td>0.0010</td>
      <td>262.2603</td>
      <td>1743.9504</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1095</td>
      <td>23</td>
      <td>9</td>
      <td>1523.3900</td>
      <td>0.0128</td>
      <td>115.5678</td>
      <td>2931.2122</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1098</td>
      <td>24</td>
      <td>27</td>
      <td>1612.2338</td>
      <td>0.0010</td>
      <td>591.1238</td>
      <td>2633.3437</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1099</td>
      <td>24</td>
      <td>28</td>
      <td>659.6449</td>
      <td>0.0308</td>
      <td>19.6931</td>
      <td>1299.5967</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1100</td>
      <td>24</td>
      <td>29</td>
      <td>2430.5933</td>
      <td>0.0010</td>
      <td>1784.4276</td>
      <td>3076.7590</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1110</td>
      <td>24</td>
      <td>38</td>
      <td>6169.1866</td>
      <td>0.0010</td>
      <td>5467.6738</td>
      <td>6870.6993</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1116</td>
      <td>24</td>
      <td>43</td>
      <td>746.4819</td>
      <td>0.0083</td>
      <td>71.6359</td>
      <td>1421.3279</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1125</td>
      <td>24</td>
      <td>51</td>
      <td>929.9133</td>
      <td>0.0010</td>
      <td>321.2914</td>
      <td>1538.5352</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1130</td>
      <td>24</td>
      <td>56</td>
      <td>822.2689</td>
      <td>0.0010</td>
      <td>256.2742</td>
      <td>1388.2636</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1133</td>
      <td>24</td>
      <td>59</td>
      <td>1164.9603</td>
      <td>0.0010</td>
      <td>604.3788</td>
      <td>1725.5418</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1135</td>
      <td>24</td>
      <td>60</td>
      <td>857.5649</td>
      <td>0.0010</td>
      <td>291.5702</td>
      <td>1423.5596</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1137</td>
      <td>24</td>
      <td>62</td>
      <td>896.0981</td>
      <td>0.0010</td>
      <td>321.2323</td>
      <td>1470.9639</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1138</td>
      <td>24</td>
      <td>63</td>
      <td>960.8037</td>
      <td>0.0010</td>
      <td>168.2526</td>
      <td>1753.3548</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1144</td>
      <td>24</td>
      <td>69</td>
      <td>703.9481</td>
      <td>0.0112</td>
      <td>57.7824</td>
      <td>1350.1138</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1145</td>
      <td>24</td>
      <td>7</td>
      <td>694.4656</td>
      <td>0.0213</td>
      <td>34.7936</td>
      <td>1354.1376</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1154</td>
      <td>24</td>
      <td>8</td>
      <td>978.3064</td>
      <td>0.0072</td>
      <td>99.8830</td>
      <td>1856.7299</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1155</td>
      <td>24</td>
      <td>9</td>
      <td>1685.2449</td>
      <td>0.0010</td>
      <td>363.3661</td>
      <td>3007.1237</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1157</td>
      <td>25</td>
      <td>27</td>
      <td>1467.3000</td>
      <td>0.0010</td>
      <td>317.8180</td>
      <td>2616.7820</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1159</td>
      <td>25</td>
      <td>29</td>
      <td>2285.6595</td>
      <td>0.0010</td>
      <td>1451.2894</td>
      <td>3120.0296</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1169</td>
      <td>25</td>
      <td>38</td>
      <td>6024.2528</td>
      <td>0.0010</td>
      <td>5146.3214</td>
      <td>6902.1842</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1192</td>
      <td>25</td>
      <td>59</td>
      <td>1020.0265</td>
      <td>0.0010</td>
      <td>250.0297</td>
      <td>1790.0233</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1214</td>
      <td>25</td>
      <td>9</td>
      <td>1540.3111</td>
      <td>0.0128</td>
      <td>116.9324</td>
      <td>2963.6898</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1217</td>
      <td>26</td>
      <td>29</td>
      <td>1837.7828</td>
      <td>0.0010</td>
      <td>1128.2177</td>
      <td>2547.3479</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1227</td>
      <td>26</td>
      <td>38</td>
      <td>5576.3760</td>
      <td>0.0010</td>
      <td>4816.0652</td>
      <td>6336.6869</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1275</td>
      <td>27</td>
      <td>3</td>
      <td>-1435.7222</td>
      <td>0.0032</td>
      <td>-2677.3047</td>
      <td>-194.1397</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1276</td>
      <td>27</td>
      <td>30</td>
      <td>-1230.6533</td>
      <td>0.0030</td>
      <td>-2293.0176</td>
      <td>-168.2889</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1277</td>
      <td>27</td>
      <td>31</td>
      <td>-1375.2810</td>
      <td>0.0010</td>
      <td>-2393.2794</td>
      <td>-357.2827</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1279</td>
      <td>27</td>
      <td>33</td>
      <td>-1638.8420</td>
      <td>0.0010</td>
      <td>-2701.2064</td>
      <td>-576.4777</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1280</td>
      <td>27</td>
      <td>34</td>
      <td>-1391.3889</td>
      <td>0.0011</td>
      <td>-2540.8709</td>
      <td>-241.9069</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1281</td>
      <td>27</td>
      <td>35</td>
      <td>-1318.1946</td>
      <td>0.0010</td>
      <td>-2370.5171</td>
      <td>-265.8721</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1282</td>
      <td>27</td>
      <td>36</td>
      <td>-1223.2728</td>
      <td>0.0038</td>
      <td>-2289.3918</td>
      <td>-157.1537</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1284</td>
      <td>27</td>
      <td>38</td>
      <td>4556.9528</td>
      <td>0.0010</td>
      <td>3456.4075</td>
      <td>5657.4980</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1285</td>
      <td>27</td>
      <td>39</td>
      <td>-1319.6027</td>
      <td>0.0010</td>
      <td>-2393.9615</td>
      <td>-245.2439</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1286</td>
      <td>27</td>
      <td>4</td>
      <td>-1221.1489</td>
      <td>0.0131</td>
      <td>-2351.3105</td>
      <td>-90.9873</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1287</td>
      <td>27</td>
      <td>40</td>
      <td>-1258.0414</td>
      <td>0.0010</td>
      <td>-2296.8238</td>
      <td>-219.2590</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1288</td>
      <td>27</td>
      <td>41</td>
      <td>-1533.0978</td>
      <td>0.0010</td>
      <td>-2561.2257</td>
      <td>-504.9698</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1289</td>
      <td>27</td>
      <td>42</td>
      <td>-1418.8579</td>
      <td>0.0010</td>
      <td>-2493.2167</td>
      <td>-344.4990</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1291</td>
      <td>27</td>
      <td>44</td>
      <td>-1302.2063</td>
      <td>0.0021</td>
      <td>-2409.2573</td>
      <td>-195.1553</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1292</td>
      <td>27</td>
      <td>45</td>
      <td>-1353.7817</td>
      <td>0.0058</td>
      <td>-2556.7563</td>
      <td>-150.8072</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1293</td>
      <td>27</td>
      <td>46</td>
      <td>-1464.8333</td>
      <td>0.0010</td>
      <td>-2548.5754</td>
      <td>-381.0913</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1294</td>
      <td>27</td>
      <td>47</td>
      <td>-1484.8365</td>
      <td>0.0010</td>
      <td>-2606.6161</td>
      <td>-363.0569</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1296</td>
      <td>27</td>
      <td>49</td>
      <td>-1240.0079</td>
      <td>0.0084</td>
      <td>-2361.7875</td>
      <td>-118.2284</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1298</td>
      <td>27</td>
      <td>50</td>
      <td>-1341.3889</td>
      <td>0.0278</td>
      <td>-2635.0882</td>
      <td>-47.6896</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1300</td>
      <td>27</td>
      <td>52</td>
      <td>-1589.0389</td>
      <td>0.0010</td>
      <td>-2667.9319</td>
      <td>-510.1458</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1301</td>
      <td>27</td>
      <td>53</td>
      <td>-1086.3820</td>
      <td>0.0422</td>
      <td>-2160.7408</td>
      <td>-12.0232</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1302</td>
      <td>27</td>
      <td>54</td>
      <td>-1550.1389</td>
      <td>0.0010</td>
      <td>-2599.4676</td>
      <td>-500.8102</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1303</td>
      <td>27</td>
      <td>55</td>
      <td>-1101.1162</td>
      <td>0.0264</td>
      <td>-2159.9413</td>
      <td>-42.2911</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1305</td>
      <td>27</td>
      <td>57</td>
      <td>-1352.9193</td>
      <td>0.0010</td>
      <td>-2459.9703</td>
      <td>-245.8683</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1306</td>
      <td>27</td>
      <td>58</td>
      <td>-1322.1250</td>
      <td>0.0036</td>
      <td>-2471.6070</td>
      <td>-172.6430</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1310</td>
      <td>27</td>
      <td>61</td>
      <td>-1126.3541</td>
      <td>0.0382</td>
      <td>-2233.4051</td>
      <td>-19.3031</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1314</td>
      <td>27</td>
      <td>65</td>
      <td>-1275.5179</td>
      <td>0.0014</td>
      <td>-2341.6370</td>
      <td>-209.3989</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1316</td>
      <td>27</td>
      <td>67</td>
      <td>-1436.1889</td>
      <td>0.0077</td>
      <td>-2729.8882</td>
      <td>-142.4896</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1317</td>
      <td>27</td>
      <td>68</td>
      <td>-1438.9798</td>
      <td>0.0010</td>
      <td>-2497.8049</td>
      <td>-380.1547</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1320</td>
      <td>27</td>
      <td>70</td>
      <td>-1398.2350</td>
      <td>0.0010</td>
      <td>-2439.4607</td>
      <td>-357.0094</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1321</td>
      <td>27</td>
      <td>71</td>
      <td>-1195.3294</td>
      <td>0.0032</td>
      <td>-2229.5590</td>
      <td>-161.0997</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1322</td>
      <td>27</td>
      <td>72</td>
      <td>-1053.1781</td>
      <td>0.0454</td>
      <td>-2099.6669</td>
      <td>-6.6892</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1323</td>
      <td>27</td>
      <td>73</td>
      <td>-1392.3889</td>
      <td>0.0031</td>
      <td>-2595.3635</td>
      <td>-189.4143</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1324</td>
      <td>27</td>
      <td>74</td>
      <td>-1495.0043</td>
      <td>0.0010</td>
      <td>-2715.9496</td>
      <td>-274.0590</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1325</td>
      <td>27</td>
      <td>75</td>
      <td>-1520.8211</td>
      <td>0.0010</td>
      <td>-2548.9491</td>
      <td>-492.6931</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1326</td>
      <td>27</td>
      <td>76</td>
      <td>-1293.0731</td>
      <td>0.0010</td>
      <td>-2336.8644</td>
      <td>-249.2818</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1327</td>
      <td>27</td>
      <td>77</td>
      <td>-1455.2267</td>
      <td>0.0010</td>
      <td>-2501.7156</td>
      <td>-408.7379</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1330</td>
      <td>28</td>
      <td>29</td>
      <td>1770.9484</td>
      <td>0.0010</td>
      <td>1061.3833</td>
      <td>2480.5135</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1340</td>
      <td>28</td>
      <td>38</td>
      <td>5509.5417</td>
      <td>0.0010</td>
      <td>4749.2308</td>
      <td>6269.8525</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1386</td>
      <td>29</td>
      <td>3</td>
      <td>-2254.0817</td>
      <td>0.0010</td>
      <td>-3211.3652</td>
      <td>-1296.7982</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1387</td>
      <td>29</td>
      <td>30</td>
      <td>-2049.0128</td>
      <td>0.0010</td>
      <td>-2758.5779</td>
      <td>-1339.4477</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1388</td>
      <td>29</td>
      <td>31</td>
      <td>-2193.6405</td>
      <td>0.0010</td>
      <td>-2834.8779</td>
      <td>-1552.4032</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1389</td>
      <td>29</td>
      <td>32</td>
      <td>-1899.3351</td>
      <td>0.0010</td>
      <td>-2784.9200</td>
      <td>-1013.7501</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1390</td>
      <td>29</td>
      <td>33</td>
      <td>-2457.2015</td>
      <td>0.0010</td>
      <td>-3166.7666</td>
      <td>-1747.6364</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1391</td>
      <td>29</td>
      <td>34</td>
      <td>-2209.7484</td>
      <td>0.0010</td>
      <td>-3044.1185</td>
      <td>-1375.3783</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1392</td>
      <td>29</td>
      <td>35</td>
      <td>-2136.5541</td>
      <td>0.0010</td>
      <td>-2830.9944</td>
      <td>-1442.1138</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1393</td>
      <td>29</td>
      <td>36</td>
      <td>-2041.6323</td>
      <td>0.0010</td>
      <td>-2756.8066</td>
      <td>-1326.4579</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1394</td>
      <td>29</td>
      <td>37</td>
      <td>-2002.8817</td>
      <td>0.0010</td>
      <td>-3258.6867</td>
      <td>-747.0768</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1395</td>
      <td>29</td>
      <td>38</td>
      <td>3738.5933</td>
      <td>0.0010</td>
      <td>2973.0448</td>
      <td>4504.1417</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1396</td>
      <td>29</td>
      <td>39</td>
      <td>-2137.9622</td>
      <td>0.0010</td>
      <td>-2865.3627</td>
      <td>-1410.5617</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1397</td>
      <td>29</td>
      <td>4</td>
      <td>-2039.5084</td>
      <td>0.0010</td>
      <td>-2847.0540</td>
      <td>-1231.9628</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1398</td>
      <td>29</td>
      <td>40</td>
      <td>-2076.4009</td>
      <td>0.0010</td>
      <td>-2750.1468</td>
      <td>-1402.6550</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1399</td>
      <td>29</td>
      <td>41</td>
      <td>-2351.4573</td>
      <td>0.0010</td>
      <td>-3008.6572</td>
      <td>-1694.2574</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1400</td>
      <td>29</td>
      <td>42</td>
      <td>-2237.2174</td>
      <td>0.0010</td>
      <td>-2964.6178</td>
      <td>-1509.8169</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1401</td>
      <td>29</td>
      <td>43</td>
      <td>-1684.1114</td>
      <td>0.0010</td>
      <td>-2425.3005</td>
      <td>-942.9222</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1402</td>
      <td>29</td>
      <td>44</td>
      <td>-2120.5658</td>
      <td>0.0010</td>
      <td>-2895.4377</td>
      <td>-1345.6939</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1403</td>
      <td>29</td>
      <td>45</td>
      <td>-2172.1412</td>
      <td>0.0010</td>
      <td>-3078.7903</td>
      <td>-1265.4922</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1404</td>
      <td>29</td>
      <td>46</td>
      <td>-2283.1928</td>
      <td>0.0010</td>
      <td>-3024.3820</td>
      <td>-1542.0037</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1405</td>
      <td>29</td>
      <td>47</td>
      <td>-2303.1960</td>
      <td>0.0010</td>
      <td>-3098.9686</td>
      <td>-1507.4234</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1406</td>
      <td>29</td>
      <td>48</td>
      <td>-2253.6234</td>
      <td>0.0010</td>
      <td>-3509.4283</td>
      <td>-997.8184</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1407</td>
      <td>29</td>
      <td>49</td>
      <td>-2058.3674</td>
      <td>0.0010</td>
      <td>-2854.1400</td>
      <td>-1262.5948</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1408</td>
      <td>29</td>
      <td>5</td>
      <td>-1930.6334</td>
      <td>0.0010</td>
      <td>-2954.6073</td>
      <td>-906.6595</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1409</td>
      <td>29</td>
      <td>50</td>
      <td>-2159.7484</td>
      <td>0.0010</td>
      <td>-3183.7223</td>
      <td>-1135.7745</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1410</td>
      <td>29</td>
      <td>51</td>
      <td>-1500.6800</td>
      <td>0.0010</td>
      <td>-2182.1232</td>
      <td>-819.2367</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1411</td>
      <td>29</td>
      <td>52</td>
      <td>-2407.3984</td>
      <td>0.0010</td>
      <td>-3141.4793</td>
      <td>-1673.3174</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1412</td>
      <td>29</td>
      <td>53</td>
      <td>-1904.7415</td>
      <td>0.0010</td>
      <td>-2632.1420</td>
      <td>-1177.3410</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1413</td>
      <td>29</td>
      <td>54</td>
      <td>-2368.4984</td>
      <td>0.0010</td>
      <td>-3058.3936</td>
      <td>-1678.6032</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1414</td>
      <td>29</td>
      <td>55</td>
      <td>-1919.4757</td>
      <td>0.0010</td>
      <td>-2623.7307</td>
      <td>-1215.2206</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1415</td>
      <td>29</td>
      <td>56</td>
      <td>-1608.3244</td>
      <td>0.0010</td>
      <td>-2251.9813</td>
      <td>-964.6674</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1416</td>
      <td>29</td>
      <td>57</td>
      <td>-2171.2788</td>
      <td>0.0010</td>
      <td>-2946.1507</td>
      <td>-1396.4069</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1417</td>
      <td>29</td>
      <td>58</td>
      <td>-2140.4845</td>
      <td>0.0010</td>
      <td>-2974.8546</td>
      <td>-1306.1144</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1418</td>
      <td>29</td>
      <td>59</td>
      <td>-1265.6330</td>
      <td>0.0010</td>
      <td>-1904.5351</td>
      <td>-626.7309</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1419</td>
      <td>29</td>
      <td>6</td>
      <td>-1898.6651</td>
      <td>0.0010</td>
      <td>-2855.9485</td>
      <td>-941.3816</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1420</td>
      <td>29</td>
      <td>60</td>
      <td>-1573.0284</td>
      <td>0.0010</td>
      <td>-2216.6853</td>
      <td>-929.3714</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1421</td>
      <td>29</td>
      <td>61</td>
      <td>-1944.7136</td>
      <td>0.0010</td>
      <td>-2719.5855</td>
      <td>-1169.8417</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1422</td>
      <td>29</td>
      <td>62</td>
      <td>-1534.4952</td>
      <td>0.0010</td>
      <td>-2185.9666</td>
      <td>-883.0238</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1423</td>
      <td>29</td>
      <td>63</td>
      <td>-1469.7896</td>
      <td>0.0010</td>
      <td>-2319.5434</td>
      <td>-620.0358</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1424</td>
      <td>29</td>
      <td>64</td>
      <td>-1866.3863</td>
      <td>0.0010</td>
      <td>-2593.7868</td>
      <td>-1138.9858</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1425</td>
      <td>29</td>
      <td>65</td>
      <td>-2093.8774</td>
      <td>0.0010</td>
      <td>-2809.0518</td>
      <td>-1378.7030</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1426</td>
      <td>29</td>
      <td>66</td>
      <td>-2070.8734</td>
      <td>0.0010</td>
      <td>-3187.4390</td>
      <td>-954.3077</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1427</td>
      <td>29</td>
      <td>67</td>
      <td>-2254.5484</td>
      <td>0.0010</td>
      <td>-3278.5223</td>
      <td>-1230.5745</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1428</td>
      <td>29</td>
      <td>68</td>
      <td>-2257.3393</td>
      <td>0.0010</td>
      <td>-2961.5944</td>
      <td>-1553.0842</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1429</td>
      <td>29</td>
      <td>69</td>
      <td>-1726.6452</td>
      <td>0.0010</td>
      <td>-2441.8196</td>
      <td>-1011.4708</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1430</td>
      <td>29</td>
      <td>7</td>
      <td>-1736.1277</td>
      <td>0.0010</td>
      <td>-2463.5282</td>
      <td>-1008.7272</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1431</td>
      <td>29</td>
      <td>70</td>
      <td>-2216.5945</td>
      <td>0.0010</td>
      <td>-2894.1014</td>
      <td>-1539.0877</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1432</td>
      <td>29</td>
      <td>71</td>
      <td>-2013.6889</td>
      <td>0.0010</td>
      <td>-2680.3939</td>
      <td>-1346.9838</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1433</td>
      <td>29</td>
      <td>72</td>
      <td>-1871.5376</td>
      <td>0.0010</td>
      <td>-2557.1056</td>
      <td>-1185.9696</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1434</td>
      <td>29</td>
      <td>73</td>
      <td>-2210.7484</td>
      <td>0.0010</td>
      <td>-3117.3974</td>
      <td>-1304.0994</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1435</td>
      <td>29</td>
      <td>74</td>
      <td>-2313.3638</td>
      <td>0.0010</td>
      <td>-3243.7250</td>
      <td>-1383.0025</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1436</td>
      <td>29</td>
      <td>75</td>
      <td>-2339.1806</td>
      <td>0.0010</td>
      <td>-2996.3805</td>
      <td>-1681.9807</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1437</td>
      <td>29</td>
      <td>76</td>
      <td>-2111.4326</td>
      <td>0.0010</td>
      <td>-2792.8759</td>
      <td>-1429.9893</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1438</td>
      <td>29</td>
      <td>77</td>
      <td>-2273.5862</td>
      <td>0.0010</td>
      <td>-2959.1542</td>
      <td>-1588.0182</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1439</td>
      <td>29</td>
      <td>8</td>
      <td>-1452.2868</td>
      <td>0.0010</td>
      <td>-2382.6481</td>
      <td>-521.9256</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1449</td>
      <td>3</td>
      <td>38</td>
      <td>5992.6750</td>
      <td>0.0010</td>
      <td>4997.1944</td>
      <td>6988.1556</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1472</td>
      <td>3</td>
      <td>59</td>
      <td>988.4487</td>
      <td>0.0099</td>
      <td>86.7208</td>
      <td>1890.1766</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1494</td>
      <td>3</td>
      <td>9</td>
      <td>1508.7333</td>
      <td>0.0453</td>
      <td>9.9922</td>
      <td>3007.4745</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1502</td>
      <td>30</td>
      <td>38</td>
      <td>5787.6060</td>
      <td>0.0010</td>
      <td>5027.2952</td>
      <td>6547.9169</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1525</td>
      <td>30</td>
      <td>59</td>
      <td>783.3798</td>
      <td>0.0010</td>
      <td>150.7629</td>
      <td>1415.9967</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1554</td>
      <td>31</td>
      <td>38</td>
      <td>5932.2338</td>
      <td>0.0010</td>
      <td>5235.2580</td>
      <td>6629.2097</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1569</td>
      <td>31</td>
      <td>51</td>
      <td>692.9606</td>
      <td>0.0037</td>
      <td>89.5736</td>
      <td>1296.3475</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1574</td>
      <td>31</td>
      <td>56</td>
      <td>585.3162</td>
      <td>0.0244</td>
      <td>24.9545</td>
      <td>1145.6778</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1577</td>
      <td>31</td>
      <td>59</td>
      <td>928.0075</td>
      <td>0.0010</td>
      <td>373.1140</td>
      <td>1482.9011</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1579</td>
      <td>31</td>
      <td>60</td>
      <td>620.6122</td>
      <td>0.0081</td>
      <td>60.2505</td>
      <td>1180.9738</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1581</td>
      <td>31</td>
      <td>62</td>
      <td>659.1453</td>
      <td>0.0031</td>
      <td>89.8248</td>
      <td>1228.4659</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1599</td>
      <td>31</td>
      <td>9</td>
      <td>1448.2922</td>
      <td>0.0096</td>
      <td>128.8155</td>
      <td>2767.7689</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1605</td>
      <td>32</td>
      <td>38</td>
      <td>5637.9283</td>
      <td>0.0010</td>
      <td>4711.1863</td>
      <td>6564.6704</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1655</td>
      <td>33</td>
      <td>38</td>
      <td>6195.7948</td>
      <td>0.0010</td>
      <td>5435.4839</td>
      <td>6956.1057</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1661</td>
      <td>33</td>
      <td>43</td>
      <td>773.0902</td>
      <td>0.0220</td>
      <td>37.3119</td>
      <td>1508.8684</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1670</td>
      <td>33</td>
      <td>51</td>
      <td>956.5215</td>
      <td>0.0010</td>
      <td>280.9676</td>
      <td>1632.0755</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1675</td>
      <td>33</td>
      <td>56</td>
      <td>848.8771</td>
      <td>0.0010</td>
      <td>211.4585</td>
      <td>1486.2957</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1678</td>
      <td>33</td>
      <td>59</td>
      <td>1191.5685</td>
      <td>0.0010</td>
      <td>558.9516</td>
      <td>1824.1854</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1680</td>
      <td>33</td>
      <td>60</td>
      <td>884.1731</td>
      <td>0.0010</td>
      <td>246.7545</td>
      <td>1521.5917</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1682</td>
      <td>33</td>
      <td>62</td>
      <td>922.7063</td>
      <td>0.0010</td>
      <td>277.3977</td>
      <td>1568.0149</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1683</td>
      <td>33</td>
      <td>63</td>
      <td>987.4119</td>
      <td>0.0025</td>
      <td>142.3736</td>
      <td>1832.4502</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1689</td>
      <td>33</td>
      <td>69</td>
      <td>730.5564</td>
      <td>0.0314</td>
      <td>20.9913</td>
      <td>1440.1214</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1699</td>
      <td>33</td>
      <td>8</td>
      <td>1004.9147</td>
      <td>0.0121</td>
      <td>78.8584</td>
      <td>1930.9710</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1700</td>
      <td>33</td>
      <td>9</td>
      <td>1711.8531</td>
      <td>0.0010</td>
      <td>357.8531</td>
      <td>3065.8532</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1704</td>
      <td>34</td>
      <td>38</td>
      <td>5948.3417</td>
      <td>0.0010</td>
      <td>5070.4103</td>
      <td>6826.2731</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1727</td>
      <td>34</td>
      <td>59</td>
      <td>944.1154</td>
      <td>0.0010</td>
      <td>174.1186</td>
      <td>1714.1121</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1749</td>
      <td>34</td>
      <td>9</td>
      <td>1464.4000</td>
      <td>0.0318</td>
      <td>41.0213</td>
      <td>2887.7787</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1752</td>
      <td>35</td>
      <td>38</td>
      <td>5875.1474</td>
      <td>0.0010</td>
      <td>5128.9321</td>
      <td>6621.3627</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1775</td>
      <td>35</td>
      <td>59</td>
      <td>870.9211</td>
      <td>0.0010</td>
      <td>255.3167</td>
      <td>1486.5255</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1797</td>
      <td>35</td>
      <td>9</td>
      <td>1391.2057</td>
      <td>0.0294</td>
      <td>45.0702</td>
      <td>2737.3412</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1799</td>
      <td>36</td>
      <td>38</td>
      <td>5780.2255</td>
      <td>0.0010</td>
      <td>5014.6771</td>
      <td>6545.7740</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1822</td>
      <td>36</td>
      <td>59</td>
      <td>775.9993</td>
      <td>0.0010</td>
      <td>137.0971</td>
      <td>1414.9014</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1845</td>
      <td>37</td>
      <td>38</td>
      <td>5741.4750</td>
      <td>0.0010</td>
      <td>4456.3150</td>
      <td>7026.6350</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1891</td>
      <td>38</td>
      <td>39</td>
      <td>-5876.5555</td>
      <td>0.0010</td>
      <td>-6653.5377</td>
      <td>-5099.5732</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1892</td>
      <td>38</td>
      <td>4</td>
      <td>-5778.1017</td>
      <td>0.0010</td>
      <td>-6630.5803</td>
      <td>-4925.6230</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1893</td>
      <td>38</td>
      <td>40</td>
      <td>-5814.9942</td>
      <td>0.0010</td>
      <td>-6541.9904</td>
      <td>-5087.9979</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1894</td>
      <td>38</td>
      <td>41</td>
      <td>-6090.0506</td>
      <td>0.0010</td>
      <td>-6801.7399</td>
      <td>-5378.3612</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1895</td>
      <td>38</td>
      <td>42</td>
      <td>-5975.8106</td>
      <td>0.0010</td>
      <td>-6752.7929</td>
      <td>-5198.8283</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1896</td>
      <td>38</td>
      <td>43</td>
      <td>-5422.7046</td>
      <td>0.0010</td>
      <td>-6212.6106</td>
      <td>-4632.7987</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1897</td>
      <td>38</td>
      <td>44</td>
      <td>-5859.1591</td>
      <td>0.0010</td>
      <td>-6680.7529</td>
      <td>-5037.5652</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1898</td>
      <td>38</td>
      <td>45</td>
      <td>-5910.7345</td>
      <td>0.0010</td>
      <td>-6857.6255</td>
      <td>-4963.8436</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1899</td>
      <td>38</td>
      <td>46</td>
      <td>-6021.7861</td>
      <td>0.0010</td>
      <td>-6811.6921</td>
      <td>-5231.8802</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1900</td>
      <td>38</td>
      <td>47</td>
      <td>-6041.7893</td>
      <td>0.0010</td>
      <td>-6883.1240</td>
      <td>-5200.4546</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1901</td>
      <td>38</td>
      <td>48</td>
      <td>-5992.2167</td>
      <td>0.0010</td>
      <td>-7277.3766</td>
      <td>-4707.0567</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1902</td>
      <td>38</td>
      <td>49</td>
      <td>-5796.9607</td>
      <td>0.0010</td>
      <td>-6638.2954</td>
      <td>-4955.6260</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1903</td>
      <td>38</td>
      <td>5</td>
      <td>-5669.2267</td>
      <td>0.0010</td>
      <td>-6728.9967</td>
      <td>-4609.4566</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1904</td>
      <td>38</td>
      <td>50</td>
      <td>-5898.3417</td>
      <td>0.0010</td>
      <td>-6958.1117</td>
      <td>-4838.5716</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1905</td>
      <td>38</td>
      <td>51</td>
      <td>-5239.2732</td>
      <td>0.0010</td>
      <td>-5973.4088</td>
      <td>-4505.1377</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1906</td>
      <td>38</td>
      <td>52</td>
      <td>-6145.9917</td>
      <td>0.0010</td>
      <td>-6929.2316</td>
      <td>-5362.7517</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1907</td>
      <td>38</td>
      <td>53</td>
      <td>-5643.3348</td>
      <td>0.0010</td>
      <td>-6420.3171</td>
      <td>-4866.3525</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1908</td>
      <td>38</td>
      <td>54</td>
      <td>-6107.0917</td>
      <td>0.0010</td>
      <td>-6849.0791</td>
      <td>-5365.1042</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1909</td>
      <td>38</td>
      <td>55</td>
      <td>-5658.0689</td>
      <td>0.0010</td>
      <td>-6413.4266</td>
      <td>-4902.7113</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1910</td>
      <td>38</td>
      <td>56</td>
      <td>-5346.9177</td>
      <td>0.0010</td>
      <td>-6046.1203</td>
      <td>-4647.7151</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1911</td>
      <td>38</td>
      <td>57</td>
      <td>-5909.8721</td>
      <td>0.0010</td>
      <td>-6731.4660</td>
      <td>-5088.2782</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1912</td>
      <td>38</td>
      <td>58</td>
      <td>-5879.0778</td>
      <td>0.0010</td>
      <td>-6757.0092</td>
      <td>-5001.1464</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1913</td>
      <td>38</td>
      <td>59</td>
      <td>-5004.2263</td>
      <td>0.0010</td>
      <td>-5699.0543</td>
      <td>-4309.3983</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1914</td>
      <td>38</td>
      <td>6</td>
      <td>-5637.2583</td>
      <td>0.0010</td>
      <td>-6632.7390</td>
      <td>-4641.7777</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1915</td>
      <td>38</td>
      <td>60</td>
      <td>-5311.6217</td>
      <td>0.0010</td>
      <td>-6010.8243</td>
      <td>-4612.4191</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1916</td>
      <td>38</td>
      <td>61</td>
      <td>-5683.3069</td>
      <td>0.0010</td>
      <td>-6504.9008</td>
      <td>-4861.7130</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1917</td>
      <td>38</td>
      <td>62</td>
      <td>-5273.0885</td>
      <td>0.0010</td>
      <td>-5979.4913</td>
      <td>-4566.6856</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1918</td>
      <td>38</td>
      <td>63</td>
      <td>-5208.3828</td>
      <td>0.0010</td>
      <td>-6100.9474</td>
      <td>-4315.8183</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1919</td>
      <td>38</td>
      <td>64</td>
      <td>-5604.9796</td>
      <td>0.0010</td>
      <td>-6381.9619</td>
      <td>-4827.9973</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1920</td>
      <td>38</td>
      <td>65</td>
      <td>-5832.4707</td>
      <td>0.0010</td>
      <td>-6598.0191</td>
      <td>-5066.9223</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1921</td>
      <td>38</td>
      <td>66</td>
      <td>-5809.4667</td>
      <td>0.0010</td>
      <td>-6958.9487</td>
      <td>-4659.9847</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1922</td>
      <td>38</td>
      <td>67</td>
      <td>-5993.1417</td>
      <td>0.0010</td>
      <td>-7052.9117</td>
      <td>-4933.3716</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1923</td>
      <td>38</td>
      <td>68</td>
      <td>-5995.9326</td>
      <td>0.0010</td>
      <td>-6751.2902</td>
      <td>-5240.5749</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1924</td>
      <td>38</td>
      <td>69</td>
      <td>-5465.2384</td>
      <td>0.0010</td>
      <td>-6230.7869</td>
      <td>-4699.6900</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1925</td>
      <td>38</td>
      <td>7</td>
      <td>-5474.7210</td>
      <td>0.0010</td>
      <td>-6251.7033</td>
      <td>-4697.7387</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1926</td>
      <td>38</td>
      <td>70</td>
      <td>-5955.1878</td>
      <td>0.0010</td>
      <td>-6685.6709</td>
      <td>-5224.7048</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1927</td>
      <td>38</td>
      <td>71</td>
      <td>-5752.2821</td>
      <td>0.0010</td>
      <td>-6472.7581</td>
      <td>-5031.8062</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1928</td>
      <td>38</td>
      <td>72</td>
      <td>-5610.1309</td>
      <td>0.0010</td>
      <td>-6348.0967</td>
      <td>-4872.1651</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1929</td>
      <td>38</td>
      <td>73</td>
      <td>-5949.3417</td>
      <td>0.0010</td>
      <td>-6896.2326</td>
      <td>-5002.4507</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1930</td>
      <td>38</td>
      <td>74</td>
      <td>-6051.9571</td>
      <td>0.0010</td>
      <td>-7021.5766</td>
      <td>-5082.3375</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1931</td>
      <td>38</td>
      <td>75</td>
      <td>-6077.7739</td>
      <td>0.0010</td>
      <td>-6789.4632</td>
      <td>-5366.0845</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1932</td>
      <td>38</td>
      <td>76</td>
      <td>-5850.0259</td>
      <td>0.0010</td>
      <td>-6584.1614</td>
      <td>-5115.8904</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1933</td>
      <td>38</td>
      <td>77</td>
      <td>-6012.1795</td>
      <td>0.0010</td>
      <td>-6750.1453</td>
      <td>-5274.2137</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1934</td>
      <td>38</td>
      <td>8</td>
      <td>-5190.8801</td>
      <td>0.0010</td>
      <td>-6160.4997</td>
      <td>-4221.2606</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1935</td>
      <td>38</td>
      <td>9</td>
      <td>-4483.9417</td>
      <td>0.0010</td>
      <td>-5868.1013</td>
      <td>-3099.7820</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1957</td>
      <td>39</td>
      <td>59</td>
      <td>872.3292</td>
      <td>0.0010</td>
      <td>219.7704</td>
      <td>1524.8880</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1979</td>
      <td>39</td>
      <td>9</td>
      <td>1392.6138</td>
      <td>0.0359</td>
      <td>29.1825</td>
      <td>2756.0451</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2000</td>
      <td>4</td>
      <td>59</td>
      <td>773.8754</td>
      <td>0.0244</td>
      <td>33.0303</td>
      <td>1514.7204</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2042</td>
      <td>40</td>
      <td>59</td>
      <td>810.7679</td>
      <td>0.0010</td>
      <td>218.6065</td>
      <td>1402.9292</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2075</td>
      <td>41</td>
      <td>51</td>
      <td>850.7773</td>
      <td>0.0010</td>
      <td>230.4530</td>
      <td>1471.1016</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2080</td>
      <td>41</td>
      <td>56</td>
      <td>743.1329</td>
      <td>0.0010</td>
      <td>164.5730</td>
      <td>1321.6928</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2083</td>
      <td>41</td>
      <td>59</td>
      <td>1085.8243</td>
      <td>0.0010</td>
      <td>512.5589</td>
      <td>1659.0897</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2085</td>
      <td>41</td>
      <td>60</td>
      <td>778.4289</td>
      <td>0.0010</td>
      <td>199.8690</td>
      <td>1356.9888</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2087</td>
      <td>41</td>
      <td>62</td>
      <td>816.9621</td>
      <td>0.0010</td>
      <td>229.7209</td>
      <td>1404.2033</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2088</td>
      <td>41</td>
      <td>63</td>
      <td>881.6677</td>
      <td>0.0093</td>
      <td>80.0950</td>
      <td>1683.2404</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2104</td>
      <td>41</td>
      <td>8</td>
      <td>899.1704</td>
      <td>0.0403</td>
      <td>12.5987</td>
      <td>1785.7421</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2105</td>
      <td>41</td>
      <td>9</td>
      <td>1606.1089</td>
      <td>0.0011</td>
      <td>278.8014</td>
      <td>2933.4164</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2115</td>
      <td>42</td>
      <td>51</td>
      <td>736.5374</td>
      <td>0.0186</td>
      <td>42.2738</td>
      <td>1430.8010</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2123</td>
      <td>42</td>
      <td>59</td>
      <td>971.5844</td>
      <td>0.0010</td>
      <td>319.0256</td>
      <td>1624.1431</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2125</td>
      <td>42</td>
      <td>60</td>
      <td>664.1890</td>
      <td>0.0426</td>
      <td>6.9741</td>
      <td>1321.4038</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2127</td>
      <td>42</td>
      <td>62</td>
      <td>702.7222</td>
      <td>0.0198</td>
      <td>37.8523</td>
      <td>1367.5921</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2145</td>
      <td>42</td>
      <td>9</td>
      <td>1491.8690</td>
      <td>0.0103</td>
      <td>128.4377</td>
      <td>2855.3003</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2200</td>
      <td>44</td>
      <td>59</td>
      <td>854.9328</td>
      <td>0.0010</td>
      <td>149.8456</td>
      <td>1560.0200</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2237</td>
      <td>45</td>
      <td>59</td>
      <td>906.5082</td>
      <td>0.0160</td>
      <td>58.7265</td>
      <td>1754.2900</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2265</td>
      <td>46</td>
      <td>51</td>
      <td>782.5129</td>
      <td>0.0086</td>
      <td>73.8155</td>
      <td>1491.2102</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2270</td>
      <td>46</td>
      <td>56</td>
      <td>674.8684</td>
      <td>0.0474</td>
      <td>2.4242</td>
      <td>1347.3127</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2273</td>
      <td>46</td>
      <td>59</td>
      <td>1017.5598</td>
      <td>0.0010</td>
      <td>349.6654</td>
      <td>1685.4542</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2275</td>
      <td>46</td>
      <td>60</td>
      <td>710.1644</td>
      <td>0.0201</td>
      <td>37.7202</td>
      <td>1382.6087</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2277</td>
      <td>46</td>
      <td>62</td>
      <td>748.6976</td>
      <td>0.0090</td>
      <td>68.7698</td>
      <td>1428.6255</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2295</td>
      <td>46</td>
      <td>9</td>
      <td>1537.8444</td>
      <td>0.0062</td>
      <td>167.0072</td>
      <td>2908.6817</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2300</td>
      <td>47</td>
      <td>51</td>
      <td>802.5160</td>
      <td>0.0230</td>
      <td>36.9153</td>
      <td>1568.1168</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2308</td>
      <td>47</td>
      <td>59</td>
      <td>1037.5630</td>
      <td>0.0010</td>
      <td>309.5688</td>
      <td>1765.5572</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2312</td>
      <td>47</td>
      <td>62</td>
      <td>768.7008</td>
      <td>0.0263</td>
      <td>29.6510</td>
      <td>1507.7506</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2330</td>
      <td>47</td>
      <td>9</td>
      <td>1557.8476</td>
      <td>0.0074</td>
      <td>156.7454</td>
      <td>2958.9499</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2375</td>
      <td>49</td>
      <td>59</td>
      <td>792.7344</td>
      <td>0.0113</td>
      <td>64.7402</td>
      <td>1520.7286</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2461</td>
      <td>51</td>
      <td>52</td>
      <td>-906.7184</td>
      <td>0.0010</td>
      <td>-1607.9782</td>
      <td>-205.4586</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2463</td>
      <td>51</td>
      <td>54</td>
      <td>-867.8184</td>
      <td>0.0010</td>
      <td>-1522.6817</td>
      <td>-212.9552</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2478</td>
      <td>51</td>
      <td>68</td>
      <td>-756.6593</td>
      <td>0.0053</td>
      <td>-1426.6337</td>
      <td>-86.6849</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2481</td>
      <td>51</td>
      <td>70</td>
      <td>-715.9146</td>
      <td>0.0069</td>
      <td>-1357.7136</td>
      <td>-74.1155</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2486</td>
      <td>51</td>
      <td>75</td>
      <td>-838.5006</td>
      <td>0.0010</td>
      <td>-1458.8249</td>
      <td>-218.1763</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2488</td>
      <td>51</td>
      <td>77</td>
      <td>-772.9063</td>
      <td>0.0017</td>
      <td>-1423.2093</td>
      <td>-122.6032</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2494</td>
      <td>52</td>
      <td>56</td>
      <td>799.0740</td>
      <td>0.0013</td>
      <td>134.4729</td>
      <td>1463.6751</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2497</td>
      <td>52</td>
      <td>59</td>
      <td>1141.7654</td>
      <td>0.0010</td>
      <td>481.7682</td>
      <td>1801.7626</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2499</td>
      <td>52</td>
      <td>60</td>
      <td>834.3700</td>
      <td>0.0010</td>
      <td>169.7689</td>
      <td>1498.9711</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2501</td>
      <td>52</td>
      <td>62</td>
      <td>872.9032</td>
      <td>0.0010</td>
      <td>200.7311</td>
      <td>1545.0753</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2502</td>
      <td>52</td>
      <td>63</td>
      <td>937.6088</td>
      <td>0.0126</td>
      <td>71.8826</td>
      <td>1803.3351</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2518</td>
      <td>52</td>
      <td>8</td>
      <td>955.1115</td>
      <td>0.0425</td>
      <td>10.1393</td>
      <td>1900.0838</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2519</td>
      <td>52</td>
      <td>9</td>
      <td>1662.0500</td>
      <td>0.0010</td>
      <td>295.0429</td>
      <td>3029.0571</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2549</td>
      <td>54</td>
      <td>56</td>
      <td>760.1740</td>
      <td>0.0010</td>
      <td>144.7268</td>
      <td>1375.6212</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2552</td>
      <td>54</td>
      <td>59</td>
      <td>1102.8654</td>
      <td>0.0010</td>
      <td>492.3927</td>
      <td>1713.3380</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2554</td>
      <td>54</td>
      <td>60</td>
      <td>795.4700</td>
      <td>0.0010</td>
      <td>180.0228</td>
      <td>1410.9172</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2556</td>
      <td>54</td>
      <td>62</td>
      <td>834.0032</td>
      <td>0.0010</td>
      <td>210.3880</td>
      <td>1457.6184</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2557</td>
      <td>54</td>
      <td>63</td>
      <td>898.7088</td>
      <td>0.0122</td>
      <td>70.1182</td>
      <td>1727.2995</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2573</td>
      <td>54</td>
      <td>8</td>
      <td>916.2115</td>
      <td>0.0460</td>
      <td>5.1391</td>
      <td>1827.2840</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2574</td>
      <td>54</td>
      <td>9</td>
      <td>1623.1500</td>
      <td>0.0011</td>
      <td>279.3536</td>
      <td>2966.9464</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2578</td>
      <td>55</td>
      <td>59</td>
      <td>653.8427</td>
      <td>0.0249</td>
      <td>27.1875</td>
      <td>1280.4978</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2613</td>
      <td>56</td>
      <td>68</td>
      <td>-649.0149</td>
      <td>0.0323</td>
      <td>-1280.5171</td>
      <td>-17.5127</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2616</td>
      <td>56</td>
      <td>70</td>
      <td>-608.2702</td>
      <td>0.0422</td>
      <td>-1209.7977</td>
      <td>-6.7426</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2621</td>
      <td>56</td>
      <td>75</td>
      <td>-730.8562</td>
      <td>0.0010</td>
      <td>-1309.4161</td>
      <td>-152.2963</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2623</td>
      <td>56</td>
      <td>77</td>
      <td>-665.2618</td>
      <td>0.0112</td>
      <td>-1275.8545</td>
      <td>-54.6692</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2627</td>
      <td>57</td>
      <td>59</td>
      <td>905.6458</td>
      <td>0.0010</td>
      <td>200.5586</td>
      <td>1610.7330</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2649</td>
      <td>57</td>
      <td>9</td>
      <td>1425.9304</td>
      <td>0.0331</td>
      <td>36.5925</td>
      <td>2815.2684</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2650</td>
      <td>58</td>
      <td>59</td>
      <td>874.8515</td>
      <td>0.0047</td>
      <td>104.8547</td>
      <td>1644.8483</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2679</td>
      <td>59</td>
      <td>65</td>
      <td>-828.2444</td>
      <td>0.0010</td>
      <td>-1467.1465</td>
      <td>-189.3423</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2681</td>
      <td>59</td>
      <td>67</td>
      <td>-988.9154</td>
      <td>0.0384</td>
      <td>-1961.1520</td>
      <td>-16.6788</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2682</td>
      <td>59</td>
      <td>68</td>
      <td>-991.7063</td>
      <td>0.0010</td>
      <td>-1618.3615</td>
      <td>-365.0511</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2685</td>
      <td>59</td>
      <td>70</td>
      <td>-950.9615</td>
      <td>0.0010</td>
      <td>-1547.3985</td>
      <td>-354.5246</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2686</td>
      <td>59</td>
      <td>71</td>
      <td>-748.0559</td>
      <td>0.0010</td>
      <td>-1332.1938</td>
      <td>-163.9179</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2687</td>
      <td>59</td>
      <td>72</td>
      <td>-605.9046</td>
      <td>0.0496</td>
      <td>-1211.4828</td>
      <td>-0.3263</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2688</td>
      <td>59</td>
      <td>73</td>
      <td>-945.1154</td>
      <td>0.0070</td>
      <td>-1792.8972</td>
      <td>-97.3336</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2689</td>
      <td>59</td>
      <td>74</td>
      <td>-1047.7308</td>
      <td>0.0013</td>
      <td>-1920.8250</td>
      <td>-174.6365</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2690</td>
      <td>59</td>
      <td>75</td>
      <td>-1073.5476</td>
      <td>0.0010</td>
      <td>-1646.8130</td>
      <td>-500.2822</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2691</td>
      <td>59</td>
      <td>76</td>
      <td>-845.7996</td>
      <td>0.0010</td>
      <td>-1446.7043</td>
      <td>-244.8949</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2692</td>
      <td>59</td>
      <td>77</td>
      <td>-1007.9532</td>
      <td>0.0010</td>
      <td>-1613.5315</td>
      <td>-402.3750</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2723</td>
      <td>60</td>
      <td>68</td>
      <td>-684.3109</td>
      <td>0.0124</td>
      <td>-1315.8131</td>
      <td>-52.8087</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2726</td>
      <td>60</td>
      <td>70</td>
      <td>-643.5662</td>
      <td>0.0159</td>
      <td>-1245.0937</td>
      <td>-42.0386</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2731</td>
      <td>60</td>
      <td>75</td>
      <td>-766.1522</td>
      <td>0.0010</td>
      <td>-1344.7121</td>
      <td>-187.5923</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2733</td>
      <td>60</td>
      <td>77</td>
      <td>-700.5578</td>
      <td>0.0038</td>
      <td>-1311.1505</td>
      <td>-89.9652</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2760</td>
      <td>62</td>
      <td>68</td>
      <td>-722.8441</td>
      <td>0.0052</td>
      <td>-1362.3093</td>
      <td>-83.3789</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2763</td>
      <td>62</td>
      <td>70</td>
      <td>-682.0993</td>
      <td>0.0066</td>
      <td>-1291.9813</td>
      <td>-72.2174</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2768</td>
      <td>62</td>
      <td>75</td>
      <td>-804.6854</td>
      <td>0.0010</td>
      <td>-1391.9266</td>
      <td>-217.4442</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2770</td>
      <td>62</td>
      <td>77</td>
      <td>-739.0910</td>
      <td>0.0015</td>
      <td>-1357.9158</td>
      <td>-120.2663</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2785</td>
      <td>63</td>
      <td>75</td>
      <td>-869.3910</td>
      <td>0.0122</td>
      <td>-1670.9638</td>
      <td>-67.8183</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2859</td>
      <td>68</td>
      <td>9</td>
      <td>1511.9909</td>
      <td>0.0065</td>
      <td>160.7660</td>
      <td>2863.2158</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2889</td>
      <td>70</td>
      <td>9</td>
      <td>1471.2462</td>
      <td>0.0092</td>
      <td>133.7676</td>
      <td>2808.7247</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2915</td>
      <td>74</td>
      <td>9</td>
      <td>1568.0154</td>
      <td>0.0194</td>
      <td>86.3253</td>
      <td>3049.7055</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2918</td>
      <td>75</td>
      <td>8</td>
      <td>886.8938</td>
      <td>0.0497</td>
      <td>0.3221</td>
      <td>1773.4655</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2919</td>
      <td>75</td>
      <td>9</td>
      <td>1593.8322</td>
      <td>0.0013</td>
      <td>266.5247</td>
      <td>2921.1397</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2922</td>
      <td>76</td>
      <td>9</td>
      <td>1366.0842</td>
      <td>0.0368</td>
      <td>26.6073</td>
      <td>2705.5611</td>
      <td>True</td>
    </tr>
    <tr>
      <td>2924</td>
      <td>77</td>
      <td>9</td>
      <td>1528.2378</td>
      <td>0.0044</td>
      <td>186.6578</td>
      <td>2869.8179</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



### This Tukey's Test shows that there is a large number of products that have statistical signficnance when compared against each other when speaking in terms of revenue.


```python
means = df_rev_tukey.groupby('group').mean().sort_values(by='data', ascending=False)
```


```python
with plt.style.context('seaborn-poster'):
    
    fig, ax = plt.subplots(figsize=(24,12))
    sns.barplot(data=df_rev_tukey, x='group', y='data', ci=68, ax=ax, order=list(means.index))
    ax.grid()
    ax.set_xticklabels(ax.get_xticklabels(), fontsize=12, fontweight='bold')
    ax.set(xlabel='Product', ylabel='Revenue')
```


![png](output_79_0.png)


### Recommendation: From the Tukey's Test, it is very clear that there is one product that is far outperforming all others - product 38. Therefore, my recommendation would be to promote and market product 38 as much as possible to further increase sales, and thus increase revenue.

# HYPOTHESIS 4

- $H_0$: Shipping Region will not have a statistically signficant effect on Product Revenue.
- $H_1$: Shipping Region will have a statistically significant effect on Product Revenue.

## Query Data


```python
cur.execute("""SELECT *
            FROM OrderDetail""")
cur.description
df_order_detail = pd.DataFrame(cur.fetchall(), columns = [x[0] for x in cur.description])
df_order_detail
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
      <th>Id</th>
      <th>OrderId</th>
      <th>ProductId</th>
      <th>UnitPrice</th>
      <th>Quantity</th>
      <th>Discount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>10248/11</td>
      <td>10248</td>
      <td>11</td>
      <td>14.00</td>
      <td>12</td>
      <td>0.00</td>
    </tr>
    <tr>
      <td>1</td>
      <td>10248/42</td>
      <td>10248</td>
      <td>42</td>
      <td>9.80</td>
      <td>10</td>
      <td>0.00</td>
    </tr>
    <tr>
      <td>2</td>
      <td>10248/72</td>
      <td>10248</td>
      <td>72</td>
      <td>34.80</td>
      <td>5</td>
      <td>0.00</td>
    </tr>
    <tr>
      <td>3</td>
      <td>10249/14</td>
      <td>10249</td>
      <td>14</td>
      <td>18.60</td>
      <td>9</td>
      <td>0.00</td>
    </tr>
    <tr>
      <td>4</td>
      <td>10249/51</td>
      <td>10249</td>
      <td>51</td>
      <td>42.40</td>
      <td>40</td>
      <td>0.00</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>2150</td>
      <td>11077/64</td>
      <td>11077</td>
      <td>64</td>
      <td>33.25</td>
      <td>2</td>
      <td>0.03</td>
    </tr>
    <tr>
      <td>2151</td>
      <td>11077/66</td>
      <td>11077</td>
      <td>66</td>
      <td>17.00</td>
      <td>1</td>
      <td>0.00</td>
    </tr>
    <tr>
      <td>2152</td>
      <td>11077/73</td>
      <td>11077</td>
      <td>73</td>
      <td>15.00</td>
      <td>2</td>
      <td>0.01</td>
    </tr>
    <tr>
      <td>2153</td>
      <td>11077/75</td>
      <td>11077</td>
      <td>75</td>
      <td>7.75</td>
      <td>4</td>
      <td>0.00</td>
    </tr>
    <tr>
      <td>2154</td>
      <td>11077/77</td>
      <td>11077</td>
      <td>77</td>
      <td>13.00</td>
      <td>2</td>
      <td>0.00</td>
    </tr>
  </tbody>
</table>
<p>2155 rows × 6 columns</p>
</div>




```python
cur.execute("""SELECT *
            FROM 'Order'""")
cur.description
df_order = pd.DataFrame(cur.fetchall(), columns = [x[0] for x in cur.description])
df_order
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
      <th>Id</th>
      <th>CustomerId</th>
      <th>EmployeeId</th>
      <th>OrderDate</th>
      <th>RequiredDate</th>
      <th>ShippedDate</th>
      <th>ShipVia</th>
      <th>Freight</th>
      <th>ShipName</th>
      <th>ShipAddress</th>
      <th>ShipCity</th>
      <th>ShipRegion</th>
      <th>ShipPostalCode</th>
      <th>ShipCountry</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>10248</td>
      <td>VINET</td>
      <td>5</td>
      <td>2012-07-04</td>
      <td>2012-08-01</td>
      <td>2012-07-16</td>
      <td>3</td>
      <td>32.38</td>
      <td>Vins et alcools Chevalier</td>
      <td>59 rue de l'Abbaye</td>
      <td>Reims</td>
      <td>Western Europe</td>
      <td>51100</td>
      <td>France</td>
    </tr>
    <tr>
      <td>1</td>
      <td>10249</td>
      <td>TOMSP</td>
      <td>6</td>
      <td>2012-07-05</td>
      <td>2012-08-16</td>
      <td>2012-07-10</td>
      <td>1</td>
      <td>11.61</td>
      <td>Toms Spezialitäten</td>
      <td>Luisenstr. 48</td>
      <td>Münster</td>
      <td>Western Europe</td>
      <td>44087</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>2</td>
      <td>10250</td>
      <td>HANAR</td>
      <td>4</td>
      <td>2012-07-08</td>
      <td>2012-08-05</td>
      <td>2012-07-12</td>
      <td>2</td>
      <td>65.83</td>
      <td>Hanari Carnes</td>
      <td>Rua do Paço, 67</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>05454-876</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>3</td>
      <td>10251</td>
      <td>VICTE</td>
      <td>3</td>
      <td>2012-07-08</td>
      <td>2012-08-05</td>
      <td>2012-07-15</td>
      <td>1</td>
      <td>41.34</td>
      <td>Victuailles en stock</td>
      <td>2, rue du Commerce</td>
      <td>Lyon</td>
      <td>Western Europe</td>
      <td>69004</td>
      <td>France</td>
    </tr>
    <tr>
      <td>4</td>
      <td>10252</td>
      <td>SUPRD</td>
      <td>4</td>
      <td>2012-07-09</td>
      <td>2012-08-06</td>
      <td>2012-07-11</td>
      <td>2</td>
      <td>51.30</td>
      <td>Suprêmes délices</td>
      <td>Boulevard Tirou, 255</td>
      <td>Charleroi</td>
      <td>Western Europe</td>
      <td>B-6000</td>
      <td>Belgium</td>
    </tr>
    <tr>
      <td>5</td>
      <td>10253</td>
      <td>HANAR</td>
      <td>3</td>
      <td>2012-07-10</td>
      <td>2012-07-24</td>
      <td>2012-07-16</td>
      <td>2</td>
      <td>58.17</td>
      <td>Hanari Carnes</td>
      <td>Rua do Paço, 67</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>05454-876</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>6</td>
      <td>10254</td>
      <td>CHOPS</td>
      <td>5</td>
      <td>2012-07-11</td>
      <td>2012-08-08</td>
      <td>2012-07-23</td>
      <td>2</td>
      <td>22.98</td>
      <td>Chop-suey Chinese</td>
      <td>Hauptstr. 31</td>
      <td>Bern</td>
      <td>Western Europe</td>
      <td>3012</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <td>7</td>
      <td>10255</td>
      <td>RICSU</td>
      <td>9</td>
      <td>2012-07-12</td>
      <td>2012-08-09</td>
      <td>2012-07-15</td>
      <td>3</td>
      <td>148.33</td>
      <td>Richter Supermarkt</td>
      <td>Starenweg 5</td>
      <td>Genève</td>
      <td>Western Europe</td>
      <td>1204</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <td>8</td>
      <td>10256</td>
      <td>WELLI</td>
      <td>3</td>
      <td>2012-07-15</td>
      <td>2012-08-12</td>
      <td>2012-07-17</td>
      <td>2</td>
      <td>13.97</td>
      <td>Wellington Importadora</td>
      <td>Rua do Mercado, 12</td>
      <td>Resende</td>
      <td>South America</td>
      <td>08737-363</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>9</td>
      <td>10257</td>
      <td>HILAA</td>
      <td>4</td>
      <td>2012-07-16</td>
      <td>2012-08-13</td>
      <td>2012-07-22</td>
      <td>3</td>
      <td>81.91</td>
      <td>HILARION-Abastos</td>
      <td>Carrera 22 con Ave. Carlos Soublette #8-35</td>
      <td>San Cristóbal</td>
      <td>South America</td>
      <td>5022</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>10</td>
      <td>10258</td>
      <td>ERNSH</td>
      <td>1</td>
      <td>2012-07-17</td>
      <td>2012-08-14</td>
      <td>2012-07-23</td>
      <td>1</td>
      <td>140.51</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>11</td>
      <td>10259</td>
      <td>CENTC</td>
      <td>4</td>
      <td>2012-07-18</td>
      <td>2012-08-15</td>
      <td>2012-07-25</td>
      <td>3</td>
      <td>3.25</td>
      <td>Centro comercial Moctezuma</td>
      <td>Sierras de Granada 9993</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05022</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>12</td>
      <td>10260</td>
      <td>OTTIK</td>
      <td>4</td>
      <td>2012-07-19</td>
      <td>2012-08-16</td>
      <td>2012-07-29</td>
      <td>1</td>
      <td>55.09</td>
      <td>Ottilies Käseladen</td>
      <td>Mehrheimerstr. 369</td>
      <td>Köln</td>
      <td>Western Europe</td>
      <td>50739</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>13</td>
      <td>10261</td>
      <td>QUEDE</td>
      <td>4</td>
      <td>2012-07-19</td>
      <td>2012-08-16</td>
      <td>2012-07-30</td>
      <td>2</td>
      <td>3.05</td>
      <td>Que Delícia</td>
      <td>Rua da Panificadora, 12</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>02389-673</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>14</td>
      <td>10262</td>
      <td>RATTC</td>
      <td>8</td>
      <td>2012-07-22</td>
      <td>2012-08-19</td>
      <td>2012-07-25</td>
      <td>3</td>
      <td>48.29</td>
      <td>Rattlesnake Canyon Grocery</td>
      <td>2817 Milton Dr.</td>
      <td>Albuquerque</td>
      <td>North America</td>
      <td>87110</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>15</td>
      <td>10263</td>
      <td>ERNSH</td>
      <td>9</td>
      <td>2012-07-23</td>
      <td>2012-08-20</td>
      <td>2012-07-31</td>
      <td>3</td>
      <td>146.06</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>16</td>
      <td>10264</td>
      <td>FOLKO</td>
      <td>6</td>
      <td>2012-07-24</td>
      <td>2012-08-21</td>
      <td>2012-08-23</td>
      <td>3</td>
      <td>3.67</td>
      <td>Folk och fä HB</td>
      <td>Åkergatan 24</td>
      <td>Bräcke</td>
      <td>Northern Europe</td>
      <td>S-844 67</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>17</td>
      <td>10265</td>
      <td>BLONP</td>
      <td>2</td>
      <td>2012-07-25</td>
      <td>2012-08-22</td>
      <td>2012-08-12</td>
      <td>1</td>
      <td>55.28</td>
      <td>Blondel père et fils</td>
      <td>24, place Kléber</td>
      <td>Strasbourg</td>
      <td>Western Europe</td>
      <td>67000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>18</td>
      <td>10266</td>
      <td>WARTH</td>
      <td>3</td>
      <td>2012-07-26</td>
      <td>2012-09-06</td>
      <td>2012-07-31</td>
      <td>3</td>
      <td>25.73</td>
      <td>Wartian Herkku</td>
      <td>Torikatu 38</td>
      <td>Oulu</td>
      <td>Scandinavia</td>
      <td>90110</td>
      <td>Finland</td>
    </tr>
    <tr>
      <td>19</td>
      <td>10267</td>
      <td>FRANK</td>
      <td>4</td>
      <td>2012-07-29</td>
      <td>2012-08-26</td>
      <td>2012-08-06</td>
      <td>1</td>
      <td>208.58</td>
      <td>Frankenversand</td>
      <td>Berliner Platz 43</td>
      <td>München</td>
      <td>Western Europe</td>
      <td>80805</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>20</td>
      <td>10268</td>
      <td>GROSR</td>
      <td>8</td>
      <td>2012-07-30</td>
      <td>2012-08-27</td>
      <td>2012-08-02</td>
      <td>3</td>
      <td>66.29</td>
      <td>GROSELLA-Restaurante</td>
      <td>5ª Ave. Los Palos Grandes</td>
      <td>Caracas</td>
      <td>South America</td>
      <td>1081</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>21</td>
      <td>10269</td>
      <td>WHITC</td>
      <td>5</td>
      <td>2012-07-31</td>
      <td>2012-08-14</td>
      <td>2012-08-09</td>
      <td>1</td>
      <td>4.56</td>
      <td>White Clover Markets</td>
      <td>1029 - 12th Ave. S.</td>
      <td>Seattle</td>
      <td>North America</td>
      <td>98124</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>22</td>
      <td>10270</td>
      <td>WARTH</td>
      <td>1</td>
      <td>2012-08-01</td>
      <td>2012-08-29</td>
      <td>2012-08-02</td>
      <td>1</td>
      <td>136.54</td>
      <td>Wartian Herkku</td>
      <td>Torikatu 38</td>
      <td>Oulu</td>
      <td>Scandinavia</td>
      <td>90110</td>
      <td>Finland</td>
    </tr>
    <tr>
      <td>23</td>
      <td>10271</td>
      <td>SPLIR</td>
      <td>6</td>
      <td>2012-08-01</td>
      <td>2012-08-29</td>
      <td>2012-08-30</td>
      <td>2</td>
      <td>4.54</td>
      <td>Split Rail Beer &amp; Ale</td>
      <td>P.O. Box 555</td>
      <td>Lander</td>
      <td>North America</td>
      <td>82520</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>24</td>
      <td>10272</td>
      <td>RATTC</td>
      <td>6</td>
      <td>2012-08-02</td>
      <td>2012-08-30</td>
      <td>2012-08-06</td>
      <td>2</td>
      <td>98.03</td>
      <td>Rattlesnake Canyon Grocery</td>
      <td>2817 Milton Dr.</td>
      <td>Albuquerque</td>
      <td>North America</td>
      <td>87110</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>25</td>
      <td>10273</td>
      <td>QUICK</td>
      <td>3</td>
      <td>2012-08-05</td>
      <td>2012-09-02</td>
      <td>2012-08-12</td>
      <td>3</td>
      <td>76.07</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>26</td>
      <td>10274</td>
      <td>VINET</td>
      <td>6</td>
      <td>2012-08-06</td>
      <td>2012-09-03</td>
      <td>2012-08-16</td>
      <td>1</td>
      <td>6.01</td>
      <td>Vins et alcools Chevalier</td>
      <td>59 rue de l'Abbaye</td>
      <td>Reims</td>
      <td>Western Europe</td>
      <td>51100</td>
      <td>France</td>
    </tr>
    <tr>
      <td>27</td>
      <td>10275</td>
      <td>MAGAA</td>
      <td>1</td>
      <td>2012-08-07</td>
      <td>2012-09-04</td>
      <td>2012-08-09</td>
      <td>1</td>
      <td>26.93</td>
      <td>Magazzini Alimentari Riuniti</td>
      <td>Via Ludovico il Moro 22</td>
      <td>Bergamo</td>
      <td>Southern Europe</td>
      <td>24100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>28</td>
      <td>10276</td>
      <td>TORTU</td>
      <td>8</td>
      <td>2012-08-08</td>
      <td>2012-08-22</td>
      <td>2012-08-14</td>
      <td>3</td>
      <td>13.84</td>
      <td>Tortuga Restaurante</td>
      <td>Avda. Azteca 123</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05033</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>29</td>
      <td>10277</td>
      <td>MORGK</td>
      <td>2</td>
      <td>2012-08-09</td>
      <td>2012-09-06</td>
      <td>2012-08-13</td>
      <td>3</td>
      <td>125.77</td>
      <td>Morgenstern Gesundkost</td>
      <td>Heerstr. 22</td>
      <td>Leipzig</td>
      <td>Western Europe</td>
      <td>04179</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>30</td>
      <td>10278</td>
      <td>BERGS</td>
      <td>8</td>
      <td>2012-08-12</td>
      <td>2012-09-09</td>
      <td>2012-08-16</td>
      <td>2</td>
      <td>92.69</td>
      <td>Berglunds snabbköp</td>
      <td>Berguvsvägen  8</td>
      <td>Luleå</td>
      <td>Northern Europe</td>
      <td>S-958 22</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>31</td>
      <td>10279</td>
      <td>LEHMS</td>
      <td>8</td>
      <td>2012-08-13</td>
      <td>2012-09-10</td>
      <td>2012-08-16</td>
      <td>2</td>
      <td>25.83</td>
      <td>Lehmanns Marktstand</td>
      <td>Magazinweg 7</td>
      <td>Frankfurt a.M.</td>
      <td>Western Europe</td>
      <td>60528</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>32</td>
      <td>10280</td>
      <td>BERGS</td>
      <td>2</td>
      <td>2012-08-14</td>
      <td>2012-09-11</td>
      <td>2012-09-12</td>
      <td>1</td>
      <td>8.98</td>
      <td>Berglunds snabbköp</td>
      <td>Berguvsvägen  8</td>
      <td>Luleå</td>
      <td>Northern Europe</td>
      <td>S-958 22</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>33</td>
      <td>10281</td>
      <td>ROMEY</td>
      <td>4</td>
      <td>2012-08-14</td>
      <td>2012-08-28</td>
      <td>2012-08-21</td>
      <td>1</td>
      <td>2.94</td>
      <td>Romero y tomillo</td>
      <td>Gran Vía, 1</td>
      <td>Madrid</td>
      <td>Southern Europe</td>
      <td>28001</td>
      <td>Spain</td>
    </tr>
    <tr>
      <td>34</td>
      <td>10282</td>
      <td>ROMEY</td>
      <td>4</td>
      <td>2012-08-15</td>
      <td>2012-09-12</td>
      <td>2012-08-21</td>
      <td>1</td>
      <td>12.69</td>
      <td>Romero y tomillo</td>
      <td>Gran Vía, 1</td>
      <td>Madrid</td>
      <td>Southern Europe</td>
      <td>28001</td>
      <td>Spain</td>
    </tr>
    <tr>
      <td>35</td>
      <td>10283</td>
      <td>LILAS</td>
      <td>3</td>
      <td>2012-08-16</td>
      <td>2012-09-13</td>
      <td>2012-08-23</td>
      <td>3</td>
      <td>84.81</td>
      <td>LILA-Supermercado</td>
      <td>Carrera 52 con Ave. Bolívar #65-98 Llano Largo</td>
      <td>Barquisimeto</td>
      <td>South America</td>
      <td>3508</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>36</td>
      <td>10284</td>
      <td>LEHMS</td>
      <td>4</td>
      <td>2012-08-19</td>
      <td>2012-09-16</td>
      <td>2012-08-27</td>
      <td>1</td>
      <td>76.56</td>
      <td>Lehmanns Marktstand</td>
      <td>Magazinweg 7</td>
      <td>Frankfurt a.M.</td>
      <td>Western Europe</td>
      <td>60528</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>37</td>
      <td>10285</td>
      <td>QUICK</td>
      <td>1</td>
      <td>2012-08-20</td>
      <td>2012-09-17</td>
      <td>2012-08-26</td>
      <td>2</td>
      <td>76.83</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>38</td>
      <td>10286</td>
      <td>QUICK</td>
      <td>8</td>
      <td>2012-08-21</td>
      <td>2012-09-18</td>
      <td>2012-08-30</td>
      <td>3</td>
      <td>229.24</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>39</td>
      <td>10287</td>
      <td>RICAR</td>
      <td>8</td>
      <td>2012-08-22</td>
      <td>2012-09-19</td>
      <td>2012-08-28</td>
      <td>3</td>
      <td>12.76</td>
      <td>Ricardo Adocicados</td>
      <td>Av. Copacabana, 267</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>02389-890</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>40</td>
      <td>10288</td>
      <td>REGGC</td>
      <td>4</td>
      <td>2012-08-23</td>
      <td>2012-09-20</td>
      <td>2012-09-03</td>
      <td>1</td>
      <td>7.45</td>
      <td>Reggiani Caseifici</td>
      <td>Strada Provinciale 124</td>
      <td>Reggio Emilia</td>
      <td>Southern Europe</td>
      <td>42100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>41</td>
      <td>10289</td>
      <td>BSBEV</td>
      <td>7</td>
      <td>2012-08-26</td>
      <td>2012-09-23</td>
      <td>2012-08-28</td>
      <td>3</td>
      <td>22.77</td>
      <td>B's Beverages</td>
      <td>Fauntleroy Circus</td>
      <td>London</td>
      <td>British Isles</td>
      <td>EC2 5NT</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>42</td>
      <td>10290</td>
      <td>COMMI</td>
      <td>8</td>
      <td>2012-08-27</td>
      <td>2012-09-24</td>
      <td>2012-09-03</td>
      <td>1</td>
      <td>79.70</td>
      <td>Comércio Mineiro</td>
      <td>Av. dos Lusíadas, 23</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05432-043</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>43</td>
      <td>10291</td>
      <td>QUEDE</td>
      <td>6</td>
      <td>2012-08-27</td>
      <td>2012-09-24</td>
      <td>2012-09-04</td>
      <td>2</td>
      <td>6.40</td>
      <td>Que Delícia</td>
      <td>Rua da Panificadora, 12</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>02389-673</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>44</td>
      <td>10292</td>
      <td>TRADH</td>
      <td>1</td>
      <td>2012-08-28</td>
      <td>2012-09-25</td>
      <td>2012-09-02</td>
      <td>2</td>
      <td>1.35</td>
      <td>Tradiçao Hipermercados</td>
      <td>Av. Inês de Castro, 414</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05634-030</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>45</td>
      <td>10293</td>
      <td>TORTU</td>
      <td>1</td>
      <td>2012-08-29</td>
      <td>2012-09-26</td>
      <td>2012-09-11</td>
      <td>3</td>
      <td>21.18</td>
      <td>Tortuga Restaurante</td>
      <td>Avda. Azteca 123</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05033</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>46</td>
      <td>10294</td>
      <td>RATTC</td>
      <td>4</td>
      <td>2012-08-30</td>
      <td>2012-09-27</td>
      <td>2012-09-05</td>
      <td>2</td>
      <td>147.26</td>
      <td>Rattlesnake Canyon Grocery</td>
      <td>2817 Milton Dr.</td>
      <td>Albuquerque</td>
      <td>North America</td>
      <td>87110</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>47</td>
      <td>10295</td>
      <td>VINET</td>
      <td>2</td>
      <td>2012-09-02</td>
      <td>2012-09-30</td>
      <td>2012-09-10</td>
      <td>2</td>
      <td>1.15</td>
      <td>Vins et alcools Chevalier</td>
      <td>59 rue de l'Abbaye</td>
      <td>Reims</td>
      <td>Western Europe</td>
      <td>51100</td>
      <td>France</td>
    </tr>
    <tr>
      <td>48</td>
      <td>10296</td>
      <td>LILAS</td>
      <td>6</td>
      <td>2012-09-03</td>
      <td>2012-10-01</td>
      <td>2012-09-11</td>
      <td>1</td>
      <td>0.12</td>
      <td>LILA-Supermercado</td>
      <td>Carrera 52 con Ave. Bolívar #65-98 Llano Largo</td>
      <td>Barquisimeto</td>
      <td>South America</td>
      <td>3508</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>49</td>
      <td>10297</td>
      <td>BLONP</td>
      <td>5</td>
      <td>2012-09-04</td>
      <td>2012-10-16</td>
      <td>2012-09-10</td>
      <td>2</td>
      <td>5.74</td>
      <td>Blondel père et fils</td>
      <td>24, place Kléber</td>
      <td>Strasbourg</td>
      <td>Western Europe</td>
      <td>67000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>50</td>
      <td>10298</td>
      <td>HUNGO</td>
      <td>6</td>
      <td>2012-09-05</td>
      <td>2012-10-03</td>
      <td>2012-09-11</td>
      <td>2</td>
      <td>168.22</td>
      <td>Hungry Owl All-Night Grocers</td>
      <td>8 Johnstown Road</td>
      <td>Cork</td>
      <td>British Isles</td>
      <td>None</td>
      <td>Ireland</td>
    </tr>
    <tr>
      <td>51</td>
      <td>10299</td>
      <td>RICAR</td>
      <td>4</td>
      <td>2012-09-06</td>
      <td>2012-10-04</td>
      <td>2012-09-13</td>
      <td>2</td>
      <td>29.76</td>
      <td>Ricardo Adocicados</td>
      <td>Av. Copacabana, 267</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>02389-890</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>52</td>
      <td>10300</td>
      <td>MAGAA</td>
      <td>2</td>
      <td>2012-09-09</td>
      <td>2012-10-07</td>
      <td>2012-09-18</td>
      <td>2</td>
      <td>17.68</td>
      <td>Magazzini Alimentari Riuniti</td>
      <td>Via Ludovico il Moro 22</td>
      <td>Bergamo</td>
      <td>Southern Europe</td>
      <td>24100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>53</td>
      <td>10301</td>
      <td>WANDK</td>
      <td>8</td>
      <td>2012-09-09</td>
      <td>2012-10-07</td>
      <td>2012-09-17</td>
      <td>2</td>
      <td>45.08</td>
      <td>Die Wandernde Kuh</td>
      <td>Adenauerallee 900</td>
      <td>Stuttgart</td>
      <td>Western Europe</td>
      <td>70563</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>54</td>
      <td>10302</td>
      <td>SUPRD</td>
      <td>4</td>
      <td>2012-09-10</td>
      <td>2012-10-08</td>
      <td>2012-10-09</td>
      <td>2</td>
      <td>6.27</td>
      <td>Suprêmes délices</td>
      <td>Boulevard Tirou, 255</td>
      <td>Charleroi</td>
      <td>Western Europe</td>
      <td>B-6000</td>
      <td>Belgium</td>
    </tr>
    <tr>
      <td>55</td>
      <td>10303</td>
      <td>GODOS</td>
      <td>7</td>
      <td>2012-09-11</td>
      <td>2012-10-09</td>
      <td>2012-09-18</td>
      <td>2</td>
      <td>107.83</td>
      <td>Godos Cocina Típica</td>
      <td>C/ Romero, 33</td>
      <td>Sevilla</td>
      <td>Southern Europe</td>
      <td>41101</td>
      <td>Spain</td>
    </tr>
    <tr>
      <td>56</td>
      <td>10304</td>
      <td>TORTU</td>
      <td>1</td>
      <td>2012-09-12</td>
      <td>2012-10-10</td>
      <td>2012-09-17</td>
      <td>2</td>
      <td>63.79</td>
      <td>Tortuga Restaurante</td>
      <td>Avda. Azteca 123</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05033</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>57</td>
      <td>10305</td>
      <td>OLDWO</td>
      <td>8</td>
      <td>2012-09-13</td>
      <td>2012-10-11</td>
      <td>2012-10-09</td>
      <td>3</td>
      <td>257.62</td>
      <td>Old World Delicatessen</td>
      <td>2743 Bering St.</td>
      <td>Anchorage</td>
      <td>North America</td>
      <td>99508</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>58</td>
      <td>10306</td>
      <td>ROMEY</td>
      <td>1</td>
      <td>2012-09-16</td>
      <td>2012-10-14</td>
      <td>2012-09-23</td>
      <td>3</td>
      <td>7.56</td>
      <td>Romero y tomillo</td>
      <td>Gran Vía, 1</td>
      <td>Madrid</td>
      <td>Southern Europe</td>
      <td>28001</td>
      <td>Spain</td>
    </tr>
    <tr>
      <td>59</td>
      <td>10307</td>
      <td>LONEP</td>
      <td>2</td>
      <td>2012-09-17</td>
      <td>2012-10-15</td>
      <td>2012-09-25</td>
      <td>2</td>
      <td>0.56</td>
      <td>Lonesome Pine Restaurant</td>
      <td>89 Chiaroscuro Rd.</td>
      <td>Portland</td>
      <td>North America</td>
      <td>97219</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>60</td>
      <td>10308</td>
      <td>ANATR</td>
      <td>7</td>
      <td>2012-09-18</td>
      <td>2012-10-16</td>
      <td>2012-09-24</td>
      <td>3</td>
      <td>1.61</td>
      <td>Ana Trujillo Emparedados y helados</td>
      <td>Avda. de la Constitución 2222</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05021</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>61</td>
      <td>10309</td>
      <td>HUNGO</td>
      <td>3</td>
      <td>2012-09-19</td>
      <td>2012-10-17</td>
      <td>2012-10-23</td>
      <td>1</td>
      <td>47.30</td>
      <td>Hungry Owl All-Night Grocers</td>
      <td>8 Johnstown Road</td>
      <td>Cork</td>
      <td>British Isles</td>
      <td>None</td>
      <td>Ireland</td>
    </tr>
    <tr>
      <td>62</td>
      <td>10310</td>
      <td>THEBI</td>
      <td>8</td>
      <td>2012-09-20</td>
      <td>2012-10-18</td>
      <td>2012-09-27</td>
      <td>2</td>
      <td>17.52</td>
      <td>The Big Cheese</td>
      <td>89 Jefferson Way Suite 2</td>
      <td>Portland</td>
      <td>North America</td>
      <td>97201</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>63</td>
      <td>10311</td>
      <td>DUMO</td>
      <td>1</td>
      <td>2012-09-20</td>
      <td>2012-10-04</td>
      <td>2012-09-26</td>
      <td>3</td>
      <td>24.69</td>
      <td>Du monde entier</td>
      <td>67, rue des Cinquante Otages</td>
      <td>Nantes</td>
      <td>Western Europe</td>
      <td>44000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>64</td>
      <td>10312</td>
      <td>WANDK</td>
      <td>2</td>
      <td>2012-09-23</td>
      <td>2012-10-21</td>
      <td>2012-10-03</td>
      <td>2</td>
      <td>40.26</td>
      <td>Die Wandernde Kuh</td>
      <td>Adenauerallee 900</td>
      <td>Stuttgart</td>
      <td>Western Europe</td>
      <td>70563</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>65</td>
      <td>10313</td>
      <td>QUICK</td>
      <td>2</td>
      <td>2012-09-24</td>
      <td>2012-10-22</td>
      <td>2012-10-04</td>
      <td>2</td>
      <td>1.96</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>66</td>
      <td>10314</td>
      <td>RATTC</td>
      <td>1</td>
      <td>2012-09-25</td>
      <td>2012-10-23</td>
      <td>2012-10-04</td>
      <td>2</td>
      <td>74.16</td>
      <td>Rattlesnake Canyon Grocery</td>
      <td>2817 Milton Dr.</td>
      <td>Albuquerque</td>
      <td>North America</td>
      <td>87110</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>67</td>
      <td>10315</td>
      <td>ISLAT</td>
      <td>4</td>
      <td>2012-09-26</td>
      <td>2012-10-24</td>
      <td>2012-10-03</td>
      <td>2</td>
      <td>41.76</td>
      <td>Island Trading</td>
      <td>Garden House Crowther Way</td>
      <td>Cowes</td>
      <td>British Isles</td>
      <td>PO31 7PJ</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>68</td>
      <td>10316</td>
      <td>RATTC</td>
      <td>1</td>
      <td>2012-09-27</td>
      <td>2012-10-25</td>
      <td>2012-10-08</td>
      <td>3</td>
      <td>150.15</td>
      <td>Rattlesnake Canyon Grocery</td>
      <td>2817 Milton Dr.</td>
      <td>Albuquerque</td>
      <td>North America</td>
      <td>87110</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>69</td>
      <td>10317</td>
      <td>LONEP</td>
      <td>6</td>
      <td>2012-09-30</td>
      <td>2012-10-28</td>
      <td>2012-10-10</td>
      <td>1</td>
      <td>12.69</td>
      <td>Lonesome Pine Restaurant</td>
      <td>89 Chiaroscuro Rd.</td>
      <td>Portland</td>
      <td>North America</td>
      <td>97219</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>70</td>
      <td>10318</td>
      <td>ISLAT</td>
      <td>8</td>
      <td>2012-10-01</td>
      <td>2012-10-29</td>
      <td>2012-10-04</td>
      <td>2</td>
      <td>4.73</td>
      <td>Island Trading</td>
      <td>Garden House Crowther Way</td>
      <td>Cowes</td>
      <td>British Isles</td>
      <td>PO31 7PJ</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>71</td>
      <td>10319</td>
      <td>TORTU</td>
      <td>7</td>
      <td>2012-10-02</td>
      <td>2012-10-30</td>
      <td>2012-10-11</td>
      <td>3</td>
      <td>64.50</td>
      <td>Tortuga Restaurante</td>
      <td>Avda. Azteca 123</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05033</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>72</td>
      <td>10320</td>
      <td>WARTH</td>
      <td>5</td>
      <td>2012-10-03</td>
      <td>2012-10-17</td>
      <td>2012-10-18</td>
      <td>3</td>
      <td>34.57</td>
      <td>Wartian Herkku</td>
      <td>Torikatu 38</td>
      <td>Oulu</td>
      <td>Scandinavia</td>
      <td>90110</td>
      <td>Finland</td>
    </tr>
    <tr>
      <td>73</td>
      <td>10321</td>
      <td>ISLAT</td>
      <td>3</td>
      <td>2012-10-03</td>
      <td>2012-10-31</td>
      <td>2012-10-11</td>
      <td>2</td>
      <td>3.43</td>
      <td>Island Trading</td>
      <td>Garden House Crowther Way</td>
      <td>Cowes</td>
      <td>British Isles</td>
      <td>PO31 7PJ</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>74</td>
      <td>10322</td>
      <td>PERIC</td>
      <td>7</td>
      <td>2012-10-04</td>
      <td>2012-11-01</td>
      <td>2012-10-23</td>
      <td>3</td>
      <td>0.40</td>
      <td>Pericles Comidas clásicas</td>
      <td>Calle Dr. Jorge Cash 321</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05033</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>75</td>
      <td>10323</td>
      <td>KOENE</td>
      <td>4</td>
      <td>2012-10-07</td>
      <td>2012-11-04</td>
      <td>2012-10-14</td>
      <td>1</td>
      <td>4.88</td>
      <td>Königlich Essen</td>
      <td>Maubelstr. 90</td>
      <td>Brandenburg</td>
      <td>Western Europe</td>
      <td>14776</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>76</td>
      <td>10324</td>
      <td>SAVEA</td>
      <td>9</td>
      <td>2012-10-08</td>
      <td>2012-11-05</td>
      <td>2012-10-10</td>
      <td>1</td>
      <td>214.27</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>77</td>
      <td>10325</td>
      <td>KOENE</td>
      <td>1</td>
      <td>2012-10-09</td>
      <td>2012-10-23</td>
      <td>2012-10-14</td>
      <td>3</td>
      <td>64.86</td>
      <td>Königlich Essen</td>
      <td>Maubelstr. 90</td>
      <td>Brandenburg</td>
      <td>Western Europe</td>
      <td>14776</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>78</td>
      <td>10326</td>
      <td>BOLID</td>
      <td>4</td>
      <td>2012-10-10</td>
      <td>2012-11-07</td>
      <td>2012-10-14</td>
      <td>2</td>
      <td>77.92</td>
      <td>Bólido Comidas preparadas</td>
      <td>C/ Araquil, 67</td>
      <td>Madrid</td>
      <td>Southern Europe</td>
      <td>28023</td>
      <td>Spain</td>
    </tr>
    <tr>
      <td>79</td>
      <td>10327</td>
      <td>FOLKO</td>
      <td>2</td>
      <td>2012-10-11</td>
      <td>2012-11-08</td>
      <td>2012-10-14</td>
      <td>1</td>
      <td>63.36</td>
      <td>Folk och fä HB</td>
      <td>Åkergatan 24</td>
      <td>Bräcke</td>
      <td>Northern Europe</td>
      <td>S-844 67</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>80</td>
      <td>10328</td>
      <td>FURIB</td>
      <td>4</td>
      <td>2012-10-14</td>
      <td>2012-11-11</td>
      <td>2012-10-17</td>
      <td>3</td>
      <td>87.03</td>
      <td>Furia Bacalhau e Frutos do Mar</td>
      <td>Jardim das rosas n. 32</td>
      <td>Lisboa</td>
      <td>Southern Europe</td>
      <td>1675</td>
      <td>Portugal</td>
    </tr>
    <tr>
      <td>81</td>
      <td>10329</td>
      <td>SPLIR</td>
      <td>4</td>
      <td>2012-10-15</td>
      <td>2012-11-26</td>
      <td>2012-10-23</td>
      <td>2</td>
      <td>191.67</td>
      <td>Split Rail Beer &amp; Ale</td>
      <td>P.O. Box 555</td>
      <td>Lander</td>
      <td>North America</td>
      <td>82520</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>82</td>
      <td>10330</td>
      <td>LILAS</td>
      <td>3</td>
      <td>2012-10-16</td>
      <td>2012-11-13</td>
      <td>2012-10-28</td>
      <td>1</td>
      <td>12.75</td>
      <td>LILA-Supermercado</td>
      <td>Carrera 52 con Ave. Bolívar #65-98 Llano Largo</td>
      <td>Barquisimeto</td>
      <td>South America</td>
      <td>3508</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>83</td>
      <td>10331</td>
      <td>BONAP</td>
      <td>9</td>
      <td>2012-10-16</td>
      <td>2012-11-27</td>
      <td>2012-10-21</td>
      <td>1</td>
      <td>10.19</td>
      <td>Bon app'</td>
      <td>12, rue des Bouchers</td>
      <td>Marseille</td>
      <td>Western Europe</td>
      <td>13008</td>
      <td>France</td>
    </tr>
    <tr>
      <td>84</td>
      <td>10332</td>
      <td>MEREP</td>
      <td>3</td>
      <td>2012-10-17</td>
      <td>2012-11-28</td>
      <td>2012-10-21</td>
      <td>2</td>
      <td>52.84</td>
      <td>Mère Paillarde</td>
      <td>43 rue St. Laurent</td>
      <td>Montréal</td>
      <td>North America</td>
      <td>H1J 1C3</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>85</td>
      <td>10333</td>
      <td>WARTH</td>
      <td>5</td>
      <td>2012-10-18</td>
      <td>2012-11-15</td>
      <td>2012-10-25</td>
      <td>3</td>
      <td>0.59</td>
      <td>Wartian Herkku</td>
      <td>Torikatu 38</td>
      <td>Oulu</td>
      <td>Scandinavia</td>
      <td>90110</td>
      <td>Finland</td>
    </tr>
    <tr>
      <td>86</td>
      <td>10334</td>
      <td>VICTE</td>
      <td>8</td>
      <td>2012-10-21</td>
      <td>2012-11-18</td>
      <td>2012-10-28</td>
      <td>2</td>
      <td>8.56</td>
      <td>Victuailles en stock</td>
      <td>2, rue du Commerce</td>
      <td>Lyon</td>
      <td>Western Europe</td>
      <td>69004</td>
      <td>France</td>
    </tr>
    <tr>
      <td>87</td>
      <td>10335</td>
      <td>HUNGO</td>
      <td>7</td>
      <td>2012-10-22</td>
      <td>2012-11-19</td>
      <td>2012-10-24</td>
      <td>2</td>
      <td>42.11</td>
      <td>Hungry Owl All-Night Grocers</td>
      <td>8 Johnstown Road</td>
      <td>Cork</td>
      <td>British Isles</td>
      <td>None</td>
      <td>Ireland</td>
    </tr>
    <tr>
      <td>88</td>
      <td>10336</td>
      <td>PRINI</td>
      <td>7</td>
      <td>2012-10-23</td>
      <td>2012-11-20</td>
      <td>2012-10-25</td>
      <td>2</td>
      <td>15.51</td>
      <td>Princesa Isabel Vinhos</td>
      <td>Estrada da saúde n. 58</td>
      <td>Lisboa</td>
      <td>Southern Europe</td>
      <td>1756</td>
      <td>Portugal</td>
    </tr>
    <tr>
      <td>89</td>
      <td>10337</td>
      <td>FRANK</td>
      <td>4</td>
      <td>2012-10-24</td>
      <td>2012-11-21</td>
      <td>2012-10-29</td>
      <td>3</td>
      <td>108.26</td>
      <td>Frankenversand</td>
      <td>Berliner Platz 43</td>
      <td>München</td>
      <td>Western Europe</td>
      <td>80805</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>90</td>
      <td>10338</td>
      <td>OLDWO</td>
      <td>4</td>
      <td>2012-10-25</td>
      <td>2012-11-22</td>
      <td>2012-10-29</td>
      <td>3</td>
      <td>84.21</td>
      <td>Old World Delicatessen</td>
      <td>2743 Bering St.</td>
      <td>Anchorage</td>
      <td>North America</td>
      <td>99508</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>91</td>
      <td>10339</td>
      <td>MEREP</td>
      <td>2</td>
      <td>2012-10-28</td>
      <td>2012-11-25</td>
      <td>2012-11-04</td>
      <td>2</td>
      <td>15.66</td>
      <td>Mère Paillarde</td>
      <td>43 rue St. Laurent</td>
      <td>Montréal</td>
      <td>North America</td>
      <td>H1J 1C3</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>92</td>
      <td>10340</td>
      <td>BONAP</td>
      <td>1</td>
      <td>2012-10-29</td>
      <td>2012-11-26</td>
      <td>2012-11-08</td>
      <td>3</td>
      <td>166.31</td>
      <td>Bon app'</td>
      <td>12, rue des Bouchers</td>
      <td>Marseille</td>
      <td>Western Europe</td>
      <td>13008</td>
      <td>France</td>
    </tr>
    <tr>
      <td>93</td>
      <td>10341</td>
      <td>SIMOB</td>
      <td>7</td>
      <td>2012-10-29</td>
      <td>2012-11-26</td>
      <td>2012-11-05</td>
      <td>3</td>
      <td>26.78</td>
      <td>Simons bistro</td>
      <td>Vinbæltet 34</td>
      <td>Kobenhavn</td>
      <td>Northern Europe</td>
      <td>1734</td>
      <td>Denmark</td>
    </tr>
    <tr>
      <td>94</td>
      <td>10342</td>
      <td>FRANK</td>
      <td>4</td>
      <td>2012-10-30</td>
      <td>2012-11-13</td>
      <td>2012-11-04</td>
      <td>2</td>
      <td>54.83</td>
      <td>Frankenversand</td>
      <td>Berliner Platz 43</td>
      <td>München</td>
      <td>Western Europe</td>
      <td>80805</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>95</td>
      <td>10343</td>
      <td>LEHMS</td>
      <td>4</td>
      <td>2012-10-31</td>
      <td>2012-11-28</td>
      <td>2012-11-06</td>
      <td>1</td>
      <td>110.37</td>
      <td>Lehmanns Marktstand</td>
      <td>Magazinweg 7</td>
      <td>Frankfurt a.M.</td>
      <td>Western Europe</td>
      <td>60528</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>96</td>
      <td>10344</td>
      <td>WHITC</td>
      <td>4</td>
      <td>2012-11-01</td>
      <td>2012-11-29</td>
      <td>2012-11-05</td>
      <td>2</td>
      <td>23.29</td>
      <td>White Clover Markets</td>
      <td>1029 - 12th Ave. S.</td>
      <td>Seattle</td>
      <td>North America</td>
      <td>98124</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>97</td>
      <td>10345</td>
      <td>QUICK</td>
      <td>2</td>
      <td>2012-11-04</td>
      <td>2012-12-02</td>
      <td>2012-11-11</td>
      <td>2</td>
      <td>249.06</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>98</td>
      <td>10346</td>
      <td>RATTC</td>
      <td>3</td>
      <td>2012-11-05</td>
      <td>2012-12-17</td>
      <td>2012-11-08</td>
      <td>3</td>
      <td>142.08</td>
      <td>Rattlesnake Canyon Grocery</td>
      <td>2817 Milton Dr.</td>
      <td>Albuquerque</td>
      <td>North America</td>
      <td>87110</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>99</td>
      <td>10347</td>
      <td>FAMIA</td>
      <td>4</td>
      <td>2012-11-06</td>
      <td>2012-12-04</td>
      <td>2012-11-08</td>
      <td>3</td>
      <td>3.10</td>
      <td>Familia Arquibaldo</td>
      <td>Rua Orós, 92</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05442-030</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>100</td>
      <td>10348</td>
      <td>WANDK</td>
      <td>4</td>
      <td>2012-11-07</td>
      <td>2012-12-05</td>
      <td>2012-11-15</td>
      <td>2</td>
      <td>0.78</td>
      <td>Die Wandernde Kuh</td>
      <td>Adenauerallee 900</td>
      <td>Stuttgart</td>
      <td>Western Europe</td>
      <td>70563</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>101</td>
      <td>10349</td>
      <td>SPLIR</td>
      <td>7</td>
      <td>2012-11-08</td>
      <td>2012-12-06</td>
      <td>2012-11-15</td>
      <td>1</td>
      <td>8.63</td>
      <td>Split Rail Beer &amp; Ale</td>
      <td>P.O. Box 555</td>
      <td>Lander</td>
      <td>North America</td>
      <td>82520</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>102</td>
      <td>10350</td>
      <td>LAMAI</td>
      <td>6</td>
      <td>2012-11-11</td>
      <td>2012-12-09</td>
      <td>2012-12-03</td>
      <td>2</td>
      <td>64.19</td>
      <td>La maison d'Asie</td>
      <td>1 rue Alsace-Lorraine</td>
      <td>Toulouse</td>
      <td>Western Europe</td>
      <td>31000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>103</td>
      <td>10351</td>
      <td>ERNSH</td>
      <td>1</td>
      <td>2012-11-11</td>
      <td>2012-12-09</td>
      <td>2012-11-20</td>
      <td>1</td>
      <td>162.33</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>104</td>
      <td>10352</td>
      <td>FURIB</td>
      <td>3</td>
      <td>2012-11-12</td>
      <td>2012-11-26</td>
      <td>2012-11-18</td>
      <td>3</td>
      <td>1.30</td>
      <td>Furia Bacalhau e Frutos do Mar</td>
      <td>Jardim das rosas n. 32</td>
      <td>Lisboa</td>
      <td>Southern Europe</td>
      <td>1675</td>
      <td>Portugal</td>
    </tr>
    <tr>
      <td>105</td>
      <td>10353</td>
      <td>PICCO</td>
      <td>7</td>
      <td>2012-11-13</td>
      <td>2012-12-11</td>
      <td>2012-11-25</td>
      <td>3</td>
      <td>360.63</td>
      <td>Piccolo und mehr</td>
      <td>Geislweg 14</td>
      <td>Salzburg</td>
      <td>Western Europe</td>
      <td>5020</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>106</td>
      <td>10354</td>
      <td>PERIC</td>
      <td>8</td>
      <td>2012-11-14</td>
      <td>2012-12-12</td>
      <td>2012-11-20</td>
      <td>3</td>
      <td>53.80</td>
      <td>Pericles Comidas clásicas</td>
      <td>Calle Dr. Jorge Cash 321</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05033</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>107</td>
      <td>10355</td>
      <td>AROUT</td>
      <td>6</td>
      <td>2012-11-15</td>
      <td>2012-12-13</td>
      <td>2012-11-20</td>
      <td>1</td>
      <td>41.95</td>
      <td>Around the Horn</td>
      <td>Brook Farm Stratford St. Mary</td>
      <td>Colchester</td>
      <td>British Isles</td>
      <td>CO7 6JX</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>108</td>
      <td>10356</td>
      <td>WANDK</td>
      <td>6</td>
      <td>2012-11-18</td>
      <td>2012-12-16</td>
      <td>2012-11-27</td>
      <td>2</td>
      <td>36.71</td>
      <td>Die Wandernde Kuh</td>
      <td>Adenauerallee 900</td>
      <td>Stuttgart</td>
      <td>Western Europe</td>
      <td>70563</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>109</td>
      <td>10357</td>
      <td>LILAS</td>
      <td>1</td>
      <td>2012-11-19</td>
      <td>2012-12-17</td>
      <td>2012-12-02</td>
      <td>3</td>
      <td>34.88</td>
      <td>LILA-Supermercado</td>
      <td>Carrera 52 con Ave. Bolívar #65-98 Llano Largo</td>
      <td>Barquisimeto</td>
      <td>South America</td>
      <td>3508</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>110</td>
      <td>10358</td>
      <td>LAMAI</td>
      <td>5</td>
      <td>2012-11-20</td>
      <td>2012-12-18</td>
      <td>2012-11-27</td>
      <td>1</td>
      <td>19.64</td>
      <td>La maison d'Asie</td>
      <td>1 rue Alsace-Lorraine</td>
      <td>Toulouse</td>
      <td>Western Europe</td>
      <td>31000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>111</td>
      <td>10359</td>
      <td>SEVES</td>
      <td>5</td>
      <td>2012-11-21</td>
      <td>2012-12-19</td>
      <td>2012-11-26</td>
      <td>3</td>
      <td>288.43</td>
      <td>Seven Seas Imports</td>
      <td>90 Wadhurst Rd.</td>
      <td>London</td>
      <td>British Isles</td>
      <td>OX15 4NB</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>112</td>
      <td>10360</td>
      <td>BLONP</td>
      <td>4</td>
      <td>2012-11-22</td>
      <td>2012-12-20</td>
      <td>2012-12-02</td>
      <td>3</td>
      <td>131.70</td>
      <td>Blondel père et fils</td>
      <td>24, place Kléber</td>
      <td>Strasbourg</td>
      <td>Western Europe</td>
      <td>67000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>113</td>
      <td>10361</td>
      <td>QUICK</td>
      <td>1</td>
      <td>2012-11-22</td>
      <td>2012-12-20</td>
      <td>2012-12-03</td>
      <td>2</td>
      <td>183.17</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>114</td>
      <td>10362</td>
      <td>BONAP</td>
      <td>3</td>
      <td>2012-11-25</td>
      <td>2012-12-23</td>
      <td>2012-11-28</td>
      <td>1</td>
      <td>96.04</td>
      <td>Bon app'</td>
      <td>12, rue des Bouchers</td>
      <td>Marseille</td>
      <td>Western Europe</td>
      <td>13008</td>
      <td>France</td>
    </tr>
    <tr>
      <td>115</td>
      <td>10363</td>
      <td>DRACD</td>
      <td>4</td>
      <td>2012-11-26</td>
      <td>2012-12-24</td>
      <td>2012-12-04</td>
      <td>3</td>
      <td>30.54</td>
      <td>Drachenblut Delikatessen</td>
      <td>Walserweg 21</td>
      <td>Aachen</td>
      <td>Western Europe</td>
      <td>52066</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>116</td>
      <td>10364</td>
      <td>EASTC</td>
      <td>1</td>
      <td>2012-11-26</td>
      <td>2013-01-07</td>
      <td>2012-12-04</td>
      <td>1</td>
      <td>71.97</td>
      <td>Eastern Connection</td>
      <td>35 King George</td>
      <td>London</td>
      <td>British Isles</td>
      <td>WX3 6FW</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>117</td>
      <td>10365</td>
      <td>ANTO</td>
      <td>3</td>
      <td>2012-11-27</td>
      <td>2012-12-25</td>
      <td>2012-12-02</td>
      <td>2</td>
      <td>22.00</td>
      <td>Antonio Moreno Taquería</td>
      <td>Mataderos  2312</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05023</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>118</td>
      <td>10366</td>
      <td>GALED</td>
      <td>8</td>
      <td>2012-11-28</td>
      <td>2013-01-09</td>
      <td>2012-12-30</td>
      <td>2</td>
      <td>10.14</td>
      <td>Galería del gastronómo</td>
      <td>Rambla de Cataluña, 23</td>
      <td>Barcelona</td>
      <td>Southern Europe</td>
      <td>8022</td>
      <td>Spain</td>
    </tr>
    <tr>
      <td>119</td>
      <td>10367</td>
      <td>VAFFE</td>
      <td>7</td>
      <td>2012-11-28</td>
      <td>2012-12-26</td>
      <td>2012-12-02</td>
      <td>3</td>
      <td>13.55</td>
      <td>Vaffeljernet</td>
      <td>Smagsloget 45</td>
      <td>Århus</td>
      <td>Northern Europe</td>
      <td>8200</td>
      <td>Denmark</td>
    </tr>
    <tr>
      <td>120</td>
      <td>10368</td>
      <td>ERNSH</td>
      <td>2</td>
      <td>2012-11-29</td>
      <td>2012-12-27</td>
      <td>2012-12-02</td>
      <td>2</td>
      <td>101.95</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>121</td>
      <td>10369</td>
      <td>SPLIR</td>
      <td>8</td>
      <td>2012-12-02</td>
      <td>2012-12-30</td>
      <td>2012-12-09</td>
      <td>2</td>
      <td>195.68</td>
      <td>Split Rail Beer &amp; Ale</td>
      <td>P.O. Box 555</td>
      <td>Lander</td>
      <td>North America</td>
      <td>82520</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>122</td>
      <td>10370</td>
      <td>CHOPS</td>
      <td>6</td>
      <td>2012-12-03</td>
      <td>2012-12-31</td>
      <td>2012-12-27</td>
      <td>2</td>
      <td>1.17</td>
      <td>Chop-suey Chinese</td>
      <td>Hauptstr. 31</td>
      <td>Bern</td>
      <td>Western Europe</td>
      <td>3012</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <td>123</td>
      <td>10371</td>
      <td>LAMAI</td>
      <td>1</td>
      <td>2012-12-03</td>
      <td>2012-12-31</td>
      <td>2012-12-24</td>
      <td>1</td>
      <td>0.45</td>
      <td>La maison d'Asie</td>
      <td>1 rue Alsace-Lorraine</td>
      <td>Toulouse</td>
      <td>Western Europe</td>
      <td>31000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>124</td>
      <td>10372</td>
      <td>QUEE</td>
      <td>5</td>
      <td>2012-12-04</td>
      <td>2013-01-01</td>
      <td>2012-12-09</td>
      <td>2</td>
      <td>890.78</td>
      <td>Queen Cozinha</td>
      <td>Alameda dos Canàrios, 891</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05487-020</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>125</td>
      <td>10373</td>
      <td>HUNGO</td>
      <td>4</td>
      <td>2012-12-05</td>
      <td>2013-01-02</td>
      <td>2012-12-11</td>
      <td>3</td>
      <td>124.12</td>
      <td>Hungry Owl All-Night Grocers</td>
      <td>8 Johnstown Road</td>
      <td>Cork</td>
      <td>British Isles</td>
      <td>None</td>
      <td>Ireland</td>
    </tr>
    <tr>
      <td>126</td>
      <td>10374</td>
      <td>WOLZA</td>
      <td>1</td>
      <td>2012-12-05</td>
      <td>2013-01-02</td>
      <td>2012-12-09</td>
      <td>3</td>
      <td>3.94</td>
      <td>Wolski Zajazd</td>
      <td>ul. Filtrowa 68</td>
      <td>Warszawa</td>
      <td>Eastern Europe</td>
      <td>01-012</td>
      <td>Poland</td>
    </tr>
    <tr>
      <td>127</td>
      <td>10375</td>
      <td>HUNGC</td>
      <td>3</td>
      <td>2012-12-06</td>
      <td>2013-01-03</td>
      <td>2012-12-09</td>
      <td>2</td>
      <td>20.12</td>
      <td>Hungry Coyote Import Store</td>
      <td>City Center Plaza 516 Main St.</td>
      <td>Elgin</td>
      <td>North America</td>
      <td>97827</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>128</td>
      <td>10376</td>
      <td>MEREP</td>
      <td>1</td>
      <td>2012-12-09</td>
      <td>2013-01-06</td>
      <td>2012-12-13</td>
      <td>2</td>
      <td>20.39</td>
      <td>Mère Paillarde</td>
      <td>43 rue St. Laurent</td>
      <td>Montréal</td>
      <td>North America</td>
      <td>H1J 1C3</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>129</td>
      <td>10377</td>
      <td>SEVES</td>
      <td>1</td>
      <td>2012-12-09</td>
      <td>2013-01-06</td>
      <td>2012-12-13</td>
      <td>3</td>
      <td>22.21</td>
      <td>Seven Seas Imports</td>
      <td>90 Wadhurst Rd.</td>
      <td>London</td>
      <td>British Isles</td>
      <td>OX15 4NB</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>130</td>
      <td>10378</td>
      <td>FOLKO</td>
      <td>5</td>
      <td>2012-12-10</td>
      <td>2013-01-07</td>
      <td>2012-12-19</td>
      <td>3</td>
      <td>5.44</td>
      <td>Folk och fä HB</td>
      <td>Åkergatan 24</td>
      <td>Bräcke</td>
      <td>Northern Europe</td>
      <td>S-844 67</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>131</td>
      <td>10379</td>
      <td>QUEDE</td>
      <td>2</td>
      <td>2012-12-11</td>
      <td>2013-01-08</td>
      <td>2012-12-13</td>
      <td>1</td>
      <td>45.03</td>
      <td>Que Delícia</td>
      <td>Rua da Panificadora, 12</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>02389-673</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>132</td>
      <td>10380</td>
      <td>HUNGO</td>
      <td>8</td>
      <td>2012-12-12</td>
      <td>2013-01-09</td>
      <td>2013-01-16</td>
      <td>3</td>
      <td>35.03</td>
      <td>Hungry Owl All-Night Grocers</td>
      <td>8 Johnstown Road</td>
      <td>Cork</td>
      <td>British Isles</td>
      <td>None</td>
      <td>Ireland</td>
    </tr>
    <tr>
      <td>133</td>
      <td>10381</td>
      <td>LILAS</td>
      <td>3</td>
      <td>2012-12-12</td>
      <td>2013-01-09</td>
      <td>2012-12-13</td>
      <td>3</td>
      <td>7.99</td>
      <td>LILA-Supermercado</td>
      <td>Carrera 52 con Ave. Bolívar #65-98 Llano Largo</td>
      <td>Barquisimeto</td>
      <td>South America</td>
      <td>3508</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>134</td>
      <td>10382</td>
      <td>ERNSH</td>
      <td>4</td>
      <td>2012-12-13</td>
      <td>2013-01-10</td>
      <td>2012-12-16</td>
      <td>1</td>
      <td>94.77</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>135</td>
      <td>10383</td>
      <td>AROUT</td>
      <td>8</td>
      <td>2012-12-16</td>
      <td>2013-01-13</td>
      <td>2012-12-18</td>
      <td>3</td>
      <td>34.24</td>
      <td>Around the Horn</td>
      <td>Brook Farm Stratford St. Mary</td>
      <td>Colchester</td>
      <td>British Isles</td>
      <td>CO7 6JX</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>136</td>
      <td>10384</td>
      <td>BERGS</td>
      <td>3</td>
      <td>2012-12-16</td>
      <td>2013-01-13</td>
      <td>2012-12-20</td>
      <td>3</td>
      <td>168.64</td>
      <td>Berglunds snabbköp</td>
      <td>Berguvsvägen  8</td>
      <td>Luleå</td>
      <td>Northern Europe</td>
      <td>S-958 22</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>137</td>
      <td>10385</td>
      <td>SPLIR</td>
      <td>1</td>
      <td>2012-12-17</td>
      <td>2013-01-14</td>
      <td>2012-12-23</td>
      <td>2</td>
      <td>30.96</td>
      <td>Split Rail Beer &amp; Ale</td>
      <td>P.O. Box 555</td>
      <td>Lander</td>
      <td>North America</td>
      <td>82520</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>138</td>
      <td>10386</td>
      <td>FAMIA</td>
      <td>9</td>
      <td>2012-12-18</td>
      <td>2013-01-01</td>
      <td>2012-12-25</td>
      <td>3</td>
      <td>13.99</td>
      <td>Familia Arquibaldo</td>
      <td>Rua Orós, 92</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05442-030</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>139</td>
      <td>10387</td>
      <td>SANTG</td>
      <td>1</td>
      <td>2012-12-18</td>
      <td>2013-01-15</td>
      <td>2012-12-20</td>
      <td>2</td>
      <td>93.63</td>
      <td>Santé Gourmet</td>
      <td>Erling Skakkes gate 78</td>
      <td>Stavern</td>
      <td>Scandinavia</td>
      <td>4110</td>
      <td>Norway</td>
    </tr>
    <tr>
      <td>140</td>
      <td>10388</td>
      <td>SEVES</td>
      <td>2</td>
      <td>2012-12-19</td>
      <td>2013-01-16</td>
      <td>2012-12-20</td>
      <td>1</td>
      <td>34.86</td>
      <td>Seven Seas Imports</td>
      <td>90 Wadhurst Rd.</td>
      <td>London</td>
      <td>British Isles</td>
      <td>OX15 4NB</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>141</td>
      <td>10389</td>
      <td>BOTTM</td>
      <td>4</td>
      <td>2012-12-20</td>
      <td>2013-01-17</td>
      <td>2012-12-24</td>
      <td>2</td>
      <td>47.42</td>
      <td>Bottom-Dollar Markets</td>
      <td>23 Tsawassen Blvd.</td>
      <td>Tsawassen</td>
      <td>North America</td>
      <td>T2F 8M4</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>142</td>
      <td>10390</td>
      <td>ERNSH</td>
      <td>6</td>
      <td>2012-12-23</td>
      <td>2013-01-20</td>
      <td>2012-12-26</td>
      <td>1</td>
      <td>126.38</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>143</td>
      <td>10391</td>
      <td>DRACD</td>
      <td>3</td>
      <td>2012-12-23</td>
      <td>2013-01-20</td>
      <td>2012-12-31</td>
      <td>3</td>
      <td>5.45</td>
      <td>Drachenblut Delikatessen</td>
      <td>Walserweg 21</td>
      <td>Aachen</td>
      <td>Western Europe</td>
      <td>52066</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>144</td>
      <td>10392</td>
      <td>PICCO</td>
      <td>2</td>
      <td>2012-12-24</td>
      <td>2013-01-21</td>
      <td>2013-01-01</td>
      <td>3</td>
      <td>122.46</td>
      <td>Piccolo und mehr</td>
      <td>Geislweg 14</td>
      <td>Salzburg</td>
      <td>Western Europe</td>
      <td>5020</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>145</td>
      <td>10393</td>
      <td>SAVEA</td>
      <td>1</td>
      <td>2012-12-25</td>
      <td>2013-01-22</td>
      <td>2013-01-03</td>
      <td>3</td>
      <td>126.56</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>146</td>
      <td>10394</td>
      <td>HUNGC</td>
      <td>1</td>
      <td>2012-12-25</td>
      <td>2013-01-22</td>
      <td>2013-01-03</td>
      <td>3</td>
      <td>30.34</td>
      <td>Hungry Coyote Import Store</td>
      <td>City Center Plaza 516 Main St.</td>
      <td>Elgin</td>
      <td>North America</td>
      <td>97827</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>147</td>
      <td>10395</td>
      <td>HILAA</td>
      <td>6</td>
      <td>2012-12-26</td>
      <td>2013-01-23</td>
      <td>2013-01-03</td>
      <td>1</td>
      <td>184.41</td>
      <td>HILARION-Abastos</td>
      <td>Carrera 22 con Ave. Carlos Soublette #8-35</td>
      <td>San Cristóbal</td>
      <td>South America</td>
      <td>5022</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>148</td>
      <td>10396</td>
      <td>FRANK</td>
      <td>1</td>
      <td>2012-12-27</td>
      <td>2013-01-10</td>
      <td>2013-01-06</td>
      <td>3</td>
      <td>135.35</td>
      <td>Frankenversand</td>
      <td>Berliner Platz 43</td>
      <td>München</td>
      <td>Western Europe</td>
      <td>80805</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>149</td>
      <td>10397</td>
      <td>PRINI</td>
      <td>5</td>
      <td>2012-12-27</td>
      <td>2013-01-24</td>
      <td>2013-01-02</td>
      <td>1</td>
      <td>60.26</td>
      <td>Princesa Isabel Vinhos</td>
      <td>Estrada da saúde n. 58</td>
      <td>Lisboa</td>
      <td>Southern Europe</td>
      <td>1756</td>
      <td>Portugal</td>
    </tr>
    <tr>
      <td>150</td>
      <td>10398</td>
      <td>SAVEA</td>
      <td>2</td>
      <td>2012-12-30</td>
      <td>2013-01-27</td>
      <td>2013-01-09</td>
      <td>3</td>
      <td>89.16</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>151</td>
      <td>10399</td>
      <td>VAFFE</td>
      <td>8</td>
      <td>2012-12-31</td>
      <td>2013-01-14</td>
      <td>2013-01-08</td>
      <td>3</td>
      <td>27.36</td>
      <td>Vaffeljernet</td>
      <td>Smagsloget 45</td>
      <td>Århus</td>
      <td>Northern Europe</td>
      <td>8200</td>
      <td>Denmark</td>
    </tr>
    <tr>
      <td>152</td>
      <td>10400</td>
      <td>EASTC</td>
      <td>1</td>
      <td>2013-01-01</td>
      <td>2013-01-29</td>
      <td>2013-01-16</td>
      <td>3</td>
      <td>83.93</td>
      <td>Eastern Connection</td>
      <td>35 King George</td>
      <td>London</td>
      <td>British Isles</td>
      <td>WX3 6FW</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>153</td>
      <td>10401</td>
      <td>RATTC</td>
      <td>1</td>
      <td>2013-01-01</td>
      <td>2013-01-29</td>
      <td>2013-01-10</td>
      <td>1</td>
      <td>12.51</td>
      <td>Rattlesnake Canyon Grocery</td>
      <td>2817 Milton Dr.</td>
      <td>Albuquerque</td>
      <td>North America</td>
      <td>87110</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>154</td>
      <td>10402</td>
      <td>ERNSH</td>
      <td>8</td>
      <td>2013-01-02</td>
      <td>2013-02-13</td>
      <td>2013-01-10</td>
      <td>2</td>
      <td>67.88</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>155</td>
      <td>10403</td>
      <td>ERNSH</td>
      <td>4</td>
      <td>2013-01-03</td>
      <td>2013-01-31</td>
      <td>2013-01-09</td>
      <td>3</td>
      <td>73.79</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>156</td>
      <td>10404</td>
      <td>MAGAA</td>
      <td>2</td>
      <td>2013-01-03</td>
      <td>2013-01-31</td>
      <td>2013-01-08</td>
      <td>1</td>
      <td>155.97</td>
      <td>Magazzini Alimentari Riuniti</td>
      <td>Via Ludovico il Moro 22</td>
      <td>Bergamo</td>
      <td>Southern Europe</td>
      <td>24100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>157</td>
      <td>10405</td>
      <td>LINOD</td>
      <td>1</td>
      <td>2013-01-06</td>
      <td>2013-02-03</td>
      <td>2013-01-22</td>
      <td>1</td>
      <td>34.82</td>
      <td>LINO-Delicateses</td>
      <td>Ave. 5 de Mayo Porlamar</td>
      <td>I. de Margarita</td>
      <td>South America</td>
      <td>4980</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>158</td>
      <td>10406</td>
      <td>QUEE</td>
      <td>7</td>
      <td>2013-01-07</td>
      <td>2013-02-18</td>
      <td>2013-01-13</td>
      <td>1</td>
      <td>108.04</td>
      <td>Queen Cozinha</td>
      <td>Alameda dos Canàrios, 891</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05487-020</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>159</td>
      <td>10407</td>
      <td>OTTIK</td>
      <td>2</td>
      <td>2013-01-07</td>
      <td>2013-02-04</td>
      <td>2013-01-30</td>
      <td>2</td>
      <td>91.48</td>
      <td>Ottilies Käseladen</td>
      <td>Mehrheimerstr. 369</td>
      <td>Köln</td>
      <td>Western Europe</td>
      <td>50739</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>160</td>
      <td>10408</td>
      <td>FOLIG</td>
      <td>8</td>
      <td>2013-01-08</td>
      <td>2013-02-05</td>
      <td>2013-01-14</td>
      <td>1</td>
      <td>11.26</td>
      <td>Folies gourmandes</td>
      <td>184, chaussée de Tournai</td>
      <td>Lille</td>
      <td>Western Europe</td>
      <td>59000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>161</td>
      <td>10409</td>
      <td>OCEA</td>
      <td>3</td>
      <td>2013-01-09</td>
      <td>2013-02-06</td>
      <td>2013-01-14</td>
      <td>1</td>
      <td>29.83</td>
      <td>Océano Atlántico Ltda.</td>
      <td>Ing. Gustavo Moncada 8585 Piso 20-A</td>
      <td>Buenos Aires</td>
      <td>South America</td>
      <td>1010</td>
      <td>Argentina</td>
    </tr>
    <tr>
      <td>162</td>
      <td>10410</td>
      <td>BOTTM</td>
      <td>3</td>
      <td>2013-01-10</td>
      <td>2013-02-07</td>
      <td>2013-01-15</td>
      <td>3</td>
      <td>2.40</td>
      <td>Bottom-Dollar Markets</td>
      <td>23 Tsawassen Blvd.</td>
      <td>Tsawassen</td>
      <td>North America</td>
      <td>T2F 8M4</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>163</td>
      <td>10411</td>
      <td>BOTTM</td>
      <td>9</td>
      <td>2013-01-10</td>
      <td>2013-02-07</td>
      <td>2013-01-21</td>
      <td>3</td>
      <td>23.65</td>
      <td>Bottom-Dollar Markets</td>
      <td>23 Tsawassen Blvd.</td>
      <td>Tsawassen</td>
      <td>North America</td>
      <td>T2F 8M4</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>164</td>
      <td>10412</td>
      <td>WARTH</td>
      <td>8</td>
      <td>2013-01-13</td>
      <td>2013-02-10</td>
      <td>2013-01-15</td>
      <td>2</td>
      <td>3.77</td>
      <td>Wartian Herkku</td>
      <td>Torikatu 38</td>
      <td>Oulu</td>
      <td>Scandinavia</td>
      <td>90110</td>
      <td>Finland</td>
    </tr>
    <tr>
      <td>165</td>
      <td>10413</td>
      <td>LAMAI</td>
      <td>3</td>
      <td>2013-01-14</td>
      <td>2013-02-11</td>
      <td>2013-01-16</td>
      <td>2</td>
      <td>95.66</td>
      <td>La maison d'Asie</td>
      <td>1 rue Alsace-Lorraine</td>
      <td>Toulouse</td>
      <td>Western Europe</td>
      <td>31000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>166</td>
      <td>10414</td>
      <td>FAMIA</td>
      <td>2</td>
      <td>2013-01-14</td>
      <td>2013-02-11</td>
      <td>2013-01-17</td>
      <td>3</td>
      <td>21.48</td>
      <td>Familia Arquibaldo</td>
      <td>Rua Orós, 92</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05442-030</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>167</td>
      <td>10415</td>
      <td>HUNGC</td>
      <td>3</td>
      <td>2013-01-15</td>
      <td>2013-02-12</td>
      <td>2013-01-24</td>
      <td>1</td>
      <td>0.20</td>
      <td>Hungry Coyote Import Store</td>
      <td>City Center Plaza 516 Main St.</td>
      <td>Elgin</td>
      <td>North America</td>
      <td>97827</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>168</td>
      <td>10416</td>
      <td>WARTH</td>
      <td>8</td>
      <td>2013-01-16</td>
      <td>2013-02-13</td>
      <td>2013-01-27</td>
      <td>3</td>
      <td>22.72</td>
      <td>Wartian Herkku</td>
      <td>Torikatu 38</td>
      <td>Oulu</td>
      <td>Scandinavia</td>
      <td>90110</td>
      <td>Finland</td>
    </tr>
    <tr>
      <td>169</td>
      <td>10417</td>
      <td>SIMOB</td>
      <td>4</td>
      <td>2013-01-16</td>
      <td>2013-02-13</td>
      <td>2013-01-28</td>
      <td>3</td>
      <td>70.29</td>
      <td>Simons bistro</td>
      <td>Vinbæltet 34</td>
      <td>Kobenhavn</td>
      <td>Northern Europe</td>
      <td>1734</td>
      <td>Denmark</td>
    </tr>
    <tr>
      <td>170</td>
      <td>10418</td>
      <td>QUICK</td>
      <td>4</td>
      <td>2013-01-17</td>
      <td>2013-02-14</td>
      <td>2013-01-24</td>
      <td>1</td>
      <td>17.55</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>171</td>
      <td>10419</td>
      <td>RICSU</td>
      <td>4</td>
      <td>2013-01-20</td>
      <td>2013-02-17</td>
      <td>2013-01-30</td>
      <td>2</td>
      <td>137.35</td>
      <td>Richter Supermarkt</td>
      <td>Starenweg 5</td>
      <td>Genève</td>
      <td>Western Europe</td>
      <td>1204</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <td>172</td>
      <td>10420</td>
      <td>WELLI</td>
      <td>3</td>
      <td>2013-01-21</td>
      <td>2013-02-18</td>
      <td>2013-01-27</td>
      <td>1</td>
      <td>44.12</td>
      <td>Wellington Importadora</td>
      <td>Rua do Mercado, 12</td>
      <td>Resende</td>
      <td>South America</td>
      <td>08737-363</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>173</td>
      <td>10421</td>
      <td>QUEDE</td>
      <td>8</td>
      <td>2013-01-21</td>
      <td>2013-03-04</td>
      <td>2013-01-27</td>
      <td>1</td>
      <td>99.23</td>
      <td>Que Delícia</td>
      <td>Rua da Panificadora, 12</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>02389-673</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>174</td>
      <td>10422</td>
      <td>FRANS</td>
      <td>2</td>
      <td>2013-01-22</td>
      <td>2013-02-19</td>
      <td>2013-01-31</td>
      <td>1</td>
      <td>3.02</td>
      <td>Franchi S.p.A.</td>
      <td>Via Monte Bianco 34</td>
      <td>Torino</td>
      <td>Southern Europe</td>
      <td>10100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>175</td>
      <td>10423</td>
      <td>GOURL</td>
      <td>6</td>
      <td>2013-01-23</td>
      <td>2013-02-06</td>
      <td>2013-02-24</td>
      <td>3</td>
      <td>24.50</td>
      <td>Gourmet Lanchonetes</td>
      <td>Av. Brasil, 442</td>
      <td>Campinas</td>
      <td>South America</td>
      <td>04876-786</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>176</td>
      <td>10424</td>
      <td>MEREP</td>
      <td>7</td>
      <td>2013-01-23</td>
      <td>2013-02-20</td>
      <td>2013-01-27</td>
      <td>2</td>
      <td>370.61</td>
      <td>Mère Paillarde</td>
      <td>43 rue St. Laurent</td>
      <td>Montréal</td>
      <td>North America</td>
      <td>H1J 1C3</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>177</td>
      <td>10425</td>
      <td>LAMAI</td>
      <td>6</td>
      <td>2013-01-24</td>
      <td>2013-02-21</td>
      <td>2013-02-14</td>
      <td>2</td>
      <td>7.93</td>
      <td>La maison d'Asie</td>
      <td>1 rue Alsace-Lorraine</td>
      <td>Toulouse</td>
      <td>Western Europe</td>
      <td>31000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>178</td>
      <td>10426</td>
      <td>GALED</td>
      <td>4</td>
      <td>2013-01-27</td>
      <td>2013-02-24</td>
      <td>2013-02-06</td>
      <td>1</td>
      <td>18.69</td>
      <td>Galería del gastronómo</td>
      <td>Rambla de Cataluña, 23</td>
      <td>Barcelona</td>
      <td>Southern Europe</td>
      <td>8022</td>
      <td>Spain</td>
    </tr>
    <tr>
      <td>179</td>
      <td>10427</td>
      <td>PICCO</td>
      <td>4</td>
      <td>2013-01-27</td>
      <td>2013-02-24</td>
      <td>2013-03-03</td>
      <td>2</td>
      <td>31.29</td>
      <td>Piccolo und mehr</td>
      <td>Geislweg 14</td>
      <td>Salzburg</td>
      <td>Western Europe</td>
      <td>5020</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>180</td>
      <td>10428</td>
      <td>REGGC</td>
      <td>7</td>
      <td>2013-01-28</td>
      <td>2013-02-25</td>
      <td>2013-02-04</td>
      <td>1</td>
      <td>11.09</td>
      <td>Reggiani Caseifici</td>
      <td>Strada Provinciale 124</td>
      <td>Reggio Emilia</td>
      <td>Southern Europe</td>
      <td>42100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>181</td>
      <td>10429</td>
      <td>HUNGO</td>
      <td>3</td>
      <td>2013-01-29</td>
      <td>2013-03-12</td>
      <td>2013-02-07</td>
      <td>2</td>
      <td>56.63</td>
      <td>Hungry Owl All-Night Grocers</td>
      <td>8 Johnstown Road</td>
      <td>Cork</td>
      <td>British Isles</td>
      <td>None</td>
      <td>Ireland</td>
    </tr>
    <tr>
      <td>182</td>
      <td>10430</td>
      <td>ERNSH</td>
      <td>4</td>
      <td>2013-01-30</td>
      <td>2013-02-13</td>
      <td>2013-02-03</td>
      <td>1</td>
      <td>458.78</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>183</td>
      <td>10431</td>
      <td>BOTTM</td>
      <td>4</td>
      <td>2013-01-30</td>
      <td>2013-02-13</td>
      <td>2013-02-07</td>
      <td>2</td>
      <td>44.17</td>
      <td>Bottom-Dollar Markets</td>
      <td>23 Tsawassen Blvd.</td>
      <td>Tsawassen</td>
      <td>North America</td>
      <td>T2F 8M4</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>184</td>
      <td>10432</td>
      <td>SPLIR</td>
      <td>3</td>
      <td>2013-01-31</td>
      <td>2013-02-14</td>
      <td>2013-02-07</td>
      <td>2</td>
      <td>4.34</td>
      <td>Split Rail Beer &amp; Ale</td>
      <td>P.O. Box 555</td>
      <td>Lander</td>
      <td>North America</td>
      <td>82520</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>185</td>
      <td>10433</td>
      <td>PRINI</td>
      <td>3</td>
      <td>2013-02-03</td>
      <td>2013-03-03</td>
      <td>2013-03-04</td>
      <td>3</td>
      <td>73.83</td>
      <td>Princesa Isabel Vinhos</td>
      <td>Estrada da saúde n. 58</td>
      <td>Lisboa</td>
      <td>Southern Europe</td>
      <td>1756</td>
      <td>Portugal</td>
    </tr>
    <tr>
      <td>186</td>
      <td>10434</td>
      <td>FOLKO</td>
      <td>3</td>
      <td>2013-02-03</td>
      <td>2013-03-03</td>
      <td>2013-02-13</td>
      <td>2</td>
      <td>17.92</td>
      <td>Folk och fä HB</td>
      <td>Åkergatan 24</td>
      <td>Bräcke</td>
      <td>Northern Europe</td>
      <td>S-844 67</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>187</td>
      <td>10435</td>
      <td>CONSH</td>
      <td>8</td>
      <td>2013-02-04</td>
      <td>2013-03-18</td>
      <td>2013-02-07</td>
      <td>2</td>
      <td>9.21</td>
      <td>Consolidated Holdings</td>
      <td>Berkeley Gardens 12  Brewery</td>
      <td>London</td>
      <td>British Isles</td>
      <td>WX1 6LT</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>188</td>
      <td>10436</td>
      <td>BLONP</td>
      <td>3</td>
      <td>2013-02-05</td>
      <td>2013-03-05</td>
      <td>2013-02-11</td>
      <td>2</td>
      <td>156.66</td>
      <td>Blondel père et fils</td>
      <td>24, place Kléber</td>
      <td>Strasbourg</td>
      <td>Western Europe</td>
      <td>67000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>189</td>
      <td>10437</td>
      <td>WARTH</td>
      <td>8</td>
      <td>2013-02-05</td>
      <td>2013-03-05</td>
      <td>2013-02-12</td>
      <td>1</td>
      <td>19.97</td>
      <td>Wartian Herkku</td>
      <td>Torikatu 38</td>
      <td>Oulu</td>
      <td>Scandinavia</td>
      <td>90110</td>
      <td>Finland</td>
    </tr>
    <tr>
      <td>190</td>
      <td>10438</td>
      <td>TOMSP</td>
      <td>3</td>
      <td>2013-02-06</td>
      <td>2013-03-06</td>
      <td>2013-02-14</td>
      <td>2</td>
      <td>8.24</td>
      <td>Toms Spezialitäten</td>
      <td>Luisenstr. 48</td>
      <td>Münster</td>
      <td>Western Europe</td>
      <td>44087</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>191</td>
      <td>10439</td>
      <td>MEREP</td>
      <td>6</td>
      <td>2013-02-07</td>
      <td>2013-03-07</td>
      <td>2013-02-10</td>
      <td>3</td>
      <td>4.07</td>
      <td>Mère Paillarde</td>
      <td>43 rue St. Laurent</td>
      <td>Montréal</td>
      <td>North America</td>
      <td>H1J 1C3</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>192</td>
      <td>10440</td>
      <td>SAVEA</td>
      <td>4</td>
      <td>2013-02-10</td>
      <td>2013-03-10</td>
      <td>2013-02-28</td>
      <td>2</td>
      <td>86.53</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>193</td>
      <td>10441</td>
      <td>OLDWO</td>
      <td>3</td>
      <td>2013-02-10</td>
      <td>2013-03-24</td>
      <td>2013-03-14</td>
      <td>2</td>
      <td>73.02</td>
      <td>Old World Delicatessen</td>
      <td>2743 Bering St.</td>
      <td>Anchorage</td>
      <td>North America</td>
      <td>99508</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>194</td>
      <td>10442</td>
      <td>ERNSH</td>
      <td>3</td>
      <td>2013-02-11</td>
      <td>2013-03-11</td>
      <td>2013-02-18</td>
      <td>2</td>
      <td>47.94</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>195</td>
      <td>10443</td>
      <td>REGGC</td>
      <td>8</td>
      <td>2013-02-12</td>
      <td>2013-03-12</td>
      <td>2013-02-14</td>
      <td>1</td>
      <td>13.95</td>
      <td>Reggiani Caseifici</td>
      <td>Strada Provinciale 124</td>
      <td>Reggio Emilia</td>
      <td>Southern Europe</td>
      <td>42100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>196</td>
      <td>10444</td>
      <td>BERGS</td>
      <td>3</td>
      <td>2013-02-12</td>
      <td>2013-03-12</td>
      <td>2013-02-21</td>
      <td>3</td>
      <td>3.50</td>
      <td>Berglunds snabbköp</td>
      <td>Berguvsvägen  8</td>
      <td>Luleå</td>
      <td>Northern Europe</td>
      <td>S-958 22</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>197</td>
      <td>10445</td>
      <td>BERGS</td>
      <td>3</td>
      <td>2013-02-13</td>
      <td>2013-03-13</td>
      <td>2013-02-20</td>
      <td>1</td>
      <td>9.30</td>
      <td>Berglunds snabbköp</td>
      <td>Berguvsvägen  8</td>
      <td>Luleå</td>
      <td>Northern Europe</td>
      <td>S-958 22</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>198</td>
      <td>10446</td>
      <td>TOMSP</td>
      <td>6</td>
      <td>2013-02-14</td>
      <td>2013-03-14</td>
      <td>2013-02-19</td>
      <td>1</td>
      <td>14.68</td>
      <td>Toms Spezialitäten</td>
      <td>Luisenstr. 48</td>
      <td>Münster</td>
      <td>Western Europe</td>
      <td>44087</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>199</td>
      <td>10447</td>
      <td>RICAR</td>
      <td>4</td>
      <td>2013-02-14</td>
      <td>2013-03-14</td>
      <td>2013-03-07</td>
      <td>2</td>
      <td>68.66</td>
      <td>Ricardo Adocicados</td>
      <td>Av. Copacabana, 267</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>02389-890</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>200</td>
      <td>10448</td>
      <td>RANCH</td>
      <td>4</td>
      <td>2013-02-17</td>
      <td>2013-03-17</td>
      <td>2013-02-24</td>
      <td>2</td>
      <td>38.82</td>
      <td>Rancho grande</td>
      <td>Av. del Libertador 900</td>
      <td>Buenos Aires</td>
      <td>South America</td>
      <td>1010</td>
      <td>Argentina</td>
    </tr>
    <tr>
      <td>201</td>
      <td>10449</td>
      <td>BLONP</td>
      <td>3</td>
      <td>2013-02-18</td>
      <td>2013-03-18</td>
      <td>2013-02-27</td>
      <td>2</td>
      <td>53.30</td>
      <td>Blondel père et fils</td>
      <td>24, place Kléber</td>
      <td>Strasbourg</td>
      <td>Western Europe</td>
      <td>67000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>202</td>
      <td>10450</td>
      <td>VICTE</td>
      <td>8</td>
      <td>2013-02-19</td>
      <td>2013-03-19</td>
      <td>2013-03-11</td>
      <td>2</td>
      <td>7.23</td>
      <td>Victuailles en stock</td>
      <td>2, rue du Commerce</td>
      <td>Lyon</td>
      <td>Western Europe</td>
      <td>69004</td>
      <td>France</td>
    </tr>
    <tr>
      <td>203</td>
      <td>10451</td>
      <td>QUICK</td>
      <td>4</td>
      <td>2013-02-19</td>
      <td>2013-03-05</td>
      <td>2013-03-12</td>
      <td>3</td>
      <td>189.09</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>204</td>
      <td>10452</td>
      <td>SAVEA</td>
      <td>8</td>
      <td>2013-02-20</td>
      <td>2013-03-20</td>
      <td>2013-02-26</td>
      <td>1</td>
      <td>140.26</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>205</td>
      <td>10453</td>
      <td>AROUT</td>
      <td>1</td>
      <td>2013-02-21</td>
      <td>2013-03-21</td>
      <td>2013-02-26</td>
      <td>2</td>
      <td>25.36</td>
      <td>Around the Horn</td>
      <td>Brook Farm Stratford St. Mary</td>
      <td>Colchester</td>
      <td>British Isles</td>
      <td>CO7 6JX</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>206</td>
      <td>10454</td>
      <td>LAMAI</td>
      <td>4</td>
      <td>2013-02-21</td>
      <td>2013-03-21</td>
      <td>2013-02-25</td>
      <td>3</td>
      <td>2.74</td>
      <td>La maison d'Asie</td>
      <td>1 rue Alsace-Lorraine</td>
      <td>Toulouse</td>
      <td>Western Europe</td>
      <td>31000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>207</td>
      <td>10455</td>
      <td>WARTH</td>
      <td>8</td>
      <td>2013-02-24</td>
      <td>2013-04-07</td>
      <td>2013-03-03</td>
      <td>2</td>
      <td>180.45</td>
      <td>Wartian Herkku</td>
      <td>Torikatu 38</td>
      <td>Oulu</td>
      <td>Scandinavia</td>
      <td>90110</td>
      <td>Finland</td>
    </tr>
    <tr>
      <td>208</td>
      <td>10456</td>
      <td>KOENE</td>
      <td>8</td>
      <td>2013-02-25</td>
      <td>2013-04-08</td>
      <td>2013-02-28</td>
      <td>2</td>
      <td>8.12</td>
      <td>Königlich Essen</td>
      <td>Maubelstr. 90</td>
      <td>Brandenburg</td>
      <td>Western Europe</td>
      <td>14776</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>209</td>
      <td>10457</td>
      <td>KOENE</td>
      <td>2</td>
      <td>2013-02-25</td>
      <td>2013-03-25</td>
      <td>2013-03-03</td>
      <td>1</td>
      <td>11.57</td>
      <td>Königlich Essen</td>
      <td>Maubelstr. 90</td>
      <td>Brandenburg</td>
      <td>Western Europe</td>
      <td>14776</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>210</td>
      <td>10458</td>
      <td>SUPRD</td>
      <td>7</td>
      <td>2013-02-26</td>
      <td>2013-03-26</td>
      <td>2013-03-04</td>
      <td>3</td>
      <td>147.06</td>
      <td>Suprêmes délices</td>
      <td>Boulevard Tirou, 255</td>
      <td>Charleroi</td>
      <td>Western Europe</td>
      <td>B-6000</td>
      <td>Belgium</td>
    </tr>
    <tr>
      <td>211</td>
      <td>10459</td>
      <td>VICTE</td>
      <td>4</td>
      <td>2013-02-27</td>
      <td>2013-03-27</td>
      <td>2013-02-28</td>
      <td>2</td>
      <td>25.09</td>
      <td>Victuailles en stock</td>
      <td>2, rue du Commerce</td>
      <td>Lyon</td>
      <td>Western Europe</td>
      <td>69004</td>
      <td>France</td>
    </tr>
    <tr>
      <td>212</td>
      <td>10460</td>
      <td>FOLKO</td>
      <td>8</td>
      <td>2013-02-28</td>
      <td>2013-03-28</td>
      <td>2013-03-03</td>
      <td>1</td>
      <td>16.27</td>
      <td>Folk och fä HB</td>
      <td>Åkergatan 24</td>
      <td>Bräcke</td>
      <td>Northern Europe</td>
      <td>S-844 67</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>213</td>
      <td>10461</td>
      <td>LILAS</td>
      <td>1</td>
      <td>2013-02-28</td>
      <td>2013-03-28</td>
      <td>2013-03-05</td>
      <td>3</td>
      <td>148.61</td>
      <td>LILA-Supermercado</td>
      <td>Carrera 52 con Ave. Bolívar #65-98 Llano Largo</td>
      <td>Barquisimeto</td>
      <td>South America</td>
      <td>3508</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>214</td>
      <td>10462</td>
      <td>CONSH</td>
      <td>2</td>
      <td>2013-03-03</td>
      <td>2013-03-31</td>
      <td>2013-03-18</td>
      <td>1</td>
      <td>6.17</td>
      <td>Consolidated Holdings</td>
      <td>Berkeley Gardens 12  Brewery</td>
      <td>London</td>
      <td>British Isles</td>
      <td>WX1 6LT</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>215</td>
      <td>10463</td>
      <td>SUPRD</td>
      <td>5</td>
      <td>2013-03-04</td>
      <td>2013-04-01</td>
      <td>2013-03-06</td>
      <td>3</td>
      <td>14.78</td>
      <td>Suprêmes délices</td>
      <td>Boulevard Tirou, 255</td>
      <td>Charleroi</td>
      <td>Western Europe</td>
      <td>B-6000</td>
      <td>Belgium</td>
    </tr>
    <tr>
      <td>216</td>
      <td>10464</td>
      <td>FURIB</td>
      <td>4</td>
      <td>2013-03-04</td>
      <td>2013-04-01</td>
      <td>2013-03-14</td>
      <td>2</td>
      <td>89.00</td>
      <td>Furia Bacalhau e Frutos do Mar</td>
      <td>Jardim das rosas n. 32</td>
      <td>Lisboa</td>
      <td>Southern Europe</td>
      <td>1675</td>
      <td>Portugal</td>
    </tr>
    <tr>
      <td>217</td>
      <td>10465</td>
      <td>VAFFE</td>
      <td>1</td>
      <td>2013-03-05</td>
      <td>2013-04-02</td>
      <td>2013-03-14</td>
      <td>3</td>
      <td>145.04</td>
      <td>Vaffeljernet</td>
      <td>Smagsloget 45</td>
      <td>Århus</td>
      <td>Northern Europe</td>
      <td>8200</td>
      <td>Denmark</td>
    </tr>
    <tr>
      <td>218</td>
      <td>10466</td>
      <td>COMMI</td>
      <td>4</td>
      <td>2013-03-06</td>
      <td>2013-04-03</td>
      <td>2013-03-13</td>
      <td>1</td>
      <td>11.93</td>
      <td>Comércio Mineiro</td>
      <td>Av. dos Lusíadas, 23</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05432-043</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>219</td>
      <td>10467</td>
      <td>MAGAA</td>
      <td>8</td>
      <td>2013-03-06</td>
      <td>2013-04-03</td>
      <td>2013-03-11</td>
      <td>2</td>
      <td>4.93</td>
      <td>Magazzini Alimentari Riuniti</td>
      <td>Via Ludovico il Moro 22</td>
      <td>Bergamo</td>
      <td>Southern Europe</td>
      <td>24100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>220</td>
      <td>10468</td>
      <td>KOENE</td>
      <td>3</td>
      <td>2013-03-07</td>
      <td>2013-04-04</td>
      <td>2013-03-12</td>
      <td>3</td>
      <td>44.12</td>
      <td>Königlich Essen</td>
      <td>Maubelstr. 90</td>
      <td>Brandenburg</td>
      <td>Western Europe</td>
      <td>14776</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>221</td>
      <td>10469</td>
      <td>WHITC</td>
      <td>1</td>
      <td>2013-03-10</td>
      <td>2013-04-07</td>
      <td>2013-03-14</td>
      <td>1</td>
      <td>60.18</td>
      <td>White Clover Markets</td>
      <td>1029 - 12th Ave. S.</td>
      <td>Seattle</td>
      <td>North America</td>
      <td>98124</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>222</td>
      <td>10470</td>
      <td>BONAP</td>
      <td>4</td>
      <td>2013-03-11</td>
      <td>2013-04-08</td>
      <td>2013-03-14</td>
      <td>2</td>
      <td>64.56</td>
      <td>Bon app'</td>
      <td>12, rue des Bouchers</td>
      <td>Marseille</td>
      <td>Western Europe</td>
      <td>13008</td>
      <td>France</td>
    </tr>
    <tr>
      <td>223</td>
      <td>10471</td>
      <td>BSBEV</td>
      <td>2</td>
      <td>2013-03-11</td>
      <td>2013-04-08</td>
      <td>2013-03-18</td>
      <td>3</td>
      <td>45.59</td>
      <td>B's Beverages</td>
      <td>Fauntleroy Circus</td>
      <td>London</td>
      <td>British Isles</td>
      <td>EC2 5NT</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>224</td>
      <td>10472</td>
      <td>SEVES</td>
      <td>8</td>
      <td>2013-03-12</td>
      <td>2013-04-09</td>
      <td>2013-03-19</td>
      <td>1</td>
      <td>4.20</td>
      <td>Seven Seas Imports</td>
      <td>90 Wadhurst Rd.</td>
      <td>London</td>
      <td>British Isles</td>
      <td>OX15 4NB</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>225</td>
      <td>10473</td>
      <td>ISLAT</td>
      <td>1</td>
      <td>2013-03-13</td>
      <td>2013-03-27</td>
      <td>2013-03-21</td>
      <td>3</td>
      <td>16.37</td>
      <td>Island Trading</td>
      <td>Garden House Crowther Way</td>
      <td>Cowes</td>
      <td>British Isles</td>
      <td>PO31 7PJ</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>226</td>
      <td>10474</td>
      <td>PERIC</td>
      <td>5</td>
      <td>2013-03-13</td>
      <td>2013-04-10</td>
      <td>2013-03-21</td>
      <td>2</td>
      <td>83.49</td>
      <td>Pericles Comidas clásicas</td>
      <td>Calle Dr. Jorge Cash 321</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05033</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>227</td>
      <td>10475</td>
      <td>SUPRD</td>
      <td>9</td>
      <td>2013-03-14</td>
      <td>2013-04-11</td>
      <td>2013-04-04</td>
      <td>1</td>
      <td>68.52</td>
      <td>Suprêmes délices</td>
      <td>Boulevard Tirou, 255</td>
      <td>Charleroi</td>
      <td>Western Europe</td>
      <td>B-6000</td>
      <td>Belgium</td>
    </tr>
    <tr>
      <td>228</td>
      <td>10476</td>
      <td>HILAA</td>
      <td>8</td>
      <td>2013-03-17</td>
      <td>2013-04-14</td>
      <td>2013-03-24</td>
      <td>3</td>
      <td>4.41</td>
      <td>HILARION-Abastos</td>
      <td>Carrera 22 con Ave. Carlos Soublette #8-35</td>
      <td>San Cristóbal</td>
      <td>South America</td>
      <td>5022</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>229</td>
      <td>10477</td>
      <td>PRINI</td>
      <td>5</td>
      <td>2013-03-17</td>
      <td>2013-04-14</td>
      <td>2013-03-25</td>
      <td>2</td>
      <td>13.02</td>
      <td>Princesa Isabel Vinhos</td>
      <td>Estrada da saúde n. 58</td>
      <td>Lisboa</td>
      <td>Southern Europe</td>
      <td>1756</td>
      <td>Portugal</td>
    </tr>
    <tr>
      <td>230</td>
      <td>10478</td>
      <td>VICTE</td>
      <td>2</td>
      <td>2013-03-18</td>
      <td>2013-04-01</td>
      <td>2013-03-26</td>
      <td>3</td>
      <td>4.81</td>
      <td>Victuailles en stock</td>
      <td>2, rue du Commerce</td>
      <td>Lyon</td>
      <td>Western Europe</td>
      <td>69004</td>
      <td>France</td>
    </tr>
    <tr>
      <td>231</td>
      <td>10479</td>
      <td>RATTC</td>
      <td>3</td>
      <td>2013-03-19</td>
      <td>2013-04-16</td>
      <td>2013-03-21</td>
      <td>3</td>
      <td>708.95</td>
      <td>Rattlesnake Canyon Grocery</td>
      <td>2817 Milton Dr.</td>
      <td>Albuquerque</td>
      <td>North America</td>
      <td>87110</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>232</td>
      <td>10480</td>
      <td>FOLIG</td>
      <td>6</td>
      <td>2013-03-20</td>
      <td>2013-04-17</td>
      <td>2013-03-24</td>
      <td>2</td>
      <td>1.35</td>
      <td>Folies gourmandes</td>
      <td>184, chaussée de Tournai</td>
      <td>Lille</td>
      <td>Western Europe</td>
      <td>59000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>233</td>
      <td>10481</td>
      <td>RICAR</td>
      <td>8</td>
      <td>2013-03-20</td>
      <td>2013-04-17</td>
      <td>2013-03-25</td>
      <td>2</td>
      <td>64.33</td>
      <td>Ricardo Adocicados</td>
      <td>Av. Copacabana, 267</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>02389-890</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>234</td>
      <td>10482</td>
      <td>LAZYK</td>
      <td>1</td>
      <td>2013-03-21</td>
      <td>2013-04-18</td>
      <td>2013-04-10</td>
      <td>3</td>
      <td>7.48</td>
      <td>Lazy K Kountry Store</td>
      <td>12 Orchestra Terrace</td>
      <td>Walla Walla</td>
      <td>North America</td>
      <td>99362</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>235</td>
      <td>10483</td>
      <td>WHITC</td>
      <td>7</td>
      <td>2013-03-24</td>
      <td>2013-04-21</td>
      <td>2013-04-25</td>
      <td>2</td>
      <td>15.28</td>
      <td>White Clover Markets</td>
      <td>1029 - 12th Ave. S.</td>
      <td>Seattle</td>
      <td>North America</td>
      <td>98124</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>236</td>
      <td>10484</td>
      <td>BSBEV</td>
      <td>3</td>
      <td>2013-03-24</td>
      <td>2013-04-21</td>
      <td>2013-04-01</td>
      <td>3</td>
      <td>6.88</td>
      <td>B's Beverages</td>
      <td>Fauntleroy Circus</td>
      <td>London</td>
      <td>British Isles</td>
      <td>EC2 5NT</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>237</td>
      <td>10485</td>
      <td>LINOD</td>
      <td>4</td>
      <td>2013-03-25</td>
      <td>2013-04-08</td>
      <td>2013-03-31</td>
      <td>2</td>
      <td>64.45</td>
      <td>LINO-Delicateses</td>
      <td>Ave. 5 de Mayo Porlamar</td>
      <td>I. de Margarita</td>
      <td>South America</td>
      <td>4980</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>238</td>
      <td>10486</td>
      <td>HILAA</td>
      <td>1</td>
      <td>2013-03-26</td>
      <td>2013-04-23</td>
      <td>2013-04-02</td>
      <td>2</td>
      <td>30.53</td>
      <td>HILARION-Abastos</td>
      <td>Carrera 22 con Ave. Carlos Soublette #8-35</td>
      <td>San Cristóbal</td>
      <td>South America</td>
      <td>5022</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>239</td>
      <td>10487</td>
      <td>QUEE</td>
      <td>2</td>
      <td>2013-03-26</td>
      <td>2013-04-23</td>
      <td>2013-03-28</td>
      <td>2</td>
      <td>71.07</td>
      <td>Queen Cozinha</td>
      <td>Alameda dos Canàrios, 891</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05487-020</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>240</td>
      <td>10488</td>
      <td>FRANK</td>
      <td>8</td>
      <td>2013-03-27</td>
      <td>2013-04-24</td>
      <td>2013-04-02</td>
      <td>2</td>
      <td>4.93</td>
      <td>Frankenversand</td>
      <td>Berliner Platz 43</td>
      <td>München</td>
      <td>Western Europe</td>
      <td>80805</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>241</td>
      <td>10489</td>
      <td>PICCO</td>
      <td>6</td>
      <td>2013-03-28</td>
      <td>2013-04-25</td>
      <td>2013-04-09</td>
      <td>2</td>
      <td>5.29</td>
      <td>Piccolo und mehr</td>
      <td>Geislweg 14</td>
      <td>Salzburg</td>
      <td>Western Europe</td>
      <td>5020</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>242</td>
      <td>10490</td>
      <td>HILAA</td>
      <td>7</td>
      <td>2013-03-31</td>
      <td>2013-04-28</td>
      <td>2013-04-03</td>
      <td>2</td>
      <td>210.19</td>
      <td>HILARION-Abastos</td>
      <td>Carrera 22 con Ave. Carlos Soublette #8-35</td>
      <td>San Cristóbal</td>
      <td>South America</td>
      <td>5022</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>243</td>
      <td>10491</td>
      <td>FURIB</td>
      <td>8</td>
      <td>2013-03-31</td>
      <td>2013-04-28</td>
      <td>2013-04-08</td>
      <td>3</td>
      <td>16.96</td>
      <td>Furia Bacalhau e Frutos do Mar</td>
      <td>Jardim das rosas n. 32</td>
      <td>Lisboa</td>
      <td>Southern Europe</td>
      <td>1675</td>
      <td>Portugal</td>
    </tr>
    <tr>
      <td>244</td>
      <td>10492</td>
      <td>BOTTM</td>
      <td>3</td>
      <td>2013-04-01</td>
      <td>2013-04-29</td>
      <td>2013-04-11</td>
      <td>1</td>
      <td>62.89</td>
      <td>Bottom-Dollar Markets</td>
      <td>23 Tsawassen Blvd.</td>
      <td>Tsawassen</td>
      <td>North America</td>
      <td>T2F 8M4</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>245</td>
      <td>10493</td>
      <td>LAMAI</td>
      <td>4</td>
      <td>2013-04-02</td>
      <td>2013-04-30</td>
      <td>2013-04-10</td>
      <td>3</td>
      <td>10.64</td>
      <td>La maison d'Asie</td>
      <td>1 rue Alsace-Lorraine</td>
      <td>Toulouse</td>
      <td>Western Europe</td>
      <td>31000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>246</td>
      <td>10494</td>
      <td>COMMI</td>
      <td>4</td>
      <td>2013-04-02</td>
      <td>2013-04-30</td>
      <td>2013-04-09</td>
      <td>2</td>
      <td>65.99</td>
      <td>Comércio Mineiro</td>
      <td>Av. dos Lusíadas, 23</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05432-043</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>247</td>
      <td>10495</td>
      <td>LAUGB</td>
      <td>3</td>
      <td>2013-04-03</td>
      <td>2013-05-01</td>
      <td>2013-04-11</td>
      <td>3</td>
      <td>4.65</td>
      <td>Laughing Bacchus Wine Cellars</td>
      <td>2319 Elm St.</td>
      <td>Vancouver</td>
      <td>North America</td>
      <td>V3F 2K1</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>248</td>
      <td>10496</td>
      <td>TRADH</td>
      <td>7</td>
      <td>2013-04-04</td>
      <td>2013-05-02</td>
      <td>2013-04-07</td>
      <td>2</td>
      <td>46.77</td>
      <td>Tradiçao Hipermercados</td>
      <td>Av. Inês de Castro, 414</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05634-030</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>249</td>
      <td>10497</td>
      <td>LEHMS</td>
      <td>7</td>
      <td>2013-04-04</td>
      <td>2013-05-02</td>
      <td>2013-04-07</td>
      <td>1</td>
      <td>36.21</td>
      <td>Lehmanns Marktstand</td>
      <td>Magazinweg 7</td>
      <td>Frankfurt a.M.</td>
      <td>Western Europe</td>
      <td>60528</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>250</td>
      <td>10498</td>
      <td>HILAA</td>
      <td>8</td>
      <td>2013-04-07</td>
      <td>2013-05-05</td>
      <td>2013-04-11</td>
      <td>2</td>
      <td>29.75</td>
      <td>HILARION-Abastos</td>
      <td>Carrera 22 con Ave. Carlos Soublette #8-35</td>
      <td>San Cristóbal</td>
      <td>South America</td>
      <td>5022</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>251</td>
      <td>10499</td>
      <td>LILAS</td>
      <td>4</td>
      <td>2013-04-08</td>
      <td>2013-05-06</td>
      <td>2013-04-16</td>
      <td>2</td>
      <td>102.02</td>
      <td>LILA-Supermercado</td>
      <td>Carrera 52 con Ave. Bolívar #65-98 Llano Largo</td>
      <td>Barquisimeto</td>
      <td>South America</td>
      <td>3508</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>252</td>
      <td>10500</td>
      <td>LAMAI</td>
      <td>6</td>
      <td>2013-04-09</td>
      <td>2013-05-07</td>
      <td>2013-04-17</td>
      <td>1</td>
      <td>42.68</td>
      <td>La maison d'Asie</td>
      <td>1 rue Alsace-Lorraine</td>
      <td>Toulouse</td>
      <td>Western Europe</td>
      <td>31000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>253</td>
      <td>10501</td>
      <td>BLAUS</td>
      <td>9</td>
      <td>2013-04-09</td>
      <td>2013-05-07</td>
      <td>2013-04-16</td>
      <td>3</td>
      <td>8.85</td>
      <td>Blauer See Delikatessen</td>
      <td>Forsterstr. 57</td>
      <td>Mannheim</td>
      <td>Western Europe</td>
      <td>68306</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>254</td>
      <td>10502</td>
      <td>PERIC</td>
      <td>2</td>
      <td>2013-04-10</td>
      <td>2013-05-08</td>
      <td>2013-04-29</td>
      <td>1</td>
      <td>69.32</td>
      <td>Pericles Comidas clásicas</td>
      <td>Calle Dr. Jorge Cash 321</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05033</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>255</td>
      <td>10503</td>
      <td>HUNGO</td>
      <td>6</td>
      <td>2013-04-11</td>
      <td>2013-05-09</td>
      <td>2013-04-16</td>
      <td>2</td>
      <td>16.74</td>
      <td>Hungry Owl All-Night Grocers</td>
      <td>8 Johnstown Road</td>
      <td>Cork</td>
      <td>British Isles</td>
      <td>None</td>
      <td>Ireland</td>
    </tr>
    <tr>
      <td>256</td>
      <td>10504</td>
      <td>WHITC</td>
      <td>4</td>
      <td>2013-04-11</td>
      <td>2013-05-09</td>
      <td>2013-04-18</td>
      <td>3</td>
      <td>59.13</td>
      <td>White Clover Markets</td>
      <td>1029 - 12th Ave. S.</td>
      <td>Seattle</td>
      <td>North America</td>
      <td>98124</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>257</td>
      <td>10505</td>
      <td>MEREP</td>
      <td>3</td>
      <td>2013-04-14</td>
      <td>2013-05-12</td>
      <td>2013-04-21</td>
      <td>3</td>
      <td>7.13</td>
      <td>Mère Paillarde</td>
      <td>43 rue St. Laurent</td>
      <td>Montréal</td>
      <td>North America</td>
      <td>H1J 1C3</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>258</td>
      <td>10506</td>
      <td>KOENE</td>
      <td>9</td>
      <td>2013-04-15</td>
      <td>2013-05-13</td>
      <td>2013-05-02</td>
      <td>2</td>
      <td>21.19</td>
      <td>Königlich Essen</td>
      <td>Maubelstr. 90</td>
      <td>Brandenburg</td>
      <td>Western Europe</td>
      <td>14776</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>259</td>
      <td>10507</td>
      <td>ANTO</td>
      <td>7</td>
      <td>2013-04-15</td>
      <td>2013-05-13</td>
      <td>2013-04-22</td>
      <td>1</td>
      <td>47.45</td>
      <td>Antonio Moreno Taquería</td>
      <td>Mataderos  2312</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05023</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>260</td>
      <td>10508</td>
      <td>OTTIK</td>
      <td>1</td>
      <td>2013-04-16</td>
      <td>2013-05-14</td>
      <td>2013-05-13</td>
      <td>2</td>
      <td>4.99</td>
      <td>Ottilies Käseladen</td>
      <td>Mehrheimerstr. 369</td>
      <td>Köln</td>
      <td>Western Europe</td>
      <td>50739</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>261</td>
      <td>10509</td>
      <td>BLAUS</td>
      <td>4</td>
      <td>2013-04-17</td>
      <td>2013-05-15</td>
      <td>2013-04-29</td>
      <td>1</td>
      <td>0.15</td>
      <td>Blauer See Delikatessen</td>
      <td>Forsterstr. 57</td>
      <td>Mannheim</td>
      <td>Western Europe</td>
      <td>68306</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>262</td>
      <td>10510</td>
      <td>SAVEA</td>
      <td>6</td>
      <td>2013-04-18</td>
      <td>2013-05-16</td>
      <td>2013-04-28</td>
      <td>3</td>
      <td>367.63</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>263</td>
      <td>10511</td>
      <td>BONAP</td>
      <td>4</td>
      <td>2013-04-18</td>
      <td>2013-05-16</td>
      <td>2013-04-21</td>
      <td>3</td>
      <td>350.64</td>
      <td>Bon app'</td>
      <td>12, rue des Bouchers</td>
      <td>Marseille</td>
      <td>Western Europe</td>
      <td>13008</td>
      <td>France</td>
    </tr>
    <tr>
      <td>264</td>
      <td>10512</td>
      <td>FAMIA</td>
      <td>7</td>
      <td>2013-04-21</td>
      <td>2013-05-19</td>
      <td>2013-04-24</td>
      <td>2</td>
      <td>3.53</td>
      <td>Familia Arquibaldo</td>
      <td>Rua Orós, 92</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05442-030</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>265</td>
      <td>10513</td>
      <td>WANDK</td>
      <td>7</td>
      <td>2013-04-22</td>
      <td>2013-06-03</td>
      <td>2013-04-28</td>
      <td>1</td>
      <td>105.65</td>
      <td>Die Wandernde Kuh</td>
      <td>Adenauerallee 900</td>
      <td>Stuttgart</td>
      <td>Western Europe</td>
      <td>70563</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>266</td>
      <td>10514</td>
      <td>ERNSH</td>
      <td>3</td>
      <td>2013-04-22</td>
      <td>2013-05-20</td>
      <td>2013-05-16</td>
      <td>2</td>
      <td>789.95</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>267</td>
      <td>10515</td>
      <td>QUICK</td>
      <td>2</td>
      <td>2013-04-23</td>
      <td>2013-05-07</td>
      <td>2013-05-23</td>
      <td>1</td>
      <td>204.47</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>268</td>
      <td>10516</td>
      <td>HUNGO</td>
      <td>2</td>
      <td>2013-04-24</td>
      <td>2013-05-22</td>
      <td>2013-05-01</td>
      <td>3</td>
      <td>62.78</td>
      <td>Hungry Owl All-Night Grocers</td>
      <td>8 Johnstown Road</td>
      <td>Cork</td>
      <td>British Isles</td>
      <td>None</td>
      <td>Ireland</td>
    </tr>
    <tr>
      <td>269</td>
      <td>10517</td>
      <td>NORTS</td>
      <td>3</td>
      <td>2013-04-24</td>
      <td>2013-05-22</td>
      <td>2013-04-29</td>
      <td>3</td>
      <td>32.07</td>
      <td>North/South</td>
      <td>South House 300 Queensbridge</td>
      <td>London</td>
      <td>British Isles</td>
      <td>SW7 1RZ</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>270</td>
      <td>10518</td>
      <td>TORTU</td>
      <td>4</td>
      <td>2013-04-25</td>
      <td>2013-05-09</td>
      <td>2013-05-05</td>
      <td>2</td>
      <td>218.15</td>
      <td>Tortuga Restaurante</td>
      <td>Avda. Azteca 123</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05033</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>271</td>
      <td>10519</td>
      <td>CHOPS</td>
      <td>6</td>
      <td>2013-04-28</td>
      <td>2013-05-26</td>
      <td>2013-05-01</td>
      <td>3</td>
      <td>91.76</td>
      <td>Chop-suey Chinese</td>
      <td>Hauptstr. 31</td>
      <td>Bern</td>
      <td>Western Europe</td>
      <td>3012</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <td>272</td>
      <td>10520</td>
      <td>SANTG</td>
      <td>7</td>
      <td>2013-04-29</td>
      <td>2013-05-27</td>
      <td>2013-05-01</td>
      <td>1</td>
      <td>13.37</td>
      <td>Santé Gourmet</td>
      <td>Erling Skakkes gate 78</td>
      <td>Stavern</td>
      <td>Scandinavia</td>
      <td>4110</td>
      <td>Norway</td>
    </tr>
    <tr>
      <td>273</td>
      <td>10521</td>
      <td>CACTU</td>
      <td>8</td>
      <td>2013-04-29</td>
      <td>2013-05-27</td>
      <td>2013-05-02</td>
      <td>2</td>
      <td>17.22</td>
      <td>Cactus Comidas para llevar</td>
      <td>Cerrito 333</td>
      <td>Buenos Aires</td>
      <td>South America</td>
      <td>1010</td>
      <td>Argentina</td>
    </tr>
    <tr>
      <td>274</td>
      <td>10522</td>
      <td>LEHMS</td>
      <td>4</td>
      <td>2013-04-30</td>
      <td>2013-05-28</td>
      <td>2013-05-06</td>
      <td>1</td>
      <td>45.33</td>
      <td>Lehmanns Marktstand</td>
      <td>Magazinweg 7</td>
      <td>Frankfurt a.M.</td>
      <td>Western Europe</td>
      <td>60528</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>275</td>
      <td>10523</td>
      <td>SEVES</td>
      <td>7</td>
      <td>2013-05-01</td>
      <td>2013-05-29</td>
      <td>2013-05-30</td>
      <td>2</td>
      <td>77.63</td>
      <td>Seven Seas Imports</td>
      <td>90 Wadhurst Rd.</td>
      <td>London</td>
      <td>British Isles</td>
      <td>OX15 4NB</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>276</td>
      <td>10524</td>
      <td>BERGS</td>
      <td>1</td>
      <td>2013-05-01</td>
      <td>2013-05-29</td>
      <td>2013-05-07</td>
      <td>2</td>
      <td>244.79</td>
      <td>Berglunds snabbköp</td>
      <td>Berguvsvägen  8</td>
      <td>Luleå</td>
      <td>Northern Europe</td>
      <td>S-958 22</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>277</td>
      <td>10525</td>
      <td>BONAP</td>
      <td>1</td>
      <td>2013-05-02</td>
      <td>2013-05-30</td>
      <td>2013-05-23</td>
      <td>2</td>
      <td>11.06</td>
      <td>Bon app'</td>
      <td>12, rue des Bouchers</td>
      <td>Marseille</td>
      <td>Western Europe</td>
      <td>13008</td>
      <td>France</td>
    </tr>
    <tr>
      <td>278</td>
      <td>10526</td>
      <td>WARTH</td>
      <td>4</td>
      <td>2013-05-05</td>
      <td>2013-06-02</td>
      <td>2013-05-15</td>
      <td>2</td>
      <td>58.59</td>
      <td>Wartian Herkku</td>
      <td>Torikatu 38</td>
      <td>Oulu</td>
      <td>Scandinavia</td>
      <td>90110</td>
      <td>Finland</td>
    </tr>
    <tr>
      <td>279</td>
      <td>10527</td>
      <td>QUICK</td>
      <td>7</td>
      <td>2013-05-05</td>
      <td>2013-06-02</td>
      <td>2013-05-07</td>
      <td>1</td>
      <td>41.90</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>280</td>
      <td>10528</td>
      <td>GREAL</td>
      <td>6</td>
      <td>2013-05-06</td>
      <td>2013-05-20</td>
      <td>2013-05-09</td>
      <td>2</td>
      <td>3.35</td>
      <td>Great Lakes Food Market</td>
      <td>2732 Baker Blvd.</td>
      <td>Eugene</td>
      <td>North America</td>
      <td>97403</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>281</td>
      <td>10529</td>
      <td>MAISD</td>
      <td>5</td>
      <td>2013-05-07</td>
      <td>2013-06-04</td>
      <td>2013-05-09</td>
      <td>2</td>
      <td>66.69</td>
      <td>Maison Dewey</td>
      <td>Rue Joseph-Bens 532</td>
      <td>Bruxelles</td>
      <td>Western Europe</td>
      <td>B-1180</td>
      <td>Belgium</td>
    </tr>
    <tr>
      <td>282</td>
      <td>10530</td>
      <td>PICCO</td>
      <td>3</td>
      <td>2013-05-08</td>
      <td>2013-06-05</td>
      <td>2013-05-12</td>
      <td>2</td>
      <td>339.22</td>
      <td>Piccolo und mehr</td>
      <td>Geislweg 14</td>
      <td>Salzburg</td>
      <td>Western Europe</td>
      <td>5020</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>283</td>
      <td>10531</td>
      <td>OCEA</td>
      <td>7</td>
      <td>2013-05-08</td>
      <td>2013-06-05</td>
      <td>2013-05-19</td>
      <td>1</td>
      <td>8.12</td>
      <td>Océano Atlántico Ltda.</td>
      <td>Ing. Gustavo Moncada 8585 Piso 20-A</td>
      <td>Buenos Aires</td>
      <td>South America</td>
      <td>1010</td>
      <td>Argentina</td>
    </tr>
    <tr>
      <td>284</td>
      <td>10532</td>
      <td>EASTC</td>
      <td>7</td>
      <td>2013-05-09</td>
      <td>2013-06-06</td>
      <td>2013-05-12</td>
      <td>3</td>
      <td>74.46</td>
      <td>Eastern Connection</td>
      <td>35 King George</td>
      <td>London</td>
      <td>British Isles</td>
      <td>WX3 6FW</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>285</td>
      <td>10533</td>
      <td>FOLKO</td>
      <td>8</td>
      <td>2013-05-12</td>
      <td>2013-06-09</td>
      <td>2013-05-22</td>
      <td>1</td>
      <td>188.04</td>
      <td>Folk och fä HB</td>
      <td>Åkergatan 24</td>
      <td>Bräcke</td>
      <td>Northern Europe</td>
      <td>S-844 67</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>286</td>
      <td>10534</td>
      <td>LEHMS</td>
      <td>8</td>
      <td>2013-05-12</td>
      <td>2013-06-09</td>
      <td>2013-05-14</td>
      <td>2</td>
      <td>27.94</td>
      <td>Lehmanns Marktstand</td>
      <td>Magazinweg 7</td>
      <td>Frankfurt a.M.</td>
      <td>Western Europe</td>
      <td>60528</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>287</td>
      <td>10535</td>
      <td>ANTO</td>
      <td>4</td>
      <td>2013-05-13</td>
      <td>2013-06-10</td>
      <td>2013-05-21</td>
      <td>1</td>
      <td>15.64</td>
      <td>Antonio Moreno Taquería</td>
      <td>Mataderos  2312</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05023</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>288</td>
      <td>10536</td>
      <td>LEHMS</td>
      <td>3</td>
      <td>2013-05-14</td>
      <td>2013-06-11</td>
      <td>2013-06-06</td>
      <td>2</td>
      <td>58.88</td>
      <td>Lehmanns Marktstand</td>
      <td>Magazinweg 7</td>
      <td>Frankfurt a.M.</td>
      <td>Western Europe</td>
      <td>60528</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>289</td>
      <td>10537</td>
      <td>RICSU</td>
      <td>1</td>
      <td>2013-05-14</td>
      <td>2013-05-28</td>
      <td>2013-05-19</td>
      <td>1</td>
      <td>78.85</td>
      <td>Richter Supermarkt</td>
      <td>Starenweg 5</td>
      <td>Genève</td>
      <td>Western Europe</td>
      <td>1204</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <td>290</td>
      <td>10538</td>
      <td>BSBEV</td>
      <td>9</td>
      <td>2013-05-15</td>
      <td>2013-06-12</td>
      <td>2013-05-16</td>
      <td>3</td>
      <td>4.87</td>
      <td>B's Beverages</td>
      <td>Fauntleroy Circus</td>
      <td>London</td>
      <td>British Isles</td>
      <td>EC2 5NT</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>291</td>
      <td>10539</td>
      <td>BSBEV</td>
      <td>6</td>
      <td>2013-05-16</td>
      <td>2013-06-13</td>
      <td>2013-05-23</td>
      <td>3</td>
      <td>12.36</td>
      <td>B's Beverages</td>
      <td>Fauntleroy Circus</td>
      <td>London</td>
      <td>British Isles</td>
      <td>EC2 5NT</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>292</td>
      <td>10540</td>
      <td>QUICK</td>
      <td>3</td>
      <td>2013-05-19</td>
      <td>2013-06-16</td>
      <td>2013-06-13</td>
      <td>3</td>
      <td>1007.64</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>293</td>
      <td>10541</td>
      <td>HANAR</td>
      <td>2</td>
      <td>2013-05-19</td>
      <td>2013-06-16</td>
      <td>2013-05-29</td>
      <td>1</td>
      <td>68.65</td>
      <td>Hanari Carnes</td>
      <td>Rua do Paço, 67</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>05454-876</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>294</td>
      <td>10542</td>
      <td>KOENE</td>
      <td>1</td>
      <td>2013-05-20</td>
      <td>2013-06-17</td>
      <td>2013-05-26</td>
      <td>3</td>
      <td>10.95</td>
      <td>Königlich Essen</td>
      <td>Maubelstr. 90</td>
      <td>Brandenburg</td>
      <td>Western Europe</td>
      <td>14776</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>295</td>
      <td>10543</td>
      <td>LILAS</td>
      <td>8</td>
      <td>2013-05-21</td>
      <td>2013-06-18</td>
      <td>2013-05-23</td>
      <td>2</td>
      <td>48.17</td>
      <td>LILA-Supermercado</td>
      <td>Carrera 52 con Ave. Bolívar #65-98 Llano Largo</td>
      <td>Barquisimeto</td>
      <td>South America</td>
      <td>3508</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>296</td>
      <td>10544</td>
      <td>LONEP</td>
      <td>4</td>
      <td>2013-05-21</td>
      <td>2013-06-18</td>
      <td>2013-05-30</td>
      <td>1</td>
      <td>24.91</td>
      <td>Lonesome Pine Restaurant</td>
      <td>89 Chiaroscuro Rd.</td>
      <td>Portland</td>
      <td>North America</td>
      <td>97219</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>297</td>
      <td>10545</td>
      <td>LAZYK</td>
      <td>8</td>
      <td>2013-05-22</td>
      <td>2013-06-19</td>
      <td>2013-06-26</td>
      <td>2</td>
      <td>11.92</td>
      <td>Lazy K Kountry Store</td>
      <td>12 Orchestra Terrace</td>
      <td>Walla Walla</td>
      <td>North America</td>
      <td>99362</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>298</td>
      <td>10546</td>
      <td>VICTE</td>
      <td>1</td>
      <td>2013-05-23</td>
      <td>2013-06-20</td>
      <td>2013-05-27</td>
      <td>3</td>
      <td>194.72</td>
      <td>Victuailles en stock</td>
      <td>2, rue du Commerce</td>
      <td>Lyon</td>
      <td>Western Europe</td>
      <td>69004</td>
      <td>France</td>
    </tr>
    <tr>
      <td>299</td>
      <td>10547</td>
      <td>SEVES</td>
      <td>3</td>
      <td>2013-05-23</td>
      <td>2013-06-20</td>
      <td>2013-06-02</td>
      <td>2</td>
      <td>178.43</td>
      <td>Seven Seas Imports</td>
      <td>90 Wadhurst Rd.</td>
      <td>London</td>
      <td>British Isles</td>
      <td>OX15 4NB</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>300</td>
      <td>10548</td>
      <td>TOMSP</td>
      <td>3</td>
      <td>2013-05-26</td>
      <td>2013-06-23</td>
      <td>2013-06-02</td>
      <td>2</td>
      <td>1.43</td>
      <td>Toms Spezialitäten</td>
      <td>Luisenstr. 48</td>
      <td>Münster</td>
      <td>Western Europe</td>
      <td>44087</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>301</td>
      <td>10549</td>
      <td>QUICK</td>
      <td>5</td>
      <td>2013-05-27</td>
      <td>2013-06-10</td>
      <td>2013-05-30</td>
      <td>1</td>
      <td>171.24</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>302</td>
      <td>10550</td>
      <td>GODOS</td>
      <td>7</td>
      <td>2013-05-28</td>
      <td>2013-06-25</td>
      <td>2013-06-06</td>
      <td>3</td>
      <td>4.32</td>
      <td>Godos Cocina Típica</td>
      <td>C/ Romero, 33</td>
      <td>Sevilla</td>
      <td>Southern Europe</td>
      <td>41101</td>
      <td>Spain</td>
    </tr>
    <tr>
      <td>303</td>
      <td>10551</td>
      <td>FURIB</td>
      <td>4</td>
      <td>2013-05-28</td>
      <td>2013-07-09</td>
      <td>2013-06-06</td>
      <td>3</td>
      <td>72.95</td>
      <td>Furia Bacalhau e Frutos do Mar</td>
      <td>Jardim das rosas n. 32</td>
      <td>Lisboa</td>
      <td>Southern Europe</td>
      <td>1675</td>
      <td>Portugal</td>
    </tr>
    <tr>
      <td>304</td>
      <td>10552</td>
      <td>HILAA</td>
      <td>2</td>
      <td>2013-05-29</td>
      <td>2013-06-26</td>
      <td>2013-06-05</td>
      <td>1</td>
      <td>83.22</td>
      <td>HILARION-Abastos</td>
      <td>Carrera 22 con Ave. Carlos Soublette #8-35</td>
      <td>San Cristóbal</td>
      <td>South America</td>
      <td>5022</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>305</td>
      <td>10553</td>
      <td>WARTH</td>
      <td>2</td>
      <td>2013-05-30</td>
      <td>2013-06-27</td>
      <td>2013-06-03</td>
      <td>2</td>
      <td>149.49</td>
      <td>Wartian Herkku</td>
      <td>Torikatu 38</td>
      <td>Oulu</td>
      <td>Scandinavia</td>
      <td>90110</td>
      <td>Finland</td>
    </tr>
    <tr>
      <td>306</td>
      <td>10554</td>
      <td>OTTIK</td>
      <td>4</td>
      <td>2013-05-30</td>
      <td>2013-06-27</td>
      <td>2013-06-05</td>
      <td>3</td>
      <td>120.97</td>
      <td>Ottilies Käseladen</td>
      <td>Mehrheimerstr. 369</td>
      <td>Köln</td>
      <td>Western Europe</td>
      <td>50739</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>307</td>
      <td>10555</td>
      <td>SAVEA</td>
      <td>6</td>
      <td>2013-06-02</td>
      <td>2013-06-30</td>
      <td>2013-06-04</td>
      <td>3</td>
      <td>252.49</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>308</td>
      <td>10556</td>
      <td>SIMOB</td>
      <td>2</td>
      <td>2013-06-03</td>
      <td>2013-07-15</td>
      <td>2013-06-13</td>
      <td>1</td>
      <td>9.80</td>
      <td>Simons bistro</td>
      <td>Vinbæltet 34</td>
      <td>Kobenhavn</td>
      <td>Northern Europe</td>
      <td>1734</td>
      <td>Denmark</td>
    </tr>
    <tr>
      <td>309</td>
      <td>10557</td>
      <td>LEHMS</td>
      <td>9</td>
      <td>2013-06-03</td>
      <td>2013-06-17</td>
      <td>2013-06-06</td>
      <td>2</td>
      <td>96.72</td>
      <td>Lehmanns Marktstand</td>
      <td>Magazinweg 7</td>
      <td>Frankfurt a.M.</td>
      <td>Western Europe</td>
      <td>60528</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>310</td>
      <td>10558</td>
      <td>AROUT</td>
      <td>1</td>
      <td>2013-06-04</td>
      <td>2013-07-02</td>
      <td>2013-06-10</td>
      <td>2</td>
      <td>72.97</td>
      <td>Around the Horn</td>
      <td>Brook Farm Stratford St. Mary</td>
      <td>Colchester</td>
      <td>British Isles</td>
      <td>CO7 6JX</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>311</td>
      <td>10559</td>
      <td>BLONP</td>
      <td>6</td>
      <td>2013-06-05</td>
      <td>2013-07-03</td>
      <td>2013-06-13</td>
      <td>1</td>
      <td>8.05</td>
      <td>Blondel père et fils</td>
      <td>24, place Kléber</td>
      <td>Strasbourg</td>
      <td>Western Europe</td>
      <td>67000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>312</td>
      <td>10560</td>
      <td>FRANK</td>
      <td>8</td>
      <td>2013-06-06</td>
      <td>2013-07-04</td>
      <td>2013-06-09</td>
      <td>1</td>
      <td>36.65</td>
      <td>Frankenversand</td>
      <td>Berliner Platz 43</td>
      <td>München</td>
      <td>Western Europe</td>
      <td>80805</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>313</td>
      <td>10561</td>
      <td>FOLKO</td>
      <td>2</td>
      <td>2013-06-06</td>
      <td>2013-07-04</td>
      <td>2013-06-09</td>
      <td>2</td>
      <td>242.21</td>
      <td>Folk och fä HB</td>
      <td>Åkergatan 24</td>
      <td>Bräcke</td>
      <td>Northern Europe</td>
      <td>S-844 67</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>314</td>
      <td>10562</td>
      <td>REGGC</td>
      <td>1</td>
      <td>2013-06-09</td>
      <td>2013-07-07</td>
      <td>2013-06-12</td>
      <td>1</td>
      <td>22.95</td>
      <td>Reggiani Caseifici</td>
      <td>Strada Provinciale 124</td>
      <td>Reggio Emilia</td>
      <td>Southern Europe</td>
      <td>42100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>315</td>
      <td>10563</td>
      <td>RICAR</td>
      <td>2</td>
      <td>2013-06-10</td>
      <td>2013-07-22</td>
      <td>2013-06-24</td>
      <td>2</td>
      <td>60.43</td>
      <td>Ricardo Adocicados</td>
      <td>Av. Copacabana, 267</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>02389-890</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>316</td>
      <td>10564</td>
      <td>RATTC</td>
      <td>4</td>
      <td>2013-06-10</td>
      <td>2013-07-08</td>
      <td>2013-06-16</td>
      <td>3</td>
      <td>13.75</td>
      <td>Rattlesnake Canyon Grocery</td>
      <td>2817 Milton Dr.</td>
      <td>Albuquerque</td>
      <td>North America</td>
      <td>87110</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>317</td>
      <td>10565</td>
      <td>MEREP</td>
      <td>8</td>
      <td>2013-06-11</td>
      <td>2013-07-09</td>
      <td>2013-06-18</td>
      <td>2</td>
      <td>7.15</td>
      <td>Mère Paillarde</td>
      <td>43 rue St. Laurent</td>
      <td>Montréal</td>
      <td>North America</td>
      <td>H1J 1C3</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>318</td>
      <td>10566</td>
      <td>BLONP</td>
      <td>9</td>
      <td>2013-06-12</td>
      <td>2013-07-10</td>
      <td>2013-06-18</td>
      <td>1</td>
      <td>88.40</td>
      <td>Blondel père et fils</td>
      <td>24, place Kléber</td>
      <td>Strasbourg</td>
      <td>Western Europe</td>
      <td>67000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>319</td>
      <td>10567</td>
      <td>HUNGO</td>
      <td>1</td>
      <td>2013-06-12</td>
      <td>2013-07-10</td>
      <td>2013-06-17</td>
      <td>1</td>
      <td>33.97</td>
      <td>Hungry Owl All-Night Grocers</td>
      <td>8 Johnstown Road</td>
      <td>Cork</td>
      <td>British Isles</td>
      <td>None</td>
      <td>Ireland</td>
    </tr>
    <tr>
      <td>320</td>
      <td>10568</td>
      <td>GALED</td>
      <td>3</td>
      <td>2013-06-13</td>
      <td>2013-07-11</td>
      <td>2013-07-09</td>
      <td>3</td>
      <td>6.54</td>
      <td>Galería del gastronómo</td>
      <td>Rambla de Cataluña, 23</td>
      <td>Barcelona</td>
      <td>Southern Europe</td>
      <td>8022</td>
      <td>Spain</td>
    </tr>
    <tr>
      <td>321</td>
      <td>10569</td>
      <td>RATTC</td>
      <td>5</td>
      <td>2013-06-16</td>
      <td>2013-07-14</td>
      <td>2013-07-11</td>
      <td>1</td>
      <td>58.98</td>
      <td>Rattlesnake Canyon Grocery</td>
      <td>2817 Milton Dr.</td>
      <td>Albuquerque</td>
      <td>North America</td>
      <td>87110</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>322</td>
      <td>10570</td>
      <td>MEREP</td>
      <td>3</td>
      <td>2013-06-17</td>
      <td>2013-07-15</td>
      <td>2013-06-19</td>
      <td>3</td>
      <td>188.99</td>
      <td>Mère Paillarde</td>
      <td>43 rue St. Laurent</td>
      <td>Montréal</td>
      <td>North America</td>
      <td>H1J 1C3</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>323</td>
      <td>10571</td>
      <td>ERNSH</td>
      <td>8</td>
      <td>2013-06-17</td>
      <td>2013-07-29</td>
      <td>2013-07-04</td>
      <td>3</td>
      <td>26.06</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>324</td>
      <td>10572</td>
      <td>BERGS</td>
      <td>3</td>
      <td>2013-06-18</td>
      <td>2013-07-16</td>
      <td>2013-06-25</td>
      <td>2</td>
      <td>116.43</td>
      <td>Berglunds snabbköp</td>
      <td>Berguvsvägen  8</td>
      <td>Luleå</td>
      <td>Northern Europe</td>
      <td>S-958 22</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>325</td>
      <td>10573</td>
      <td>ANTO</td>
      <td>7</td>
      <td>2013-06-19</td>
      <td>2013-07-17</td>
      <td>2013-06-20</td>
      <td>3</td>
      <td>84.84</td>
      <td>Antonio Moreno Taquería</td>
      <td>Mataderos  2312</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05023</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>326</td>
      <td>10574</td>
      <td>TRAIH</td>
      <td>4</td>
      <td>2013-06-19</td>
      <td>2013-07-17</td>
      <td>2013-06-30</td>
      <td>2</td>
      <td>37.60</td>
      <td>Trail's Head Gourmet Provisioners</td>
      <td>722 DaVinci Blvd.</td>
      <td>Kirkland</td>
      <td>North America</td>
      <td>98034</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>327</td>
      <td>10575</td>
      <td>MORGK</td>
      <td>5</td>
      <td>2013-06-20</td>
      <td>2013-07-04</td>
      <td>2013-06-30</td>
      <td>1</td>
      <td>127.34</td>
      <td>Morgenstern Gesundkost</td>
      <td>Heerstr. 22</td>
      <td>Leipzig</td>
      <td>Western Europe</td>
      <td>04179</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>328</td>
      <td>10576</td>
      <td>TORTU</td>
      <td>3</td>
      <td>2013-06-23</td>
      <td>2013-07-07</td>
      <td>2013-06-30</td>
      <td>3</td>
      <td>18.56</td>
      <td>Tortuga Restaurante</td>
      <td>Avda. Azteca 123</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05033</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>329</td>
      <td>10577</td>
      <td>TRAIH</td>
      <td>9</td>
      <td>2013-06-23</td>
      <td>2013-08-04</td>
      <td>2013-06-30</td>
      <td>2</td>
      <td>25.41</td>
      <td>Trail's Head Gourmet Provisioners</td>
      <td>722 DaVinci Blvd.</td>
      <td>Kirkland</td>
      <td>North America</td>
      <td>98034</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>330</td>
      <td>10578</td>
      <td>BSBEV</td>
      <td>4</td>
      <td>2013-06-24</td>
      <td>2013-07-22</td>
      <td>2013-07-25</td>
      <td>3</td>
      <td>29.60</td>
      <td>B's Beverages</td>
      <td>Fauntleroy Circus</td>
      <td>London</td>
      <td>British Isles</td>
      <td>EC2 5NT</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>331</td>
      <td>10579</td>
      <td>LETSS</td>
      <td>1</td>
      <td>2013-06-25</td>
      <td>2013-07-23</td>
      <td>2013-07-04</td>
      <td>2</td>
      <td>13.73</td>
      <td>Let's Stop N Shop</td>
      <td>87 Polk St. Suite 5</td>
      <td>San Francisco</td>
      <td>North America</td>
      <td>94117</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>332</td>
      <td>10580</td>
      <td>OTTIK</td>
      <td>4</td>
      <td>2013-06-26</td>
      <td>2013-07-24</td>
      <td>2013-07-01</td>
      <td>3</td>
      <td>75.89</td>
      <td>Ottilies Käseladen</td>
      <td>Mehrheimerstr. 369</td>
      <td>Köln</td>
      <td>Western Europe</td>
      <td>50739</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>333</td>
      <td>10581</td>
      <td>FAMIA</td>
      <td>3</td>
      <td>2013-06-26</td>
      <td>2013-07-24</td>
      <td>2013-07-02</td>
      <td>1</td>
      <td>3.01</td>
      <td>Familia Arquibaldo</td>
      <td>Rua Orós, 92</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05442-030</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>334</td>
      <td>10582</td>
      <td>BLAUS</td>
      <td>3</td>
      <td>2013-06-27</td>
      <td>2013-07-25</td>
      <td>2013-07-14</td>
      <td>2</td>
      <td>27.71</td>
      <td>Blauer See Delikatessen</td>
      <td>Forsterstr. 57</td>
      <td>Mannheim</td>
      <td>Western Europe</td>
      <td>68306</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>335</td>
      <td>10583</td>
      <td>WARTH</td>
      <td>2</td>
      <td>2013-06-30</td>
      <td>2013-07-28</td>
      <td>2013-07-04</td>
      <td>2</td>
      <td>7.28</td>
      <td>Wartian Herkku</td>
      <td>Torikatu 38</td>
      <td>Oulu</td>
      <td>Scandinavia</td>
      <td>90110</td>
      <td>Finland</td>
    </tr>
    <tr>
      <td>336</td>
      <td>10584</td>
      <td>BLONP</td>
      <td>4</td>
      <td>2013-06-30</td>
      <td>2013-07-28</td>
      <td>2013-07-04</td>
      <td>1</td>
      <td>59.14</td>
      <td>Blondel père et fils</td>
      <td>24, place Kléber</td>
      <td>Strasbourg</td>
      <td>Western Europe</td>
      <td>67000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>337</td>
      <td>10585</td>
      <td>WELLI</td>
      <td>7</td>
      <td>2013-07-01</td>
      <td>2013-07-29</td>
      <td>2013-07-10</td>
      <td>1</td>
      <td>13.41</td>
      <td>Wellington Importadora</td>
      <td>Rua do Mercado, 12</td>
      <td>Resende</td>
      <td>South America</td>
      <td>08737-363</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>338</td>
      <td>10586</td>
      <td>REGGC</td>
      <td>9</td>
      <td>2013-07-02</td>
      <td>2013-07-30</td>
      <td>2013-07-09</td>
      <td>1</td>
      <td>0.48</td>
      <td>Reggiani Caseifici</td>
      <td>Strada Provinciale 124</td>
      <td>Reggio Emilia</td>
      <td>Southern Europe</td>
      <td>42100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>339</td>
      <td>10587</td>
      <td>QUEDE</td>
      <td>1</td>
      <td>2013-07-02</td>
      <td>2013-07-30</td>
      <td>2013-07-09</td>
      <td>1</td>
      <td>62.52</td>
      <td>Que Delícia</td>
      <td>Rua da Panificadora, 12</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>02389-673</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>340</td>
      <td>10588</td>
      <td>QUICK</td>
      <td>2</td>
      <td>2013-07-03</td>
      <td>2013-07-31</td>
      <td>2013-07-10</td>
      <td>3</td>
      <td>194.67</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>341</td>
      <td>10589</td>
      <td>GREAL</td>
      <td>8</td>
      <td>2013-07-04</td>
      <td>2013-08-01</td>
      <td>2013-07-14</td>
      <td>2</td>
      <td>4.42</td>
      <td>Great Lakes Food Market</td>
      <td>2732 Baker Blvd.</td>
      <td>Eugene</td>
      <td>North America</td>
      <td>97403</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>342</td>
      <td>10590</td>
      <td>MEREP</td>
      <td>4</td>
      <td>2013-07-07</td>
      <td>2013-08-04</td>
      <td>2013-07-14</td>
      <td>3</td>
      <td>44.77</td>
      <td>Mère Paillarde</td>
      <td>43 rue St. Laurent</td>
      <td>Montréal</td>
      <td>North America</td>
      <td>H1J 1C3</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>343</td>
      <td>10591</td>
      <td>VAFFE</td>
      <td>1</td>
      <td>2013-07-07</td>
      <td>2013-07-21</td>
      <td>2013-07-16</td>
      <td>1</td>
      <td>55.92</td>
      <td>Vaffeljernet</td>
      <td>Smagsloget 45</td>
      <td>Århus</td>
      <td>Northern Europe</td>
      <td>8200</td>
      <td>Denmark</td>
    </tr>
    <tr>
      <td>344</td>
      <td>10592</td>
      <td>LEHMS</td>
      <td>3</td>
      <td>2013-07-08</td>
      <td>2013-08-05</td>
      <td>2013-07-16</td>
      <td>1</td>
      <td>32.10</td>
      <td>Lehmanns Marktstand</td>
      <td>Magazinweg 7</td>
      <td>Frankfurt a.M.</td>
      <td>Western Europe</td>
      <td>60528</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>345</td>
      <td>10593</td>
      <td>LEHMS</td>
      <td>7</td>
      <td>2013-07-09</td>
      <td>2013-08-06</td>
      <td>2013-08-13</td>
      <td>2</td>
      <td>174.20</td>
      <td>Lehmanns Marktstand</td>
      <td>Magazinweg 7</td>
      <td>Frankfurt a.M.</td>
      <td>Western Europe</td>
      <td>60528</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>346</td>
      <td>10594</td>
      <td>OLDWO</td>
      <td>3</td>
      <td>2013-07-09</td>
      <td>2013-08-06</td>
      <td>2013-07-16</td>
      <td>2</td>
      <td>5.24</td>
      <td>Old World Delicatessen</td>
      <td>2743 Bering St.</td>
      <td>Anchorage</td>
      <td>North America</td>
      <td>99508</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>347</td>
      <td>10595</td>
      <td>ERNSH</td>
      <td>2</td>
      <td>2013-07-10</td>
      <td>2013-08-07</td>
      <td>2013-07-14</td>
      <td>1</td>
      <td>96.78</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>348</td>
      <td>10596</td>
      <td>WHITC</td>
      <td>8</td>
      <td>2013-07-11</td>
      <td>2013-08-08</td>
      <td>2013-08-12</td>
      <td>1</td>
      <td>16.34</td>
      <td>White Clover Markets</td>
      <td>1029 - 12th Ave. S.</td>
      <td>Seattle</td>
      <td>North America</td>
      <td>98124</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>349</td>
      <td>10597</td>
      <td>PICCO</td>
      <td>7</td>
      <td>2013-07-11</td>
      <td>2013-08-08</td>
      <td>2013-07-18</td>
      <td>3</td>
      <td>35.12</td>
      <td>Piccolo und mehr</td>
      <td>Geislweg 14</td>
      <td>Salzburg</td>
      <td>Western Europe</td>
      <td>5020</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>350</td>
      <td>10598</td>
      <td>RATTC</td>
      <td>1</td>
      <td>2013-07-14</td>
      <td>2013-08-11</td>
      <td>2013-07-18</td>
      <td>3</td>
      <td>44.42</td>
      <td>Rattlesnake Canyon Grocery</td>
      <td>2817 Milton Dr.</td>
      <td>Albuquerque</td>
      <td>North America</td>
      <td>87110</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>351</td>
      <td>10599</td>
      <td>BSBEV</td>
      <td>6</td>
      <td>2013-07-15</td>
      <td>2013-08-26</td>
      <td>2013-07-21</td>
      <td>3</td>
      <td>29.98</td>
      <td>B's Beverages</td>
      <td>Fauntleroy Circus</td>
      <td>London</td>
      <td>British Isles</td>
      <td>EC2 5NT</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>352</td>
      <td>10600</td>
      <td>HUNGC</td>
      <td>4</td>
      <td>2013-07-16</td>
      <td>2013-08-13</td>
      <td>2013-07-21</td>
      <td>1</td>
      <td>45.13</td>
      <td>Hungry Coyote Import Store</td>
      <td>City Center Plaza 516 Main St.</td>
      <td>Elgin</td>
      <td>North America</td>
      <td>97827</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>353</td>
      <td>10601</td>
      <td>HILAA</td>
      <td>7</td>
      <td>2013-07-16</td>
      <td>2013-08-27</td>
      <td>2013-07-22</td>
      <td>1</td>
      <td>58.30</td>
      <td>HILARION-Abastos</td>
      <td>Carrera 22 con Ave. Carlos Soublette #8-35</td>
      <td>San Cristóbal</td>
      <td>South America</td>
      <td>5022</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>354</td>
      <td>10602</td>
      <td>VAFFE</td>
      <td>8</td>
      <td>2013-07-17</td>
      <td>2013-08-14</td>
      <td>2013-07-22</td>
      <td>2</td>
      <td>2.92</td>
      <td>Vaffeljernet</td>
      <td>Smagsloget 45</td>
      <td>Århus</td>
      <td>Northern Europe</td>
      <td>8200</td>
      <td>Denmark</td>
    </tr>
    <tr>
      <td>355</td>
      <td>10603</td>
      <td>SAVEA</td>
      <td>8</td>
      <td>2013-07-18</td>
      <td>2013-08-15</td>
      <td>2013-08-08</td>
      <td>2</td>
      <td>48.77</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>356</td>
      <td>10604</td>
      <td>FURIB</td>
      <td>1</td>
      <td>2013-07-18</td>
      <td>2013-08-15</td>
      <td>2013-07-29</td>
      <td>1</td>
      <td>7.46</td>
      <td>Furia Bacalhau e Frutos do Mar</td>
      <td>Jardim das rosas n. 32</td>
      <td>Lisboa</td>
      <td>Southern Europe</td>
      <td>1675</td>
      <td>Portugal</td>
    </tr>
    <tr>
      <td>357</td>
      <td>10605</td>
      <td>MEREP</td>
      <td>1</td>
      <td>2013-07-21</td>
      <td>2013-08-18</td>
      <td>2013-07-29</td>
      <td>2</td>
      <td>379.13</td>
      <td>Mère Paillarde</td>
      <td>43 rue St. Laurent</td>
      <td>Montréal</td>
      <td>North America</td>
      <td>H1J 1C3</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>358</td>
      <td>10606</td>
      <td>TRADH</td>
      <td>4</td>
      <td>2013-07-22</td>
      <td>2013-08-19</td>
      <td>2013-07-31</td>
      <td>3</td>
      <td>79.40</td>
      <td>Tradiçao Hipermercados</td>
      <td>Av. Inês de Castro, 414</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05634-030</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>359</td>
      <td>10607</td>
      <td>SAVEA</td>
      <td>5</td>
      <td>2013-07-22</td>
      <td>2013-08-19</td>
      <td>2013-07-25</td>
      <td>1</td>
      <td>200.24</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>360</td>
      <td>10608</td>
      <td>TOMSP</td>
      <td>4</td>
      <td>2013-07-23</td>
      <td>2013-08-20</td>
      <td>2013-08-01</td>
      <td>2</td>
      <td>27.79</td>
      <td>Toms Spezialitäten</td>
      <td>Luisenstr. 48</td>
      <td>Münster</td>
      <td>Western Europe</td>
      <td>44087</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>361</td>
      <td>10609</td>
      <td>DUMO</td>
      <td>7</td>
      <td>2013-07-24</td>
      <td>2013-08-21</td>
      <td>2013-07-30</td>
      <td>2</td>
      <td>1.85</td>
      <td>Du monde entier</td>
      <td>67, rue des Cinquante Otages</td>
      <td>Nantes</td>
      <td>Western Europe</td>
      <td>44000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>362</td>
      <td>10610</td>
      <td>LAMAI</td>
      <td>8</td>
      <td>2013-07-25</td>
      <td>2013-08-22</td>
      <td>2013-08-06</td>
      <td>1</td>
      <td>26.78</td>
      <td>La maison d'Asie</td>
      <td>1 rue Alsace-Lorraine</td>
      <td>Toulouse</td>
      <td>Western Europe</td>
      <td>31000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>363</td>
      <td>10611</td>
      <td>WOLZA</td>
      <td>6</td>
      <td>2013-07-25</td>
      <td>2013-08-22</td>
      <td>2013-08-01</td>
      <td>2</td>
      <td>80.65</td>
      <td>Wolski Zajazd</td>
      <td>ul. Filtrowa 68</td>
      <td>Warszawa</td>
      <td>Eastern Europe</td>
      <td>01-012</td>
      <td>Poland</td>
    </tr>
    <tr>
      <td>364</td>
      <td>10612</td>
      <td>SAVEA</td>
      <td>1</td>
      <td>2013-07-28</td>
      <td>2013-08-25</td>
      <td>2013-08-01</td>
      <td>2</td>
      <td>544.08</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>365</td>
      <td>10613</td>
      <td>HILAA</td>
      <td>4</td>
      <td>2013-07-29</td>
      <td>2013-08-26</td>
      <td>2013-08-01</td>
      <td>2</td>
      <td>8.11</td>
      <td>HILARION-Abastos</td>
      <td>Carrera 22 con Ave. Carlos Soublette #8-35</td>
      <td>San Cristóbal</td>
      <td>South America</td>
      <td>5022</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>366</td>
      <td>10614</td>
      <td>BLAUS</td>
      <td>8</td>
      <td>2013-07-29</td>
      <td>2013-08-26</td>
      <td>2013-08-01</td>
      <td>3</td>
      <td>1.93</td>
      <td>Blauer See Delikatessen</td>
      <td>Forsterstr. 57</td>
      <td>Mannheim</td>
      <td>Western Europe</td>
      <td>68306</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>367</td>
      <td>10615</td>
      <td>WILMK</td>
      <td>2</td>
      <td>2013-07-30</td>
      <td>2013-08-27</td>
      <td>2013-08-06</td>
      <td>3</td>
      <td>0.75</td>
      <td>Wilman Kala</td>
      <td>Keskuskatu 45</td>
      <td>Helsinki</td>
      <td>Scandinavia</td>
      <td>21240</td>
      <td>Finland</td>
    </tr>
    <tr>
      <td>368</td>
      <td>10616</td>
      <td>GREAL</td>
      <td>1</td>
      <td>2013-07-31</td>
      <td>2013-08-28</td>
      <td>2013-08-05</td>
      <td>2</td>
      <td>116.53</td>
      <td>Great Lakes Food Market</td>
      <td>2732 Baker Blvd.</td>
      <td>Eugene</td>
      <td>North America</td>
      <td>97403</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>369</td>
      <td>10617</td>
      <td>GREAL</td>
      <td>4</td>
      <td>2013-07-31</td>
      <td>2013-08-28</td>
      <td>2013-08-04</td>
      <td>2</td>
      <td>18.53</td>
      <td>Great Lakes Food Market</td>
      <td>2732 Baker Blvd.</td>
      <td>Eugene</td>
      <td>North America</td>
      <td>97403</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>370</td>
      <td>10618</td>
      <td>MEREP</td>
      <td>1</td>
      <td>2013-08-01</td>
      <td>2013-09-12</td>
      <td>2013-08-08</td>
      <td>1</td>
      <td>154.68</td>
      <td>Mère Paillarde</td>
      <td>43 rue St. Laurent</td>
      <td>Montréal</td>
      <td>North America</td>
      <td>H1J 1C3</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>371</td>
      <td>10619</td>
      <td>MEREP</td>
      <td>3</td>
      <td>2013-08-04</td>
      <td>2013-09-01</td>
      <td>2013-08-07</td>
      <td>3</td>
      <td>91.05</td>
      <td>Mère Paillarde</td>
      <td>43 rue St. Laurent</td>
      <td>Montréal</td>
      <td>North America</td>
      <td>H1J 1C3</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>372</td>
      <td>10620</td>
      <td>LAUGB</td>
      <td>2</td>
      <td>2013-08-05</td>
      <td>2013-09-02</td>
      <td>2013-08-14</td>
      <td>3</td>
      <td>0.94</td>
      <td>Laughing Bacchus Wine Cellars</td>
      <td>2319 Elm St.</td>
      <td>Vancouver</td>
      <td>North America</td>
      <td>V3F 2K1</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>373</td>
      <td>10621</td>
      <td>ISLAT</td>
      <td>4</td>
      <td>2013-08-05</td>
      <td>2013-09-02</td>
      <td>2013-08-11</td>
      <td>2</td>
      <td>23.73</td>
      <td>Island Trading</td>
      <td>Garden House Crowther Way</td>
      <td>Cowes</td>
      <td>British Isles</td>
      <td>PO31 7PJ</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>374</td>
      <td>10622</td>
      <td>RICAR</td>
      <td>4</td>
      <td>2013-08-06</td>
      <td>2013-09-03</td>
      <td>2013-08-11</td>
      <td>3</td>
      <td>50.97</td>
      <td>Ricardo Adocicados</td>
      <td>Av. Copacabana, 267</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>02389-890</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>375</td>
      <td>10623</td>
      <td>FRANK</td>
      <td>8</td>
      <td>2013-08-07</td>
      <td>2013-09-04</td>
      <td>2013-08-12</td>
      <td>2</td>
      <td>97.18</td>
      <td>Frankenversand</td>
      <td>Berliner Platz 43</td>
      <td>München</td>
      <td>Western Europe</td>
      <td>80805</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>376</td>
      <td>10624</td>
      <td>THECR</td>
      <td>4</td>
      <td>2013-08-07</td>
      <td>2013-09-04</td>
      <td>2013-08-19</td>
      <td>2</td>
      <td>94.80</td>
      <td>The Cracker Box</td>
      <td>55 Grizzly Peak Rd.</td>
      <td>Butte</td>
      <td>North America</td>
      <td>59801</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>377</td>
      <td>10625</td>
      <td>ANATR</td>
      <td>3</td>
      <td>2013-08-08</td>
      <td>2013-09-05</td>
      <td>2013-08-14</td>
      <td>1</td>
      <td>43.90</td>
      <td>Ana Trujillo Emparedados y helados</td>
      <td>Avda. de la Constitución 2222</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05021</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>378</td>
      <td>10626</td>
      <td>BERGS</td>
      <td>1</td>
      <td>2013-08-11</td>
      <td>2013-09-08</td>
      <td>2013-08-20</td>
      <td>2</td>
      <td>138.69</td>
      <td>Berglunds snabbköp</td>
      <td>Berguvsvägen  8</td>
      <td>Luleå</td>
      <td>Northern Europe</td>
      <td>S-958 22</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>379</td>
      <td>10627</td>
      <td>SAVEA</td>
      <td>8</td>
      <td>2013-08-11</td>
      <td>2013-09-22</td>
      <td>2013-08-21</td>
      <td>3</td>
      <td>107.46</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>380</td>
      <td>10628</td>
      <td>BLONP</td>
      <td>4</td>
      <td>2013-08-12</td>
      <td>2013-09-09</td>
      <td>2013-08-20</td>
      <td>3</td>
      <td>30.36</td>
      <td>Blondel père et fils</td>
      <td>24, place Kléber</td>
      <td>Strasbourg</td>
      <td>Western Europe</td>
      <td>67000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>381</td>
      <td>10629</td>
      <td>GODOS</td>
      <td>4</td>
      <td>2013-08-12</td>
      <td>2013-09-09</td>
      <td>2013-08-20</td>
      <td>3</td>
      <td>85.46</td>
      <td>Godos Cocina Típica</td>
      <td>C/ Romero, 33</td>
      <td>Sevilla</td>
      <td>Southern Europe</td>
      <td>41101</td>
      <td>Spain</td>
    </tr>
    <tr>
      <td>382</td>
      <td>10630</td>
      <td>KOENE</td>
      <td>1</td>
      <td>2013-08-13</td>
      <td>2013-09-10</td>
      <td>2013-08-19</td>
      <td>2</td>
      <td>32.35</td>
      <td>Königlich Essen</td>
      <td>Maubelstr. 90</td>
      <td>Brandenburg</td>
      <td>Western Europe</td>
      <td>14776</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>383</td>
      <td>10631</td>
      <td>LAMAI</td>
      <td>8</td>
      <td>2013-08-14</td>
      <td>2013-09-11</td>
      <td>2013-08-15</td>
      <td>1</td>
      <td>0.87</td>
      <td>La maison d'Asie</td>
      <td>1 rue Alsace-Lorraine</td>
      <td>Toulouse</td>
      <td>Western Europe</td>
      <td>31000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>384</td>
      <td>10632</td>
      <td>WANDK</td>
      <td>8</td>
      <td>2013-08-14</td>
      <td>2013-09-11</td>
      <td>2013-08-19</td>
      <td>1</td>
      <td>41.38</td>
      <td>Die Wandernde Kuh</td>
      <td>Adenauerallee 900</td>
      <td>Stuttgart</td>
      <td>Western Europe</td>
      <td>70563</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>385</td>
      <td>10633</td>
      <td>ERNSH</td>
      <td>7</td>
      <td>2013-08-15</td>
      <td>2013-09-12</td>
      <td>2013-08-18</td>
      <td>3</td>
      <td>477.90</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>386</td>
      <td>10634</td>
      <td>FOLIG</td>
      <td>4</td>
      <td>2013-08-15</td>
      <td>2013-09-12</td>
      <td>2013-08-21</td>
      <td>3</td>
      <td>487.38</td>
      <td>Folies gourmandes</td>
      <td>184, chaussée de Tournai</td>
      <td>Lille</td>
      <td>Western Europe</td>
      <td>59000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>387</td>
      <td>10635</td>
      <td>MAGAA</td>
      <td>8</td>
      <td>2013-08-18</td>
      <td>2013-09-15</td>
      <td>2013-08-21</td>
      <td>3</td>
      <td>47.46</td>
      <td>Magazzini Alimentari Riuniti</td>
      <td>Via Ludovico il Moro 22</td>
      <td>Bergamo</td>
      <td>Southern Europe</td>
      <td>24100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>388</td>
      <td>10636</td>
      <td>WARTH</td>
      <td>4</td>
      <td>2013-08-19</td>
      <td>2013-09-16</td>
      <td>2013-08-26</td>
      <td>1</td>
      <td>1.15</td>
      <td>Wartian Herkku</td>
      <td>Torikatu 38</td>
      <td>Oulu</td>
      <td>Scandinavia</td>
      <td>90110</td>
      <td>Finland</td>
    </tr>
    <tr>
      <td>389</td>
      <td>10637</td>
      <td>QUEE</td>
      <td>6</td>
      <td>2013-08-19</td>
      <td>2013-09-16</td>
      <td>2013-08-26</td>
      <td>1</td>
      <td>201.29</td>
      <td>Queen Cozinha</td>
      <td>Alameda dos Canàrios, 891</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05487-020</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>390</td>
      <td>10638</td>
      <td>LINOD</td>
      <td>3</td>
      <td>2013-08-20</td>
      <td>2013-09-17</td>
      <td>2013-09-01</td>
      <td>1</td>
      <td>158.44</td>
      <td>LINO-Delicateses</td>
      <td>Ave. 5 de Mayo Porlamar</td>
      <td>I. de Margarita</td>
      <td>South America</td>
      <td>4980</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>391</td>
      <td>10639</td>
      <td>SANTG</td>
      <td>7</td>
      <td>2013-08-20</td>
      <td>2013-09-17</td>
      <td>2013-08-27</td>
      <td>3</td>
      <td>38.64</td>
      <td>Santé Gourmet</td>
      <td>Erling Skakkes gate 78</td>
      <td>Stavern</td>
      <td>Scandinavia</td>
      <td>4110</td>
      <td>Norway</td>
    </tr>
    <tr>
      <td>392</td>
      <td>10640</td>
      <td>WANDK</td>
      <td>4</td>
      <td>2013-08-21</td>
      <td>2013-09-18</td>
      <td>2013-08-28</td>
      <td>1</td>
      <td>23.55</td>
      <td>Die Wandernde Kuh</td>
      <td>Adenauerallee 900</td>
      <td>Stuttgart</td>
      <td>Western Europe</td>
      <td>70563</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>393</td>
      <td>10641</td>
      <td>HILAA</td>
      <td>4</td>
      <td>2013-08-22</td>
      <td>2013-09-19</td>
      <td>2013-08-26</td>
      <td>2</td>
      <td>179.61</td>
      <td>HILARION-Abastos</td>
      <td>Carrera 22 con Ave. Carlos Soublette #8-35</td>
      <td>San Cristóbal</td>
      <td>South America</td>
      <td>5022</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>394</td>
      <td>10642</td>
      <td>SIMOB</td>
      <td>7</td>
      <td>2013-08-22</td>
      <td>2013-09-19</td>
      <td>2013-09-05</td>
      <td>3</td>
      <td>41.89</td>
      <td>Simons bistro</td>
      <td>Vinbæltet 34</td>
      <td>Kobenhavn</td>
      <td>Northern Europe</td>
      <td>1734</td>
      <td>Denmark</td>
    </tr>
    <tr>
      <td>395</td>
      <td>10643</td>
      <td>ALFKI</td>
      <td>6</td>
      <td>2013-08-25</td>
      <td>2013-09-22</td>
      <td>2013-09-02</td>
      <td>1</td>
      <td>29.46</td>
      <td>Alfreds Futterkiste</td>
      <td>Obere Str. 57</td>
      <td>Berlin</td>
      <td>Western Europe</td>
      <td>12209</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>396</td>
      <td>10644</td>
      <td>WELLI</td>
      <td>3</td>
      <td>2013-08-25</td>
      <td>2013-09-22</td>
      <td>2013-09-01</td>
      <td>2</td>
      <td>0.14</td>
      <td>Wellington Importadora</td>
      <td>Rua do Mercado, 12</td>
      <td>Resende</td>
      <td>South America</td>
      <td>08737-363</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>397</td>
      <td>10645</td>
      <td>HANAR</td>
      <td>4</td>
      <td>2013-08-26</td>
      <td>2013-09-23</td>
      <td>2013-09-02</td>
      <td>1</td>
      <td>12.41</td>
      <td>Hanari Carnes</td>
      <td>Rua do Paço, 67</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>05454-876</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>398</td>
      <td>10646</td>
      <td>HUNGO</td>
      <td>9</td>
      <td>2013-08-27</td>
      <td>2013-10-08</td>
      <td>2013-09-03</td>
      <td>3</td>
      <td>142.33</td>
      <td>Hungry Owl All-Night Grocers</td>
      <td>8 Johnstown Road</td>
      <td>Cork</td>
      <td>British Isles</td>
      <td>None</td>
      <td>Ireland</td>
    </tr>
    <tr>
      <td>399</td>
      <td>10647</td>
      <td>QUEDE</td>
      <td>4</td>
      <td>2013-08-27</td>
      <td>2013-09-10</td>
      <td>2013-09-03</td>
      <td>2</td>
      <td>45.54</td>
      <td>Que Delícia</td>
      <td>Rua da Panificadora, 12</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>02389-673</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>400</td>
      <td>10648</td>
      <td>RICAR</td>
      <td>5</td>
      <td>2013-08-28</td>
      <td>2013-10-09</td>
      <td>2013-09-09</td>
      <td>2</td>
      <td>14.25</td>
      <td>Ricardo Adocicados</td>
      <td>Av. Copacabana, 267</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>02389-890</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>401</td>
      <td>10649</td>
      <td>MAISD</td>
      <td>5</td>
      <td>2013-08-28</td>
      <td>2013-09-25</td>
      <td>2013-08-29</td>
      <td>3</td>
      <td>6.20</td>
      <td>Maison Dewey</td>
      <td>Rue Joseph-Bens 532</td>
      <td>Bruxelles</td>
      <td>Western Europe</td>
      <td>B-1180</td>
      <td>Belgium</td>
    </tr>
    <tr>
      <td>402</td>
      <td>10650</td>
      <td>FAMIA</td>
      <td>5</td>
      <td>2013-08-29</td>
      <td>2013-09-26</td>
      <td>2013-09-03</td>
      <td>3</td>
      <td>176.81</td>
      <td>Familia Arquibaldo</td>
      <td>Rua Orós, 92</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05442-030</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>403</td>
      <td>10651</td>
      <td>WANDK</td>
      <td>8</td>
      <td>2013-09-01</td>
      <td>2013-09-29</td>
      <td>2013-09-11</td>
      <td>2</td>
      <td>20.60</td>
      <td>Die Wandernde Kuh</td>
      <td>Adenauerallee 900</td>
      <td>Stuttgart</td>
      <td>Western Europe</td>
      <td>70563</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>404</td>
      <td>10652</td>
      <td>GOURL</td>
      <td>4</td>
      <td>2013-09-01</td>
      <td>2013-09-29</td>
      <td>2013-09-08</td>
      <td>2</td>
      <td>7.14</td>
      <td>Gourmet Lanchonetes</td>
      <td>Av. Brasil, 442</td>
      <td>Campinas</td>
      <td>South America</td>
      <td>04876-786</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>405</td>
      <td>10653</td>
      <td>FRANK</td>
      <td>1</td>
      <td>2013-09-02</td>
      <td>2013-09-30</td>
      <td>2013-09-19</td>
      <td>1</td>
      <td>93.25</td>
      <td>Frankenversand</td>
      <td>Berliner Platz 43</td>
      <td>München</td>
      <td>Western Europe</td>
      <td>80805</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>406</td>
      <td>10654</td>
      <td>BERGS</td>
      <td>5</td>
      <td>2013-09-02</td>
      <td>2013-09-30</td>
      <td>2013-09-11</td>
      <td>1</td>
      <td>55.26</td>
      <td>Berglunds snabbköp</td>
      <td>Berguvsvägen  8</td>
      <td>Luleå</td>
      <td>Northern Europe</td>
      <td>S-958 22</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>407</td>
      <td>10655</td>
      <td>REGGC</td>
      <td>1</td>
      <td>2013-09-03</td>
      <td>2013-10-01</td>
      <td>2013-09-11</td>
      <td>2</td>
      <td>4.41</td>
      <td>Reggiani Caseifici</td>
      <td>Strada Provinciale 124</td>
      <td>Reggio Emilia</td>
      <td>Southern Europe</td>
      <td>42100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>408</td>
      <td>10656</td>
      <td>GREAL</td>
      <td>6</td>
      <td>2013-09-04</td>
      <td>2013-10-02</td>
      <td>2013-09-10</td>
      <td>1</td>
      <td>57.15</td>
      <td>Great Lakes Food Market</td>
      <td>2732 Baker Blvd.</td>
      <td>Eugene</td>
      <td>North America</td>
      <td>97403</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>409</td>
      <td>10657</td>
      <td>SAVEA</td>
      <td>2</td>
      <td>2013-09-04</td>
      <td>2013-10-02</td>
      <td>2013-09-15</td>
      <td>2</td>
      <td>352.69</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>410</td>
      <td>10658</td>
      <td>QUICK</td>
      <td>4</td>
      <td>2013-09-05</td>
      <td>2013-10-03</td>
      <td>2013-09-08</td>
      <td>1</td>
      <td>364.15</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>411</td>
      <td>10659</td>
      <td>QUEE</td>
      <td>7</td>
      <td>2013-09-05</td>
      <td>2013-10-03</td>
      <td>2013-09-10</td>
      <td>2</td>
      <td>105.81</td>
      <td>Queen Cozinha</td>
      <td>Alameda dos Canàrios, 891</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05487-020</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>412</td>
      <td>10660</td>
      <td>HUNGC</td>
      <td>8</td>
      <td>2013-09-08</td>
      <td>2013-10-06</td>
      <td>2013-10-15</td>
      <td>1</td>
      <td>111.29</td>
      <td>Hungry Coyote Import Store</td>
      <td>City Center Plaza 516 Main St.</td>
      <td>Elgin</td>
      <td>North America</td>
      <td>97827</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>413</td>
      <td>10661</td>
      <td>HUNGO</td>
      <td>7</td>
      <td>2013-09-09</td>
      <td>2013-10-07</td>
      <td>2013-09-15</td>
      <td>3</td>
      <td>17.55</td>
      <td>Hungry Owl All-Night Grocers</td>
      <td>8 Johnstown Road</td>
      <td>Cork</td>
      <td>British Isles</td>
      <td>None</td>
      <td>Ireland</td>
    </tr>
    <tr>
      <td>414</td>
      <td>10662</td>
      <td>LONEP</td>
      <td>3</td>
      <td>2013-09-09</td>
      <td>2013-10-07</td>
      <td>2013-09-18</td>
      <td>2</td>
      <td>1.28</td>
      <td>Lonesome Pine Restaurant</td>
      <td>89 Chiaroscuro Rd.</td>
      <td>Portland</td>
      <td>North America</td>
      <td>97219</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>415</td>
      <td>10663</td>
      <td>BONAP</td>
      <td>2</td>
      <td>2013-09-10</td>
      <td>2013-09-24</td>
      <td>2013-10-03</td>
      <td>2</td>
      <td>113.15</td>
      <td>Bon app'</td>
      <td>12, rue des Bouchers</td>
      <td>Marseille</td>
      <td>Western Europe</td>
      <td>13008</td>
      <td>France</td>
    </tr>
    <tr>
      <td>416</td>
      <td>10664</td>
      <td>FURIB</td>
      <td>1</td>
      <td>2013-09-10</td>
      <td>2013-10-08</td>
      <td>2013-09-19</td>
      <td>3</td>
      <td>1.27</td>
      <td>Furia Bacalhau e Frutos do Mar</td>
      <td>Jardim das rosas n. 32</td>
      <td>Lisboa</td>
      <td>Southern Europe</td>
      <td>1675</td>
      <td>Portugal</td>
    </tr>
    <tr>
      <td>417</td>
      <td>10665</td>
      <td>LONEP</td>
      <td>1</td>
      <td>2013-09-11</td>
      <td>2013-10-09</td>
      <td>2013-09-17</td>
      <td>2</td>
      <td>26.31</td>
      <td>Lonesome Pine Restaurant</td>
      <td>89 Chiaroscuro Rd.</td>
      <td>Portland</td>
      <td>North America</td>
      <td>97219</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>418</td>
      <td>10666</td>
      <td>RICSU</td>
      <td>7</td>
      <td>2013-09-12</td>
      <td>2013-10-10</td>
      <td>2013-09-22</td>
      <td>2</td>
      <td>232.42</td>
      <td>Richter Supermarkt</td>
      <td>Starenweg 5</td>
      <td>Genève</td>
      <td>Western Europe</td>
      <td>1204</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <td>419</td>
      <td>10667</td>
      <td>ERNSH</td>
      <td>7</td>
      <td>2013-09-12</td>
      <td>2013-10-10</td>
      <td>2013-09-19</td>
      <td>1</td>
      <td>78.09</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>420</td>
      <td>10668</td>
      <td>WANDK</td>
      <td>1</td>
      <td>2013-09-15</td>
      <td>2013-10-13</td>
      <td>2013-09-23</td>
      <td>2</td>
      <td>47.22</td>
      <td>Die Wandernde Kuh</td>
      <td>Adenauerallee 900</td>
      <td>Stuttgart</td>
      <td>Western Europe</td>
      <td>70563</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>421</td>
      <td>10669</td>
      <td>SIMOB</td>
      <td>2</td>
      <td>2013-09-15</td>
      <td>2013-10-13</td>
      <td>2013-09-22</td>
      <td>1</td>
      <td>24.39</td>
      <td>Simons bistro</td>
      <td>Vinbæltet 34</td>
      <td>Kobenhavn</td>
      <td>Northern Europe</td>
      <td>1734</td>
      <td>Denmark</td>
    </tr>
    <tr>
      <td>422</td>
      <td>10670</td>
      <td>FRANK</td>
      <td>4</td>
      <td>2013-09-16</td>
      <td>2013-10-14</td>
      <td>2013-09-18</td>
      <td>1</td>
      <td>203.48</td>
      <td>Frankenversand</td>
      <td>Berliner Platz 43</td>
      <td>München</td>
      <td>Western Europe</td>
      <td>80805</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>423</td>
      <td>10671</td>
      <td>FRANR</td>
      <td>1</td>
      <td>2013-09-17</td>
      <td>2013-10-15</td>
      <td>2013-09-24</td>
      <td>1</td>
      <td>30.34</td>
      <td>France restauration</td>
      <td>54, rue Royale</td>
      <td>Nantes</td>
      <td>Western Europe</td>
      <td>44000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>424</td>
      <td>10672</td>
      <td>BERGS</td>
      <td>9</td>
      <td>2013-09-17</td>
      <td>2013-10-01</td>
      <td>2013-09-26</td>
      <td>2</td>
      <td>95.75</td>
      <td>Berglunds snabbköp</td>
      <td>Berguvsvägen  8</td>
      <td>Luleå</td>
      <td>Northern Europe</td>
      <td>S-958 22</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>425</td>
      <td>10673</td>
      <td>WILMK</td>
      <td>2</td>
      <td>2013-09-18</td>
      <td>2013-10-16</td>
      <td>2013-09-19</td>
      <td>1</td>
      <td>22.76</td>
      <td>Wilman Kala</td>
      <td>Keskuskatu 45</td>
      <td>Helsinki</td>
      <td>Scandinavia</td>
      <td>21240</td>
      <td>Finland</td>
    </tr>
    <tr>
      <td>426</td>
      <td>10674</td>
      <td>ISLAT</td>
      <td>4</td>
      <td>2013-09-18</td>
      <td>2013-10-16</td>
      <td>2013-09-30</td>
      <td>2</td>
      <td>0.90</td>
      <td>Island Trading</td>
      <td>Garden House Crowther Way</td>
      <td>Cowes</td>
      <td>British Isles</td>
      <td>PO31 7PJ</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>427</td>
      <td>10675</td>
      <td>FRANK</td>
      <td>5</td>
      <td>2013-09-19</td>
      <td>2013-10-17</td>
      <td>2013-09-23</td>
      <td>2</td>
      <td>31.85</td>
      <td>Frankenversand</td>
      <td>Berliner Platz 43</td>
      <td>München</td>
      <td>Western Europe</td>
      <td>80805</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>428</td>
      <td>10676</td>
      <td>TORTU</td>
      <td>2</td>
      <td>2013-09-22</td>
      <td>2013-10-20</td>
      <td>2013-09-29</td>
      <td>2</td>
      <td>2.01</td>
      <td>Tortuga Restaurante</td>
      <td>Avda. Azteca 123</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05033</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>429</td>
      <td>10677</td>
      <td>ANTO</td>
      <td>1</td>
      <td>2013-09-22</td>
      <td>2013-10-20</td>
      <td>2013-09-26</td>
      <td>3</td>
      <td>4.03</td>
      <td>Antonio Moreno Taquería</td>
      <td>Mataderos  2312</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05023</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>430</td>
      <td>10678</td>
      <td>SAVEA</td>
      <td>7</td>
      <td>2013-09-23</td>
      <td>2013-10-21</td>
      <td>2013-10-16</td>
      <td>3</td>
      <td>388.98</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>431</td>
      <td>10679</td>
      <td>BLONP</td>
      <td>8</td>
      <td>2013-09-23</td>
      <td>2013-10-21</td>
      <td>2013-09-30</td>
      <td>3</td>
      <td>27.94</td>
      <td>Blondel père et fils</td>
      <td>24, place Kléber</td>
      <td>Strasbourg</td>
      <td>Western Europe</td>
      <td>67000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>432</td>
      <td>10680</td>
      <td>OLDWO</td>
      <td>1</td>
      <td>2013-09-24</td>
      <td>2013-10-22</td>
      <td>2013-09-26</td>
      <td>1</td>
      <td>26.61</td>
      <td>Old World Delicatessen</td>
      <td>2743 Bering St.</td>
      <td>Anchorage</td>
      <td>North America</td>
      <td>99508</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>433</td>
      <td>10681</td>
      <td>GREAL</td>
      <td>3</td>
      <td>2013-09-25</td>
      <td>2013-10-23</td>
      <td>2013-09-30</td>
      <td>3</td>
      <td>76.13</td>
      <td>Great Lakes Food Market</td>
      <td>2732 Baker Blvd.</td>
      <td>Eugene</td>
      <td>North America</td>
      <td>97403</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>434</td>
      <td>10682</td>
      <td>ANTO</td>
      <td>3</td>
      <td>2013-09-25</td>
      <td>2013-10-23</td>
      <td>2013-10-01</td>
      <td>2</td>
      <td>36.13</td>
      <td>Antonio Moreno Taquería</td>
      <td>Mataderos  2312</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05023</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>435</td>
      <td>10683</td>
      <td>DUMO</td>
      <td>2</td>
      <td>2013-09-26</td>
      <td>2013-10-24</td>
      <td>2013-10-01</td>
      <td>1</td>
      <td>4.40</td>
      <td>Du monde entier</td>
      <td>67, rue des Cinquante Otages</td>
      <td>Nantes</td>
      <td>Western Europe</td>
      <td>44000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>436</td>
      <td>10684</td>
      <td>OTTIK</td>
      <td>3</td>
      <td>2013-09-26</td>
      <td>2013-10-24</td>
      <td>2013-09-30</td>
      <td>1</td>
      <td>145.63</td>
      <td>Ottilies Käseladen</td>
      <td>Mehrheimerstr. 369</td>
      <td>Köln</td>
      <td>Western Europe</td>
      <td>50739</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>437</td>
      <td>10685</td>
      <td>GOURL</td>
      <td>4</td>
      <td>2013-09-29</td>
      <td>2013-10-13</td>
      <td>2013-10-03</td>
      <td>2</td>
      <td>33.75</td>
      <td>Gourmet Lanchonetes</td>
      <td>Av. Brasil, 442</td>
      <td>Campinas</td>
      <td>South America</td>
      <td>04876-786</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>438</td>
      <td>10686</td>
      <td>PICCO</td>
      <td>2</td>
      <td>2013-09-30</td>
      <td>2013-10-28</td>
      <td>2013-10-08</td>
      <td>1</td>
      <td>96.50</td>
      <td>Piccolo und mehr</td>
      <td>Geislweg 14</td>
      <td>Salzburg</td>
      <td>Western Europe</td>
      <td>5020</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>439</td>
      <td>10687</td>
      <td>HUNGO</td>
      <td>9</td>
      <td>2013-09-30</td>
      <td>2013-10-28</td>
      <td>2013-10-30</td>
      <td>2</td>
      <td>296.43</td>
      <td>Hungry Owl All-Night Grocers</td>
      <td>8 Johnstown Road</td>
      <td>Cork</td>
      <td>British Isles</td>
      <td>None</td>
      <td>Ireland</td>
    </tr>
    <tr>
      <td>440</td>
      <td>10688</td>
      <td>VAFFE</td>
      <td>4</td>
      <td>2013-10-01</td>
      <td>2013-10-15</td>
      <td>2013-10-07</td>
      <td>2</td>
      <td>299.09</td>
      <td>Vaffeljernet</td>
      <td>Smagsloget 45</td>
      <td>Århus</td>
      <td>Northern Europe</td>
      <td>8200</td>
      <td>Denmark</td>
    </tr>
    <tr>
      <td>441</td>
      <td>10689</td>
      <td>BERGS</td>
      <td>1</td>
      <td>2013-10-01</td>
      <td>2013-10-29</td>
      <td>2013-10-07</td>
      <td>2</td>
      <td>13.42</td>
      <td>Berglunds snabbköp</td>
      <td>Berguvsvägen  8</td>
      <td>Luleå</td>
      <td>Northern Europe</td>
      <td>S-958 22</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>442</td>
      <td>10690</td>
      <td>HANAR</td>
      <td>1</td>
      <td>2013-10-02</td>
      <td>2013-10-30</td>
      <td>2013-10-03</td>
      <td>1</td>
      <td>15.80</td>
      <td>Hanari Carnes</td>
      <td>Rua do Paço, 67</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>05454-876</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>443</td>
      <td>10691</td>
      <td>QUICK</td>
      <td>2</td>
      <td>2013-10-03</td>
      <td>2013-11-14</td>
      <td>2013-10-22</td>
      <td>2</td>
      <td>810.05</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>444</td>
      <td>10692</td>
      <td>ALFKI</td>
      <td>4</td>
      <td>2013-10-03</td>
      <td>2013-10-31</td>
      <td>2013-10-13</td>
      <td>2</td>
      <td>61.02</td>
      <td>Alfred's Futterkiste</td>
      <td>Obere Str. 57</td>
      <td>Berlin</td>
      <td>Western Europe</td>
      <td>12209</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>445</td>
      <td>10693</td>
      <td>WHITC</td>
      <td>3</td>
      <td>2013-10-06</td>
      <td>2013-10-20</td>
      <td>2013-10-10</td>
      <td>3</td>
      <td>139.34</td>
      <td>White Clover Markets</td>
      <td>1029 - 12th Ave. S.</td>
      <td>Seattle</td>
      <td>North America</td>
      <td>98124</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>446</td>
      <td>10694</td>
      <td>QUICK</td>
      <td>8</td>
      <td>2013-10-06</td>
      <td>2013-11-03</td>
      <td>2013-10-09</td>
      <td>3</td>
      <td>398.36</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>447</td>
      <td>10695</td>
      <td>WILMK</td>
      <td>7</td>
      <td>2013-10-07</td>
      <td>2013-11-18</td>
      <td>2013-10-14</td>
      <td>1</td>
      <td>16.72</td>
      <td>Wilman Kala</td>
      <td>Keskuskatu 45</td>
      <td>Helsinki</td>
      <td>Scandinavia</td>
      <td>21240</td>
      <td>Finland</td>
    </tr>
    <tr>
      <td>448</td>
      <td>10696</td>
      <td>WHITC</td>
      <td>8</td>
      <td>2013-10-08</td>
      <td>2013-11-19</td>
      <td>2013-10-14</td>
      <td>3</td>
      <td>102.55</td>
      <td>White Clover Markets</td>
      <td>1029 - 12th Ave. S.</td>
      <td>Seattle</td>
      <td>North America</td>
      <td>98124</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>449</td>
      <td>10697</td>
      <td>LINOD</td>
      <td>3</td>
      <td>2013-10-08</td>
      <td>2013-11-05</td>
      <td>2013-10-14</td>
      <td>1</td>
      <td>45.52</td>
      <td>LINO-Delicateses</td>
      <td>Ave. 5 de Mayo Porlamar</td>
      <td>I. de Margarita</td>
      <td>South America</td>
      <td>4980</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>450</td>
      <td>10698</td>
      <td>ERNSH</td>
      <td>4</td>
      <td>2013-10-09</td>
      <td>2013-11-06</td>
      <td>2013-10-17</td>
      <td>1</td>
      <td>272.47</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>451</td>
      <td>10699</td>
      <td>MORGK</td>
      <td>3</td>
      <td>2013-10-09</td>
      <td>2013-11-06</td>
      <td>2013-10-13</td>
      <td>3</td>
      <td>0.58</td>
      <td>Morgenstern Gesundkost</td>
      <td>Heerstr. 22</td>
      <td>Leipzig</td>
      <td>Western Europe</td>
      <td>04179</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>452</td>
      <td>10700</td>
      <td>SAVEA</td>
      <td>3</td>
      <td>2013-10-10</td>
      <td>2013-11-07</td>
      <td>2013-10-16</td>
      <td>1</td>
      <td>65.10</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>453</td>
      <td>10701</td>
      <td>HUNGO</td>
      <td>6</td>
      <td>2013-10-13</td>
      <td>2013-10-27</td>
      <td>2013-10-15</td>
      <td>3</td>
      <td>220.31</td>
      <td>Hungry Owl All-Night Grocers</td>
      <td>8 Johnstown Road</td>
      <td>Cork</td>
      <td>British Isles</td>
      <td>None</td>
      <td>Ireland</td>
    </tr>
    <tr>
      <td>454</td>
      <td>10702</td>
      <td>ALFKI</td>
      <td>4</td>
      <td>2013-10-13</td>
      <td>2013-11-24</td>
      <td>2013-10-21</td>
      <td>1</td>
      <td>23.94</td>
      <td>Alfred's Futterkiste</td>
      <td>Obere Str. 57</td>
      <td>Berlin</td>
      <td>Western Europe</td>
      <td>12209</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>455</td>
      <td>10703</td>
      <td>FOLKO</td>
      <td>6</td>
      <td>2013-10-14</td>
      <td>2013-11-11</td>
      <td>2013-10-20</td>
      <td>2</td>
      <td>152.30</td>
      <td>Folk och fä HB</td>
      <td>Åkergatan 24</td>
      <td>Bräcke</td>
      <td>Northern Europe</td>
      <td>S-844 67</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>456</td>
      <td>10704</td>
      <td>QUEE</td>
      <td>6</td>
      <td>2013-10-14</td>
      <td>2013-11-11</td>
      <td>2013-11-07</td>
      <td>1</td>
      <td>4.78</td>
      <td>Queen Cozinha</td>
      <td>Alameda dos Canàrios, 891</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05487-020</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>457</td>
      <td>10705</td>
      <td>HILAA</td>
      <td>9</td>
      <td>2013-10-15</td>
      <td>2013-11-12</td>
      <td>2013-11-18</td>
      <td>2</td>
      <td>3.52</td>
      <td>HILARION-Abastos</td>
      <td>Carrera 22 con Ave. Carlos Soublette #8-35</td>
      <td>San Cristóbal</td>
      <td>South America</td>
      <td>5022</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>458</td>
      <td>10706</td>
      <td>OLDWO</td>
      <td>8</td>
      <td>2013-10-16</td>
      <td>2013-11-13</td>
      <td>2013-10-21</td>
      <td>3</td>
      <td>135.63</td>
      <td>Old World Delicatessen</td>
      <td>2743 Bering St.</td>
      <td>Anchorage</td>
      <td>North America</td>
      <td>99508</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>459</td>
      <td>10707</td>
      <td>AROUT</td>
      <td>4</td>
      <td>2013-10-16</td>
      <td>2013-10-30</td>
      <td>2013-10-23</td>
      <td>3</td>
      <td>21.74</td>
      <td>Around the Horn</td>
      <td>Brook Farm Stratford St. Mary</td>
      <td>Colchester</td>
      <td>British Isles</td>
      <td>CO7 6JX</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>460</td>
      <td>10708</td>
      <td>THEBI</td>
      <td>6</td>
      <td>2013-10-17</td>
      <td>2013-11-28</td>
      <td>2013-11-05</td>
      <td>2</td>
      <td>2.96</td>
      <td>The Big Cheese</td>
      <td>89 Jefferson Way Suite 2</td>
      <td>Portland</td>
      <td>North America</td>
      <td>97201</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>461</td>
      <td>10709</td>
      <td>GOURL</td>
      <td>1</td>
      <td>2013-10-17</td>
      <td>2013-11-14</td>
      <td>2013-11-20</td>
      <td>3</td>
      <td>210.80</td>
      <td>Gourmet Lanchonetes</td>
      <td>Av. Brasil, 442</td>
      <td>Campinas</td>
      <td>South America</td>
      <td>04876-786</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>462</td>
      <td>10710</td>
      <td>FRANS</td>
      <td>1</td>
      <td>2013-10-20</td>
      <td>2013-11-17</td>
      <td>2013-10-23</td>
      <td>1</td>
      <td>4.98</td>
      <td>Franchi S.p.A.</td>
      <td>Via Monte Bianco 34</td>
      <td>Torino</td>
      <td>Southern Europe</td>
      <td>10100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>463</td>
      <td>10711</td>
      <td>SAVEA</td>
      <td>5</td>
      <td>2013-10-21</td>
      <td>2013-12-02</td>
      <td>2013-10-29</td>
      <td>2</td>
      <td>52.41</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>464</td>
      <td>10712</td>
      <td>HUNGO</td>
      <td>3</td>
      <td>2013-10-21</td>
      <td>2013-11-18</td>
      <td>2013-10-31</td>
      <td>1</td>
      <td>89.93</td>
      <td>Hungry Owl All-Night Grocers</td>
      <td>8 Johnstown Road</td>
      <td>Cork</td>
      <td>British Isles</td>
      <td>None</td>
      <td>Ireland</td>
    </tr>
    <tr>
      <td>465</td>
      <td>10713</td>
      <td>SAVEA</td>
      <td>1</td>
      <td>2013-10-22</td>
      <td>2013-11-19</td>
      <td>2013-10-24</td>
      <td>1</td>
      <td>167.05</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>466</td>
      <td>10714</td>
      <td>SAVEA</td>
      <td>5</td>
      <td>2013-10-22</td>
      <td>2013-11-19</td>
      <td>2013-10-27</td>
      <td>3</td>
      <td>24.49</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>467</td>
      <td>10715</td>
      <td>BONAP</td>
      <td>3</td>
      <td>2013-10-23</td>
      <td>2013-11-06</td>
      <td>2013-10-29</td>
      <td>1</td>
      <td>63.20</td>
      <td>Bon app'</td>
      <td>12, rue des Bouchers</td>
      <td>Marseille</td>
      <td>Western Europe</td>
      <td>13008</td>
      <td>France</td>
    </tr>
    <tr>
      <td>468</td>
      <td>10716</td>
      <td>RANCH</td>
      <td>4</td>
      <td>2013-10-24</td>
      <td>2013-11-21</td>
      <td>2013-10-27</td>
      <td>2</td>
      <td>22.57</td>
      <td>Rancho grande</td>
      <td>Av. del Libertador 900</td>
      <td>Buenos Aires</td>
      <td>South America</td>
      <td>1010</td>
      <td>Argentina</td>
    </tr>
    <tr>
      <td>469</td>
      <td>10717</td>
      <td>FRANK</td>
      <td>1</td>
      <td>2013-10-24</td>
      <td>2013-11-21</td>
      <td>2013-10-29</td>
      <td>2</td>
      <td>59.25</td>
      <td>Frankenversand</td>
      <td>Berliner Platz 43</td>
      <td>München</td>
      <td>Western Europe</td>
      <td>80805</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>470</td>
      <td>10718</td>
      <td>KOENE</td>
      <td>1</td>
      <td>2013-10-27</td>
      <td>2013-11-24</td>
      <td>2013-10-29</td>
      <td>3</td>
      <td>170.88</td>
      <td>Königlich Essen</td>
      <td>Maubelstr. 90</td>
      <td>Brandenburg</td>
      <td>Western Europe</td>
      <td>14776</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>471</td>
      <td>10719</td>
      <td>LETSS</td>
      <td>8</td>
      <td>2013-10-27</td>
      <td>2013-11-24</td>
      <td>2013-11-05</td>
      <td>2</td>
      <td>51.44</td>
      <td>Let's Stop N Shop</td>
      <td>87 Polk St. Suite 5</td>
      <td>San Francisco</td>
      <td>North America</td>
      <td>94117</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>472</td>
      <td>10720</td>
      <td>QUEDE</td>
      <td>8</td>
      <td>2013-10-28</td>
      <td>2013-11-11</td>
      <td>2013-11-05</td>
      <td>2</td>
      <td>9.53</td>
      <td>Que Delícia</td>
      <td>Rua da Panificadora, 12</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>02389-673</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>473</td>
      <td>10721</td>
      <td>QUICK</td>
      <td>5</td>
      <td>2013-10-29</td>
      <td>2013-11-26</td>
      <td>2013-10-31</td>
      <td>3</td>
      <td>48.92</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>474</td>
      <td>10722</td>
      <td>SAVEA</td>
      <td>8</td>
      <td>2013-10-29</td>
      <td>2013-12-10</td>
      <td>2013-11-04</td>
      <td>1</td>
      <td>74.58</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>475</td>
      <td>10723</td>
      <td>WHITC</td>
      <td>3</td>
      <td>2013-10-30</td>
      <td>2013-11-27</td>
      <td>2013-11-25</td>
      <td>1</td>
      <td>21.72</td>
      <td>White Clover Markets</td>
      <td>1029 - 12th Ave. S.</td>
      <td>Seattle</td>
      <td>North America</td>
      <td>98124</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>476</td>
      <td>10724</td>
      <td>MEREP</td>
      <td>8</td>
      <td>2013-10-30</td>
      <td>2013-12-11</td>
      <td>2013-11-05</td>
      <td>2</td>
      <td>57.75</td>
      <td>Mère Paillarde</td>
      <td>43 rue St. Laurent</td>
      <td>Montréal</td>
      <td>North America</td>
      <td>H1J 1C3</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>477</td>
      <td>10725</td>
      <td>FAMIA</td>
      <td>4</td>
      <td>2013-10-31</td>
      <td>2013-11-28</td>
      <td>2013-11-05</td>
      <td>3</td>
      <td>10.83</td>
      <td>Familia Arquibaldo</td>
      <td>Rua Orós, 92</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05442-030</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>478</td>
      <td>10726</td>
      <td>EASTC</td>
      <td>4</td>
      <td>2013-11-03</td>
      <td>2013-11-17</td>
      <td>2013-12-05</td>
      <td>1</td>
      <td>16.56</td>
      <td>Eastern Connection</td>
      <td>35 King George</td>
      <td>London</td>
      <td>British Isles</td>
      <td>WX3 6FW</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>479</td>
      <td>10727</td>
      <td>REGGC</td>
      <td>2</td>
      <td>2013-11-03</td>
      <td>2013-12-01</td>
      <td>2013-12-05</td>
      <td>1</td>
      <td>89.90</td>
      <td>Reggiani Caseifici</td>
      <td>Strada Provinciale 124</td>
      <td>Reggio Emilia</td>
      <td>Southern Europe</td>
      <td>42100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>480</td>
      <td>10728</td>
      <td>QUEE</td>
      <td>4</td>
      <td>2013-11-04</td>
      <td>2013-12-02</td>
      <td>2013-11-11</td>
      <td>2</td>
      <td>58.33</td>
      <td>Queen Cozinha</td>
      <td>Alameda dos Canàrios, 891</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05487-020</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>481</td>
      <td>10729</td>
      <td>LINOD</td>
      <td>8</td>
      <td>2013-11-04</td>
      <td>2013-12-16</td>
      <td>2013-11-14</td>
      <td>3</td>
      <td>141.06</td>
      <td>LINO-Delicateses</td>
      <td>Ave. 5 de Mayo Porlamar</td>
      <td>I. de Margarita</td>
      <td>South America</td>
      <td>4980</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>482</td>
      <td>10730</td>
      <td>BONAP</td>
      <td>5</td>
      <td>2013-11-05</td>
      <td>2013-12-03</td>
      <td>2013-11-14</td>
      <td>1</td>
      <td>20.12</td>
      <td>Bon app'</td>
      <td>12, rue des Bouchers</td>
      <td>Marseille</td>
      <td>Western Europe</td>
      <td>13008</td>
      <td>France</td>
    </tr>
    <tr>
      <td>483</td>
      <td>10731</td>
      <td>CHOPS</td>
      <td>7</td>
      <td>2013-11-06</td>
      <td>2013-12-04</td>
      <td>2013-11-14</td>
      <td>1</td>
      <td>96.65</td>
      <td>Chop-suey Chinese</td>
      <td>Hauptstr. 31</td>
      <td>Bern</td>
      <td>Western Europe</td>
      <td>3012</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <td>484</td>
      <td>10732</td>
      <td>BONAP</td>
      <td>3</td>
      <td>2013-11-06</td>
      <td>2013-12-04</td>
      <td>2013-11-07</td>
      <td>1</td>
      <td>16.97</td>
      <td>Bon app'</td>
      <td>12, rue des Bouchers</td>
      <td>Marseille</td>
      <td>Western Europe</td>
      <td>13008</td>
      <td>France</td>
    </tr>
    <tr>
      <td>485</td>
      <td>10733</td>
      <td>BERGS</td>
      <td>1</td>
      <td>2013-11-07</td>
      <td>2013-12-05</td>
      <td>2013-11-10</td>
      <td>3</td>
      <td>110.11</td>
      <td>Berglunds snabbköp</td>
      <td>Berguvsvägen  8</td>
      <td>Luleå</td>
      <td>Northern Europe</td>
      <td>S-958 22</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>486</td>
      <td>10734</td>
      <td>GOURL</td>
      <td>2</td>
      <td>2013-11-07</td>
      <td>2013-12-05</td>
      <td>2013-11-12</td>
      <td>3</td>
      <td>1.63</td>
      <td>Gourmet Lanchonetes</td>
      <td>Av. Brasil, 442</td>
      <td>Campinas</td>
      <td>South America</td>
      <td>04876-786</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>487</td>
      <td>10735</td>
      <td>LETSS</td>
      <td>6</td>
      <td>2013-11-10</td>
      <td>2013-12-08</td>
      <td>2013-11-21</td>
      <td>2</td>
      <td>45.97</td>
      <td>Let's Stop N Shop</td>
      <td>87 Polk St. Suite 5</td>
      <td>San Francisco</td>
      <td>North America</td>
      <td>94117</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>488</td>
      <td>10736</td>
      <td>HUNGO</td>
      <td>9</td>
      <td>2013-11-11</td>
      <td>2013-12-09</td>
      <td>2013-11-21</td>
      <td>2</td>
      <td>44.10</td>
      <td>Hungry Owl All-Night Grocers</td>
      <td>8 Johnstown Road</td>
      <td>Cork</td>
      <td>British Isles</td>
      <td>None</td>
      <td>Ireland</td>
    </tr>
    <tr>
      <td>489</td>
      <td>10737</td>
      <td>VINET</td>
      <td>2</td>
      <td>2013-11-11</td>
      <td>2013-12-09</td>
      <td>2013-11-18</td>
      <td>2</td>
      <td>7.79</td>
      <td>Vins et alcools Chevalier</td>
      <td>59 rue de l'Abbaye</td>
      <td>Reims</td>
      <td>Western Europe</td>
      <td>51100</td>
      <td>France</td>
    </tr>
    <tr>
      <td>490</td>
      <td>10738</td>
      <td>SPECD</td>
      <td>2</td>
      <td>2013-11-12</td>
      <td>2013-12-10</td>
      <td>2013-11-18</td>
      <td>1</td>
      <td>2.91</td>
      <td>Spécialités du monde</td>
      <td>25, rue Lauriston</td>
      <td>Paris</td>
      <td>Western Europe</td>
      <td>75016</td>
      <td>France</td>
    </tr>
    <tr>
      <td>491</td>
      <td>10739</td>
      <td>VINET</td>
      <td>3</td>
      <td>2013-11-12</td>
      <td>2013-12-10</td>
      <td>2013-11-17</td>
      <td>3</td>
      <td>11.08</td>
      <td>Vins et alcools Chevalier</td>
      <td>59 rue de l'Abbaye</td>
      <td>Reims</td>
      <td>Western Europe</td>
      <td>51100</td>
      <td>France</td>
    </tr>
    <tr>
      <td>492</td>
      <td>10740</td>
      <td>WHITC</td>
      <td>4</td>
      <td>2013-11-13</td>
      <td>2013-12-11</td>
      <td>2013-11-25</td>
      <td>2</td>
      <td>81.88</td>
      <td>White Clover Markets</td>
      <td>1029 - 12th Ave. S.</td>
      <td>Seattle</td>
      <td>North America</td>
      <td>98124</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>493</td>
      <td>10741</td>
      <td>AROUT</td>
      <td>4</td>
      <td>2013-11-14</td>
      <td>2013-11-28</td>
      <td>2013-11-18</td>
      <td>3</td>
      <td>10.96</td>
      <td>Around the Horn</td>
      <td>Brook Farm Stratford St. Mary</td>
      <td>Colchester</td>
      <td>British Isles</td>
      <td>CO7 6JX</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>494</td>
      <td>10742</td>
      <td>BOTTM</td>
      <td>3</td>
      <td>2013-11-14</td>
      <td>2013-12-12</td>
      <td>2013-11-18</td>
      <td>3</td>
      <td>243.73</td>
      <td>Bottom-Dollar Markets</td>
      <td>23 Tsawassen Blvd.</td>
      <td>Tsawassen</td>
      <td>North America</td>
      <td>T2F 8M4</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>495</td>
      <td>10743</td>
      <td>AROUT</td>
      <td>1</td>
      <td>2013-11-17</td>
      <td>2013-12-15</td>
      <td>2013-11-21</td>
      <td>2</td>
      <td>23.72</td>
      <td>Around the Horn</td>
      <td>Brook Farm Stratford St. Mary</td>
      <td>Colchester</td>
      <td>British Isles</td>
      <td>CO7 6JX</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>496</td>
      <td>10744</td>
      <td>VAFFE</td>
      <td>6</td>
      <td>2013-11-17</td>
      <td>2013-12-15</td>
      <td>2013-11-24</td>
      <td>1</td>
      <td>69.19</td>
      <td>Vaffeljernet</td>
      <td>Smagsloget 45</td>
      <td>Århus</td>
      <td>Northern Europe</td>
      <td>8200</td>
      <td>Denmark</td>
    </tr>
    <tr>
      <td>497</td>
      <td>10745</td>
      <td>QUICK</td>
      <td>9</td>
      <td>2013-11-18</td>
      <td>2013-12-16</td>
      <td>2013-11-27</td>
      <td>1</td>
      <td>3.52</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>498</td>
      <td>10746</td>
      <td>CHOPS</td>
      <td>1</td>
      <td>2013-11-19</td>
      <td>2013-12-17</td>
      <td>2013-11-21</td>
      <td>3</td>
      <td>31.43</td>
      <td>Chop-suey Chinese</td>
      <td>Hauptstr. 31</td>
      <td>Bern</td>
      <td>Western Europe</td>
      <td>3012</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <td>499</td>
      <td>10747</td>
      <td>PICCO</td>
      <td>6</td>
      <td>2013-11-19</td>
      <td>2013-12-17</td>
      <td>2013-11-26</td>
      <td>1</td>
      <td>117.33</td>
      <td>Piccolo und mehr</td>
      <td>Geislweg 14</td>
      <td>Salzburg</td>
      <td>Western Europe</td>
      <td>5020</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>500</td>
      <td>10748</td>
      <td>SAVEA</td>
      <td>3</td>
      <td>2013-11-20</td>
      <td>2013-12-18</td>
      <td>2013-11-28</td>
      <td>1</td>
      <td>232.55</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>501</td>
      <td>10749</td>
      <td>ISLAT</td>
      <td>4</td>
      <td>2013-11-20</td>
      <td>2013-12-18</td>
      <td>2013-12-19</td>
      <td>2</td>
      <td>61.53</td>
      <td>Island Trading</td>
      <td>Garden House Crowther Way</td>
      <td>Cowes</td>
      <td>British Isles</td>
      <td>PO31 7PJ</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>502</td>
      <td>10750</td>
      <td>WARTH</td>
      <td>9</td>
      <td>2013-11-21</td>
      <td>2013-12-19</td>
      <td>2013-11-24</td>
      <td>1</td>
      <td>79.30</td>
      <td>Wartian Herkku</td>
      <td>Torikatu 38</td>
      <td>Oulu</td>
      <td>Scandinavia</td>
      <td>90110</td>
      <td>Finland</td>
    </tr>
    <tr>
      <td>503</td>
      <td>10751</td>
      <td>RICSU</td>
      <td>3</td>
      <td>2013-11-24</td>
      <td>2013-12-22</td>
      <td>2013-12-03</td>
      <td>3</td>
      <td>130.79</td>
      <td>Richter Supermarkt</td>
      <td>Starenweg 5</td>
      <td>Genève</td>
      <td>Western Europe</td>
      <td>1204</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <td>504</td>
      <td>10752</td>
      <td>NORTS</td>
      <td>2</td>
      <td>2013-11-24</td>
      <td>2013-12-22</td>
      <td>2013-11-28</td>
      <td>3</td>
      <td>1.39</td>
      <td>North/South</td>
      <td>South House 300 Queensbridge</td>
      <td>London</td>
      <td>British Isles</td>
      <td>SW7 1RZ</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>505</td>
      <td>10753</td>
      <td>FRANS</td>
      <td>3</td>
      <td>2013-11-25</td>
      <td>2013-12-23</td>
      <td>2013-11-27</td>
      <td>1</td>
      <td>7.70</td>
      <td>Franchi S.p.A.</td>
      <td>Via Monte Bianco 34</td>
      <td>Torino</td>
      <td>Southern Europe</td>
      <td>10100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>506</td>
      <td>10754</td>
      <td>MAGAA</td>
      <td>6</td>
      <td>2013-11-25</td>
      <td>2013-12-23</td>
      <td>2013-11-27</td>
      <td>3</td>
      <td>2.38</td>
      <td>Magazzini Alimentari Riuniti</td>
      <td>Via Ludovico il Moro 22</td>
      <td>Bergamo</td>
      <td>Southern Europe</td>
      <td>24100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>507</td>
      <td>10755</td>
      <td>BONAP</td>
      <td>4</td>
      <td>2013-11-26</td>
      <td>2013-12-24</td>
      <td>2013-11-28</td>
      <td>2</td>
      <td>16.71</td>
      <td>Bon app'</td>
      <td>12, rue des Bouchers</td>
      <td>Marseille</td>
      <td>Western Europe</td>
      <td>13008</td>
      <td>France</td>
    </tr>
    <tr>
      <td>508</td>
      <td>10756</td>
      <td>SPLIR</td>
      <td>8</td>
      <td>2013-11-27</td>
      <td>2013-12-25</td>
      <td>2013-12-02</td>
      <td>2</td>
      <td>73.21</td>
      <td>Split Rail Beer &amp; Ale</td>
      <td>P.O. Box 555</td>
      <td>Lander</td>
      <td>North America</td>
      <td>82520</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>509</td>
      <td>10757</td>
      <td>SAVEA</td>
      <td>6</td>
      <td>2013-11-27</td>
      <td>2013-12-25</td>
      <td>2013-12-15</td>
      <td>1</td>
      <td>8.19</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>510</td>
      <td>10758</td>
      <td>RICSU</td>
      <td>3</td>
      <td>2013-11-28</td>
      <td>2013-12-26</td>
      <td>2013-12-04</td>
      <td>3</td>
      <td>138.17</td>
      <td>Richter Supermarkt</td>
      <td>Starenweg 5</td>
      <td>Genève</td>
      <td>Western Europe</td>
      <td>1204</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <td>511</td>
      <td>10759</td>
      <td>ANATR</td>
      <td>3</td>
      <td>2013-11-28</td>
      <td>2013-12-26</td>
      <td>2013-12-12</td>
      <td>3</td>
      <td>11.99</td>
      <td>Ana Trujillo Emparedados y helados</td>
      <td>Avda. de la Constitución 2222</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05021</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>512</td>
      <td>10760</td>
      <td>MAISD</td>
      <td>4</td>
      <td>2013-12-01</td>
      <td>2013-12-29</td>
      <td>2013-12-10</td>
      <td>1</td>
      <td>155.64</td>
      <td>Maison Dewey</td>
      <td>Rue Joseph-Bens 532</td>
      <td>Bruxelles</td>
      <td>Western Europe</td>
      <td>B-1180</td>
      <td>Belgium</td>
    </tr>
    <tr>
      <td>513</td>
      <td>10761</td>
      <td>RATTC</td>
      <td>5</td>
      <td>2013-12-02</td>
      <td>2013-12-30</td>
      <td>2013-12-08</td>
      <td>2</td>
      <td>18.66</td>
      <td>Rattlesnake Canyon Grocery</td>
      <td>2817 Milton Dr.</td>
      <td>Albuquerque</td>
      <td>North America</td>
      <td>87110</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>514</td>
      <td>10762</td>
      <td>FOLKO</td>
      <td>3</td>
      <td>2013-12-02</td>
      <td>2013-12-30</td>
      <td>2013-12-09</td>
      <td>1</td>
      <td>328.74</td>
      <td>Folk och fä HB</td>
      <td>Åkergatan 24</td>
      <td>Bräcke</td>
      <td>Northern Europe</td>
      <td>S-844 67</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>515</td>
      <td>10763</td>
      <td>FOLIG</td>
      <td>3</td>
      <td>2013-12-03</td>
      <td>2013-12-31</td>
      <td>2013-12-08</td>
      <td>3</td>
      <td>37.35</td>
      <td>Folies gourmandes</td>
      <td>184, chaussée de Tournai</td>
      <td>Lille</td>
      <td>Western Europe</td>
      <td>59000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>516</td>
      <td>10764</td>
      <td>ERNSH</td>
      <td>6</td>
      <td>2013-12-03</td>
      <td>2013-12-31</td>
      <td>2013-12-08</td>
      <td>3</td>
      <td>145.45</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>517</td>
      <td>10765</td>
      <td>QUICK</td>
      <td>3</td>
      <td>2013-12-04</td>
      <td>2014-01-01</td>
      <td>2013-12-09</td>
      <td>3</td>
      <td>42.74</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>518</td>
      <td>10766</td>
      <td>OTTIK</td>
      <td>4</td>
      <td>2013-12-05</td>
      <td>2014-01-02</td>
      <td>2013-12-09</td>
      <td>1</td>
      <td>157.55</td>
      <td>Ottilies Käseladen</td>
      <td>Mehrheimerstr. 369</td>
      <td>Köln</td>
      <td>Western Europe</td>
      <td>50739</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>519</td>
      <td>10767</td>
      <td>SUPRD</td>
      <td>4</td>
      <td>2013-12-05</td>
      <td>2014-01-02</td>
      <td>2013-12-15</td>
      <td>3</td>
      <td>1.59</td>
      <td>Suprêmes délices</td>
      <td>Boulevard Tirou, 255</td>
      <td>Charleroi</td>
      <td>Western Europe</td>
      <td>B-6000</td>
      <td>Belgium</td>
    </tr>
    <tr>
      <td>520</td>
      <td>10768</td>
      <td>AROUT</td>
      <td>3</td>
      <td>2013-12-08</td>
      <td>2014-01-05</td>
      <td>2013-12-15</td>
      <td>2</td>
      <td>146.32</td>
      <td>Around the Horn</td>
      <td>Brook Farm Stratford St. Mary</td>
      <td>Colchester</td>
      <td>British Isles</td>
      <td>CO7 6JX</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>521</td>
      <td>10769</td>
      <td>VAFFE</td>
      <td>3</td>
      <td>2013-12-08</td>
      <td>2014-01-05</td>
      <td>2013-12-12</td>
      <td>1</td>
      <td>65.06</td>
      <td>Vaffeljernet</td>
      <td>Smagsloget 45</td>
      <td>Århus</td>
      <td>Northern Europe</td>
      <td>8200</td>
      <td>Denmark</td>
    </tr>
    <tr>
      <td>522</td>
      <td>10770</td>
      <td>HANAR</td>
      <td>8</td>
      <td>2013-12-09</td>
      <td>2014-01-06</td>
      <td>2013-12-17</td>
      <td>3</td>
      <td>5.32</td>
      <td>Hanari Carnes</td>
      <td>Rua do Paço, 67</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>05454-876</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>523</td>
      <td>10771</td>
      <td>ERNSH</td>
      <td>9</td>
      <td>2013-12-10</td>
      <td>2014-01-07</td>
      <td>2014-01-02</td>
      <td>2</td>
      <td>11.19</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>524</td>
      <td>10772</td>
      <td>LEHMS</td>
      <td>3</td>
      <td>2013-12-10</td>
      <td>2014-01-07</td>
      <td>2013-12-19</td>
      <td>2</td>
      <td>91.28</td>
      <td>Lehmanns Marktstand</td>
      <td>Magazinweg 7</td>
      <td>Frankfurt a.M.</td>
      <td>Western Europe</td>
      <td>60528</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>525</td>
      <td>10773</td>
      <td>ERNSH</td>
      <td>1</td>
      <td>2013-12-11</td>
      <td>2014-01-08</td>
      <td>2013-12-16</td>
      <td>3</td>
      <td>96.43</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>526</td>
      <td>10774</td>
      <td>FOLKO</td>
      <td>4</td>
      <td>2013-12-11</td>
      <td>2013-12-25</td>
      <td>2013-12-12</td>
      <td>1</td>
      <td>48.20</td>
      <td>Folk och fä HB</td>
      <td>Åkergatan 24</td>
      <td>Bräcke</td>
      <td>Northern Europe</td>
      <td>S-844 67</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>527</td>
      <td>10775</td>
      <td>THECR</td>
      <td>7</td>
      <td>2013-12-12</td>
      <td>2014-01-09</td>
      <td>2013-12-26</td>
      <td>1</td>
      <td>20.25</td>
      <td>The Cracker Box</td>
      <td>55 Grizzly Peak Rd.</td>
      <td>Butte</td>
      <td>North America</td>
      <td>59801</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>528</td>
      <td>10776</td>
      <td>ERNSH</td>
      <td>1</td>
      <td>2013-12-15</td>
      <td>2014-01-12</td>
      <td>2013-12-18</td>
      <td>3</td>
      <td>351.53</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>529</td>
      <td>10777</td>
      <td>GOURL</td>
      <td>7</td>
      <td>2013-12-15</td>
      <td>2013-12-29</td>
      <td>2014-01-21</td>
      <td>2</td>
      <td>3.01</td>
      <td>Gourmet Lanchonetes</td>
      <td>Av. Brasil, 442</td>
      <td>Campinas</td>
      <td>South America</td>
      <td>04876-786</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>530</td>
      <td>10778</td>
      <td>BERGS</td>
      <td>3</td>
      <td>2013-12-16</td>
      <td>2014-01-13</td>
      <td>2013-12-24</td>
      <td>1</td>
      <td>6.79</td>
      <td>Berglunds snabbköp</td>
      <td>Berguvsvägen  8</td>
      <td>Luleå</td>
      <td>Northern Europe</td>
      <td>S-958 22</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>531</td>
      <td>10779</td>
      <td>MORGK</td>
      <td>3</td>
      <td>2013-12-16</td>
      <td>2014-01-13</td>
      <td>2014-01-14</td>
      <td>2</td>
      <td>58.13</td>
      <td>Morgenstern Gesundkost</td>
      <td>Heerstr. 22</td>
      <td>Leipzig</td>
      <td>Western Europe</td>
      <td>04179</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>532</td>
      <td>10780</td>
      <td>LILAS</td>
      <td>2</td>
      <td>2013-12-16</td>
      <td>2013-12-30</td>
      <td>2013-12-25</td>
      <td>1</td>
      <td>42.13</td>
      <td>LILA-Supermercado</td>
      <td>Carrera 52 con Ave. Bolívar #65-98 Llano Largo</td>
      <td>Barquisimeto</td>
      <td>South America</td>
      <td>3508</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>533</td>
      <td>10781</td>
      <td>WARTH</td>
      <td>2</td>
      <td>2013-12-17</td>
      <td>2014-01-14</td>
      <td>2013-12-19</td>
      <td>3</td>
      <td>73.16</td>
      <td>Wartian Herkku</td>
      <td>Torikatu 38</td>
      <td>Oulu</td>
      <td>Scandinavia</td>
      <td>90110</td>
      <td>Finland</td>
    </tr>
    <tr>
      <td>534</td>
      <td>10782</td>
      <td>CACTU</td>
      <td>9</td>
      <td>2013-12-17</td>
      <td>2014-01-14</td>
      <td>2013-12-22</td>
      <td>3</td>
      <td>1.10</td>
      <td>Cactus Comidas para llevar</td>
      <td>Cerrito 333</td>
      <td>Buenos Aires</td>
      <td>South America</td>
      <td>1010</td>
      <td>Argentina</td>
    </tr>
    <tr>
      <td>535</td>
      <td>10783</td>
      <td>HANAR</td>
      <td>4</td>
      <td>2013-12-18</td>
      <td>2014-01-15</td>
      <td>2013-12-19</td>
      <td>2</td>
      <td>124.98</td>
      <td>Hanari Carnes</td>
      <td>Rua do Paço, 67</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>05454-876</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>536</td>
      <td>10784</td>
      <td>MAGAA</td>
      <td>4</td>
      <td>2013-12-18</td>
      <td>2014-01-15</td>
      <td>2013-12-22</td>
      <td>3</td>
      <td>70.09</td>
      <td>Magazzini Alimentari Riuniti</td>
      <td>Via Ludovico il Moro 22</td>
      <td>Bergamo</td>
      <td>Southern Europe</td>
      <td>24100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>537</td>
      <td>10785</td>
      <td>GROSR</td>
      <td>1</td>
      <td>2013-12-18</td>
      <td>2014-01-15</td>
      <td>2013-12-24</td>
      <td>3</td>
      <td>1.51</td>
      <td>GROSELLA-Restaurante</td>
      <td>5ª Ave. Los Palos Grandes</td>
      <td>Caracas</td>
      <td>South America</td>
      <td>1081</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>538</td>
      <td>10786</td>
      <td>QUEE</td>
      <td>8</td>
      <td>2013-12-19</td>
      <td>2014-01-16</td>
      <td>2013-12-23</td>
      <td>1</td>
      <td>110.87</td>
      <td>Queen Cozinha</td>
      <td>Alameda dos Canàrios, 891</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05487-020</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>539</td>
      <td>10787</td>
      <td>LAMAI</td>
      <td>2</td>
      <td>2013-12-19</td>
      <td>2014-01-02</td>
      <td>2013-12-26</td>
      <td>1</td>
      <td>249.93</td>
      <td>La maison d'Asie</td>
      <td>1 rue Alsace-Lorraine</td>
      <td>Toulouse</td>
      <td>Western Europe</td>
      <td>31000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>540</td>
      <td>10788</td>
      <td>QUICK</td>
      <td>1</td>
      <td>2013-12-22</td>
      <td>2014-01-19</td>
      <td>2014-01-19</td>
      <td>2</td>
      <td>42.70</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>541</td>
      <td>10789</td>
      <td>FOLIG</td>
      <td>1</td>
      <td>2013-12-22</td>
      <td>2014-01-19</td>
      <td>2013-12-31</td>
      <td>2</td>
      <td>100.60</td>
      <td>Folies gourmandes</td>
      <td>184, chaussée de Tournai</td>
      <td>Lille</td>
      <td>Western Europe</td>
      <td>59000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>542</td>
      <td>10790</td>
      <td>GOURL</td>
      <td>6</td>
      <td>2013-12-22</td>
      <td>2014-01-19</td>
      <td>2013-12-26</td>
      <td>1</td>
      <td>28.23</td>
      <td>Gourmet Lanchonetes</td>
      <td>Av. Brasil, 442</td>
      <td>Campinas</td>
      <td>South America</td>
      <td>04876-786</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>543</td>
      <td>10791</td>
      <td>FRANK</td>
      <td>6</td>
      <td>2013-12-23</td>
      <td>2014-01-20</td>
      <td>2014-01-01</td>
      <td>2</td>
      <td>16.85</td>
      <td>Frankenversand</td>
      <td>Berliner Platz 43</td>
      <td>München</td>
      <td>Western Europe</td>
      <td>80805</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>544</td>
      <td>10792</td>
      <td>WOLZA</td>
      <td>1</td>
      <td>2013-12-23</td>
      <td>2014-01-20</td>
      <td>2013-12-31</td>
      <td>3</td>
      <td>23.79</td>
      <td>Wolski Zajazd</td>
      <td>ul. Filtrowa 68</td>
      <td>Warszawa</td>
      <td>Eastern Europe</td>
      <td>01-012</td>
      <td>Poland</td>
    </tr>
    <tr>
      <td>545</td>
      <td>10793</td>
      <td>AROUT</td>
      <td>3</td>
      <td>2013-12-24</td>
      <td>2014-01-21</td>
      <td>2014-01-08</td>
      <td>3</td>
      <td>4.52</td>
      <td>Around the Horn</td>
      <td>Brook Farm Stratford St. Mary</td>
      <td>Colchester</td>
      <td>British Isles</td>
      <td>CO7 6JX</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>546</td>
      <td>10794</td>
      <td>QUEDE</td>
      <td>6</td>
      <td>2013-12-24</td>
      <td>2014-01-21</td>
      <td>2014-01-02</td>
      <td>1</td>
      <td>21.49</td>
      <td>Que Delícia</td>
      <td>Rua da Panificadora, 12</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>02389-673</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>547</td>
      <td>10795</td>
      <td>ERNSH</td>
      <td>8</td>
      <td>2013-12-24</td>
      <td>2014-01-21</td>
      <td>2014-01-20</td>
      <td>2</td>
      <td>126.66</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>548</td>
      <td>10796</td>
      <td>HILAA</td>
      <td>3</td>
      <td>2013-12-25</td>
      <td>2014-01-22</td>
      <td>2014-01-14</td>
      <td>1</td>
      <td>26.52</td>
      <td>HILARION-Abastos</td>
      <td>Carrera 22 con Ave. Carlos Soublette #8-35</td>
      <td>San Cristóbal</td>
      <td>South America</td>
      <td>5022</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>549</td>
      <td>10797</td>
      <td>DRACD</td>
      <td>7</td>
      <td>2013-12-25</td>
      <td>2014-01-22</td>
      <td>2014-01-05</td>
      <td>2</td>
      <td>33.35</td>
      <td>Drachenblut Delikatessen</td>
      <td>Walserweg 21</td>
      <td>Aachen</td>
      <td>Western Europe</td>
      <td>52066</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>550</td>
      <td>10798</td>
      <td>ISLAT</td>
      <td>2</td>
      <td>2013-12-26</td>
      <td>2014-01-23</td>
      <td>2014-01-05</td>
      <td>1</td>
      <td>2.33</td>
      <td>Island Trading</td>
      <td>Garden House Crowther Way</td>
      <td>Cowes</td>
      <td>British Isles</td>
      <td>PO31 7PJ</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>551</td>
      <td>10799</td>
      <td>KOENE</td>
      <td>9</td>
      <td>2013-12-26</td>
      <td>2014-02-06</td>
      <td>2014-01-05</td>
      <td>3</td>
      <td>30.76</td>
      <td>Königlich Essen</td>
      <td>Maubelstr. 90</td>
      <td>Brandenburg</td>
      <td>Western Europe</td>
      <td>14776</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>552</td>
      <td>10800</td>
      <td>SEVES</td>
      <td>1</td>
      <td>2013-12-26</td>
      <td>2014-01-23</td>
      <td>2014-01-05</td>
      <td>3</td>
      <td>137.44</td>
      <td>Seven Seas Imports</td>
      <td>90 Wadhurst Rd.</td>
      <td>London</td>
      <td>British Isles</td>
      <td>OX15 4NB</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>553</td>
      <td>10801</td>
      <td>BOLID</td>
      <td>4</td>
      <td>2013-12-29</td>
      <td>2014-01-26</td>
      <td>2013-12-31</td>
      <td>2</td>
      <td>97.09</td>
      <td>Bólido Comidas preparadas</td>
      <td>C/ Araquil, 67</td>
      <td>Madrid</td>
      <td>Southern Europe</td>
      <td>28023</td>
      <td>Spain</td>
    </tr>
    <tr>
      <td>554</td>
      <td>10802</td>
      <td>SIMOB</td>
      <td>4</td>
      <td>2013-12-29</td>
      <td>2014-01-26</td>
      <td>2014-01-02</td>
      <td>2</td>
      <td>257.26</td>
      <td>Simons bistro</td>
      <td>Vinbæltet 34</td>
      <td>Kobenhavn</td>
      <td>Northern Europe</td>
      <td>1734</td>
      <td>Denmark</td>
    </tr>
    <tr>
      <td>555</td>
      <td>10803</td>
      <td>WELLI</td>
      <td>4</td>
      <td>2013-12-30</td>
      <td>2014-01-27</td>
      <td>2014-01-06</td>
      <td>1</td>
      <td>55.23</td>
      <td>Wellington Importadora</td>
      <td>Rua do Mercado, 12</td>
      <td>Resende</td>
      <td>South America</td>
      <td>08737-363</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>556</td>
      <td>10804</td>
      <td>SEVES</td>
      <td>6</td>
      <td>2013-12-30</td>
      <td>2014-01-27</td>
      <td>2014-01-07</td>
      <td>2</td>
      <td>27.33</td>
      <td>Seven Seas Imports</td>
      <td>90 Wadhurst Rd.</td>
      <td>London</td>
      <td>British Isles</td>
      <td>OX15 4NB</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>557</td>
      <td>10805</td>
      <td>THEBI</td>
      <td>2</td>
      <td>2013-12-30</td>
      <td>2014-01-27</td>
      <td>2014-01-09</td>
      <td>3</td>
      <td>237.34</td>
      <td>The Big Cheese</td>
      <td>89 Jefferson Way Suite 2</td>
      <td>Portland</td>
      <td>North America</td>
      <td>97201</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>558</td>
      <td>10806</td>
      <td>VICTE</td>
      <td>3</td>
      <td>2013-12-31</td>
      <td>2014-01-28</td>
      <td>2014-01-05</td>
      <td>2</td>
      <td>22.11</td>
      <td>Victuailles en stock</td>
      <td>2, rue du Commerce</td>
      <td>Lyon</td>
      <td>Western Europe</td>
      <td>69004</td>
      <td>France</td>
    </tr>
    <tr>
      <td>559</td>
      <td>10807</td>
      <td>FRANS</td>
      <td>4</td>
      <td>2013-12-31</td>
      <td>2014-01-28</td>
      <td>2014-01-30</td>
      <td>1</td>
      <td>1.36</td>
      <td>Franchi S.p.A.</td>
      <td>Via Monte Bianco 34</td>
      <td>Torino</td>
      <td>Southern Europe</td>
      <td>10100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>560</td>
      <td>10808</td>
      <td>OLDWO</td>
      <td>2</td>
      <td>2014-01-01</td>
      <td>2014-01-29</td>
      <td>2014-01-09</td>
      <td>3</td>
      <td>45.53</td>
      <td>Old World Delicatessen</td>
      <td>2743 Bering St.</td>
      <td>Anchorage</td>
      <td>North America</td>
      <td>99508</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>561</td>
      <td>10809</td>
      <td>WELLI</td>
      <td>7</td>
      <td>2014-01-01</td>
      <td>2014-01-29</td>
      <td>2014-01-07</td>
      <td>1</td>
      <td>4.87</td>
      <td>Wellington Importadora</td>
      <td>Rua do Mercado, 12</td>
      <td>Resende</td>
      <td>South America</td>
      <td>08737-363</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>562</td>
      <td>10810</td>
      <td>LAUGB</td>
      <td>2</td>
      <td>2014-01-01</td>
      <td>2014-01-29</td>
      <td>2014-01-07</td>
      <td>3</td>
      <td>4.33</td>
      <td>Laughing Bacchus Wine Cellars</td>
      <td>2319 Elm St.</td>
      <td>Vancouver</td>
      <td>North America</td>
      <td>V3F 2K1</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>563</td>
      <td>10811</td>
      <td>LINOD</td>
      <td>8</td>
      <td>2014-01-02</td>
      <td>2014-01-30</td>
      <td>2014-01-08</td>
      <td>1</td>
      <td>31.22</td>
      <td>LINO-Delicateses</td>
      <td>Ave. 5 de Mayo Porlamar</td>
      <td>I. de Margarita</td>
      <td>South America</td>
      <td>4980</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>564</td>
      <td>10812</td>
      <td>REGGC</td>
      <td>5</td>
      <td>2014-01-02</td>
      <td>2014-01-30</td>
      <td>2014-01-12</td>
      <td>1</td>
      <td>59.78</td>
      <td>Reggiani Caseifici</td>
      <td>Strada Provinciale 124</td>
      <td>Reggio Emilia</td>
      <td>Southern Europe</td>
      <td>42100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>565</td>
      <td>10813</td>
      <td>RICAR</td>
      <td>1</td>
      <td>2014-01-05</td>
      <td>2014-02-02</td>
      <td>2014-01-09</td>
      <td>1</td>
      <td>47.38</td>
      <td>Ricardo Adocicados</td>
      <td>Av. Copacabana, 267</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>02389-890</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>566</td>
      <td>10814</td>
      <td>VICTE</td>
      <td>3</td>
      <td>2014-01-05</td>
      <td>2014-02-02</td>
      <td>2014-01-14</td>
      <td>3</td>
      <td>130.94</td>
      <td>Victuailles en stock</td>
      <td>2, rue du Commerce</td>
      <td>Lyon</td>
      <td>Western Europe</td>
      <td>69004</td>
      <td>France</td>
    </tr>
    <tr>
      <td>567</td>
      <td>10815</td>
      <td>SAVEA</td>
      <td>2</td>
      <td>2014-01-05</td>
      <td>2014-02-02</td>
      <td>2014-01-14</td>
      <td>3</td>
      <td>14.62</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>568</td>
      <td>10816</td>
      <td>GREAL</td>
      <td>4</td>
      <td>2014-01-06</td>
      <td>2014-02-03</td>
      <td>2014-02-04</td>
      <td>2</td>
      <td>719.78</td>
      <td>Great Lakes Food Market</td>
      <td>2732 Baker Blvd.</td>
      <td>Eugene</td>
      <td>North America</td>
      <td>97403</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>569</td>
      <td>10817</td>
      <td>KOENE</td>
      <td>3</td>
      <td>2014-01-06</td>
      <td>2014-01-20</td>
      <td>2014-01-13</td>
      <td>2</td>
      <td>306.07</td>
      <td>Königlich Essen</td>
      <td>Maubelstr. 90</td>
      <td>Brandenburg</td>
      <td>Western Europe</td>
      <td>14776</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>570</td>
      <td>10818</td>
      <td>MAGAA</td>
      <td>7</td>
      <td>2014-01-07</td>
      <td>2014-02-04</td>
      <td>2014-01-12</td>
      <td>3</td>
      <td>65.48</td>
      <td>Magazzini Alimentari Riuniti</td>
      <td>Via Ludovico il Moro 22</td>
      <td>Bergamo</td>
      <td>Southern Europe</td>
      <td>24100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>571</td>
      <td>10819</td>
      <td>CACTU</td>
      <td>2</td>
      <td>2014-01-07</td>
      <td>2014-02-04</td>
      <td>2014-01-16</td>
      <td>3</td>
      <td>19.76</td>
      <td>Cactus Comidas para llevar</td>
      <td>Cerrito 333</td>
      <td>Buenos Aires</td>
      <td>South America</td>
      <td>1010</td>
      <td>Argentina</td>
    </tr>
    <tr>
      <td>572</td>
      <td>10820</td>
      <td>RATTC</td>
      <td>3</td>
      <td>2014-01-07</td>
      <td>2014-02-04</td>
      <td>2014-01-13</td>
      <td>2</td>
      <td>37.52</td>
      <td>Rattlesnake Canyon Grocery</td>
      <td>2817 Milton Dr.</td>
      <td>Albuquerque</td>
      <td>North America</td>
      <td>87110</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>573</td>
      <td>10821</td>
      <td>SPLIR</td>
      <td>1</td>
      <td>2014-01-08</td>
      <td>2014-02-05</td>
      <td>2014-01-15</td>
      <td>1</td>
      <td>36.68</td>
      <td>Split Rail Beer &amp; Ale</td>
      <td>P.O. Box 555</td>
      <td>Lander</td>
      <td>North America</td>
      <td>82520</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>574</td>
      <td>10822</td>
      <td>TRAIH</td>
      <td>6</td>
      <td>2014-01-08</td>
      <td>2014-02-05</td>
      <td>2014-01-16</td>
      <td>3</td>
      <td>7.00</td>
      <td>Trail's Head Gourmet Provisioners</td>
      <td>722 DaVinci Blvd.</td>
      <td>Kirkland</td>
      <td>North America</td>
      <td>98034</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>575</td>
      <td>10823</td>
      <td>LILAS</td>
      <td>5</td>
      <td>2014-01-09</td>
      <td>2014-02-06</td>
      <td>2014-01-13</td>
      <td>2</td>
      <td>163.97</td>
      <td>LILA-Supermercado</td>
      <td>Carrera 52 con Ave. Bolívar #65-98 Llano Largo</td>
      <td>Barquisimeto</td>
      <td>South America</td>
      <td>3508</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>576</td>
      <td>10824</td>
      <td>FOLKO</td>
      <td>8</td>
      <td>2014-01-09</td>
      <td>2014-02-06</td>
      <td>2014-01-30</td>
      <td>1</td>
      <td>1.23</td>
      <td>Folk och fä HB</td>
      <td>Åkergatan 24</td>
      <td>Bräcke</td>
      <td>Northern Europe</td>
      <td>S-844 67</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>577</td>
      <td>10825</td>
      <td>DRACD</td>
      <td>1</td>
      <td>2014-01-09</td>
      <td>2014-02-06</td>
      <td>2014-01-14</td>
      <td>1</td>
      <td>79.25</td>
      <td>Drachenblut Delikatessen</td>
      <td>Walserweg 21</td>
      <td>Aachen</td>
      <td>Western Europe</td>
      <td>52066</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>578</td>
      <td>10826</td>
      <td>BLONP</td>
      <td>6</td>
      <td>2014-01-12</td>
      <td>2014-02-09</td>
      <td>2014-02-06</td>
      <td>1</td>
      <td>7.09</td>
      <td>Blondel père et fils</td>
      <td>24, place Kléber</td>
      <td>Strasbourg</td>
      <td>Western Europe</td>
      <td>67000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>579</td>
      <td>10827</td>
      <td>BONAP</td>
      <td>1</td>
      <td>2014-01-12</td>
      <td>2014-01-26</td>
      <td>2014-02-06</td>
      <td>2</td>
      <td>63.54</td>
      <td>Bon app'</td>
      <td>12, rue des Bouchers</td>
      <td>Marseille</td>
      <td>Western Europe</td>
      <td>13008</td>
      <td>France</td>
    </tr>
    <tr>
      <td>580</td>
      <td>10828</td>
      <td>RANCH</td>
      <td>9</td>
      <td>2014-01-13</td>
      <td>2014-01-27</td>
      <td>2014-02-04</td>
      <td>1</td>
      <td>90.85</td>
      <td>Rancho grande</td>
      <td>Av. del Libertador 900</td>
      <td>Buenos Aires</td>
      <td>South America</td>
      <td>1010</td>
      <td>Argentina</td>
    </tr>
    <tr>
      <td>581</td>
      <td>10829</td>
      <td>ISLAT</td>
      <td>9</td>
      <td>2014-01-13</td>
      <td>2014-02-10</td>
      <td>2014-01-23</td>
      <td>1</td>
      <td>154.72</td>
      <td>Island Trading</td>
      <td>Garden House Crowther Way</td>
      <td>Cowes</td>
      <td>British Isles</td>
      <td>PO31 7PJ</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>582</td>
      <td>10830</td>
      <td>TRADH</td>
      <td>4</td>
      <td>2014-01-13</td>
      <td>2014-02-24</td>
      <td>2014-01-21</td>
      <td>2</td>
      <td>81.83</td>
      <td>Tradiçao Hipermercados</td>
      <td>Av. Inês de Castro, 414</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05634-030</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>583</td>
      <td>10831</td>
      <td>SANTG</td>
      <td>3</td>
      <td>2014-01-14</td>
      <td>2014-02-11</td>
      <td>2014-01-23</td>
      <td>2</td>
      <td>72.19</td>
      <td>Santé Gourmet</td>
      <td>Erling Skakkes gate 78</td>
      <td>Stavern</td>
      <td>Scandinavia</td>
      <td>4110</td>
      <td>Norway</td>
    </tr>
    <tr>
      <td>584</td>
      <td>10832</td>
      <td>LAMAI</td>
      <td>2</td>
      <td>2014-01-14</td>
      <td>2014-02-11</td>
      <td>2014-01-19</td>
      <td>2</td>
      <td>43.26</td>
      <td>La maison d'Asie</td>
      <td>1 rue Alsace-Lorraine</td>
      <td>Toulouse</td>
      <td>Western Europe</td>
      <td>31000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>585</td>
      <td>10833</td>
      <td>OTTIK</td>
      <td>6</td>
      <td>2014-01-15</td>
      <td>2014-02-12</td>
      <td>2014-01-23</td>
      <td>2</td>
      <td>71.49</td>
      <td>Ottilies Käseladen</td>
      <td>Mehrheimerstr. 369</td>
      <td>Köln</td>
      <td>Western Europe</td>
      <td>50739</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>586</td>
      <td>10834</td>
      <td>TRADH</td>
      <td>1</td>
      <td>2014-01-15</td>
      <td>2014-02-12</td>
      <td>2014-01-19</td>
      <td>3</td>
      <td>29.78</td>
      <td>Tradiçao Hipermercados</td>
      <td>Av. Inês de Castro, 414</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05634-030</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>587</td>
      <td>10835</td>
      <td>ALFKI</td>
      <td>1</td>
      <td>2014-01-15</td>
      <td>2014-02-12</td>
      <td>2014-01-21</td>
      <td>3</td>
      <td>69.53</td>
      <td>Alfred's Futterkiste</td>
      <td>Obere Str. 57</td>
      <td>Berlin</td>
      <td>Western Europe</td>
      <td>12209</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>588</td>
      <td>10836</td>
      <td>ERNSH</td>
      <td>7</td>
      <td>2014-01-16</td>
      <td>2014-02-13</td>
      <td>2014-01-21</td>
      <td>1</td>
      <td>411.88</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>589</td>
      <td>10837</td>
      <td>BERGS</td>
      <td>9</td>
      <td>2014-01-16</td>
      <td>2014-02-13</td>
      <td>2014-01-23</td>
      <td>3</td>
      <td>13.32</td>
      <td>Berglunds snabbköp</td>
      <td>Berguvsvägen  8</td>
      <td>Luleå</td>
      <td>Northern Europe</td>
      <td>S-958 22</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>590</td>
      <td>10838</td>
      <td>LINOD</td>
      <td>3</td>
      <td>2014-01-19</td>
      <td>2014-02-16</td>
      <td>2014-01-23</td>
      <td>3</td>
      <td>59.28</td>
      <td>LINO-Delicateses</td>
      <td>Ave. 5 de Mayo Porlamar</td>
      <td>I. de Margarita</td>
      <td>South America</td>
      <td>4980</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>591</td>
      <td>10839</td>
      <td>TRADH</td>
      <td>3</td>
      <td>2014-01-19</td>
      <td>2014-02-16</td>
      <td>2014-01-22</td>
      <td>3</td>
      <td>35.43</td>
      <td>Tradiçao Hipermercados</td>
      <td>Av. Inês de Castro, 414</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05634-030</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>592</td>
      <td>10840</td>
      <td>LINOD</td>
      <td>4</td>
      <td>2014-01-19</td>
      <td>2014-03-02</td>
      <td>2014-02-16</td>
      <td>2</td>
      <td>2.71</td>
      <td>LINO-Delicateses</td>
      <td>Ave. 5 de Mayo Porlamar</td>
      <td>I. de Margarita</td>
      <td>South America</td>
      <td>4980</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>593</td>
      <td>10841</td>
      <td>SUPRD</td>
      <td>5</td>
      <td>2014-01-20</td>
      <td>2014-02-17</td>
      <td>2014-01-29</td>
      <td>2</td>
      <td>424.30</td>
      <td>Suprêmes délices</td>
      <td>Boulevard Tirou, 255</td>
      <td>Charleroi</td>
      <td>Western Europe</td>
      <td>B-6000</td>
      <td>Belgium</td>
    </tr>
    <tr>
      <td>594</td>
      <td>10842</td>
      <td>TORTU</td>
      <td>1</td>
      <td>2014-01-20</td>
      <td>2014-02-17</td>
      <td>2014-01-29</td>
      <td>3</td>
      <td>54.42</td>
      <td>Tortuga Restaurante</td>
      <td>Avda. Azteca 123</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05033</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>595</td>
      <td>10843</td>
      <td>VICTE</td>
      <td>4</td>
      <td>2014-01-21</td>
      <td>2014-02-18</td>
      <td>2014-01-26</td>
      <td>2</td>
      <td>9.26</td>
      <td>Victuailles en stock</td>
      <td>2, rue du Commerce</td>
      <td>Lyon</td>
      <td>Western Europe</td>
      <td>69004</td>
      <td>France</td>
    </tr>
    <tr>
      <td>596</td>
      <td>10844</td>
      <td>PICCO</td>
      <td>8</td>
      <td>2014-01-21</td>
      <td>2014-02-18</td>
      <td>2014-01-26</td>
      <td>2</td>
      <td>25.22</td>
      <td>Piccolo und mehr</td>
      <td>Geislweg 14</td>
      <td>Salzburg</td>
      <td>Western Europe</td>
      <td>5020</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>597</td>
      <td>10845</td>
      <td>QUICK</td>
      <td>8</td>
      <td>2014-01-21</td>
      <td>2014-02-04</td>
      <td>2014-01-30</td>
      <td>1</td>
      <td>212.98</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>598</td>
      <td>10846</td>
      <td>SUPRD</td>
      <td>2</td>
      <td>2014-01-22</td>
      <td>2014-03-05</td>
      <td>2014-01-23</td>
      <td>3</td>
      <td>56.46</td>
      <td>Suprêmes délices</td>
      <td>Boulevard Tirou, 255</td>
      <td>Charleroi</td>
      <td>Western Europe</td>
      <td>B-6000</td>
      <td>Belgium</td>
    </tr>
    <tr>
      <td>599</td>
      <td>10847</td>
      <td>SAVEA</td>
      <td>4</td>
      <td>2014-01-22</td>
      <td>2014-02-05</td>
      <td>2014-02-10</td>
      <td>3</td>
      <td>487.57</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>600</td>
      <td>10848</td>
      <td>CONSH</td>
      <td>7</td>
      <td>2014-01-23</td>
      <td>2014-02-20</td>
      <td>2014-01-29</td>
      <td>2</td>
      <td>38.24</td>
      <td>Consolidated Holdings</td>
      <td>Berkeley Gardens 12  Brewery</td>
      <td>London</td>
      <td>British Isles</td>
      <td>WX1 6LT</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>601</td>
      <td>10849</td>
      <td>KOENE</td>
      <td>9</td>
      <td>2014-01-23</td>
      <td>2014-02-20</td>
      <td>2014-01-30</td>
      <td>2</td>
      <td>0.56</td>
      <td>Königlich Essen</td>
      <td>Maubelstr. 90</td>
      <td>Brandenburg</td>
      <td>Western Europe</td>
      <td>14776</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>602</td>
      <td>10850</td>
      <td>VICTE</td>
      <td>1</td>
      <td>2014-01-23</td>
      <td>2014-03-06</td>
      <td>2014-01-30</td>
      <td>1</td>
      <td>49.19</td>
      <td>Victuailles en stock</td>
      <td>2, rue du Commerce</td>
      <td>Lyon</td>
      <td>Western Europe</td>
      <td>69004</td>
      <td>France</td>
    </tr>
    <tr>
      <td>603</td>
      <td>10851</td>
      <td>RICAR</td>
      <td>5</td>
      <td>2014-01-26</td>
      <td>2014-02-23</td>
      <td>2014-02-02</td>
      <td>1</td>
      <td>160.55</td>
      <td>Ricardo Adocicados</td>
      <td>Av. Copacabana, 267</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>02389-890</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>604</td>
      <td>10852</td>
      <td>RATTC</td>
      <td>8</td>
      <td>2014-01-26</td>
      <td>2014-02-09</td>
      <td>2014-01-30</td>
      <td>1</td>
      <td>174.05</td>
      <td>Rattlesnake Canyon Grocery</td>
      <td>2817 Milton Dr.</td>
      <td>Albuquerque</td>
      <td>North America</td>
      <td>87110</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>605</td>
      <td>10853</td>
      <td>BLAUS</td>
      <td>9</td>
      <td>2014-01-27</td>
      <td>2014-02-24</td>
      <td>2014-02-03</td>
      <td>2</td>
      <td>53.83</td>
      <td>Blauer See Delikatessen</td>
      <td>Forsterstr. 57</td>
      <td>Mannheim</td>
      <td>Western Europe</td>
      <td>68306</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>606</td>
      <td>10854</td>
      <td>ERNSH</td>
      <td>3</td>
      <td>2014-01-27</td>
      <td>2014-02-24</td>
      <td>2014-02-05</td>
      <td>2</td>
      <td>100.22</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>607</td>
      <td>10855</td>
      <td>OLDWO</td>
      <td>3</td>
      <td>2014-01-27</td>
      <td>2014-02-24</td>
      <td>2014-02-04</td>
      <td>1</td>
      <td>170.97</td>
      <td>Old World Delicatessen</td>
      <td>2743 Bering St.</td>
      <td>Anchorage</td>
      <td>North America</td>
      <td>99508</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>608</td>
      <td>10856</td>
      <td>ANTO</td>
      <td>3</td>
      <td>2014-01-28</td>
      <td>2014-02-25</td>
      <td>2014-02-10</td>
      <td>2</td>
      <td>58.43</td>
      <td>Antonio Moreno Taquería</td>
      <td>Mataderos  2312</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05023</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>609</td>
      <td>10857</td>
      <td>BERGS</td>
      <td>8</td>
      <td>2014-01-28</td>
      <td>2014-02-25</td>
      <td>2014-02-06</td>
      <td>2</td>
      <td>188.85</td>
      <td>Berglunds snabbköp</td>
      <td>Berguvsvägen  8</td>
      <td>Luleå</td>
      <td>Northern Europe</td>
      <td>S-958 22</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>610</td>
      <td>10858</td>
      <td>LACOR</td>
      <td>2</td>
      <td>2014-01-29</td>
      <td>2014-02-26</td>
      <td>2014-02-03</td>
      <td>1</td>
      <td>52.51</td>
      <td>La corne d'abondance</td>
      <td>67, avenue de l'Europe</td>
      <td>Versailles</td>
      <td>Western Europe</td>
      <td>78000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>611</td>
      <td>10859</td>
      <td>FRANK</td>
      <td>1</td>
      <td>2014-01-29</td>
      <td>2014-02-26</td>
      <td>2014-02-02</td>
      <td>2</td>
      <td>76.10</td>
      <td>Frankenversand</td>
      <td>Berliner Platz 43</td>
      <td>München</td>
      <td>Western Europe</td>
      <td>80805</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>612</td>
      <td>10860</td>
      <td>FRANR</td>
      <td>3</td>
      <td>2014-01-29</td>
      <td>2014-02-26</td>
      <td>2014-02-04</td>
      <td>3</td>
      <td>19.26</td>
      <td>France restauration</td>
      <td>54, rue Royale</td>
      <td>Nantes</td>
      <td>Western Europe</td>
      <td>44000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>613</td>
      <td>10861</td>
      <td>WHITC</td>
      <td>4</td>
      <td>2014-01-30</td>
      <td>2014-02-27</td>
      <td>2014-02-17</td>
      <td>2</td>
      <td>14.93</td>
      <td>White Clover Markets</td>
      <td>1029 - 12th Ave. S.</td>
      <td>Seattle</td>
      <td>North America</td>
      <td>98124</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>614</td>
      <td>10862</td>
      <td>LEHMS</td>
      <td>8</td>
      <td>2014-01-30</td>
      <td>2014-03-13</td>
      <td>2014-02-02</td>
      <td>2</td>
      <td>53.23</td>
      <td>Lehmanns Marktstand</td>
      <td>Magazinweg 7</td>
      <td>Frankfurt a.M.</td>
      <td>Western Europe</td>
      <td>60528</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>615</td>
      <td>10863</td>
      <td>HILAA</td>
      <td>4</td>
      <td>2014-02-02</td>
      <td>2014-03-02</td>
      <td>2014-02-17</td>
      <td>2</td>
      <td>30.26</td>
      <td>HILARION-Abastos</td>
      <td>Carrera 22 con Ave. Carlos Soublette #8-35</td>
      <td>San Cristóbal</td>
      <td>South America</td>
      <td>5022</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>616</td>
      <td>10864</td>
      <td>AROUT</td>
      <td>4</td>
      <td>2014-02-02</td>
      <td>2014-03-02</td>
      <td>2014-02-09</td>
      <td>2</td>
      <td>3.04</td>
      <td>Around the Horn</td>
      <td>Brook Farm Stratford St. Mary</td>
      <td>Colchester</td>
      <td>British Isles</td>
      <td>CO7 6JX</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>617</td>
      <td>10865</td>
      <td>QUICK</td>
      <td>2</td>
      <td>2014-02-02</td>
      <td>2014-02-16</td>
      <td>2014-02-12</td>
      <td>1</td>
      <td>348.14</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>618</td>
      <td>10866</td>
      <td>BERGS</td>
      <td>5</td>
      <td>2014-02-03</td>
      <td>2014-03-03</td>
      <td>2014-02-12</td>
      <td>1</td>
      <td>109.11</td>
      <td>Berglunds snabbköp</td>
      <td>Berguvsvägen  8</td>
      <td>Luleå</td>
      <td>Northern Europe</td>
      <td>S-958 22</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>619</td>
      <td>10867</td>
      <td>LONEP</td>
      <td>6</td>
      <td>2014-02-03</td>
      <td>2014-03-17</td>
      <td>2014-02-11</td>
      <td>1</td>
      <td>1.93</td>
      <td>Lonesome Pine Restaurant</td>
      <td>89 Chiaroscuro Rd.</td>
      <td>Portland</td>
      <td>North America</td>
      <td>97219</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>620</td>
      <td>10868</td>
      <td>QUEE</td>
      <td>7</td>
      <td>2014-02-04</td>
      <td>2014-03-04</td>
      <td>2014-02-23</td>
      <td>2</td>
      <td>191.27</td>
      <td>Queen Cozinha</td>
      <td>Alameda dos Canàrios, 891</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05487-020</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>621</td>
      <td>10869</td>
      <td>SEVES</td>
      <td>5</td>
      <td>2014-02-04</td>
      <td>2014-03-04</td>
      <td>2014-02-09</td>
      <td>1</td>
      <td>143.28</td>
      <td>Seven Seas Imports</td>
      <td>90 Wadhurst Rd.</td>
      <td>London</td>
      <td>British Isles</td>
      <td>OX15 4NB</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>622</td>
      <td>10870</td>
      <td>WOLZA</td>
      <td>5</td>
      <td>2014-02-04</td>
      <td>2014-03-04</td>
      <td>2014-02-13</td>
      <td>3</td>
      <td>12.04</td>
      <td>Wolski Zajazd</td>
      <td>ul. Filtrowa 68</td>
      <td>Warszawa</td>
      <td>Eastern Europe</td>
      <td>01-012</td>
      <td>Poland</td>
    </tr>
    <tr>
      <td>623</td>
      <td>10871</td>
      <td>BONAP</td>
      <td>9</td>
      <td>2014-02-05</td>
      <td>2014-03-05</td>
      <td>2014-02-10</td>
      <td>2</td>
      <td>112.27</td>
      <td>Bon app'</td>
      <td>12, rue des Bouchers</td>
      <td>Marseille</td>
      <td>Western Europe</td>
      <td>13008</td>
      <td>France</td>
    </tr>
    <tr>
      <td>624</td>
      <td>10872</td>
      <td>GODOS</td>
      <td>5</td>
      <td>2014-02-05</td>
      <td>2014-03-05</td>
      <td>2014-02-09</td>
      <td>2</td>
      <td>175.32</td>
      <td>Godos Cocina Típica</td>
      <td>C/ Romero, 33</td>
      <td>Sevilla</td>
      <td>Southern Europe</td>
      <td>41101</td>
      <td>Spain</td>
    </tr>
    <tr>
      <td>625</td>
      <td>10873</td>
      <td>WILMK</td>
      <td>4</td>
      <td>2014-02-06</td>
      <td>2014-03-06</td>
      <td>2014-02-09</td>
      <td>1</td>
      <td>0.82</td>
      <td>Wilman Kala</td>
      <td>Keskuskatu 45</td>
      <td>Helsinki</td>
      <td>Scandinavia</td>
      <td>21240</td>
      <td>Finland</td>
    </tr>
    <tr>
      <td>626</td>
      <td>10874</td>
      <td>GODOS</td>
      <td>5</td>
      <td>2014-02-06</td>
      <td>2014-03-06</td>
      <td>2014-02-11</td>
      <td>2</td>
      <td>19.58</td>
      <td>Godos Cocina Típica</td>
      <td>C/ Romero, 33</td>
      <td>Sevilla</td>
      <td>Southern Europe</td>
      <td>41101</td>
      <td>Spain</td>
    </tr>
    <tr>
      <td>627</td>
      <td>10875</td>
      <td>BERGS</td>
      <td>4</td>
      <td>2014-02-06</td>
      <td>2014-03-06</td>
      <td>2014-03-03</td>
      <td>2</td>
      <td>32.37</td>
      <td>Berglunds snabbköp</td>
      <td>Berguvsvägen  8</td>
      <td>Luleå</td>
      <td>Northern Europe</td>
      <td>S-958 22</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>628</td>
      <td>10876</td>
      <td>BONAP</td>
      <td>7</td>
      <td>2014-02-09</td>
      <td>2014-03-09</td>
      <td>2014-02-12</td>
      <td>3</td>
      <td>60.42</td>
      <td>Bon app'</td>
      <td>12, rue des Bouchers</td>
      <td>Marseille</td>
      <td>Western Europe</td>
      <td>13008</td>
      <td>France</td>
    </tr>
    <tr>
      <td>629</td>
      <td>10877</td>
      <td>RICAR</td>
      <td>1</td>
      <td>2014-02-09</td>
      <td>2014-03-09</td>
      <td>2014-02-19</td>
      <td>1</td>
      <td>38.06</td>
      <td>Ricardo Adocicados</td>
      <td>Av. Copacabana, 267</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>02389-890</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>630</td>
      <td>10878</td>
      <td>QUICK</td>
      <td>4</td>
      <td>2014-02-10</td>
      <td>2014-03-10</td>
      <td>2014-02-12</td>
      <td>1</td>
      <td>46.69</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>631</td>
      <td>10879</td>
      <td>WILMK</td>
      <td>3</td>
      <td>2014-02-10</td>
      <td>2014-03-10</td>
      <td>2014-02-12</td>
      <td>3</td>
      <td>8.50</td>
      <td>Wilman Kala</td>
      <td>Keskuskatu 45</td>
      <td>Helsinki</td>
      <td>Scandinavia</td>
      <td>21240</td>
      <td>Finland</td>
    </tr>
    <tr>
      <td>632</td>
      <td>10880</td>
      <td>FOLKO</td>
      <td>7</td>
      <td>2014-02-10</td>
      <td>2014-03-24</td>
      <td>2014-02-18</td>
      <td>1</td>
      <td>88.01</td>
      <td>Folk och fä HB</td>
      <td>Åkergatan 24</td>
      <td>Bräcke</td>
      <td>Northern Europe</td>
      <td>S-844 67</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>633</td>
      <td>10881</td>
      <td>CACTU</td>
      <td>4</td>
      <td>2014-02-11</td>
      <td>2014-03-11</td>
      <td>2014-02-18</td>
      <td>1</td>
      <td>2.84</td>
      <td>Cactus Comidas para llevar</td>
      <td>Cerrito 333</td>
      <td>Buenos Aires</td>
      <td>South America</td>
      <td>1010</td>
      <td>Argentina</td>
    </tr>
    <tr>
      <td>634</td>
      <td>10882</td>
      <td>SAVEA</td>
      <td>4</td>
      <td>2014-02-11</td>
      <td>2014-03-11</td>
      <td>2014-02-20</td>
      <td>3</td>
      <td>23.10</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>635</td>
      <td>10883</td>
      <td>LONEP</td>
      <td>8</td>
      <td>2014-02-12</td>
      <td>2014-03-12</td>
      <td>2014-02-20</td>
      <td>3</td>
      <td>0.53</td>
      <td>Lonesome Pine Restaurant</td>
      <td>89 Chiaroscuro Rd.</td>
      <td>Portland</td>
      <td>North America</td>
      <td>97219</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>636</td>
      <td>10884</td>
      <td>LETSS</td>
      <td>4</td>
      <td>2014-02-12</td>
      <td>2014-03-12</td>
      <td>2014-02-13</td>
      <td>2</td>
      <td>90.97</td>
      <td>Let's Stop N Shop</td>
      <td>87 Polk St. Suite 5</td>
      <td>San Francisco</td>
      <td>North America</td>
      <td>94117</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>637</td>
      <td>10885</td>
      <td>SUPRD</td>
      <td>6</td>
      <td>2014-02-12</td>
      <td>2014-03-12</td>
      <td>2014-02-18</td>
      <td>3</td>
      <td>5.64</td>
      <td>Suprêmes délices</td>
      <td>Boulevard Tirou, 255</td>
      <td>Charleroi</td>
      <td>Western Europe</td>
      <td>B-6000</td>
      <td>Belgium</td>
    </tr>
    <tr>
      <td>638</td>
      <td>10886</td>
      <td>HANAR</td>
      <td>1</td>
      <td>2014-02-13</td>
      <td>2014-03-13</td>
      <td>2014-03-02</td>
      <td>1</td>
      <td>4.99</td>
      <td>Hanari Carnes</td>
      <td>Rua do Paço, 67</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>05454-876</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>639</td>
      <td>10887</td>
      <td>GALED</td>
      <td>8</td>
      <td>2014-02-13</td>
      <td>2014-03-13</td>
      <td>2014-02-16</td>
      <td>3</td>
      <td>1.25</td>
      <td>Galería del gastronómo</td>
      <td>Rambla de Cataluña, 23</td>
      <td>Barcelona</td>
      <td>Southern Europe</td>
      <td>8022</td>
      <td>Spain</td>
    </tr>
    <tr>
      <td>640</td>
      <td>10888</td>
      <td>GODOS</td>
      <td>1</td>
      <td>2014-02-16</td>
      <td>2014-03-16</td>
      <td>2014-02-23</td>
      <td>2</td>
      <td>51.87</td>
      <td>Godos Cocina Típica</td>
      <td>C/ Romero, 33</td>
      <td>Sevilla</td>
      <td>Southern Europe</td>
      <td>41101</td>
      <td>Spain</td>
    </tr>
    <tr>
      <td>641</td>
      <td>10889</td>
      <td>RATTC</td>
      <td>9</td>
      <td>2014-02-16</td>
      <td>2014-03-16</td>
      <td>2014-02-23</td>
      <td>3</td>
      <td>280.61</td>
      <td>Rattlesnake Canyon Grocery</td>
      <td>2817 Milton Dr.</td>
      <td>Albuquerque</td>
      <td>North America</td>
      <td>87110</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>642</td>
      <td>10890</td>
      <td>DUMO</td>
      <td>7</td>
      <td>2014-02-16</td>
      <td>2014-03-16</td>
      <td>2014-02-18</td>
      <td>1</td>
      <td>32.76</td>
      <td>Du monde entier</td>
      <td>67, rue des Cinquante Otages</td>
      <td>Nantes</td>
      <td>Western Europe</td>
      <td>44000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>643</td>
      <td>10891</td>
      <td>LEHMS</td>
      <td>7</td>
      <td>2014-02-17</td>
      <td>2014-03-17</td>
      <td>2014-02-19</td>
      <td>2</td>
      <td>20.37</td>
      <td>Lehmanns Marktstand</td>
      <td>Magazinweg 7</td>
      <td>Frankfurt a.M.</td>
      <td>Western Europe</td>
      <td>60528</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>644</td>
      <td>10892</td>
      <td>MAISD</td>
      <td>4</td>
      <td>2014-02-17</td>
      <td>2014-03-17</td>
      <td>2014-02-19</td>
      <td>2</td>
      <td>120.27</td>
      <td>Maison Dewey</td>
      <td>Rue Joseph-Bens 532</td>
      <td>Bruxelles</td>
      <td>Western Europe</td>
      <td>B-1180</td>
      <td>Belgium</td>
    </tr>
    <tr>
      <td>645</td>
      <td>10893</td>
      <td>KOENE</td>
      <td>9</td>
      <td>2014-02-18</td>
      <td>2014-03-18</td>
      <td>2014-02-20</td>
      <td>2</td>
      <td>77.78</td>
      <td>Königlich Essen</td>
      <td>Maubelstr. 90</td>
      <td>Brandenburg</td>
      <td>Western Europe</td>
      <td>14776</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>646</td>
      <td>10894</td>
      <td>SAVEA</td>
      <td>1</td>
      <td>2014-02-18</td>
      <td>2014-03-18</td>
      <td>2014-02-20</td>
      <td>1</td>
      <td>116.13</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>647</td>
      <td>10895</td>
      <td>ERNSH</td>
      <td>3</td>
      <td>2014-02-18</td>
      <td>2014-03-18</td>
      <td>2014-02-23</td>
      <td>1</td>
      <td>162.75</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>648</td>
      <td>10896</td>
      <td>MAISD</td>
      <td>7</td>
      <td>2014-02-19</td>
      <td>2014-03-19</td>
      <td>2014-02-27</td>
      <td>3</td>
      <td>32.45</td>
      <td>Maison Dewey</td>
      <td>Rue Joseph-Bens 532</td>
      <td>Bruxelles</td>
      <td>Western Europe</td>
      <td>B-1180</td>
      <td>Belgium</td>
    </tr>
    <tr>
      <td>649</td>
      <td>10897</td>
      <td>HUNGO</td>
      <td>3</td>
      <td>2014-02-19</td>
      <td>2014-03-19</td>
      <td>2014-02-25</td>
      <td>2</td>
      <td>603.54</td>
      <td>Hungry Owl All-Night Grocers</td>
      <td>8 Johnstown Road</td>
      <td>Cork</td>
      <td>British Isles</td>
      <td>None</td>
      <td>Ireland</td>
    </tr>
    <tr>
      <td>650</td>
      <td>10898</td>
      <td>OCEA</td>
      <td>4</td>
      <td>2014-02-20</td>
      <td>2014-03-20</td>
      <td>2014-03-06</td>
      <td>2</td>
      <td>1.27</td>
      <td>Océano Atlántico Ltda.</td>
      <td>Ing. Gustavo Moncada 8585 Piso 20-A</td>
      <td>Buenos Aires</td>
      <td>South America</td>
      <td>1010</td>
      <td>Argentina</td>
    </tr>
    <tr>
      <td>651</td>
      <td>10899</td>
      <td>LILAS</td>
      <td>5</td>
      <td>2014-02-20</td>
      <td>2014-03-20</td>
      <td>2014-02-26</td>
      <td>3</td>
      <td>1.21</td>
      <td>LILA-Supermercado</td>
      <td>Carrera 52 con Ave. Bolívar #65-98 Llano Largo</td>
      <td>Barquisimeto</td>
      <td>South America</td>
      <td>3508</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>652</td>
      <td>10900</td>
      <td>WELLI</td>
      <td>1</td>
      <td>2014-02-20</td>
      <td>2014-03-20</td>
      <td>2014-03-04</td>
      <td>2</td>
      <td>1.66</td>
      <td>Wellington Importadora</td>
      <td>Rua do Mercado, 12</td>
      <td>Resende</td>
      <td>South America</td>
      <td>08737-363</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>653</td>
      <td>10901</td>
      <td>HILAA</td>
      <td>4</td>
      <td>2014-02-23</td>
      <td>2014-03-23</td>
      <td>2014-02-26</td>
      <td>1</td>
      <td>62.09</td>
      <td>HILARION-Abastos</td>
      <td>Carrera 22 con Ave. Carlos Soublette #8-35</td>
      <td>San Cristóbal</td>
      <td>South America</td>
      <td>5022</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>654</td>
      <td>10902</td>
      <td>FOLKO</td>
      <td>1</td>
      <td>2014-02-23</td>
      <td>2014-03-23</td>
      <td>2014-03-03</td>
      <td>1</td>
      <td>44.15</td>
      <td>Folk och fä HB</td>
      <td>Åkergatan 24</td>
      <td>Bräcke</td>
      <td>Northern Europe</td>
      <td>S-844 67</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>655</td>
      <td>10903</td>
      <td>HANAR</td>
      <td>3</td>
      <td>2014-02-24</td>
      <td>2014-03-24</td>
      <td>2014-03-04</td>
      <td>3</td>
      <td>36.71</td>
      <td>Hanari Carnes</td>
      <td>Rua do Paço, 67</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>05454-876</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>656</td>
      <td>10904</td>
      <td>WHITC</td>
      <td>3</td>
      <td>2014-02-24</td>
      <td>2014-03-24</td>
      <td>2014-02-27</td>
      <td>3</td>
      <td>162.95</td>
      <td>White Clover Markets</td>
      <td>1029 - 12th Ave. S.</td>
      <td>Seattle</td>
      <td>North America</td>
      <td>98124</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>657</td>
      <td>10905</td>
      <td>WELLI</td>
      <td>9</td>
      <td>2014-02-24</td>
      <td>2014-03-24</td>
      <td>2014-03-06</td>
      <td>2</td>
      <td>13.72</td>
      <td>Wellington Importadora</td>
      <td>Rua do Mercado, 12</td>
      <td>Resende</td>
      <td>South America</td>
      <td>08737-363</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>658</td>
      <td>10906</td>
      <td>WOLZA</td>
      <td>4</td>
      <td>2014-02-25</td>
      <td>2014-03-11</td>
      <td>2014-03-03</td>
      <td>3</td>
      <td>26.29</td>
      <td>Wolski Zajazd</td>
      <td>ul. Filtrowa 68</td>
      <td>Warszawa</td>
      <td>Eastern Europe</td>
      <td>01-012</td>
      <td>Poland</td>
    </tr>
    <tr>
      <td>659</td>
      <td>10907</td>
      <td>SPECD</td>
      <td>6</td>
      <td>2014-02-25</td>
      <td>2014-03-25</td>
      <td>2014-02-27</td>
      <td>3</td>
      <td>9.19</td>
      <td>Spécialités du monde</td>
      <td>25, rue Lauriston</td>
      <td>Paris</td>
      <td>Western Europe</td>
      <td>75016</td>
      <td>France</td>
    </tr>
    <tr>
      <td>660</td>
      <td>10908</td>
      <td>REGGC</td>
      <td>4</td>
      <td>2014-02-26</td>
      <td>2014-03-26</td>
      <td>2014-03-06</td>
      <td>2</td>
      <td>32.96</td>
      <td>Reggiani Caseifici</td>
      <td>Strada Provinciale 124</td>
      <td>Reggio Emilia</td>
      <td>Southern Europe</td>
      <td>42100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>661</td>
      <td>10909</td>
      <td>SANTG</td>
      <td>1</td>
      <td>2014-02-26</td>
      <td>2014-03-26</td>
      <td>2014-03-10</td>
      <td>2</td>
      <td>53.05</td>
      <td>Santé Gourmet</td>
      <td>Erling Skakkes gate 78</td>
      <td>Stavern</td>
      <td>Scandinavia</td>
      <td>4110</td>
      <td>Norway</td>
    </tr>
    <tr>
      <td>662</td>
      <td>10910</td>
      <td>WILMK</td>
      <td>1</td>
      <td>2014-02-26</td>
      <td>2014-03-26</td>
      <td>2014-03-04</td>
      <td>3</td>
      <td>38.11</td>
      <td>Wilman Kala</td>
      <td>Keskuskatu 45</td>
      <td>Helsinki</td>
      <td>Scandinavia</td>
      <td>21240</td>
      <td>Finland</td>
    </tr>
    <tr>
      <td>663</td>
      <td>10911</td>
      <td>GODOS</td>
      <td>3</td>
      <td>2014-02-26</td>
      <td>2014-03-26</td>
      <td>2014-03-05</td>
      <td>1</td>
      <td>38.19</td>
      <td>Godos Cocina Típica</td>
      <td>C/ Romero, 33</td>
      <td>Sevilla</td>
      <td>Southern Europe</td>
      <td>41101</td>
      <td>Spain</td>
    </tr>
    <tr>
      <td>664</td>
      <td>10912</td>
      <td>HUNGO</td>
      <td>2</td>
      <td>2014-02-26</td>
      <td>2014-03-26</td>
      <td>2014-03-18</td>
      <td>2</td>
      <td>580.91</td>
      <td>Hungry Owl All-Night Grocers</td>
      <td>8 Johnstown Road</td>
      <td>Cork</td>
      <td>British Isles</td>
      <td>None</td>
      <td>Ireland</td>
    </tr>
    <tr>
      <td>665</td>
      <td>10913</td>
      <td>QUEE</td>
      <td>4</td>
      <td>2014-02-26</td>
      <td>2014-03-26</td>
      <td>2014-03-04</td>
      <td>1</td>
      <td>33.05</td>
      <td>Queen Cozinha</td>
      <td>Alameda dos Canàrios, 891</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05487-020</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>666</td>
      <td>10914</td>
      <td>QUEE</td>
      <td>6</td>
      <td>2014-02-27</td>
      <td>2014-03-27</td>
      <td>2014-03-02</td>
      <td>1</td>
      <td>21.19</td>
      <td>Queen Cozinha</td>
      <td>Alameda dos Canàrios, 891</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05487-020</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>667</td>
      <td>10915</td>
      <td>TORTU</td>
      <td>2</td>
      <td>2014-02-27</td>
      <td>2014-03-27</td>
      <td>2014-03-02</td>
      <td>2</td>
      <td>3.51</td>
      <td>Tortuga Restaurante</td>
      <td>Avda. Azteca 123</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05033</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>668</td>
      <td>10916</td>
      <td>RANCH</td>
      <td>1</td>
      <td>2014-02-27</td>
      <td>2014-03-27</td>
      <td>2014-03-09</td>
      <td>2</td>
      <td>63.77</td>
      <td>Rancho grande</td>
      <td>Av. del Libertador 900</td>
      <td>Buenos Aires</td>
      <td>South America</td>
      <td>1010</td>
      <td>Argentina</td>
    </tr>
    <tr>
      <td>669</td>
      <td>10917</td>
      <td>ROMEY</td>
      <td>4</td>
      <td>2014-03-02</td>
      <td>2014-03-30</td>
      <td>2014-03-11</td>
      <td>2</td>
      <td>8.29</td>
      <td>Romero y tomillo</td>
      <td>Gran Vía, 1</td>
      <td>Madrid</td>
      <td>Southern Europe</td>
      <td>28001</td>
      <td>Spain</td>
    </tr>
    <tr>
      <td>670</td>
      <td>10918</td>
      <td>BOTTM</td>
      <td>3</td>
      <td>2014-03-02</td>
      <td>2014-03-30</td>
      <td>2014-03-11</td>
      <td>3</td>
      <td>48.83</td>
      <td>Bottom-Dollar Markets</td>
      <td>23 Tsawassen Blvd.</td>
      <td>Tsawassen</td>
      <td>North America</td>
      <td>T2F 8M4</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>671</td>
      <td>10919</td>
      <td>LINOD</td>
      <td>2</td>
      <td>2014-03-02</td>
      <td>2014-03-30</td>
      <td>2014-03-04</td>
      <td>2</td>
      <td>19.80</td>
      <td>LINO-Delicateses</td>
      <td>Ave. 5 de Mayo Porlamar</td>
      <td>I. de Margarita</td>
      <td>South America</td>
      <td>4980</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>672</td>
      <td>10920</td>
      <td>AROUT</td>
      <td>4</td>
      <td>2014-03-03</td>
      <td>2014-03-31</td>
      <td>2014-03-09</td>
      <td>2</td>
      <td>29.61</td>
      <td>Around the Horn</td>
      <td>Brook Farm Stratford St. Mary</td>
      <td>Colchester</td>
      <td>British Isles</td>
      <td>CO7 6JX</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>673</td>
      <td>10921</td>
      <td>VAFFE</td>
      <td>1</td>
      <td>2014-03-03</td>
      <td>2014-04-14</td>
      <td>2014-03-09</td>
      <td>1</td>
      <td>176.48</td>
      <td>Vaffeljernet</td>
      <td>Smagsloget 45</td>
      <td>Århus</td>
      <td>Northern Europe</td>
      <td>8200</td>
      <td>Denmark</td>
    </tr>
    <tr>
      <td>674</td>
      <td>10922</td>
      <td>HANAR</td>
      <td>5</td>
      <td>2014-03-03</td>
      <td>2014-03-31</td>
      <td>2014-03-05</td>
      <td>3</td>
      <td>62.74</td>
      <td>Hanari Carnes</td>
      <td>Rua do Paço, 67</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>05454-876</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>675</td>
      <td>10923</td>
      <td>LAMAI</td>
      <td>7</td>
      <td>2014-03-03</td>
      <td>2014-04-14</td>
      <td>2014-03-13</td>
      <td>3</td>
      <td>68.26</td>
      <td>La maison d'Asie</td>
      <td>1 rue Alsace-Lorraine</td>
      <td>Toulouse</td>
      <td>Western Europe</td>
      <td>31000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>676</td>
      <td>10924</td>
      <td>BERGS</td>
      <td>3</td>
      <td>2014-03-04</td>
      <td>2014-04-01</td>
      <td>2014-04-08</td>
      <td>2</td>
      <td>151.52</td>
      <td>Berglunds snabbköp</td>
      <td>Berguvsvägen  8</td>
      <td>Luleå</td>
      <td>Northern Europe</td>
      <td>S-958 22</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>677</td>
      <td>10925</td>
      <td>HANAR</td>
      <td>3</td>
      <td>2014-03-04</td>
      <td>2014-04-01</td>
      <td>2014-03-13</td>
      <td>1</td>
      <td>2.27</td>
      <td>Hanari Carnes</td>
      <td>Rua do Paço, 67</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>05454-876</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>678</td>
      <td>10926</td>
      <td>ANATR</td>
      <td>4</td>
      <td>2014-03-04</td>
      <td>2014-04-01</td>
      <td>2014-03-11</td>
      <td>3</td>
      <td>39.92</td>
      <td>Ana Trujillo Emparedados y helados</td>
      <td>Avda. de la Constitución 2222</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05021</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>679</td>
      <td>10927</td>
      <td>LACOR</td>
      <td>4</td>
      <td>2014-03-05</td>
      <td>2014-04-02</td>
      <td>2014-04-08</td>
      <td>1</td>
      <td>19.79</td>
      <td>La corne d'abondance</td>
      <td>67, avenue de l'Europe</td>
      <td>Versailles</td>
      <td>Western Europe</td>
      <td>78000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>680</td>
      <td>10928</td>
      <td>GALED</td>
      <td>1</td>
      <td>2014-03-05</td>
      <td>2014-04-02</td>
      <td>2014-03-18</td>
      <td>1</td>
      <td>1.36</td>
      <td>Galería del gastronómo</td>
      <td>Rambla de Cataluña, 23</td>
      <td>Barcelona</td>
      <td>Southern Europe</td>
      <td>8022</td>
      <td>Spain</td>
    </tr>
    <tr>
      <td>681</td>
      <td>10929</td>
      <td>FRANK</td>
      <td>6</td>
      <td>2014-03-05</td>
      <td>2014-04-02</td>
      <td>2014-03-12</td>
      <td>1</td>
      <td>33.93</td>
      <td>Frankenversand</td>
      <td>Berliner Platz 43</td>
      <td>München</td>
      <td>Western Europe</td>
      <td>80805</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>682</td>
      <td>10930</td>
      <td>SUPRD</td>
      <td>4</td>
      <td>2014-03-06</td>
      <td>2014-04-17</td>
      <td>2014-03-18</td>
      <td>3</td>
      <td>15.55</td>
      <td>Suprêmes délices</td>
      <td>Boulevard Tirou, 255</td>
      <td>Charleroi</td>
      <td>Western Europe</td>
      <td>B-6000</td>
      <td>Belgium</td>
    </tr>
    <tr>
      <td>683</td>
      <td>10931</td>
      <td>RICSU</td>
      <td>4</td>
      <td>2014-03-06</td>
      <td>2014-03-20</td>
      <td>2014-03-19</td>
      <td>2</td>
      <td>13.60</td>
      <td>Richter Supermarkt</td>
      <td>Starenweg 5</td>
      <td>Genève</td>
      <td>Western Europe</td>
      <td>1204</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <td>684</td>
      <td>10932</td>
      <td>BONAP</td>
      <td>8</td>
      <td>2014-03-06</td>
      <td>2014-04-03</td>
      <td>2014-03-24</td>
      <td>1</td>
      <td>134.64</td>
      <td>Bon app'</td>
      <td>12, rue des Bouchers</td>
      <td>Marseille</td>
      <td>Western Europe</td>
      <td>13008</td>
      <td>France</td>
    </tr>
    <tr>
      <td>685</td>
      <td>10933</td>
      <td>ISLAT</td>
      <td>6</td>
      <td>2014-03-06</td>
      <td>2014-04-03</td>
      <td>2014-03-16</td>
      <td>3</td>
      <td>54.15</td>
      <td>Island Trading</td>
      <td>Garden House Crowther Way</td>
      <td>Cowes</td>
      <td>British Isles</td>
      <td>PO31 7PJ</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>686</td>
      <td>10934</td>
      <td>LEHMS</td>
      <td>3</td>
      <td>2014-03-09</td>
      <td>2014-04-06</td>
      <td>2014-03-12</td>
      <td>3</td>
      <td>32.01</td>
      <td>Lehmanns Marktstand</td>
      <td>Magazinweg 7</td>
      <td>Frankfurt a.M.</td>
      <td>Western Europe</td>
      <td>60528</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>687</td>
      <td>10935</td>
      <td>WELLI</td>
      <td>4</td>
      <td>2014-03-09</td>
      <td>2014-04-06</td>
      <td>2014-03-18</td>
      <td>3</td>
      <td>47.59</td>
      <td>Wellington Importadora</td>
      <td>Rua do Mercado, 12</td>
      <td>Resende</td>
      <td>South America</td>
      <td>08737-363</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>688</td>
      <td>10936</td>
      <td>GREAL</td>
      <td>3</td>
      <td>2014-03-09</td>
      <td>2014-04-06</td>
      <td>2014-03-18</td>
      <td>2</td>
      <td>33.68</td>
      <td>Great Lakes Food Market</td>
      <td>2732 Baker Blvd.</td>
      <td>Eugene</td>
      <td>North America</td>
      <td>97403</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>689</td>
      <td>10937</td>
      <td>CACTU</td>
      <td>7</td>
      <td>2014-03-10</td>
      <td>2014-03-24</td>
      <td>2014-03-13</td>
      <td>3</td>
      <td>31.51</td>
      <td>Cactus Comidas para llevar</td>
      <td>Cerrito 333</td>
      <td>Buenos Aires</td>
      <td>South America</td>
      <td>1010</td>
      <td>Argentina</td>
    </tr>
    <tr>
      <td>690</td>
      <td>10938</td>
      <td>QUICK</td>
      <td>3</td>
      <td>2014-03-10</td>
      <td>2014-04-07</td>
      <td>2014-03-16</td>
      <td>2</td>
      <td>31.89</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>691</td>
      <td>10939</td>
      <td>MAGAA</td>
      <td>2</td>
      <td>2014-03-10</td>
      <td>2014-04-07</td>
      <td>2014-03-13</td>
      <td>2</td>
      <td>76.33</td>
      <td>Magazzini Alimentari Riuniti</td>
      <td>Via Ludovico il Moro 22</td>
      <td>Bergamo</td>
      <td>Southern Europe</td>
      <td>24100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>692</td>
      <td>10940</td>
      <td>BONAP</td>
      <td>8</td>
      <td>2014-03-11</td>
      <td>2014-04-08</td>
      <td>2014-03-23</td>
      <td>3</td>
      <td>19.77</td>
      <td>Bon app'</td>
      <td>12, rue des Bouchers</td>
      <td>Marseille</td>
      <td>Western Europe</td>
      <td>13008</td>
      <td>France</td>
    </tr>
    <tr>
      <td>693</td>
      <td>10941</td>
      <td>SAVEA</td>
      <td>7</td>
      <td>2014-03-11</td>
      <td>2014-04-08</td>
      <td>2014-03-20</td>
      <td>2</td>
      <td>400.81</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>694</td>
      <td>10942</td>
      <td>REGGC</td>
      <td>9</td>
      <td>2014-03-11</td>
      <td>2014-04-08</td>
      <td>2014-03-18</td>
      <td>3</td>
      <td>17.95</td>
      <td>Reggiani Caseifici</td>
      <td>Strada Provinciale 124</td>
      <td>Reggio Emilia</td>
      <td>Southern Europe</td>
      <td>42100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>695</td>
      <td>10943</td>
      <td>BSBEV</td>
      <td>4</td>
      <td>2014-03-11</td>
      <td>2014-04-08</td>
      <td>2014-03-19</td>
      <td>2</td>
      <td>2.17</td>
      <td>B's Beverages</td>
      <td>Fauntleroy Circus</td>
      <td>London</td>
      <td>British Isles</td>
      <td>EC2 5NT</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>696</td>
      <td>10944</td>
      <td>BOTTM</td>
      <td>6</td>
      <td>2014-03-12</td>
      <td>2014-03-26</td>
      <td>2014-03-13</td>
      <td>3</td>
      <td>52.92</td>
      <td>Bottom-Dollar Markets</td>
      <td>23 Tsawassen Blvd.</td>
      <td>Tsawassen</td>
      <td>North America</td>
      <td>T2F 8M4</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>697</td>
      <td>10945</td>
      <td>MORGK</td>
      <td>4</td>
      <td>2014-03-12</td>
      <td>2014-04-09</td>
      <td>2014-03-18</td>
      <td>1</td>
      <td>10.22</td>
      <td>Morgenstern Gesundkost</td>
      <td>Heerstr. 22</td>
      <td>Leipzig</td>
      <td>Western Europe</td>
      <td>04179</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>698</td>
      <td>10946</td>
      <td>VAFFE</td>
      <td>1</td>
      <td>2014-03-12</td>
      <td>2014-04-09</td>
      <td>2014-03-19</td>
      <td>2</td>
      <td>27.20</td>
      <td>Vaffeljernet</td>
      <td>Smagsloget 45</td>
      <td>Århus</td>
      <td>Northern Europe</td>
      <td>8200</td>
      <td>Denmark</td>
    </tr>
    <tr>
      <td>699</td>
      <td>10947</td>
      <td>BSBEV</td>
      <td>3</td>
      <td>2014-03-13</td>
      <td>2014-04-10</td>
      <td>2014-03-16</td>
      <td>2</td>
      <td>3.26</td>
      <td>B's Beverages</td>
      <td>Fauntleroy Circus</td>
      <td>London</td>
      <td>British Isles</td>
      <td>EC2 5NT</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>700</td>
      <td>10948</td>
      <td>GODOS</td>
      <td>3</td>
      <td>2014-03-13</td>
      <td>2014-04-10</td>
      <td>2014-03-19</td>
      <td>3</td>
      <td>23.39</td>
      <td>Godos Cocina Típica</td>
      <td>C/ Romero, 33</td>
      <td>Sevilla</td>
      <td>Southern Europe</td>
      <td>41101</td>
      <td>Spain</td>
    </tr>
    <tr>
      <td>701</td>
      <td>10949</td>
      <td>BOTTM</td>
      <td>2</td>
      <td>2014-03-13</td>
      <td>2014-04-10</td>
      <td>2014-03-17</td>
      <td>3</td>
      <td>74.44</td>
      <td>Bottom-Dollar Markets</td>
      <td>23 Tsawassen Blvd.</td>
      <td>Tsawassen</td>
      <td>North America</td>
      <td>T2F 8M4</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>702</td>
      <td>10950</td>
      <td>MAGAA</td>
      <td>1</td>
      <td>2014-03-16</td>
      <td>2014-04-13</td>
      <td>2014-03-23</td>
      <td>2</td>
      <td>2.50</td>
      <td>Magazzini Alimentari Riuniti</td>
      <td>Via Ludovico il Moro 22</td>
      <td>Bergamo</td>
      <td>Southern Europe</td>
      <td>24100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>703</td>
      <td>10951</td>
      <td>RICSU</td>
      <td>9</td>
      <td>2014-03-16</td>
      <td>2014-04-27</td>
      <td>2014-04-07</td>
      <td>2</td>
      <td>30.85</td>
      <td>Richter Supermarkt</td>
      <td>Starenweg 5</td>
      <td>Genève</td>
      <td>Western Europe</td>
      <td>1204</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <td>704</td>
      <td>10952</td>
      <td>ALFKI</td>
      <td>1</td>
      <td>2014-03-16</td>
      <td>2014-04-27</td>
      <td>2014-03-24</td>
      <td>1</td>
      <td>40.42</td>
      <td>Alfred's Futterkiste</td>
      <td>Obere Str. 57</td>
      <td>Berlin</td>
      <td>Western Europe</td>
      <td>12209</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>705</td>
      <td>10953</td>
      <td>AROUT</td>
      <td>9</td>
      <td>2014-03-16</td>
      <td>2014-03-30</td>
      <td>2014-03-25</td>
      <td>2</td>
      <td>23.72</td>
      <td>Around the Horn</td>
      <td>Brook Farm Stratford St. Mary</td>
      <td>Colchester</td>
      <td>British Isles</td>
      <td>CO7 6JX</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>706</td>
      <td>10954</td>
      <td>LINOD</td>
      <td>5</td>
      <td>2014-03-17</td>
      <td>2014-04-28</td>
      <td>2014-03-20</td>
      <td>1</td>
      <td>27.91</td>
      <td>LINO-Delicateses</td>
      <td>Ave. 5 de Mayo Porlamar</td>
      <td>I. de Margarita</td>
      <td>South America</td>
      <td>4980</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>707</td>
      <td>10955</td>
      <td>FOLKO</td>
      <td>8</td>
      <td>2014-03-17</td>
      <td>2014-04-14</td>
      <td>2014-03-20</td>
      <td>2</td>
      <td>3.26</td>
      <td>Folk och fä HB</td>
      <td>Åkergatan 24</td>
      <td>Bräcke</td>
      <td>Northern Europe</td>
      <td>S-844 67</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>708</td>
      <td>10956</td>
      <td>BLAUS</td>
      <td>6</td>
      <td>2014-03-17</td>
      <td>2014-04-28</td>
      <td>2014-03-20</td>
      <td>2</td>
      <td>44.65</td>
      <td>Blauer See Delikatessen</td>
      <td>Forsterstr. 57</td>
      <td>Mannheim</td>
      <td>Western Europe</td>
      <td>68306</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>709</td>
      <td>10957</td>
      <td>HILAA</td>
      <td>8</td>
      <td>2014-03-18</td>
      <td>2014-04-15</td>
      <td>2014-03-27</td>
      <td>3</td>
      <td>105.36</td>
      <td>HILARION-Abastos</td>
      <td>Carrera 22 con Ave. Carlos Soublette #8-35</td>
      <td>San Cristóbal</td>
      <td>South America</td>
      <td>5022</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>710</td>
      <td>10958</td>
      <td>OCEA</td>
      <td>7</td>
      <td>2014-03-18</td>
      <td>2014-04-15</td>
      <td>2014-03-27</td>
      <td>2</td>
      <td>49.56</td>
      <td>Océano Atlántico Ltda.</td>
      <td>Ing. Gustavo Moncada 8585 Piso 20-A</td>
      <td>Buenos Aires</td>
      <td>South America</td>
      <td>1010</td>
      <td>Argentina</td>
    </tr>
    <tr>
      <td>711</td>
      <td>10959</td>
      <td>GOURL</td>
      <td>6</td>
      <td>2014-03-18</td>
      <td>2014-04-29</td>
      <td>2014-03-23</td>
      <td>2</td>
      <td>4.98</td>
      <td>Gourmet Lanchonetes</td>
      <td>Av. Brasil, 442</td>
      <td>Campinas</td>
      <td>South America</td>
      <td>04876-786</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>712</td>
      <td>10960</td>
      <td>HILAA</td>
      <td>3</td>
      <td>2014-03-19</td>
      <td>2014-04-02</td>
      <td>2014-04-08</td>
      <td>1</td>
      <td>2.08</td>
      <td>HILARION-Abastos</td>
      <td>Carrera 22 con Ave. Carlos Soublette #8-35</td>
      <td>San Cristóbal</td>
      <td>South America</td>
      <td>5022</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>713</td>
      <td>10961</td>
      <td>QUEE</td>
      <td>8</td>
      <td>2014-03-19</td>
      <td>2014-04-16</td>
      <td>2014-03-30</td>
      <td>1</td>
      <td>104.47</td>
      <td>Queen Cozinha</td>
      <td>Alameda dos Canàrios, 891</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05487-020</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>714</td>
      <td>10962</td>
      <td>QUICK</td>
      <td>8</td>
      <td>2014-03-19</td>
      <td>2014-04-16</td>
      <td>2014-03-23</td>
      <td>2</td>
      <td>275.79</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>715</td>
      <td>10963</td>
      <td>FURIB</td>
      <td>9</td>
      <td>2014-03-19</td>
      <td>2014-04-16</td>
      <td>2014-03-26</td>
      <td>3</td>
      <td>2.70</td>
      <td>Furia Bacalhau e Frutos do Mar</td>
      <td>Jardim das rosas n. 32</td>
      <td>Lisboa</td>
      <td>Southern Europe</td>
      <td>1675</td>
      <td>Portugal</td>
    </tr>
    <tr>
      <td>716</td>
      <td>10964</td>
      <td>SPECD</td>
      <td>3</td>
      <td>2014-03-20</td>
      <td>2014-04-17</td>
      <td>2014-03-24</td>
      <td>2</td>
      <td>87.38</td>
      <td>Spécialités du monde</td>
      <td>25, rue Lauriston</td>
      <td>Paris</td>
      <td>Western Europe</td>
      <td>75016</td>
      <td>France</td>
    </tr>
    <tr>
      <td>717</td>
      <td>10965</td>
      <td>OLDWO</td>
      <td>6</td>
      <td>2014-03-20</td>
      <td>2014-04-17</td>
      <td>2014-03-30</td>
      <td>3</td>
      <td>144.38</td>
      <td>Old World Delicatessen</td>
      <td>2743 Bering St.</td>
      <td>Anchorage</td>
      <td>North America</td>
      <td>99508</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>718</td>
      <td>10966</td>
      <td>CHOPS</td>
      <td>4</td>
      <td>2014-03-20</td>
      <td>2014-04-17</td>
      <td>2014-04-08</td>
      <td>1</td>
      <td>27.19</td>
      <td>Chop-suey Chinese</td>
      <td>Hauptstr. 31</td>
      <td>Bern</td>
      <td>Western Europe</td>
      <td>3012</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <td>719</td>
      <td>10967</td>
      <td>TOMSP</td>
      <td>2</td>
      <td>2014-03-23</td>
      <td>2014-04-20</td>
      <td>2014-04-02</td>
      <td>2</td>
      <td>62.22</td>
      <td>Toms Spezialitäten</td>
      <td>Luisenstr. 48</td>
      <td>Münster</td>
      <td>Western Europe</td>
      <td>44087</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>720</td>
      <td>10968</td>
      <td>ERNSH</td>
      <td>1</td>
      <td>2014-03-23</td>
      <td>2014-04-20</td>
      <td>2014-04-01</td>
      <td>3</td>
      <td>74.60</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>721</td>
      <td>10969</td>
      <td>COMMI</td>
      <td>1</td>
      <td>2014-03-23</td>
      <td>2014-04-20</td>
      <td>2014-03-30</td>
      <td>2</td>
      <td>0.21</td>
      <td>Comércio Mineiro</td>
      <td>Av. dos Lusíadas, 23</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05432-043</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>722</td>
      <td>10970</td>
      <td>BOLID</td>
      <td>9</td>
      <td>2014-03-24</td>
      <td>2014-04-07</td>
      <td>2014-04-24</td>
      <td>1</td>
      <td>16.16</td>
      <td>Bólido Comidas preparadas</td>
      <td>C/ Araquil, 67</td>
      <td>Madrid</td>
      <td>Southern Europe</td>
      <td>28023</td>
      <td>Spain</td>
    </tr>
    <tr>
      <td>723</td>
      <td>10971</td>
      <td>FRANR</td>
      <td>2</td>
      <td>2014-03-24</td>
      <td>2014-04-21</td>
      <td>2014-04-02</td>
      <td>2</td>
      <td>121.82</td>
      <td>France restauration</td>
      <td>54, rue Royale</td>
      <td>Nantes</td>
      <td>Western Europe</td>
      <td>44000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>724</td>
      <td>10972</td>
      <td>LACOR</td>
      <td>4</td>
      <td>2014-03-24</td>
      <td>2014-04-21</td>
      <td>2014-03-26</td>
      <td>2</td>
      <td>0.02</td>
      <td>La corne d'abondance</td>
      <td>67, avenue de l'Europe</td>
      <td>Versailles</td>
      <td>Western Europe</td>
      <td>78000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>725</td>
      <td>10973</td>
      <td>LACOR</td>
      <td>6</td>
      <td>2014-03-24</td>
      <td>2014-04-21</td>
      <td>2014-03-27</td>
      <td>2</td>
      <td>15.17</td>
      <td>La corne d'abondance</td>
      <td>67, avenue de l'Europe</td>
      <td>Versailles</td>
      <td>Western Europe</td>
      <td>78000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>726</td>
      <td>10974</td>
      <td>SPLIR</td>
      <td>3</td>
      <td>2014-03-25</td>
      <td>2014-04-08</td>
      <td>2014-04-03</td>
      <td>3</td>
      <td>12.96</td>
      <td>Split Rail Beer &amp; Ale</td>
      <td>P.O. Box 555</td>
      <td>Lander</td>
      <td>North America</td>
      <td>82520</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>727</td>
      <td>10975</td>
      <td>BOTTM</td>
      <td>1</td>
      <td>2014-03-25</td>
      <td>2014-04-22</td>
      <td>2014-03-27</td>
      <td>3</td>
      <td>32.27</td>
      <td>Bottom-Dollar Markets</td>
      <td>23 Tsawassen Blvd.</td>
      <td>Tsawassen</td>
      <td>North America</td>
      <td>T2F 8M4</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>728</td>
      <td>10976</td>
      <td>HILAA</td>
      <td>1</td>
      <td>2014-03-25</td>
      <td>2014-05-06</td>
      <td>2014-04-03</td>
      <td>1</td>
      <td>37.97</td>
      <td>HILARION-Abastos</td>
      <td>Carrera 22 con Ave. Carlos Soublette #8-35</td>
      <td>San Cristóbal</td>
      <td>South America</td>
      <td>5022</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>729</td>
      <td>10977</td>
      <td>FOLKO</td>
      <td>8</td>
      <td>2014-03-26</td>
      <td>2014-04-23</td>
      <td>2014-04-10</td>
      <td>3</td>
      <td>208.50</td>
      <td>Folk och fä HB</td>
      <td>Åkergatan 24</td>
      <td>Bräcke</td>
      <td>Northern Europe</td>
      <td>S-844 67</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>730</td>
      <td>10978</td>
      <td>MAISD</td>
      <td>9</td>
      <td>2014-03-26</td>
      <td>2014-04-23</td>
      <td>2014-04-23</td>
      <td>2</td>
      <td>32.82</td>
      <td>Maison Dewey</td>
      <td>Rue Joseph-Bens 532</td>
      <td>Bruxelles</td>
      <td>Western Europe</td>
      <td>B-1180</td>
      <td>Belgium</td>
    </tr>
    <tr>
      <td>731</td>
      <td>10979</td>
      <td>ERNSH</td>
      <td>8</td>
      <td>2014-03-26</td>
      <td>2014-04-23</td>
      <td>2014-03-31</td>
      <td>2</td>
      <td>353.07</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>732</td>
      <td>10980</td>
      <td>FOLKO</td>
      <td>4</td>
      <td>2014-03-27</td>
      <td>2014-05-08</td>
      <td>2014-04-17</td>
      <td>1</td>
      <td>1.26</td>
      <td>Folk och fä HB</td>
      <td>Åkergatan 24</td>
      <td>Bräcke</td>
      <td>Northern Europe</td>
      <td>S-844 67</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>733</td>
      <td>10981</td>
      <td>HANAR</td>
      <td>1</td>
      <td>2014-03-27</td>
      <td>2014-04-24</td>
      <td>2014-04-02</td>
      <td>2</td>
      <td>193.37</td>
      <td>Hanari Carnes</td>
      <td>Rua do Paço, 67</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>05454-876</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>734</td>
      <td>10982</td>
      <td>BOTTM</td>
      <td>2</td>
      <td>2014-03-27</td>
      <td>2014-04-24</td>
      <td>2014-04-08</td>
      <td>1</td>
      <td>14.01</td>
      <td>Bottom-Dollar Markets</td>
      <td>23 Tsawassen Blvd.</td>
      <td>Tsawassen</td>
      <td>North America</td>
      <td>T2F 8M4</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>735</td>
      <td>10983</td>
      <td>SAVEA</td>
      <td>2</td>
      <td>2014-03-27</td>
      <td>2014-04-24</td>
      <td>2014-04-06</td>
      <td>2</td>
      <td>657.54</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>736</td>
      <td>10984</td>
      <td>SAVEA</td>
      <td>1</td>
      <td>2014-03-30</td>
      <td>2014-04-27</td>
      <td>2014-04-03</td>
      <td>3</td>
      <td>211.22</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>737</td>
      <td>10985</td>
      <td>HUNGO</td>
      <td>2</td>
      <td>2014-03-30</td>
      <td>2014-04-27</td>
      <td>2014-04-02</td>
      <td>1</td>
      <td>91.51</td>
      <td>Hungry Owl All-Night Grocers</td>
      <td>8 Johnstown Road</td>
      <td>Cork</td>
      <td>British Isles</td>
      <td>None</td>
      <td>Ireland</td>
    </tr>
    <tr>
      <td>738</td>
      <td>10986</td>
      <td>OCEA</td>
      <td>8</td>
      <td>2014-03-30</td>
      <td>2014-04-27</td>
      <td>2014-04-21</td>
      <td>2</td>
      <td>217.86</td>
      <td>Océano Atlántico Ltda.</td>
      <td>Ing. Gustavo Moncada 8585 Piso 20-A</td>
      <td>Buenos Aires</td>
      <td>South America</td>
      <td>1010</td>
      <td>Argentina</td>
    </tr>
    <tr>
      <td>739</td>
      <td>10987</td>
      <td>EASTC</td>
      <td>8</td>
      <td>2014-03-31</td>
      <td>2014-04-28</td>
      <td>2014-04-06</td>
      <td>1</td>
      <td>185.48</td>
      <td>Eastern Connection</td>
      <td>35 King George</td>
      <td>London</td>
      <td>British Isles</td>
      <td>WX3 6FW</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>740</td>
      <td>10988</td>
      <td>RATTC</td>
      <td>3</td>
      <td>2014-03-31</td>
      <td>2014-04-28</td>
      <td>2014-04-10</td>
      <td>2</td>
      <td>61.14</td>
      <td>Rattlesnake Canyon Grocery</td>
      <td>2817 Milton Dr.</td>
      <td>Albuquerque</td>
      <td>North America</td>
      <td>87110</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>741</td>
      <td>10989</td>
      <td>QUEDE</td>
      <td>2</td>
      <td>2014-03-31</td>
      <td>2014-04-28</td>
      <td>2014-04-02</td>
      <td>1</td>
      <td>34.76</td>
      <td>Que Delícia</td>
      <td>Rua da Panificadora, 12</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>02389-673</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>742</td>
      <td>10990</td>
      <td>ERNSH</td>
      <td>2</td>
      <td>2014-04-01</td>
      <td>2014-05-13</td>
      <td>2014-04-07</td>
      <td>3</td>
      <td>117.61</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>743</td>
      <td>10991</td>
      <td>QUICK</td>
      <td>1</td>
      <td>2014-04-01</td>
      <td>2014-04-29</td>
      <td>2014-04-07</td>
      <td>1</td>
      <td>38.51</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>744</td>
      <td>10992</td>
      <td>THEBI</td>
      <td>1</td>
      <td>2014-04-01</td>
      <td>2014-04-29</td>
      <td>2014-04-03</td>
      <td>3</td>
      <td>4.27</td>
      <td>The Big Cheese</td>
      <td>89 Jefferson Way Suite 2</td>
      <td>Portland</td>
      <td>North America</td>
      <td>97201</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>745</td>
      <td>10993</td>
      <td>FOLKO</td>
      <td>7</td>
      <td>2014-04-01</td>
      <td>2014-04-29</td>
      <td>2014-04-10</td>
      <td>3</td>
      <td>8.81</td>
      <td>Folk och fä HB</td>
      <td>Åkergatan 24</td>
      <td>Bräcke</td>
      <td>Northern Europe</td>
      <td>S-844 67</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>746</td>
      <td>10994</td>
      <td>VAFFE</td>
      <td>2</td>
      <td>2014-04-02</td>
      <td>2014-04-16</td>
      <td>2014-04-09</td>
      <td>3</td>
      <td>65.53</td>
      <td>Vaffeljernet</td>
      <td>Smagsloget 45</td>
      <td>Århus</td>
      <td>Northern Europe</td>
      <td>8200</td>
      <td>Denmark</td>
    </tr>
    <tr>
      <td>747</td>
      <td>10995</td>
      <td>PERIC</td>
      <td>1</td>
      <td>2014-04-02</td>
      <td>2014-04-30</td>
      <td>2014-04-06</td>
      <td>3</td>
      <td>46.00</td>
      <td>Pericles Comidas clásicas</td>
      <td>Calle Dr. Jorge Cash 321</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05033</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>748</td>
      <td>10996</td>
      <td>QUICK</td>
      <td>4</td>
      <td>2014-04-02</td>
      <td>2014-04-30</td>
      <td>2014-04-10</td>
      <td>2</td>
      <td>1.12</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>749</td>
      <td>10997</td>
      <td>LILAS</td>
      <td>8</td>
      <td>2014-04-03</td>
      <td>2014-05-15</td>
      <td>2014-04-13</td>
      <td>2</td>
      <td>73.91</td>
      <td>LILA-Supermercado</td>
      <td>Carrera 52 con Ave. Bolívar #65-98 Llano Largo</td>
      <td>Barquisimeto</td>
      <td>South America</td>
      <td>3508</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>750</td>
      <td>10998</td>
      <td>WOLZA</td>
      <td>8</td>
      <td>2014-04-03</td>
      <td>2014-04-17</td>
      <td>2014-04-17</td>
      <td>2</td>
      <td>20.31</td>
      <td>Wolski Zajazd</td>
      <td>ul. Filtrowa 68</td>
      <td>Warszawa</td>
      <td>Eastern Europe</td>
      <td>01-012</td>
      <td>Poland</td>
    </tr>
    <tr>
      <td>751</td>
      <td>10999</td>
      <td>OTTIK</td>
      <td>6</td>
      <td>2014-04-03</td>
      <td>2014-05-01</td>
      <td>2014-04-10</td>
      <td>2</td>
      <td>96.35</td>
      <td>Ottilies Käseladen</td>
      <td>Mehrheimerstr. 369</td>
      <td>Köln</td>
      <td>Western Europe</td>
      <td>50739</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>752</td>
      <td>11000</td>
      <td>RATTC</td>
      <td>2</td>
      <td>2014-04-06</td>
      <td>2014-05-04</td>
      <td>2014-04-14</td>
      <td>3</td>
      <td>55.12</td>
      <td>Rattlesnake Canyon Grocery</td>
      <td>2817 Milton Dr.</td>
      <td>Albuquerque</td>
      <td>North America</td>
      <td>87110</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>753</td>
      <td>11001</td>
      <td>FOLKO</td>
      <td>2</td>
      <td>2014-04-06</td>
      <td>2014-05-04</td>
      <td>2014-04-14</td>
      <td>2</td>
      <td>197.30</td>
      <td>Folk och fä HB</td>
      <td>Åkergatan 24</td>
      <td>Bräcke</td>
      <td>Northern Europe</td>
      <td>S-844 67</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>754</td>
      <td>11002</td>
      <td>SAVEA</td>
      <td>4</td>
      <td>2014-04-06</td>
      <td>2014-05-04</td>
      <td>2014-04-16</td>
      <td>1</td>
      <td>141.16</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>755</td>
      <td>11003</td>
      <td>THECR</td>
      <td>3</td>
      <td>2014-04-06</td>
      <td>2014-05-04</td>
      <td>2014-04-08</td>
      <td>3</td>
      <td>14.91</td>
      <td>The Cracker Box</td>
      <td>55 Grizzly Peak Rd.</td>
      <td>Butte</td>
      <td>North America</td>
      <td>59801</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>756</td>
      <td>11004</td>
      <td>MAISD</td>
      <td>3</td>
      <td>2014-04-07</td>
      <td>2014-05-05</td>
      <td>2014-04-20</td>
      <td>1</td>
      <td>44.84</td>
      <td>Maison Dewey</td>
      <td>Rue Joseph-Bens 532</td>
      <td>Bruxelles</td>
      <td>Western Europe</td>
      <td>B-1180</td>
      <td>Belgium</td>
    </tr>
    <tr>
      <td>757</td>
      <td>11005</td>
      <td>WILMK</td>
      <td>2</td>
      <td>2014-04-07</td>
      <td>2014-05-05</td>
      <td>2014-04-10</td>
      <td>1</td>
      <td>0.75</td>
      <td>Wilman Kala</td>
      <td>Keskuskatu 45</td>
      <td>Helsinki</td>
      <td>Scandinavia</td>
      <td>21240</td>
      <td>Finland</td>
    </tr>
    <tr>
      <td>758</td>
      <td>11006</td>
      <td>GREAL</td>
      <td>3</td>
      <td>2014-04-07</td>
      <td>2014-05-05</td>
      <td>2014-04-15</td>
      <td>2</td>
      <td>25.19</td>
      <td>Great Lakes Food Market</td>
      <td>2732 Baker Blvd.</td>
      <td>Eugene</td>
      <td>North America</td>
      <td>97403</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>759</td>
      <td>11007</td>
      <td>PRINI</td>
      <td>8</td>
      <td>2014-04-08</td>
      <td>2014-05-06</td>
      <td>2014-04-13</td>
      <td>2</td>
      <td>202.24</td>
      <td>Princesa Isabel Vinhos</td>
      <td>Estrada da saúde n. 58</td>
      <td>Lisboa</td>
      <td>Southern Europe</td>
      <td>1756</td>
      <td>Portugal</td>
    </tr>
    <tr>
      <td>760</td>
      <td>11008</td>
      <td>ERNSH</td>
      <td>7</td>
      <td>2014-04-08</td>
      <td>2014-05-06</td>
      <td>None</td>
      <td>3</td>
      <td>79.46</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>761</td>
      <td>11009</td>
      <td>GODOS</td>
      <td>2</td>
      <td>2014-04-08</td>
      <td>2014-05-06</td>
      <td>2014-04-10</td>
      <td>1</td>
      <td>59.11</td>
      <td>Godos Cocina Típica</td>
      <td>C/ Romero, 33</td>
      <td>Sevilla</td>
      <td>Southern Europe</td>
      <td>41101</td>
      <td>Spain</td>
    </tr>
    <tr>
      <td>762</td>
      <td>11010</td>
      <td>REGGC</td>
      <td>2</td>
      <td>2014-04-09</td>
      <td>2014-05-07</td>
      <td>2014-04-21</td>
      <td>2</td>
      <td>28.71</td>
      <td>Reggiani Caseifici</td>
      <td>Strada Provinciale 124</td>
      <td>Reggio Emilia</td>
      <td>Southern Europe</td>
      <td>42100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>763</td>
      <td>11011</td>
      <td>ALFKI</td>
      <td>3</td>
      <td>2014-04-09</td>
      <td>2014-05-07</td>
      <td>2014-04-13</td>
      <td>1</td>
      <td>1.21</td>
      <td>Alfred's Futterkiste</td>
      <td>Obere Str. 57</td>
      <td>Berlin</td>
      <td>Western Europe</td>
      <td>12209</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>764</td>
      <td>11012</td>
      <td>FRANK</td>
      <td>1</td>
      <td>2014-04-09</td>
      <td>2014-04-23</td>
      <td>2014-04-17</td>
      <td>3</td>
      <td>242.95</td>
      <td>Frankenversand</td>
      <td>Berliner Platz 43</td>
      <td>München</td>
      <td>Western Europe</td>
      <td>80805</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>765</td>
      <td>11013</td>
      <td>ROMEY</td>
      <td>2</td>
      <td>2014-04-09</td>
      <td>2014-05-07</td>
      <td>2014-04-10</td>
      <td>1</td>
      <td>32.99</td>
      <td>Romero y tomillo</td>
      <td>Gran Vía, 1</td>
      <td>Madrid</td>
      <td>Southern Europe</td>
      <td>28001</td>
      <td>Spain</td>
    </tr>
    <tr>
      <td>766</td>
      <td>11014</td>
      <td>LINOD</td>
      <td>2</td>
      <td>2014-04-10</td>
      <td>2014-05-08</td>
      <td>2014-04-15</td>
      <td>3</td>
      <td>23.60</td>
      <td>LINO-Delicateses</td>
      <td>Ave. 5 de Mayo Porlamar</td>
      <td>I. de Margarita</td>
      <td>South America</td>
      <td>4980</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>767</td>
      <td>11015</td>
      <td>SANTG</td>
      <td>2</td>
      <td>2014-04-10</td>
      <td>2014-04-24</td>
      <td>2014-04-20</td>
      <td>2</td>
      <td>4.62</td>
      <td>Santé Gourmet</td>
      <td>Erling Skakkes gate 78</td>
      <td>Stavern</td>
      <td>Scandinavia</td>
      <td>4110</td>
      <td>Norway</td>
    </tr>
    <tr>
      <td>768</td>
      <td>11016</td>
      <td>AROUT</td>
      <td>9</td>
      <td>2014-04-10</td>
      <td>2014-05-08</td>
      <td>2014-04-13</td>
      <td>2</td>
      <td>33.80</td>
      <td>Around the Horn</td>
      <td>Brook Farm Stratford St. Mary</td>
      <td>Colchester</td>
      <td>British Isles</td>
      <td>CO7 6JX</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>769</td>
      <td>11017</td>
      <td>ERNSH</td>
      <td>9</td>
      <td>2014-04-13</td>
      <td>2014-05-11</td>
      <td>2014-04-20</td>
      <td>2</td>
      <td>754.26</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>770</td>
      <td>11018</td>
      <td>LONEP</td>
      <td>4</td>
      <td>2014-04-13</td>
      <td>2014-05-11</td>
      <td>2014-04-16</td>
      <td>2</td>
      <td>11.65</td>
      <td>Lonesome Pine Restaurant</td>
      <td>89 Chiaroscuro Rd.</td>
      <td>Portland</td>
      <td>North America</td>
      <td>97219</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>771</td>
      <td>11019</td>
      <td>RANCH</td>
      <td>6</td>
      <td>2014-04-13</td>
      <td>2014-05-11</td>
      <td>None</td>
      <td>3</td>
      <td>3.17</td>
      <td>Rancho grande</td>
      <td>Av. del Libertador 900</td>
      <td>Buenos Aires</td>
      <td>South America</td>
      <td>1010</td>
      <td>Argentina</td>
    </tr>
    <tr>
      <td>772</td>
      <td>11020</td>
      <td>OTTIK</td>
      <td>2</td>
      <td>2014-04-14</td>
      <td>2014-05-12</td>
      <td>2014-04-16</td>
      <td>2</td>
      <td>43.30</td>
      <td>Ottilies Käseladen</td>
      <td>Mehrheimerstr. 369</td>
      <td>Köln</td>
      <td>Western Europe</td>
      <td>50739</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>773</td>
      <td>11021</td>
      <td>QUICK</td>
      <td>3</td>
      <td>2014-04-14</td>
      <td>2014-05-12</td>
      <td>2014-04-21</td>
      <td>1</td>
      <td>297.18</td>
      <td>QUICK-Stop</td>
      <td>Taucherstraße 10</td>
      <td>Cunewalde</td>
      <td>Western Europe</td>
      <td>01307</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>774</td>
      <td>11022</td>
      <td>HANAR</td>
      <td>9</td>
      <td>2014-04-14</td>
      <td>2014-05-12</td>
      <td>2014-05-04</td>
      <td>2</td>
      <td>6.27</td>
      <td>Hanari Carnes</td>
      <td>Rua do Paço, 67</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>05454-876</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>775</td>
      <td>11023</td>
      <td>BSBEV</td>
      <td>1</td>
      <td>2014-04-14</td>
      <td>2014-04-28</td>
      <td>2014-04-24</td>
      <td>2</td>
      <td>123.83</td>
      <td>B's Beverages</td>
      <td>Fauntleroy Circus</td>
      <td>London</td>
      <td>British Isles</td>
      <td>EC2 5NT</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>776</td>
      <td>11024</td>
      <td>EASTC</td>
      <td>4</td>
      <td>2014-04-15</td>
      <td>2014-05-13</td>
      <td>2014-04-20</td>
      <td>1</td>
      <td>74.36</td>
      <td>Eastern Connection</td>
      <td>35 King George</td>
      <td>London</td>
      <td>British Isles</td>
      <td>WX3 6FW</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>777</td>
      <td>11025</td>
      <td>WARTH</td>
      <td>6</td>
      <td>2014-04-15</td>
      <td>2014-05-13</td>
      <td>2014-04-24</td>
      <td>3</td>
      <td>29.17</td>
      <td>Wartian Herkku</td>
      <td>Torikatu 38</td>
      <td>Oulu</td>
      <td>Scandinavia</td>
      <td>90110</td>
      <td>Finland</td>
    </tr>
    <tr>
      <td>778</td>
      <td>11026</td>
      <td>FRANS</td>
      <td>4</td>
      <td>2014-04-15</td>
      <td>2014-05-13</td>
      <td>2014-04-28</td>
      <td>1</td>
      <td>47.09</td>
      <td>Franchi S.p.A.</td>
      <td>Via Monte Bianco 34</td>
      <td>Torino</td>
      <td>Southern Europe</td>
      <td>10100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>779</td>
      <td>11027</td>
      <td>BOTTM</td>
      <td>1</td>
      <td>2014-04-16</td>
      <td>2014-05-14</td>
      <td>2014-04-20</td>
      <td>1</td>
      <td>52.52</td>
      <td>Bottom-Dollar Markets</td>
      <td>23 Tsawassen Blvd.</td>
      <td>Tsawassen</td>
      <td>North America</td>
      <td>T2F 8M4</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>780</td>
      <td>11028</td>
      <td>KOENE</td>
      <td>2</td>
      <td>2014-04-16</td>
      <td>2014-05-14</td>
      <td>2014-04-22</td>
      <td>1</td>
      <td>29.59</td>
      <td>Königlich Essen</td>
      <td>Maubelstr. 90</td>
      <td>Brandenburg</td>
      <td>Western Europe</td>
      <td>14776</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>781</td>
      <td>11029</td>
      <td>CHOPS</td>
      <td>4</td>
      <td>2014-04-16</td>
      <td>2014-05-14</td>
      <td>2014-04-27</td>
      <td>1</td>
      <td>47.84</td>
      <td>Chop-suey Chinese</td>
      <td>Hauptstr. 31</td>
      <td>Bern</td>
      <td>Western Europe</td>
      <td>3012</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <td>782</td>
      <td>11030</td>
      <td>SAVEA</td>
      <td>7</td>
      <td>2014-04-17</td>
      <td>2014-05-15</td>
      <td>2014-04-27</td>
      <td>2</td>
      <td>830.75</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>783</td>
      <td>11031</td>
      <td>SAVEA</td>
      <td>6</td>
      <td>2014-04-17</td>
      <td>2014-05-15</td>
      <td>2014-04-24</td>
      <td>2</td>
      <td>227.22</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>784</td>
      <td>11032</td>
      <td>WHITC</td>
      <td>2</td>
      <td>2014-04-17</td>
      <td>2014-05-15</td>
      <td>2014-04-23</td>
      <td>3</td>
      <td>606.19</td>
      <td>White Clover Markets</td>
      <td>1029 - 12th Ave. S.</td>
      <td>Seattle</td>
      <td>North America</td>
      <td>98124</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>785</td>
      <td>11033</td>
      <td>RICSU</td>
      <td>7</td>
      <td>2014-04-17</td>
      <td>2014-05-15</td>
      <td>2014-04-23</td>
      <td>3</td>
      <td>84.74</td>
      <td>Richter Supermarkt</td>
      <td>Starenweg 5</td>
      <td>Genève</td>
      <td>Western Europe</td>
      <td>1204</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <td>786</td>
      <td>11034</td>
      <td>OLDWO</td>
      <td>8</td>
      <td>2014-04-20</td>
      <td>2014-06-01</td>
      <td>2014-04-27</td>
      <td>1</td>
      <td>40.32</td>
      <td>Old World Delicatessen</td>
      <td>2743 Bering St.</td>
      <td>Anchorage</td>
      <td>North America</td>
      <td>99508</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>787</td>
      <td>11035</td>
      <td>SUPRD</td>
      <td>2</td>
      <td>2014-04-20</td>
      <td>2014-05-18</td>
      <td>2014-04-24</td>
      <td>2</td>
      <td>0.17</td>
      <td>Suprêmes délices</td>
      <td>Boulevard Tirou, 255</td>
      <td>Charleroi</td>
      <td>Western Europe</td>
      <td>B-6000</td>
      <td>Belgium</td>
    </tr>
    <tr>
      <td>788</td>
      <td>11036</td>
      <td>DRACD</td>
      <td>8</td>
      <td>2014-04-20</td>
      <td>2014-05-18</td>
      <td>2014-04-22</td>
      <td>3</td>
      <td>149.47</td>
      <td>Drachenblut Delikatessen</td>
      <td>Walserweg 21</td>
      <td>Aachen</td>
      <td>Western Europe</td>
      <td>52066</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>789</td>
      <td>11037</td>
      <td>GODOS</td>
      <td>7</td>
      <td>2014-04-21</td>
      <td>2014-05-19</td>
      <td>2014-04-27</td>
      <td>1</td>
      <td>3.20</td>
      <td>Godos Cocina Típica</td>
      <td>C/ Romero, 33</td>
      <td>Sevilla</td>
      <td>Southern Europe</td>
      <td>41101</td>
      <td>Spain</td>
    </tr>
    <tr>
      <td>790</td>
      <td>11038</td>
      <td>SUPRD</td>
      <td>1</td>
      <td>2014-04-21</td>
      <td>2014-05-19</td>
      <td>2014-04-30</td>
      <td>2</td>
      <td>29.59</td>
      <td>Suprêmes délices</td>
      <td>Boulevard Tirou, 255</td>
      <td>Charleroi</td>
      <td>Western Europe</td>
      <td>B-6000</td>
      <td>Belgium</td>
    </tr>
    <tr>
      <td>791</td>
      <td>11039</td>
      <td>LINOD</td>
      <td>1</td>
      <td>2014-04-21</td>
      <td>2014-05-19</td>
      <td>None</td>
      <td>2</td>
      <td>65.00</td>
      <td>LINO-Delicateses</td>
      <td>Ave. 5 de Mayo Porlamar</td>
      <td>I. de Margarita</td>
      <td>South America</td>
      <td>4980</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>792</td>
      <td>11040</td>
      <td>GREAL</td>
      <td>4</td>
      <td>2014-04-22</td>
      <td>2014-05-20</td>
      <td>None</td>
      <td>3</td>
      <td>18.84</td>
      <td>Great Lakes Food Market</td>
      <td>2732 Baker Blvd.</td>
      <td>Eugene</td>
      <td>North America</td>
      <td>97403</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>793</td>
      <td>11041</td>
      <td>CHOPS</td>
      <td>3</td>
      <td>2014-04-22</td>
      <td>2014-05-20</td>
      <td>2014-04-28</td>
      <td>2</td>
      <td>48.22</td>
      <td>Chop-suey Chinese</td>
      <td>Hauptstr. 31</td>
      <td>Bern</td>
      <td>Western Europe</td>
      <td>3012</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <td>794</td>
      <td>11042</td>
      <td>COMMI</td>
      <td>2</td>
      <td>2014-04-22</td>
      <td>2014-05-06</td>
      <td>2014-05-01</td>
      <td>1</td>
      <td>29.99</td>
      <td>Comércio Mineiro</td>
      <td>Av. dos Lusíadas, 23</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05432-043</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>795</td>
      <td>11043</td>
      <td>SPECD</td>
      <td>5</td>
      <td>2014-04-22</td>
      <td>2014-05-20</td>
      <td>2014-04-29</td>
      <td>2</td>
      <td>8.80</td>
      <td>Spécialités du monde</td>
      <td>25, rue Lauriston</td>
      <td>Paris</td>
      <td>Western Europe</td>
      <td>75016</td>
      <td>France</td>
    </tr>
    <tr>
      <td>796</td>
      <td>11044</td>
      <td>WOLZA</td>
      <td>4</td>
      <td>2014-04-23</td>
      <td>2014-05-21</td>
      <td>2014-05-01</td>
      <td>1</td>
      <td>8.72</td>
      <td>Wolski Zajazd</td>
      <td>ul. Filtrowa 68</td>
      <td>Warszawa</td>
      <td>Eastern Europe</td>
      <td>01-012</td>
      <td>Poland</td>
    </tr>
    <tr>
      <td>797</td>
      <td>11045</td>
      <td>BOTTM</td>
      <td>6</td>
      <td>2014-04-23</td>
      <td>2014-05-21</td>
      <td>None</td>
      <td>2</td>
      <td>70.58</td>
      <td>Bottom-Dollar Markets</td>
      <td>23 Tsawassen Blvd.</td>
      <td>Tsawassen</td>
      <td>North America</td>
      <td>T2F 8M4</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>798</td>
      <td>11046</td>
      <td>WANDK</td>
      <td>8</td>
      <td>2014-04-23</td>
      <td>2014-05-21</td>
      <td>2014-04-24</td>
      <td>2</td>
      <td>71.64</td>
      <td>Die Wandernde Kuh</td>
      <td>Adenauerallee 900</td>
      <td>Stuttgart</td>
      <td>Western Europe</td>
      <td>70563</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>799</td>
      <td>11047</td>
      <td>EASTC</td>
      <td>7</td>
      <td>2014-04-24</td>
      <td>2014-05-22</td>
      <td>2014-05-01</td>
      <td>3</td>
      <td>46.62</td>
      <td>Eastern Connection</td>
      <td>35 King George</td>
      <td>London</td>
      <td>British Isles</td>
      <td>WX3 6FW</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>800</td>
      <td>11048</td>
      <td>BOTTM</td>
      <td>7</td>
      <td>2014-04-24</td>
      <td>2014-05-22</td>
      <td>2014-04-30</td>
      <td>3</td>
      <td>24.12</td>
      <td>Bottom-Dollar Markets</td>
      <td>23 Tsawassen Blvd.</td>
      <td>Tsawassen</td>
      <td>North America</td>
      <td>T2F 8M4</td>
      <td>Canada</td>
    </tr>
    <tr>
      <td>801</td>
      <td>11049</td>
      <td>GOURL</td>
      <td>3</td>
      <td>2014-04-24</td>
      <td>2014-05-22</td>
      <td>2014-05-04</td>
      <td>1</td>
      <td>8.34</td>
      <td>Gourmet Lanchonetes</td>
      <td>Av. Brasil, 442</td>
      <td>Campinas</td>
      <td>South America</td>
      <td>04876-786</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>802</td>
      <td>11050</td>
      <td>FOLKO</td>
      <td>8</td>
      <td>2014-04-27</td>
      <td>2014-05-25</td>
      <td>2014-05-05</td>
      <td>2</td>
      <td>59.41</td>
      <td>Folk och fä HB</td>
      <td>Åkergatan 24</td>
      <td>Bräcke</td>
      <td>Northern Europe</td>
      <td>S-844 67</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <td>803</td>
      <td>11051</td>
      <td>LAMAI</td>
      <td>7</td>
      <td>2014-04-27</td>
      <td>2014-05-25</td>
      <td>None</td>
      <td>3</td>
      <td>2.79</td>
      <td>La maison d'Asie</td>
      <td>1 rue Alsace-Lorraine</td>
      <td>Toulouse</td>
      <td>Western Europe</td>
      <td>31000</td>
      <td>France</td>
    </tr>
    <tr>
      <td>804</td>
      <td>11052</td>
      <td>HANAR</td>
      <td>3</td>
      <td>2014-04-27</td>
      <td>2014-05-25</td>
      <td>2014-05-01</td>
      <td>1</td>
      <td>67.26</td>
      <td>Hanari Carnes</td>
      <td>Rua do Paço, 67</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>05454-876</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>805</td>
      <td>11053</td>
      <td>PICCO</td>
      <td>2</td>
      <td>2014-04-27</td>
      <td>2014-05-25</td>
      <td>2014-04-29</td>
      <td>2</td>
      <td>53.05</td>
      <td>Piccolo und mehr</td>
      <td>Geislweg 14</td>
      <td>Salzburg</td>
      <td>Western Europe</td>
      <td>5020</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>806</td>
      <td>11054</td>
      <td>CACTU</td>
      <td>8</td>
      <td>2014-04-28</td>
      <td>2014-05-26</td>
      <td>None</td>
      <td>1</td>
      <td>0.33</td>
      <td>Cactus Comidas para llevar</td>
      <td>Cerrito 333</td>
      <td>Buenos Aires</td>
      <td>South America</td>
      <td>1010</td>
      <td>Argentina</td>
    </tr>
    <tr>
      <td>807</td>
      <td>11055</td>
      <td>HILAA</td>
      <td>7</td>
      <td>2014-04-28</td>
      <td>2014-05-26</td>
      <td>2014-05-05</td>
      <td>2</td>
      <td>120.92</td>
      <td>HILARION-Abastos</td>
      <td>Carrera 22 con Ave. Carlos Soublette #8-35</td>
      <td>San Cristóbal</td>
      <td>South America</td>
      <td>5022</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>808</td>
      <td>11056</td>
      <td>EASTC</td>
      <td>8</td>
      <td>2014-04-28</td>
      <td>2014-05-12</td>
      <td>2014-05-01</td>
      <td>2</td>
      <td>278.96</td>
      <td>Eastern Connection</td>
      <td>35 King George</td>
      <td>London</td>
      <td>British Isles</td>
      <td>WX3 6FW</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>809</td>
      <td>11057</td>
      <td>NORTS</td>
      <td>3</td>
      <td>2014-04-29</td>
      <td>2014-05-27</td>
      <td>2014-05-01</td>
      <td>3</td>
      <td>4.13</td>
      <td>North/South</td>
      <td>South House 300 Queensbridge</td>
      <td>London</td>
      <td>British Isles</td>
      <td>SW7 1RZ</td>
      <td>UK</td>
    </tr>
    <tr>
      <td>810</td>
      <td>11058</td>
      <td>BLAUS</td>
      <td>9</td>
      <td>2014-04-29</td>
      <td>2014-05-27</td>
      <td>None</td>
      <td>3</td>
      <td>31.14</td>
      <td>Blauer See Delikatessen</td>
      <td>Forsterstr. 57</td>
      <td>Mannheim</td>
      <td>Western Europe</td>
      <td>68306</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>811</td>
      <td>11059</td>
      <td>RICAR</td>
      <td>2</td>
      <td>2014-04-29</td>
      <td>2014-06-10</td>
      <td>None</td>
      <td>2</td>
      <td>85.80</td>
      <td>Ricardo Adocicados</td>
      <td>Av. Copacabana, 267</td>
      <td>Rio de Janeiro</td>
      <td>South America</td>
      <td>02389-890</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>812</td>
      <td>11060</td>
      <td>FRANS</td>
      <td>2</td>
      <td>2014-04-30</td>
      <td>2014-05-28</td>
      <td>2014-05-04</td>
      <td>2</td>
      <td>10.98</td>
      <td>Franchi S.p.A.</td>
      <td>Via Monte Bianco 34</td>
      <td>Torino</td>
      <td>Southern Europe</td>
      <td>10100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>813</td>
      <td>11061</td>
      <td>GREAL</td>
      <td>4</td>
      <td>2014-04-30</td>
      <td>2014-06-11</td>
      <td>None</td>
      <td>3</td>
      <td>14.01</td>
      <td>Great Lakes Food Market</td>
      <td>2732 Baker Blvd.</td>
      <td>Eugene</td>
      <td>North America</td>
      <td>97403</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>814</td>
      <td>11062</td>
      <td>REGGC</td>
      <td>4</td>
      <td>2014-04-30</td>
      <td>2014-05-28</td>
      <td>None</td>
      <td>2</td>
      <td>29.93</td>
      <td>Reggiani Caseifici</td>
      <td>Strada Provinciale 124</td>
      <td>Reggio Emilia</td>
      <td>Southern Europe</td>
      <td>42100</td>
      <td>Italy</td>
    </tr>
    <tr>
      <td>815</td>
      <td>11063</td>
      <td>HUNGO</td>
      <td>3</td>
      <td>2014-04-30</td>
      <td>2014-05-28</td>
      <td>2014-05-06</td>
      <td>2</td>
      <td>81.73</td>
      <td>Hungry Owl All-Night Grocers</td>
      <td>8 Johnstown Road</td>
      <td>Cork</td>
      <td>British Isles</td>
      <td>None</td>
      <td>Ireland</td>
    </tr>
    <tr>
      <td>816</td>
      <td>11064</td>
      <td>SAVEA</td>
      <td>1</td>
      <td>2014-05-01</td>
      <td>2014-05-29</td>
      <td>2014-05-04</td>
      <td>1</td>
      <td>30.09</td>
      <td>Save-a-lot Markets</td>
      <td>187 Suffolk Ln.</td>
      <td>Boise</td>
      <td>North America</td>
      <td>83720</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>817</td>
      <td>11065</td>
      <td>LILAS</td>
      <td>8</td>
      <td>2014-05-01</td>
      <td>2014-05-29</td>
      <td>None</td>
      <td>1</td>
      <td>12.91</td>
      <td>LILA-Supermercado</td>
      <td>Carrera 52 con Ave. Bolívar #65-98 Llano Largo</td>
      <td>Barquisimeto</td>
      <td>South America</td>
      <td>3508</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>818</td>
      <td>11066</td>
      <td>WHITC</td>
      <td>7</td>
      <td>2014-05-01</td>
      <td>2014-05-29</td>
      <td>2014-05-04</td>
      <td>2</td>
      <td>44.72</td>
      <td>White Clover Markets</td>
      <td>1029 - 12th Ave. S.</td>
      <td>Seattle</td>
      <td>North America</td>
      <td>98124</td>
      <td>USA</td>
    </tr>
    <tr>
      <td>819</td>
      <td>11067</td>
      <td>DRACD</td>
      <td>1</td>
      <td>2014-05-04</td>
      <td>2014-05-18</td>
      <td>2014-05-06</td>
      <td>2</td>
      <td>7.98</td>
      <td>Drachenblut Delikatessen</td>
      <td>Walserweg 21</td>
      <td>Aachen</td>
      <td>Western Europe</td>
      <td>52066</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>820</td>
      <td>11068</td>
      <td>QUEE</td>
      <td>8</td>
      <td>2014-05-04</td>
      <td>2014-06-01</td>
      <td>None</td>
      <td>2</td>
      <td>81.75</td>
      <td>Queen Cozinha</td>
      <td>Alameda dos Canàrios, 891</td>
      <td>Sao Paulo</td>
      <td>South America</td>
      <td>05487-020</td>
      <td>Brazil</td>
    </tr>
    <tr>
      <td>821</td>
      <td>11069</td>
      <td>TORTU</td>
      <td>1</td>
      <td>2014-05-04</td>
      <td>2014-06-01</td>
      <td>2014-05-06</td>
      <td>2</td>
      <td>15.67</td>
      <td>Tortuga Restaurante</td>
      <td>Avda. Azteca 123</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05033</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>822</td>
      <td>11070</td>
      <td>LEHMS</td>
      <td>2</td>
      <td>2014-05-05</td>
      <td>2014-06-02</td>
      <td>None</td>
      <td>1</td>
      <td>136.00</td>
      <td>Lehmanns Marktstand</td>
      <td>Magazinweg 7</td>
      <td>Frankfurt a.M.</td>
      <td>Western Europe</td>
      <td>60528</td>
      <td>Germany</td>
    </tr>
    <tr>
      <td>823</td>
      <td>11071</td>
      <td>LILAS</td>
      <td>1</td>
      <td>2014-05-05</td>
      <td>2014-06-02</td>
      <td>None</td>
      <td>1</td>
      <td>0.93</td>
      <td>LILA-Supermercado</td>
      <td>Carrera 52 con Ave. Bolívar #65-98 Llano Largo</td>
      <td>Barquisimeto</td>
      <td>South America</td>
      <td>3508</td>
      <td>Venezuela</td>
    </tr>
    <tr>
      <td>824</td>
      <td>11072</td>
      <td>ERNSH</td>
      <td>4</td>
      <td>2014-05-05</td>
      <td>2014-06-02</td>
      <td>None</td>
      <td>2</td>
      <td>258.64</td>
      <td>Ernst Handel</td>
      <td>Kirchgasse 6</td>
      <td>Graz</td>
      <td>Western Europe</td>
      <td>8010</td>
      <td>Austria</td>
    </tr>
    <tr>
      <td>825</td>
      <td>11073</td>
      <td>PERIC</td>
      <td>2</td>
      <td>2014-05-05</td>
      <td>2014-06-02</td>
      <td>None</td>
      <td>2</td>
      <td>24.95</td>
      <td>Pericles Comidas clásicas</td>
      <td>Calle Dr. Jorge Cash 321</td>
      <td>México D.F.</td>
      <td>Central America</td>
      <td>05033</td>
      <td>Mexico</td>
    </tr>
    <tr>
      <td>826</td>
      <td>11074</td>
      <td>SIMOB</td>
      <td>7</td>
      <td>2014-05-06</td>
      <td>2014-06-03</td>
      <td>None</td>
      <td>2</td>
      <td>18.44</td>
      <td>Simons bistro</td>
      <td>Vinbæltet 34</td>
      <td>Kobenhavn</td>
      <td>Northern Europe</td>
      <td>1734</td>
      <td>Denmark</td>
    </tr>
    <tr>
      <td>827</td>
      <td>11075</td>
      <td>RICSU</td>
      <td>8</td>
      <td>2014-05-06</td>
      <td>2014-06-03</td>
      <td>None</td>
      <td>2</td>
      <td>6.19</td>
      <td>Richter Supermarkt</td>
      <td>Starenweg 5</td>
      <td>Genève</td>
      <td>Western Europe</td>
      <td>1204</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <td>828</td>
      <td>11076</td>
      <td>BONAP</td>
      <td>4</td>
      <td>2014-05-06</td>
      <td>2014-06-03</td>
      <td>None</td>
      <td>2</td>
      <td>38.28</td>
      <td>Bon app'</td>
      <td>12, rue des Bouchers</td>
      <td>Marseille</td>
      <td>Western Europe</td>
      <td>13008</td>
      <td>France</td>
    </tr>
    <tr>
      <td>829</td>
      <td>11077</td>
      <td>RATTC</td>
      <td>1</td>
      <td>2014-05-06</td>
      <td>2014-06-03</td>
      <td>None</td>
      <td>2</td>
      <td>8.53</td>
      <td>Rattlesnake Canyon Grocery</td>
      <td>2817 Milton Dr.</td>
      <td>Albuquerque</td>
      <td>North America</td>
      <td>87110</td>
      <td>USA</td>
    </tr>
  </tbody>
</table>
</div>



## Merge the Two Tables


```python
df_order_use = pd.merge(df_order, df_order_detail, left_on='Id', right_on='OrderId')
df_order_use.head()
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
      <th>Id_x</th>
      <th>CustomerId</th>
      <th>EmployeeId</th>
      <th>OrderDate</th>
      <th>RequiredDate</th>
      <th>ShippedDate</th>
      <th>ShipVia</th>
      <th>Freight</th>
      <th>ShipName</th>
      <th>ShipAddress</th>
      <th>ShipCity</th>
      <th>ShipRegion</th>
      <th>ShipPostalCode</th>
      <th>ShipCountry</th>
      <th>Id_y</th>
      <th>OrderId</th>
      <th>ProductId</th>
      <th>UnitPrice</th>
      <th>Quantity</th>
      <th>Discount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>10248</td>
      <td>VINET</td>
      <td>5</td>
      <td>2012-07-04</td>
      <td>2012-08-01</td>
      <td>2012-07-16</td>
      <td>3</td>
      <td>32.38</td>
      <td>Vins et alcools Chevalier</td>
      <td>59 rue de l'Abbaye</td>
      <td>Reims</td>
      <td>Western Europe</td>
      <td>51100</td>
      <td>France</td>
      <td>10248/11</td>
      <td>10248</td>
      <td>11</td>
      <td>14.0</td>
      <td>12</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>10248</td>
      <td>VINET</td>
      <td>5</td>
      <td>2012-07-04</td>
      <td>2012-08-01</td>
      <td>2012-07-16</td>
      <td>3</td>
      <td>32.38</td>
      <td>Vins et alcools Chevalier</td>
      <td>59 rue de l'Abbaye</td>
      <td>Reims</td>
      <td>Western Europe</td>
      <td>51100</td>
      <td>France</td>
      <td>10248/42</td>
      <td>10248</td>
      <td>42</td>
      <td>9.8</td>
      <td>10</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>2</td>
      <td>10248</td>
      <td>VINET</td>
      <td>5</td>
      <td>2012-07-04</td>
      <td>2012-08-01</td>
      <td>2012-07-16</td>
      <td>3</td>
      <td>32.38</td>
      <td>Vins et alcools Chevalier</td>
      <td>59 rue de l'Abbaye</td>
      <td>Reims</td>
      <td>Western Europe</td>
      <td>51100</td>
      <td>France</td>
      <td>10248/72</td>
      <td>10248</td>
      <td>72</td>
      <td>34.8</td>
      <td>5</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>3</td>
      <td>10249</td>
      <td>TOMSP</td>
      <td>6</td>
      <td>2012-07-05</td>
      <td>2012-08-16</td>
      <td>2012-07-10</td>
      <td>1</td>
      <td>11.61</td>
      <td>Toms Spezialitäten</td>
      <td>Luisenstr. 48</td>
      <td>Münster</td>
      <td>Western Europe</td>
      <td>44087</td>
      <td>Germany</td>
      <td>10249/14</td>
      <td>10249</td>
      <td>14</td>
      <td>18.6</td>
      <td>9</td>
      <td>0.0</td>
    </tr>
    <tr>
      <td>4</td>
      <td>10249</td>
      <td>TOMSP</td>
      <td>6</td>
      <td>2012-07-05</td>
      <td>2012-08-16</td>
      <td>2012-07-10</td>
      <td>1</td>
      <td>11.61</td>
      <td>Toms Spezialitäten</td>
      <td>Luisenstr. 48</td>
      <td>Münster</td>
      <td>Western Europe</td>
      <td>44087</td>
      <td>Germany</td>
      <td>10249/51</td>
      <td>10249</td>
      <td>51</td>
      <td>42.4</td>
      <td>40</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>



## Create Revenue Column and Add to Table


```python
df_order_use['Revenue'] = revenue(df_order_use['UnitPrice'], df_order_use['Quantity'])
df_order_use.head()
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
      <th>Id_x</th>
      <th>CustomerId</th>
      <th>EmployeeId</th>
      <th>OrderDate</th>
      <th>RequiredDate</th>
      <th>ShippedDate</th>
      <th>ShipVia</th>
      <th>Freight</th>
      <th>ShipName</th>
      <th>ShipAddress</th>
      <th>...</th>
      <th>ShipRegion</th>
      <th>ShipPostalCode</th>
      <th>ShipCountry</th>
      <th>Id_y</th>
      <th>OrderId</th>
      <th>ProductId</th>
      <th>UnitPrice</th>
      <th>Quantity</th>
      <th>Discount</th>
      <th>Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>10248</td>
      <td>VINET</td>
      <td>5</td>
      <td>2012-07-04</td>
      <td>2012-08-01</td>
      <td>2012-07-16</td>
      <td>3</td>
      <td>32.38</td>
      <td>Vins et alcools Chevalier</td>
      <td>59 rue de l'Abbaye</td>
      <td>...</td>
      <td>Western Europe</td>
      <td>51100</td>
      <td>France</td>
      <td>10248/11</td>
      <td>10248</td>
      <td>11</td>
      <td>14.0</td>
      <td>12</td>
      <td>0.0</td>
      <td>168.0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>10248</td>
      <td>VINET</td>
      <td>5</td>
      <td>2012-07-04</td>
      <td>2012-08-01</td>
      <td>2012-07-16</td>
      <td>3</td>
      <td>32.38</td>
      <td>Vins et alcools Chevalier</td>
      <td>59 rue de l'Abbaye</td>
      <td>...</td>
      <td>Western Europe</td>
      <td>51100</td>
      <td>France</td>
      <td>10248/42</td>
      <td>10248</td>
      <td>42</td>
      <td>9.8</td>
      <td>10</td>
      <td>0.0</td>
      <td>98.0</td>
    </tr>
    <tr>
      <td>2</td>
      <td>10248</td>
      <td>VINET</td>
      <td>5</td>
      <td>2012-07-04</td>
      <td>2012-08-01</td>
      <td>2012-07-16</td>
      <td>3</td>
      <td>32.38</td>
      <td>Vins et alcools Chevalier</td>
      <td>59 rue de l'Abbaye</td>
      <td>...</td>
      <td>Western Europe</td>
      <td>51100</td>
      <td>France</td>
      <td>10248/72</td>
      <td>10248</td>
      <td>72</td>
      <td>34.8</td>
      <td>5</td>
      <td>0.0</td>
      <td>174.0</td>
    </tr>
    <tr>
      <td>3</td>
      <td>10249</td>
      <td>TOMSP</td>
      <td>6</td>
      <td>2012-07-05</td>
      <td>2012-08-16</td>
      <td>2012-07-10</td>
      <td>1</td>
      <td>11.61</td>
      <td>Toms Spezialitäten</td>
      <td>Luisenstr. 48</td>
      <td>...</td>
      <td>Western Europe</td>
      <td>44087</td>
      <td>Germany</td>
      <td>10249/14</td>
      <td>10249</td>
      <td>14</td>
      <td>18.6</td>
      <td>9</td>
      <td>0.0</td>
      <td>167.4</td>
    </tr>
    <tr>
      <td>4</td>
      <td>10249</td>
      <td>TOMSP</td>
      <td>6</td>
      <td>2012-07-05</td>
      <td>2012-08-16</td>
      <td>2012-07-10</td>
      <td>1</td>
      <td>11.61</td>
      <td>Toms Spezialitäten</td>
      <td>Luisenstr. 48</td>
      <td>...</td>
      <td>Western Europe</td>
      <td>44087</td>
      <td>Germany</td>
      <td>10249/51</td>
      <td>10249</td>
      <td>51</td>
      <td>42.4</td>
      <td>40</td>
      <td>0.0</td>
      <td>1696.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 21 columns</p>
</div>




```python
df_order_use['ShipRegion'].unique()
# 9 shipping locations
```




    array(['Western Europe', 'South America', 'Central America',
           'North America', 'Northern Europe', 'Scandinavia',
           'Southern Europe', 'British Isles', 'Eastern Europe'], dtype=object)



## Create Dictionaries for Each Region


```python
data_region = {}
for region in df_order_use['ShipRegion'].unique():
    print(region)
    data_region[region] = df_order_use.groupby('ShipRegion').get_group(region)['Revenue']
    
data_region
```

    Western Europe
    South America
    Central America
    North America
    Northern Europe
    Scandinavia
    Southern Europe
    British Isles
    Eastern Europe





    {'Western Europe': 0         168.00
     1          98.00
     2         174.00
     3         167.40
     4        1696.00
     8         100.80
     9         234.00
     10        336.00
     11       2592.00
     12         50.00
     13       1088.00
     17         54.00
     18        403.20
     19        168.00
     20        304.00
     21        486.50
     22        380.00
     23       1320.00
     29        760.00
     30       1105.00
     31        153.60
     34        123.20
     35        780.00
     36        591.00
     37        252.00
     43        834.00
     44        100.80
     45       1242.00
     46        288.00
     49        936.00
     50        240.00
     52        735.00
     53       3080.00
     54        216.00
     65        595.20
     66        150.00
     67         40.00
     68        882.00
     69        475.20
     70        344.00
     71        194.60
     76        728.00
     77        472.80
     82        468.00
     95        526.50
     96        325.50
     97        544.00
     98         56.00
     99        648.00
     100       588.00
     101       943.20
     102      1440.00
     103      1576.00
     128       121.60
     132       864.00
     133       556.00
     142       147.00
     143       608.00
     144      1248.00
     145      1019.20
     146       441.60
     170        67.20
     171       201.60
     172       145.60
     173       883.20
     174       524.00
     175        62.00
     176       182.40
     193        62.00
     194        44.80
     195        57.60
     201       120.00
     202        57.60
     203       167.40
     204        40.00
     205      1112.00
     222        88.50
     229        44.80
     230       100.00
     236       288.00
     237       597.60
     238       304.00
     239       582.40
     240       695.00
     246      1000.00
     247        92.40
     248      1472.00
     251       364.80
     252       560.00
     253       608.00
     254       768.00
     255      1330.00
     256        40.00
     257       216.00
     260      2240.00
     261       584.00
     262       100.80
     269       216.00
     270       180.00
     272       195.00
     273       518.40
     274      4216.00
     275       100.10
     276      1193.50
     277       168.00
     280       201.60
     281     10540.00
     286       300.00
     287       230.40
     288       576.00
     292        36.00
     293       112.00
     294       304.00
     298      1092.00
     299      3465.00
     300      2108.00
     301       560.00
     302       165.20
     303       777.60
     304      1496.00
     305       560.00
     306       848.00
     307       141.60
     308       200.00
     309        74.40
     310       172.80
     320        40.00
     321       473.20
     322       390.00
     323       931.00
     326       216.00
     327       798.00
     328       160.00
     329        91.20
     352       544.00
     353       450.00
     354      1386.00
     355       120.00
     356       400.00
     378       600.00
     379       576.00
     380       432.00
     381       667.20
     382        86.40
     383      1440.00
     394       288.00
     395      1032.00
     396       583.80
     412       432.00
     413      2281.50
     414       291.90
     415       714.00
     425       504.00
     426       432.00
     427       258.00
     428       208.00
     429        35.40
     430      1379.00
     439       345.60
     440      1576.00
     441       201.60
     453       912.00
     454       418.00
     455       364.80
     456       120.00
     457      1632.00
     458       576.00
     473       192.00
     474       288.00
     477       651.00
     481      1404.00
     482       400.00
     483       912.00
     484      3080.00
     496        48.00
     497      1216.00
     498       798.00
     499       148.80
     501       109.50
     502       224.00
     503       234.00
     513       504.00
     514       472.00
     515       816.00
     524        87.60
     525        72.00
     526        30.00
     527        84.00
     533       347.20
     534       112.00
     535      1379.00
     536       496.00
     537        35.40
     538      2304.00
     539       931.00
     540       470.40
     541       572.00
     546       278.00
     547        40.00
     548        96.00
     553       320.00
     554       336.00
     555      1584.00
     556       747.00
     557      1092.00
     558       736.00
     559       456.00
     560       860.00
     561       384.00
     562       192.00
     563      1112.00
     571       153.30
     572       560.00
     586       165.60
     587       552.00
     591      1500.00
     592       108.00
     593       212.80
     604       350.00
     605       816.00
     606       604.80
     612       496.00
     617       228.00
     618       528.00
     637      1320.00
     638       240.00
     639       252.00
     640       250.20
     648       252.00
     649       136.00
     650       288.00
     656       425.60
     657       695.00
     658       260.00
     664       186.00
     665       364.80
     666       149.00
     677       252.00
     678       210.00
     681        60.00
     682       180.00
     683       136.80
     686      1100.00
     687      1500.00
     688       400.00
     693       400.00
     694      1600.00
     695       427.50
     696      3159.00
     697      1596.00
     698      2660.00
     699       820.95
     700       387.50
     701      1552.00
     702       872.50
     703      5268.00
     704        40.00
     705      2856.00
     715       496.00
     716      1520.00
     717       340.00
     723       720.00
     724       960.00
     725       517.80
     726       460.00
     735       570.00
     736       276.00
     740      1100.00
     741       570.00
     745       336.00
     746       250.00
     747       360.00
     748      1560.00
     749      1150.00
     750       570.00
     751       900.00
     758       258.90
     759       184.00
     760        74.50
     765       570.00
     766       250.00
     767        75.00
     768      1190.00
     769       375.00
     770       318.00
     771       265.00
     772       730.80
     773       135.00
     780       600.00
     781      1249.20
     782      7905.00
     783       437.50
     788       315.00
     789       178.80
     795       300.00
     796       540.00
     797      1972.00
     800       140.00
     801       135.10
     802       687.50
     803       950.00
     804      2544.00
     819       523.50
     820       180.00
     821       986.00
     822       130.00
     829       997.50
     830       155.00
     836       115.80
     837       432.00
     838       517.80
     839       739.50
     851       735.00
     852      1125.00
     853       180.00
     862       255.75
     863       392.00
     875       660.00
     876       263.40
     877      1044.00
     878       180.00
     889       348.75
     890        86.85
     891       631.50
     893        78.00
     894       252.00
     898       625.00
     904      2500.00
     905      1400.00
     912       387.50
     913       156.15
     914      1701.00
     915       720.00
     916        72.00
     919       540.00
     920      3420.00
     921      2340.00
     925       157.50
     926       390.00
     927       252.60
     952      1064.00
     953        54.00
     954       310.00
     955        60.00
     956       399.00
     967       294.00
     968        80.00
     969        90.00
     989       488.25
     990       138.00
     991       250.00
     992        13.50
     993       540.00
     1005      450.00
     1008      288.00
     1009      630.00
     1010       62.00
     1011      570.00
     1012       50.00
     1013     1368.00
     1014       78.00
     1015     1093.05
     1016     3944.00
     1017     1050.00
     1018     3125.00
     1019      795.00
     1020       15.50
     1033      720.00
     1034      225.00
     1039      684.00
     1040      378.00
     1041       24.00
     1055      912.00
     1056      522.00
     1060      110.40
     1061      420.00
     1064      523.50
     1065      680.00
     1079      600.00
     1080     1288.00
     1081     1870.00
     1082      910.00
     1090      552.00
     1091      420.00
     1092     1060.00
     1099     4456.44
     1100      210.50
     1101     1620.00
     1102      301.00
     1103      100.00
     1104       96.00
     1105      498.75
     1107      288.00
     1108      720.00
     1109      350.00
     1110      750.00
     1111      193.75
     1112      174.50
     1113      493.00
     1114      252.60
     1121      697.50
     1122      328.00
     1123      397.50
     1133      660.00
     1143       63.00
     1144      368.00
     1145      380.00
     1146     1020.00
     1150     1170.00
     1151      468.45
     1161      540.00
     1162     4951.60
     1163     1840.00
     1164      466.80
     1165     2366.40
     1166      878.00
     1171     2700.00
     1172     1375.00
     1173      750.00
     1183      315.00
     1184      312.00
     1185     1485.48
     1186     1368.25
     1187      120.00
     1188      114.00
     1196       60.00
     1197      270.00
     1233      651.00
     1234      645.00
     1238      320.00
     1239      111.75
     1240      900.00
     1241     1368.00
     1242      349.00
     1243      760.00
     1244      986.00
     1250      972.50
     1273      261.75
     1274       37.50
     1275      210.50
     1276      400.00
     1277     1590.00
     1278      360.00
     1289       24.00
     1290      115.80
     1291       52.35
     1292      114.00
     1293      126.00
     1304     1500.00
     1305      311.20
     1306     2475.00
     1307      243.60
     1308       36.00
     1309      392.00
     1310      443.70
     1311     1440.00
     1312      100.00
     1313      337.75
     1314      395.10
     1315     1080.00
     1325      374.76
     1326      776.70
     1327      325.00
     1328      225.00
     1334      285.00
     1335     1140.00
     1336      273.00
     1337      900.00
     1346      624.60
     1347      420.00
     1348      600.00
     1350      168.00
     1351     1756.00
     1352     1380.00
     1359      400.00
     1360      126.00
     1361       90.00
     1362      200.00
     1363     2340.00
     1364     1684.00
     1365      760.00
     1366     1050.00
     1367      500.00
     1368       28.00
     1378      344.00
     1379     2228.22
     1380     1375.00
     1381     1287.00
     1382      875.00
     1383       54.25
     1388      200.00
     1389      168.00
     1390      256.50
     1391     6360.00
     1394      349.00
     1395      986.00
     1412      285.00
     1413     2475.80
     1414      460.00
     1415      310.00
     1416     1875.00
     1417      270.00
     1418     1317.00
     1419      225.00
     1422     1733.06
     1423      193.00
     1431     1134.25
     1432     1365.00
     1437      420.00
     1440      120.00
     1441       90.00
     1442     1375.00
     1460      380.00
     1461       42.10
     1462      150.00
     1478      193.00
     1479      920.00
     1480      102.00
     1481      855.00
     1485     1249.20
     1486     7905.00
     1487     1104.00
     1488     1232.50
     1504      374.76
     1505      656.00
     1506      437.50
     1507      292.50
     1508      465.00
     1509      378.00
     1524       18.00
     1525      140.00
     1526      311.20
     1527       99.75
     1528      600.00
     1529      112.50
     1530      295.20
     1533      825.00
     1534       26.00
     1535     1092.00
     1536      108.00
     1537      468.00
     1538     2040.00
     1539      997.50
     1551      496.00
     1552     1140.00
     1553     2750.00
     1554      195.00
     1559      212.00
     1560      735.00
     1561      630.00
     1562      450.00
     1563      588.00
     1564      795.00
     1565     1596.00
     1566      462.00
     1567      450.00
     1568      200.00
     1577      490.00
     1578      562.14
     1579      280.00
     1580       10.00
     1581      450.00
     1589      625.00
     1590     3100.00
     1591      390.00
     1601      150.00
     1602      439.00
     1603       60.00
     1604      180.00
     1605      260.75
     1606      997.50
     1607      159.00
     1608      360.00
     1614      525.00
     1615       56.00
     1620    15810.00
     1621     1440.00
     1635     1250.00
     1636      209.40
     1637      624.00
     1648      252.00
     1649      665.00
     1652     1620.00
     1667      380.00
     1668       54.00
     1669      450.00
     1670      325.00
     1679      585.00
     1680      140.00
     1681      135.10
     1682      388.35
     1683     2200.00
     1684     1200.00
     1685       45.00
     1686     2970.96
     1687      906.15
     1688      380.00
     1692      495.00
     1693      810.00
     1694     1674.40
     1695     3400.00
     1696      142.50
     1697      608.00
     1714      108.50
     1750      140.00
     1751      460.00
     1752      336.00
     1762      405.00
     1763       35.00
     1764      360.00
     1767      600.00
     1768      379.75
     1769      195.00
     1770      360.00
     1771     1097.50
     1772      600.00
     1773      397.50
     1774      252.00
     1775      585.00
     1776      523.50
     1777      690.20
     1778      556.80
     1779      155.00
     1782      500.00
     1789      120.00
     1790     1104.00
     1791     1666.00
     1792      752.50
     1795      240.00
     1796      120.00
     1808      120.00
     1809      125.00
     1822       37.50
     1823       57.90
     1824      387.50
     1825      400.00
     1826       91.20
     1834      120.00
     1835      133.00
     1836      424.00
     1848     1350.00
     1849      462.00
     1850      656.00
     1851      324.00
     1852      792.00
     1854      375.00
     1855     1317.50
     1856      360.00
     1858      208.00
     1859      456.00
     1860      591.60
     1861      110.40
     1862      800.00
     1863     1140.00
     1864      135.00
     1865      133.00
     1868     1733.06
     1869      234.00
     1870       17.50
     1871      156.15
     1872       57.90
     1873       77.50
     1882      800.00
     1883      400.00
     1884      184.00
     1885      116.70
     1886      540.00
     1887      760.00
     1888      360.00
     1889     1317.00
     1890      300.00
     1891     1536.50
     1916      650.00
     1917      840.00
     1918     1560.00
     1919     1881.00
     1920      950.00
     1921      300.00
     1922     1620.00
     1929      560.00
     1937      193.00
     1938      795.00
     1939      273.00
     1954      187.38
     1955      108.00
     1963     3192.00
     1964     1260.00
     1965      451.50
     1971      530.00
     1972      430.00
     1973      460.00
     1974     1224.00
     1975     1290.00
     1985      250.00
     1986     6050.00
     1987      450.00
     1993      744.00
     1994      209.00
     1995     1215.00
     1996     1967.49
     1997     2332.00
     1998     1218.00
     2013      840.00
     2014     1320.00
     2015      760.00
     2016      526.80
     2029     2296.00
     2030     1296.00
     2034      180.00
     2035     1080.00
     2036      420.00
     2037       74.50
     2038       42.00
     2039     1650.00
     2041       92.00
     2042       14.00
     2043      645.00
     2049      570.00
     2050     1317.00
     2053      210.00
     2057      760.00
     2058      480.00
     2059      324.00
     2066       45.00
     2069     2187.50
     2070      640.00
     2071      831.25
     2082       30.00
     2083      714.00
     2084      114.00
     2106       86.85
     2111      720.00
     2112      380.00
     2113      523.50
     2114      250.00
     2117      152.00
     2118      386.00
     2119      357.50
     2120     4322.50
     2124      190.00
     2125      360.00
     2126       36.00
     2127      500.00
     2128      465.00
     2129       92.00
     Name: Revenue, dtype: float64, 'South America': 5          77.00
     6        1484.00
     7         252.00
     14        200.00
     15        604.80
     16        640.00
     24        393.00
     25        124.80
     26        877.50
     27         86.40
     28        156.00
     38        160.00
     39        288.00
     55        990.00
     56        111.20
     91        248.00
     92        131.40
     93        952.00
     94         83.40
     104       556.00
     105       224.00
     106       144.00
     111       340.00
     112      1485.00
     113       240.00
     114       104.00
     115        96.00
     116       372.00
     117        84.80
     118      1296.00
     129       201.60
     130       417.00
     131       432.00
     138       109.50
     139       240.00
     220      1245.00
     221       695.00
     265       112.00
     266       720.00
     267        58.80
     268        37.20
     289       744.00
     290       398.40
     291       217.60
     330       777.60
     331      8432.00
     332      1904.00
     333      1167.60
     344        61.60
     345       561.60
     346       336.00
     351       112.00
     365        54.00
     366       112.00
     391       268.80
     392      1834.00
     393       230.40
     419       400.00
     420       144.00
     421       240.00
     422      1528.80
     423        76.00
     424        29.40
     431       223.20
     432        96.00
     442       131.40
     443       100.00
     459      1552.00
     460         9.60
     461        96.00
     462       240.00
     463        29.20
     464       747.00
     465       393.00
     466       104.00
     468       140.00
     469       880.00
     528       292.00
     529       588.00
     530        34.40
     531       149.40
     532       294.00
     566       320.00
     567       579.60
     568      1152.00
     582       168.00
     583        48.00
     607        38.40
     608       144.00
     619       384.00
     620      1088.00
     627       304.00
     628       160.00
     629       576.00
     630       720.00
     631        84.00
     632      1060.00
     633       128.00
     634        36.50
     635       747.00
     636       141.60
     641      2640.00
     642       300.00
     643       223.20
     651       912.00
     655       200.00
     659        63.00
     660        92.00
     661       420.00
     662       912.00
     663       500.00
     689        45.00
     690       108.00
     691        57.00
     692       408.00
     720        54.00
     721        96.50
     722        75.00
     752       110.00
     784       157.50
     785      1054.00
     786       757.80
     787       193.50
     790      1140.00
     791       630.00
     812       648.00
     813       232.50
     844       475.00
     845       490.00
     892       387.50
     899       142.50
     901       187.38
     902       360.00
     903       260.00
     933       360.00
     934      1925.00
     944       440.00
     945       480.00
     946       493.00
     965        48.00
     966       310.00
     987       380.00
     988       225.00
     1026      210.00
     1027      406.25
     1028     2280.00
     1029      190.00
     1030      442.05
     1031     2088.00
     1035      950.00
     1036     1104.00
     1042      250.00
     1043      920.00
     1044      252.00
     1045     1250.00
     1046      285.00
     1051      276.00
     1052      360.00
     1053      315.00
     1054       67.50
     1057      776.70
     1058      820.00
     1059      223.50
     1062       51.78
     1063      280.00
     1083      250.00
     1084      441.60
     1085      600.00
     1147      620.00
     1148       38.60
     1149      142.50
     1159      760.00
     1160      390.00
     1179       64.40
     1180      162.00
     1181      397.50
     1182      450.00
     1201      132.00
     1202      157.50
     1203      306.00
     1204      250.00
     1205      128.00
     1214     1600.00
     1215     1484.00
     1216      340.00
     1235       50.00
     1236      371.00
     1237      285.00
     1248      378.00
     1249      172.00
     1258      115.80
     1259       28.00
     1260      144.00
     1266      388.35
     1267      110.40
     1268      288.00
     1269      510.00
     1270      900.00
     1271      300.00
     1272      650.00
     1282      750.00
     1283      388.35
     1284      360.00
     1377      315.00
     1392      280.00
     1396      525.00
     1397      195.00
     1401       12.50
     1402      125.00
     1403     1317.50
     1407      310.00
     1408       77.50
     1409     1200.00
     1410      388.35
     1411      325.50
     1420       90.00
     1421      760.00
     1429      348.75
     1430       44.70
     1433      655.83
     1434      194.50
     1435     1163.75
     1436      864.00
     1452      220.80
     1453      210.00
     1454      825.00
     1466      140.00
     1470      138.00
     1471      162.00
     1472      552.00
     1476      228.00
     1477      420.00
     1491      322.00
     1492      155.00
     1498      420.00
     1499      292.50
     1500     2200.00
     1501      195.00
     1510      405.00
     1511      527.00
     1516      150.00
     1517      504.00
     1518     1020.00
     1519      300.00
     1531      990.32
     1532      517.80
     1544       72.00
     1545     1562.50
     1546      950.00
     1547      397.50
     1548      522.00
     1549       84.00
     1550      180.00
     1582       95.00
     1583      140.00
     1584      195.00
     1585     2310.00
     1616      360.00
     1617      159.00
     1626      624.60
     1627      540.00
     1628      840.00
     1650      523.50
     1651     1562.50
     1659      150.00
     1671     2170.00
     1672      437.50
     1673      520.00
     1700       30.00
     1701      144.00
     1702       45.00
     1703      289.50
     1704      645.00
     1707      240.00
     1708      442.05
     1709      250.00
     1712      360.00
     1728      660.00
     1729      100.00
     1730      198.75
     1731      537.50
     1735      104.70
     1736      192.00
     1737      390.00
     1742      418.80
     1743      336.00
     1744      368.00
     1748      585.00
     1749      157.50
     1756      475.00
     1757       84.00
     1783      378.00
     1784      250.00
     1785       72.00
     1787      364.80
     1788      280.00
     1829      488.60
     1830      312.50
     1831      285.00
     1832      816.00
     1837      776.70
     1838      720.00
     1839      266.00
     1840      427.00
     1841      180.00
     1842      174.00
     1843      155.00
     1844       45.00
     1845      231.60
     1846       42.00
     1847     1080.00
     1866      108.00
     1877      912.00
     1893    15810.00
     1904      630.00
     1905     1215.00
     1906      180.00
     1907      195.00
     1913     1000.00
     1914      315.00
     1915       38.60
     1930     1600.00
     1931      240.00
     1932      140.00
     1980      270.20
     1991       36.00
     1992       40.00
     1999      322.00
     2000     1080.00
     2044      912.00
     2045      432.00
     2046     1200.00
     2047      546.00
     2051      291.75
     2052      114.00
     2063      190.00
     2064      152.00
     2067     1380.00
     2068      285.00
     2072       25.00
     2073      280.00
     2074       67.50
     2075      210.00
     2076     1060.00
     2077      390.00
     2085      180.00
     2086      468.00
     2087     1190.00
     2101      103.56
     2102      149.00
     2107      364.80
     2108     1656.00
     2109      364.00
     2115      450.00
     2116       60.00
     Name: Revenue, dtype: float64, 'Central America': 32        80.00
     33        20.80
     74       372.00
     75        48.00
     119      600.00
     120       36.00
     121      175.50
     122       37.20
     150      480.00
     151      440.00
     152       34.40
     161       28.80
     162       60.00
     187      249.60
     188      509.60
     189      432.00
     192      112.00
     282      172.80
     283      396.00
     313      403.20
     600      223.20
     601      655.20
     602      308.70
     603       62.00
     667      199.50
     668      196.80
     669      420.00
     679      690.00
     680      191.25
     712       22.50
     713     3952.50
     714      175.05
     761     1050.00
     762      184.00
     763       97.50
     764      825.00
     868      702.00
     869      560.00
     870      820.00
     879      180.00
     880      250.00
     881      408.45
     997       69.75
     998       70.00
     999      340.00
     1124      62.00
     1125      64.40
     1126     408.45
     1127     936.90
     1128      20.00
     1140      75.00
     1141      68.00
     1142     232.50
     1349     320.00
     1555     315.00
     1556     230.00
     1557     250.00
     1558     180.00
     1596     380.00
     1597     280.00
     1732     390.00
     1733      75.00
     1734      74.50
     1758      42.00
     1759      60.00
     1760      64.40
     1761     348.00
     1927    1060.00
     1928     136.00
     2110     360.00
     2121     210.00
     2122      90.00
     Name: Revenue, dtype: float64, 'North America': 40        204.00
     41        360.00
     42         60.80
     57        120.00
     58        556.00
     61         48.00
     62        388.80
     63        400.00
     64        667.20
     123       259.20
     124       468.00
     125       552.00
     126       571.20
     127        37.20
     153      1250.00
     154      2475.00
     155       432.00
     159       394.00
     160        30.00
     168       139.00
     169       197.00
     177      1024.00
     178       318.00
     179       985.00
     182        77.00
     183      2758.00
     184       288.00
     196       291.90
     197      1008.00
     198       288.00
     199      1760.00
     200      2808.00
     216        73.00
     217       165.60
     218      4216.00
     219       364.80
     223      2000.00
     224       112.00
     225       121.60
     241       624.00
     242       310.50
     243       176.00
     244      2184.00
     245      1103.20
     258       616.00
     259      2240.00
     263      1123.20
     264       608.00
     271       141.60
     324      1980.00
     325       547.20
     338       279.00
     339        59.00
     340       420.00
     362       240.00
     363       544.00
     364        80.00
     374       396.80
     375       288.00
     376       788.00
     377       360.00
     384       380.00
     385       781.20
     386        78.40
     387      1743.00
     388       320.00
     389        48.00
     390       394.00
     399       432.00
     400      2304.00
     408       372.60
     409      2128.00
     410       336.00
     411      1032.00
     433        98.00
     434       704.00
     435       192.50
     436       620.00
     437       396.00
     444        62.40
     445        40.00
     470       864.00
     471     10329.20
     472       300.00
     485      1560.00
     486       735.00
     487       228.00
     488       249.00
     489       236.00
     504       456.00
     505       222.40
     506       159.60
     507       240.00
     508       684.00
     509       681.10
     510      2376.00
     511      2052.00
     512      1755.00
     542       546.00
     543      1550.00
     588       608.00
     589       486.50
     590        31.00
     613      6324.00
     614       733.60
     615      2640.00
     616       798.00
     621       147.00
     622       392.00
     623       312.00
     646       672.00
     647       224.00
     652        72.00
     653       154.00
     654        52.00
     672       228.00
     673       120.00
     674       328.00
     675       712.50
     676       147.90
     684      4456.44
     685       279.00
     742        63.00
     743        20.00
     744       313.20
     792       319.20
     793        98.00
     794       210.00
     823       697.50
     824       322.00
     825        81.00
     826      1060.00
     827      1520.00
     846       624.00
     847        75.00
     848       600.00
     849       112.50
     850       598.50
     858       437.50
     859       540.00
     860       315.00
     861      2280.00
     871        35.00
     872        36.80
     873       493.00
     874       199.50
     882       180.00
     883       155.00
     884       234.00
     887       155.00
     888       162.75
     906        72.00
     907       360.00
     908       780.00
     917       168.00
     918       397.50
     922       190.00
     923      1053.60
     924       232.50
     928      2195.00
     929       193.50
     931        29.80
     932       450.00
     936      1008.00
     937       500.00
     940       523.50
     941      1100.00
     942      2380.00
     943       322.50
     947      1350.00
     948      3900.00
     949        35.00
     950       772.80
     951       417.60
     960      2170.00
     961      1045.00
     962       360.00
     963      1360.00
     964      1440.00
     971      3952.50
     972       532.00
     973       225.00
     974       322.50
     975      1650.00
     976      1750.00
     977       760.00
     978       187.50
     979       420.00
     980       840.00
     981        22.50
     982        35.00
     994       456.00
     995       742.74
     996       194.50
     1003      739.50
     1004      525.00
     1070       69.75
     1071      544.60
     1072       57.00
     1073      775.00
     1074      231.60
     1075      540.00
     1076       95.00
     1077     1710.00
     1078     1020.00
     1086     1701.00
     1089      125.00
     1096     1060.00
     1097       55.00
     1098      180.00
     1129     3800.00
     1130       75.00
     1131     1158.00
     1132      223.50
     1134      872.50
     1135      250.00
     1136      560.00
     1137      276.00
     1138      120.00
     1139      931.00
     1167      582.00
     1168      447.00
     1169     1080.00
     1170      225.00
     1177      780.00
     1178      216.00
     1189       90.00
     1190      168.00
     1191      500.00
     1192     1290.00
     1206      349.00
     1207     1104.00
     1208      440.00
     1212       85.40
     1213       95.00
     1219      110.40
     1220      405.30
     1221     3936.00
     1224      558.00
     1225      936.90
     1226     1045.00
     1227      288.00
     1228      570.00
     1229     1053.00
     1230      475.00
     1231      684.00
     1232      159.00
     1245      750.00
     1246       77.67
     1247      298.00
     1251       57.00
     1252      625.00
     1253      562.50
     1254      325.50
     1255      468.45
     1256      496.00
     1257      142.50
     1285      570.00
     1286       26.00
     1294      228.00
     1295      630.00
     1296      380.00
     1297      532.00
     1299      200.00
     1300     1700.00
     1301     1218.00
     1316      396.00
     1317      736.00
     1318     1064.00
     1338     1312.50
     1339      380.00
     1340       75.00
     1341      720.00
     1342      420.00
     1343      385.00
     1344     1479.00
     1345      798.00
     1353      490.00
     1354      139.50
     1386      186.00
     1387       42.00
     1458      140.00
     1459     2635.00
     1464      760.00
     1465      900.00
     1467       42.00
     1468       70.00
     1469       75.00
     1482       40.00
     1483     7905.00
     1484      986.00
     1493     1140.00
     1494      360.00
     1495      318.00
     1496      147.90
     1497       90.00
     1569     1440.00
     1570      110.40
     1571     1560.00
     1572      342.00
     1573     1530.00
     1574     1182.50
     1586      285.00
     1587      234.00
     1588     2465.00
     1592      872.50
     1593      175.00
     1594      912.00
     1595      315.75
     1609     1638.00
     1610     1250.00
     1611      400.00
     1612       87.50
     1613      147.90
     1625       98.40
     1660      350.00
     1661      400.00
     1662      238.40
     1663       36.00
     1664      400.00
     1665      798.00
     1666      252.60
     1677      840.00
     1678    10540.00
     1689      168.00
     1690     1800.00
     1691      930.00
     1710      198.75
     1711     1725.50
     1740     1080.00
     1741      850.00
     1786      570.00
     1797      550.00
     1798     1479.00
     1799     1000.00
     1800     1740.00
     1805      105.00
     1806      350.10
     1807      684.00
     1817      300.00
     1818      930.00
     1819      234.00
     1820     2958.00
     1857      848.00
     1874      439.00
     1875      640.00
     1876       77.50
     1894      600.00
     1895      414.00
     1896      504.00
     1897      292.50
     1898      959.75
     1899       90.00
     1900      760.00
     1911     1800.00
     1912     1972.00
     1923       69.60
     1940      550.00
     1941      135.00
     1942      390.00
     1947      336.00
     1948      270.00
     1949      336.00
     1950      960.00
     1951       72.00
     1952      184.00
     1953       70.00
     1958      144.00
     1959      247.58
     1988      760.00
     1989      625.00
     1990      190.00
     2011      135.00
     2012     1035.30
     2017     1900.00
     2018     1494.50
     2019     7427.40
     2020     5500.00
     2021      810.00
     2022      480.00
     2023       94.50
     2024      665.00
     2025      344.00
     2026      665.00
     2027     6587.50
     2028     1650.00
     2031      150.00
     2032      233.40
     2033      171.00
     2048      200.00
     2055       37.50
     2056     1272.00
     2062      525.00
     2090      510.00
     2096     3003.00
     2097      115.80
     2098      820.00
     2099       96.00
     2100      687.50
     2103       52.35
     2104      386.40
     2105      490.00
     2130      456.00
     2131       40.00
     2132       22.00
     2133       25.00
     2134       30.00
     2135       80.00
     2136       31.00
     2137       76.00
     2138       24.00
     2139       23.25
     2140       34.90
     2141       81.00
     2142       18.00
     2143       32.00
     2144       36.00
     2145       28.95
     2146       36.00
     2147       14.00
     2148       48.00
     2149       68.00
     2150       66.50
     2151       17.00
     2152       30.00
     2153       31.00
     2154       26.00
     Name: Revenue, dtype: float64, 'Northern Europe': 47        532.00
     48        192.50
     78        248.00
     79        660.00
     80        280.80
     81        300.00
     83         43.20
     84        384.00
     85        186.00
     209       380.00
     210       840.00
     211       724.50
     212       318.00
     249        16.00
     250       396.00
     316       403.20
     317       106.20
     318       252.00
     319        72.80
     343       103.20
     360      1814.40
     361       408.00
     401       600.00
     402       516.00
     403       504.00
     404       145.60
     449     10540.00
     450        19.20
     451       360.00
     452       364.00
     491       100.80
     492       259.20
     518       312.00
     519       373.50
     520       115.20
     521       231.00
     522        86.40
     523        88.50
     564       210.00
     565        24.80
     577        90.00
     578      1782.00
     579       294.00
     580       228.00
     581       325.00
     731        62.00
     732       258.90
     733      2760.00
     734       111.75
     755      1100.00
     756       835.20
     757       360.00
     828       835.20
     840       194.50
     841      2650.00
     864       209.40
     865       320.00
     866       920.00
     867       116.25
     909       140.00
     910       300.00
     911       372.50
     935        65.00
     1000      393.60
     1001      680.00
     1002      430.00
     1037      300.00
     1038      570.00
     1066      264.00
     1067      360.00
     1068       44.70
     1106      570.00
     1115     3952.50
     1116      258.00
     1155      558.00
     1156     2736.00
     1157      196.00
     1158      630.00
     1198       95.00
     1199     1925.00
     1200      525.00
     1279      372.00
     1280      912.00
     1281      175.00
     1303      920.00
     1355      288.00
     1356      285.00
     1357     1484.00
     1358     2280.00
     1373      289.50
     1374      105.00
     1375      570.00
     1376      739.50
     1384       25.00
     1385      850.00
     1393       96.50
     1448      647.25
     1449     1590.00
     1450     1440.00
     1451      246.50
     1502      115.80
     1503      135.00
     1540       36.00
     1541      460.00
     1542      380.00
     1543      378.00
     1598      300.00
     1599     1093.05
     1600     1237.90
     1622      399.00
     1623       27.00
     1624     1035.60
     1645      230.00
     1646      199.50
     1647      300.00
     1656      270.00
     1657      855.00
     1658      750.00
     1705      720.00
     1706      295.80
     1746      180.00
     1747     1756.00
     1753      620.00
     1754     1368.00
     1755       46.50
     1810      775.00
     1811      112.50
     1812      520.00
     1833       93.00
     1878      540.00
     1879      285.00
     1880      530.00
     1881      878.00
     1892      310.00
     1924     6189.50
     1925      337.75
     1926      990.00
     1943     1800.00
     1944      525.00
     1945      300.00
     1946      144.00
     2065      900.00
     2123      244.30
     Name: Revenue, dtype: float64, 'Scandinavia': 51       364.80
     59       456.00
     60       920.00
     190      516.00
     226      186.00
     227       80.00
     228      688.00
     367       54.00
     368      218.40
     369      528.00
     370      258.00
     438      372.00
     446      146.00
     447      262.00
     448      312.00
     500      393.00
     549      288.00
     550     1310.00
     551      570.00
     552      516.00
     718       36.00
     719      164.00
     737      144.00
     738       60.00
     739     1140.00
     814      315.00
     815      244.30
     816      504.00
     817      375.00
     818      108.00
     895     1237.90
     896      816.00
     897      360.00
     970      120.00
     1024     550.00
     1025      79.50
     1032     500.00
     1117      52.35
     1118      84.00
     1119     276.00
     1174     400.00
     1175     152.00
     1176      90.00
     1322     116.25
     1323     380.00
     1324    1375.00
     1398      22.35
     1399     760.00
     1400     350.00
     1520      18.40
     1521     144.00
     1522    2108.00
     1523     414.00
     1642     200.00
     1643     136.80
     1653     220.80
     1654     210.50
     1655     180.00
     1717     360.00
     1718     261.75
     1719      48.25
     1720     110.40
     1721     200.00
     1722     142.50
     1956      36.00
     1957     550.00
     1981     388.35
     1982     234.00
     2007     180.00
     2008     120.00
     Name: Revenue, dtype: float64, 'Southern Europe': 72        43.20
     73       264.00
     86         7.30
     87        21.60
     88        57.60
     89       124.20
     90        31.20
     107       59.00
     108       30.00
     140      408.00
     141      200.00
     147      588.00
     148      504.00
     149      150.00
     156      207.00
     157      262.00
     158       29.50
     206      422.40
     207      249.60
     208      310.00
     213      396.00
     214      672.00
     215      100.00
     235      316.80
     278       36.00
     279      118.00
     314       84.00
     315       52.00
     397       80.00
     398      763.20
     416      747.00
     417      448.00
     418      480.00
     467       49.80
     475      152.00
     476      186.20
     478      192.00
     490      851.20
     516      100.80
     517      436.80
     573      281.60
     574      110.40
     575      912.00
     576      544.00
     584      100.80
     585      134.40
     609      216.00
     610      168.00
     611      288.00
     644      232.50
     645       72.80
     805      312.00
     806       92.00
     807       60.00
     808      285.00
     809      698.00
     810      360.00
     811      778.00
     842       50.00
     843      493.00
     857      155.00
     900       28.00
     938       76.50
     939      180.00
     1006    2475.80
     1007     299.25
     1021     220.00
     1022     320.25
     1023     840.00
     1069     193.00
     1093     744.00
     1094     456.00
     1095     315.75
     1217      46.00
     1218      47.50
     1263     780.00
     1264     380.00
     1265     550.00
     1331      38.00
     1332      50.00
     1333      55.20
     1404     570.00
     1405      36.00
     1406    1044.00
     1446    1560.00
     1447    2475.80
     1463      18.40
     1473     200.00
     1474    1392.00
     1475     260.00
     1489     640.00
     1490     193.00
     1638     240.00
     1639     986.00
     1640     498.75
     1641     442.05
     1644     310.00
     1674      70.00
     1675     380.00
     1676     225.00
     1715     600.00
     1716      98.00
     1723     180.00
     1724     468.00
     1725     210.00
     1738      25.89
     1739     340.00
     1765      47.50
     1766      90.00
     1793     190.00
     1794     560.00
     1801     560.00
     1814     146.25
     1815    2120.00
     1816      96.00
     1821     110.00
     1853      68.00
     1867     280.00
     1960    1200.00
     1961    1237.90
     1962     196.00
     1966      54.00
     1967     342.00
     1968     306.00
     1969     600.00
     1970      45.00
     1976      90.00
     1977      56.00
     1978     190.00
     1979      25.00
     2009     500.00
     2010     530.00
     2040      60.00
     2088     136.00
     2089     130.00
     2091     328.00
     2092     180.00
     Name: Revenue, dtype: float64, 'British Isles': 109      240.00
     110      239.40
     134      608.00
     135      608.00
     136     1320.00
     137      591.00
     163      352.00
     164      600.00
     165       22.40
     166      736.00
     167       51.60
     180      156.80
     181      360.00
     185      154.00
     186       86.40
     191      144.00
     231      106.40
     232      250.00
     233      153.60
     234     2035.20
     284       90.00
     285      390.00
     295      778.40
     296      700.00
     297     2176.00
     311      864.00
     312       86.00
     334      848.00
     335      860.00
     341      728.00
     342      288.00
     347      372.60
     348      524.00
     349      163.20
     350      360.00
     357       96.00
     358      195.00
     359      608.00
     371      114.00
     372      112.00
     373     1048.00
     405     2079.00
     406      504.00
     407      480.00
     479      520.00
     480     1228.50
     493      152.00
     494      201.60
     495      278.00
     544      153.00
     545      300.00
     569        4.80
     570      151.20
     594      720.00
     595      608.00
     596      288.00
     597      763.20
     598       24.00
     599      206.40
     624      112.00
     625      147.00
     626      127.20
     670     1627.50
     671      421.00
     706     1562.50
     707      772.00
     708      280.00
     709       42.00
     710      220.00
     711       90.00
     727      975.00
     728     1215.00
     729      468.00
     730       57.90
     753      388.35
     754      408.00
     774      105.00
     775       34.80
     776       48.00
     777      150.00
     778       37.50
     779      120.00
     798      768.00
     799     1140.00
     831      237.50
     832     1060.00
     833      210.00
     834      590.40
     835       45.00
     854      750.00
     855      159.00
     856     2200.00
     885      360.00
     886      117.00
     930      493.00
     983       46.00
     984       90.00
     985      300.00
     986      322.50
     1047     270.00
     1048     558.00
     1049     645.00
     1050     455.00
     1087      54.00
     1088     649.25
     1120      45.00
     1152    4850.00
     1153    1237.90
     1154     114.00
     1193    2310.00
     1194     430.00
     1195     630.00
     1209     504.00
     1210     780.00
     1211     420.00
     1222      98.40
     1223    1140.00
     1261     550.00
     1262     105.00
     1287     842.00
     1288     155.00
     1298     285.00
     1302     336.00
     1319     570.00
     1320     330.00
     1321     180.00
     1329     144.00
     1330     108.00
     1369      84.00
     1370     625.00
     1371     510.00
     1372     258.00
     1427     135.10
     1428      56.00
     1438      98.60
     1439     348.00
     1443    1050.00
     1444     530.00
     1445      52.15
     1455    1116.00
     1456    1094.40
     1457      80.00
     1512     190.00
     1513     800.00
     1514      60.00
     1515     714.00
     1575     640.50
     1576     291.00
     1618      72.00
     1619     210.00
     1629     720.00
     1630     210.00
     1631     450.00
     1632     250.00
     1698    9903.20
     1699     932.04
     1726     840.00
     1727    7427.40
     1745     390.00
     1780      65.60
     1781     855.00
     1802      90.00
     1803     441.00
     1804     180.00
     1813     220.00
     1827    4050.00
     1828     625.00
     1901     628.20
     1902     500.00
     1903    1120.00
     1908    1800.00
     1909     276.00
     1910     696.00
     1983     187.50
     1984     304.00
     2001     120.00
     2002    1380.00
     2003     374.76
     2004      75.00
     2005     442.05
     2006    1075.00
     2060     450.00
     2061     640.50
     2078    1200.00
     2079     840.00
     2080    1700.00
     2081      45.00
     2093     420.00
     2094     736.00
     2095     289.50
     Name: Revenue, dtype: float64, 'Eastern Europe': 336     300.00
     337     159.00
     957     108.00
     958     190.00
     959     510.00
     1424    190.00
     1425     22.35
     1426    187.50
     1633     54.00
     1634    106.00
     1713    427.50
     1933     54.00
     1934    199.50
     1935    200.00
     1936    232.50
     2054    591.60
     Name: Revenue, dtype: float64}



## Outlier Removal and Normality Testing


```python
clean_data_region = {}
clean_list_region = []
for k, v in data_region.items():
    
    idx_outs = find_outliers_Z(v)
    data_clean = v[~idx_outs].copy()
    clean_list_region.append(data_clean)
    stat, p = stats.shapiro(data_clean)
    print(f"For {k} normal test, p = {round(p, 4)}, n = {len(data_clean)}")
    clean_data_region[k] = data_clean
```

    For Western Europe normal test, p = 0.0, n = 734
    For South America normal test, p = 0.0, n = 353
    For Central America normal test, p = 0.0, n = 71
    For North America normal test, p = 0.0, n = 419
    For Northern Europe normal test, p = 0.0, n = 141
    For Scandinavia normal test, p = 0.0, n = 69
    For Southern Europe normal test, p = 0.0, n = 134
    For British Isles normal test, p = 0.0, n = 186
    For Eastern Europe normal test, p = 0.0386, n = 16


### Our normality test shows that the data is not normally distributed, so we will test for equal variance.

## Equal Variance Test


```python
empty_list_2 = []
for k,v in clean_data_region.items():
    empty_list_2.append(v)
```


```python
stats.levene(*empty_list_2)
```




    LeveneResult(statistic=8.78556378723223, pvalue=6.963976436546475e-12)



### Running this test shows that there is not equal variance, so we will once again have to use the non-parametric version of the ANOVA to test our hypothesis.

## Hypothesis Test: Non-Parametric ANOVA (Alpha = .05)


```python
stats.kruskal(*clean_list_region)
```




    KruskalResult(statistic=85.91867392774088, pvalue=3.12379890853068e-15)



### Based on our p-value, we can confidently reject our null hypothesis and accept our alternative hypothesis, stating that shipping region does have a statistically significant effect on product revenue.

## Tukey's Test


```python
df_reg_tukey = prep_data_for_tukeys(clean_data_region)
```


```python
results = pairwise_tukeyhsd(df_reg_tukey['data'].values, df_reg_tukey['group'].values)
results.summary()
```




<table class="simpletable">
<caption>Multiple Comparison of Means - Tukey HSD, FWER=0.05</caption>
<tr>
      <th>group1</th>          <th>group2</th>      <th>meandiff</th>   <th>p-adj</th>   <th>lower</th>     <th>upper</th>   <th>reject</th>
</tr>
<tr>
   <td>British Isles</td>  <td>Central America</td> <td>-209.6348</td> <td>0.1729</td> <td>-456.654</td>   <td>37.3843</td>   <td>False</td>
</tr>
<tr>
   <td>British Isles</td>  <td>Eastern Europe</td>  <td>-272.2816</td> <td>0.6387</td> <td>-733.6086</td> <td>189.0454</td>   <td>False</td>
</tr>
<tr>
   <td>British Isles</td>   <td>North America</td>  <td>127.0945</td>  <td>0.2184</td> <td>-28.9196</td>  <td>283.1086</td>   <td>False</td>
</tr>
<tr>
   <td>British Isles</td>  <td>Northern Europe</td>  <td>57.1591</td>    <td>0.9</td>  <td>-140.564</td>  <td>254.8822</td>   <td>False</td>
</tr>
<tr>
   <td>British Isles</td>    <td>Scandinavia</td>   <td>-153.8169</td> <td>0.5896</td> <td>-403.4135</td>  <td>95.7797</td>   <td>False</td>
</tr>
<tr>
   <td>British Isles</td>   <td>South America</td>  <td>-40.7325</td>    <td>0.9</td>  <td>-201.1679</td> <td>119.7029</td>   <td>False</td>
</tr>
<tr>
   <td>British Isles</td>  <td>Southern Europe</td> <td>-183.0726</td> <td>0.1065</td> <td>-383.7118</td>  <td>17.5666</td>   <td>False</td>
</tr>
<tr>
   <td>British Isles</td>  <td>Western Europe</td>  <td>133.5464</td>  <td>0.1011</td> <td>-11.8117</td>  <td>278.9044</td>   <td>False</td>
</tr>
<tr>
  <td>Central America</td> <td>Eastern Europe</td>  <td>-62.6468</td>    <td>0.9</td>  <td>-552.6739</td> <td>427.3803</td>   <td>False</td>
</tr>
<tr>
  <td>Central America</td>  <td>North America</td>  <td>336.7293</td>   <td>0.001</td> <td>109.4754</td>  <td>563.9833</td>   <td>True</td> 
</tr>
<tr>
  <td>Central America</td> <td>Northern Europe</td> <td>266.7939</td>  <td>0.0359</td>   <td>9.115</td>   <td>524.4728</td>   <td>True</td> 
</tr>
<tr>
  <td>Central America</td>   <td>Scandinavia</td>    <td>55.8179</td>    <td>0.9</td>  <td>-243.5188</td> <td>355.1546</td>   <td>False</td>
</tr>
<tr>
  <td>Central America</td>  <td>South America</td>  <td>168.9023</td>  <td>0.3575</td> <td>-61.4094</td>   <td>399.214</td>   <td>False</td>
</tr>
<tr>
  <td>Central America</td> <td>Southern Europe</td>  <td>26.5622</td>    <td>0.9</td>  <td>-233.3609</td> <td>286.4854</td>   <td>False</td>
</tr>
<tr>
  <td>Central America</td> <td>Western Europe</td>  <td>343.1812</td>   <td>0.001</td> <td>123.1064</td>  <td>563.2561</td>   <td>True</td> 
</tr>
<tr>
  <td>Eastern Europe</td>   <td>North America</td>  <td>399.3761</td>  <td>0.1311</td> <td>-51.6766</td>  <td>850.4288</td>   <td>False</td>
</tr>
<tr>
  <td>Eastern Europe</td>  <td>Northern Europe</td> <td>329.4407</td>  <td>0.4155</td> <td>-137.6809</td> <td>796.5623</td>   <td>False</td>
</tr>
<tr>
  <td>Eastern Europe</td>    <td>Scandinavia</td>   <td>118.4647</td>    <td>0.9</td>  <td>-372.8667</td> <td>609.7962</td>   <td>False</td>
</tr>
<tr>
  <td>Eastern Europe</td>   <td>South America</td>  <td>231.5491</td>  <td>0.7866</td> <td>-221.0519</td> <td>684.1501</td>   <td>False</td>
</tr>
<tr>
  <td>Eastern Europe</td>  <td>Southern Europe</td>  <td>89.209</td>     <td>0.9</td>  <td>-379.1543</td> <td>557.5724</td>   <td>False</td>
</tr>
<tr>
  <td>Eastern Europe</td>  <td>Western Europe</td>   <td>405.828</td>  <td>0.1114</td> <td>-41.6506</td>  <td>853.3066</td>   <td>False</td>
</tr>
<tr>
   <td>North America</td>  <td>Northern Europe</td> <td>-69.9354</td>    <td>0.9</td>  <td>-242.3314</td> <td>102.4605</td>   <td>False</td>
</tr>
<tr>
   <td>North America</td>    <td>Scandinavia</td>   <td>-280.9114</td> <td>0.0048</td> <td>-510.9645</td> <td>-50.8584</td>   <td>True</td> 
</tr>
<tr>
   <td>North America</td>   <td>South America</td>  <td>-167.8271</td> <td>0.0016</td> <td>-295.7546</td> <td>-39.8995</td>   <td>True</td> 
</tr>
<tr>
   <td>North America</td>  <td>Southern Europe</td> <td>-310.1671</td>  <td>0.001</td> <td>-485.8999</td> <td>-134.4343</td>  <td>True</td> 
</tr>
<tr>
   <td>North America</td>  <td>Western Europe</td>   <td>6.4519</td>     <td>0.9</td>  <td>-101.9681</td> <td>114.8718</td>   <td>False</td>
</tr>
<tr>
  <td>Northern Europe</td>   <td>Scandinavia</td>   <td>-210.976</td>  <td>0.2238</td> <td>-471.1268</td>  <td>49.1748</td>   <td>False</td>
</tr>
<tr>
  <td>Northern Europe</td>  <td>South America</td>  <td>-97.8916</td>  <td>0.7051</td> <td>-274.2988</td>  <td>78.5155</td>   <td>False</td>
</tr>
<tr>
  <td>Northern Europe</td> <td>Southern Europe</td> <td>-240.2317</td> <td>0.0144</td> <td>-453.8577</td> <td>-26.6057</td>   <td>True</td> 
</tr>
<tr>
  <td>Northern Europe</td> <td>Western Europe</td>   <td>76.3873</td>  <td>0.8664</td> <td>-86.4283</td>  <td>239.2029</td>   <td>False</td>
</tr>
<tr>
    <td>Scandinavia</td>    <td>South America</td>  <td>113.0844</td>  <td>0.8363</td> <td>-119.9897</td> <td>346.1584</td>   <td>False</td>
</tr>
<tr>
    <td>Scandinavia</td>   <td>Southern Europe</td> <td>-29.2557</td>    <td>0.9</td>  <td>-291.6297</td> <td>233.1183</td>   <td>False</td>
</tr>
<tr>
    <td>Scandinavia</td>   <td>Western Europe</td>  <td>287.3633</td>  <td>0.0021</td>  <td>64.3992</td>  <td>510.3273</td>   <td>True</td> 
</tr>
<tr>
   <td>South America</td>  <td>Southern Europe</td> <td>-142.3401</td> <td>0.2523</td> <td>-322.0096</td>  <td>37.3295</td>   <td>False</td>
</tr>
<tr>
   <td>South America</td>  <td>Western Europe</td>  <td>174.2789</td>   <td>0.001</td>  <td>59.588</td>   <td>288.9699</td>   <td>True</td> 
</tr>
<tr>
  <td>Southern Europe</td> <td>Western Europe</td>   <td>316.619</td>   <td>0.001</td> <td>150.2742</td>  <td>482.9637</td>   <td>True</td> 
</tr>
</table>




```python
cool_df = pd.DataFrame(data=results._results_table.data[1:], columns=results._results_table.data[0])
pd.set_option('display.max_rows', 999)
cool_df.loc[cool_df['reject'] == True]
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
      <th>group1</th>
      <th>group2</th>
      <th>meandiff</th>
      <th>p-adj</th>
      <th>lower</th>
      <th>upper</th>
      <th>reject</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>9</td>
      <td>Central America</td>
      <td>North America</td>
      <td>336.7293</td>
      <td>0.0010</td>
      <td>109.4754</td>
      <td>563.9833</td>
      <td>True</td>
    </tr>
    <tr>
      <td>10</td>
      <td>Central America</td>
      <td>Northern Europe</td>
      <td>266.7939</td>
      <td>0.0359</td>
      <td>9.1150</td>
      <td>524.4728</td>
      <td>True</td>
    </tr>
    <tr>
      <td>14</td>
      <td>Central America</td>
      <td>Western Europe</td>
      <td>343.1812</td>
      <td>0.0010</td>
      <td>123.1064</td>
      <td>563.2561</td>
      <td>True</td>
    </tr>
    <tr>
      <td>22</td>
      <td>North America</td>
      <td>Scandinavia</td>
      <td>-280.9114</td>
      <td>0.0048</td>
      <td>-510.9645</td>
      <td>-50.8584</td>
      <td>True</td>
    </tr>
    <tr>
      <td>23</td>
      <td>North America</td>
      <td>South America</td>
      <td>-167.8271</td>
      <td>0.0016</td>
      <td>-295.7546</td>
      <td>-39.8995</td>
      <td>True</td>
    </tr>
    <tr>
      <td>24</td>
      <td>North America</td>
      <td>Southern Europe</td>
      <td>-310.1671</td>
      <td>0.0010</td>
      <td>-485.8999</td>
      <td>-134.4343</td>
      <td>True</td>
    </tr>
    <tr>
      <td>28</td>
      <td>Northern Europe</td>
      <td>Southern Europe</td>
      <td>-240.2317</td>
      <td>0.0144</td>
      <td>-453.8577</td>
      <td>-26.6057</td>
      <td>True</td>
    </tr>
    <tr>
      <td>32</td>
      <td>Scandinavia</td>
      <td>Western Europe</td>
      <td>287.3633</td>
      <td>0.0021</td>
      <td>64.3992</td>
      <td>510.3273</td>
      <td>True</td>
    </tr>
    <tr>
      <td>34</td>
      <td>South America</td>
      <td>Western Europe</td>
      <td>174.2789</td>
      <td>0.0010</td>
      <td>59.5880</td>
      <td>288.9699</td>
      <td>True</td>
    </tr>
    <tr>
      <td>35</td>
      <td>Southern Europe</td>
      <td>Western Europe</td>
      <td>316.6190</td>
      <td>0.0010</td>
      <td>150.2742</td>
      <td>482.9637</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



### Our Tukey's Test shows that there are some strong effects on product revenue when comparing regions against each other, particularly in the following cases:

### - Central America & North America
### - Central America & Western Europe
### - North America & Southern Europe
### - South America & Western Europe
### - Southern Europe & Western Europe


```python
fig, ax = plt.subplots(figsize=(7,4))
sns.barplot(data=df_reg_tukey, x='group', y='data', ci=68, ax=ax)
ax.grid()
ax.set_xticklabels(ax.get_xticklabels(), rotation=45, ha='right')
ax.set(xlabel='Shipping Region', ylabel='Revenue')
```




    [Text(0, 0.5, 'Revenue'), Text(0.5, 0, 'Shipping Region')]




![png](output_108_1.png)


### Recommendation: I have two recommendations. First, I would halt shipping products out of Eastern Europe. That region is significantly underperforming. I would consider taking the products & resources there and consolidating them with another region (perhaps Southern Europe) so that we can make shipping more efficient.

### On the flipside, I believe we should invest more into shipping out of Western Europe & North America because they are the two clear-cut performers when it comes to shipping. If the budget allows, we should also consider investing more into Northern Europe as well to see if we can have a bump in performance.

# Conclusion

### Our mission for Northwind was to come up with 4 business oriented hypotheses in the attempt to test them, achieve statistically significant results, and then make recommendation how to apply our findings to improve the company's performance. Thankfully, we were able generate significant results with each test, and make the following recommendations:

### - Remove the use of 25% discounts on all products
### - Invest into the Western Europe, North American, and Northern Europe shipping regions to further increase sales and profits
### - Heavily market product 38 using discounts
### - Stop shipping products out of Eastern Europe
