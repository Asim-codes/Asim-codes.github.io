---
jupyter:
  colab:
  kernelspec:
    display_name: Python 3
    name: python3
  language_info:
    codemirror_mode:
      name: ipython
      version: 3
    file_extension: .py
    mimetype: text/x-python
    name: python
    nbconvert_exporter: python
    pygments_lexer: ipython3
    version: 3.12.0
  nbformat: 4
  nbformat_minor: 0
---

<div class="cell markdown" id="9VRaNYoVavoP">

**Overview \[Key Energy End-use\]**

</div>

<div class="cell code" execution_count="41"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="-N2YCKy8Uu2P" outputId="6a8b775b-012b-4fc2-e410-9f72d07142c1">

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

<div class="output stream stdout">

    Data read successfully.

</div>

</div>

<div class="cell code" execution_count="2"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:446}"
id="Oe9JaKtwWizA" outputId="b916c012-3f08-4456-949e-614fe8ec498d">

``` python
df_overview
```

<div class="output execute_result" execution_count="2">

        Year  Energy End-use (TJ)/ GDP (HK$ billion)  Energy End-use (TJ)  \
    0   2010                                     122               281729   
    1   2011                                     116               279524   
    2   2012                                     115               282055   
    3   2013                                     110               279588   
    4   2014                                     109               283984   
    5   2015                                     106               282960   
    6   2016                                     104               283564   
    7   2017                                      99               281006   
    8   2018                                      97               282486   
    9   2019                                      99               283527   
    10  2020                                     102               272490   

        GDP in Hong Kong in chained 2020 HKD (HK$ million)  \
    0                                             2308742    
    1                                             2419901    
    2                                             2461047    
    3                                             2537377    
    4                                             2607470    
    5                                             2669732    
    6                                             2727810    
    7                                             2831361    
    8                                             2911968    
    9                                             2863098    
    10                                            2675708    

        Energy End-use/ Capita (GJ)  Electricity/ Capita (GJ)  Population ('000)  
    0                         40.11                     21.48               7024  
    1                         39.53                     21.44               7072  
    2                         39.45                     21.69               7150  
    3                         38.95                     21.36               7179  
    4                         39.28                     21.88               7230  
    5                         38.81                     21.72               7291  
    6                         38.65                     21.65               7337  
    7                         38.01                     21.37               7393  
    8                         37.90                     21.40               7453  
    9                         37.76                     21.53               7508  
    10                        36.42                     21.27               7481  

</div>

</div>

<div class="cell markdown" id="DLTM6Cita8LO">

**Total Energy Consumption by fuel**

</div>

<div class="cell code" execution_count="3"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="deg27nosXXq4" outputId="c623edd7-cad5-4ac3-c97f-a3980314e25b">

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

<div class="output stream stdout">

    Data read successfully.

</div>

</div>

<div class="cell code" execution_count="4"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:464}"
id="7iv8_nTgXffA" outputId="77e01185-3829-4868-945e-9c3a3765d770">

``` python
df_total_fuel
```

<div class="output execute_result" execution_count="4">

        Year  Town Gas & Liquefied Petroleum Gas (Unit : Terajoule)  \
    0   2010                                              49084       
    1   2011                                              49568       
    2   2012                                              49616       
    3   2013                                              49723       
    4   2014                                              50844       
    5   2015                                              48954       
    6   2016                                              49374       
    7   2017                                              47907       
    8   2018                                              48541       
    9   2019                                              47338       
    10  2020                                              44195       

        Town Gas & Liquefied Petroleum Gas Percentage (%)  \
    0                                                  17   
    1                                                  18   
    2                                                  18   
    3                                                  18   
    4                                                  18   
    5                                                  17   
    6                                                  17   
    7                                                  17   
    8                                                  17   
    9                                                  17   
    10                                                 16   

        Oil & Coal Products (Unit : Terajoule)  \
    0                                    81786   
    1                                    78349   
    2                                    77359   
    3                                    76503   
    4                                    74992   
    5                                    75626   
    6                                    75349   
    7                                    75121   
    8                                    74452   
    9                                    74520   
    10                                   69195   

        Oil & Coal Products Percentage (%)  Electricity (Unit : Terajoule)  \
    0                                   29                          150859   
    1                                   28                          151606   
    2                                   27                          155080   
    3                                   27                          153362   
    4                                   26                          158148   
    5                                   27                          158380   
    6                                   27                          158841   
    7                                   27                          157977   
    8                                   26                          159494   
    9                                   26                          161669   
    10                                  25                          159100   

        Electricity Percentage (%)  
    0                           54  
    1                           54  
    2                           55  
    3                           55  
    4                           56  
    5                           56  
    6                           56  
    7                           56  
    8                           56  
    9                           57  
    10                          58  

</div>

</div>

<div class="cell markdown" id="zk9r4KhSbDD_">

**Energy Consumption in Residential Sector by Fuel**

</div>

<div class="cell code" execution_count="5"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="cFwJ5b1xXyXw" outputId="301d5f8c-c4a8-4cce-b4e1-14e3b129d9a9">

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

<div class="output stream stdout">

    Data read successfully.

</div>

</div>

<div class="cell code" execution_count="6"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:464}"
id="yEgoGVWuY1-j" outputId="840cb113-c606-4089-864e-193fd35a57c7">

``` python
df_residential_fuel
```

<div class="output execute_result" execution_count="6">

        Year  Town Gas & Liquefied Petroleum Gas (Unit : Terajoule)  \
    0   2010                                              19038       
    1   2011                                              18977       
    2   2012                                              18841       
    3   2013                                              18635       
    4   2014                                              18681       
    5   2015                                              18063       
    6   2016                                              18574       
    7   2017                                              18335       
    8   2018                                              19578       
    9   2019                                              18070       
    10  2020                                              19726       

        Town Gas & Liquefied Petroleum Gas Percentage (%)  \
    0                                                  33   
    1                                                  32   
    2                                                  31   
    3                                                  32   
    4                                                  30   
    5                                                  30   
    6                                                  30   
    7                                                  30   
    8                                                  32   
    9                                                  30   
    10                                                 30   

        Oil & Coal Products (Unit : Terajoule)  \
    0                                       13   
    1                                        8   
    2                                        8   
    3                                        7   
    4                                        7   
    5                                        8   
    6                                       10   
    7                                       14   
    8                                       14   
    9                                       15   
    10                                      15   

        Oil & Coal Products Percentage (%)  Electricity (Unit : Terajoule)  \
    0                                    0                           39344   
    1                                    0                           39872   
    2                                    0                           41189   
    3                                    0                           39941   
    4                                    0                           43415   
    5                                    0                           42368   
    6                                    0                           43120   
    7                                    0                           42127   
    8                                    0                           41965   
    9                                    0                           42937   
    10                                   0                           46675   

        Electricity Percentage (%)  
    0                           67  
    1                           68  
    2                           69  
    3                           68  
    4                           70  
    5                           70  
    6                           70  
    7                           70  
    8                           68  
    9                           70  
    10                          70  

