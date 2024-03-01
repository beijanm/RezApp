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
    <div id="editStatsContainer"></div>
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
                        playerItem.textContent = player.name; // Set the player name as the list item's text

                        // Wrap the player's name in a span for click handling
                        const playerNameSpan = document.createElement('span');
                        playerNameSpan.textContent = player.name;
                        playerNameSpan.style.cursor = 'pointer';
                        playerNameSpan.onclick = () => fetchPlayerStats(player.id);
                        
                        // Clear existing content and append the clickable name span
                        playerItem.innerHTML = '';
                        playerItem.appendChild(playerNameSpan);

                        // Create and append the "Edit Stats" button next to the player's name
                        const editStatsBtn = document.createElement('button');
                        editStatsBtn.textContent = 'Edit Stats';
                        editStatsBtn.className = 'editStatsBtn'; // Ensure this class exists and styles the button appropriately
                        editStatsBtn.onclick = () => showEditStatsForm(player.id);

                        // Create and append the "Delete" button
                        const deleteBtn = document.createElement('button');
                        deleteBtn.textContent = 'Delete';
                        deleteBtn.className = 'deleteBtn';
                        deleteBtn.onclick = () => deletePlayer(player.id);

                        playerItem.appendChild(editStatsBtn);
                        playerItem.appendChild(deleteBtn);
                        playerList.appendChild(playerItem);
                    });
                })
                .catch(error => console.error('Error:', error));
        }


        function fetchPlayerStats(playerId) {
            fetch(`http://127.0.0.1:8086/api/ballers/${playerId}/stats`)
                .then(response => response.json())
                .then(stats => {
                    const statsContainer = document.getElementById('playerStats');
                    statsContainer.innerHTML = ''; // Clear existing stats
                    if (stats && stats.length > 0) {
                        stats.forEach(stat => {
                            const statDetail = document.createElement('p');
                            statDetail.textContent = `Points Per Game: ${stat.points_per_game}, Assists Per Game: ${stat.assists_per_game}, Rebounds Per Game: ${stat.rebounds_per_game}`;
                            statsContainer.appendChild(statDetail);
                        });
                    } else {
                        statsContainer.textContent = 'No stats available for this player.';
                    }
                })
                .catch(error => console.error('Error fetching player stats:', error));
        }


        function deletePlayer(playerId) {
            fetch(`http://127.0.0.1:8086/api/ballers/${playerId}`, { method: 'DELETE' })
            .then(response => {
                if (!response.ok) {
                    throw new Error('Error deleting player');
                }
                return response.json();
            })
            .then(data => console.log(data))
            .catch(error => console.error('Error:', error));
        }



    </script>
</body>
</html>


