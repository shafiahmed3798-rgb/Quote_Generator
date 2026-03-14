# Quote_Generator
## Date:14.03.2026
## Objective:
To create a simple thirukkural generator using HTML, CSS, and JavaScript that displays a new random thirukkural each time a button is clicked — similar to daily quote sections on blogs or productivity apps.

## Tasks:

### 1. Create the HTML Structure:
<ul>
  <li>Add a heading Thirukkural Generator</li>
  <li>Use a div or p to display the Thirukkural (Tamil couplet).</li>
  <li>Use another p or span to display the meaning or explanation.</li>
  <li>Add a button labeled “Get Thirukkural”.</li>
  <li>Add a label showing the Kural number.</li>
</ul>

### 2. Style the Layout Using CSS:

<ul>
  <li>Center everything on the page using Flexbox.</li>
  <li>Style the quote box with:
  <ul type="square">
    <li>Padding</li>
    <li>Background color</li>
    <li>Rounded borders</li>
    <li>Soft shadow</li>
    <li>Add hover effects for the button.</li>
  </ul>
  </li>
</ul>

### 3. Add JavaScript Functionality:
<ul>
  <li>Store an array of Thirukkural objects containing:
  <ul type="square">
    <li>Kural number</li>
    <li>Kural Meaning</li>
  </ul>
  </li>
  <li>When the button is clicked:
  <ul type="square">
    <li>Generate a random index using Math.random().</li>
    <li>Retrieve the corresponding Thirukkural object.</li>
    <li>Display the Kural number and meaning in the HTML.</li>
    <li>Update content dynamically using innerText.</li>
  </ul>
  </li>
</ul>