</div>

</div>

<div class="cell markdown" id="pmfnzkJ0bRU-">

**Energy Consumption in Commercial Sector by Fuel**

</div>

<div class="cell code" execution_count="7"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="k8G4qW9jbJv5" outputId="ca250cfa-d143-488c-e0e2-21787b9520bd">

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

<div class="output stream stdout">

    Data read successfully.

</div>

</div>

<div class="cell code" execution_count="8"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:464}"
id="qhMGEywdbig-" outputId="613bd796-2182-45e1-d34f-5711a15861de">

``` python
df_commercial_fuel
```

<div class="output execute_result" execution_count="8">

        Year  Town Gas & Liquefied Petroleum Gas (Unit : Terajoule)  \
    0   2010                                              13971       
    1   2011                                              14129       
    2   2012                                              14280       
    3   2013                                              14512       
    4   2014                                              14713       
    5   2015                                              14535       
    6   2016                                              14601       
    7   2017                                              14908       
    8   2018                                              15253       
    9   2019                                              14440       
    10  2020                                              11844       

        Town Gas & Liquefied Petroleum Gas Percentage (%)  \
    0                                                  12   
    1                                                  12   
    2                                                  12   
    3                                                  12   
    4                                                  12   
    5                                                  12   
    6                                                  12   
    7                                                  12   
    8                                                  12   
    9                                                  12   
    10                                                 10   

        Oil & Coal Products (Unit : Terajoule)  \
    0                                     4526   
    1                                     1979   
    2                                     1696   
    3                                     1477   
    4                                     1431   
    5                                     1235   
    6                                     1019   
    7                                      830   
    8                                      675   
    9                                      574   
    10                                     498   

        Oil & Coal Products Percentage (%)  Electricity (Unit : Terajoule)  \
    0                                    4                           97894   
    1                                    2                           99905   
    2                                    1                          102353   
    3                                    1                          102221   
    4                                    1                          103473   
    5                                    1                          104649   
    6                                    1                          104841   
    7                                    1                          104672   
    8                                    1                          106294   
    9                                    0                          107992   
    10                                   0                          102171   

        Electricity Percentage (%)  
    0                           84  
    1                           86  
    2                           86  
    3                           86  
    4                           87  
    5                           87  
    6                           87  
    7                           87  
    8                           87  
    9                           88  
    10                          89  

</div>

</div>

<div class="cell markdown" id="Cq7CNZgjbnz-">

**Energy Consumption in Industrial Sector by Fuel**

</div>

<div class="cell code" execution_count="9"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="RL39OsFpbu_l" outputId="7ce52e24-58d2-45cc-dbed-10654df9cd17">

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

<div class="output stream stdout">

    Data read successfully.

</div>

</div>

<div class="cell code" execution_count="10"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:464}"
id="WHp0AVOgb9M4" outputId="030f8864-87f4-4f6d-fb3c-d83760122be6">

``` python
df_industrial_fuel
```

<div class="output execute_result" execution_count="10">

        Year  Town Gas & Liquefied Petroleum Gas (Unit : Terajoule)  \
    0   2010                                                937       
    1   2011                                                956       
    2   2012                                               1111       
    3   2013                                               1229       
    4   2014                                               1264       
    5   2015                                               1308       
    6   2016                                               1232       
    7   2017                                               1317       
    8   2018                                               1448       
    9   2019                                               1596       
    10  2020                                               1470       

        Town Gas & Liquefied Petroleum Gas Percentage (%)  \
    0                                                   6   
    1                                                   7   
    2                                                   8   
    3                                                   9   
    4                                                  10   
    5                                                  10   
    6                                                  10   
    7                                                  10   
    8                                                  11   
    9                                                  13   
    10                                                 12   

        Oil & Coal Products (Unit : Terajoule)  \
    0                                     4035   
    1                                     3978   
    2                                     3728   
    3                                     3571   
    4                                     3389   
    5                                     3386   
    6                                     3190   
    7                                     3442   
    8                                     3443   
    9                                     3177   
    10                                    3309   

        Oil & Coal Products Percentage (%)  Electricity (Unit : Terajoule)  \
    0                                   25                           11082   
    1                                   28                            9220   
    2                                   27                            8816   
    3                                   27                            8405   
    4                                   26                            8374   
    5                                   26                            8359   
    6                                   26                            7872   
    7                                   27                            7963   
    8                                   27                            7938   
    9                                   26                            7501   
    10                                  27                            7383   

        Electricity Percentage (%)  
    0                           69  
    1                           65  
    2                           65  
    3                           64  
    4                           64  
    5                           64  
    6                           64  
    7                           63  
    8                           62  
    9                           61  
    10                          61  

</div>

</div>

<div class="cell markdown" id="HwTqMq5AcD3_">

**Energy Consumption in Transport Sector by Fuel**

</div>

<div class="cell code" execution_count="11"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="IcnePoL8cQ3d" outputId="158315b6-3061-4ddf-dc3d-d76cecabf43f">

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

<div class="output stream stdout">

    Data read successfully.

</div>

</div>

<div class="cell code" execution_count="12"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:464}"
id="jZ5QoWgactxu" outputId="a5ba9727-efb1-4f32-c574-9514d196d345">

``` python
df_transport_fuel
```

<div class="output execute_result" execution_count="12">

        Year  Town Gas & Liquefied Petroleum Gas (Unit : Terajoule)  \
    0   2010                                              15137       
    1   2011                                              15506       
    2   2012                                              15384       
    3   2013                                              15348       
    4   2014                                              16185       
    5   2015                                              15048       
    6   2016                                              14967       
    7   2017                                              13347       
    8   2018                                              12262       
    9   2019                                              13232       
    10  2020                                              11155       

        Town Gas & Liquefied Petroleum Gas Percentage (%)  \
    0                                                  17   
    1                                                  17   
    2                                                  17   
    3                                                  17   
    4                                                  18   
    5                                                  17   
    6                                                  17   
    7                                                  15   
    8                                                  14   
    9                                                  15   
    10                                                 14   

        Oil & Coal Products (Unit : Terajoule)  \
    0                                    73213   
    1                                    72383   
    2                                    71927   
    3                                    71449   
    4                                    70165   
    5                                    70997   
    6                                    71130   
    7                                    70835   
    8                                    70320   
    9                                    70754   
    10                                   65373   

        Oil & Coal Products Percentage (%)  Electricity (Unit : Terajoule)  \
    0                                   81                            2540   
    1                                   80                            2609   
    2                                   80                            2722   
    3                                   80                            2796   
    4                                   79                            2886   
    5                                   80                            3004   
    6                                   80                            3008   
    7                                   81                            3215   
    8                                   82                            3297   
    9                                   81                            3239   
    10                                  82                            2871   

        Electricity Percentage (%)  
    0                            3  
    1                            3  
    2                            3  
    3                            3  
    4                            3  
    5                            3  
    6                            3  
    7                            4  
    8                            4  
    9                            4  
    10                           4  

