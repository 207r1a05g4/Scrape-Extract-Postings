# Scrape-Extract-Postings
import requests
from bs4 import BeautifulSoup

def scrape_postings():
    url = "https://qcpi.questcdn.com/cdn/results/?group=1950787&provider=1950787" 

    response = requests.get(url)
    
    soup = BeautifulSoup(response.text, 'html.parser')

    postings_section = soup.find('h2', text='Search Postings').find_next('ul')

    postings = postings_section.find_all('li')
    
    for posting in postings[:5]:
        
        est_value_notes = posting.find('span', class_='est-value-notes').text.strip()
        description = posting.find('span', class_='description').text.strip()
        closing_date = posting.find('span', class_='closing-date').text.strip()

        print("Est. Value Notes:", est_value_notes)
        print("Description:", description)
        print("Closing Date:", closing_date)
        print("--------------------")

scrape_postings()
