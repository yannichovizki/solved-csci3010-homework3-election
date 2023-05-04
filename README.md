Download Link: https://assignmentchef.com/product/solved-csci3010-homework3-election
<br>
This is an individual coding assignment. You may have one design buddy, as described below. Having a design buddy is *highly* recommended. You will be attending interview grading for this assignment the week before spring break.

<strong>Objectives: </strong>

<ul>

 <li>Develop familiarity with the concept of “static”</li>

 <li>Implement and use the Singleton design pattern</li>

 <li>Design and implement a multi-object program, dealing with the intricacies of objects communicating with one another</li>

</ul>

<strong>Credit:</strong>

<ul>

 <li>pdf (​ deliverable 1)</li>

 <li>Makefile, ElectoralMap.[h,cpp], District.[h, cpp], main.cpp (​ deliverable 2)</li>

 <li>Makefile, all header and implementation files, main.cpp (​ deliverable 3)</li>

 <li>txt</li>

</ul>

<strong>Instructions: </strong>

You will write a program that simulates elections. You will use inheritance to implement two kinds of elections: a direct election in which constituents vote directly for candidates and the candidate with the most votes wins (regardless of whether or not that candidate has received a majority of votes), and a representative election in which all representatives from a district vote for the candidate who received the most votes (again, not necessarily a majority) in their district.




<strong><u>Part 1 (Design Document &amp; getting started):</u> </strong>




<strong>Design Document (</strong><strong>deliverable 1</strong>​ <strong>):</strong>​

You <strong>may</strong>​             have one design buddy for this assignment. You and your design buddy should figure out which​   classes are in charge of what (see class description table later in the assignment), how they will communicate (what methods they will have), and what data they will control (what fields will they have). You and your design buddy cannot write code together, but you may discuss what each method should be doing in general.




If you have a design buddy (<strong><u>recommended</u></strong><u>​ </u>)​ , you should indicate this in comments at the top of your main.cpp file as well as in your design document. Your design document, whether created with a buddy or not, is worth 10 points.




Your design document should be similar to the document that you produced for PE 6 when diagramming the provided code. You do not need to follow a formal diagramming language, but your diagram needs to be legible and communicate the information described above.  It must include:

<ol>

 <li>the interfaces that your classes will have (what methods will they have, what methods will they call/use?)</li>

 <li>the data members (fields/attribute) that your classes will have</li>

 <li>pseudocode for your main function</li>

</ol>




<strong>Program Flow: </strong>




<ul>

 <li>First, you should create an Election or a RepresentativeElection based on whether the user chooses “direct” or “representative”.</li>

 <li>Next, you should register Candidates for that election.</li>

 <li>Then, Candidates are allowed to campaign as much as they want. When all Candidates are done campaigning, this step is over.</li>

 <li>Finally, the Election calls for votes from the Districts.</li>

 <li>These votes are tallied (differently for Elections vs. RepresentativeElections) and a winner is announced.</li>

 <li>Return to step 1, using a new Election, but maintaining the same ElectoralMap.</li>

</ul>

<strong> </strong>

<strong>Next, a note on randomness: </strong>

You only want to seed your random number generator once each time your program runs. You should not seed your random number inside of a loop, for instance.

<strong> </strong>

<strong>Campaigning and converting constituents: </strong>

If a Candidate chooses to campaign in a given District, they can have 1 of the following 4 outcomes:

<ul>

 <li>A constituent is converted from Party::None to the Party of the Candidate.</li>

 <li>A constituent is converted from Party::None to the Party of the Candidate <strong><u>and</u></strong><u>​ </u> a constituent is​                converted from the majority Party that is not the Candidate’s Party to the Party of the Candidate.</li>

 <li>A constituent is converted from the majority Party that is not the Candidate’s Party to the Party of the Candidate.</li>

 <li>No one is converted.</li>

</ul>




To determine which of these situations occurs, the probability of the candidate is calculated according to the following formula:




