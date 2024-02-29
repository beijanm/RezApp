---
toc: false
comments: false 
layout: post
title: Basic NBA
type: hacks
courses: { compsci: {week: 5} }
---


<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Player Stats</title>
</head>
<body>
    <h1>Player List</h1>
    <ul id="playerList"></ul>

    <h2>Player Stats</h2>
    <div id="playerStats"></div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            fetchPlayers();
        });

        function fetchPlayers() {
            fetch('http://127.0.0.1:8086/api/ballers') // Adjust this URL to your API endpoint
                .then(response => response.json())
                .then(players => {
                    const playerList = document.getElementById('playerList');
                    playerList.innerHTML = ''; // Clear the list

                    players.forEach(player => {
                        const playerItem = document.createElement('li');
                        playerItem.textContent = player.name; // Adjust based on your data structure
                        playerItem.setAttribute('data-player-id', player.id); // Add player ID as data attribute
                        
                        // Click event to fetch player stats
                        playerItem.addEventListener('click', () => {
                            fetchPlayerStats(player.id);
                        });

                        playerList.appendChild(playerItem);
                    });
                })
                .catch(error => console.error('Error fetching players:', error));
        }

        function fetchPlayerStats(playerId) {
            fetch(`http://127.0.0.1:8086/api/ballers/${playerId}/stats`) // Adjust this URL to your API endpoint
                .then(response => response.json())
                .then(data => {
                    displayPlayerStats(data);
                })
                .catch(error => console.error('Error fetching player stats:', error));
        }

        function displayPlayerStats(data) {
            const statsContainer = document.getElementById('playerStats');
            statsContainer.innerHTML = ''; // Clear existing stats

            // Assuming 'data' structure includes player info and stats array
            const playerInfo = `
                <h3>${data.player.name} (${data.player.team})</h3>
                <p>Date of Birth: ${data.player.dob}</p>
            `;
            statsContainer.innerHTML += playerInfo;

            if (data.stats && data.stats.length > 0) {
                const statsList = data.stats.map(stat => `
                    <li>Points Per Game: ${stat.points_per_game}, Assists Per Game: ${stat.assists_per_game}, Rebounds Per Game: ${stat.rebounds_per_game}</li>
                `).join('');
                statsContainer.innerHTML += `<ul>${statsList}</ul>`;
            } else {
                statsContainer.innerHTML += '<p>No stats available for this player.</p>';
            }
        }
    </script>
</body>
</html>
