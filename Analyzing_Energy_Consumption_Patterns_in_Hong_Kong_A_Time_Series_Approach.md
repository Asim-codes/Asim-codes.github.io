---
jupyter:
  colab:
  kernelspec:
    display_name: Python 3
    name: python3
  language_info:
    name: python
  nbformat: 4
  nbformat_minor: 0
---

**Overview \[Key Energy End-use\]**


::: {.cell .code execution_count="41" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="-N2YCKy8Uu2P" outputId="6a8b775b-012b-4fc2-e410-9f72d07142c1"}

``` python
import requests
import pandas as pd
import io
import numpy as np

# Send a GET request to the API endpoint
response = requests.get('https://api.data.gov.hk/v1/historical-archive/get-file?url=https%3A%2F%2Fwww.emsd.gov.hk%2Ffilemanager%2Fen%2Fshare%2Fenergy_efficiency%2Fenergy_end_use%2F2022%2Ftable01.csv&time=20221019-1038')

# Check if the request was successful
if response.status_code == 200:
    #convert it into a file-like object
    data_io = io.StringIO(response.text)

    df_overview = pd.read_csv(data_io)
    print('Data read successfully.')
else:
    print(f'Request failed with status code {response.status_code}')
```

::: {.output .stream .stdout}
    Data read successfully.
:::
:::

::: {.cell .code execution_count="2" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":446}" id="Oe9JaKtwWizA" outputId="b916c012-3f08-4456-949e-614fe8ec498d"}
``` python
df_overview
```

```{=html}
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
      <th>Year</th>
      <th>Energy End-use (TJ)/ GDP (HK$ billion)</th>
      <th>Energy End-use (TJ)</th>
      <th>GDP in Hong Kong in chained 2020 HKD (HK$ million)</th>
      <th>Energy End-use/ Capita (GJ)</th>
      <th>Electricity/ Capita (GJ)</th>
      <th>Population ('000)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2010</td>
      <td>122</td>
      <td>281729</td>
      <td>2308742</td>
      <td>40.11</td>
      <td>21.48</td>
      <td>7024</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2011</td>
      <td>116</td>
      <td>279524</td>
      <td>2419901</td>
      <td>39.53</td>
      <td>21.44</td>
      <td>7072</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2012</td>
      <td>115</td>
      <td>282055</td>
      <td>2461047</td>
      <td>39.45</td>
      <td>21.69</td>
      <td>7150</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2013</td>
      <td>110</td>
      <td>279588</td>
      <td>2537377</td>
      <td>38.95</td>
      <td>21.36</td>
      <td>7179</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2014</td>
      <td>109</td>
      <td>283984</td>
      <td>2607470</td>
      <td>39.28</td>
      <td>21.88</td>
      <td>7230</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2015</td>
      <td>106</td>
      <td>282960</td>
      <td>2669732</td>
      <td>38.81</td>
      <td>21.72</td>
      <td>7291</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2016</td>
      <td>104</td>
      <td>283564</td>
      <td>2727810</td>
      <td>38.65</td>
      <td>21.65</td>
      <td>7337</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2017</td>
      <td>99</td>
      <td>281006</td>
      <td>2831361</td>
      <td>38.01</td>
      <td>21.37</td>
      <td>7393</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2018</td>
      <td>97</td>
      <td>282486</td>
      <td>2911968</td>
      <td>37.90</td>
      <td>21.40</td>
      <td>7453</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2019</td>
      <td>99</td>
      <td>283527</td>
      <td>2863098</td>
      <td>37.76</td>
      <td>21.53</td>
      <td>7508</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2020</td>
      <td>102</td>
      <td>272490</td>
      <td>2675708</td>
      <td>36.42</td>
      <td>21.27</td>
      <td>7481</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {.cell .markdown id="DLTM6Cita8LO"}
**Total Energy Consumption by fuel**
:::

::: {.cell .code execution_count="3" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="deg27nosXXq4" outputId="c623edd7-cad5-4ac3-c97f-a3980314e25b"}
``` python
# Send a GET request to the API endpoint
response = requests.get('https://api.data.gov.hk/v1/historical-archive/get-file?url=https%3A%2F%2Fwww.emsd.gov.hk%2Ffilemanager%2Fen%2Fshare%2Fenergy_efficiency%2Fenergy_end_use%2F2022%2Ftable02.csv&time=20231007-1113')
# Check if the request was successful
if response.status_code == 200:
    #convert it into a file-like object
    data_io = io.StringIO(response.text)

    df_total_fuel = pd.read_csv(data_io)
    print('Data read successfully.')
else:
    print(f'Request failed with status code {response.status_code}')
```

::: {.output .stream .stdout}
    Data read successfully.
:::
:::

::: {.cell .code execution_count="4" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":464}" id="7iv8_nTgXffA" outputId="77e01185-3829-4868-945e-9c3a3765d770"}
``` python
df_total_fuel
```

::: {.output .execute_result execution_count="4"}
```{=html}
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
      <th>Year</th>
      <th>Town Gas &amp; Liquefied Petroleum Gas (Unit : Terajoule)</th>
      <th>Town Gas &amp; Liquefied Petroleum Gas Percentage (%)</th>
      <th>Oil &amp; Coal Products (Unit : Terajoule)</th>
      <th>Oil &amp; Coal Products Percentage (%)</th>
      <th>Electricity (Unit : Terajoule)</th>
      <th>Electricity Percentage (%)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2010</td>
      <td>49084</td>
      <td>17</td>
      <td>81786</td>
      <td>29</td>
      <td>150859</td>
      <td>54</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2011</td>
      <td>49568</td>
      <td>18</td>
      <td>78349</td>
      <td>28</td>
      <td>151606</td>
      <td>54</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2012</td>
      <td>49616</td>
      <td>18</td>
      <td>77359</td>
      <td>27</td>
      <td>155080</td>
      <td>55</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2013</td>
      <td>49723</td>
      <td>18</td>
      <td>76503</td>
      <td>27</td>
      <td>153362</td>
      <td>55</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2014</td>
      <td>50844</td>
      <td>18</td>
      <td>74992</td>
      <td>26</td>
      <td>158148</td>
      <td>56</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2015</td>
      <td>48954</td>
      <td>17</td>
      <td>75626</td>
      <td>27</td>
      <td>158380</td>
      <td>56</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2016</td>
      <td>49374</td>
      <td>17</td>
      <td>75349</td>
      <td>27</td>
      <td>158841</td>
      <td>56</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2017</td>
      <td>47907</td>
      <td>17</td>
      <td>75121</td>
      <td>27</td>
      <td>157977</td>
      <td>56</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2018</td>
      <td>48541</td>
      <td>17</td>
      <td>74452</td>
      <td>26</td>
      <td>159494</td>
      <td>56</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2019</td>
      <td>47338</td>
      <td>17</td>
      <td>74520</td>
      <td>26</td>
      <td>161669</td>
      <td>57</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2020</td>
      <td>44195</td>
      <td>16</td>
      <td>69195</td>
      <td>25</td>
      <td>159100</td>
      <td>58</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {.cell .markdown id="zk9r4KhSbDD_"}
**Energy Consumption in Residential Sector by Fuel**
:::

::: {.cell .code execution_count="5" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="cFwJ5b1xXyXw" outputId="301d5f8c-c4a8-4cce-b4e1-14e3b129d9a9"}
``` python
# Send a GET request to the API endpoint
response = requests.get('https://api.data.gov.hk/v1/historical-archive/get-file?url=https%3A%2F%2Fwww.emsd.gov.hk%2Ffilemanager%2Fen%2Fshare%2Fenergy_efficiency%2Fenergy_end_use%2F2022%2Ftable03.csv&time=20231007-1112')
# Check if the request was successful
if response.status_code == 200:
    #convert it into a file-like object
    data_io = io.StringIO(response.text)

    df_residential_fuel = pd.read_csv(data_io)
    print('Data read successfully.')
else:
    print(f'Request failed with status code {response.status_code}')
```

::: {.output .stream .stdout}
    Data read successfully.
:::
:::

::: {.cell .code execution_count="6" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":464}" id="yEgoGVWuY1-j" outputId="840cb113-c606-4089-864e-193fd35a57c7"}
``` python
df_residential_fuel
```

::: {.output .execute_result execution_count="6"}
```{=html}
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
      <th>Year</th>
      <th>Town Gas &amp; Liquefied Petroleum Gas (Unit : Terajoule)</th>
      <th>Town Gas &amp; Liquefied Petroleum Gas Percentage (%)</th>
      <th>Oil &amp; Coal Products (Unit : Terajoule)</th>
      <th>Oil &amp; Coal Products Percentage (%)</th>
      <th>Electricity (Unit : Terajoule)</th>
      <th>Electricity Percentage (%)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2010</td>
      <td>19038</td>
      <td>33</td>
      <td>13</td>
      <td>0</td>
      <td>39344</td>
      <td>67</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2011</td>
      <td>18977</td>
      <td>32</td>
      <td>8</td>
      <td>0</td>
      <td>39872</td>
      <td>68</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2012</td>
      <td>18841</td>
      <td>31</td>
      <td>8</td>
      <td>0</td>
      <td>41189</td>
      <td>69</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2013</td>
      <td>18635</td>
      <td>32</td>
      <td>7</td>
      <td>0</td>
      <td>39941</td>
      <td>68</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2014</td>
      <td>18681</td>
      <td>30</td>
      <td>7</td>
      <td>0</td>
      <td>43415</td>
      <td>70</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2015</td>
      <td>18063</td>
      <td>30</td>
      <td>8</td>
      <td>0</td>
      <td>42368</td>
      <td>70</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2016</td>
      <td>18574</td>
      <td>30</td>
      <td>10</td>
      <td>0</td>
      <td>43120</td>
      <td>70</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2017</td>
      <td>18335</td>
      <td>30</td>
      <td>14</td>
      <td>0</td>
      <td>42127</td>
      <td>70</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2018</td>
      <td>19578</td>
      <td>32</td>
      <td>14</td>
      <td>0</td>
      <td>41965</td>
      <td>68</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2019</td>
      <td>18070</td>
      <td>30</td>
      <td>15</td>
      <td>0</td>
      <td>42937</td>
      <td>70</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2020</td>
      <td>19726</td>
      <td>30</td>
      <td>15</td>
      <td>0</td>
      <td>46675</td>
      <td>70</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {.cell .markdown id="pmfnzkJ0bRU-"}
**Energy Consumption in Commercial Sector by Fuel**
:::

::: {.cell .code execution_count="7" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="k8G4qW9jbJv5" outputId="ca250cfa-d143-488c-e0e2-21787b9520bd"}
``` python
# Send a GET request to the API endpoint
response = requests.get('https://api.data.gov.hk/v1/historical-archive/get-file?url=https%3A%2F%2Fwww.emsd.gov.hk%2Ffilemanager%2Fen%2Fshare%2Fenergy_efficiency%2Fenergy_end_use%2F2022%2Ftable04.csv&time=20231007-1113')
# Check if the request was successful
if response.status_code == 200:
    #convert it into a file-like object
    data_io = io.StringIO(response.text)

    df_commercial_fuel = pd.read_csv(data_io)
    print('Data read successfully.')
