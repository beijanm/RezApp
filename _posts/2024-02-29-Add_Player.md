---
toc: false
comments: false 
layout: base
title: Add Player
type: hacks
courses: { compsci: {week: 5} }
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Add NBA Player</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(to right, #6a11cb 0%, #2575fc 100%);
            padding: 20px;
            color: #fff;
        }
        form {
            background: #ffffff1a;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            backdrop-filter: blur(10px);
        }
        input, button {
            width: calc(100% - 22px);
            padding: 10px;
            margin: 10px 0;
            border-radius: 5px;
            border: 1px solid #ddd;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            transition: transform 0.2s ease-in-out;
        }
        input:focus, button:hover {
            transform: scale(1.02);
        }
        button {
            cursor: pointer;
            background-color: #007bff;
            color: #fff;
            border: none;
        }
        button:hover {
            background-color: #0056b3;
        }
        a {
            display: inline-block;
            margin-top: 20px;
            color: #fff;
            text-decoration: none;
        }
        a:hover {
            text-decoration: underline;
        }
    </style>
</head>
<body>
    <h1>Add NBA Player</h1>
    <form id="addPlayerForm">
        <input type="text" id="playerName" placeholder="Player Name" required>
        <input type="text" id="playerTeam" placeholder="Team" required>
        <button type="submit">Add Player</button>
    </form>
    <a href="http://127.0.0.1:4200/RezApp//2024/02/28/nbafrontend.html">Back to Player List</a>

    <script>
        document.getElementById('addPlayerForm').addEventListener('submit', function(event) {
            event.preventDefault();
            const name = document.getElementById('playerName').value;
            const team = document.getElementById('playerTeam').value;

            fetch('http://127.0.0.1:8086/api/ballers', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ name, team })
            })
            .then(response => response.json())
            .then(data => {
                alert('Player added successfully');
                window.location.href = 'index.html';
            })
            .catch(error => {
                console.error('Error:', error);
                alert('Error adding player');
            });
        });
    </script>
</body>
</html>

