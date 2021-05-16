Ideia principal: correlacionar id_category (x) com views (y)
https://www.kaggle.com/datasnaek/youtube-new?select=US_category_id.json
or
https://www.kaggle.com/rsrishav/youtube-trending-video-dataset?select=US_youtube_trending_data.csv


Topics

a)	Média, variância, desvio padrão e mediana para x e y

b)	O histograma de x e y.

c)	O coeficiente de correlação de x e y.

d)	Fazer o teste de normalidade para  y e x


# Probability and statistics in Python

### Import Dataset


```python
import pandas as pd

data = pd.read_csv('../data/US_youtube_trending_data.csv', header=0)

print(f"Number of rows and columns: {data.shape}")
data.head(25)
```

    Number of rows and columns: (53791, 16)





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
      <th>video_id</th>
      <th>title</th>
      <th>publishedAt</th>
      <th>channelId</th>
      <th>channelTitle</th>
      <th>categoryId</th>
      <th>trending_date</th>
      <th>tags</th>
      <th>view_count</th>
      <th>likes</th>
      <th>dislikes</th>
      <th>comment_count</th>
      <th>thumbnail_link</th>
      <th>comments_disabled</th>
      <th>ratings_disabled</th>
      <th>description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3C66w5Z0ixs</td>
      <td>I ASKED HER TO BE MY GIRLFRIEND...</td>
      <td>2020-08-11T19:20:14Z</td>
      <td>UCvtRTOMP2TqYqu51xNrqAzg</td>
      <td>Brawadis</td>
      <td>22</td>
      <td>2020-08-12T00:00:00Z</td>
      <td>brawadis|prank|basketball|skits|ghost|funny vi...</td>
      <td>1514614</td>
      <td>156908</td>
      <td>5855</td>
      <td>35313</td>
      <td>https://i.ytimg.com/vi/3C66w5Z0ixs/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>SUBSCRIBE to BRAWADIS ▶ http://bit.ly/Subscrib...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>M9Pmf9AB4Mo</td>
      <td>Apex Legends | Stories from the Outlands – “Th...</td>
      <td>2020-08-11T17:00:10Z</td>
      <td>UC0ZV6M2THA81QT9hrVWJG3A</td>
      <td>Apex Legends</td>
      <td>20</td>
      <td>2020-08-12T00:00:00Z</td>
      <td>Apex Legends|Apex Legends characters|new Apex ...</td>
      <td>2381688</td>
      <td>146739</td>
      <td>2794</td>
      <td>16549</td>
      <td>https://i.ytimg.com/vi/M9Pmf9AB4Mo/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>While running her own modding shop, Ramya Pare...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>J78aPJ3VyNs</td>
      <td>I left youtube for a month and THIS is what ha...</td>
      <td>2020-08-11T16:34:06Z</td>
      <td>UCYzPXprvl5Y-Sf0g4vX-m6g</td>
      <td>jacksepticeye</td>
      <td>24</td>
      <td>2020-08-12T00:00:00Z</td>
      <td>jacksepticeye|funny|funny meme|memes|jacksepti...</td>
      <td>2038853</td>
      <td>353787</td>
      <td>2628</td>
      <td>40221</td>
      <td>https://i.ytimg.com/vi/J78aPJ3VyNs/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>I left youtube for a month and this is what ha...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>kXLn3HkpjaA</td>
      <td>XXL 2020 Freshman Class Revealed - Official An...</td>
      <td>2020-08-11T16:38:55Z</td>
      <td>UCbg_UMjlHJg_19SZckaKajg</td>
      <td>XXL</td>
      <td>10</td>
      <td>2020-08-12T00:00:00Z</td>
      <td>xxl freshman|xxl freshmen|2020 xxl freshman|20...</td>
      <td>496771</td>
      <td>23251</td>
      <td>1856</td>
      <td>7647</td>
      <td>https://i.ytimg.com/vi/kXLn3HkpjaA/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>Subscribe to XXL → http://bit.ly/subscribe-xxl...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>VIUo6yapDbc</td>
      <td>Ultimate DIY Home Movie Theater for The LaBran...</td>
      <td>2020-08-11T15:10:05Z</td>
      <td>UCDVPcEbVLQgLZX0Rt6jo34A</td>
      <td>Mr. Kate</td>
      <td>26</td>
      <td>2020-08-12T00:00:00Z</td>
      <td>The LaBrant Family|DIY|Interior Design|Makeove...</td>
      <td>1123889</td>
      <td>45802</td>
      <td>964</td>
      <td>2196</td>
      <td>https://i.ytimg.com/vi/VIUo6yapDbc/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>Transforming The LaBrant Family's empty white ...</td>
    </tr>
    <tr>
      <th>5</th>
      <td>w-aidBdvZo8</td>
      <td>I Haven't Been Honest About My Injury.. Here's...</td>
      <td>2020-08-11T20:00:04Z</td>
      <td>UC5zJwsFtEs9WYe3A76p7xIA</td>
      <td>Professor Live</td>
      <td>24</td>
      <td>2020-08-12T00:00:00Z</td>
      <td>Professor injury|professor achilles|professor ...</td>
      <td>949491</td>
      <td>77487</td>
      <td>746</td>
      <td>7506</td>
      <td>https://i.ytimg.com/vi/w-aidBdvZo8/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>Subscribe To My Channel - https://www.youtube....</td>
    </tr>
    <tr>
      <th>6</th>
      <td>uet14uf9NsE</td>
      <td>OUR FIRST FAMILY INTRO!!</td>
      <td>2020-08-12T00:17:41Z</td>
      <td>UCDSJCBYqL7VQrlXfhr1RtwA</td>
      <td>Les Do Makeup</td>
      <td>26</td>
      <td>2020-08-12T00:00:00Z</td>
      <td>[None]</td>
      <td>470446</td>
      <td>47990</td>
      <td>440</td>
      <td>4558</td>
      <td>https://i.ytimg.com/vi/uet14uf9NsE/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>Hi babygirls!  Thank you so much for watching ...</td>
    </tr>
    <tr>
      <th>7</th>
      <td>ua4QMFQATco</td>
      <td>CGP Grey was WRONG</td>
      <td>2020-08-11T17:15:11Z</td>
      <td>UC2C_jShtL725hvbm1arSV9w</td>
      <td>CGP Grey</td>
      <td>27</td>
      <td>2020-08-12T00:00:00Z</td>
      <td>cgpgrey|education|hello internet</td>
      <td>1050143</td>
      <td>89190</td>
      <td>854</td>
      <td>6455</td>
      <td>https://i.ytimg.com/vi/ua4QMFQATco/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>‣ What Was TEKOI: https://www.youtube.com/watc...</td>
    </tr>
    <tr>
      <th>8</th>
      <td>SnsPZj91R7E</td>
      <td>SURPRISING MY DAD WITH HIS DREAM TRUCK!! | Lou...</td>
      <td>2020-08-10T22:26:59Z</td>
      <td>UCZDdF_p-L88NWVpzF0vjvMQ</td>
      <td>Louie's Life</td>
      <td>24</td>
      <td>2020-08-12T00:00:00Z</td>
      <td>surprising|dad|father|papa|with|dream|car|truc...</td>
      <td>1402687</td>
      <td>95694</td>
      <td>2158</td>
      <td>6613</td>
      <td>https://i.ytimg.com/vi/SnsPZj91R7E/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>Since I was little, i've had these goals for m...</td>
    </tr>
    <tr>
      <th>9</th>
      <td>SsWHMAhshPQ</td>
      <td>Ovi x Natanael Cano x Aleman x Big Soto - Veng...</td>
      <td>2020-08-11T23:00:10Z</td>
      <td>UC648rgJOboZlgcDbW00vTSA</td>
      <td>Rancho Humilde</td>
      <td>10</td>
      <td>2020-08-12T00:00:00Z</td>
      <td>Vengo De Nada|Aleman|Ovi|Big Soto|Trap|Ovi Nat...</td>
      <td>741028</td>
      <td>113983</td>
      <td>4373</td>
      <td>5618</td>
      <td>https://i.ytimg.com/vi/SsWHMAhshPQ/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>Vengo De Nada - Ovi x Natanael Cano x Aleman x...</td>
    </tr>
    <tr>
      <th>10</th>
      <td>49Z6Mv4_WCA</td>
      <td>i don't know what im doing anymore</td>
      <td>2020-08-11T20:24:34Z</td>
      <td>UCtinbF-Q-fVthA0qrFQTgXQ</td>
      <td>CaseyNeistat</td>
      <td>22</td>
      <td>2020-08-12T00:00:00Z</td>
      <td>[None]</td>
      <td>940036</td>
      <td>87111</td>
      <td>1860</td>
      <td>7052</td>
      <td>https://i.ytimg.com/vi/49Z6Mv4_WCA/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>ssend love to my sponsor; for a super Limited ...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>nt3VVyv5pxQ</td>
      <td>Try Not To Laugh Challenge #51</td>
      <td>2020-08-11T17:00:31Z</td>
      <td>UCYJPby9DRCteedh5tfxVbrw</td>
      <td>Smosh Pit</td>
      <td>22</td>
      <td>2020-08-12T00:00:00Z</td>
      <td>smosh|smosh pit|smosh games|funny|comedy</td>
      <td>591837</td>
      <td>44168</td>
      <td>409</td>
      <td>2652</td>
      <td>https://i.ytimg.com/vi/nt3VVyv5pxQ/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>You know what time it is— time to try not to l...</td>
    </tr>
    <tr>
      <th>12</th>
      <td>I6hswz4rIrU</td>
      <td>Rainbow Six Siege: Operation Shadow Legacy Rev...</td>
      <td>2020-08-11T17:13:53Z</td>
      <td>UCBMvc6jvuTxH6TNo9ThpYjg</td>
      <td>Ubisoft North America</td>
      <td>20</td>
      <td>2020-08-12T00:00:00Z</td>
      <td>R6|R6S|Siege|New Siege|New Operators|New Ops|G...</td>
      <td>320872</td>
      <td>14288</td>
      <td>774</td>
      <td>2085</td>
      <td>https://i.ytimg.com/vi/I6hswz4rIrU/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>“Prepare. Execute. Vanish”Sam Fisher joins Tea...</td>
    </tr>
    <tr>
      <th>13</th>
      <td>W7VK4DUHvKU</td>
      <td>Lil Yachty &amp; Future - Pardon Me (Official Video)</td>
      <td>2020-08-11T19:00:10Z</td>
      <td>UC1X3TRsCt36QPjF1p5f3HTg</td>
      <td>LilYachtyVEVO</td>
      <td>10</td>
      <td>2020-08-12T00:00:00Z</td>
      <td>Lil Yachty|Lil Boat 3|Future Lil Yachty|Pardon...</td>
      <td>413372</td>
      <td>26440</td>
      <td>293</td>
      <td>1495</td>
      <td>https://i.ytimg.com/vi/W7VK4DUHvKU/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>Watch the official video for Lil Yachty &amp; Futu...</td>
    </tr>
    <tr>
      <th>14</th>
      <td>W9Aen8hG20Y</td>
      <td>When Our Generation Gets Old and Hears a Throw...</td>
      <td>2020-08-10T22:33:48Z</td>
      <td>UCR9NuNwCUIhMOLUQnLN7_WA</td>
      <td>Kyle Exum</td>
      <td>23</td>
      <td>2020-08-12T00:00:00Z</td>
      <td>When Our Generation Gets Old and Hears a Throw...</td>
      <td>921261</td>
      <td>124183</td>
      <td>1678</td>
      <td>16460</td>
      <td>https://i.ytimg.com/vi/W9Aen8hG20Y/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>500,000 Likes and I’ll drop a Part 6!Thanks fo...</td>
    </tr>
    <tr>
      <th>15</th>
      <td>BNeDH6UTmXw</td>
      <td>Ten Minutes with Tyler Cameron | Q&amp;A</td>
      <td>2020-08-11T22:00:05Z</td>
      <td>UCMw7m-ScQ6jV1FQzQnn1y8Q</td>
      <td>Tyler Cameron</td>
      <td>22</td>
      <td>2020-08-12T00:00:00Z</td>
      <td>the bachelor|the bachelorette|Tyler c|Tyler Ca...</td>
      <td>105955</td>
      <td>4511</td>
      <td>69</td>
      <td>673</td>
      <td>https://i.ytimg.com/vi/BNeDH6UTmXw/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>Come hang out me with me for 10 minutes where ...</td>
    </tr>
    <tr>
      <th>16</th>
      <td>6TIsR_7nrNc</td>
      <td>Kylie Jenner Reacts To 'WAP' Music Video Backlash</td>
      <td>2020-08-10T18:41:19Z</td>
      <td>UC2rJLq19N0dGrxfib80M_fg</td>
      <td>HollywoodLife</td>
      <td>24</td>
      <td>2020-08-12T00:00:00Z</td>
      <td>kylie jenner|kendall jenner|cardi b|wap|reacts...</td>
      <td>1007540</td>
      <td>10102</td>
      <td>7932</td>
      <td>2763</td>
      <td>https://i.ytimg.com/vi/6TIsR_7nrNc/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>Kylie Jenner dissed over cameo in Cardi B and ...</td>
    </tr>
    <tr>
      <th>17</th>
      <td>gPdUslndvVI</td>
      <td>Our Farm Got Destroyed.</td>
      <td>2020-08-11T23:00:06Z</td>
      <td>UCuxlXCfVyV-i5YLL30jkomw</td>
      <td>Cole The Cornstar</td>
      <td>22</td>
      <td>2020-08-12T00:00:00Z</td>
      <td>farming|family farm|agriculture|agriculture jo...</td>
      <td>277338</td>
      <td>37533</td>
      <td>197</td>
      <td>3666</td>
      <td>https://i.ytimg.com/vi/gPdUslndvVI/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>Wind storm, rain, and lots of destruction; wel...</td>
    </tr>
    <tr>
      <th>18</th>
      <td>GTp-0S82guE</td>
      <td>Time to Talk..</td>
      <td>2020-08-11T12:04:40Z</td>
      <td>UCCgLoMYIyP0U56dEhEL1wXQ</td>
      <td>Chloe Ting</td>
      <td>26</td>
      <td>2020-08-12T00:00:00Z</td>
      <td>chloe ting|chloeting|defamation|cyber bullying...</td>
      <td>1648441</td>
      <td>130147</td>
      <td>1425</td>
      <td>15773</td>
      <td>https://i.ytimg.com/vi/GTp-0S82guE/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>I talked about some claims about me that was h...</td>
    </tr>
    <tr>
      <th>19</th>
      <td>jbGRowa5tIk</td>
      <td>ITZY “Not Shy” M/V TEASER</td>
      <td>2020-08-11T15:00:13Z</td>
      <td>UCaO6TYtlC8U5ttz62hTrZgg</td>
      <td>JYP Entertainment</td>
      <td>10</td>
      <td>2020-08-12T00:00:00Z</td>
      <td>JYP Entertainment|JYP|ITZY|있지|ITZY Video|ITZY ...</td>
      <td>5999732</td>
      <td>714287</td>
      <td>15174</td>
      <td>31039</td>
      <td>https://i.ytimg.com/vi/jbGRowa5tIk/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>ITZY Not Shy M/V[ITZY Official] https://www.yo...</td>
    </tr>
    <tr>
      <th>20</th>
      <td>vePc5V4h_kg</td>
      <td>Shark Attack Test- Human Blood vs. Fish Blood</td>
      <td>2020-08-09T16:00:11Z</td>
      <td>UCY1kMZp36IQSyNx_9h4mpCg</td>
      <td>Mark Rober</td>
      <td>28</td>
      <td>2020-08-12T00:00:00Z</td>
      <td>sharks|sharkweek|jaws|shark attack|blood in wa...</td>
      <td>14684474</td>
      <td>544038</td>
      <td>15818</td>
      <td>33507</td>
      <td>https://i.ytimg.com/vi/vePc5V4h_kg/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>I personally got in the water and tested if Sh...</td>
    </tr>
    <tr>
      <th>21</th>
      <td>5WjcDji3xYc</td>
      <td>Honest Trailers | Avatar: The Last Airbender</td>
      <td>2020-08-11T17:03:59Z</td>
      <td>UCOpcACMWblDls9Z6GERVi1A</td>
      <td>Screen Junkies</td>
      <td>1</td>
      <td>2020-08-12T00:00:00Z</td>
      <td>screenjunkies|screen junkies|honest trailers|h...</td>
      <td>833369</td>
      <td>50181</td>
      <td>1120</td>
      <td>4634</td>
      <td>https://i.ytimg.com/vi/5WjcDji3xYc/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>►►Subscribe to ScreenJunkies!► https://fandom....</td>
    </tr>
    <tr>
      <th>22</th>
      <td>FopIxceEr8g</td>
      <td>EXTREME Game of Hide and Seek in my NEW HOUSE!!</td>
      <td>2020-08-10T17:09:53Z</td>
      <td>UCilwZiBBfI9X6yiZRzWty8Q</td>
      <td>FaZe Rug</td>
      <td>24</td>
      <td>2020-08-12T00:00:00Z</td>
      <td>faze rug|rug|rugfaze|fazerug|hide n seek|hide ...</td>
      <td>3061467</td>
      <td>206840</td>
      <td>2646</td>
      <td>14934</td>
      <td>https://i.ytimg.com/vi/FopIxceEr8g/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>THIS WAS SO MUCH FUNWe played hide n seek for ...</td>
    </tr>
    <tr>
      <th>23</th>
      <td>p7HGUZWq_8s</td>
      <td>Doing Doja Cat’s Makeup!!</td>
      <td>2020-08-11T19:00:09Z</td>
      <td>UCucot-Zp428OwkyRm2I7v2Q</td>
      <td>James Charles</td>
      <td>24</td>
      <td>2020-08-12T00:00:00Z</td>
      <td>james|james charles|makeup artist|covergirl|co...</td>
      <td>3662673</td>
      <td>394675</td>
      <td>5757</td>
      <td>27346</td>
      <td>https://i.ytimg.com/vi/p7HGUZWq_8s/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>HI SISTERS! Today’s video is a collaboration w...</td>
    </tr>
    <tr>
      <th>24</th>
      <td>AMXT1ok5UBg</td>
      <td>THIS IS THE END.</td>
      <td>2020-08-11T23:00:02Z</td>
      <td>UCWwWOFsW68TqXE-HZLC3WIA</td>
      <td>The ACE Family</td>
      <td>22</td>
      <td>2020-08-12T00:00:00Z</td>
      <td>the ace family this is the end|ace family this...</td>
      <td>2630410</td>
      <td>185419</td>
      <td>4744</td>
      <td>15908</td>
      <td>https://i.ytimg.com/vi/AMXT1ok5UBg/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>THIS IS THE END.Shop on The RealReal and get $...</td>
    </tr>
  </tbody>
