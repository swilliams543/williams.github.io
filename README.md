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

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chic Threads - Fashion Blog & Shop</title>
    <style>
        /* CSS goes here! (See section 2 below) */
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #F8F8F8; /* Light off-white for a clean look */
            color: #333;
        }

        /* Header Styles */
        header {
            background-color: #FF69B4; /* Hot Pink - Very Fashionable */
            color: white;
            padding: 20px 0;
            text-align: center;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }

        header h1 {
            margin: 0;
            font-size: 2.5em;
            letter-spacing: 3px;
        }

        /* Navigation Styles */
        nav {
            background-color: #4CAF50; /* Vibrant Green - A complementary splash */
            padding: 10px 0;
            text-align: center;
        }

        nav a {
            color: white;
            text-decoration: none;
            padding: 0 15px;
            font-weight: bold;
            text-transform: uppercase;
            transition: color 0.3s;
        }

        nav a:hover {
            color: #FFD700; /* Gold on hover */
        }

        /* Main Content Styles */
        .container {
            width: 90%;
            margin: 20px auto;
            display: flex; /* Use Flexbox for side-by-side layout */
            gap: 20px;
        }

        /* Blog Section */
        .blog-section {
            flex: 2; /* Takes up 2/3 of the space */
            padding: 20px;
            background-color: white;
            border-left: 5px solid #FF69B4; /* Pink accent border */
        }

        .blog-post {
            margin-bottom: 30px;
            padding-bottom: 20px;
            border-bottom: 1px dashed #ccc;
        }

        .blog-post h3 {
            color: #FF4500; /* Orange-Red for Post Titles */
        }

        /* Shop Section (Sidebar) */
        .shop-section {
            flex: 1; /* Takes up 1/3 of the space */
            padding: 20px;
            background-color: #DDA0DD; /* Plum/Lavender for a different colorful section */
            color: #333;
            text-align: center;
        }

        .shop-item {
            background-color: white;
            padding: 10px;
            margin-bottom: 15px;
            border-radius: 5px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }

        .shop-item button {
            background-color: #FFD700; /* Gold button */
            color: #333;
            border: none;
            padding: 8px 15px;
            cursor: pointer;
            font-weight: bold;
            border-radius: 3px;
        }

        /* Footer Styles */
        footer {
            background-color: #333;
            color: white;
            text-align: center;
            padding: 15px 0;
            margin-top: 20px;
            font-size: 0.9em;
        }

    </style>
</head>
<body>

    <header>
        <h1>**CHIC THREADS**</h1>
        <p>Your Daily Dose of Style & Shopping</p>
    </header>

    <nav>
        <a href="#blog">Blog Home</a>
        <a href="#shop">Shop New Arrivals</a>
        <a href="#about">About</a>
        <a href="#contact">Contact</a>
    </nav>

    <div class="container">
        
        <section class="blog-section" id="blog">
            <h2>**Latest Fashion Trends**</h2>

            <article class="blog-post">
                <h3>Spring's Must-Have Prints: Floral & Geometric</h3>
                <p><small>Posted on Oct 22, 2025</small></p>
                <p>Forget the neutrals—this season is all about bold statements! We dive into how to style the perfect floral dress for day and geometric patterns for night. <a href="#">Read More...</a></p>
            </article>
            
            <article class="blog-post">
                <h3>The Return of the Wide-Leg Pant</h3>
                <p><small>Posted on Oct 20, 2025</small></p>
                <p>Narrow silhouettes are out, and comfort is in. See our top 5 picks for wide-leg pants that flatter every figure and find out where to shop them. <a href="#">Read More...</a></p>
            </article>

        </section>

        <aside class="shop-section" id="shop">
            <h2>**Shop The Look**</h2>
            <p>New arrivals posted weekly!</p>

            <div class="shop-item">
                <p><strong>The "Sunset" Maxi Dress</strong></p>
                <p>$49.99</p>
                <button>Add to Cart</button>
            </div>

            <div class="shop-item">
                <p><strong>Emerald Green Blazer</strong></p>
                <p>$75.00</p>
                <button>Add to Cart</button>
            </div>
            
            <div class="shop-item">
                <p><strong>Chunky Gold Hoops</strong></p>
                <p>$19.50</p>
                <button>Add to Cart</button>
            </div>
            
        </aside>

    </div> <footer>
        &copy; 2025 Chic Threads Fashion Co. | Style Your Life.
    </footer>

</body>
</html>
    
<aside class="shop-section" id="shop">
            <h2>**Shop The Look**</h2>
            <p>New arrivals posted weekly!</p>

            <div class="shop-item">
                <p><strong>[AUTOMATED_PRODUCT_NAME_1]</strong></p>
                <p>[AUTOMATED_PRICE_1]</p>
                <button>[IF STOCK > 0] Add to Cart [ELSE] Out of Stock</button> 
            </div>

            <div class="shop-item">
                <p><strong>[AUTOMATED_PRODUCT_NAME_2]</strong></p>
                <p>[AUTOMATED_PRICE_2]</p>
                <button>[IF STOCK > 0] Add to Cart [ELSE] Out of Stock</button>
            </div>
            
            </aside>
