<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Into the Wild: A Mountain Lion Encounter</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      color: #222;
      background-color: #f2f2f2;
      line-height: 1.6;
      transition: background-color 0.5s, color 0.5s;
    }
    body.night {
      background-color: #0d0d0d;
      color: #ccc;
    }
    header {
      background-image: url('https://images.unsplash.com/photo-1617201168646-e2ba27da729b?ixlib=rb-4.0.3&auto=format&fit=crop&w=1400&q=80');
      background-size: cover;
      background-position: center;
      height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      text-align: center;
      padding: 2rem;
    }
    header h1 {
      font-size: 3rem;
      background-color: rgba(255, 255, 255, 0.7);
      color: #111;
      padding: 1rem 2rem;
      border-radius: 10px;
    }
    section {
      padding: 3rem 2rem;
      max-width: 800px;
      margin: auto;
    }
    .gallery {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 1rem;
      margin-top: 2rem;
    }
    .gallery img {
      width: 100%;
      height: 200px;
      object-fit: cover;
      border-radius: 10px;
    }
    footer {
      text-align: center;
      padding: 2rem;
      background-color: #ddd;
      font-size: 0.9rem;
      color: #555;
    }
    nav {
      text-align: center;
      padding: 1rem;
      background-color: #e4e4e4;
    }
    nav a {
      margin: 0 1rem;
      text-decoration: none;
      color: #444;
      font-weight: bold;
    }
    nav a:hover {
      text-decoration: underline;
    }
    iframe {
      width: 100%;
      height: 400px;
      border: none;
      margin-top: 2rem;
    }
    .quiz-container {
      background: white;
      padding: 2rem;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    .quiz-container h2 {
      text-align: center;
    }
    .question {
      margin-bottom: 1rem;
    }
    .answers label {
      display: block;
      margin-bottom: 0.5rem;
    }
    .quiz-container button {
      margin-top: 1rem;
      padding: 0.5rem 1rem;
      font-size: 1rem;
      background-color: #444;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    .quiz-container button:hover {
      background-color: #222;
    }
    .result {
      font-weight: bold;
      margin-top: 1rem;
    }
  </style>
</head>
<body>
  <audio id="scream-audio" src="https://www.fesliyanstudios.com/play-mp3/387" preload="auto"></audio>

  <script>
    const hour = new Date().getHours();
    if (hour >= 19 || hour <= 5) {
      document.body.classList.add("night");
    }

    window.addEventListener("scroll", () => {
      const encounter = document.getElementById("encounter");
      const rect = encounter.getBoundingClientRect();
      if (rect.top < window.innerHeight && rect.bottom >= 0) {
        document.getElementById("scream-audio").play();
      }
    }, { once: true });

    const quiz = [
      {
        question: "How far can a mountain lion leap in a single bound?",
        answers: ["10 feet", "20 feet", "40 feet"],
        correct: 2
      },
      {
        question: "How fast can a mountain lion sprint?",
        answers: ["30 mph", "40 mph", "50 mph"],
        correct: 2
      },
      {
        question: "What kind of predator is a mountain lion?",
        answers: ["Ambush predator", "Pack hunter", "Scavenger"],
        correct: 0
      },
      {
        question: "What size territory can a mountain lion cover?",
        answers: ["10 square miles", "50 square miles", "150 square miles"],
        correct: 2
      }
    ];

    let currentQuestion = 0;
    let score = 0;

    function displayQuestion() {
      const q = quiz[currentQuestion];
      document.getElementById("question").innerText = q.question;
      const answersDiv = document.getElementById("answers");
      answersDiv.innerHTML = "";
      q.answers.forEach((answer, index) => {
        const label = document.createElement("label");
        label.innerHTML = `<input type='radio' name='answer' value='${index}' /> ${answer}`;
        answersDiv.appendChild(label);
      });
    }

    function nextQuestion() {
      const selected = document.querySelector("input[name='answer']:checked");
      if (!selected) {
        alert("Please select an answer.");
        return;
      }
      const answer = parseInt(selected.value);
      if (answer === quiz[currentQuestion].correct) {
        score++;
      }
      currentQuestion++;
      if (currentQuestion < quiz.length) {
        displayQuestion();
      } else {
        document.getElementById("quiz-container").innerHTML = `<h2>Your Score: ${score}/${quiz.length}</h2>`;
      }
    }
  </script>

  <header>
    <h1>Into the Wild: A Mountain Lion Encounter</h1>
  </header>

  <nav>
    <a href="#encounter">The Encounter</a>
    <a href="#lessons">What It Taught Me</a>
    <a href="#gallery">Gallery</a>
    <a href="#facts">Scary Facts</a>
    <a href="#quiz">Quiz</a>
    <a href="#map">Map</a>
  </nav>

  <!-- ... other sections stay the same ... -->

  <section id="quiz">
    <h2>Test Your Mountain Lion Knowledge</h2>
    <div class="quiz-container" id="quiz-container">
      <div class="question" id="question"></div>
      <div class="answers" id="answers"></div>
      <button onclick="nextQuestion()">Next</button>
      <div class="result" id="result"></div>
    </div>
  </section>

  <footer>
    <p>Site created by Sean Campos | Inspired by a true encounter in Northern California</p>
  </footer>

  <script>
    displayQuestion();
  </script>
</body>
</html>
