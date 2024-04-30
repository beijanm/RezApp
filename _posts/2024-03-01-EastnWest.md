Sure! I've modified the code to showcase three teams from each conference, and when you click the "Favorite" button, it toggles between "Favorite" and "Unfavorite" for each team individually. Here's the updated code:

```html
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

    <h2>Western Conference Top 3 Teams:</h2>
    <div id="western-conference">
        <h3>Western Conference</h3>
        <ul id="western-teams"></ul>
    </div>

    <h2>Eastern Conference Top 3 Teams:</h2>
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
                this.isFavorite = false;
            }

            toggleFavorite() {
                this.isFavorite = !this.isFavorite;
            }
        }

        // Define NBA players for each team
        const playersWest = {
            "LAL": [new NBAPlayer("LeBron James", "SF"), new NBAPlayer("Anthony Davis", "PF"), new NBAPlayer("Russell Westbrook", "PG"), new NBAPlayer("Malcolm Brogdon", "SG"), new NBAPlayer("Dwight Howard", "C")],
            "GSW": [new NBAPlayer("Stephen Curry", "PG"), new NBAPlayer("Klay Thompson", "SG"), new NBAPlayer("Andrew Wiggins", "SF"), new NBAPlayer("Draymond Green", "PF"), new NBAPlayer("James Wiseman", "C")],
            "PHX": [new NBAPlayer("Chris Paul", "PG"), new NBAPlayer("Devin Booker", "SG"), new NBAPlayer("Mikal Bridges", "SF"), new NBAPlayer("Jae Crowder", "PF"), new NBAPlayer("Deandre Ayton", "C")]
            // Add other Western Conference teams and their starting players here...
        };

        const playersEast = {
            "BKN": [new NBAPlayer("Kevin Durant", "SF"), new NBAPlayer("James Harden", "SG"), new NBAPlayer("Kyrie Irving", "PG"), new NBAPlayer("Blake Griffin", "PF"), new NBAPlayer("LaMarcus Aldridge", "C")],
            "MIL": [new NBAPlayer("Giannis Antetokounmpo", "PF"), new NBAPlayer("Khris Middleton", "SF"), new NBAPlayer("Jrue Holiday", "PG"), new NBAPlayer("Brook Lopez", "C"), new NBAPlayer("Grayson Allen", "SG")],
            "PHI": [new NBAPlayer("Tyrese Maxey", "PG"), new NBAPlayer("Seth Curry", "SG"), new NBAPlayer("Danny Green", "SF"), new NBAPlayer("Tobias Harris", "PF"), new NBAPlayer("Joel Embiid", "C")]
            // Add other Eastern Conference teams and their starting players here...
        };

        // Define NBA teams with their respective conference and starting players
        const westernConferenceTeams = [
            new NBATeam("Los Angeles Lakers", "West", playersWest["LAL"]),
            new NBATeam("Golden State Warriors", "West", playersWest["GSW"]),
            new NBATeam("Phoenix Suns", "West", playersWest["PHX"])
            // Add other Western Conference teams here...
        ];

        const easternConferenceTeams = [
            new NBATeam("Brooklyn Nets", "East", playersEast["BKN"]),
            new NBATeam("Milwaukee Bucks", "East", playersEast["MIL"]),
            new NBATeam("Philadelphia 76ers", "East", playersEast["PHI"])
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
            favoriteButton.textContent = team.isFavorite ? "Unfavorite" : "Favorite";
            favoriteButton.classList.add("favorite-button");
            favoriteButton.addEventListener("click", () => {
                team.toggleFavorite();
                favoriteButton.textContent = team.isFavorite ? "Unfavorite" : "Favorite";
            });
            teamElement.appendChild(favoriteButton);

            return teamElement;
        }

        // Display starting lineup for each team in the Western Conference
        const westernTeamsList = document.getElementById("western-teams");
        westernConferenceTeams.slice(0, 3).forEach(team => {
            const teamElement = displayStartingLineup(team, team.conference);
            westernTeamsList.appendChild(teamElement);
