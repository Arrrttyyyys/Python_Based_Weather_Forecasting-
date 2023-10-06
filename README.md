# Python_Based_Weather_Forecasting
import requests

# Replace with your OpenWeatherMap API key
API_KEY = "YOUR_API_KEY"

def get_weather_data(city):
    try:
        # Construct the API URL
        base_url = "https://api.openweathermap.org/data/2.5/weather"
        params = {"q": city, "appid": API_KEY, "units": "metric"}  # You can change units to "imperial" for Fahrenheit

        # Make the API request
        response = requests.get(base_url, params=params)

        # Check if the request was successful
        if response.status_code == 200:
            data = response.json()
            return data
        else:
            print("Failed to retrieve weather data.")
            return None
    except Exception as e:
        print(f"An error occurred: {e}")
        return None

def display_weather(data):
    if data:
        city = data["name"]
        temperature = data["main"]["temp"]
        description = data["weather"][0]["description"]
        
        print(f"Weather in {city}:")
        print(f"Temperature: {temperature}°C")
        print(f"Description: {description.capitalize()}")

def main():
    print("Python Weather Forecasting Program")
    city = input("Enter the name of the city: ")
    
    weather_data = get_weather_data(city)
    
    if weather_data:
        display_weather(weather_data)

if __name__ == "__main__":
    main()