</div>

</div>

<div class="cell markdown" id="pq7W7ohac05j">

**Total Energy Consumption by Sector**

</div>

<div class="cell code" execution_count="13"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="MOX3BsL8c8V9" outputId="b9fb12ee-fec1-4886-b4f7-196acec67031">

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

<div class="output stream stdout">

    Data read successfully.

</div>

</div>

<div class="cell code" execution_count="14"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:449}"
id="oHku9q38dfnJ" outputId="d9fee852-9e94-401a-9772-a1db11fa4730">

``` python
df_energy_sector
```

<div class="output execute_result" execution_count="14">

        Year  Residential (Unit : Terajoule)  Residential Percentage (%)  \
    0   2010                           58396                          21   
    1   2011                           58857                          21   
    2   2012                           60037                          21   
    3   2013                           58582                          21   
    4   2014                           62103                          22   
    5   2015                           60439                          21   
    6   2016                           61704                          22   
    7   2017                           60476                          22   
    8   2018                           61557                          22   
    9   2019                           61022                          22   
    10  2020                           66416                          24   

        Commercial (Unit : Terajoule)  Commercial Percentage (%)  \
    0                          116391                         41   
    1                          116013                         42   
    2                          118330                         42   
    3                          118209                         42   
    4                          119617                         42   
    5                          120419                         43   
    6                          120460                         42   
    7                          120410                         43   
    8                          122222                         43   
    9                          123005                         43   
    10                         114513                         42   

        Industrial (Unit : Terajoule)  Industrial Percentage (%)  \
    0                           16053                          6   
    1                           14155                          5   
    2                           13655                          5   
    3                           13204                          5   
    4                           13028                          5   
    5                           13054                          5   
    6                           12294                          4   
    7                           12722                          5   
    8                           12829                          5   
    9                           12274                          4   
    10                          12162                          4   

        Transport (Unit : Terajoule)  Transport Percentage (%)  
    0                          90889                        32  
    1                          90498                        32  
    2                          90033                        32  
    3                          89593                        32  
    4                          89236                        31  
    5                          89049                        31  
    6                          89105                        31  
    7                          87397                        31  
    8                          85878                        30  
    9                          87225                        31  
    10                         79399                        29  

</div>

</div>

<div class="cell markdown" id="6ihcYJ8meIEf">

**Electricity Consumption by Sector**

</div>

<div class="cell code" execution_count="15"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="SpHbF6HXeHxA" outputId="68f8acb0-20fd-4074-be92-695b0e24bdd3">

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

<div class="output stream stdout">

    Data read successfully.

</div>

</div>

<div class="cell code" execution_count="16"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:449}"
id="AX3KoCIpeW_f" outputId="12280e7c-7328-4d9c-d0c9-020bb8b14361">

``` python
df_electricity_sector
```

<div class="output execute_result" execution_count="16">

        Year  Residential (Unit : Terajoule)  Residential Percentage (%)  \
    0   2010                           39344                          26   
    1   2011                           39872                          26   
    2   2012                           41189                          27   
    3   2013                           39941                          26   
    4   2014                           43415                          27   
    5   2015                           42368                          27   
    6   2016                           43120                          27   
    7   2017                           42127                          27   
    8   2018                           41965                          26   
    9   2019                           42937                          27   
    10  2020                           46675                          29   

        Commercial (Unit : Terajoule)  Commercial Percentage (%)  \
    0                           97894                         65   
    1                           99905                         66   
    2                          102353                         66   
    3                          102221                         67   
    4                          103473                         65   
    5                          104649                         66   
    6                          104841                         66   
    7                          104672                         66   
    8                          106294                         67   
    9                          107992                         67   
    10                         102171                         64   

        Industrial (Unit : Terajoule)  Industrial Percentage (%)  \
    0                           11082                          7   
    1                            9220                          6   
    2                            8816                          6   
    3                            8405                          5   
    4                            8374                          5   
    5                            8359                          5   
    6                            7872                          5   
    7                            7963                          5   
    8                            7938                          5   
    9                            7501                          5   
    10                           7383                          5   

        Transport (Unit : Terajoule)  Transport Percentage (%)  
    0                           2540                         2  
    1                           2609                         2  
    2                           2722                         2  
    3                           2796                         2  
    4                           2886                         2  
    5                           3004                         2  
    6                           3008                         2  
    7                           3215                         2  
    8                           3297                         2  
    9                           3239                         2  
    10                          2871                         2  

</div>

</div>

<div class="cell markdown" id="OfOe2xWifqqa">

**Oil & Coal Products Consumption by Sector**

</div>

<div class="cell code" execution_count="17"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="OmNOfSlNfnvE" outputId="18212ff3-1aad-438b-ad80-47a039695336">

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

<div class="output stream stdout">

    Data read successfully.

</div>

</div>

<div class="cell code" execution_count="18"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:449}"
id="m27XOACZiIVs" outputId="054d3ec3-bde8-4ee3-f173-61e9769c4c9f">

``` python
df_oilcoal_sector
```

<div class="output execute_result" execution_count="18">

        Year  Residential (Unit : Terajoule)  Residential Percentage (%)  \
    0   2010                              13                           0   
    1   2011                               8                           0   
    2   2012                               8                           0   
    3   2013                               7                           0   
    4   2014                               7                           0   
    5   2015                               8                           0   
    6   2016                              10                           0   
    7   2017                              14                           0   
    8   2018                              14                           0   
    9   2019                              15                           0   
    10  2020                              15                           0   

        Commercial (Unit : Terajoule)  Commercial Percentage (%)  \
    0                            4526                          6   
    1                            1979                          3   
    2                            1696                          2   
    3                            1477                          2   
    4                            1431                          2   
    5                            1235                          2   
    6                            1019                          1   
    7                             830                          1   
    8                             675                          1   
    9                             574                          1   
    10                            498                          1   

        Industrial (Unit : Terajoule)  Industrial Percentage (%)  \
    0                            4035                          5   
    1                            3978                          5   
    2                            3728                          5   
    3                            3571                          5   
    4                            3389                          5   
    5                            3386                          4   
    6                            3190                          4   
    7                            3442                          5   
    8                            3443                          5   
    9                            3177                          4   
    10                           3309                          5   

        Transport (Unit : Terajoule)  Transport Percentage (%)  
    0                          73213                        90  
    1                          72383                        92  
    2                          71927                        93  
    3                          71449                        93  
    4                          70165                        94  
    5                          70997                        94  
    6                          71130                        94  
    7                          70835                        94  
    8                          70320                        94  
    9                          70754                        95  
    10                         65373                        94  

</div>

</div>

<div class="cell markdown" id="8Z-dZarWf9Ok">

