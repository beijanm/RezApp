---
toc: false
comments: false 
layout: base
title: Team Assortment
type: hacks
courses: { compsci: {week: 5} }
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>NBA Teams</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f8f8f8;
            color: #333;
            margin: 0;
            padding: 0;
        }

        h1 {
            text-align: center;
            color: #e74c3c;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            background-color: #fff;
        }

        th, td {
            border: 1px solid #ddd;
            padding: 15px;
            text-align: left;
        }

        th {
            background-color: #e74c3c;
            color: white;
        }

        td {
            background-color: #fff;
        }

        button {
            background-color: #e74c3c;
            border: none;
            color: white;
            padding: 8px 16px;
            text-align: center;
            text-decoration: none;
            display: inline-block;
            font-size: 14px;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        button:hover {
            background-color: #c0392b;
        }
    </style>
</head>
<body>
    <h1>NBA Teams</h1>
    <table id="nbaTeamsTable">
        <thead>
            <tr>
                <th>Team</th>
                <th>Player 1</th>
                <th>Player 2</th>
                <th>Player 3</th>
                <th>Player 4</th>
                <th>Player 5</th>
                <th>Favorite</th>
            </tr>
        </thead>
        <tbody>
            <!-- Team rows will be added here by JavaScript -->
        </tbody>
    </table>

    <script>
        const teams = [
            { name: "Los Angeles Lakers", players: ["LeBron James", "Anthony Davis", "Russell Westbrook", "Dwight Howard", "Kentavious Caldwell-Pope"] },
            { name: "Golden State Warriors", players: ["Stephen Curry", "Klay Thompson", "Draymond Green", "Andrew Wiggins", "James Wiseman"] },
            { name: "Brooklyn Nets", players: ["Kevin Durant", "James Harden", "Kyrie Irving", "Joe Harris", "DeAndre Jordan"] },
            // Add more teams with players here
            { name: "Chicago Bulls", players: ["Zach LaVine", "Nikola Vucevic", "Lonzo Ball", "DeMar DeRozan", "Patrick Williams"] },
            { name: "Miami Heat", players: ["Jimmy Butler", "Bam Adebayo", "Kyle Lowry", "Tyler Herro", "Duncan Robinson"] },
            { name: "Dallas Mavericks", players: ["Luka Doncic", "Kristaps Porzingis", "Tim Hardaway Jr.", "Jalen Brunson", "Dwight Powell"] },
            // Add more teams with players here
        ];

        const favorites = new Set();

        const tableBody = document.getElementById("nbaTeamsTable").getElementsByTagName("tbody")[0];

        teams.forEach(team => {
            const row = tableBody.insertRow();
            row.insertCell().textContent = team.name;
            team.players.forEach(player => {
                row.insertCell().textContent = player;
            });

            const favoriteCell = row.insertCell();
            const favoriteButton = document.createElement("button");
            favoriteButton.textContent = "Favorite";
            favoriteButton.onclick = function() {
                if (favorites.has(team.name)) {
                    favorites.delete(team.name);
                    favoriteButton.textContent = "Favorite";
                } else {
                    favorites.add(team.name);
                    favoriteButton.textContent = "Unfavorite";
                }
            };
            favoriteCell.appendChild(favoriteButton);
        });
    </script>
</body>
</html>