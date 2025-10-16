# williams.github.io
Fashion Blog

Look of the week
<img width="1920" height="3420" alt="image" src="https://github.com/user-attachments/assets/e53d79a8-cdfa-4a8d-90f5-8bb4ad881727" />
For this look I have paired a long, sleeveless colorful vest with dress pants. I paired it with a black cami. You can also pair this with a silky top as well. Since the color is bright, I paired this suit with brown, pointed toe sandals. This is a great look for work or an event. You are sure to have your own individually if you opt for this unique, chic look. For my hair, I wore a red bob which complements the color green. Whether you are going to work or going to an event, you're such to be unique with this summer, inspired look! 
# Create a virtual environment (best practice)
python -m venv venv
# Activate the environment
# Windows: .\venv\Scripts\activate
# macOS/Linux: source venv/bin/activate

# Install the necessary libraries
pip install selenium
pip install webdriver-manager
import requests
import json
import os
import platform
import ctypes
from io import BytesIO

# --- Configuration ---
# Path where the downloaded image will be saved
OUTPUT_PATH = os.path.join(os.path.expanduser('~'), 'DesktopBackground.jpg')
# Wikimedia Commons API endpoint for a random image
COMMONS_API_URL = "https://commons.wikimedia.org/w/api.php?action=query&list=random&rnnamespace=6&rnlimit=1&format=json"

def get_random_image_url():
    """Fetches the URL of a random image file from Wikimedia Commons API."""
    try:
        print("1. Fetching random file title from Wikimedia Commons...")
        response = requests.get(COMMONS_API_URL)
        response.raise_for_status() # Raise an exception for bad status codes
        data = response.json()

        # Extract the file title (e.g., 'File:Example.jpg')
        file_title = data['query']['random'][0]['title']
        print(f"   -> Found title: {file_title}")

        # Construct the API request to get the file's information and direct URL
        info_api_url = (
            "https://commons.wikimedia.org/w/api.php?action=query&titles="
            f"{file_title}&prop=imageinfo&iiprop=url|size&format=json"
        )
        
        print("2. Fetching file direct URL...")
        info_response = requests.get(info_api_url)
        info_response.raise_for_status()
        info_data = info_response.json()

        # Navigate the complex JSON structure to find the direct URL
        page_id = list(info_data['query']['pages'].keys())[0]
        image_info = info_data['query']['pages'][page_id]['imageinfo'][0]
        
        direct_url = image_info['url']
        file_size_bytes = image_info['size']
        print(f"   -> Direct URL: {direct_url}")
        print(f"   -> File size: {file_size_bytes / (1024*1024):.2f} MB")
        
        return direct_url

    except requests.exceptions.RequestException as e:
        print(f"Error fetching data from API: {e}")
        return None
    except (KeyError, IndexError) as e:
        print(f"Error parsing API response: {e}")
        return None

def download_image(url, path):
    """Downloads the image from the URL to the specified path."""
    if not url:
        return False
    try:
        print(f"3. Downloading image to {path}...")
        image_response = requests.get(url, stream=True)
        image_response.raise_for_status()
        
        # Save the file chunk by chunk
        with open(path, 'wb') as file:
            for chunk in image_response.iter_content(chunk_size=8192):
                file.write(chunk)
        
        print("   -> Download successful.")
        return True
    except requests.exceptions.RequestException as e:
        print(f"Error downloading image: {e}")
        return False

def set_wallpaper_windows(image_path):
    """Sets the desktop background on Windows."""
    try:
        print("4. Setting desktop background (Windows)...")
        # Define the necessary Windows API functions
        SPI_SETDESKWALLPAPER = 20
        # Style flags (0: centered, 2: stretched, 10: tiled, 6: filled/fit)
        # Using 0 for centered/tiled, as 'stretched' often requires specific registry keys
        ctypes.windll.user32.SystemParametersInfoW(SPI_SETDESKWALLPAPER, 0, image_path, 3)
        print("   -> Background changed successfully.")
        return True
    except Exception as e:
        print(f"Error setting Windows background: {e}")
        return False

def main():
    image_url = get_random_image_url()
    
    if image_url and download_image(image_url, OUTPUT_PATH):
        # Check the operating system and call the appropriate function
        if platform.system() == "Windows":
            set_wallpaper_windows(OUTPUT_PATH)
        elif platform.system() == "Darwin": # macOS
            print("\n**Platform Note:** To set the background on macOS, you'll need the 'osascript' command or a library like 'pyobjc'. See instructions below.")
        elif platform.system() == "Linux":
            print("\n**Platform Note:** To set the background on Linux, you'll need a command-line tool like 'gsettings' (for Gnome) or 'feh'. See instructions below.")
        else:
            print(f"\n**Platform Note:** Auto-setting the background is not supported for your OS ({platform.system()}) in this script.")

if __name__ == "__main__":
    # Ensure necessary libraries are installed
    # pip install requests
    
    main()
