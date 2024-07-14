Mahindra Mumbai Data Analysis
This Jupyter notebook performs data extraction and analysis for used Mahindra cars listed in Mumbai. The dataset includes various details such as the car title, price, EMI, parking location, fuel type, transmission type, owner type, and kilometers driven.

Table of Contents
Setup
Data Extraction
Data Analysis
Save Data
Output
Setup
Install Dependencies: Ensure you have the required Python packages installed. You can install the necessary packages using:

bash
Copy code
pip install bs4 requests pandas numpy
Import Libraries: The notebook uses the following libraries:

pandas for data manipulation.
numpy for numerical operations.
beautifulsoup4 and requests for web scraping.
Data Extraction
The notebook begins by defining functions to extract various details from the HTML content using BeautifulSoup. The functions include:

get_title(soup): Extracts the car title.
get_price(soup): Extracts the price of the car.
get_emi(soup): Extracts the EMI for the car.
get_parking(soup): Extracts the parking location.
get_km_driven(soup): Extracts the kilometers driven.
get_fuel_type(soup): Extracts the fuel type.
get_transmission(soup): Extracts the transmission type.
get_owner_type(soup): Extracts the owner type.
The main URL used for scraping is:

python
Copy code
URL = "https://www.cars24.com/buy-used-car?f=make%3A%3D%3Amahindra&sort=bestmatch&serveWarrantyCount=true&gaId=319284782.1720028907&listingSource=TabFilter&storeCityId=1692"
webpage = requests.get(URL)
soup = BeautifulSoup(webpage.content, "html.parser")
Data Analysis
The extracted data is stored in a dictionary and then converted into a DataFrame for further analysis. The dictionary includes:

title
price
emi
parking location
km driven
fuel type
transmission
owner type
Example of creating the DataFrame:

python
Copy code
d = {
    "title": [], "price": [], "emi": [], "parking location": [],
    "fuel type": [], "transmission": [], "owner type": [], "km driven": []
}

# Loop for extracting product details from each link
for link in links_list:
    new_webpage = requests.get(link)
    new_soup = BeautifulSoup(new_webpage.content, "html.parser")
    d["title"].append(get_title(new_soup))
    d["price"].append(get_price(new_soup))
    d["emi"].append(get_emi(new_soup))
    d["parking location"].append(get_parking(new_soup))
    d["km driven"].append(get_km_driven(new_soup))
    d["fuel type"].append(get_fuel_type(new_soup))
    d["transmission"].append(get_transmission(new_soup))
    d["owner type"].append(get_owner_type(new_soup))

cars_df = pd.DataFrame.from_dict(d)
cars_df['title'].replace('', np.nan, inplace=True)
cars_df = cars_df.dropna(subset=['title'])
Save Data
The analyzed data is saved to a CSV file for future use:

python
Copy code
cars_df.to_csv("cars2_data.csv", header=True, index=False)
Output
The notebook displays the DataFrame and confirms the successful saving of data to a CSV file:

python
Copy code
from google.colab import files
files.download('cars2_data.csv')
This README provides a clear overview of what the notebook does, how to set it up, and the key steps involved in the process. ​