</table>
</div>



## Data Treatment

### Check duplicates


```python
# TODO: print duplicates
duplicated = data.duplicated()
num_duplicated = 0

for isDuplicated in duplicated:
    num_duplicated += 1 if num_duplicated else 0

print(f"Number of duplicated values: {num_duplicated}")
```

    Number of duplicated values: 0



```python
#TODO: fix duplicates
```

### Check NAN values


```python
# TODO: print NAN values
```


```python
# TODO: fix NAN
```


```python
import numpy as np
```

## Select target(y) and atribute (x)


```python
numpy_data = data.to_numpy()
```


```python
x = data['categoryId']

x.head(25)
```




    0     22
    1     20
    2     24
    3     10
    4     26
    5     24
    6     26
    7     27
    8     24
    9     10
    10    22
    11    22
    12    20
    13    10
    14    23
    15    22
    16    24
    17    22
    18    26
    19    10
    20    28
    21     1
    22    24
    23    24
    24    22
    Name: categoryId, dtype: int64




```python
y = data['view_count']

y.head(25)
```




    0      1514614
    1      2381688
    2      2038853
    3       496771
    4      1123889
    5       949491
    6       470446
    7      1050143
    8      1402687
    9       741028
    10      940036
    11      591837
    12      320872
    13      413372
    14      921261
    15      105955
    16     1007540
    17      277338
    18     1648441
    19     5999732
    20    14684474
    21      833369
    22     3061467
    23     3662673
    24     2630410
    Name: view_count, dtype: int64