**Town Gas & LPG Consumption by Sector**

</div>

<div class="cell code" execution_count="19"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="vgiU8WHmfonI" outputId="5b1da677-bce3-469a-ecde-537b0a1dd193">

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

<div class="output stream stdout">

    Data read successfully.

</div>

</div>

<div class="cell code" execution_count="20"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:449}"
id="DaXxkCQmiKaU" outputId="04661e59-dc7d-40ba-defb-68c618b102f8">

``` python
df_gaslpg_sector
```

<div class="output execute_result" execution_count="20">

        Year  Residential (Unit : Terajoule)  Residential Percentage (%)  \
    0   2010                           19038                          39   
    1   2011                           18977                          38   
    2   2012                           18841                          38   
    3   2013                           18635                          37   
    4   2014                           18681                          37   
    5   2015                           18063                          37   
    6   2016                           18574                          38   
    7   2017                           18335                          38   
    8   2018                           19578                          40   
    9   2019                           18070                          38   
    10  2020                           19726                          45   

        Commercial (Unit : Terajoule)  Commercial Percentage (%)  \
    0                           13971                         28   
    1                           14129                         29   
    2                           14280                         29   
    3                           14512                         29   
    4                           14713                         29   
    5                           14535                         30   
    6                           14601                         30   
    7                           14908                         31   
    8                           15253                         31   
    9                           14440                         31   
    10                          11844                         27   

        Industrial (Unit : Terajoule)  Industrial Percentage (%)  \
    0                             937                          2   
    1                             956                          2   
    2                            1111                          2   
    3                            1229                          2   
    4                            1264                          2   
    5                            1308                          3   
    6                            1232                          2   
    7                            1317                          3   
    8                            1448                          3   
    9                            1596                          3   
    10                           1470                          3   

        Transport (Unit : Terajoule)  Transport Percentage (%)  
    0                          15137                        31  
    1                          15506                        31  
    2                          15384                        31  
    3                          15348                        31  
    4                          16185                        32  
    5                          15048                        31  
    6                          14967                        30  
    7                          13347                        28  
    8                          12262                        25  
    9                          13232                        28  
    10                         11155                        25  

</div>

</div>

<div class="cell markdown" id="PP_DUbfigAk8">

**Total Energy Consumption by End-use**

</div>

<div class="cell code" execution_count="21"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="pMwdqEZYfpZk" outputId="715f0b63-1bb1-4bc9-b387-4db79624bd8d">

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

<div class="output stream stdout">

    Data read successfully.

</div>

</div>

<div class="cell code" execution_count="22"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:513}"
id="fJGHjDr-iM3B" outputId="0c98b8ab-d837-4b1f-f1fa-1c9ee13cb423">

``` python
df_energy_enduse
```

<div class="output execute_result" execution_count="22">

        Year  Air Conditioning (Unit : Terajoule)  \
    0   2010                                45511   
    1   2011                                44617   
    2   2012                                45091   
    3   2013                                43834   
    4   2014                                47277   
    5   2015                                46940   
    6   2016                                46455   
    7   2017                                46410   
    8   2018                                48047   
    9   2019                                47979   
    10  2020                                48634   

        Air Conditioning Percentage (%)  Cooking (Unit : Terajoule)  \
    0                                16                       33379   
    1                                16                       30830   
    2                                16                       30876   
    3                                16                       32205   
    4                                17                       32578   
    5                                17                       32461   
    6                                16                       33208   
    7                                17                       33510   
    8                                17                       34947   
    9                                17                       32871   
    10                               18                       29668   

        Cooking Percentage (%)  Industrial Process/ Equipment (Unit : Terajoule)  \
    0                       12                                             18620   
    1                       11                                             15452   
    2                       11                                             15514   
    3                       12                                             15595   
    4                       11                                             15722   
    5                       11                                             15857   
    6                       12                                             15127   
    7                       12                                             15591   
    8                       12                                             15779   
    9                       12                                             15107   
    10                      11                                             14467   

        Industrial Process/ Equipment Percentage (%)  Lighting (Unit : Terajoule)  \
    0                                              7                        19563   
    1                                              6                        18357   
    2                                              6                        18524   
    3                                              6                        17774   
    4                                              6                        17365   
    5                                              6                        16914   
    6                                              5                        16385   
    7                                              6                        16026   
    8                                              6                        16255   
    9                                              5                        16094   
    10                                             5                        15786   

        Lighting Percentage (%)  Office Equipment (Unit : Terajoule)  ...  \
    0                         7                                11758  ...   
    1                         7                                12313  ...   
    2                         7                                12896  ...   
    3                         6                                11825  ...   
    4                         6                                11583  ...   
    5                         6                                11026  ...   
    6                         6                                10709  ...   
    7                         6                                10233  ...   
    8                         6                                10412  ...   
    9                         6                                10534  ...   
    10                        6                                10605  ...   

        Bus (Unit : Terajoule)  Bus Percentage (%)  Taxi (Unit : Terajoule)  \
    0                    18842                   7                    13373   
    1                    18911                   7                    13593   
    2                    19128                   7                    13469   
    3                    19144                   7                    13319   
    4                    19285                   7                    13696   
    5                    19168                   7                    12437   
    6                    18918                   7                    12288   
    7                    18663                   7                    10686   
    8                    18286                   6                     9519   
    9                    18028                   6                    10463   
    10                   14811                   5                     8701   

        Taxi Percentage (%)  Car (Unit : Terajoule)  Car Percentage (%)  \
    0                     5                   18247                   6   
    1                     5                   18795                   7   
    2                     5                   19432                   7   
    3                     5                   20955                   7   
    4                     5                   20641                   7   
    5                     4                   21354                   8   
    6                     4                   22189                   8   
    7                     4                   22005                   8   
    8                     3                   22421                   8   
    9                     4                   22925                   8   
    10                    3                   22067                   8   

        Marine (Unit : Terajoule)  Marine Percentage (%)  \
    0                        8672                      3   
    1                        8245                      3   
    2                        8077                      3   
    3                        7739                      3   
    4                        7705                      3   
    5                        7792                      3   
    6                        7474                      3   
    7                        7459                      3   
    8                        7006                      2   
    9                        7342                      3   
    10                       7094                      3   

        Others (Unit : Terajoule)  Others Percentage (%)  
    0                       42031                     15  
    1                       48544                     17  
    2                       50636                     18  
    3                       50315                     18  
    4                       50956                     18  
    5                       51870                     18  
    6                       52893                     19  
    7                       41947                     15  
    8                       41172                     15  
    9                       44928                     16  
    10                      44320                     16  

    [11 rows x 29 columns]

</div>

</div>

<div class="cell markdown" id="F08745tmgIyR">

**Electricity Consumption by End-use**

</div>

<div class="cell code" execution_count="23"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="ReCtu-IXfpSU" outputId="88f2f566-6f86-4404-f3cd-3f5958ccff95">

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

