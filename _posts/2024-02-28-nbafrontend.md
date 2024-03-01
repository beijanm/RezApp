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
        li { background-color: #fff; margin-bottom: 10px; padding: 10px; border: 1px solid #ddd; display: flex; justify-content: space-between; align-items: center; }
        button { cursor: pointer; background-color: #007bff; color: #fff; border: none; padding: 5px 10px; border-radius: 5px; margin-left: 5px; }
        button:hover { background-color: #0056b3; }
        .statsBtn { background-color: #555; }
        .statsBtn:hover { background-color: #d40000; }
        #playerStats { background-color: #fff; border: 1px solid #ddd; padding: 20px; margin-top: 20px; }
        .actionLink { display: inline-block; margin-top: 20px; padding: 10px 15px; background-color: #007bff; color: #fff; text-decoration: none; border-radius: 5px; }
        .actionLink:hover { background-color: #0056b3; text-decoration: none; color: #fff; }
    </style>
</head>
<body>
    <h1>NBA Player List</h1>
    <ul id="playerList"></ul>
    <h2>Player Stats</h2>
    <div id="playerStats"></div>
    <button class="actionLink" onclick="location.href='http://127.0.0.1:4200/RezApp//2024/02/29/Add_Player.html'">Add a New Player</button>
    <button class="actionLink" onclick="location.href='http://127.0.0.1:4200/RezApp//2024/02/29/Add_Stats.html'">Add Player Stats</button>

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

                        const playerNameSpan = document.createElement('span');
                        playerNameSpan.textContent = player.name;
                        playerNameSpan.style.cursor = 'pointer';
                        playerNameSpan.addEventListener('click', () => fetchPlayerStats(player.id));
                        playerItem.appendChild(playerNameSpan);

                        const editStatsBtn = document.createElement('button');
                        editStatsBtn.textContent = 'Edit Stats';
                        editStatsBtn.className = 'editStatsBtn';
                        editStatsBtn.addEventListener('click', () => showEditStatsForm(player.id));
                        playerItem.appendChild(editStatsBtn);

                        const deleteBtn = document.createElement('button');
                        deleteBtn.textContent = 'Delete';
                        deleteBtn.className = 'deleteBtn';
                        deleteBtn.addEventListener('click', () => deletePlayer(player.id));
                        playerItem.appendChild(deleteBtn);

                        playerList.appendChild(playerItem);
                    });
                })
                .catch(error => console.error('Error:', error));
        }

        function fetchPlayerStats(playerId) {
            // Fetch player stats logic
        }


        function deletePlayer(playerId) {
            // Delete player logic
        }

        function showEditStatsForm(playerId) {
            // Show edit stats form logic
        }
    </script>
</body>
</html>


