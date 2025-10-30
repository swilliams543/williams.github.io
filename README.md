<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Williams' Fashion Blog - Look of the Week</title>
    <style>
        /* --- General Styles --- */
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #F8F8F8; /* Light off-white for a clean look */
            color: #333;
        }

        /* --- Header Styles --- */
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

        /* --- Navigation Styles --- */
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

        /* --- Main Content Styles (Flexbox Layout) --- */
        .container {
            width: 90%;
            max-width: 1200px;
            margin: 20px auto;
            display: flex; /* Use Flexbox for side-by-side layout */
            gap: 20px;
        }

        /* --- Blog Section --- */
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
        
        /* Image adjustments for the blog post */
        .blog-post img {
            max-width: 100%; /* Ensures image fits within the blog section */
            height: auto;
            display: block; /* Removes any extra space below the image */
            margin: 15px 0;
            border: 1px solid #ddd;
            border-radius: 5px;
        }

        .blog-post h3 {
            color: #FF4500; /* Orange-Red for Post Titles */
            margin-top: 0;
        }

        /* --- Shop Section (Sidebar) --- */
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
            transition: background-color 0.3s;
        }

        .shop-item button:hover {
            background-color: #FFA500; /* Orange on hover */
        }

        /* --- Footer Styles --- */
        footer {
            background-color: #333;
            color: white;
            text-align: center;
            padding: 15px 0;
            margin-top: 20px;
            font-size: 0.9em;
        }

        /* Responsive Design: Stack columns on smaller screens */
        @media (max-width: 768px) {
            .container {
                flex-direction: column;
            }
            .blog-section, .shop-section {
                flex: none; /* Disable flex scaling */
                width: 100%; /* Take full width */
                padding: 15px;
            }
        }

    </style>
</head>
<body>

    <header>
        <h1>**WILLIAMS' FASHION BLOG**</h1>
        <p>Style & Inspiration for Your Unique Wardrobe</p>
    </header>

    <nav>
        <a href="index.html">Blog Home</a>
        <a href="#look">Look of the Week</a>
        <a href="#shop">Shop New Arrivals</a>
        <a href="#contact">Contact</a>
    </nav>

    <div class="container">
        
        <section class="blog-section" id="blog">
            <h2>**Latest Posts**</h2>

            <article class="blog-post" id="look">
                <h3>**Look of the Week: Vibrant Summer Chic**</h3>
                <p><small>Posted on Oct 30, 2025</small></p>
                
                <img src="https://github.com/user-attachments/assets/e53d79a8-cdfa-4a8d-90f5-8bb4ad881727" alt="Model wearing a long, sleeveless colorful vest with black cami and dress pants." />
                
                <p>For this look I have paired a long, sleeveless **colorful vest** with dress pants. I paired it with a black cami. You can also pair this with a silky top as well. Since the color is bright, I paired this suit with **brown, pointed toe sandals**. This is a great look for work or an event. You are sure to own your individuality if you opt for this **unique, chic look**.</p>
                
                <p>For my hair, I wore a **red bob** which complements the color green. Whether you are going to work or going to an event, you're sure to be unique with this summer, inspired look!</p>
            </article>

            <article class="blog-post">
                <h3>Style Tip: Accessorizing a Statement Piece</h3>
                <p><small>Posted on Oct 25, 2025</small></p>
                <p>Learn how to let one bold item, like a patterned coat or bright shoe, shine without overwhelming your outfit. <a href="#">Read More...</a></p>
            </article>

        </section>

        <aside class="shop-section" id="shop">
            <h2>**Shop The Look**</h2>
            <p>Direct links to similar pieces!</p>

            <div class="shop-item">
                <p><strong>Long Green Vest</strong></p>
                <p>$65.00</p>
                <button>Shop Now</button>
            </div>

            <div class="shop-item">
                <p><strong>Black Dress Trousers</strong></p>
                <p>$40.99</p>
                <button>Shop Now</button>
            </div>
            
            <div class="shop-item">
                <p><strong>Brown Pointed Sandals</strong></p>
                <p>$49.50</p>
                <button>Shop Now</button>
            </div>
            
        </aside>

    </div> 
    
    <footer>
        &copy; 2025 williams.github.io | Style Your Life.
    </footer>

</body>
</html>