<div class="output stream stdout">

    Data read successfully.

</div>

</div>

<div class="cell code" execution_count="24"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:484}"
id="mIqXu3wXiO5z" outputId="6b15f0a2-d476-4dea-9bb6-27b6dec33739">

``` python
df_electricity_enduse
```

<div class="output execute_result" execution_count="24">

        Year  Air Conditioning (Unit : Terajoule)  \
    0   2010                                45511   
    1   2011                                44605   
    2   2012                                45079   
    3   2013                                43821   
    4   2014                                47264   
    5   2015                                46927   
    6   2016                                46441   
    7   2017                                46396   
    8   2018                                48032   
    9   2019                                47965   
    10  2020                                48622   

        Air Conditioning Percentage (%)  Lighting (Unit : Terajoule)  \
    0                                30                        19563   
    1                                29                        18357   
    2                                29                        18524   
    3                                29                        17774   
    4                                30                        17365   
    5                                30                        16914   
    6                                29                        16385   
    7                                29                        16026   
    8                                30                        16255   
    9                                30                        16094   
    10                               31                        15786   

        Lighting Percentage (%)  Refrigeration (Unit : Terajoule)  \
    0                        13                              9213   
    1                        12                              8117   
    2                        12                              7723   
    3                        12                              6886   
    4                        11                              6549   
    5                        11                              5812   
    6                        10                              5176   
    7                        10                              4454   
    8                        10                              4292   
    9                        10                              4363   
    10                       10                              4492   

        Refrigeration Percentage (%)  \
    0                              6   
    1                              5   
    2                              5   
    3                              4   
    4                              4   
    5                              4   
    6                              3   
    7                              3   
    8                              3   
    9                              3   
    10                             3   

        Industrial Process/ Equipment (Unit : Terajoule)  \
    0                                              10016   
    1                                               9119   
    2                                               8915   
    3                                               8837   
    4                                               8875   
    5                                               8948   
    6                                               8365   
    7                                               8322   
    8                                               8365   
    9                                               7869   
    10                                              7391   

        Industrial Process/ Equipment Percentage (%)  Cooking (Unit : Terajoule)  \
    0                                              7                       11430   
    1                                              6                        9565   
    2                                              6                       10191   
    3                                              6                       12115   
    4                                              6                       13023   
    5                                              6                       13768   
    6                                              5                       14799   
    7                                              5                       15714   
    8                                              5                       16283   
    9                                              5                       15560   
    10                                             5                       13568   

        Cooking Percentage (%)  Hot Water (Unit : Terajoule)  \
    0                        8                          5015   
    1                        6                          4701   
    2                        7                          4610   
    3                        8                          5167   
    4                        8                          5946   
    5                        9                          6267   
    6                        9                          7104   
    7                       10                          7354   
    8                       10                          7561   
    9                       10                          7309   
    10                       9                          7093   

        Hot Water Percentage (%)  Office Equipment (Unit : Terajoule)  \
    0                          3                                11758   
    1                          3                                12313   
    2                          3                                12896   
    3                          3                                11825   
    4                          4                                11583   
    5                          4                                11026   
    6                          4                                10709   
    7                          5                                10233   
    8                          5                                10412   
    9                          5                                10534   
    10                         4                                10605   

        Office Equipment Percentage (%)  Vertical Transport (Unit : Terajoule)  \
    0                                 8                                    NaN   
    1                                 8                                    NaN   
    2                                 8                                    NaN   
    3                                 8                                    NaN   
    4                                 7                                    NaN   
    5                                 7                                    NaN   
    6                                 7                                    NaN   
    7                                 6                                10313.0   
    8                                 7                                10073.0   
    9                                 7                                 9566.0   
    10                                7                                 9417.0   

        Vertical Transport Percentage (%)  Others (Unit : Terajoule)  \
    0                                 NaN                      38354   
    1                                 NaN                      44829   
    2                                 NaN                      47143   
    3                                 NaN                      46939   
    4                                 NaN                      47542   
    5                                 NaN                      48719   
    6                                 NaN                      49861   
    7                                 7.0                      39166   
    8                                 6.0                      38220   
    9                                 6.0                      42410   
    10                                6.0                      42126   

        Others Percentage (%)  
    0                      25  
    1                      30  
    2                      30  
    3                      31  
    4                      30  
    5                      31  
    6                      31  
    7                      25  
    8                      24  
    9                      26  
    10                     26  

</div>

</div>

<div class="cell markdown" id="z25crRbsgPwT">

**Oil & Coal Products Consumption by End-use**

</div>

<div class="cell code" execution_count="25"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="egZDZ0qogNvO" outputId="8b5252e1-1863-48f2-9de7-e8b3d165038c">

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

<div class="output stream stdout">

    Data read successfully.

</div>

</div>

<div class="cell code" execution_count="26"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:484}"
id="g3JKRqf4iYpw" outputId="fe44fd1f-dafc-4709-ccf1-ff99ef4a027f">

``` python
df_oilcoal_enduse
```

<div class="output execute_result" execution_count="26">

        Year  Goods Vehicle (Unit : Terajoule)  Goods Vehicle Percentage (%)  \
    0   2010                             28585                            35   
    1   2011                             27818                            36   
    2   2012                             26681                            34   
    3   2013                             25126                            33   
    4   2014                             24510                            33   
    5   2015                             24782                            33   
    6   2016                             24718                            33   
    7   2017                             24845                            33   
    8   2018                             24837                            33   
    9   2019                             24735                            33   
    10  2020                             23261                            34   

        Bus (Unit : Terajoule)  Bus Percentage (%)  Taxi (Unit : Terajoule)  \
    0                    17077                  21                      1.0   
    1                    16997                  22                      1.0   
    2                    17212                  22                      1.0   
    3                    17114                  22                      1.0   
    4                    16795                  22                      1.0   
    5                    16556                  22                      1.0   
    6                    16239                  22                      NaN   
    7                    16002                  21                      NaN   
    8                    15543                  21                      NaN   
    9                    15259                  20                      NaN   
    10                   12358                  18                      NaN   

        Taxi Percentage (%)  Car (Unit : Terajoule)  Car Percentage (%)  \
    0                   0.0                   18247                  22   
    1                   0.0                   18795                  24   
    2                   0.0                   19432                  25   
    3                   0.0                   20955                  27   
    4                   0.0                   20630                  28   
    5                   0.0                   21323                  28   
    6                   NaN                   22132                  29   
    7                   NaN                   21919                  29   
    8                   NaN                   22333                  30   
    9                   NaN                   22815                  31   
    10                  NaN                   21922                  32   

        Motorcycle (Unit : Terajoule)  Motorcycle Percentage (%)  \
    0                             436                          1   
    1                             425                          1   
    2                             421                          1   
    3                             411                          1   
    4                             418                          1   
    5                             436                          1   
    6                             443                          1   
    7                             462                          1   
    8                             452                          1   
    9                             459                          1   
    10                            563                          1   

        Industrial Process/ Equipment (Unit : Terajoule)  \
    0                                               6423   
    1                                               4194   
    2                                               4067   
    3                                               3984   
    4                                               3828   
    5                                               3829   
    6                                               3604   
    7                                               3788   
    8                                               3689   
    9                                               3279   
    10                                              3409   

        Industrial Process/ Equipment Percentage (%)  Marine (Unit : Terajoule)  \
    0                                              8                       8672   
    1                                              5                       8245   
    2                                              5                       8077   
    3                                              5                       7739   
    4                                              5                       7705   
    5                                              5                       7792   
    6                                              5                       7474   
    7                                              5                       7459   
    8                                              5                       7006   
    9                                              4                       7342   
    10                                             5                       7094   

        Marine Percentage (%)  Others (Unit : Terajoule)  Others Percentage (%)  
    0                      11                       2346                      3  
    1                      11                       1875                      2  
    2                      10                       1467                      2  
    3                      10                       1173                      2  
    4                      10                       1105                      1  
    5                      10                        908                      1  
    6                      10                        739                      1  
    7                      10                        646                      1  
    8                       9                        592                      1  
    9                      10                        631                      1  
    10                     10                        588                      1  