## Mean


```python
mean_x = np.mean(x)
print(f"Mean(x): {mean_x}")
```

    Mean(x): 18.622594857875853



```python
mean_y = np.mean(y)
print(f"Mean(y): {mean_y}")
```

    Mean(y): 2706730.433659906


## Variance


```python
var_x = np.var(x)
print(f"Var(x): {var_x}")
```

    Var(x): 49.69740845512702



```python
var_y = np.var(y)
print(f"Var(y): {var_y}")
```

    Var(y): 37743547310036.03


## Standard Deviation


```python
std_x = np.std(x)
print(f"STD(x): {mean_x}")

```

    STD(x): 18.622594857875853



```python
std_y = np.std(y)
print(f"STD(y): {std_y}")

```

    STD(y): 6143577.72881861


## Median


```python
median_x = np.median(x)
print(f"Median(x): {median_x}")

```

    Median(x): 20.0



```python
median_y = np.median(y)
print(f"Median(y): {median_y}")
```

    Median(y): 1129434.0


## Histogram


```python
import matplotlib.pyplot as plt
from scipy import stats
```


```python
# (X histogram)

plt.hist(x, bins = 'auto')
plt.title('Data')
plt.ylabel('Frequency')
plt.xlabel('Values')
plt.show()
```


    
![png](.github/output_29_0.png)
    



```python
# (Y histogram)

plt.hist(y, bins = 'auto')
plt.title('Data')
plt.ylabel('Frequency')
plt.xlabel('Values')
plt.show()
```


    
![png](.github/output_30_0.png)
    


## X and Y Correlation


```python
# (Correlation Coefficients XY)

np.corrcoef(x, y)
```




    array([[ 1.        , -0.08332816],
           [-0.08332816,  1.        ]])




```python

```


