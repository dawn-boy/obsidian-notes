# What is it?
An Online multiplayer game app that allows the players to create or join teams, customize their profiles, Code interactively at game play

## The Features

1. Home page
	A page to say what is CompileOrDie

2. Login/Signup page

3. Profile page
	- Customization section
	- Team section
		1. Join a team
		2. Team members info: Name, Status-{ Doozing, Active }
	- Abouts section
		It says the powers and the ability of role.

4. Countdown page

5. Gameplay page
	- Questions section
	- Answer section
		- If the player is 
			1. Hacker, Cyberguardian, Debugger -> CodeBox and Player's choice
			2. Developers -> Only CodeBox

6. End page
	Thanks for playing my game, Parzival.
## Routes
1. /
2. /login
3. /signup
4. /profile
	- /profile/customize
	- /profile/team
	- /profile/abouts
5. /countdown
6. /gameplay
7. /voting
8. /end
## Tech stack
- Routing: React Router
- Styling: plain css or tailwind
- Remote state management: React Router
- UI state management: Redux

## Must've
1. Save user's progress in database lest he losses everything when he closes a session.
2. Auth: Mail verification at signup.
## Nicies
1. history of gamePlays
2. hackers and other players can chat anonymously

## Server-side logic
```json
{
	payload: {
		id: 1,
		question: "Some question here",
		description: "Some desc here"
	},
	
	// showPlayers, showQuestion, onError, 
	action: ""
}
```

1. Registration - POST
```json
{
	payload: {
		username: "actual e-mail for verification",
		password: "password"
	},
	action: "user/register"
}

{
	success: true,
	message: "Please activate your account. Look for us in your mail!"
}
{
	success: false,
	message: "some error"
}
```
- verifyUser(username, password)
- registerUser(username, password)

2. Login - POST
```json
{
	payload: {
		username: "email",
		password: "password"
	},
	action: "user/login"
}

{
	success: true,
	message: "Right this way, sire"
}
{
	success: false,
	message: "User not registered."
}
```
- verifyUser(username, password)
- loginUser(username, password)

3. profile
- getProfile(userId)
- createTeam(userId)
- joinTeam(userId, code)
- getTeam(userId)
- getAbouts() [a simple function]

4. gameplay
- getRole()
- getQuestion()
- sendCode(code)
- getCode()
- getChoice()
- sendChoice(choice)
- verifyCode(code)

5. vote
- vote(byUser, toUser)
- fire(user)

6. loop or end
- var: isGameOn


# Tables

0. history_of_teams
	- id
	- user_id
	- game_id


1. users_table
	- id
	- created_at
	- username
	- name
	- email
	- profile_pic
	- description
	- badges_earned
	- current_team_id
	- status - {online, offline, playing, doozing, undercover}
	- isUndercover
	- last_seen -> { show, invisible if undercover }
	
2. teams_table
	- id
	- team_name
	- team_code
	- created_by_user_id
	- players_id
	- status - {waiting, in-game, finished}
	- history_of_games
	- comments
	- total_hacker_wins
	- total_dev_wins
	
3. questions_table
	- id
	- question
	- description
	- difficulty - {easy, medium, hard}
	- time_limit
	- starter_code
	- expected_output

==4 rounds => ~ 1 cycle==

5. rounds_report
	- id 
	- round_num
	- name
	- player_id
	- question
	- answer
	- isCompilable
6. cycles_report
	- id
	- cycles_id
	- name
	- user_id
	- role
	- chosenOne
	- chosenOneReport 
	
		chosenOneReport based on roles should be like
		- Hacker
			- { isSaved: true, message: "Debugger saved user" } 
			- { isSaved: false, message: "Debugger saved someone else"} 
			- { isSaved: true, message: "Hacker had skill issues, couldn't bug properly"}
		- Debugger
			- { isSaved: true, message: "Debugger is your saviour!"}
			- { isSaved: false, message: "Debugger had skill issues.."}
		- Cyberguardian
			- { isCorrect: true, message: "Cyberguardian knows about he who must not be named."}
			- { isCorrect: false, message: "Cyberguardian is still on the hunt for he who must not be named.."}


7. rounds_table
	- id
	- cycle_Id
	- round_number
	- hacker_report_id - { name, userId, didCodeCompile, chosenOne, isBugged, bugMessage, }
	- cyberguardian_report_id
	- debugger_report_id
	- developer_one_report_id
	- developer_two_report_id
		
8. votes_table
	- id
	- game_id 
	- cycle_id 
	- voter_id
	- target_id
	- vote_type -> { fire, skip }
		
9. cycles_table
	- id
	- game_id 
	- cycle_number
	- votes_id - delete
		
10. games_table
	- id
	- players_role
	- cycles
	- didHackerWin
	- started_at
	- ended_at
	
11. leaderboard_table
	- id
	- user_id
	- total_wins
	- streak
	- total_losses
	- total_games
	- player_rating
	- last_game_at


# Things to do

1. Join/Create a team
	- Team page should show
		1. Team name
		2. Team members - { name, status }
		3. Ready button for the current user - { once clicked it'll be disabled }
		If all the users are ready, game countdown starts
2. each player is assigned a role and the below cycle repeats until we have 
						***==Crew fires the hacker==***
						***==4 members get eleminated==***
	*Round 1*
	- *Hacker and Cyberguardian gets a choice to pick a player*
	- *Developer and debugger gets questions*
	***==We wait till ==***
		***==Everyone finishes up==***
		***==Timer runs out==***
	*Round 2*
	- *everyone Codes*
	- *Debugger gets a choice whom to debug*
	- *Cyberguardian gets his checks*
	- *hacker gets the chosen ones code*
	***==We wait till *==***
		***==Everyone finishes up==***
		***==Timer runs out==***
	*Round 3*
	 - everyone codes
	 - debugger gets the chosen ones code
	***==We wait till *==***
		***==Everyone finishes up==***
		***==Timer runs out==***
	 Round 4 (Voting round)
	 - Voting panel opens up and timer starts
	 - discussion time 
	***==We wait till *==***
		***==Everyone casts their vote or skips==***
		***==Timer runs out==***
	A Cycles results
	- we tell them just enough
		***==IF ANYONE HAS BEEN FIRED. Either by their own hands or by HIS.==***
		nothing else.
	***==We wait till *==***
		***==Everyone casts their vote or skips==***
		***==Timer runs out==***
	***The cycle Continues***

- When the game finishes up, ***we show =="THANKS FOR PLAYING MY GAME, PARZIVAL"***
- then, we show the log of the game. what happened throughout the game ***==WHO KILLED WHOM==***
- a redirect button to get home.


# Process
1. Defining the policies for database for a tighter security




things to do
- ~~dont allow players to go to next question without runing the code atleast once~~
- ~~look what's up with that ready button, it doesn't update the state and takes three clicks to start the game~~
- ~~add a message if the user gets fired because the code didn't compile~~
- ~~waiting pages after elimination round and voting round~~
- ~~vote logic must be improved, right now ==1 vote vs 4 skips fires a player==~~
- ~~set team status~~
- ~~check who's eleminated after voting~~
- ~~check for conditions during the start of each cycle~~ 
- ~~show to end page~~
- ~~dont allow players while the team is playing~~
- ~~create team~~
- ~~cascade delete team~~
- ~~the end page message is wrong~~
- ~~add navigation links~~
- ~~add the hacker name at game end~~
- get the timer logic in

- check for proper code, no cheating 
- make those reports
- add input capabilities
