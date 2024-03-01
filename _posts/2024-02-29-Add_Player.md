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
        body { font-family: Arial, sans-serif; background-color: #f0f0f0; padding: 20px; }
        form { margin-bottom: 20px; }
        input, button { padding: 10px; margin-right: 5px; border-radius: 5px; border: 1px solid #ddd; }
        button { cursor: pointer; background-color: #007bff; color: #fff; border: none; }
        button:hover { background-color: #0056b3; }
        a { display: inline-block; margin-top: 20px; color: #007bff; text-decoration: none; }
        a:hover { text-decoration: underline; }
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