else:
    print(f'Request failed with status code {response.status_code}')
```

::: {.output .stream .stdout}
    Data read successfully.
:::
:::

::: {.cell .code execution_count="8" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":464}" id="qhMGEywdbig-" outputId="613bd796-2182-45e1-d34f-5711a15861de"}
``` python
df_commercial_fuel
```

::: {.output .execute_result execution_count="8"}
```{=html}
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
      <th>Year</th>
      <th>Town Gas &amp; Liquefied Petroleum Gas (Unit : Terajoule)</th>
      <th>Town Gas &amp; Liquefied Petroleum Gas Percentage (%)</th>
      <th>Oil &amp; Coal Products (Unit : Terajoule)</th>
      <th>Oil &amp; Coal Products Percentage (%)</th>
      <th>Electricity (Unit : Terajoule)</th>
      <th>Electricity Percentage (%)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2010</td>
      <td>13971</td>
      <td>12</td>
      <td>4526</td>
      <td>4</td>
      <td>97894</td>
      <td>84</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2011</td>
      <td>14129</td>
      <td>12</td>
      <td>1979</td>
      <td>2</td>
      <td>99905</td>
      <td>86</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2012</td>
      <td>14280</td>
      <td>12</td>
      <td>1696</td>
      <td>1</td>
      <td>102353</td>
      <td>86</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2013</td>
      <td>14512</td>
      <td>12</td>
      <td>1477</td>
      <td>1</td>
      <td>102221</td>
      <td>86</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2014</td>
      <td>14713</td>
      <td>12</td>
      <td>1431</td>
      <td>1</td>
      <td>103473</td>
      <td>87</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2015</td>
      <td>14535</td>
      <td>12</td>
      <td>1235</td>
      <td>1</td>
      <td>104649</td>
      <td>87</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2016</td>
      <td>14601</td>
      <td>12</td>
      <td>1019</td>
      <td>1</td>
      <td>104841</td>
      <td>87</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2017</td>
      <td>14908</td>
      <td>12</td>
      <td>830</td>
      <td>1</td>
      <td>104672</td>
      <td>87</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2018</td>
      <td>15253</td>
      <td>12</td>
      <td>675</td>
      <td>1</td>
      <td>106294</td>
      <td>87</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2019</td>
      <td>14440</td>
      <td>12</td>
      <td>574</td>
      <td>0</td>
      <td>107992</td>
      <td>88</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2020</td>
      <td>11844</td>
      <td>10</td>
      <td>498</td>
      <td>0</td>
      <td>102171</td>
      <td>89</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {.cell .markdown id="Cq7CNZgjbnz-"}
**Energy Consumption in Industrial Sector by Fuel**
:::

::: {.cell .code execution_count="9" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="RL39OsFpbu_l" outputId="7ce52e24-58d2-45cc-dbed-10654df9cd17"}
``` python
# Send a GET request to the API endpoint
response = requests.get('https://api.data.gov.hk/v1/historical-archive/get-file?url=https%3A%2F%2Fwww.emsd.gov.hk%2Ffilemanager%2Fen%2Fshare%2Fenergy_efficiency%2Fenergy_end_use%2F2022%2Ftable05.csv&time=20231007-1113')
# Check if the request was successful
if response.status_code == 200:
    #convert it into a file-like object
    data_io = io.StringIO(response.text)

    df_industrial_fuel = pd.read_csv(data_io)
    print('Data read successfully.')
else:
    print(f'Request failed with status code {response.status_code}')
```

::: {.output .stream .stdout}
    Data read successfully.
:::
:::

::: {.cell .code execution_count="10" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":464}" id="WHp0AVOgb9M4" outputId="030f8864-87f4-4f6d-fb3c-d83760122be6"}
``` python
df_industrial_fuel
```

::: {.output .execute_result execution_count="10"}
```{=html}
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
      <th>Year</th>
      <th>Town Gas &amp; Liquefied Petroleum Gas (Unit : Terajoule)</th>
      <th>Town Gas &amp; Liquefied Petroleum Gas Percentage (%)</th>
      <th>Oil &amp; Coal Products (Unit : Terajoule)</th>
      <th>Oil &amp; Coal Products Percentage (%)</th>
      <th>Electricity (Unit : Terajoule)</th>
      <th>Electricity Percentage (%)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2010</td>
      <td>937</td>
      <td>6</td>
      <td>4035</td>
      <td>25</td>
      <td>11082</td>
      <td>69</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2011</td>
      <td>956</td>
      <td>7</td>
      <td>3978</td>
      <td>28</td>
      <td>9220</td>
      <td>65</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2012</td>
      <td>1111</td>
      <td>8</td>
      <td>3728</td>
      <td>27</td>
      <td>8816</td>
      <td>65</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2013</td>
      <td>1229</td>
      <td>9</td>
      <td>3571</td>
      <td>27</td>
      <td>8405</td>
      <td>64</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2014</td>
      <td>1264</td>
      <td>10</td>
      <td>3389</td>
      <td>26</td>
      <td>8374</td>
      <td>64</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2015</td>
      <td>1308</td>
      <td>10</td>
      <td>3386</td>
      <td>26</td>
      <td>8359</td>
      <td>64</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2016</td>
      <td>1232</td>
      <td>10</td>
      <td>3190</td>
      <td>26</td>
      <td>7872</td>
      <td>64</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2017</td>
      <td>1317</td>
      <td>10</td>
      <td>3442</td>
      <td>27</td>
      <td>7963</td>
      <td>63</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2018</td>
      <td>1448</td>
      <td>11</td>
      <td>3443</td>
      <td>27</td>
      <td>7938</td>
      <td>62</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2019</td>
      <td>1596</td>
      <td>13</td>
      <td>3177</td>
      <td>26</td>
      <td>7501</td>
      <td>61</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2020</td>
      <td>1470</td>
      <td>12</td>
      <td>3309</td>
      <td>27</td>
      <td>7383</td>
      <td>61</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {.cell .markdown id="HwTqMq5AcD3_"}
**Energy Consumption in Transport Sector by Fuel**
:::

::: {.cell .code execution_count="11" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="IcnePoL8cQ3d" outputId="158315b6-3061-4ddf-dc3d-d76cecabf43f"}
``` python
# Send a GET request to the API endpoint
response = requests.get('https://api.data.gov.hk/v1/historical-archive/get-file?url=https%3A%2F%2Fwww.emsd.gov.hk%2Ffilemanager%2Fen%2Fshare%2Fenergy_efficiency%2Fenergy_end_use%2F2022%2Ftable06.csv&time=20231007-1118')
# Check if the request was successful
if response.status_code == 200:
    #convert it into a file-like object
    data_io = io.StringIO(response.text)

    df_transport_fuel = pd.read_csv(data_io)
    print('Data read successfully.')
else:
    print(f'Request failed with status code {response.status_code}')
```

::: {.output .stream .stdout}
    Data read successfully.
:::
:::

::: {.cell .code execution_count="12" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":464}" id="jZ5QoWgactxu" outputId="a5ba9727-efb1-4f32-c574-9514d196d345"}
``` python
df_transport_fuel
```

::: {.output .execute_result execution_count="12"}
```{=html}
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
      <th>Year</th>
      <th>Town Gas &amp; Liquefied Petroleum Gas (Unit : Terajoule)</th>
      <th>Town Gas &amp; Liquefied Petroleum Gas Percentage (%)</th>
      <th>Oil &amp; Coal Products (Unit : Terajoule)</th>
      <th>Oil &amp; Coal Products Percentage (%)</th>
      <th>Electricity (Unit : Terajoule)</th>
      <th>Electricity Percentage (%)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2010</td>
      <td>15137</td>
      <td>17</td>
      <td>73213</td>
      <td>81</td>
      <td>2540</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2011</td>
      <td>15506</td>
      <td>17</td>
      <td>72383</td>
      <td>80</td>
      <td>2609</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2012</td>
      <td>15384</td>
      <td>17</td>
      <td>71927</td>
      <td>80</td>
      <td>2722</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2013</td>
      <td>15348</td>
      <td>17</td>
      <td>71449</td>
      <td>80</td>
      <td>2796</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2014</td>
      <td>16185</td>
      <td>18</td>
      <td>70165</td>
      <td>79</td>
      <td>2886</td>
      <td>3</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2015</td>
      <td>15048</td>
      <td>17</td>
      <td>70997</td>
      <td>80</td>
      <td>3004</td>
      <td>3</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2016</td>
      <td>14967</td>
      <td>17</td>
      <td>71130</td>
      <td>80</td>
      <td>3008</td>
      <td>3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2017</td>
      <td>13347</td>
      <td>15</td>
      <td>70835</td>
      <td>81</td>
      <td>3215</td>
      <td>4</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2018</td>
      <td>12262</td>
      <td>14</td>
      <td>70320</td>
      <td>82</td>
      <td>3297</td>
      <td>4</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2019</td>
      <td>13232</td>
      <td>15</td>
      <td>70754</td>
      <td>81</td>
      <td>3239</td>
      <td>4</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2020</td>
      <td>11155</td>
      <td>14</td>
      <td>65373</td>
      <td>82</td>
      <td>2871</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {.cell .markdown id="pq7W7ohac05j"}
**Total Energy Consumption by Sector**
:::

::: {.cell .code execution_count="13" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="MOX3BsL8c8V9" outputId="b9fb12ee-fec1-4886-b4f7-196acec67031"}
``` python
# Send a GET request to the API endpoint
response = requests.get('https://api.data.gov.hk/v1/historical-archive/get-file?url=https%3A%2F%2Fwww.emsd.gov.hk%2Ffilemanager%2Fen%2Fshare%2Fenergy_efficiency%2Fenergy_end_use%2F2022%2Ftable07.csv&time=20231007-1110')
# Check if the request was successful
if response.status_code == 200:
    #convert it into a file-like object
    data_io = io.StringIO(response.text)

    df_energy_sector = pd.read_csv(data_io)
    print('Data read successfully.')
else:
    print(f'Request failed with status code {response.status_code}')
```

::: {.output .stream .stdout}
    Data read successfully.
:::
:::

