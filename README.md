<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ChatGPT-like Service</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f9;
        }
        .container {
            max-width: 600px;
            margin: 50px auto;
            padding: 20px;
            background: #fff;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            border-radius: 8px;
        }
        .input-section, .response-section {
            margin-bottom: 20px;
        }
        textarea {
            width: 100%;
            padding: 10px;
            font-size: 16px;
            border: 1px solid #ddd;
            border-radius: 4px;
            resize: none;
        }
        button {
            background-color: #007bff;
            color: #fff;
            border: none;
            padding: 10px 15px;
            cursor: pointer;
            border-radius: 4px;
            font-size: 16px;
        }
        button:hover {
            background-color: #0056b3;
        }
        .response {
            background: #f1f1f1;
            padding: 10px;
            border-radius: 4px;
            border: 1px solid #ddd;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>ChatGPT-like Service</h2>
        <div class="input-section">
            <textarea id="prompt" rows="5" placeholder="Enter your question here..."></textarea>
        </div>
        <button onclick="getResponse()">Submit</button>
        <div class="response-section">
            <h4>Response:</h4>
            <div id="response" class="response">Waiting for input...</div>
        </div>
    </div>

    <script>
        async function getResponse() {
            const prompt = document.getElementById('prompt').value;

            if (!prompt.trim()) {
                alert('Please enter a question!');
                return;
            }

            document.getElementById('response').innerText = 'Processing...';

            try {
                const response = await fetch('https://mio9o8bgck.execute-api.us-east-1.amazonaws.com/dev/ask', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({ prompt: prompt })
                });

                if (!response.ok) {
                    throw new Error('API response was not ok');
                }

                const data = await response.json();
                document.getElementById('response').innerText = data.response || 'No response received.';
            } catch (error) {
                console.error('Error:', error);
                document.getElementById('response').innerText = 'An error occurred. Please try again.';
            }
        }
    </script>
</body>
</html>

