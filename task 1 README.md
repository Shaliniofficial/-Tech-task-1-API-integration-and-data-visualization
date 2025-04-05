# -Tech-task-1-API-integration-and-data-visualization
import requests
import matplotlib.pyplot as plt
import seaborn as sns

city_name='lucknow'
API_key='feb45dd3d3a3ed693bab50132baf25a3'
url= f'https://api.openweathermap.org/data/2.5/weather?q={city_name}&appid={API_key}&units=metric'
response = requests.get(url)
if response.status_code == 200:
    data= response.json()
data = response.json()

# Extract relevant information
if data["cod"] != "404":
    main = data["main"]
    wind = data["wind"]
    weather_desc = data["weather"][0]["description"]
    temp = main["temp"]
    pressure = main["pressure"]
    humidity = main["humidity"]
    wind_speed = wind["speed"]

    print(f"Temperature: {temp}")
    print(f"Pressure: {pressure}")
    print(f"Humidity: {humidity}")
    print(f"Wind Speed: {wind_speed}")
    print(f"Weather Description: {weather_desc}")
else:
    print("City Not Found")


# Data for visualization
labels = ['Temperature', 'Pressure', 'Humidity', 'Wind Speed']
values = [temp, pressure, humidity, wind_speed]

# Bar plot
plt.figure(figsize=(10, 5))
sns.barplot(x=labels, y=values, palette='coolwarm')
plt.title('Weather Data Visualization')
plt.ylabel('Values')
plt.xlabel('Weather Parameters')
plt.xlabel(city_name)
plt.show()