::: {.cell .code execution_count="14" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":449}" id="oHku9q38dfnJ" outputId="d9fee852-9e94-401a-9772-a1db11fa4730"}
``` python
df_energy_sector
```

::: {.output .execute_result execution_count="14"}
```{=html}
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
      <th>Year</th>
      <th>Residential (Unit : Terajoule)</th>
      <th>Residential Percentage (%)</th>
      <th>Commercial (Unit : Terajoule)</th>
      <th>Commercial Percentage (%)</th>
      <th>Industrial (Unit : Terajoule)</th>
      <th>Industrial Percentage (%)</th>
      <th>Transport (Unit : Terajoule)</th>
      <th>Transport Percentage (%)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2010</td>
      <td>58396</td>
      <td>21</td>
      <td>116391</td>
      <td>41</td>
      <td>16053</td>
      <td>6</td>
      <td>90889</td>
      <td>32</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2011</td>
      <td>58857</td>
      <td>21</td>
      <td>116013</td>
      <td>42</td>
      <td>14155</td>
      <td>5</td>
      <td>90498</td>
      <td>32</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2012</td>
      <td>60037</td>
      <td>21</td>
      <td>118330</td>
      <td>42</td>
      <td>13655</td>
      <td>5</td>
      <td>90033</td>
      <td>32</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2013</td>
      <td>58582</td>
      <td>21</td>
      <td>118209</td>
      <td>42</td>
      <td>13204</td>
      <td>5</td>
      <td>89593</td>
      <td>32</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2014</td>
      <td>62103</td>
      <td>22</td>
      <td>119617</td>
      <td>42</td>
      <td>13028</td>
      <td>5</td>
      <td>89236</td>
      <td>31</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2015</td>
      <td>60439</td>
      <td>21</td>
      <td>120419</td>
      <td>43</td>
      <td>13054</td>
      <td>5</td>
      <td>89049</td>
      <td>31</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2016</td>
      <td>61704</td>
      <td>22</td>
      <td>120460</td>
      <td>42</td>
      <td>12294</td>
      <td>4</td>
      <td>89105</td>
      <td>31</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2017</td>
      <td>60476</td>
      <td>22</td>
      <td>120410</td>
      <td>43</td>
      <td>12722</td>
      <td>5</td>
      <td>87397</td>
      <td>31</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2018</td>
      <td>61557</td>
      <td>22</td>
      <td>122222</td>
      <td>43</td>
      <td>12829</td>
      <td>5</td>
      <td>85878</td>
      <td>30</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2019</td>
      <td>61022</td>
      <td>22</td>
      <td>123005</td>
      <td>43</td>
      <td>12274</td>
      <td>4</td>
      <td>87225</td>
      <td>31</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2020</td>
      <td>66416</td>
      <td>24</td>
      <td>114513</td>
      <td>42</td>
      <td>12162</td>
      <td>4</td>
      <td>79399</td>
      <td>29</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {.cell .markdown id="6ihcYJ8meIEf"}
**Electricity Consumption by Sector**
:::

::: {.cell .code execution_count="15" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="SpHbF6HXeHxA" outputId="68f8acb0-20fd-4074-be92-695b0e24bdd3"}
``` python
# Send a GET request to the API endpoint
response = requests.get('https://www.emsd.gov.hk/filemanager/en/share/energy_efficiency/energy_end_use/2022/table08.csv')
# Check if the request was successful
if response.status_code == 200:
    #convert it into a file-like object
    data_io = io.StringIO(response.text)

    df_electricity_sector = pd.read_csv(data_io)
    print('Data read successfully.')
else:
    print(f'Request failed with status code {response.status_code}')
```

::: {.output .stream .stdout}
    Data read successfully.
:::
:::

::: {.cell .code execution_count="16" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":449}" id="AX3KoCIpeW_f" outputId="12280e7c-7328-4d9c-d0c9-020bb8b14361"}
``` python
df_electricity_sector
```

::: {.output .execute_result execution_count="16"}
```{=html}
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
      <th>Year</th>
      <th>Residential (Unit : Terajoule)</th>
      <th>Residential Percentage (%)</th>
      <th>Commercial (Unit : Terajoule)</th>
      <th>Commercial Percentage (%)</th>
      <th>Industrial (Unit : Terajoule)</th>
      <th>Industrial Percentage (%)</th>
      <th>Transport (Unit : Terajoule)</th>
      <th>Transport Percentage (%)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2010</td>
      <td>39344</td>
      <td>26</td>
      <td>97894</td>
      <td>65</td>
      <td>11082</td>
      <td>7</td>
      <td>2540</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2011</td>
      <td>39872</td>
      <td>26</td>
      <td>99905</td>
      <td>66</td>
      <td>9220</td>
      <td>6</td>
      <td>2609</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2012</td>
      <td>41189</td>
      <td>27</td>
      <td>102353</td>
      <td>66</td>
      <td>8816</td>
      <td>6</td>
      <td>2722</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2013</td>
      <td>39941</td>
      <td>26</td>
      <td>102221</td>
      <td>67</td>
      <td>8405</td>
      <td>5</td>
      <td>2796</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2014</td>
      <td>43415</td>
      <td>27</td>
      <td>103473</td>
      <td>65</td>
      <td>8374</td>
      <td>5</td>
      <td>2886</td>
      <td>2</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2015</td>
      <td>42368</td>
      <td>27</td>
      <td>104649</td>
      <td>66</td>
      <td>8359</td>
      <td>5</td>
      <td>3004</td>
      <td>2</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2016</td>
      <td>43120</td>
      <td>27</td>
      <td>104841</td>
      <td>66</td>
      <td>7872</td>
      <td>5</td>
      <td>3008</td>
      <td>2</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2017</td>
      <td>42127</td>
      <td>27</td>
      <td>104672</td>
      <td>66</td>
      <td>7963</td>
      <td>5</td>
      <td>3215</td>
      <td>2</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2018</td>
      <td>41965</td>
      <td>26</td>
      <td>106294</td>
      <td>67</td>
      <td>7938</td>
      <td>5</td>
      <td>3297</td>
      <td>2</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2019</td>
      <td>42937</td>
      <td>27</td>
      <td>107992</td>
      <td>67</td>
      <td>7501</td>
      <td>5</td>
      <td>3239</td>
      <td>2</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2020</td>
      <td>46675</td>
      <td>29</td>
      <td>102171</td>
      <td>64</td>
      <td>7383</td>
      <td>5</td>
      <td>2871</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {.cell .markdown id="OfOe2xWifqqa"}
**Oil & Coal Products Consumption by Sector**
:::

::: {.cell .code execution_count="17" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="OmNOfSlNfnvE" outputId="18212ff3-1aad-438b-ad80-47a039695336"}
``` python
# Send a GET request to the API endpoint
response = requests.get('https://www.emsd.gov.hk/filemanager/en/share/energy_efficiency/energy_end_use/2022/table09.csv')
# Check if the request was successful
if response.status_code == 200:
    #convert it into a file-like object
    data_io = io.StringIO(response.text)

    df_oilcoal_sector = pd.read_csv(data_io)
    print('Data read successfully.')
else:
    print(f'Request failed with status code {response.status_code}')
```

::: {.output .stream .stdout}
    Data read successfully.
:::
:::

::: {.cell .code execution_count="18" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":449}" id="m27XOACZiIVs" outputId="054d3ec3-bde8-4ee3-f173-61e9769c4c9f"}
``` python
df_oilcoal_sector
```

::: {.output .execute_result execution_count="18"}
```{=html}
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
      <th>Year</th>
      <th>Residential (Unit : Terajoule)</th>
      <th>Residential Percentage (%)</th>
      <th>Commercial (Unit : Terajoule)</th>
      <th>Commercial Percentage (%)</th>
      <th>Industrial (Unit : Terajoule)</th>
      <th>Industrial Percentage (%)</th>
      <th>Transport (Unit : Terajoule)</th>
      <th>Transport Percentage (%)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2010</td>
      <td>13</td>
      <td>0</td>
      <td>4526</td>
      <td>6</td>
      <td>4035</td>
      <td>5</td>
      <td>73213</td>
      <td>90</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2011</td>
      <td>8</td>
      <td>0</td>
      <td>1979</td>
      <td>3</td>
      <td>3978</td>
      <td>5</td>
      <td>72383</td>
      <td>92</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2012</td>
      <td>8</td>
      <td>0</td>
      <td>1696</td>
      <td>2</td>
      <td>3728</td>
      <td>5</td>
      <td>71927</td>
      <td>93</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2013</td>
      <td>7</td>
      <td>0</td>
      <td>1477</td>
      <td>2</td>
      <td>3571</td>
      <td>5</td>
      <td>71449</td>
      <td>93</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2014</td>
      <td>7</td>
      <td>0</td>
      <td>1431</td>
      <td>2</td>
      <td>3389</td>
      <td>5</td>
      <td>70165</td>
      <td>94</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2015</td>
      <td>8</td>
      <td>0</td>
      <td>1235</td>
      <td>2</td>
      <td>3386</td>
      <td>4</td>
      <td>70997</td>
      <td>94</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2016</td>
      <td>10</td>
      <td>0</td>
      <td>1019</td>
      <td>1</td>
      <td>3190</td>
      <td>4</td>
      <td>71130</td>
      <td>94</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2017</td>
      <td>14</td>
      <td>0</td>
      <td>830</td>
      <td>1</td>
      <td>3442</td>
      <td>5</td>
      <td>70835</td>
      <td>94</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2018</td>
      <td>14</td>
      <td>0</td>
      <td>675</td>
      <td>1</td>
      <td>3443</td>
      <td>5</td>
      <td>70320</td>
      <td>94</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2019</td>
      <td>15</td>
      <td>0</td>
      <td>574</td>
      <td>1</td>
      <td>3177</td>
      <td>4</td>
      <td>70754</td>
      <td>95</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2020</td>
      <td>15</td>
      <td>0</td>
      <td>498</td>
      <td>1</td>
      <td>3309</td>
      <td>5</td>
      <td>65373</td>
      <td>94</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {.cell .markdown id="8Z-dZarWf9Ok"}
**Town Gas & LPG Consumption by Sector**
:::

::: {.cell .code execution_count="19" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="vgiU8WHmfonI" outputId="5b1da677-bce3-469a-ecde-537b0a1dd193"}
``` python
# Send a GET request to the API endpoint
response = requests.get('https://www.emsd.gov.hk/filemanager/en/share/energy_efficiency/energy_end_use/2022/table10.csv')
# Check if the request was successful
if response.status_code == 200:
    #convert it into a file-like object
    data_io = io.StringIO(response.text)

    df_gaslpg_sector = pd.read_csv(data_io)
    print('Data read successfully.')
