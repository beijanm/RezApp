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
    <div id="editStatsContainer"></div>
    <title>NBA Player Stats</title>
    <style>
        .editStatsBtn, .deleteBtn {
            cursor: pointer;
            background-color: #555;
            color: #fff;
            border: none;
            padding: 5px 10px;
            margin-left: 5px;
            border-radius: 5px;
        }
        .editStatsBtn:hover, .deleteBtn:hover {
            background-color: #d40000;
        }

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
    <a href="http://127.0.0.1:4200/RezApp//2024/02/29/Add_Stats.html">Add a Player Stats</a>

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
                        editStatsBtn.className = 'deleteBtn'; // Ensure this class exists and styles the button appropriately
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


        function showEditStatsForm(playerId) {
            // Assuming you have a div with id="editStatsContainer" to display the edit form
            const editStatsContainer = document.getElementById('editStatsContainer');
            editStatsContainer.innerHTML = `
                <h3>Edit Stats for Player ID: ${playerId}</h3>
                <form id="editStatsForm">
                    <input type="number" id="pointsPerGame" placeholder="Points per game" required>
                    <input type="number" id="assistsPerGame" placeholder="Assists per game" required>
                    <input type="number" id="reboundsPerGame" placeholder="Rebounds per game" required>
                    <button type="submit">Update Stats</button>
                </form>
            `;

            // Add an event listener to the form for handling the submission
            document.getElementById('editStatsForm').addEventListener('submit', function(e) {
                e.preventDefault();
                updateStats(playerId);
            });
        }

        function updateStats(playerId) {
            // Gather the input values
            const points = document.getElementById('pointsPerGame').value;
            const assists = document.getElementById('assistsPerGame').value;
            const rebounds = document.getElementById('reboundsPerGame').value;

            // Make a PUT request to update the stats
            fetch(`http://127.0.0.1:8086/api/ballers/${playerId}/stats`, {
                method: 'PUT', // Assuming your backend supports PUT for updating
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({
                    points_per_game: points,
                    assists_per_game: assists,
                    rebounds_per_game: rebounds
                })
            })
            .then(response => {
                if (response.ok) {
                    alert('Stats updated successfully');
                    // Optionally, refresh stats or player list here
                } else {
                    alert('Error updating stats');
                }
            })
            .catch(error => {
                console.error('Error:', error);
                alert('Error updating stats');
            });
        }


    </script>
</body>
</html>