<em><sup>P </sup></em><em><sub>s</sub></em><em>uccess </em><sup>= <em>min</em>(100, </sup>(<em>constituen</em>(<em>tcso</em> <em>inns</em> <em>toiuthteenr</em> <em>tPs</em> <em>farrotimes</em> <em>t</em> <em>hine</em>  <em>tChiasn</em> <em>Ddiidstartiec</em>′<em>st</em>,  <em>Pexacrltuyd</em> +<em>in</em> 1<em>g</em>)  <em><sub>P</sub></em>* <em>a</em>2<em>rty</em>::<em>None</em>) <sup>* </sup>((<em>constiutents</em> <em>fraorme</em><em><sub>a</sub></em> <em>t</em> <em>hoef</em>  <em>Ct</em><em><sub>h</sub></em><em>ai</em><em><sub>s</sub></em><em>n</em> <em>dDidi</em><em><sub>s</sub></em><em>attrei</em><em><sub>c</sub></em><sup>′</sup><em>st</em> <em>Party</em> + 1) * 2)<sup>)</sup>

<em>P <sub>e</sub></em><em>xtra</em> <em>success</em> = <em>P <sub>s</sub></em><em>uccess</em> * 0.1




<em>P <sub>success </sub></em>is the probability of converting a constituent affiliated with Party::None. <em>P <sub>extra</sub></em><sub> <em>success</em> </sub>is the probability of converting a constituent from the majority Party that is not the campaigning Candidate’s and is not Party::None to the Candidate’s Party. You only need to generate 1 random number. If it fulfills both these categories then two people should be converted. If there are no constituents with the needed affiliation, simply do not convert anyone from that affiliation.




Scenario 1 occurs if <em>P </em><em>success</em> and not <em>P </em><em>extra</em> <em>success</em> . Scenario 2 occurs if <em>P </em><em>success</em> and<em>P </em><em>extra</em> <em>success</em> . Scenario 3

occurs if <em>P <sub>success</sub></em> and<em>P <sub>extra</sub></em><sub> <em>success</em> </sub>but there are no constituents associated with Party::None. Scenario 4 occurs if either not <em>P <sub>success</sub></em> or if there are no constituents with the needed affiliation.




<strong>Creating your ElectoralMap: </strong>

Your ElectoralMap may have any number of Districts. This number should be hard coded as a static const int in your ElectoralMap. Your program should work if you change this number for any number of Districts. We recommend starting with 1 or 2 for debugging purposes.




Districts are generated randomly according to the following rules:

<ul>

 <li>Each Party begins with a random number of constituents between 0 and 9, including Party::None. Generate a random number for each Party.</li>

 <li>Each District is between 5 and 29 square miles, again chosen randomly.</li>

 <li>Each District should be given an id, generated by the ElectoralMap.</li>

</ul>




When you go from one Election to a new Election, your ElectoralMap must not change. You should generate it once and only once. Your ElectoralMap <strong>must</strong>​          implement the Singleton design pattern.​

<strong> </strong>

<strong>Voting: </strong>

Constituents vote as follows:

<ul>

 <li>A constituent aligned with a Party votes for a Candidate aligned with their party 100% of the time if one exists.</li>

 <li>if multiple Candidates are aligned with this Party, a random one of these options is chosen.</li>

 <li>If the constituent is aligned with Party::None, they vote for the Party that the most constituents in their District is aligned with 100% of the time.</li>

 <li>If there are multiple Candidates from this Party, a random one is chosen.</li>

 <li>If there are no Candidates aligned with the majority Party, they randomly pick a Candidate.</li>

 <li>If there is no one aligned with a constituent’s party and the constituent is not aligned with Party::None, they vote as if they were aligned with Party::None.</li>

 <li>In all cases, if there are multiple candidates from the same Party or multiple parties with the same number of constituents, a random choice is made.</li>

 <li>In all cases, constituents <strong>always</strong>​ ​ cast a vote.</li>

</ul>

<strong> </strong>

<strong> </strong>

<strong>District votes:</strong>

For the RepresentativeElection, there are a total of 5 * the number of Districts votes to be allocated. The number of votes for a given District is calculated according to the formula:

