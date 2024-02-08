# Weather App

This is a simple weather application built using Python and the Tkinter library. It fetches real-time weather information from the OpenWeatherMap API and displays it in a graphical user interface.

## How It Works

The app allows the user to input a city name, and upon clicking the "Search" button, it retrieves the current weather details for that city using the OpenWeatherMap API.

## Requirements

This project requires Python and the Tkinter library. Additionally, it uses the `requests` library to fetch data from the OpenWeatherMap API. If you don't have Python installed, you can download it from the [official Python website](https://www.python.org/).

## Installation and Usage

1. Copy the code into a file and save it with a `.py` extension (for example, `weather_app.py`).
2. Install the `requests` library by running `pip install requests` in your terminal or command prompt.
3. Run the saved file to start the Weather App.

## Usage

1. Enter the desired city in the search bar.
2. Click the "Search" button to retrieve and display the current weather information.

## Contribution

This project is open to contributions. If you'd like to contribute:

1. Fork the repository.
2. Add new features or fix bugs.
3. Submit a pull request to the main repository.

## License

This project is licensed under the MIT License. For more information, see the [LICENSE](LICENSE) file.

---

## Contact

For feedback or questions regarding the project, you can reach out via email at [furkanduzman46@gmail.com](mailto:furkanduzman46@gmail.com).

---

## Code Sample

```python
import tkinter
import requests

url = "https://api.openweathermap.org/data/2.5/weather"
api_key = "8141ab941bbebbbf4d28d6621ca902f6"

def get_weather(city):
    params = {'q':city,'appid':api_key,'lang':'tr'}
    data = requests.get(url,params).json()
    if data:
        city = data['name'].capitalize()
        country  = data['sys']['country']
        temp = int(data['main']['temp'] - 273.15)
        condition = data['weather'][0]['description']
        return(city,country,temp,condition)
    
def main():
    city = search_entry.get()
    weather = get_weather(city)
    if weather:
        location_label['text'] = '{},{}'.format(weather[0],weather[1])
        temp_label['text'] = '{}°C'.format(weather[2])
        condition_label['text'] = weather[3]


screen = tkinter.Tk()
screen.geometry("450x550")
screen.config(bg="light pink")
screen.title("Weather App")

title_message = tkinter.Label(screen,text="Enter Country or City")
title_message.config(bg="light pink",font=("arial",30))
title_message.pack()

search_entry = tkinter.Entry(screen)
search_entry.pack(fill="both",ipady=10,padx=18,pady=5)
search_entry.focus()

search_button = tkinter.Button(screen,text="Search",font=("arial,15"),command=main)
search_button.pack()

location_label = tkinter.Label(screen,font=('arial',40))
location_label.config(bg="light pink")
location_label.pack(fill="both",ipady=10,padx=20)

temp_label = tkinter.Label(screen,font=('arial',50,'bold'))
temp_label.config(bg="light pink")
temp_label.pack()

condition_label = tkinter.Label(screen,font=('arial',20))
condition_label.config(bg="light pink")
condition_label.pack()

tkinter.mainloop()
