<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Color Spark</title>
    <style>
        body {
            font-family: 'Didot', serif;
            max-width: 80em;
            margin: 0 auto; /* Center the body horizontally */
            display: flex;
            align-items: center;
            justify-content: space-between;
            min-height: 100vh; /* Center the body vertically */
            padding: 0 2em; /* Fixed and equal padding on either side */
        }

        .left-container {
            flex: 1;
            padding: 10px; /* Add padding to the container */
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .right-container {
            flex: 1;
            padding: 10px; /* Add padding to the container */
            border: 5px solid transparent; /* Set initial border color to transparent */
            transition: border-color 0.5s ease; /* Add transition for smoother color change */
        }

        h1, h2, button {
            text-align: center; /* Center text */
            margin-bottom: 20px;
        }

        h2 {
            font-size: 16px;
            padding-bottom: 1em;
        }

        button {
            font-family: 'Gill Sans', sans-serif;
            padding: 10px;
            font-size: 16px;
            cursor: pointer;
            background-color: white;
            color: black;
            border: 2px solid #000; 
        }

        p {
            font-size: 20px;
            text-align: center; /* Center text */
        }

        .colored-border {
            border-color: transparent; /* Set the border color to transparent initially */
        }
    </style>
</head>
<body>

    <div class="left-container">
        <h1>Color Spark</h1>
        <h2>A idea generator for generating painting subject matter</h2>
        <button onclick="generateIdea()">Generate</button>
    </div>

    <div class="right-container colored-border" id="novelIdea">
        <p></p>
    </div>

    <script>
        async function fetchRandomQuote() {
            try {
                const response = await fetch('https://api.quotable.io/random');
                const data = await response.json();
                const lowercaseQuote = `"${data.content.charAt(0).toLowerCase()}${data.content.slice(1)}" - ${data.author}`;
                return lowercaseQuote;
            } catch (error) {
                console.error('Error fetching quote:', error);
                return 'Error';
            }
        }

        const colors = ['red', 'blue', 'green', 'yellow', 'purple', 'magenta', 'gray', 'violet', 'white', 'pink', 'brown', 'orange', 'aqua', 'coral',
        'maroon', 'tan', 'teal', 'indigo'];
        const emotions = ['happiness', 'sadness', 'excitement', 'calmness', 'angriness', 'fear', 'hope', 'joy', 'gratitude', 'contentment', 'grief',
        'disappointment', 'hate', 'frustration', 'disgust', 'shame', 'empathy', 'courage', 'pride', 'amusement'];

        function getRandomElement(array) {
            return array[Math.floor(Math.random() * array.length)];
        }

        async function generateIdea() {
            const novelIdea = document.getElementById('novelIdea');

            // Fetch a random quote
            const quote = await fetchRandomQuote();

            // Select random words from predefined lists
            const color = getRandomElement(colors);
            const emotion = getRandomElement(emotions);

            // Combine the words to create a novel idea
            const idea = `In a ${color} atmosphere, evoking a sense of ${emotion}, ${quote}.`;
            novelIdea.getElementsByTagName('p')[0].textContent = idea;

            // Change the border color dynamically
            novelIdea.style.borderColor = color;
        }
    </script>

</body>
</html>
