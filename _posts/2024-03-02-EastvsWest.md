---
toc: false
comments: false 
layout: base
title: EastvsWest
type: hacks
courses: { compsci: {week: 5} }
---

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NBA Teams and Starting Lineups</title>
</head>
<body>
    <h1>NBA Teams and Starting Lineups</h1>

    <h2>Top 10 Teams in the Western Conference:</h2>
    <pre>
        <code>
            # Define the top 10 teams in the Western Conference
            western_teams = {
                "Los Angeles Lakers": ["LeBron James", "Russell Westbrook", "Anthony Davis", "Kent Bazemore", "Dwight Howard"],
                "Golden State Warriors": ["Stephen Curry", "Klay Thompson", "Andrew Wiggins", "Draymond Green", "Kevon Looney"],
                "Phoenix Suns": ["Chris Paul", "Devin Booker", "Mikal Bridges", "Jae Crowder", "Deandre Ayton"],
                "Utah Jazz": ["Mike Conley", "Donovan Mitchell", "Bojan Bogdanovic", "Royce O'Neale", "Rudy Gobert"],
                "Denver Nuggets": ["Jamal Murray", "Will Barton", "Michael Porter Jr.", "Aaron Gordon", "Nikola Jokic"],
                "Dallas Mavericks": ["Luka Doncic", "Tim Hardaway Jr.", "Dorian Finney-Smith", "Kristaps Porzingis", "Dwight Powell"],
                "Memphis Grizzlies": ["Ja Morant", "Dillon Brooks", "Kyle Anderson", "Jaren Jackson Jr.", "Steven Adams"],
                "Minnesota Timberwolves": ["D'Angelo Russell", "Malik Beasley", "Anthony Edwards", "Jaden McDaniels", "Karl-Anthony Towns"],
                "Los Angeles Clippers": ["Paul George", "Reggie Jackson", "Nicolas Batum", "Marcus Morris Sr.", "Ivica Zubac"],
                "Portland Trail Blazers": ["Damian Lillard", "CJ McCollum", "Norman Powell", "Robert Covington", "Jusuf Nurkic"]
            }
            
            # Print the top 10 teams in the Western Conference along with their starting lineups
            print("Top 10 Teams in the Western Conference:")
            for team, lineup in western_teams.items():
                print(f"\n{team}:")
                print("Starters:")
                for player in lineup:
                    print(player)
        </code>
    </pre>

    <h2>Top 10 Teams in the Eastern Conference:</h2>
    <pre>
        <code>
            # Define the top 10 teams in the Eastern Conference
            eastern_teams = {
                "Brooklyn Nets": ["Kyrie Irving", "James Harden", "Joe Harris", "Kevin Durant", "LaMarcus Aldridge"],
                "Milwaukee Bucks": ["Jrue Holiday", "Donte DiVincenzo", "Khris Middleton", "Giannis Antetokounmpo", "Brook Lopez"],
                "Chicago Bulls": ["Lonzo Ball", "Zach LaVine", "DeMar DeRozan", "Patrick Williams", "Nikola Vucevic"],
                "Miami Heat": ["Kyle Lowry", "Duncan Robinson", "Jimmy Butler", "PJ Tucker", "Bam Adebayo"],
                "Philadelphia 76ers": ["Tyrese Maxey", "Seth Curry", "Danny Green", "Tobias Harris", "Joel Embiid"],
                "Charlotte Hornets": ["LaMelo Ball", "Terry Rozier", "Kelly Oubre Jr.", "Miles Bridges", "Mason Plumlee"],
                "Cleveland Cavaliers": ["Darius Garland", "Collin Sexton", "Isaac Okoro", "Evan Mobley", "Jarrett Allen"],
                "Atlanta Hawks": ["Trae Young", "Bogdan Bogdanovic", "Cam Reddish", "John Collins", "Clint Capela"],
                "Toronto Raptors": ["Fred VanVleet", "Gary Trent Jr.", "OG Anunoby", "Pascal Siakam", "Precious Achiuwa"],
                "Washington Wizards": ["Spencer Dinwiddie", "Bradley Beal", "Kentavious Caldwell-Pope", "Kyle Kuzma", "Daniel Gafford"]
            }

            # Print the top 10 teams in the Eastern Conference along with their starting lineups
            print("Top 10 Teams in the Eastern Conference:")
            for team, lineup in eastern_teams.items():
                print(f"\n{team}:")
                print("Starters:")
                for player in lineup:
                    print(player)
        </code>
    </pre>
</body>
</html>
