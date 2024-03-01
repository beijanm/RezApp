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
            font-family: Arial, sans-serif;
            background-color: #333; /* Dark background */
            color: #fff; /* Light text */
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        .container {
            max-width: 600px; /* Adjust based on your content */
            width: 100%;
        }
        h1, h2 {
            color: #d40000;
            text-align: center;
        }
        ul {
            list-style-type: none;
            padding: 0;
        }
        li {
            background-color: #555; /* Darker element background */
            color: #fff;
            margin-bottom: 10px;
            padding: 10px;
            border-radius: 5px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        button {
            cursor: pointer;
            background-color: #007bff;
            color: #fff;
            border: none;
            padding: 5px 10px;
            border-radius: 5px;
        }
        button:hover {
            background-color: #0056b3;
        }
        .stats, .editStatsForm {
            display: none;
            background-color: #444;
            padding: 10px;
            margin-top: 10px;
            border-radius: 5px;
        }
        .show {
            display: block;
        }
        label, input {
            color: #fff;
        }
        input {
            background-color: #555;
            border: 1px solid #777;
            border-radius: 5px;
            padding: 5px;
            color: #ddd;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>NBA Player Stats</h1>
        <ul id="playerList"></ul>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', fetchPlayers);

        function fetchPlayers() {
            fetch('http://127.0.0.1:8086/api/ballers')
                .then(response => response.json())
                .then(players => {
                    const playerList = document.getElementById('playerList');
                    playerList.innerHTML = '';
                    players.forEach(player => {
                        const li = document.createElement('li');
                        li.innerHTML = `${player.name} - ${player.team} 
                                        <button onclick="deletePlayer(${player.id})">Delete</button>
                                        <button onclick="toggleStatsForm(${player.id})">Edit Stats</button>`;

                        const statsDiv = document.createElement('div');
                        statsDiv.id = `stats-${player.id}`;
                        statsDiv.className = 'stats';
                        statsDiv.innerHTML = `<h3>Stats for ${player.name}</h3>`;

                        const editStatsForm = document.createElement('div');
                        editStatsForm.id = `editStats-${player.id}`;
                        editStatsForm.className = 'editStatsForm';
                        editStatsForm.innerHTML = `
                            <h3>Edit Stats for ${player.name}</h3>
                            <form onsubmit="event.preventDefault(); updateStats(${player.id});">
                                <label for="points-${player.id}">Points Per Game:</label>
                                <input type="number" id="points-${player.id}" required><br>
                                <label for="assists-${player.id}">Assists Per Game:</label>
                                <input type="number" id="assists-${player.id}" required><br>
                                <label for="rebounds-${player.id}">Rebounds Per Game:</label>
                                <input type="number" id="rebounds-${player.id}" required><br>
                                <button type="submit">Update Stats</button>
                            </form>
                        `;

                        li.appendChild(statsDiv);
                        li.appendChild(editStatsForm);
                        playerList.appendChild(li);
                    });
                })
                .catch(error => console.error('Error fetching players:', error));
        }

        function deletePlayer(playerId) {
            fetch(`http://127.0.0.1:8086/api/ballers/${playerId}`, { method: 'DELETE' })
                .then(response => {
                    if (!response.ok) throw new Error('Failed to delete player');
                    fetchPlayers(); // Refresh the player list
                })
                .catch(error => console.error('Error deleting player:', error));
        }

        function toggleStatsForm(playerId) {
            const statsDiv = document.getElementById(`stats-${playerId}`);
            const editStatsForm = document.getElementById(`editStats-${playerId}`);
            statsDiv.classList.toggle('show');
            editStatsForm.classList.toggle('show');
            // Fetch and display stats if opening
            if (editStatsForm.classList.contains('show')) {
                fetch(`http://127.0.0.1:8086/api/ballers/${playerId}/stats`)
                    .then(response => response.json())
                    .then(stats => {
                        // Assuming the API returns an array of stats, and you're interested in the latest/first
                        const latestStats = stats[0] || {};
                        document.getElementById(`points-${playerId}`).value = latestStats.points_per_game || 0;
                        document.getElementById(`assists-${playerId}`).value = latestStats.assists_per_game || 0;
                        document.getElementById(`rebounds-${playerId}`).value = latestStats.rebounds_per_game || 0;
                    })
                    .catch(error => console.error('Error fetching stats:', error));
            }
        }

        function updateStats(playerId) {
            const points = document.getElementById(`points-${playerId}`).value;
            const assists = document.getElementById(`assists-${playerId}`).value;
            const rebounds = document.getElementById(`rebounds-${playerId}`).value;

            fetch(`http://127.0.0.1:8086/api/ballers/${playerId}/stats`, {
                method: 'PUT', // Assuming your API uses PUT to update stats
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ points_per_game: points, assists_per_game: assists, rebounds_per_game: rebounds })
            })
                .then(response => {
                    if (!response.ok) throw new Error('Failed to update stats');
                    alert('Stats updated successfully');
                })
                .catch(error => console.error('Error updating stats:', error));
        }
    </script>
</body>
</html>