else:
    print(f'Request failed with status code {response.status_code}')
```

::: {.output .stream .stdout}
    Data read successfully.
:::
:::

::: {.cell .code execution_count="20" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":449}" id="DaXxkCQmiKaU" outputId="04661e59-dc7d-40ba-defb-68c618b102f8"}
``` python
df_gaslpg_sector
```

::: {.output .execute_result execution_count="20"}
```{=html}
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
      <th>Year</th>
      <th>Residential (Unit : Terajoule)</th>
      <th>Residential Percentage (%)</th>
      <th>Commercial (Unit : Terajoule)</th>
      <th>Commercial Percentage (%)</th>
      <th>Industrial (Unit : Terajoule)</th>
      <th>Industrial Percentage (%)</th>
      <th>Transport (Unit : Terajoule)</th>
      <th>Transport Percentage (%)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2010</td>
      <td>19038</td>
      <td>39</td>
      <td>13971</td>
      <td>28</td>
      <td>937</td>
      <td>2</td>
      <td>15137</td>
      <td>31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2011</td>
      <td>18977</td>
      <td>38</td>
      <td>14129</td>
      <td>29</td>
      <td>956</td>
      <td>2</td>
      <td>15506</td>
      <td>31</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2012</td>
      <td>18841</td>
      <td>38</td>
      <td>14280</td>
      <td>29</td>
      <td>1111</td>
      <td>2</td>
      <td>15384</td>
      <td>31</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2013</td>
      <td>18635</td>
      <td>37</td>
      <td>14512</td>
      <td>29</td>
      <td>1229</td>
      <td>2</td>
      <td>15348</td>
      <td>31</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2014</td>
      <td>18681</td>
      <td>37</td>
      <td>14713</td>
      <td>29</td>
      <td>1264</td>
      <td>2</td>
      <td>16185</td>
      <td>32</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2015</td>
      <td>18063</td>
      <td>37</td>
      <td>14535</td>
      <td>30</td>
      <td>1308</td>
      <td>3</td>
      <td>15048</td>
      <td>31</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2016</td>
      <td>18574</td>
      <td>38</td>
      <td>14601</td>
      <td>30</td>
      <td>1232</td>
      <td>2</td>
      <td>14967</td>
      <td>30</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2017</td>
      <td>18335</td>
      <td>38</td>
      <td>14908</td>
      <td>31</td>
      <td>1317</td>
      <td>3</td>
      <td>13347</td>
      <td>28</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2018</td>
      <td>19578</td>
      <td>40</td>
      <td>15253</td>
      <td>31</td>
      <td>1448</td>
      <td>3</td>
      <td>12262</td>
      <td>25</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2019</td>
      <td>18070</td>
      <td>38</td>
      <td>14440</td>
      <td>31</td>
      <td>1596</td>
      <td>3</td>
      <td>13232</td>
      <td>28</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2020</td>
      <td>19726</td>
      <td>45</td>
      <td>11844</td>
      <td>27</td>
      <td>1470</td>
      <td>3</td>
      <td>11155</td>
      <td>25</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {.cell .markdown id="PP_DUbfigAk8"}
**Total Energy Consumption by End-use**
:::

::: {.cell .code execution_count="21" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="pMwdqEZYfpZk" outputId="715f0b63-1bb1-4bc9-b387-4db79624bd8d"}
``` python
# Send a GET request to the API endpoint
response = requests.get('https://www.emsd.gov.hk/filemanager/en/share/energy_efficiency/energy_end_use/2022/table11.csv')
# Check if the request was successful
if response.status_code == 200:
    #convert it into a file-like object
    data_io = io.StringIO(response.text)

    df_energy_enduse = pd.read_csv(data_io)
    print('Data read successfully.')
else:
    print(f'Request failed with status code {response.status_code}')
```

::: {.output .stream .stdout}
    Data read successfully.
:::
:::

::: {.cell .code execution_count="22" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":513}" id="fJGHjDr-iM3B" outputId="0c98b8ab-d837-4b1f-f1fa-1c9ee13cb423"}
``` python
df_energy_enduse
```

::: {.output .execute_result execution_count="22"}
```{=html}
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
      <th>Year</th>
      <th>Air Conditioning (Unit : Terajoule)</th>
      <th>Air Conditioning Percentage (%)</th>
      <th>Cooking (Unit : Terajoule)</th>
      <th>Cooking Percentage (%)</th>
      <th>Industrial Process/ Equipment (Unit : Terajoule)</th>
      <th>Industrial Process/ Equipment Percentage (%)</th>
      <th>Lighting (Unit : Terajoule)</th>
      <th>Lighting Percentage (%)</th>
      <th>Office Equipment (Unit : Terajoule)</th>
      <th>...</th>
      <th>Bus (Unit : Terajoule)</th>
      <th>Bus Percentage (%)</th>
      <th>Taxi (Unit : Terajoule)</th>
      <th>Taxi Percentage (%)</th>
      <th>Car (Unit : Terajoule)</th>
      <th>Car Percentage (%)</th>
      <th>Marine (Unit : Terajoule)</th>
      <th>Marine Percentage (%)</th>
      <th>Others (Unit : Terajoule)</th>
      <th>Others Percentage (%)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2010</td>
      <td>45511</td>
      <td>16</td>
      <td>33379</td>
      <td>12</td>
      <td>18620</td>
      <td>7</td>
      <td>19563</td>
      <td>7</td>
      <td>11758</td>
      <td>...</td>
      <td>18842</td>
      <td>7</td>
      <td>13373</td>
      <td>5</td>
      <td>18247</td>
      <td>6</td>
      <td>8672</td>
      <td>3</td>
      <td>42031</td>
      <td>15</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2011</td>
      <td>44617</td>
      <td>16</td>
      <td>30830</td>
      <td>11</td>
      <td>15452</td>
      <td>6</td>
      <td>18357</td>
      <td>7</td>
      <td>12313</td>
      <td>...</td>
      <td>18911</td>
      <td>7</td>
      <td>13593</td>
      <td>5</td>
      <td>18795</td>
      <td>7</td>
      <td>8245</td>
      <td>3</td>
      <td>48544</td>
      <td>17</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2012</td>
      <td>45091</td>
      <td>16</td>
      <td>30876</td>
      <td>11</td>
      <td>15514</td>
      <td>6</td>
      <td>18524</td>
      <td>7</td>
      <td>12896</td>
      <td>...</td>
      <td>19128</td>
      <td>7</td>
      <td>13469</td>
      <td>5</td>
      <td>19432</td>
      <td>7</td>
      <td>8077</td>
      <td>3</td>
      <td>50636</td>
      <td>18</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2013</td>
      <td>43834</td>
      <td>16</td>
      <td>32205</td>
      <td>12</td>
      <td>15595</td>
      <td>6</td>
      <td>17774</td>
      <td>6</td>
      <td>11825</td>
      <td>...</td>
      <td>19144</td>
      <td>7</td>
      <td>13319</td>
      <td>5</td>
      <td>20955</td>
      <td>7</td>
      <td>7739</td>
      <td>3</td>
      <td>50315</td>
      <td>18</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2014</td>
      <td>47277</td>
      <td>17</td>
      <td>32578</td>
      <td>11</td>
      <td>15722</td>
      <td>6</td>
      <td>17365</td>
      <td>6</td>
      <td>11583</td>
      <td>...</td>
      <td>19285</td>
      <td>7</td>
      <td>13696</td>
      <td>5</td>
      <td>20641</td>
      <td>7</td>
      <td>7705</td>
      <td>3</td>
      <td>50956</td>
      <td>18</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2015</td>
      <td>46940</td>
      <td>17</td>
      <td>32461</td>
      <td>11</td>
      <td>15857</td>
      <td>6</td>
      <td>16914</td>
      <td>6</td>
      <td>11026</td>
      <td>...</td>
      <td>19168</td>
      <td>7</td>
      <td>12437</td>
      <td>4</td>
      <td>21354</td>
      <td>8</td>
      <td>7792</td>
      <td>3</td>
      <td>51870</td>
      <td>18</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2016</td>
      <td>46455</td>
      <td>16</td>
      <td>33208</td>
      <td>12</td>
      <td>15127</td>
      <td>5</td>
      <td>16385</td>
      <td>6</td>
      <td>10709</td>
      <td>...</td>
      <td>18918</td>
      <td>7</td>
      <td>12288</td>
      <td>4</td>
      <td>22189</td>
      <td>8</td>
      <td>7474</td>
      <td>3</td>
      <td>52893</td>
      <td>19</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2017</td>
      <td>46410</td>
      <td>17</td>
      <td>33510</td>
      <td>12</td>
      <td>15591</td>
      <td>6</td>
      <td>16026</td>
      <td>6</td>
      <td>10233</td>
      <td>...</td>
      <td>18663</td>
      <td>7</td>
      <td>10686</td>
      <td>4</td>
      <td>22005</td>
      <td>8</td>
      <td>7459</td>
      <td>3</td>
      <td>41947</td>
      <td>15</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2018</td>
      <td>48047</td>
      <td>17</td>
      <td>34947</td>
      <td>12</td>
      <td>15779</td>
      <td>6</td>
      <td>16255</td>
      <td>6</td>
      <td>10412</td>
      <td>...</td>
      <td>18286</td>
      <td>6</td>
      <td>9519</td>
      <td>3</td>
      <td>22421</td>
      <td>8</td>
      <td>7006</td>
      <td>2</td>
      <td>41172</td>
      <td>15</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2019</td>
      <td>47979</td>
      <td>17</td>
      <td>32871</td>
      <td>12</td>
      <td>15107</td>
      <td>5</td>
      <td>16094</td>
      <td>6</td>
      <td>10534</td>
      <td>...</td>
      <td>18028</td>
      <td>6</td>
      <td>10463</td>
      <td>4</td>
      <td>22925</td>
      <td>8</td>
      <td>7342</td>
      <td>3</td>
      <td>44928</td>
      <td>16</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2020</td>
      <td>48634</td>
      <td>18</td>
      <td>29668</td>
      <td>11</td>
      <td>14467</td>
      <td>5</td>
      <td>15786</td>
      <td>6</td>
      <td>10605</td>
      <td>...</td>
      <td>14811</td>
      <td>5</td>
      <td>8701</td>
      <td>3</td>
      <td>22067</td>
      <td>8</td>
      <td>7094</td>
      <td>3</td>
      <td>44320</td>
      <td>16</td>
    </tr>
  </tbody>
</table>
<p>11 rows × 29 columns</p>
</div>
```
:::
:::

::: {.cell .markdown id="F08745tmgIyR"}
**Electricity Consumption by End-use**
:::