</div>

</div>

<div class="cell markdown" id="z_YV-XUUgUwC">

**Town Gas & Liqueﬁed Petroleum Gas Consumption by End-use**

</div>

<div class="cell code" execution_count="27"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="VP35eXXZgYD5" outputId="68965cf7-76df-468e-e087-f094fc986f6f">

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

<div class="output stream stdout">

    Data read successfully.

</div>

</div>

<div class="cell code" execution_count="28"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:449}"
id="Bhw2JyvbiadJ" outputId="42b24bb7-1d65-47b8-8b60-0be862c3480f">

``` python
df_gaslpg_enduse
```

<div class="output execute_result" execution_count="28">

        Year  Cooking (Unit : Terajoule)  Cooking Percentage (%)  \
    0   2010                       21244                      43   
    1   2011                       20771                      42   
    2   2012                       20316                      41   
    3   2013                       19751                      40   
    4   2014                       19258                      38   
    5   2015                       18414                      38   
    6   2016                       18142                      37   
    7   2017                       17551                      37   
    8   2018                       18491                      38   
    9   2019                       17069                      36   
    10  2020                       15952                      36   

        Hot Water (Unit : Terajoule)  Hot Water Percentage (%)  \
    0                           8921                        18   
    1                           9232                        19   
    2                           9395                        19   
    3                           9701                        20   
    4                          10166                        20   
    5                          10276                        21   
    6                          10912                        22   
    7                          11245                        23   
    8                          11613                        24   
    9                          11090                        23   
    10                         11886                        27   

        Bus & Taxi (Unit : Terajoule)  Bus & Taxi Percentage (%)  \
    0                           15137                         31   
    1                           15505                         31   
    2                           15384                         31   
    3                           15348                         31   
    4                           16185                         32   
    5                           15048                         31   
    6                           14967                         30   
    7                           13347                         28   
    8                           12262                         25   
    9                           13232                         28   
    10                          11155                         25   

        Others (Unit : Terajoule)  Others Percentage (%)  
    0                        3782                      8  
    1                        4060                      8  
    2                        4521                      9  
    3                        4923                     10  
    4                        5236                     10  
    5                        5217                     11  
    6                        5353                     11  
    7                        5763                     12  
    8                        6175                     13  
    9                        5947                     13  
    10                       5201                     12  

</div>

</div>

<div class="cell markdown" id="PpPOhlIagbYB">

Type of Renewable Energy in Hong Kong

</div>

<div class="cell code" execution_count="29"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="xS1IJtH0ggn7" outputId="f51dac6e-f892-4ab9-c002-4f993f5ea076">

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

<div class="output stream stdout">

    Data read successfully.

</div>

</div>

<div class="cell code" execution_count="30"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:192}"
id="RVBsYpLEic1E" outputId="123e983f-10a3-4195-b3b6-c91c11efb813">

``` python
df_energy_renewable
```

<div class="output execute_result" execution_count="30">

       Type of Renewable Energy  Renewable Energy (Unit : Terajoule)  \
    0           Waste-to-energy                                 1930   
    1  Wind Energy & Hydropower                                    9   
    2              Solar Energy                                  189   
    3                Bio-diesel                                  276   

       Renewable Energy Percentage (%)  
    0                             80.3  
    1                              0.4  
    2                              7.9  
    3                             11.5  

</div>

</div>

<div class="cell markdown" id="2qlCXIXAgi-Q">

**Type of Renewable Energy in Hong Kong by Fuel**

</div>

<div class="cell code" execution_count="31"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="P9NJHKC7gmgG" outputId="e0bca0b5-7f74-43df-ee19-c2f1cfad86b1">

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

<div class="output stream stdout">

    Data read successfully.

</div>

</div>

<div class="cell code" execution_count="32"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:230}"
id="i0HMiKjAif7I" outputId="67bfb3e4-8e91-4908-ff2a-d324cb093029">

``` python
df_energy_renewable_fuel
```

<div class="output execute_result" execution_count="32">

              Type of Fuel  \
    0          Electricity   
    1       Town Gas & LPG   
    2  Oil & Coal Products   

       Weighting of Fuel in Energy End-use (Unit : Terajoule)  \
    0                                             159100        
    1                                              44195        
    2                                              69195        

       Weighting of Fuel in Energy End-use Percentage (%)  \
    0                                               58.4    
    1                                               16.2    
    2                                               25.4    

       Weighting of Renewable Energy in Respective Fuel Type (Unit :Terajoule)  \
    0                                                608                         
    1                                               1520                         
    2                                                276                         

       Weighting of Renewable Energy in Respective Fuel Type Percentage (%)  
    0                                                0.4                     
    1                                                3.4                     
    2                                                0.4                     

</div>

</div>

<div class="cell code" execution_count="33" id="N9F05D4mx5CC">

``` python
dataframes = [df_overview, df_total_fuel, df_residential_fuel, df_commercial_fuel, df_industrial_fuel,
              df_transport_fuel, df_energy_sector, df_electricity_sector, df_oilcoal_sector,
              df_gaslpg_sector, df_energy_enduse, df_electricity_enduse, df_oilcoal_enduse,
              df_gaslpg_enduse, df_energy_renewable, df_energy_renewable_fuel]
```

</div>

<div class="cell code" execution_count="34"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="l_6AkCIux7b5" outputId="f3418c2d-85d3-4fe3-96a2-06ac2bde1926">

``` python
for df in dataframes:
    print(df.shape)
```

<div class="output stream stdout">

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

</div>

</div>

<div class="cell code" execution_count="35"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="9jzfkLh1x-tO" outputId="3d2269a8-9702-49c2-fbb0-262d4be3c26a">

