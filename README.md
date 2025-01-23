<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AWS Bedrock's Claude Model in Action</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            margin: 0;
            padding: 20px;
        }
        #container {
            max-width: 600px;
            margin: 0 auto;
            padding: 20px;
            background-color: white;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            border-radius: 8px;
        }
        h1 {
            text-align: center;
            color: #333;
        }
        textarea {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 16px;
        }
        button {
            display: block;
            width: 100%;
            padding: 10px;
            background-color: #28a745;
            color: white;
            border: none;
            border-radius: 4px;
            font-size: 16px;
            cursor: pointer;
            margin-top: 10px;
        }
        button:hover {
            background-color: #218838;
        }
        .response {
            margin-top: 20px;
            padding: 15px;
            background-color: #f1f1f1;
            border-radius: 4px;
            border: 1px solid #ddd;
            white-space: pre-wrap;
        }
    </style>
</head>
<body>

<div id="container">
    <h1>AWS Bedrock's Claude Model in Action</h1>
    <textarea id="user-prompt" rows="5" placeholder="Enter your prompt here..."></textarea>
    <button id="submit-btn">Ask</button>
    <div id="response-container" class="response" style="display: none;"></div>
</div>

<script>
    document.getElementById("submit-btn").addEventListener("click", function() {
        const prompt = document.getElementById("user-prompt").value;
        const responseContainer = document.getElementById("response-container");

        if (prompt.trim() === "") {
            alert("Please enter a prompt.");
            return;
        }

        // Display loading text
        responseContainer.style.display = "block";
        responseContainer.textContent = "Thinking...";

        // Make POST request to API Gateway
        fetch('https://mio9o8bgck.execute-api.us-east-1.amazonaws.com/dev/ask', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({
                prompt: prompt,
                temperature: 0.7,
                max_tokens: 200
            })
        })
        .then(response => response.json())
        .then(data => {
            if (data.response) {
                responseContainer.textContent = data.response;
            } else if (data.error) {
                responseContainer.textContent = `Error: ${data.error}`;
            }
        })
        .catch(error => {
            responseContainer.textContent = `Error: ${error}`;
        });
    });
</script>

</body>
</html>
