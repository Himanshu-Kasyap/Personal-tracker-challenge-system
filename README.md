<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Personal Tracker + Challenge</title>
  <style>
    /* Import a nice Google Font */
    @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap');

    /* Reset and base */
    *, *::before, *::after {
      box-sizing: border-box;
    }
    body {
      font-family: 'Poppins', sans-serif;
      margin: 0;
      padding: 0;
      background: linear-gradient(135deg, #e0f7fa, #f9fbe7);
      color: #2c3e50;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: flex-start;
      padding: 40px 20px 60px;
      transition: background 0.4s ease;
    }
    .navbar {
      width: 100%;
      max-width: 700px;
      display: flex;
      justify-content: center;
      gap: 25px;
      margin-bottom: 40px;
      padding-bottom: 10px;
      border-bottom: 2px solid #a5d6a7;
      background: #26a69a;
      border-radius: 12px;
      box-shadow: 0 4px 8px rgb(38 166 154 / 0.4);
    }
    .navbar a {
      color: #ecf0f1;
      font-weight: 600;
      font-size: 18px;
      text-decoration: none;
      padding: 10px 20px;
      border-radius: 40px;
      transition: background-color 0.3s ease, box-shadow 0.3s ease;
      user-select: none;
    }
    .navbar a:hover, .navbar a.active {
      background-color: #1b7f77;
      box-shadow: 0 4px 10px rgb(27 127 119 / 0.6);
      cursor: pointer;
    }

    .container {
      background: #fff;
      max-width: 700px;
      width: 100%;
      border-radius: 16px;
      padding: 30px 40px 40px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.08);
      animation: slideFadeIn 0.5s ease forwards;
      min-height: 480px;
    }
    h1, h2, h3 {
      text-align: center;
      margin: 0 0 25px 0;
      font-weight: 700;
      color: #34495e;
    }
    h1 {
      font-size: 2.8rem;
      letter-spacing: 1.3px;
      color: #00796b;
      margin-bottom: 35px;
    }
    h2 {
      font-size: 2rem;
      color: #00695c;
      margin-bottom: 30px;
    }
    h3 {
      font-size: 1.3rem;
      color: #00796b;
    }

    form label {
      display: block;
      margin: 15px 0 6px;
      font-weight: 600;
      font-size: 1.1rem;
      color: #2c3e50;
    }
    input[type="number"] {
      width: 100%;
      padding: 10px 15px;
      font-size: 1.1rem;
      border-radius: 12px;
      border: 2px solid #b2dfdb;
      outline-offset: 2px;
      transition: border-color 0.3s ease;
      font-weight: 500;
      color: #004d40;
    }
    input[type="number"]:focus {
      border-color: #00796b;
      box-shadow: 0 0 8px 2px #00796b66;
    }
    button[type="submit"] {
      margin-top: 30px;
      width: 100%;
      padding: 15px;
      font-size: 1.25rem;
      font-weight: 700;
      background: linear-gradient(135deg, #43a047, #1b5e20);
      color: #e0f2f1;
      border: none;
      border-radius: 40px;
      cursor: pointer;
      box-shadow: 0 6px 15px rgba(67,160,71,0.7);
      transition: background 0.3s ease, box-shadow 0.3s ease;
      user-select: none;
    }
    button[type="submit"]:hover {
      background: linear-gradient(135deg, #66bb6a, #2e7d32);
      box-shadow: 0 8px 20px rgba(102,187,106,0.85);
    }

    .result {
      margin-top: 30px;
      padding: 25px 30px;
      border-radius: 18px;
      background: #e0f2f1;
      text-align: center;
      box-shadow: inset 0 2px 5px rgb(0 121 107 / 0.3);
      font-size: 1.5rem;
      font-weight: 700;
      color: #004d40;
      user-select: none;
    }
    .status {
      margin-top: 15px;
      font-size: 1.4rem;
      font-weight: 600;
      color: #00796b;
    }

    .challenge-card {
      margin-top: 20px;
      padding: 22px 28px;
      border-radius: 20px;
      background: #a5d6a7;
      box-shadow: 0 10px 20px rgb(165 214 167 / 0.4);
      transition: transform 0.3s ease, box-shadow 0.3s ease;
      user-select: none;
    }
    .challenge-card:hover {
      transform: translateY(-5px);
      box-shadow: 0 14px 30px rgb(165 214 167 / 0.7);
    }
    .challenge-card h3 {
      margin-bottom: 10px;
      color: #1b5e20;
      font-weight: 700;
    }
    .challenge-card p {
      font-size: 1.05rem;
      font-weight: 500;
      color: #2e7d32;
      margin-bottom: 16px;
      line-height: 1.3;
    }
    .challenge-card button {
      padding: 10px 20px;
      font-size: 1.1rem;
      font-weight: 600;
      color: #e0f2f1;
      background: linear-gradient(135deg, #388e3c, #1b5e20);
      border: none;
      border-radius: 32px;
      cursor: pointer;
      box-shadow: 0 5px 15px rgba(56,142,60,0.6);
      transition: background 0.3s ease, box-shadow 0.3s ease;
      user-select: none;
    }
    .challenge-card button:hover {
      background: linear-gradient(135deg, #66bb6a, #2e7d32);
      box-shadow: 0 7px 22px rgba(102,187,106,0.8);
    }

    .progress-bar {
      width: 100%;
      height: 26px;
      background-color: #c8e6c9;
      border-radius: 18px;
      overflow: hidden;
      position: relative;
      box-shadow: inset 0 2px 6px rgb(0 0 0 / 0.1);
      user-select: none;
    }
    .progress-fill {
      height: 100%;
      background: linear-gradient(90deg, #43a047, #1b5e20);
      width: 0%;
      text-align: center;
      color: #e0f2f1;
      font-weight: 700;
      line-height: 26px;
      border-radius: 18px 0 0 18px;
      transition: width 0.5s ease, background 0.5s ease;
      user-select: none;
      box-shadow: 0 0 10px rgb(67 160 71 / 0.8);
    }

    .about p {
      font-size: 1.15rem;
      line-height: 1.5;
      color: #34495e;
      user-select: none;
      text-align: center;
      max-width: 600px;
      margin: 0 auto;
    }

    .hidden {
      display: none;
    }

    @keyframes slideFadeIn {
      from {
        opacity: 0;
        transform: translateY(30px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }

    /* Responsive tweaks */
    @media (max-width: 480px) {
      .container {
        padding: 25px 20px 30px;
        min-height: auto;
      }
      h1 {
        font-size: 2.2rem;
      }
      button[type="submit"], .challenge-card button {
        font-size: 1rem;
        padding: 12px 18px;
      }
    }
  </style>
</head>
<body>
  <nav class="navbar" aria-label="Main navigation">
    <a href="#" class="active" onclick="event.preventDefault(); showPage('home', this)">🏠 Home</a>
    <a href="#" onclick="event.preventDefault(); showPage('challenges', this)">🏆 Challenges</a>
    <a href="#" onclick="event.preventDefault(); showPage('about', this)">ℹ️ About</a>
  </nav>
  <main class="container" role="main">
    <section id="home">
      <h1>🌟 Personal Tracker</h1>
      <form id="trackerForm" aria-label="Personal tracker input form">
        <label for="sleep">Hours of Sleep:</label>
        <input type="number" id="sleep" name="sleep" min="0" max="12" required aria-required="true" />

        <label for="steps">Steps Walked:</label>
        <input type="number" id="steps" name="steps" min="0" max="20000" required aria-required="true" />

        <label for="water">Glasses of Water:</label>
        <input type="number" id="water" name="water" min="0" max="10" required aria-required="true" />

        <label for="screen">Screen Time (hrs):</label>
        <input type="number" id="screen" name="screen" min="0" max="12" required aria-required="true" />

        <label for="exercise">Meditation/Exercise (mins):</label>
        <input type="number" id="exercise" name="exercise" min="0" max="60" required aria-required="true" />

        <button type="submit" aria-label="Calculate health score">✨ Calculate Score</button>
      </form>
      <div class="result" id="result" aria-live="polite" aria-atomic="true"></div>
    </section>

    <section id="challenges" class="hidden" aria-label="Challenges section">
      <h2>🏆 Challenges</h2>
      <article class="challenge-card" aria-live="polite" aria-atomic="true">
        <h3>💧 7-Day Hydration Challenge</h3>
        <p>Drink 8 glasses of water daily for 7 days.</p>
        <div class="progress-bar" role="progressbar" aria-valuemin="0" aria-valuemax="7" aria-valuenow="0">
          <div class="progress-fill" id="hydrationProgress">0/7</div>
        </div>
        <button onclick="updateProgress('hydrationProgress', 7)" aria-label="Mark today's hydration progress">Mark Today's Water Intake</button>
      </article>

      <article class="challenge-card" aria-live="polite" aria-atomic="true">
        <h3>🚶 Step Up Challenge</h3>
        <p>Walk 10,000 steps for 5 days this week.</p>
        <div class="progress-bar" role="progressbar" aria-valuemin="0" aria-valuemax="5" aria-valuenow="0">
          <div class="progress-fill" id="stepsProgress">0/5</div>
        </div>
        <button onclick="updateProgress('stepsProgress', 5)" aria-label="Mark today's step goal progress">Mark Today's Step Goal</button>
      </article>
    </section>

    <section id="about" class="about hidden" aria-label="About section">
      <h2>About This App</h2>
      <p>This personal tracker helps you monitor your daily habits and join wellness challenges to stay motivated. Track your score based on sleep, hydration, steps, and screen time, and unlock achievements for healthier living.</p>
    </section>
  </main>

  <script>
    const form = document.getElementById('trackerForm');
    const resultDiv = document.getElementById('result');
    const navLinks = document.querySelectorAll('.navbar a');

    // Local progress trackers for challenges
    const progressData = {
      hydrationProgress: 0,
      stepsProgress: 0
    };

    form.addEventListener('submit', function(e) {
      e.preventDefault();

      let score = 0;
      const sleep = Number(document.getElementById('sleep').value);
      const steps = Number(document.getElementById('steps').value);
      const water = Number(document.getElementById('water').value);
      const screen = Number(document.getElementById('screen').value);
      const exercise = Number(document.getElementById('exercise').value);

      if (sleep >= 7 && sleep <= 9) score += 20;
      if (steps >= 8000 && steps <= 15000) score += 20;
      if (water >= 6 && water <= 10) score += 20;
      if (screen <= 4) score += 20;
      if (exercise >= 20) score += 20;

      let status = '';
      if (score >= 80) status = '🟢 Excellent';
      else if (score >= 50) status = '🟡 Improving';
      else status = '🔴 Needs Attention';

      resultDiv.innerHTML = `
        <h2>Your Score: ${score}/100</h2>
        <div class="status">Status: ${status}</div>
      `;
    });

    function updateProgress(id, totalDays) {
      const bar = document.getElementById(id);

      if (progressData[id] < totalDays) {
        progressData[id]++;
      }

      const current = progressData[id];
      const percent = (current / totalDays) * 100;
      bar.style.width = percent + '%';
      bar.innerText = `${current}/${totalDays}`;
      bar.parentElement.setAttribute('aria-valuenow', current);

      if (current === totalDays) alert('🎉 Challenge Completed! 🥳');
    }

    function showPage(page, clickedLink) {
      // Hide all pages
      ['home', 'challenges', 'about'].forEach(id => {
        document.getElementById(id).classList.add('hidden');
      });
      // Remove active from all nav links
      navLinks.forEach(link => link.classList.remove('active'));

      // Show selected page
      document.getElementById(page).classList.remove('hidden');
      // Set active nav link
      if (clickedLink) clickedLink.classList.add('active');
    }

    // Initialize with Home page active
    showPage('home');
  </script>
</body>
</html>
