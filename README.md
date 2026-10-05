# Boss-mode-game.
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Boss Mode - Build Your Empire</title>

<style>
*{
  box-sizing:border-box;
}

body{
  margin:0;
  font-family:Arial, sans-serif;
  background:linear-gradient(135deg,#111827,#312e81);
  color:white;
  min-height:100vh;
  padding:20px;
}

.container{
  max-width:700px;
  margin:auto;
}

.header{
  display:flex;
  justify-content:space-between;
  align-items:center;
  gap:15px;
  margin-bottom:20px;
}

.small{
  color:#cbd5e1;
  font-size:13px;
  letter-spacing:1px;
}

h1{
  font-size:42px;
  margin:5px 0;
}

.tagline{
  color:#cbd5e1;
}

.score-box{
  background:white;
  color:#111827;
  padding:12px 18px;
  border-radius:18px;
  text-align:center;
  min-width:100px;
}

.score{
  font-size:30px;
  font-weight:bold;
}

.badges{
  display:flex;
  gap:8px;
  margin-bottom:15px;
}

.badge{
  padding:7px 12px;
  border-radius:20px;
  background:#ffffff18;
  border:1px solid #ffffff30;
  font-size:13px;
}

.card{
  background:#ffffff12;
  border:1px solid #ffffff25;
  border-radius:22px;
  padding:22px;
}

h2{
  margin-top:0;
  font-size:25px;
}

.scenario{
  color:#e2e8f0;
  line-height:1.6;
  font-size:17px;
}

.choices{
  display:grid;
  gap:12px;
  margin-top:20px;
}

.choice{
  border:none;
  padding:16px;
  border-radius:14px;
  background:white;
  color:#111827;
  font-size:16px;
  font-weight:bold;
  cursor:pointer;
  text-align:left;
}

.choice:hover{
  transform:scale(1.01);
}

.choice:disabled{
  opacity:.7;
}

.correct{
  outline:4px solid #34d399;
}

.wrong{
  outline:4px solid #fb7185;
}

.feedback{
  min-height:50px;
  margin-top:17px;
  font-weight:bold;
  line-height:1.5;
}

.next{
  border:none;
  background:#a5b4fc;
  color:#111827;
  padding:14px 22px;
  border-radius:14px;
  font-weight:bold;
  font-size:16px;
  cursor:pointer;
}

.next:disabled{
  opacity:.4;
  cursor:not-allowed;
}

.actions{
  text-align:right;
  margin-top:10px;
}

.final{
  text-align:center;
}

.trophy{
  font-size:65px;
}

.final h2{
  font-size:32px;
}

.restart{
  margin-top:15px;
}

.footer{
  text-align:center;
  margin-top:18px;
  color:#cbd5e1;
  font-size:13px;
}

.hidden{
  display:none;
}

@media(max-width:500px){

  body{
    padding:12px;
  }

  .header{
    align-items:flex-start;
  }

  h1{
    font-size:30px;
  }

  .score-box{
    min-width:85px;
    padding:10px;
  }

  .score{
    font-size:25px;
  }

  .card{
    padding:18px;
  }
}
</style>
</head>

<body>

<div class="container">

<div class="header">

<div>
<div class="small">GEN-Z MANAGEMENT CHALLENGE</div>
<h1>🔥 BOSS MODE</h1>
<div class="tagline">
Build Your Empire • Lead Your Team
</div>
</div>

<div class="score-box">
<div>TEAM SCORE</div>
<div class="score" id="score">0</div>
</div>

</div>


<div class="badges">
<div class="badge" id="round">Round 1 / 6</div>
<div class="badge" id="skill">Planning</div>
</div>


<div class="card" id="game">

<h2 id="title"></h2>

<div class="scenario" id="scenario"></div>

<div class="choices" id="choices"></div>

<div class="feedback" id="feedback"></div>

<div class="actions">
<button class="next" id="next" disabled>
Next Challenge →
</button>
</div>

</div>


<div class="card final hidden" id="final">

<div class="trophy">🏆</div>

<h2 id="resultTitle"></h2>

<p id="resultText"></p>

<button class="next restart" id="restart">
Play Again 🔄
</button>

</div>


<div class="footer">
Planning • Organizing • Staffing • Directing • Controlling
</div>

</div>


<script>

const rounds = [

{
skill:"Planning",

title:"🚀 Round 1 — The Big Launch",

scenario:
"Your college is hosting a massive Gen-Z fest. You have limited time and budget. What should your team do FIRST?",

choices:[

["Start buying decorations immediately",0],

["Set clear goals, budget and timeline",20],

["Ask everyone to do whatever they want",2],

["Wait for another team to plan it",-5]

],

why:
"Planning starts with clear goals, resources and a timeline."
},

{

skill:"Organizing",

title:"🧩 Round 2 — Assemble the Squad",

scenario:
"You have 20 volunteers. The event needs marketing, finance, decoration and operations. What is the smartest move?",

choices:[

["Give every person the same task",0],

["Create teams and assign roles based on strengths",20],

["Let only one person handle everything",-5],

["Randomly divide people",5]

],

why:
"Organizing means dividing work and creating the right structure."
},

{

skill:"Staffing",

title:"👥 Round 3 — Choose Your Players",

scenario:
"Two students apply for Social Media Lead. One is highly creative; the other has great communication and consistency. What should you do?",

choices:[

["Choose randomly",0],

["Match skills with the role requirements",20],

["Choose your best friend",-10],

["Reject both",-5]

],

why:
"Staffing is about putting the right person in the right role."
},

{

skill:"Directing",

title:"🎤 Round 4 — Team Energy",

scenario:
"Your team is tired and losing motivation one day before the event. What should the leader do?",

choices:[

["Shout at everyone",-10],

["Give clear instructions, motivate and support the team",20],

["Cancel the event",-5],

["Ignore the problem",0]

],

why:
"Directing involves leadership, communication, motivation and guidance."
},

{

skill:"Controlling",

title:"📊 Round 5 — Something Went Wrong",

scenario:
"Your event budget is already 15% over target. What is the best response?",

choices:[

["Ignore it",-10],

["Compare actual spending with the plan and take corrective action",20],

["Spend even more",-5],

["Blame the finance team",0]

],

why:
"Controlling means measuring performance, identifying deviations and correcting them."
},

{

skill:"ALL 5",

title:"🏆 FINAL BOSS — Save The Event!",

scenario:
"One hour before the event, the main speaker cancels. What should your leadership team do?",

choices:[

["Panic and blame someone",-10],

[
"Plan a backup, organize roles, assign people, direct the response and monitor execution",
30
],

["End the event",-10],

["Do nothing and hope",-5]

],

why:
"That's the complete management cycle: Planning + Organizing + Staffing + Directing + Controlling."
}

];


let current = 0;

let score = 0;

let locked = false;


const scoreElement =
document.getElementById("score");

const roundElement =
document.getElementById("round");

const skillElement =
document.getElementById("skill");

const titleElement =
document.getElementById("title");

const scenarioElement =
document.getElementById("scenario");

const choicesElement =
document.getElementById("choices");

const feedbackElement =
document.getElementById("feedback");

const nextButton =
document.getElementById("next");


function renderRound(){

const round = rounds[current];

locked = false;

roundElement.textContent =
"Round " + (current + 1) + " / 6";

skillElement.textContent =
round.skill;

titleElement.textContent =
round.title;

scenarioElement.textContent =
round.scenario;

feedbackElement.textContent = "";

nextButton.disabled = true;

nextButton.textContent =
current === 5
? "Finish Game 🏆"
: "Next Challenge →";


choicesElement.innerHTML = "";


round.choices.forEach((choice,index)=>{

const button =
document.createElement("button");

button.className = "choice";

button.textContent =
choice[0];

button.onclick =
function(){

selectAnswer(index,button);

};

choicesElement.appendChild(button);

});

}


function selectAnswer(index,button){

if(locked) return;

locked = true;

const round = rounds[current];

const points =
round.choices[index][1];


score =
Math.max(0,score + points);

scoreElement.textContent =
score;


document
.querySelectorAll(".choice")
.forEach(button=>{
button.disabled = true;
});


if(points > 0){

button.classList.add("correct");

feedbackElement.textContent =
"✅ Great decision! " +
round.why;

}

else{

button.classList.add("wrong");

feedbackElement.textContent =
"💡 Learn from it: " +
round.why;

}


nextButton.disabled = false;

}


nextButton.onclick = function(){

if(current < 5){

current++;

renderRound();

}

else{

document
.getElementById("game")
.classList.add("hidden");

document
.getElementById("final")
.classList.remove("hidden");


let title;

if(score >= 100){

title = "LEGENDARY LEADER 👑";

}

else if(score >= 70){

title = "BOSS LEVEL 💪";

}

else{

title = "RISING LEADER 🚀";

}


document
.getElementById("resultTitle")
.textContent = title;


document
.getElementById("resultText")
.textContent =
"Your final score is " +
score +
"/130. You completed all five functions of management!";

}

};


document
.getElementById("restart")
.onclick = function(){

current = 0;

score = 0;

scoreElement.textContent = "0";

document
.getElementById("final")
.classList.add("hidden");

document
.getElementById("game")
.classList.remove("hidden");

renderRound();

};


renderRound();

</script>

</body>
</html>