::: {.cell .code execution_count="23" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="ReCtu-IXfpSU" outputId="88f2f566-6f86-4404-f3cd-3f5958ccff95"}
``` python
# Send a GET request to the API endpoint
response = requests.get('https://www.emsd.gov.hk/filemanager/en/share/energy_efficiency/energy_end_use/2022/table12.csv')
# Check if the request was successful
if response.status_code == 200:
    #convert it into a file-like object
    data_io = io.StringIO(response.text)

    df_electricity_enduse = pd.read_csv(data_io)
    print('Data read successfully.')
else:
    print(f'Request failed with status code {response.status_code}')
```

::: {.output .stream .stdout}
    Data read successfully.
:::
:::

::: {.cell .code execution_count="24" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":484}" id="mIqXu3wXiO5z" outputId="6b15f0a2-d476-4dea-9bb6-27b6dec33739"}
``` python
df_electricity_enduse
```

::: {.output .execute_result execution_count="24"}
```{=html}
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
      <th>Year</th>
      <th>Air Conditioning (Unit : Terajoule)</th>
      <th>Air Conditioning Percentage (%)</th>
      <th>Lighting (Unit : Terajoule)</th>
      <th>Lighting Percentage (%)</th>
      <th>Refrigeration (Unit : Terajoule)</th>
      <th>Refrigeration Percentage (%)</th>
      <th>Industrial Process/ Equipment (Unit : Terajoule)</th>
      <th>Industrial Process/ Equipment Percentage (%)</th>
      <th>Cooking (Unit : Terajoule)</th>
      <th>Cooking Percentage (%)</th>
      <th>Hot Water (Unit : Terajoule)</th>
      <th>Hot Water Percentage (%)</th>
      <th>Office Equipment (Unit : Terajoule)</th>
      <th>Office Equipment Percentage (%)</th>
      <th>Vertical Transport (Unit : Terajoule)</th>
      <th>Vertical Transport Percentage (%)</th>
      <th>Others (Unit : Terajoule)</th>
      <th>Others Percentage (%)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2010</td>
      <td>45511</td>
      <td>30</td>
      <td>19563</td>
      <td>13</td>
      <td>9213</td>
      <td>6</td>
      <td>10016</td>
      <td>7</td>
      <td>11430</td>
      <td>8</td>
      <td>5015</td>
      <td>3</td>
      <td>11758</td>
      <td>8</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>38354</td>
      <td>25</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2011</td>
      <td>44605</td>
      <td>29</td>
      <td>18357</td>
      <td>12</td>
      <td>8117</td>
      <td>5</td>
      <td>9119</td>
      <td>6</td>
      <td>9565</td>
      <td>6</td>
      <td>4701</td>
      <td>3</td>
      <td>12313</td>
      <td>8</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>44829</td>
      <td>30</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2012</td>
      <td>45079</td>
      <td>29</td>
      <td>18524</td>
      <td>12</td>
      <td>7723</td>
      <td>5</td>
      <td>8915</td>
      <td>6</td>
      <td>10191</td>
      <td>7</td>
      <td>4610</td>
      <td>3</td>
      <td>12896</td>
      <td>8</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>47143</td>
      <td>30</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2013</td>
      <td>43821</td>
      <td>29</td>
      <td>17774</td>
      <td>12</td>
      <td>6886</td>
      <td>4</td>
      <td>8837</td>
      <td>6</td>
      <td>12115</td>
      <td>8</td>
      <td>5167</td>
      <td>3</td>
      <td>11825</td>
      <td>8</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>46939</td>
      <td>31</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2014</td>
      <td>47264</td>
      <td>30</td>
      <td>17365</td>
      <td>11</td>
      <td>6549</td>
      <td>4</td>
      <td>8875</td>
      <td>6</td>
      <td>13023</td>
      <td>8</td>
      <td>5946</td>
      <td>4</td>
      <td>11583</td>
      <td>7</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>47542</td>
      <td>30</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2015</td>
      <td>46927</td>
      <td>30</td>
      <td>16914</td>
      <td>11</td>
      <td>5812</td>
      <td>4</td>
      <td>8948</td>
      <td>6</td>
      <td>13768</td>
      <td>9</td>
      <td>6267</td>
      <td>4</td>
      <td>11026</td>
      <td>7</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>48719</td>
      <td>31</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2016</td>
      <td>46441</td>
      <td>29</td>
      <td>16385</td>
      <td>10</td>
      <td>5176</td>
      <td>3</td>
      <td>8365</td>
      <td>5</td>
      <td>14799</td>
      <td>9</td>
      <td>7104</td>
      <td>4</td>
      <td>10709</td>
      <td>7</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>49861</td>
      <td>31</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2017</td>
      <td>46396</td>
      <td>29</td>
      <td>16026</td>
      <td>10</td>
      <td>4454</td>
      <td>3</td>
      <td>8322</td>
      <td>5</td>
      <td>15714</td>
      <td>10</td>
      <td>7354</td>
      <td>5</td>
      <td>10233</td>
      <td>6</td>
      <td>10313.0</td>
      <td>7.0</td>
      <td>39166</td>
      <td>25</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2018</td>
      <td>48032</td>
      <td>30</td>
      <td>16255</td>
      <td>10</td>
      <td>4292</td>
      <td>3</td>
      <td>8365</td>
      <td>5</td>
      <td>16283</td>
      <td>10</td>
      <td>7561</td>
      <td>5</td>
      <td>10412</td>
      <td>7</td>
      <td>10073.0</td>
      <td>6.0</td>
      <td>38220</td>
      <td>24</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2019</td>
      <td>47965</td>
      <td>30</td>
      <td>16094</td>
      <td>10</td>
      <td>4363</td>
      <td>3</td>
      <td>7869</td>
      <td>5</td>
      <td>15560</td>
      <td>10</td>
      <td>7309</td>
      <td>5</td>
      <td>10534</td>
      <td>7</td>
      <td>9566.0</td>
      <td>6.0</td>
      <td>42410</td>
      <td>26</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2020</td>
      <td>48622</td>
      <td>31</td>
      <td>15786</td>
      <td>10</td>
      <td>4492</td>
      <td>3</td>
      <td>7391</td>
      <td>5</td>
      <td>13568</td>
      <td>9</td>
      <td>7093</td>
      <td>4</td>
      <td>10605</td>
      <td>7</td>
      <td>9417.0</td>
      <td>6.0</td>
      <td>42126</td>
      <td>26</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {.cell .markdown id="z25crRbsgPwT"}
**Oil & Coal Products Consumption by End-use**
:::

::: {.cell .code execution_count="25" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="egZDZ0qogNvO" outputId="8b5252e1-1863-48f2-9de7-e8b3d165038c"}
``` python
# Send a GET request to the API endpoint
response = requests.get('https://www.emsd.gov.hk/filemanager/en/share/energy_efficiency/energy_end_use/2022/table13.csv')
# Check if the request was successful
if response.status_code == 200:
    #convert it into a file-like object
    data_io = io.StringIO(response.text)

    df_oilcoal_enduse = pd.read_csv(data_io)
    print('Data read successfully.')
else:
    print(f'Request failed with status code {response.status_code}')
```

::: {.output .stream .stdout}
    Data read successfully.
:::
:::

::: {.cell .code execution_count="26" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":484}" id="g3JKRqf4iYpw" outputId="fe44fd1f-dafc-4709-ccf1-ff99ef4a027f"}
``` python
df_oilcoal_enduse
```

::: {.output .execute_result execution_count="26"}
```{=html}
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
      <th>Year</th>
      <th>Goods Vehicle (Unit : Terajoule)</th>
      <th>Goods Vehicle Percentage (%)</th>
      <th>Bus (Unit : Terajoule)</th>
      <th>Bus Percentage (%)</th>
      <th>Taxi (Unit : Terajoule)</th>
      <th>Taxi Percentage (%)</th>
      <th>Car (Unit : Terajoule)</th>
      <th>Car Percentage (%)</th>
      <th>Motorcycle (Unit : Terajoule)</th>
      <th>Motorcycle Percentage (%)</th>
      <th>Industrial Process/ Equipment (Unit : Terajoule)</th>
      <th>Industrial Process/ Equipment Percentage (%)</th>
      <th>Marine (Unit : Terajoule)</th>
      <th>Marine Percentage (%)</th>
      <th>Others (Unit : Terajoule)</th>
      <th>Others Percentage (%)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2010</td>
      <td>28585</td>
      <td>35</td>
      <td>17077</td>
      <td>21</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>18247</td>
      <td>22</td>
      <td>436</td>
      <td>1</td>
      <td>6423</td>
      <td>8</td>
      <td>8672</td>
      <td>11</td>
      <td>2346</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2011</td>
      <td>27818</td>
      <td>36</td>
      <td>16997</td>
      <td>22</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>18795</td>
      <td>24</td>
      <td>425</td>
      <td>1</td>
      <td>4194</td>
      <td>5</td>
      <td>8245</td>
      <td>11</td>
      <td>1875</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2012</td>
      <td>26681</td>
      <td>34</td>
      <td>17212</td>
      <td>22</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>19432</td>
      <td>25</td>
      <td>421</td>
      <td>1</td>
      <td>4067</td>
      <td>5</td>
      <td>8077</td>
      <td>10</td>
      <td>1467</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2013</td>
      <td>25126</td>
      <td>33</td>
      <td>17114</td>
      <td>22</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>20955</td>
      <td>27</td>
      <td>411</td>
      <td>1</td>
      <td>3984</td>
      <td>5</td>
      <td>7739</td>
      <td>10</td>
      <td>1173</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2014</td>
      <td>24510</td>
      <td>33</td>
      <td>16795</td>
      <td>22</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>20630</td>
      <td>28</td>
      <td>418</td>
      <td>1</td>
      <td>3828</td>
      <td>5</td>
      <td>7705</td>
      <td>10</td>
      <td>1105</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2015</td>
      <td>24782</td>
      <td>33</td>
      <td>16556</td>
      <td>22</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>21323</td>
      <td>28</td>
      <td>436</td>
      <td>1</td>
      <td>3829</td>
      <td>5</td>
      <td>7792</td>
      <td>10</td>
      <td>908</td>
      <td>1</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2016</td>
      <td>24718</td>
      <td>33</td>
      <td>16239</td>
      <td>22</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>22132</td>
      <td>29</td>
      <td>443</td>
      <td>1</td>
      <td>3604</td>
      <td>5</td>
      <td>7474</td>
      <td>10</td>
      <td>739</td>
      <td>1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2017</td>
      <td>24845</td>
      <td>33</td>
      <td>16002</td>
      <td>21</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>21919</td>
      <td>29</td>
      <td>462</td>
      <td>1</td>
      <td>3788</td>
      <td>5</td>
      <td>7459</td>
      <td>10</td>
      <td>646</td>
      <td>1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2018</td>
      <td>24837</td>
      <td>33</td>
      <td>15543</td>
      <td>21</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>22333</td>
      <td>30</td>
      <td>452</td>
      <td>1</td>
      <td>3689</td>
      <td>5</td>
      <td>7006</td>
      <td>9</td>
      <td>592</td>
      <td>1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2019</td>
      <td>24735</td>
      <td>33</td>
      <td>15259</td>
      <td>20</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>22815</td>
      <td>31</td>
      <td>459</td>
      <td>1</td>
      <td>3279</td>
      <td>4</td>
      <td>7342</td>
      <td>10</td>
      <td>631</td>
      <td>1</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2020</td>
      <td>23261</td>
      <td>34</td>
      <td>12358</td>
      <td>18</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>21922</td>
      <td>32</td>
      <td>563</td>
      <td>1</td>
      <td>3409</td>
      <td>5</td>
      <td>7094</td>
      <td>10</td>
      <td>588</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {.cell .markdown id="z_YV-XUUgUwC"}
