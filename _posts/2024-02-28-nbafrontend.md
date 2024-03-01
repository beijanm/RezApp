---
toc: false
comments: false 
layout: base
title: Basic NBA
type: hacks
courses: { compsci: {week: 5} }
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>NBA Player Stats</title>
    <style>
        body { font-family: Arial, sans-serif; background-color: #f0f0f0; padding: 20px; }
        h1, h2 { color: #d40000; }
        ul { list-style-type: none; padding: 0; }
        li { background-color: #fff; margin-bottom: 10px; padding: 10px; border: 1px solid #ddd; cursor: pointer; display: flex; justify-content: space-between; align-items: center; }
        li:hover { background-color: #d40000; color: #fff; }
        .deleteBtn { cursor: pointer; background-color: #555; color: #fff; border: none; padding: 5px 10px; border-radius: 5px; }
        .deleteBtn:hover { background-color: #d40000; }
        #playerStats { background-color: #fff; border: 1px solid #ddd; padding: 20px; }
        a { display: inline-block; margin-top: 20px; color: #007bff; text-decoration: none; }
        a:hover { text-decoration: underline; }
    </style>
</head>
<body>
    <h1>NBA Player List</h1>
    <ul id="playerList"></ul>
    <h2>Player Stats</h2>
    <div id="playerStats"></div>
    <a href="http://127.0.0.1:4200/RezApp//2024/02/29/Add_Player.html">Add a New Player</a>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            fetchPlayers();
        });

        function fetchPlayers() {
            fetch('http://127.0.0.1:8086/api/ballers')
                .then(response => response.json())
                .then(players => {
                    const playerList = document.getElementById('playerList');
                    playerList.innerHTML = '';
                    players.forEach(player => {
                        const playerItem = document.createElement('li');
                        playerItem.textContent = player.name;
                        const deleteBtn = document.createElement('button');
                        deleteBtn.textContent = 'Delete';
                        deleteBtn.className = 'deleteBtn';
                        deleteBtn.onclick = () => deletePlayer(player.id);
                        playerItem.appendChild(deleteBtn);
                        playerItem.addEventListener('click', (event) => {
                            if (event.target !== deleteBtn) {
                                fetchPlayerStats(player.id);
                            }
                        });
                        playerList.appendChild(playerItem);
                    });
                })
                .catch(error => console.error('Error:', error));
        }

        function fetchPlayerStats(playerId) {
            // Placeholder for fetchPlayerStats implementation
        }

        function deletePlayer(playerId) {
            // Placeholder for deletePlayer implementation
        }
    </script>
</body>
</html>
