<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NBA Teams and Starting Lineups</title>
    <style>
        body {
            font-family: Arial, sans-serif;
        }

        h1, h2, h3 {
            color: #333;
        }

        #western-conference, #eastern-conference {
            margin-bottom: 20px;
        }

        ul {
            list-style-type: none;
            padding: 0;
        }

        li {
            margin-bottom: 5px;
        }

        .team {
            font-weight: bold;
            margin-bottom: 10px;
            position: relative;
        }

        .favorite-button {
            position: absolute;
            right: 0;
            top: 0;
            background-color: #f8f8f8;
            border: none;
            padding: 5px 10px;
            border-radius: 5px;
            cursor: pointer;
        }

        .favorite-button:hover {
            background-color: #e0e0e0;
        }
    </style>
</head>
<body>
    <h1>NBA Teams and Starting Lineups</h1>

    <h2>Western Conference Top 10 Teams:</h2>
    <div id="western-conference">
        <h3>Western Conference</h3>
        <ul id="western-teams"></ul>
    </div>

    <h2>Eastern Conference Top 10 Teams:</h2>
    <div id="eastern-conference">
        <h3>Eastern Conference</h3>
        <ul id="eastern-teams"></ul>
    </div>

    <script>
        class NBAPlayer {
            constructor(name, position) {
                this.name = name;
                this.position = position;
            }
        }

        class NBATeam {
            constructor(name, conference, players) {
                this.name = name;
                this.conference = conference;
                this.players = players; // List of NBAPlayer objects representing the starting lineup
            }
        }

        // Define NBA players for each team
        const playersWest = {
            "LAL": [new NBAPlayer("LeBron James", "SF"), new NBAPlayer("Anthony Davis", "PF"), new NBAPlayer("Russell Westbrook", "PG"), new NBAPlayer("Malcolm Brogdon", "SG"), new NBAPlayer("Dwight Howard", "C")],
            "GSW": [new NBAPlayer("Stephen Curry", "PG"), new NBAPlayer("Klay Thompson", "SG"), new NBAPlayer("Andrew Wiggins", "SF"), new NBAPlayer("Draymond Green", "PF"), new NBAPlayer("James Wiseman", "C")]
            // Add other Western Conference teams and their starting players here...
        };

        const playersEast = {
            "BKN": [new NBAPlayer("Kevin Durant", "SF"), new NBAPlayer("James Harden", "SG"), new NBAPlayer("Kyrie Irving", "PG"), new NBAPlayer("Blake Griffin", "PF"), new NBAPlayer("LaMarcus Aldridge", "C")],
            "MIL": [new NBAPlayer("Giannis Antetokounmpo", "PF"), new NBAPlayer("Khris Middleton", "SF"), new NBAPlayer("Jrue Holiday", "PG"), new NBAPlayer("Brook Lopez", "C"), new NBAPlayer("Grayson Allen", "SG")]
            // Add other Eastern Conference teams and their starting players here...
        };

        // Define NBA teams with their respective conference and starting players
        const westernConferenceTeams = [
            new NBATeam("Los Angeles Lakers", "West", playersWest["LAL"]),
            new NBATeam("Golden State Warriors", "West", playersWest["GSW"])
            // Add other Western Conference teams here...
        ];

        const easternConferenceTeams = [
            new NBATeam("Brooklyn Nets", "East", playersEast["BKN"]),
            new NBATeam("Milwaukee Bucks", "East", playersEast["MIL"])
            // Add other Eastern Conference teams here...
        ];

        // Function to display starting lineup for a team
        function displayStartingLineup(team, conference) {
            const teamElement = document.createElement("li");
            teamElement.classList.add("team");
            teamElement.textContent = `${team.name} (${conference}) - Starting Lineup: `;
            const lineupElement = document.createElement("ul");
            team.players.forEach(player => {
                const playerElement = document.createElement("li");
                playerElement.textContent = `${player.name} - ${player.position}`;
                lineupElement.appendChild(playerElement);
            });
            teamElement.appendChild(lineupElement);

            // Add favorite button
            const favoriteButton = document.createElement("button");
            favoriteButton.textContent = "Favorite";
            favoriteButton.classList.add("favorite-button");
            teamElement.appendChild(favoriteButton);

            return teamElement;
        }

        // Display starting lineup for each team in the Western Conference
        const westernTeamsList = document.getElementById("western-teams");
        westernConferenceTeams.forEach(team => {
            const teamElement = displayStartingLineup(team, team.conference);
            westernTeamsList.appendChild(teamElement);
        });

        // Display starting lineup for each team in the Eastern Conference
        const easternTeamsList = document.getElementById("eastern-teams");
        easternConferenceTeams.forEach(team => {
            const teamElement = displayStartingLineup(team, team.conference);
            easternTeamsList.appendChild(teamElement);
        });
    </script>
</body>
</html>