<em>V otes</em><em>District</em> = <em>floor</em>((# <em>o</em>#<em>f</em>  <em>ocof</em> <em>ncsotnitsuteitnutesn</em> <em>itns</em>  <em>tihni</em> <em>sa</em> <em>lDl</em> <em>iDstirsitcrti</em> <em>c</em>*<em>t</em> <em>s</em>1.0) * <em>total</em> <em>number</em> <em>of</em> <em>district</em> <em>votes</em>)

If District A has 7 constituents and District B has 5 constituents, District A would end up with 5 votes and District B would end up with 4 votes. Notice that the number of total district votes can be less, but never greater than, the number of total district votes to be allocated.




<table width="716">

 <tbody>

  <tr>

   <td width="166"><strong>Name </strong></td>

   <td width="169"><strong>Type </strong></td>

   <td width="381"><strong>Purpose </strong></td>

  </tr>

 </tbody>

</table>




<table width="716">

 <tbody>

  <tr>

   <td width="166">TextUI</td>

   <td width="169">class</td>

   <td width="381">Similar to the TextUI from PE 6, this class should facilitate the prompting of the user for various kinds of information, the routing of that information to the appropriate objects and the display of program data to the user.</td>

  </tr>

  <tr>

   <td width="166">Party</td>

   <td width="169">enum class</td>

   <td width="381">Represents each political party. You may have as many parties as you wish, but you must includeParty::None and at least two others. Make sure to​                design your program so that it could support a variable number of parties!</td>

  </tr>

  <tr>

   <td width="166">Candidate</td>

   <td width="169">struct or class</td>

   <td width="381">Candidates have names, party affiliations, and ids. Candidates cannot be affiliated with Party::None.​                Candidates should have ascending ids according to the order in which they are registered.</td>

  </tr>

  <tr>

   <td width="166">Election</td>

   <td width="169">class</td>

   <td width="381">The general manager of elections. Registerscandidates, directs them to districts to go campaigning, calls for the actual votes, and reports the winner after tallying the score.At the beginning of an election, a new Election object should be used (as opposed to having some sort of Reset method)</td>

  </tr>

  <tr>

   <td width="166">RepresentativeElection</td>

   <td width="169">class (inherits Election)</td>

   <td width="381">A derived class of Election. Rather than constituents voting directly for candidates, the candidate that wins a majority in each district gets all of that District’s votes(similar to with the American electoral college)</td>

  </tr>

  <tr>

   <td width="166">District</td>

   <td width="169">class</td>

   <td width="381">Represents a building block of the ElectoralMap.Districts keep track of their constituents by counting how many constituents are affiliated with each Party. They also handle when constituents change from one party to another. Throughout the course of the program running, the number of total constituents in each District should not change.Districts also have a size in square miles, which affects how easy it is for candidates to campaign there.</td>

  </tr>

  <tr>

   <td width="166">ElectoralMap</td>

   <td width="169">class (singleton)</td>

   <td width="381">Keeps track of Districts, manages the logistics of letting Candidates campaign in Districts, and handles the logic for determining how many votes each District has in aRepresentativeElection.Handles the logic for communicating the votes from each District to the Election. We recommend using a static field to assign ids to each District when they are created so that you can access them with maps from id to district.</td>

  </tr>

 </tbody>

</table>




<strong>Output: </strong>

Output files are on Canvas. You have complete creative freedom in how you design your UI, but it must include the functionality provided in our output files.




<strong>Getting Started (</strong><strong>deliverable 2</strong>​ <strong>):</strong>​

Note: You may find incorporating std::map into your program very helpful.

<ol>

 <li>Write the code for a class ElectoralMap that implements the singleton design pattern. When instantiated, this ElectoralMap should assign unique ids to 4 different Districts and store them in a std::map with int id mapping to District. You may want to use a static field in the District class to help with generating sequential unique ids.

  <ol>

   <li>Your District should be a regular class.</li>

   <li>You should override the operator&lt;&lt; for both the ElectoralMap and the District.</li>

   <li>You should use a static const int field in your ElectoralMap to designate the number of Districts, similar to what we saw in the Earth examples for number of continents.</li>

   <li>Each District should start with a random area between 5 and 29 square miles.</li>

   <li>You should implement a get_district(int id) method in ElectoralMap that lets you access Districts by</li>

  </ol></li>

</ol>

id.

<ol start="6">

 <li>You do <strong>not</strong>​ need to implement any other methods. (Though you will want to for your complete​ homework!)</li>

 <li>Test your code when you change your number of districts to a number other than 4.</li>

</ol>




<ol start="2">

 <li>Write a main.cpp concurrently with step 1 and include adequate code to test your ElectoralMap and District classes.</li>

</ol>




<strong><u>Part 2 (</u></strong><strong><u>deliverable 3</u></strong><u>​ <strong>):</strong></u><u>​</u>

Implement the rest of your program




<strong>Comments and style (15 points): </strong>

Your files and functions should have comments. We should know how to run your program and how to use your functions from your comments.




Your variables should have meaningful names. Your code should be easily readable. If you have complex sections of code, you should use inline comments to clarify.




You should follow the conventions set out in our Concise Style Guide, posted on the course github.


