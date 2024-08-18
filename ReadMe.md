# 🌐 Scraping Data From Web 🌐

### Project goal 🎯

To scrape a list of the top 20 largest hedge funds from a webpage and export it as CSV 



### Tools Used 🧰
1. **Python**
2. **Visual Studio Code**
3. **Git & GitHub**


### The process 

Importing BeatifulSoup and Pandas libraries 

```python

from bs4 import BeautifulSoup
import requests
import pandas as pd

```

Defining the webpage's URL and initializing scraping

```python

url = 'https://en.wikipedia.org/wiki/List_of_hedge_funds'

page = requests.get(url) 

soup = BeautifulSoup(page.text,'html')

```

Finding the table I want to scrape and checking it

```python

table = soup.find_all('table')[0]

print(table)

```


Finding headers and removing the HTML elements leaving only the relevant text



```python

titles = table.find_all('th')

table_titles = [title.text.strip() for title in titles]

```


Initializing pandas dataframe and placing found headers as column names


```python

df= pd.DataFrame(columns = table_titles)

```

Defining the row-level data and writing it into the dataframe.
(The row level data block is tr. However each row resides in its own tr block)


```python

columns = table.find_all('tr')

for row in columns[1:]:
    rows = row.find_all('td')
    each_row_data = [data.text.strip() for data in rows]
    
    length = len(df)
    df.loc[length] = each_row_data

```

Exporting results as .CSV file 

```python

df.to_csv(r'C:\Users\user\Desktop\VS workspaces\Data Scraping 1\Hedge_Funds.csv', index = False )

```

# Results 🏁

## Check out code [here](/WebScraping.ipynb)
## Check out CSV [here](/Hedge_Funds.csv)