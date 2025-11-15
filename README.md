# MY-WEBSITE<!DOCTYPE html><!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>SmartStudy AI</title>

  <!-- Google Font -->
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">

  <!-- Material Icons -->
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">

  <style>
    :root {
      --primary: #1a73e8;
      --bg: #f1f3f4;
      --card-bg: white;
      --text: #202124;
      --subtext: #5f6368;
    }

    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      font-family: "Inter", sans-serif;
      background: var(--bg);
    }

    /* HEADER */
    header {
      background: var(--card-bg);
      padding: 18px 20px;
      box-shadow: 0 2px 6px rgba(0, 0, 0, 0.09);
      display: flex;
      align-items: center;
      gap: 10px;
      font-size: 24px;
      font-weight: 600;
      position: sticky;
      top: 0;
      z-index: 10;
    }

    header .material-icons {
      color: var(--primary);
      font-size: 28px;
    }

    /* MAIN CARD */
    .container {
      max-width: 650px;
      margin: 30px auto;
      background: var(--card-bg);
      padding: 28px;
      border-radius: 16px;
      box-shadow: 0 4px 18px rgba(0, 0, 0, 0.08);
      animation: fadeIn 0.4s ease;
    }

    @keyframes fadeIn {
      from {
        opacity: 0;
        transform: translateY(25px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }

    h2 {
      color: var(--text);
      text-align: center;
      margin-bottom: 22px;
      font-size: clamp(20px, 4vw, 30px);
    }

    label {
      font-weight: 600;
      margin-top: 15px;
      display: block;
      color: var(--subtext);
      font-size: clamp(14px, 2vw, 16px);
    }

    textarea,
    input,
    select {
      width: 100%;
      padding: 14px;
      margin-top: 8px;
      border: 1px solid #dadce0;
      border-radius: 10px;
      font-size: 16px;
      background: #fafafa;
      transition: 0.2s;
    }

    textarea {
      resize: vertical;
      min-height: 90px;
    }

    textarea:focus,
    input:focus,
    select:focus {
      border-color: var(--primary);
      box-shadow: 0 0 0 2px #cfe0fc;
      outline: none;
    }

    button {
      width: 100%;
      margin-top: 25px;
      background: var(--primary);
      color: white;
      padding: 16px;
      border: none;
      border-radius: 12px;
      font-size: clamp(18px, 3.5vw, 20px);
      font-weight: 600;
      cursor: pointer;
      transition: 0.25s;
    }

    button:hover {
      background: #155ac4;
      transform: scale(1.02);
    }

    button:active {
      transform: scale(0.98);
    }

    .output-box {
      margin-top: 25px;
      background: #e8f0fe;
      color: var(--text);
      padding: 20px;
      border-radius: 12px;
      font-size: 16px;
      white-space: pre-line;
      animation: fadeIn 0.4s ease;
    }

    /* MOBILE RESPONSIVE CHANGES */
    @media (max-width: 600px) {
      .container {
        margin: 15px;
        padding: 20px;
      }

      textarea,
      input,
      select {
        font-size: 15px;
        padding: 12px;
      }

      button {
        padding: 14px;
      }
    }
  </style>
</head>

<body>

  <header>
    <span class="material-icons">auto_stories</span>
    SmartStudy AI
  </header>

  <div class="container">
    <h2>Create Your Study Plan</h2>

    <label>Enter Your Subjects:</label>
    <textarea id="subjects" placeholder="Example: Math, Physics, English"></textarea>

    <label>Hours Available Per Day:</label>
    <input type="number" id="hours" placeholder="Example: 4" />

    <label>Difficulty Level:</label>
    <select id="difficulty">
      <option value="easy">Easy</option>
      <option value="medium" selected>Medium</option>
      <option value="hard">Hard</option>
    </select>

    <button onclick="generatePlan()">Generate Study Plan</button>

    <div class="output-box" id="output">Your plan will appear here...</div>
  </div>

  <script>
    function generatePlan() {
      const subjects = document.getElementById("subjects").value.split(",").map(s => s.trim());
      const hours = parseFloat(document.getElementById("hours").value);
      const diff = document.getElementById("difficulty").value;

      if (subjects.length === 0 || !hours) {
        document.getElementById("output").innerText = "⚠ Please fill out all fields.";
        return;
      }

      let multiplier = diff === "easy" ? 0.8 : diff === "medium" ? 1 : 1.25;
      let perSubject = (hours / subjects.length) * multiplier;

      let plan = "📘 **Your Study Plan:**\n\n";
      subjects.forEach(s => {
        plan += `• ${s}: ${perSubject.toFixed(1)} hours/day\n`;
      });

      document.getElementById("output").innerText = plan;
    }
  </script>

</body>

</html>
