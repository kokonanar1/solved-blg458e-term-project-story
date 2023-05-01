Download Link: https://assignmentchef.com/product/solved-blg458e-term-project-story
<br>
You are living in a Ninja World where there are 5 great countries and all of these countries are ruled by the ninjas <a href="https://en.wikipedia.org/wiki/Naruto"><sup>1</sup></a><a href="https://en.wikipedia.org/wiki/Naruto">.</a> These countries are Land of <em>Earth</em>, Land of <em>Lightning</em>, Land of <em>Water</em>, Land of <em>Wind </em>and Land of <em>Fire </em><a href="https://www.viz.com/naruto"><sup>2</sup></a><a href="https://www.viz.com/naruto">.</a>

Each year, an exam called <em>Chunin Selection Exam </em>(CSE) is organized for the junior ninjas and this exam is an opportunity for them to be promoted to journeyman. This year, each county has decided to do their own examination as the first stage and select equal number of junior ninjas to send to CSE. They also decided to share the exam scores of the juniors with the CSE committee so that their examinations can also play a role for the decision of promotion to journeyman.

Since there are 5 countries and <em>x </em>number of selected ninjas, there will be 5*<em>x </em>juniors participated in the CSE. Each ninja gains several abilities during their training time and a junior ninja can obtain generally 2 abilities. In the CSE, ninjas will fight and the score of their fight will be decided according to their abilities. Each ability has a unique degree of importance and if a ninja has a greater ability compared to his/her opponent, he/she gets ahead of the game.

You are asked to write a program for the CSE so that some junior ninjas will be promoted to journeyman.

<h1>Details</h1>

Each county will send a report of their juniors’ information to the CSE committee in the format of:

<strong>NameOfTheJunior NameOfTheCountry ExamScore1 ExamScore2 Ability1 Ability2</strong>

e.g. Sasuke Fire 50 60 Lightning Fire

At the end, the CSE committee will make a report of consisting 5*<em>x </em>lines. Each line will be about a 1 junior ninja and 1 ninja has 6 number of important features of his/her name, his/her country’s name, his/her first exam score in the first stage that his/her country held, his/her second exam score in the first stage that his/her country held, his/her first ability and his/her second ability. All these features are given as 1 word and each 1 word of feature is separated with white space.

There are different kinds of abilities and a junior ninja can have 2 of them. These abilities and their impacts are listed as:

<strong>Clone: </strong>20, <strong>Hit: </strong>10, <strong>Lightning: </strong>50, <strong>Vision: </strong>30, <strong>Sand: </strong>50, <strong>Fire: </strong>40, <strong>Water: </strong>30, <strong>Blade: </strong>20,

<strong>Summon: </strong>50, <strong>Storm: </strong>10, <strong>Rock: </strong>20

In the CSE, score of a junior in a fight is calculated as:

<em>Score </em>= 0<em>.</em>5 ∗ <em>ExamScore</em><sub>1 </sub>+ 0<em>.</em>3 ∗ <em>ExamScore</em><sub>2 </sub>+ <em>Ability</em><sub>1 </sub>+ <em>Ability</em><sub>2</sub>

For example, in the <em>Sasuke Fire 50 60 Lightning Fire </em>case, Sasuke will have a score of 133 and he will pass the round if his opponent have a score less than 133 and fail if his opponent has a score greater than 133. If both of them have the same score, the one with the higher <em>Ability</em><sub>1 </sub>+ <em>Ability</em><sub>2 </sub>score will pass. If again the scores are equal, 1 of them will pass the round randomly. 10 points will be added to the winner’s score.

The report of the CSE committee will be given to your program as parameter. A sample report is shared as <em>csereport.txt </em>with <em>x </em>= 3. In your test cases, <em>x </em>can be different.

<h1>Implementation</h1>

In this section, UI of the program will be explained and some guidelines for the functions will be given.

You will name your module as <strong>cse.hs </strong>and you will use ghc cse.hs -o cse command to create an executable. Your program will be executed as ./cse csereport.txt.

You can create a data type called <strong>Ninja </strong>as:

data Ninja = Ninja {name:: String, country:: Char, status:: String, exam1:: Float, exam2:: Float, ability1:: String, ability2:: String, r:: Int} <em>— name is the name of the ninja.</em>

<em>— county is the county of the ninja. Character choice for each country is given below.</em>

<em>— status is the current status of the ninja. It is initialized as junior.</em>

<em>— exam1 is the score of the first examination.</em>

<em>— exam2 is the score of the second examination.</em>

<em>— ability1 is the first ability of the ninja.</em>

<em>— ability2 is the second ability of the ninja.</em>

<em>— r is the number of rounds that the ninja took place. It is initialized as 0.</em>

Remember that this definition can change according to your design such as you may add <em>score </em>of a ninja to the definition.

You should have 5 different lists in your program such as:

fire :: [Ninja] <em>— add the junior ninjas of Land of Fire to that list </em>fire = []

lightning :: [Ninja] <em>— add the junior ninjas of Land of Lightning to that list </em>lightning = [] water :: [Ninja] <em>— add the junior ninjas of Land of Water to that list </em>water = [] wind :: [Ninja] <em>— add the junior ninjas of Land of Wind to that list </em>wind = [] earth :: [Ninja] <em>— add the junior ninjas of Land of Earth to that list </em>earth = []

These lists will be manipulated during the CSE and you will mainly use these lists. Since you will initialize them after you read the file which is given as a parameter, these definitions may also differ according to your design. These are shown just to clarify that you will mainly deal with 5 different lists.

UI of the program

<ol>

 <li><strong>a) View a Country’s Ninja Information: </strong><em>(10 points)</em></li>

</ol>

