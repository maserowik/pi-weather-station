
# Pi Weather Station

This is a weather station designed to be used with a Raspberry Pi on the official 7" 800x480 touchscreen.

![pws-screenshot3](https://user-images.githubusercontent.com/15202038/91359998-4625bb80-e7bb-11ea-937e-c87eede41f35.JPG)

The weather station will require you to have API keys from [Mapbox](https://www.mapbox.com/) and [ClimaCell (v4)](https://www.climacell.co/). Optionally, you can use an API key from [LocationIQ](https://locationiq.com/) to preform reverse geocoding.

Weather maps are provided by the [RainViewer](https://www.rainviewer.com/) API, which generously does not require an [API key](https://www.rainviewer.com/api.html).

Sunrise and Sunset times are provided by [Sunrise-Sunset](https://sunrise-sunset.org/), which generously does not require an [API key](https://sunrise-sunset.org/api).

See it in action [here](https://www.youtube.com/watch?v=dvM6cyqYSw8).

> Be mindful of the plan limits for your API keys and understand the terms of each provider, as scrolling around the map and selecting different locations will incur API calls for every location. Additionally, the weather station will periodically make additional api calls to get weather updates throughout the day.

# v2.0.0

1-22-2021: Now uses [ClimaCell](https://www.climacell.co/) API v4. For ClimaCell API v3 keys, use [Pi Weather Station v1](https://github.com/elewin/pi-weather-station/releases/tag/v1.0).

# Setup



Prerequisites
Install Node.js and npm
Open a terminal on your Raspberry Pi 4.
Install Node.js (LTS version is recommended):


curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -

sudo apt install -y nodejs

Verify Installation:
Run the following commands to confirm Node.js and npm are installed:
node -v
npm -v

sudo apt update
sudo apt install -y git

Clone the Repository
Navigate to your desired directory and clone the project:

git clone https://github.com/elewin/pi-weather-station.git

cd pi-weather-station


Install Dependencies
Install the required Node.js packages:

npm install

Configure API Keys
Create a .env file in the project root directory and add your API keys:

nano .env
Add the following lines to the .env file:


MAPBOX_API_KEY=your_mapbox_key

CLIMACELL_API_KEY=your_climacell_key

LOCATIONIQ_API_KEY=your_locationiq_key (optional)

Start the Server
Launch the weather station:

npm start

Access the Application
Open a browser on your Raspberry Pi or another device on the same network and go to http://localhost:8080.
Use full-screen mode (F11) for an enhanced display.

Auto-Boot Setup 
Create a systemd Service
Open a terminal and create a new service file:

sudo nano /etc/systemd/system/pi-weather.service
Add the Following Content:
Replace /home/pi/pi-weather-station with the full path to your project directory:


[Unit]
Description=Pi Weather Station
After=network.target

[Service]
ExecStart=/usr/bin/node /home/pi/pi-weather-station/index.js
WorkingDirectory=/home/pi/pi-weather-station
Restart=always
User=pi
Environment=MAPBOX_API_KEY=your_mapbox_key
Environment=CLIMACELL_API_KEY=your_climacell_key
Environment=LOCATIONIQ_API_KEY=your_locationiq_key (optional)

[Install]
WantedBy=multi-user.target
Reload systemd and Enable the Service:


sudo systemctl daemon-reload
sudo systemctl enable pi-weather.service

Start the Service:
sudo systemctl start pi-weather.service

Check Service Status:
Ensure the service is running:

sudo systemctl status pi-weather.service


# License

The MIT License (MIT)

Copyright (c) 2020 Eric Lewin

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
