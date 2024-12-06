# import libraries 

from bs4 import BeautifulSoup
import requests
import time
import datetime
import smtplib
# Connect to Website and pull in data

URL = 'https://www.amazon.in/HP-i5-12450H-15-6-inch-Response-fa1373TX/dp/B0D2DDJ6PJ/ref=sr_1_1_sspa?crid=K2EF8MS8NXAO&dib=eyJ2IjoiMSJ9.wKYFBl3CDh5aC6wPvRrWIeKr2Psckim6jUuxzFBZyI9mynSbn0V1MGVFnmjOXbBypf0xjQyBr9ZbrCZOeFemvdzqsnz4DK4PGhuLvb8bXgfYOwSp_dXvUyde_m2UNA21xv3lT6lgLzNgV8aevY8fru6MWQOsyYFqcYMxrNKhx7u_vNDQFm9E2G_zyiDW-SqCD-hKHjEZvwXB6TqgbApj3cdt1zfdtR0T_SVIvDdHG-Q.aqj5rrjVsL1LcQ00PT6yOtdEtrqC3blJW451aOy8Txk&dib_tag=se&keywords=gaming+laptops+under+50000&qid=1733420537&sprefix=%2Caps%2C366&sr=8-1-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&psc=1'

headers = {"User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36",
           "Accept-Encoding": "gzip, deflate",
           "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8",
           "DNT": "1",
           "Connection": "close",
           "Upgrade-Insecure-Requests": "1"}

page = requests.get(URL, headers=headers)

soup1 = BeautifulSoup(page.content, "html.parser")

soup2 = BeautifulSoup(soup1.prettify(), "html.parser")

# extracttitle
title = soup2.find(id='productTitle').text.strip()

#exttract price
price = soup2.find("span", {"class": "a-price-whole"}).text.strip()
print(title)
print(price)

#extract rating
rating = soup2.find("span", {"class": "a-icon-alt"})

# if the rating exists
if rating:
    rating_text = rating.text.strip()
    print("Rating:", rating_text)
else:
    print("Rating information not found.")


# Create a Timestamp for your output to track when data was collected

import datetime

today = datetime.date.today()

print(today)


#stock

stock = soup2.find("span", {"class":"a-size-medium a-color-success"}).text.strip()
print(stock)
# Create CSV and write headers and data into the file

import csv 

header = ['Title', 'Price', 'Ratings' 'Date', 'Inventory']
data = ["HP Victus Gaming Laptop, 12th Gen Intel Core i5-12450H,4GB RTX 2050 GPU,15.6-inch(39.6 cm),FHD,IPS,144Hz,16GB DDR4,512GB SSD,Backlit KB,MSO,B&O,9ms Response time(Blue, 2.29 kg),fa1373TX/fa1227TX","62,990","4.0", "2024-12-06","In Stock"]


with open('Amazon_Web_Scraper_Dataset.csv', 'w', newline='', encoding='UTF8') as f:
    writer = csv.writer(f)
    writer.writerow(header)
    writer.writerow(data)
    

import pandas as pd

dataframe = pd.read_csv(r'C:\Users\intel\Amazon_Web_Scraper_Dataset.csv')

print(dataframe)
#Now we are appending data to the csv

with open('Amazon_Web_Scraper_Dataset.csv', 'a+', newline='', encoding='UTF8') as f:
    writer = csv.writer(f)
    writer.writerow(data)
#Combine all of the above code into one function

def check_price():
    URL = 'https://www.amazon.in/HP-i5-12450H-15-6-inch-Response-fa1373TX/dp/B0D2DDJ6PJ/ref=sr_1_1_sspa?crid=K2EF8MS8NXAO&dib=eyJ2IjoiMSJ9.wKYFBl3CDh5aC6wPvRrWIeKr2Psckim6jUuxzFBZyI9mynSbn0V1MGVFnmjOXbBypf0xjQyBr9ZbrCZOeFemvdzqsnz4DK4PGhuLvb8bXgfYOwSp_dXvUyde_m2UNA21xv3lT6lgLzNgV8aevY8fru6MWQOsyYFqcYMxrNKhx7u_vNDQFm9E2G_zyiDW-SqCD-hKHjEZvwXB6TqgbApj3cdt1zfdtR0T_SVIvDdHG-Q.aqj5rrjVsL1LcQ00PT6yOtdEtrqC3blJW451aOy8Txk&dib_tag=se&keywords=gaming+laptops+under+50000&qid=1733420537&sprefix=%2Caps%2C366&sr=8-1-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&psc=1'

    headers = {"User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36",
               "Accept-Encoding": "gzip, deflate",
               "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8",
               "DNT": "1",
               "Connection": "close",
               "Upgrade-Insecure-Requests": "1"}

    page = requests.get(URL, headers=headers)

    soup1 = BeautifulSoup(page.content, "html.parser")

    soup2 = BeautifulSoup(soup1.prettify(), "html.parser")

    # extracttitle
    title = soup2.find(id='productTitle').text.strip()

    #exttract price
    price = soup2.find("span", {"class": "a-price-whole"}).text.strip()
    print(title)
    print(price)

    #extract rating
    rating = soup2.find("span", {"class": "a-icon-alt"})

    # if the rating exists
    if rating:
        rating_text = rating.text.strip()
        print("Rating:", rating_text)
    else:
        print("Rating information not found.")


    # Create a Timestamp for your output to track when data was collected

    import datetime

    today = datetime.date.today()

    print(today)


    # stock

    stock = soup2.find("span", {"class":"a-size-medium a-color-success"}).text.strip()
    print(stock)

    import csv 

    header = ['Title', 'Price', 'Ratings' 'Date', 'Inventory']
    data = ["HP Victus Gaming Laptop, 12th Gen Intel Core i5-12450H,4GB RTX 2050 GPU,15.6-inch(39.6 cm),FHD,IPS,144Hz,16GB DDR4,512GB SSD,Backlit KB,MSO,B&O,9ms Response time(Blue, 2.29 kg),fa1373TX/fa1227TX","62,990","4.0", "2024-12-06","In Stock"]

    writer = csv.writer(f)
    writer.writerow(header)
    writer.writerow(data)

    with open('Amazon_Web_Scraper_Dataset.csv', 'w', newline='', encoding='UTF8') as f:
        writer = csv.writer(f)
        writer.writerow(data)
# Runs check_price after a set time and inputs data into your CSV

while(True):
    check_price()
    time.sleep(86400)
import pandas as pd

dataframe = pd.read_csv(r'C:\Users\intel\Amazon_Web_Scraper_Dataset.csv')

print(dataframe)
