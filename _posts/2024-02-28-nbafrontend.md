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
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #282c34;
            color: #abb2bf;
            padding: 20px;
            margin: 0;
        }
        h1, h2 {
            color: #61afef;
        }
        ul {
            list-style-type: none;
            padding: 0;
        }
        li {
            background-color: #3a3f4b;
            margin-bottom: 10px;
            padding: 10px;
            border-radius: 8px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
            transition: transform 0.2s;
        }
        li:hover {
            transform: scale(1.02);
        }
        button {
            cursor: pointer;
            background-color: #61afef;
            color: white;
            border: none;
            padding: 5px 10px;
            border-radius: 5px;
            transition: background-color 0.3s;
        }
        button:hover {
            background-color: #467ca0;
        }
        .editStatsBtn, .deleteBtn {
            background-color: #e06c75;
            margin-left: 10px;
        }
        .editStatsBtn:hover, .deleteBtn:hover {
            background-color: #be5046;
        }
        #playerStats {
            background-color: #3a3f4b;
            border-radius: 8px;
            padding: 20px;
            margin-top: 20px;
            box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
        }
        .actionLink {
            display: inline-block;
            margin-top: 20px;
            padding: 10px 15px;
            background-color: #98c379;
            color: white;
            text-decoration: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        .actionLink:hover {
            background-color: #829b67;
        }
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


