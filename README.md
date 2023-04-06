# Analysis of *Final Fantasy XIV's* Grand Company System
Hello! My name is Jason Toro-McCue, a junior data analyst in training. While learning more and more about the data analyst sphere, I wanted to practice some of my skills and analyze something important to me.  
*Final Fantasy XIV* is an MMORPG set in the world of Eorzea. This fictional realm is full of all sorts of fantastical creatures, lands, and people. While exploring this world, players will have the opportunity to meet up with other players and perform multiple cooperative – and competitive – tasks.  
One system that always seemed underdeveloped to me was the Grand Company system. There are three Grand Companies, each affiliated with a city of Eorzea: The Maelstrom with Limsa Lominsa, the Immortal Flame with Ul'dah, and the Order of the Twin Adder with Gridania. I've always put this mechanic to the side of my *Final Fantasy XIV* experience, but now I wanted to put my newly acquired data analytics skills to the test!

## Business Task
My hypothetical business task was to answer three topics regarding *FFXIV's* Grand Companies:  
1. Which grand company was the most populous? Which character race was each Grand Company the most likely to attract?
2. Which grand company was holding onto players into the endgame? Were there differences between combat and non-combat classes?
3. How in-depth were characters getting into the Grand Company Rank system?  
By answering questions regarding these three topics, I am hoping to get a more deep connection to the Grand Company system.

## The Database: *FFXIV Census*
The database to be used in this project was helpfully provided for me. The website [FFXIV Census](https://ffxivcensus.com/) is a potent resource, offering a database that can be imported directly into MySQL. For the purposes of this project, the database will be concerning the March 2023 character population of *FFXIV*.

Code and documentation copyright 2015-2018 Jonathan Price & Peter Reid, Code and documentation released under the BSD 2-Clause "Simplified" License.

### How Does the Database Work?
FFXIV Census functions by running code through the [FFXIV Lodestone](https://na.finalfantasyxiv.com/lodestone/), a public repository of information for *FFXIV* characters. The code looks through each character on the website, analyses the information that Square Enix provides for each player, and uploads it to a single-table database. The table includes information like character ID, name, gender, race, class levels, minions, mounts, and more. By tracking minions and mounts, the database can also effectively track player progress through the story, since major questlines in *FFXIV* reward their players by delivering minions or mounts.
