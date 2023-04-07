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
For clarification, a standard *FFXIV* account may have up to eight characters. However, most players tend to only have a few characters.

## The Database: *FFXIV Census*
The database to be used in this project was helpfully provided for me. The website [FFXIV Census](https://ffxivcensus.com/) is a potent resource, offering a database that can be imported directly into MySQL. For the purposes of this project, the database will be concerning the March 2023 character population of *FFXIV*. The website's analysis of the data was not used for my own analysis.

Code and documentation copyright 2015-2018 Jonathan Price & Peter Reid, Code and documentation released under the BSD 2-Clause "Simplified" License.

### How Does the Database Work?
FFXIV Census functions by running code through the [FFXIV Lodestone](https://na.finalfantasyxiv.com/lodestone/), a public repository of information for *FFXIV* characters. The code looks through each character on the website, analyses the information that Square Enix provides for each player, and uploads it to a single-table database. 

![Example Image of Character](/march_2023_census_additional_images/FFXIV_lodestone_char_example.png "My Character, Pontodour Okay, in the Lodestone")

The table includes information like character ID, name, gender, race, class levels, minions, mounts, and more. By tracking minions and mounts, the database can also effectively track player progress through the story, since major questlines in *FFXIV* reward their players by delivering minions or mounts.  
The Lodestone is not able to identify which character is owned by which player. A supporting survey would need to be included into a potential future database if that information was wanted by the higher-ups at Square Enix.  
For the purposes of this project, I am using the March 2023 database, which was accessed through direct download on the FFXIV Census website. As such, all queries will be used through MySQL, the database structure used by the project managers.

### How Clean is the Database?
This database handles over 25 million characters. As such, occasionally the analysis does falter. This can include characters with missing chunks of information, such as a missing Grand Company that they should have or missing information about their minions or mounts.  
However, due to the scope of our project, we are primarily focused on more general Grand Company trends. The amount of missing information concerning Grand Company trends amounted to less than 1% of the database. Cleaning the information by hand would still amount to doing hundreds of manual adjustments that would not be incredibly helpful in general analysis. As such, for the purposes of the scope of the project, I decided that cleaning the information manually was not necessary.  
Otherwise, the database has clean information. A random sample of characters manually checked by myself proved to have entirely correct information, including my own character, Pontodour Okay. As such, I was ready to use this database for my project!

## 1. General Population of Grand Companies
As showcased by the website itself, we have a few insights that we can immediately make concering the number of characters in each grand company:  

![Grand Company General Population Synopsis](/march_2023_census_grand_company_dashboards/General_Populations.png "General Population Dashboard")

This dashboard contains three significant tables. On the right, the general population is shown. It showcases that the Order of the Twin Adder is vastly more populous than either of the other two Grand Company options.  
The top left chart shows that Hyur is the preferred race choice in the Order of the Twin Adder and the Immortal Flames. However, the Miqo'te race is preferred in the Maelstrom.  
Finally, the bottom left chart shows that the Maelstrom is slightly preferred in terms of number of distinct Free Companies in each Grand Company. Free Companies are player-made clubs with their own individual ranking system.  
The chart that we will be paying most attention to is the general character population. While the Immortal Flames and Maelstrom are close in terms of character count, the Order of the Twin Adder has a significant lead in terms of number of characters within it.
In order to properly analyze this rather large discrepency, it is important to compare the results of these queries with the next topic.

## 2. Endgame Populations of Grand Companies
For the purposes of this data chart, I am defining "endgame" as instances where a character reached level 90 – the maximum possible level as of March 2023 – in one or more classes that match the category.  
For our purposes, "combat classes" include all classes and jobs in the "Disciples of War" and "Disciples of Magic" categories: Gladiator, Pugilist, Marauder, Lancer, Archer, Rogue, Arcanist, Thaumaturge, and Conjurer. This category also covers all of the additional jobs that a class evolves into: Paladin, Warrior, Monk, Dragoon, Ninja, Bard, Black Mage, Summoner, White Mage, and Scholar. Finally, this also includes all of the combat jobs that have no classes to begin with: Dark Knight, Gunbreaker, Machinist, Samurai, Dancer, Red Mage, Astrologian, and Sage.  
Non-combat classes include all classes in the "Disciples of the Hand" and "Disciples of the Land" categories, including: Carpenter, Blacksmith, Armorer, Goldsmith, Leatherworker, Weaver, Alchemist, Culinarian, Miner, Botanist, and Fisher.  
The following is what was obtained:  

![Grand Company Level 90 Dashboard](/march_2023_census_grand_company_dashboards/Endgame_Synopsis.png "Endgame Dashboard")

Here, the Maelstrom is proving to have the larger population – in both combat and non-combat classes. The ratios are about the same between grand companies, though non-combat classes are significantly lower in number than their combat-based peers. This is unsurprising: combat classes are required to progress the story in *Final Fantasy XIV.* In addition, having a higher level combat class makes it easier to progress the non-combat classes, through access to higher level materials, areas, and quests for the crafting and gathering roles.

## 3. Grand Company Rank
To conclude, I also wanted to look at how players were interacting with the Grand Company Rank system. Characters join their grand company as the rank "Private Third Class," with each grand company having a slightly different naming schema for each rank. As characters interact with their personal Grand Company, they can promote. From Private Third Class, they promote to: Private Second Class, Private First Class, Corporal, Sergeant Third Class, Sergeant Second Class, Sergeant First Class, Chief Sergeant, Second Lieutenant, First Lieutenant, and Captain. The following dashboard was made compiling the information:  

![Grand Company Ranks Dashboard](/march_2023_census_grand_company_dashboards/Player_Ranks.png "Rank Dashboard")

Here, we see two particularly interesting points. Once again, the Maelstrom and Immortal Flames have similar patterns in population, but the Order of the Twin Adder has significantly more Private Third Class entries.   
Private Third Class is by far the most populous rank, as expected. However, the second most populous rank is Second Lieutenant. This is the third-to-final rank in the game. So, players are advancing through most of the ranks before stopping at this rank in particular.

## Data Analysis
From here, we can actually get some rather interesting pieces of data about the grand companies. From these three databases, the following trends reveal themselves:  
1. **New players seem to prefer the Order of the Adder.** The Order of the Adder is home to Gridania. Gridania is the starting location of the Lancer, Archer, and Conjurer classes. Conjurer is the only healer available at character creation, while Lancer and Archer are two of the starting damage classes. Ul'dah – the home of the Immortal Flames – also has two damage classes – Pugilist and Thaumaturge – but has the Gladiator as it's non-damage class. Gladiator is one of two Tank classes, the other being Warrior. Warrior and Arcanist both begin play in Limsa Lominsa, home to the Maelstrom. While it is impossible to precisely pin why players are choosing the Order of the Adder on first playthrough, it is likely because most players start as the only healer or two of the more exciting Damage class roles. Then, when they choose a Grand Company, they are more likely to gravitate towards the company of their starting city. 
2. **Characters stick around in the Maelstrom.** Both combat and non-combat classes are more active in the Maelstrom than either of the other two by a significant margin. This is surprising. None of the Grand Companies offer any explicit advantage over the others. The most prevalent advantages include starting city, color of armor, and story relevance. Without a survey, it is impossible to pin down the reason why players in the Maelstrom are more likely to stay into the endgame. My personal theory is that it is a story-driven choice, as the leader of the Maelstrom – Merlwyb – leaves a lasting impression on the player in the quests that lead up to the player's choice of Grand Company. However, this conjecture has no lasting evidence.
3. **The requirements to achieve First Lieutenant overcome the want to obtain additional rewards.** Players who are interested enough in their Grand Company to rank up are occasionally not engaging in Grand Company content past the Second Lieutenant rank. In order to become a Chief Sergeant, players must complete an optional quest "Shadows Uncast." To become a Second Lieutenant, they must complete the optional quest "Gilding the Billious," and then must also complete the Rank 2 of the Hunting Log. By doing so, the player unlocks Player Housing, the Hunt, and the Adventure Squadrons system. However, once they reach this point, a significant number of players seem to stop considering the Grand Company content as being worth their time.

### Potential Actionable Statements
While most of these actions do not necessarily suggest a problem with *FFXIV*, there are minor points where editing content around the starting areas could vastly improve how the Grand Company system interacts with players. I suggest the following:  
1. **Change how starting classes begin play.** At the moment, new players are favoring Gridania, and for good reason. New Healers must begin play in Gridania, and if they wish to play with friends immediately, their friends will also have to begin play in the same city. If additional starting roles are added to Limsa Lominsa or Ul'dah, those Grand Companies are more likely to allure players. This can cause the staggering player population in the Order of the Twin Adder to potentially flatten.
2. **Entice players with better rewards in the Grand Company Ranks.** At the moment, the Second Lieutenant Rank offers many different rewards for players to dig for. First Lieutenant requires much more dedication, with a new mechanic called "Adventurer Squadrons," in order to get its promotion. And Captain requires players engage with Player vs. Player content as well as additional "Adventurer Squandron" play. In order to entice players to continue their Grand Company journey, more rewards could be presented at higher level rankings. For instance, once a player reaches First Lieutenant, then they could be invited to events with Grand Company-themed paraphenalia. Or, at Captain rank, the player could get additional bonuses towards obtaining the Grand Company currency called Seals.
3. **Learn more about why players are sticking to the game longer while in the Maelstrom.** As shown in several synopses, the Maelstrom appears to be the most popular when it comes to endgame content. Unfortunately, our current database does not offer significant detail as to why endgame players are interacting with Maelstrom for such an extended period of time. The Grand Companies offer similar rewards in terms of mounts and items in their shops. Additional analysis, such as a player survey, would be appreciated to learn more about this specific interaction. For instance, learning if location, armor color, or some other extrinsic reward causes more dedicated audiences to enjoy the Maelstrom more than the other two Grand Companies.

## Additional Resources
If you would like to learn more about this project, the [Tableau Public Page](https://public.tableau.com/app/profile/jason.toro.mccue/viz/FFXIVCaseStudyProjectMarch2023/EndgameSynopsis#1) can be accessed to more clearly see each chart used in this project for data analysis.  
In addition, for the SQL queries used to access the database to come to these conclusions, follow this link [here](https://docs.google.com/document/d/11NIh_aciSZMVYxV6rEopzuNk2PHaP84-kZ8OuG2K9lI/edit?usp=sharing).  
Thank you so much for reading along with me! *FFXIV* is a joy to analyze, since there's just so much to look for. With luck, this is just the start of my data storytelling journey!