``` python
for df in dataframes:
    print(df.isnull().sum())
```

<div class="output stream stdout">

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

</div>

</div>

<div class="cell code" execution_count="36"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:542}"
id="L2UXxF7CyCKC" outputId="63361af0-a0e7-4a94-b278-60a48f5d651a">

``` python
import plotly.express as px
import plotly.graph_objects as go
import plotly.figure_factory as ff

# Heatmap
df_corr = df_overview.corr()
fig = go.Figure(data=go.Heatmap(z=df_corr.values.tolist(), x=df_corr.columns.tolist(), y=df_corr.columns.tolist()))
fig.show()
```

<div class="output display_data">

``` json
{"config":{"plotlyServerURL":"https://plot.ly"},"data":[{"type":"heatmap","x":["Year","Energy End-use (TJ)/ GDP (HK$ billion)","Energy End-use (TJ)","GDP in Hong Kong in chained 2020 HKD (HK$ million)","Energy End-use/ Capita (GJ)","Electricity/ Capita (GJ)","Population ('000)"],"y":["Year","Energy End-use (TJ)/ GDP (HK$ billion)","Energy End-use (TJ)","GDP in Hong Kong in chained 2020 HKD (HK$ million)","Energy End-use/ Capita (GJ)","Electricity/ Capita (GJ)","Population ('000)"],"z":[[1,-0.9343487590252231,-0.2453822926744781,0.8862168778706535,-0.9489396513905969,-0.28605745392972376,0.9919886221303377],[-0.9343487590252231,1,2.0082492914328853e-2,-0.984509166021882,0.8286797337500549,0.21662128050335924,-0.9581376821870554],[-0.2453822926744781,2.0082492914328853e-2,1,0.14273917047837595,0.5338613814695787,0.7011465554127291,-0.1365385722306464],[0.8862168778706535,-0.984509166021882,0.14273917047837595,1,-0.7349704274330299,-0.12608257766916198,0.9287830789388462],[-0.9489396513905969,0.8286797337500549,0.5338613814695787,-0.7349704274330299,1,0.4925139297135226,-0.9104412462273439],[-0.28605745392972376,0.21662128050335924,0.7011465554127291,-0.12608257766916198,0.4925139297135226,1,-0.23641945488191787],[0.9919886221303377,-0.9581376821870554,-0.1365385722306464,0.9287830789388462,-0.9104412462273439,-0.23641945488191787,1]]}],"layout":{"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmap"}],"heatmapgl":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmapgl"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"sequentialminus":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":5.0e-2},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}}}}
```

</div>

</div>

<div class="cell code" execution_count="37"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:542}"
id="dzbU1OYWyD9n" outputId="41f2da6b-6a1d-486f-bf41-65e618eccaab">

``` python
# Line plot for 'Trend of Energy End-use over the Years'
fig = px.line(df_overview, x='Year', y='Energy End-use (TJ)', title='Trend of Energy End-use over the Years')
fig.show()
```

<div class="output display_data">

``` json
{"config":{"plotlyServerURL":"https://plot.ly"},"data":[{"hovertemplate":"Year=%{x}<br>Energy End-use (TJ)=%{y}<extra></extra>","legendgroup":"","line":{"color":"#636efa","dash":"solid"},"marker":{"symbol":"circle"},"mode":"lines","name":"","orientation":"v","showlegend":false,"type":"scatter","x":[2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020],"xaxis":"x","y":[281729,279524,282055,279588,283984,282960,283564,281006,282486,283527,272490],"yaxis":"y"}],"layout":{"legend":{"tracegroupgap":0},"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmap"}],"heatmapgl":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmapgl"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"sequentialminus":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":5.0e-2},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"title":{"text":"Trend of Energy End-use over the Years"},"xaxis":{"anchor":"y","domain":[0,1],"title":{"text":"Year"}},"yaxis":{"anchor":"x","domain":[0,1],"title":{"text":"Energy End-use (TJ)"}}}}
```

</div>

</div>

<div class="cell code" execution_count="38" id="4KJTbpcRyHgj">

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

</div>

<div class="cell code" execution_count="39"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="d1syfQym1ngI" outputId="7e74cf6e-1c60-48af-aff2-d7c40fce9511">

``` python
print(predictions)
```

<div class="output stream stdout">

    [282930.20184256 281933.44935531 283681.35070016]

</div>

</div>

<div class="cell code" execution_count="42"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="zW-3YbRhyJan" outputId="5ca6a15c-d2c2-40f5-d902-d4991cfab806">

``` python
from sklearn.metrics import mean_absolute_error, mean_squared_error

print("MAE: ", mean_absolute_error(y_test, predictions))
print("MSE: ", mean_squared_error(y_test, predictions))
print("RMSE: ", np.sqrt(mean_squared_error(y_test, predictions)))
```

<div class="output stream stdout">

    MAE:  129.532737636182
    MSE:  22170.535904252512
    RMSE:  148.89773639734256

</div>

</div>

<div class="cell code" execution_count="43"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:542}"
id="4e9ZY_3ByOGD" outputId="da30f924-ca6f-4d3c-9838-dbf6dd5f2cd0">

``` python
# Line plot for 'Trend of Energy End-use and GDP over the Years'
fig = go.Figure()
fig.add_trace(go.Scatter(x=df_overview['Year'], y=df_overview['Energy End-use (TJ)'], mode='lines', name='Energy End-use'))
fig.add_trace(go.Scatter(x=df_overview['Year'], y=df_overview['GDP in Hong Kong in chained 2020 HKD (HK$ million)'], mode='lines', name='GDP'))
fig.show()
```

<div class="output display_data">

``` json
{"config":{"plotlyServerURL":"https://plot.ly"},"data":[{"mode":"lines","name":"Energy End-use","type":"scatter","x":[2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020],"y":[281729,279524,282055,279588,283984,282960,283564,281006,282486,283527,272490]},{"mode":"lines","name":"GDP","type":"scatter","x":[2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020],"y":[2308742,2419901,2461047,2537377,2607470,2669732,2727810,2831361,2911968,2863098,2675708]}],"layout":{"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmap"}],"heatmapgl":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmapgl"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"sequentialminus":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":5.0e-2},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}}}}
```

</div>

</div>

<div class="cell code" execution_count="44"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:542}"
id="pjFGE4dcyPp6" outputId="55279ccf-d2d4-47fb-83a1-6502f3d8fd71">

``` python
# Grouped bar plot for 'Proportion of Different Fuels Used in Residential Sector Over the Years'
df_melted = pd.melt(df_residential_fuel, id_vars='Year', value_vars=['Town Gas & Liquefied Petroleum Gas (Unit : Terajoule)', 'Oil & Coal Products (Unit : Terajoule)', 'Electricity (Unit : Terajoule)'])
fig = px.bar(df_melted, x='Year', y='value', color='variable', title='Proportion of Different Fuels Used in Residential Sector Over the Years', labels={'value':'Energy Consumption (TJ)', 'variable':'Fuel Type'})
fig.show()
```