## Code:
```
<!DOCTYPE html>
<html lang="ta">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Thirukkural Generator</title>
<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body {
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: Arial, sans-serif;
    background-color: #302828;
  }

  .container {
    text-align: center;
    background-color: #15c5b6;
    padding: 40px 30px;
    border-radius: 12px;
    box-shadow: 0 4px 20px rgba(224, 154, 4, 0.1);
    width: 90%;
    max-width: 500px;
  }

  h1 {
    font-size: 24px;
    color: #0e0303;
    margin-bottom: 30px;
  }

  .kural-number {
    font-size: 14px;
    color: #1632e5;
    margin-bottom: 15px;
  }

  .kural-tamil {
    font-size: 20px;
    color: #dca5a5;
    line-height: 1.8;
    margin-bottom: 20px;
  }

  .kural-meaning {
    font-size: 16px;
    color: #4f0c0c;
    line-height: 1.6;
    font-style: italic;
    margin-bottom: 30px;
    padding: 0 10px;
  }

  button {
    font-size: 16px;
    padding: 12px 28px;
    background-color: #4a90d9;
    color: #8bab75;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    transition: background-color 0.2s;
  }

  button:hover {
    background-color: #131e2d;
  }

  footer {
    margin-top: 25px;
    padding-top: 15px;
    border-top: 1px solid #eee;
    font-size: 13px;
    color: #999;
    line-height: 1.6;
  }
</style>
</head>
<body>

<div class="container">
  <h1>Thirukkural Generator</h1>

  <p class="kural-number" id="kuralNum">Kural #1</p>

  <div class="kural-tamil" id="kuralText">
    அகர முதல எழுத்தெல்லாம் ஆதி<br>பகவன் முதற்றே உலகு
  </div>

  <p class="kural-meaning" id="kuralMeaning">
    As the letter 'A' is the first of all letters, so the eternal God is first in the world.
  </p>

  <button id="getKural" onclick="showRandomKural()">Get Thirukkural</button>

  <footer>
    SHAFI AHMED M S<br>
    Reg No: 25014933
  </footer>
</div>

<script>
  const kurals = [
    { num: 1, tamil: "அகர முதல எழுத்தெல்லாம் ஆதி\nபகவன் முதற்றே உலகு", meaning: "As the letter 'A' is the first of all letters, so the eternal God is first in the world." },
    { num: 2, tamil: "கற்றதனால் ஆய பயனென்கொல் வாலறிவன்\nநற்றாள் தொழாஅர் எனின்", meaning: "What is the use of learning if one does not worship the good feet of the Pure-Knowing One?" },
    { num: 10, tamil: "பிறவிப் பெருங்கடல் நீந்துவர் நீந்தார்\nஇறைவன் அடிசேரா தார்", meaning: "Those who clasp the feet of God shall cross the great sea of births; others shall not." },
    { num: 32, tamil: "அன்பிலார் எல்லாம் தமக்குரியர் அன்புடையார்\nஎன்பும் உரியர் பிறர்க்கு", meaning: "The loveless keep everything for themselves; the loving give even their bones for others." },
    { num: 47, tamil: "இன்பம் இடையறாது ஈண்டும் அவாவினை\nதுன்பத்துள் துன்பம் கெடுக்கும்", meaning: "Endless joy comes to those who vanquish desire, the sorrow within sorrow." },
    { num: 50, tamil: "அருளில்லார்க்கு அவ்வுலகம் இல்லை பொருளில்லார்க்கு\nஇவ்வுலகம் இல்லாகி யாங்கு", meaning: "As this world is lost to the poor, so the next world is lost to the merciless." },
    { num: 55, tamil: "கொல்லான் புலாலை மறுத்தானைக் கைகூப்பி\nஎல்லா உயிரும் தொழும்", meaning: "All living beings will worship with folded hands one who refuses to kill or eat meat." },
    { num: 73, tamil: "செல்வத்துள் செல்வம் செவிச்செல்வம் அச்செல்வம்\nசெல்வத்துள் எல்லாம் தலை", meaning: "The wealth of listening is the greatest of all wealth — it stands supreme among riches." },
    { num: 100, tamil: "இனிய உளவாக இன்னாத கூறல்\nகனிஇருப்பக் காய்கவர்ந் தற்று", meaning: "Speaking harsh words when kind ones exist is like plucking unripe fruit when ripe ones are available." },
    { num: 101, tamil: "செய்யாமல் செய்த உதவிக்கு வையகமும்\nவானகமும் ஆற்றல் அரிது", meaning: "Even heaven and earth cannot repay help given without prior expectation of return." },
    { num: 391, tamil: "கற்க கசடறக் கற்பவை கற்றபின்\nநிற்க அதற்குத் தக", meaning: "Learn thoroughly what should be learned, then live in accord with that learning." },
    { num: 421, tamil: "கேடில் விழுச்செல்வம் கல்வி ஒருவற்கு\nமாடல்ல மற்றை யவை", meaning: "Education is imperishable wealth; all other possessions are not true riches." },
    { num: 595, tamil: "எண்ணிய எண்ணியாங்கு எய்துப எண்ணியார்\nதிண்ணிய ராகப் பெறின்", meaning: "Those who think firmly and act with resolve will achieve exactly what they envision." },
    { num: 662, tamil: "முயற்சி திருவினை ஆக்கும் முயற்றின்மை\nஇன்மை புகுத்தி விடும்", meaning: "Effort brings prosperity; lack of effort invites poverty." },
    { num: 1330, tamil: "ஊடுதல் காமத்திற்கு இன்பம் அதற்கின்பம்\nகூடி முயங்கப் பெறின்", meaning: "Lovers' quarrels add sweetness to love; the joy is greater when reconciled in embrace." }
  ];

  const kuralNum = document.getElementById('kuralNum');
  const kuralText = document.getElementById('kuralText');
  const kuralMeaning = document.getElementById('kuralMeaning');

  function showRandomKural() {
    const randomIndex = Math.floor(Math.random() * kurals.length);
    const kural = kurals[randomIndex];

    kuralNum.innerText = 'Kural #' + kural.num;
    kuralText.innerHTML = kural.tamil.replace('\n', '<br>');
    kuralMeaning.innerText = kural.meaning;
  }
</script>

</body>
</html>
```
## Output:


## Result:
A simple quote generator using HTML, CSS, and JavaScript that displays a new random motivational quote each time a button is clicked — similar to daily quote sections on blogs or productivity apps is created successfully.