**Town Gas & Liqueﬁed Petroleum Gas Consumption by End-use**
:::

::: {.cell .code execution_count="27" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="VP35eXXZgYD5" outputId="68965cf7-76df-468e-e087-f094fc986f6f"}
``` python
# Send a GET request to the API endpoint
response = requests.get('https://www.emsd.gov.hk/filemanager/en/share/energy_efficiency/energy_end_use/2022/table14.csv')
# Check if the request was successful
if response.status_code == 200:
    #convert it into a file-like object
    data_io = io.StringIO(response.text)

    df_gaslpg_enduse = pd.read_csv(data_io)
    print('Data read successfully.')
else:
    print(f'Request failed with status code {response.status_code}')
```

::: {.output .stream .stdout}
    Data read successfully.
:::
:::

::: {.cell .code execution_count="28" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":449}" id="Bhw2JyvbiadJ" outputId="42b24bb7-1d65-47b8-8b60-0be862c3480f"}
``` python
df_gaslpg_enduse
```

::: {.output .execute_result execution_count="28"}
```{=html}
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
      <th>Year</th>
      <th>Cooking (Unit : Terajoule)</th>
      <th>Cooking Percentage (%)</th>
      <th>Hot Water (Unit : Terajoule)</th>
      <th>Hot Water Percentage (%)</th>
      <th>Bus &amp; Taxi (Unit : Terajoule)</th>
      <th>Bus &amp; Taxi Percentage (%)</th>
      <th>Others (Unit : Terajoule)</th>
      <th>Others Percentage (%)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2010</td>
      <td>21244</td>
      <td>43</td>
      <td>8921</td>
      <td>18</td>
      <td>15137</td>
      <td>31</td>
      <td>3782</td>
      <td>8</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2011</td>
      <td>20771</td>
      <td>42</td>
      <td>9232</td>
      <td>19</td>
      <td>15505</td>
      <td>31</td>
      <td>4060</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2012</td>
      <td>20316</td>
      <td>41</td>
      <td>9395</td>
      <td>19</td>
      <td>15384</td>
      <td>31</td>
      <td>4521</td>
      <td>9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2013</td>
      <td>19751</td>
      <td>40</td>
      <td>9701</td>
      <td>20</td>
      <td>15348</td>
      <td>31</td>
      <td>4923</td>
      <td>10</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2014</td>
      <td>19258</td>
      <td>38</td>
      <td>10166</td>
      <td>20</td>
      <td>16185</td>
      <td>32</td>
      <td>5236</td>
      <td>10</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2015</td>
      <td>18414</td>
      <td>38</td>
      <td>10276</td>
      <td>21</td>
      <td>15048</td>
      <td>31</td>
      <td>5217</td>
      <td>11</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2016</td>
      <td>18142</td>
      <td>37</td>
      <td>10912</td>
      <td>22</td>
      <td>14967</td>
      <td>30</td>
      <td>5353</td>
      <td>11</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2017</td>
      <td>17551</td>
      <td>37</td>
      <td>11245</td>
      <td>23</td>
      <td>13347</td>
      <td>28</td>
      <td>5763</td>
      <td>12</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2018</td>
      <td>18491</td>
      <td>38</td>
      <td>11613</td>
      <td>24</td>
      <td>12262</td>
      <td>25</td>
      <td>6175</td>
      <td>13</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2019</td>
      <td>17069</td>
      <td>36</td>
      <td>11090</td>
      <td>23</td>
      <td>13232</td>
      <td>28</td>
      <td>5947</td>
      <td>13</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2020</td>
      <td>15952</td>
      <td>36</td>
      <td>11886</td>
      <td>27</td>
      <td>11155</td>
      <td>25</td>
      <td>5201</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {.cell .markdown id="PpPOhlIagbYB"}
Type of Renewable Energy in Hong Kong
:::

::: {.cell .code execution_count="29" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="xS1IJtH0ggn7" outputId="f51dac6e-f892-4ab9-c002-4f993f5ea076"}
``` python
# Send a GET request to the API endpoint
response = requests.get('https://www.emsd.gov.hk/filemanager/en/share/energy_efficiency/energy_end_use/2022/table15.csv')
# Check if the request was successful
if response.status_code == 200:
    #convert it into a file-like object
    data_io = io.StringIO(response.text)

    df_energy_renewable = pd.read_csv(data_io)
    print('Data read successfully.')
else:
    print(f'Request failed with status code {response.status_code}')
```

::: {.output .stream .stdout}
    Data read successfully.
:::
:::

::: {.cell .code execution_count="30" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":192}" id="RVBsYpLEic1E" outputId="123e983f-10a3-4195-b3b6-c91c11efb813"}
``` python
df_energy_renewable
```

::: {.output .execute_result execution_count="30"}
```{=html}
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
      <th>Type of Renewable Energy</th>
      <th>Renewable Energy (Unit : Terajoule)</th>
      <th>Renewable Energy Percentage (%)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Waste-to-energy</td>
      <td>1930</td>
      <td>80.3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Wind Energy &amp; Hydropower</td>
      <td>9</td>
      <td>0.4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Solar Energy</td>
      <td>189</td>
      <td>7.9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Bio-diesel</td>
      <td>276</td>
      <td>11.5</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {.cell .markdown id="2qlCXIXAgi-Q"}
**Type of Renewable Energy in Hong Kong by Fuel**
:::

::: {.cell .code execution_count="31" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="P9NJHKC7gmgG" outputId="e0bca0b5-7f74-43df-ee19-c2f1cfad86b1"}
``` python
# Send a GET request to the API endpoint
response = requests.get('https://www.emsd.gov.hk/filemanager/en/share/energy_efficiency/energy_end_use/2022/table16.csv')
# Check if the request was successful
if response.status_code == 200:
    #convert it into a file-like object
    data_io = io.StringIO(response.text)

    df_energy_renewable_fuel = pd.read_csv(data_io)
    print('Data read successfully.')
else:
    print(f'Request failed with status code {response.status_code}')
```

::: {.output .stream .stdout}
    Data read successfully.
:::
:::

::: {.cell .code execution_count="32" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":230}" id="i0HMiKjAif7I" outputId="67bfb3e4-8e91-4908-ff2a-d324cb093029"}
``` python
df_energy_renewable_fuel
```

::: {.output .execute_result execution_count="32"}
```{=html}
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
      <th>Type of Fuel</th>
      <th>Weighting of Fuel in Energy End-use (Unit : Terajoule)</th>
      <th>Weighting of Fuel in Energy End-use Percentage (%)</th>
      <th>Weighting of Renewable Energy in Respective Fuel Type (Unit :Terajoule)</th>
      <th>Weighting of Renewable Energy in Respective Fuel Type Percentage (%)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Electricity</td>
      <td>159100</td>
      <td>58.4</td>
      <td>608</td>
      <td>0.4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Town Gas &amp; LPG</td>
      <td>44195</td>
      <td>16.2</td>
      <td>1520</td>
      <td>3.4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Oil &amp; Coal Products</td>
      <td>69195</td>
      <td>25.4</td>
      <td>276</td>
      <td>0.4</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {.cell .code execution_count="33" id="N9F05D4mx5CC"}
``` python
dataframes = [df_overview, df_total_fuel, df_residential_fuel, df_commercial_fuel, df_industrial_fuel,
              df_transport_fuel, df_energy_sector, df_electricity_sector, df_oilcoal_sector,
              df_gaslpg_sector, df_energy_enduse, df_electricity_enduse, df_oilcoal_enduse,
              df_gaslpg_enduse, df_energy_renewable, df_energy_renewable_fuel]
```
:::

::: {.cell .code execution_count="34" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="l_6AkCIux7b5" outputId="f3418c2d-85d3-4fe3-96a2-06ac2bde1926"}
``` python
for df in dataframes:
    print(df.shape)
```

::: {.output .stream .stdout}
    (11, 7)
    (11, 7)
    (11, 7)
    (11, 7)
    (11, 7)
    (11, 7)
    (11, 9)
    (11, 9)
    (11, 9)
    (11, 9)
    (11, 29)
    (11, 19)
    (11, 17)
    (11, 9)
    (4, 3)
    (3, 5)
:::
:::

::: {.cell .code execution_count="35" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="9jzfkLh1x-tO" outputId="3d2269a8-9702-49c2-fbb0-262d4be3c26a"}
``` python
for df in dataframes:
    print(df.isnull().sum())