<div class="output display_data">

``` json
{"config":{"plotlyServerURL":"https://plot.ly"},"data":[{"alignmentgroup":"True","hovertemplate":"Fuel Type=Town Gas & Liquefied Petroleum Gas (Unit : Terajoule)<br>Year=%{x}<br>Energy Consumption (TJ)=%{y}<extra></extra>","legendgroup":"Town Gas & Liquefied Petroleum Gas (Unit : Terajoule)","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"Town Gas & Liquefied Petroleum Gas (Unit : Terajoule)","offsetgroup":"Town Gas & Liquefied Petroleum Gas (Unit : Terajoule)","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020],"xaxis":"x","y":[19038,18977,18841,18635,18681,18063,18574,18335,19578,18070,19726],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"Fuel Type=Oil & Coal Products (Unit : Terajoule)<br>Year=%{x}<br>Energy Consumption (TJ)=%{y}<extra></extra>","legendgroup":"Oil & Coal Products (Unit : Terajoule)","marker":{"color":"#EF553B","pattern":{"shape":""}},"name":"Oil & Coal Products (Unit : Terajoule)","offsetgroup":"Oil & Coal Products (Unit : Terajoule)","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020],"xaxis":"x","y":[13,8,8,7,7,8,10,14,14,15,15],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"Fuel Type=Electricity (Unit : Terajoule)<br>Year=%{x}<br>Energy Consumption (TJ)=%{y}<extra></extra>","legendgroup":"Electricity (Unit : Terajoule)","marker":{"color":"#00cc96","pattern":{"shape":""}},"name":"Electricity (Unit : Terajoule)","offsetgroup":"Electricity (Unit : Terajoule)","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020],"xaxis":"x","y":[39344,39872,41189,39941,43415,42368,43120,42127,41965,42937,46675],"yaxis":"y"}],"layout":{"barmode":"relative","legend":{"title":{"text":"Fuel Type"},"tracegroupgap":0},"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmap"}],"heatmapgl":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmapgl"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"sequentialminus":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":5.0e-2},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"title":{"text":"Proportion of Different Fuels Used in Residential Sector Over the Years"},"xaxis":{"anchor":"y","domain":[0,1],"title":{"text":"Year"}},"yaxis":{"anchor":"x","domain":[0,1],"title":{"text":"Energy Consumption (TJ)"}}}}
```

</div>

</div>

<div class="cell code" execution_count="45"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:542}"
id="dhcThP5PyRbk" outputId="42f84e2b-226c-4b93-edc3-2f3e580dfb3a">

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

<div class="output display_data">

``` json
{"config":{"plotlyServerURL":"https://plot.ly"},"data":[{"mode":"lines","name":"Residential","type":"scatter","x":[2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020],"y":[58396,58857,60037,58582,62103,60439,61704,60476,61557,61022,66416]},{"mode":"lines","name":"Commercial","type":"scatter","x":[2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020],"y":[116391,116013,118330,118209,119617,120419,120460,120410,122222,123005,114513]},{"mode":"lines","name":"Industrial","type":"scatter","x":[2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020],"y":[16053,14155,13655,13204,13028,13054,12294,12722,12829,12274,12162]},{"mode":"lines","name":"Transport","type":"scatter","x":[2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020],"y":[90889,90498,90033,89593,89236,89049,89105,87397,85878,87225,79399]}],"layout":{"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmap"}],"heatmapgl":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmapgl"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"sequentialminus":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":5.0e-2},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"title":{"text":"Energy Consumption by Sector"},"xaxis":{"title":{"text":"Year"}},"yaxis":{"title":{"text":"Energy Consumption (TJ)"}}}}
```

</div>

</div>

<div class="cell code" execution_count="46"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:542}"
id="5SRBoq2ZyVd8" outputId="a8990669-98a7-4418-c1b2-973afc911c90">

``` python
# Line plot for 'Electricity Consumption by End-use'
fig = go.Figure()
fig.add_trace(go.Scatter(x=df_electricity_enduse['Year'], y=df_electricity_enduse['Air Conditioning (Unit : Terajoule)'], mode='lines', name='Air Conditioning'))
fig.add_trace(go.Scatter(x=df_electricity_enduse['Year'], y=df_electricity_enduse['Lighting (Unit : Terajoule)'], mode='lines', name='Lighting'))
fig.add_trace(go.Scatter(x=df_electricity_enduse['Year'], y=df_electricity_enduse['Refrigeration (Unit : Terajoule)'], mode='lines', name='Refrigeration'))
fig.update_layout(title='Electricity Consumption by End-use', xaxis_title='Year', yaxis_title='Electricity Consumption (TJ)')
fig.show()
```

<div class="output display_data">

``` json
{"config":{"plotlyServerURL":"https://plot.ly"},"data":[{"mode":"lines","name":"Air Conditioning","type":"scatter","x":[2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020],"y":[45511,44605,45079,43821,47264,46927,46441,46396,48032,47965,48622]},{"mode":"lines","name":"Lighting","type":"scatter","x":[2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020],"y":[19563,18357,18524,17774,17365,16914,16385,16026,16255,16094,15786]},{"mode":"lines","name":"Refrigeration","type":"scatter","x":[2010,2011,2012,2013,2014,2015,2016,2017,2018,2019,2020],"y":[9213,8117,7723,6886,6549,5812,5176,4454,4292,4363,4492]}],"layout":{"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmap"}],"heatmapgl":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmapgl"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"sequentialminus":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":5.0e-2},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"title":{"text":"Electricity Consumption by End-use"},"xaxis":{"title":{"text":"Year"}},"yaxis":{"title":{"text":"Electricity Consumption (TJ)"}}}}
```

</div>

</div>

<div class="cell code" execution_count="47"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:542}"
id="sBz2xVWNyXEA" outputId="b057b4eb-67af-4d35-a5ee-781cd3cbee6b">

``` python
# Pie chart for 'Proportion of Different Types of Renewable Energy'
fig = go.Figure(data=[go.Pie(labels=df_energy_renewable['Type of Renewable Energy'].values, values=df_energy_renewable['Renewable Energy (Unit : Terajoule)'].values)])
fig.update_layout(title_text='Proportion of Different Types of Renewable Energy')
fig.show()
```

<div class="output display_data">

``` json
{"config":{"plotlyServerURL":"https://plot.ly"},"data":[{"labels":["Waste-to-energy","Wind Energy & Hydropower","Solar Energy","Bio-diesel"],"type":"pie","values":[1930,9,189,276]}],"layout":{"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmap"}],"heatmapgl":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmapgl"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"sequentialminus":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":5.0e-2},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"title":{"text":"Proportion of Different Types of Renewable Energy"}}}
```

</div>

</div>