With this option, the user will be asked to enter the county code. <strong>e </strong>or <strong>E </strong>is Land of Earth, <strong>l </strong>or <strong>L </strong>is Land of Lightning, <strong>w </strong>or <strong>W </strong>is Land of Water, <strong>n </strong>or <strong>N </strong>is Land of Wind and <strong>f </strong>or <strong>F </strong>is Land of Fire. When the user enters the country code, the program will show all of the ninjas of that country in the CSE, according to their scores in descending order. However, if the number of rounds for the ninjas of this country are not the same, the ones with the greater number of rounds will be listed later than the ones with the lower number of rounds even if their scores are greater than the previously listed ninjas.

Taking everything into consideration, the ninjas with the same number of rounds will be listed in descending order while the number of rounds will be in ascending order. Actually, the ordering of the ninjas in their country list will be also the same, meaning that making some rounds will affect the ordering of the ninjas in the country lists. Therefore, you will not need to reorder the ninjas in the country list for the purpose of viewing the ninjas. You will just iterate over the related country list.

Each country will promote only 1 ninja to journeyman. Therefore, if this country has already 1 promoted ninja, then a warning will be given to the user and any ninja from this country cannot be included to the fights anymore even if they are not disqualified. You can use a Boolean flag for each country in order to give this warning.

A ninja is promoted to journeyman if he/she wins 3 rounds. If none of the ninjas in a country does not satisfy this condition, the related country will not promote any ninja to journeyman.

(a) Example for View a Country’s Ninja Information                                                                   (b) Example for the warning

<ol>

 <li><strong>View All Countries’ Ninja Information: </strong><em>(15 points)</em></li>

</ol>

With this option, all of the ninjas that take the CSE will be listed according to their scores in descending order and their number of rounds in ascending order (the same rule described in <em>View a Country’s Ninja Information</em>), meaning that all 5*<em>x </em>number of ninjas will be treated together. If some of the ninjas have the same score and same number of rounds, the ordering between them does not matter.

Example for View All Countries’ Ninja Information

<ol>

 <li><strong>Make a Round Between Ninjas: </strong><em>(25 points)</em></li>

</ol>

With this option, the user will be asked to enter the opponents’ names and country codes. After the round is completed, the number of rounds for the winner will be incremented by 1 and his/her position in the country list will also change according to the rules described in <em>View a Country’s Ninja Information</em>, in order to give a higher chance for the other ninjas of the same country to make a round by <em>Make a Round Between Countries </em>option (Details of that option will be explained later). If a ninja loses a round, he/she should be disqualified, meaning that he/she should be removed from the related country list. Example of a round between ninjas is shown and the effect of this round for the related country lists are also shown.

Any case of user mistake such as writing a name of ninja which is not in CSE or writing a wrong country code should be considered and meaningful error messages should be given to the user. Consider these kinds of cases for all options.

(a) Example for Make a Round Between Ninjas                                                    (b) Land of Fire ninjas after a round

(c) Land of Earth ninjas after a round

<ol>

 <li><strong>Make a Round Between Countries: </strong><em>(20 points)</em></li>

</ol>

With this option, the user will be asked to enter 2 country codes. Then, the first ninjas of each country list will make a round. Since the ones who have the first place in their country lists are selected, that is why changing the order of the ninjas in the country lists after each round increases the chance for other ninjas to have a fight with this option. Again, after the winner is decided, the loser will be removed and the order of the winner will be changed in the related country lists.

(d) Example for Make a Round Between Countries                                                 (e) Land of Fire ninjas after a round

(f) Land of Water ninjas after a round

<ol>

 <li><strong>Exit: </strong><em>(5 points)</em></li>

</ol>

With this option, the program will terminate after listing the ninjas who are promoted to journeyman. Normally, the program will always ask the user to enter an action (you may list the action options to the user every time you ask for an action, it is your choice) until this <em>Exit </em>option is selected. You can use country flags that are suggested in <em>View a Country’s Ninja Information </em>section in order to list the journeymen.

Example for Exit and listing the journeymen

<h1>Evaluation</h1>

The distribution of 75 points is given with the explanations. The remaining 25 points will be about your program’s efficiency, clarity and how much you use functional programming concepts in your implementation.

After the deadline, a schedule will be shared and we will hold Zoom meetings with each group as our demonstration sessions. Details of the meetings will be announced later.

You will use Github for your projects. You will create a private repository named as <strong>BLG458E Group X </strong>where <em>X </em>will be your group id. One of you can create this repository for your group and add others as collaborators. You can create a Github account with your ITU e-mail in order to create a private repository for free.

<h1>Tips &amp; Restrictions</h1>

<ul>

 <li>You need to use <a href="https://hackage.haskell.org/package/base-4.7.0.2/docs/System-IO.html">IO</a> to handle I/O operations.</li>

 <li>You need to use <a href="https://hackage.haskell.org/package/base-4.11.1.0/docs/System-Environment.html">Environment</a> to handle command line arguments.</li>

 <li>Since you will manipulate the lists according to the given action, do not forget to work on the outputs of your functions (manipulated lists) when you want to perform new action.</li>

 <li><a href="http://learnyouahaskell.com/input-and-output#files-and-streams">This</a> page includes helpful examples for both I/O operations and string manipulations.</li>

 <li>You should use function compositions, function applications, higher order functions, list comprehensions and currying wherever they can be used. Therefore, your program should have at least <strong>3 </strong>different kinds of higher order functions, at least <strong>1 </strong>function composition and at least <strong>1 </strong></li>

 <li>There will be a message board on Ninova and you will be able to ask for further restrictions on message board. It is your responsibility to check the message board regularly for further explanations.</li>

 <li>All the code you submit must be your own. You are not allowed to take any code from any resource.</li>

 <li>You are not allowed to use any construct that was not covered in the class.</li>

</ul>