```

::: {.output .stream .stdout}
    Year                                                  0
    Energy End-use (TJ)/ GDP (HK$ billion)                0
    Energy End-use (TJ)                                   0
    GDP in Hong Kong in chained 2020 HKD (HK$ million)    0
    Energy End-use/ Capita (GJ)                           0
    Electricity/ Capita (GJ)                              0
    Population ('000)                                     0
    dtype: int64
    Year                                                     0
    Town Gas & Liquefied Petroleum Gas (Unit : Terajoule)    0
    Town Gas & Liquefied Petroleum Gas Percentage (%)        0
    Oil & Coal Products (Unit : Terajoule)                   0
    Oil & Coal Products Percentage (%)                       0
    Electricity (Unit : Terajoule)                           0
    Electricity Percentage (%)                               0
    dtype: int64
    Year                                                     0
    Town Gas & Liquefied Petroleum Gas (Unit : Terajoule)    0
    Town Gas & Liquefied Petroleum Gas Percentage (%)        0
    Oil & Coal Products (Unit : Terajoule)                   0
    Oil & Coal Products Percentage (%)                       0
    Electricity (Unit : Terajoule)                           0
    Electricity Percentage (%)                               0
    dtype: int64
    Year                                                     0
    Town Gas & Liquefied Petroleum Gas (Unit : Terajoule)    0
    Town Gas & Liquefied Petroleum Gas Percentage (%)        0
    Oil & Coal Products (Unit : Terajoule)                   0
    Oil & Coal Products Percentage (%)                       0
    Electricity (Unit : Terajoule)                           0
    Electricity Percentage (%)                               0
    dtype: int64
    Year                                                     0
    Town Gas & Liquefied Petroleum Gas (Unit : Terajoule)    0
    Town Gas & Liquefied Petroleum Gas Percentage (%)        0
    Oil & Coal Products (Unit : Terajoule)                   0
    Oil & Coal Products Percentage (%)                       0
    Electricity (Unit : Terajoule)                           0
    Electricity Percentage (%)                               0
    dtype: int64
    Year                                                     0
    Town Gas & Liquefied Petroleum Gas (Unit : Terajoule)    0
    Town Gas & Liquefied Petroleum Gas Percentage (%)        0
    Oil & Coal Products (Unit : Terajoule)                   0
    Oil & Coal Products Percentage (%)                       0
    Electricity (Unit : Terajoule)                           0
    Electricity Percentage (%)                               0
    dtype: int64
    Year                              0
    Residential (Unit : Terajoule)    0
    Residential Percentage (%)        0
    Commercial (Unit : Terajoule)     0
    Commercial Percentage (%)         0
    Industrial (Unit : Terajoule)     0
    Industrial Percentage (%)         0
    Transport (Unit : Terajoule)      0
    Transport Percentage (%)          0
    dtype: int64
    Year                              0
    Residential (Unit : Terajoule)    0
    Residential Percentage (%)        0
    Commercial (Unit : Terajoule)     0
    Commercial Percentage (%)         0
    Industrial (Unit : Terajoule)     0
    Industrial Percentage (%)         0
    Transport (Unit : Terajoule)      0
    Transport Percentage (%)          0
    dtype: int64
    Year                              0
    Residential (Unit : Terajoule)    0
    Residential Percentage (%)        0
    Commercial (Unit : Terajoule)     0
    Commercial Percentage (%)         0
    Industrial (Unit : Terajoule)     0
    Industrial Percentage (%)         0
    Transport (Unit : Terajoule)      0
    Transport Percentage (%)          0
    dtype: int64
    Year                              0
    Residential (Unit : Terajoule)    0
    Residential Percentage (%)        0
    Commercial (Unit : Terajoule)     0
    Commercial Percentage (%)         0
    Industrial (Unit : Terajoule)     0
    Industrial Percentage (%)         0
    Transport (Unit : Terajoule)      0
    Transport Percentage (%)          0
    dtype: int64
    Year                                                0
    Air Conditioning (Unit : Terajoule)                 0
    Air Conditioning Percentage (%)                     0
    Cooking (Unit : Terajoule)                          0
    Cooking Percentage (%)                              0
    Industrial Process/ Equipment (Unit : Terajoule)    0
    Industrial Process/ Equipment Percentage (%)        0
    Lighting (Unit : Terajoule)                         0
    Lighting Percentage (%)                             0
    Office Equipment (Unit : Terajoule)                 0
    Office Equipment Percentage (%)                     0
    Refrigeration (Unit : Terajoule)                    0
    Refrigeration Percentage (%)                        0
    Hot Water (Unit : Terajoule)                        0
    Hot Water Percentage (%)                            0
    Vertical Transport (Unit : Terajoule)               7
    Vertical Transport Percentage (%)                   7
    Goods Vehicle (Unit : Terajoule)                    0
    Goods Vehicle Percentage (%)                        0
    Bus (Unit : Terajoule)                              0
    Bus Percentage (%)                                  0
    Taxi (Unit : Terajoule)                             0
    Taxi Percentage (%)                                 0
    Car (Unit : Terajoule)                              0
    Car Percentage (%)                                  0
    Marine (Unit : Terajoule)                           0
    Marine Percentage (%)                               0
    Others (Unit : Terajoule)                           0
    Others Percentage (%)                               0
    dtype: int64
    Year                                                0
    Air Conditioning (Unit : Terajoule)                 0
    Air Conditioning Percentage (%)                     0
    Lighting (Unit : Terajoule)                         0
    Lighting Percentage (%)                             0
    Refrigeration (Unit : Terajoule)                    0
    Refrigeration Percentage (%)                        0
    Industrial Process/ Equipment (Unit : Terajoule)    0
    Industrial Process/ Equipment Percentage (%)        0
    Cooking (Unit : Terajoule)                          0
    Cooking Percentage (%)                              0
    Hot Water (Unit : Terajoule)                        0
    Hot Water Percentage (%)                            0
    Office Equipment (Unit : Terajoule)                 0
    Office Equipment Percentage (%)                     0
    Vertical Transport (Unit : Terajoule)               7
    Vertical Transport Percentage (%)                   7
    Others (Unit : Terajoule)                           0
    Others Percentage (%)                               0
    dtype: int64
    Year                                                0
    Goods Vehicle (Unit : Terajoule)                    0
    Goods Vehicle Percentage (%)                        0
    Bus (Unit : Terajoule)                              0
    Bus Percentage (%)                                  0
    Taxi (Unit : Terajoule)                             5
    Taxi Percentage (%)                                 5
    Car (Unit : Terajoule)                              0
    Car Percentage (%)                                  0
    Motorcycle (Unit : Terajoule)                       0
    Motorcycle Percentage (%)                           0
    Industrial Process/ Equipment (Unit : Terajoule)    0
    Industrial Process/ Equipment Percentage (%)        0
    Marine (Unit : Terajoule)                           0
    Marine Percentage (%)                               0
    Others (Unit : Terajoule)                           0
    Others Percentage (%)                               0
    dtype: int64
    Year                             0
    Cooking (Unit : Terajoule)       0
    Cooking Percentage (%)           0
    Hot Water (Unit : Terajoule)     0
    Hot Water Percentage (%)         0
    Bus & Taxi (Unit : Terajoule)    0
    Bus & Taxi Percentage (%)        0
    Others (Unit : Terajoule)        0
    Others Percentage (%)            0
    dtype: int64
    Type of Renewable Energy               0
    Renewable Energy (Unit : Terajoule)    0
    Renewable Energy Percentage (%)        0
    dtype: int64
    Type of Fuel                                                               0
    Weighting of Fuel in Energy End-use (Unit : Terajoule)                     0
    Weighting of Fuel in Energy End-use Percentage (%)                         0
    Weighting of Renewable Energy in Respective Fuel Type (Unit :Terajoule)    0
    Weighting of Renewable Energy in Respective Fuel Type Percentage (%)       0
    dtype: int64
:::
:::

::: {.cell .code execution_count="36" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":542}" id="L2UXxF7CyCKC" outputId="63361af0-a0e7-4a94-b278-60a48f5d651a"}
``` python
import plotly.express as px
import plotly.graph_objects as go
import plotly.figure_factory as ff

# Heatmap
df_corr = df_overview.corr()
fig = go.Figure(data=go.Heatmap(z=df_corr.values.tolist(), x=df_corr.columns.tolist(), y=df_corr.columns.tolist()))
fig.show()
```

::: {.output .display_data}
``` json
{"config":{"plotlyServerURL":"https://plot.ly"},"data":[{"type":"heatmap","x":["Year","Energy End-use (TJ)/ GDP (HK$ billion)","Energy End-use (TJ)","GDP in Hong Kong in chained 2020 HKD (HK$ million)","Energy End-use/ Capita (GJ)","Electricity/ Capita (GJ)","Population ('000)"],"y":["Year","Energy End-use (TJ)/ GDP (HK$ billion)","Energy End-use (TJ)","GDP in Hong Kong in chained 2020 HKD (HK$ million)","Energy End-use/ Capita (GJ)","Electricity/ Capita (GJ)","Population ('000)"],"z":[[1,-0.9343487590252231,-0.2453822926744781,0.8862168778706535,-0.9489396513905969,-0.28605745392972376,0.9919886221303377],[-0.9343487590252231,1,2.0082492914328853e-2,-0.984509166021882,0.8286797337500549,0.21662128050335924,-0.9581376821870554],[-0.2453822926744781,2.0082492914328853e-2,1,0.14273917047837595,0.5338613814695787,0.7011465554127291,-0.1365385722306464],[0.8862168778706535,-0.984509166021882,0.14273917047837595,1,-0.7349704274330299,-0.12608257766916198,0.9287830789388462],[-0.9489396513905969,0.8286797337500549,0.5338613814695787,-0.7349704274330299,1,0.4925139297135226,-0.9104412462273439],[-0.28605745392972376,0.21662128050335924,0.7011465554127291,-0.12608257766916198,0.4925139297135226,1,-0.23641945488191787],[0.9919886221303377,-0.9581376821870554,-0.1365385722306464,0.9287830789388462,-0.9104412462273439,-0.23641945488191787,1]]}],"layout":{"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmap"}],"heatmapgl":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmapgl"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"sequentialminus":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":5.0e-2},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}}}}
```
:::
:::

::: {.cell .code execution_count="37" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":542}" id="dzbU1OYWyD9n" outputId="41f2da6b-6a1d-486f-bf41-65e618eccaab"}
``` python
# Line plot for 'Trend of Energy End-use over the Years'
fig = px.line(df_overview, x='Year', y='Energy End-use (TJ)', title='Trend of Energy End-use over the Years')
fig.show()
```

::: {.output .display_data}
``` json
{"config":{"plotlyServerURL":"https://plot.ly"},"data":[{"hovertemplate":"Year=%{x}<br>Energy End-use (TJ)=%{y}<extra></extra>","legendgroup":"","line":{"color":"#636efa","dash":"solid"},"marker":{"symbol":"circle"},"mode":"lines","name":"","orientation":"v","showlegend":false,"type":"scatter","x":[2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020],"xaxis":"x","y":[281729,279524,282055,279588,283984,282960,283564,281006,282486,283527,272490],"yaxis":"y"}],"layout":{"legend":{"tracegroupgap":0},"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmap"}],"heatmapgl":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmapgl"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"sequentialminus":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":5.0e-2},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"title":{"text":"Trend of Energy End-use over the Years"},"xaxis":{"anchor":"y","domain":[0,1],"title":{"text":"Year"}},"yaxis":{"anchor":"x","domain":[0,1],"title":{"text":"Energy End-use (TJ)"}}}}
```
:::
:::

::: {.cell .code execution_count="38" id="4KJTbpcRyHgj"}
``` python
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression

X = df_overview.drop('Energy End-use (TJ)', axis=1)
y = df_overview['Energy End-use (TJ)']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

model = LinearRegression()
model.fit(X_train, y_train)

predictions = model.predict(X_test)
```
:::

::: {.cell .code execution_count="39" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="d1syfQym1ngI" outputId="7e74cf6e-1c60-48af-aff2-d7c40fce9511"}
``` python
print(predictions)
```

::: {.output .stream .stdout}
    [282930.20184256 281933.44935531 283681.35070016]
:::
:::

::: {.cell .code execution_count="42" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="zW-3YbRhyJan" outputId="5ca6a15c-d2c2-40f5-d902-d4991cfab806"}
``` python
from sklearn.metrics import mean_absolute_error, mean_squared_error

print("MAE: ", mean_absolute_error(y_test, predictions))
print("MSE: ", mean_squared_error(y_test, predictions))
print("RMSE: ", np.sqrt(mean_squared_error(y_test, predictions)))
```

::: {.output .stream .stdout}
    MAE:  129.532737636182
    MSE:  22170.535904252512
    RMSE:  148.89773639734256
:::
:::

::: {.cell .code execution_count="43" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":542}" id="4e9ZY_3ByOGD" outputId="da30f924-ca6f-4d3c-9838-dbf6dd5f2cd0"}
``` python
# Line plot for 'Trend of Energy End-use and GDP over the Years'
fig = go.Figure()
fig.add_trace(go.Scatter(x=df_overview['Year'], y=df_overview['Energy End-use (TJ)'], mode='lines', name='Energy End-use'))
fig.add_trace(go.Scatter(x=df_overview['Year'], y=df_overview['GDP in Hong Kong in chained 2020 HKD (HK$ million)'], mode='lines', name='GDP'))
fig.show()
```

::: {.output .display_data}
``` json
{"config":{"plotlyServerURL":"https://plot.ly"},"data":[{"mode":"lines","name":"Energy End-use","type":"scatter","x":[2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020],"y":[281729,279524,282055,279588,283984,282960,283564,281006,282486,283527,272490]},{"mode":"lines","name":"GDP","type":"scatter","x":[2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020],"y":[2308742,2419901,2461047,2537377,2607470,2669732,2727810,2831361,2911968,2863098,2675708]}],"layout":{"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmap"}],"heatmapgl":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmapgl"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"sequentialminus":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":5.0e-2},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}}}}
```
:::
:::

::: {.cell .code execution_count="44" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":542}" id="pjFGE4dcyPp6" outputId="55279ccf-d2d4-47fb-83a1-6502f3d8fd71"}
``` python
# Grouped bar plot for 'Proportion of Different Fuels Used in Residential Sector Over the Years'
df_melted = pd.melt(df_residential_fuel, id_vars='Year', value_vars=['Town Gas & Liquefied Petroleum Gas (Unit : Terajoule)', 'Oil & Coal Products (Unit : Terajoule)', 'Electricity (Unit : Terajoule)'])
fig = px.bar(df_melted, x='Year', y='value', color='variable', title='Proportion of Different Fuels Used in Residential Sector Over the Years', labels={'value':'Energy Consumption (TJ)', 'variable':'Fuel Type'})
fig.show()
```

::: {.output .display_data}
``` json
{"config":{"plotlyServerURL":"https://plot.ly"},"data":[{"alignmentgroup":"True","hovertemplate":"Fuel Type=Town Gas & Liquefied Petroleum Gas (Unit : Terajoule)<br>Year=%{x}<br>Energy Consumption (TJ)=%{y}<extra></extra>","legendgroup":"Town Gas & Liquefied Petroleum Gas (Unit : Terajoule)","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"Town Gas & Liquefied Petroleum Gas (Unit : Terajoule)","offsetgroup":"Town Gas & Liquefied Petroleum Gas (Unit : Terajoule)","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020],"xaxis":"x","y":[19038,18977,18841,18635,18681,18063,18574,18335,19578,18070,19726],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"Fuel Type=Oil & Coal Products (Unit : Terajoule)<br>Year=%{x}<br>Energy Consumption (TJ)=%{y}<extra></extra>","legendgroup":"Oil & Coal Products (Unit : Terajoule)","marker":{"color":"#EF553B","pattern":{"shape":""}},"name":"Oil & Coal Products (Unit : Terajoule)","offsetgroup":"Oil & Coal Products (Unit : Terajoule)","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020],"xaxis":"x","y":[13,8,8,7,7,8,10,14,14,15,15],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"Fuel Type=Electricity (Unit : Terajoule)<br>Year=%{x}<br>Energy Consumption (TJ)=%{y}<extra></extra>","legendgroup":"Electricity (Unit : Terajoule)","marker":{"color":"#00cc96","pattern":{"shape":""}},"name":"Electricity (Unit : Terajoule)","offsetgroup":"Electricity (Unit : Terajoule)","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020],"xaxis":"x","y":[39344,39872,41189,39941,43415,42368,43120,42127,41965,42937,46675],"yaxis":"y"}],"layout":{"barmode":"relative","legend":{"title":{"text":"Fuel Type"},"tracegroupgap":0},"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmap"}],"heatmapgl":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmapgl"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"sequentialminus":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":5.0e-2},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"title":{"text":"Proportion of Different Fuels Used in Residential Sector Over the Years"},"xaxis":{"anchor":"y","domain":[0,1],"title":{"text":"Year"}},"yaxis":{"anchor":"x","domain":[0,1],"title":{"text":"Energy Consumption (TJ)"}}}}
```
:::
:::

::: {.cell .code execution_count="45" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":542}" id="dhcThP5PyRbk" outputId="42f84e2b-226c-4b93-edc3-2f3e580dfb3a"}
``` python
# Line plot for 'Energy Consumption by Sector'
fig = go.Figure()
fig.add_trace(go.Scatter(x=df_energy_sector['Year'], y=df_energy_sector['Residential (Unit : Terajoule)'], mode='lines', name='Residential'))
fig.add_trace(go.Scatter(x=df_energy_sector['Year'], y=df_energy_sector['Commercial (Unit : Terajoule)'], mode='lines', name='Commercial'))
fig.add_trace(go.Scatter(x=df_energy_sector['Year'], y=df_energy_sector['Industrial (Unit : Terajoule)'], mode='lines', name='Industrial'))
fig.add_trace(go.Scatter(x=df_energy_sector['Year'], y=df_energy_sector['Transport (Unit : Terajoule)'], mode='lines', name='Transport'))
fig.update_layout(title='Energy Consumption by Sector', xaxis_title='Year', yaxis_title='Energy Consumption (TJ)')
fig.show()
```

::: {.output .display_data}
``` json
{"config":{"plotlyServerURL":"https://plot.ly"},"data":[{"mode":"lines","name":"Residential","type":"scatter","x":[2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020],"y":[58396,58857,60037,58582,62103,60439,61704,60476,61557,61022,66416]},{"mode":"lines","name":"Commercial","type":"scatter","x":[2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020],"y":[116391,116013,118330,118209,119617,120419,120460,120410,122222,123005,114513]},{"mode":"lines","name":"Industrial","type":"scatter","x":[2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020],"y":[16053,14155,13655,13204,13028,13054,12294,12722,12829,12274,12162]},{"mode":"lines","name":"Transport","type":"scatter","x":[2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020],"y":[90889,90498,90033,89593,89236,89049,89105,87397,85878,87225,79399]}],"layout":{"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmap"}],"heatmapgl":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmapgl"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"sequentialminus":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":5.0e-2},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"title":{"text":"Energy Consumption by Sector"},"xaxis":{"title":{"text":"Year"}},"yaxis":{"title":{"text":"Energy Consumption (TJ)"}}}}
```
:::
:::

::: {.cell .code execution_count="46" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":542}" id="5SRBoq2ZyVd8" outputId="a8990669-98a7-4418-c1b2-973afc911c90"}
``` python
# Line plot for 'Electricity Consumption by End-use'
fig = go.Figure()
fig.add_trace(go.Scatter(x=df_electricity_enduse['Year'], y=df_electricity_enduse['Air Conditioning (Unit : Terajoule)'], mode='lines', name='Air Conditioning'))
fig.add_trace(go.Scatter(x=df_electricity_enduse['Year'], y=df_electricity_enduse['Lighting (Unit : Terajoule)'], mode='lines', name='Lighting'))
fig.add_trace(go.Scatter(x=df_electricity_enduse['Year'], y=df_electricity_enduse['Refrigeration (Unit : Terajoule)'], mode='lines', name='Refrigeration'))
fig.update_layout(title='Electricity Consumption by End-use', xaxis_title='Year', yaxis_title='Electricity Consumption (TJ)')
fig.show()
```

::: {.output .display_data}
``` json
{"config":{"plotlyServerURL":"https://plot.ly"},"data":[{"mode":"lines","name":"Air Conditioning","type":"scatter","x":[2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020],"y":[45511,44605,45079,43821,47264,46927,46441,46396,48032,47965,48622]},{"mode":"lines","name":"Lighting","type":"scatter","x":[2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020],"y":[19563,18357,18524,17774,17365,16914,16385,16026,16255,16094,15786]},{"mode":"lines","name":"Refrigeration","type":"scatter","x":[2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020],"y":[9213,8117,7723,6886,6549,5812,5176,4454,4292,4363,4492]}],"layout":{"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmap"}],"heatmapgl":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmapgl"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"sequentialminus":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":5.0e-2},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"title":{"text":"Electricity Consumption by End-use"},"xaxis":{"title":{"text":"Year"}},"yaxis":{"title":{"text":"Electricity Consumption (TJ)"}}}}
```
:::
:::

::: {.cell .code execution_count="47" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":542}" id="sBz2xVWNyXEA" outputId="b057b4eb-67af-4d35-a5ee-781cd3cbee6b"}
``` python
# Pie chart for 'Proportion of Different Types of Renewable Energy'
fig = go.Figure(data=[go.Pie(labels=df_energy_renewable['Type of Renewable Energy'].values, values=df_energy_renewable['Renewable Energy (Unit : Terajoule)'].values)])
fig.update_layout(title_text='Proportion of Different Types of Renewable Energy')
fig.show()
```

::: {.output .display_data}
``` json
{"config":{"plotlyServerURL":"https://plot.ly"},"data":[{"labels":["Waste-to-energy","Wind Energy & Hydropower","Solar Energy","Bio-diesel"],"type":"pie","values":[1930,9,189,276]}],"layout":{"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmap"}],"heatmapgl":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmapgl"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"sequentialminus":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":5.0e-2},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"title":{"text":"Proportion of Different Types of Renewable Energy"}}}
```
:::
:::
