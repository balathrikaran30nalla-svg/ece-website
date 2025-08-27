<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>ECE Toolkit</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      background: #f2f2f2;
    }
    header {
      background-color: #003366;
      color: white;
      padding: 20px;
      text-align: center;
    }
    nav {
      background: #005599;
      display: flex;
      justify-content: center;
      padding: 10px;
    }
    nav a {
      color: white;
      margin: 0 15px;
      text-decoration: none;
      font-weight: bold;
    }
    nav a:hover {
      text-decoration: underline;
    }
    section {
      padding: 40px 20px;
      max-width: 1000px;
      margin: auto;
    }
    h2 {
      color: #003366;
    }
    .toolbox {
      background: white;
      padding: 20px;
      border-radius: 6px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
      margin-bottom: 30px;
    }
    input, select {
      padding: 8px;
      margin: 5px;
    }
    .result {
      font-weight: bold;
      margin-top: 10px;
    }
    footer {
      background: #003366;
      color: white;
      text-align: center;
      padding: 15px;
      margin-top: 40px;
    }
  </style>
</head>
<body>

  <header>
    <h1>ECE Toolkit</h1>
    <p>Your Electronics Assistant</p>
  </header>

  <nav>
    <a href="#resistor">Resistor Tool</a>
    <a href="#capacitor">Capacitor Tool</a>
    <a href="#ic">IC Library</a>
    <a href="#formulas">Formulas</a>
  </nav>

  <!-- Resistor Tool -->
  <section id="resistor">
    <h2>Resistor Color Code Calculator</h2>
    <div class="toolbox">
      <label>Band 1:</label>
      <select id="band1">
        <option value="1">Brown</option>
        <option value="2">Red</option>
        <option value="3">Orange</option>
        <option value="4">Yellow</option>
        <option value="5">Green</option>
        <option value="6">Blue</option>
        <option value="7">Violet</option>
        <option value="8">Gray</option>
        <option value="9">White</option>
      </select>
      <label>Band 2:</label>
      <select id="band2">
        <option value="0">Black</option>
        <option value="1">Brown</option>
        <option value="2">Red</option>
        <option value="3">Orange</option>
        <option value="4">Yellow</option>
        <option value="5">Green</option>
        <option value="6">Blue</option>
        <option value="7">Violet</option>
        <option value="8">Gray</option>
        <option value="9">White</option>
      </select>
      <label>Multiplier:</label>
      <select id="multiplier">
        <option value="1">Black (x1)</option>
        <option value="10">Brown (x10)</option>
        <option value="100">Red (x100)</option>
        <option value="1000">Orange (x1k)</option>
        <option value="10000">Yellow (x10k)</option>
        <option value="100000">Green (x100k)</option>
        <option value="1000000">Blue (x1M)</option>
      </select>
      <button onclick="calculateResistor()">Calculate</button>
      <div class="result" id="resistorResult"></div>
    </div>
  </section>

  <!-- Capacitor Tool -->
  <section id="capacitor">
    <h2>Capacitor Code Decoder</h2>
    <div class="toolbox">
      <label>Enter 3-digit code (e.g. 104): </label>
      <input type="text" id="capCode" />
      <button onclick="decodeCapacitor()">Decode</button>
      <div class="result" id="capacitorResult"></div>
    </div>
  </section>

  <!-- IC Library -->
  <section id="ic">
    <h2>IC Library</h2>
    <div class="toolbox">
      <label>Choose IC:</label>
      <select id="icSelect" onchange="showICInfo()">
        <option value="">Select</option>
        <option value="555">555 Timer</option>
        <option value="741">741 Op-Amp</option>
        <option value="4017">CD4017 Decade Counter</option>
      </select>
      <div class="result" id="icInfo"></div>
    </div>
  </section>

  <!-- Formulas -->
  <section id="formulas">
    <h2>ECE Formulas</h2>
    <div class="toolbox">
      <ul>
        <li><strong>Ohm’s Law:</strong> V = I × R</li>
        <li><strong>Capacitance:</strong> C = Q / V</li>
        <li><strong>Inductive Reactance:</strong> X<sub>L</sub> = 2πfL</li>
        <li><strong>Capacitive Reactance:</strong> X<sub>C</sub> = 1 / (2πfC)</li>
        <li><strong>Power:</strong> P = V × I</li>
        <li><strong>Gain (dB):</strong> 20 × log(V<sub>out</sub>/V<sub>in</sub>)</li>
      </ul>
    </div>
  </section>

  <footer>
    <p>© 2025 ECE Toolkit. All rights reserved.</p>
  </footer>

  <script>
    function calculateResistor() {
      let b1 = parseInt(document.getElementById("band1").value);
      let b2 = parseInt(document.getElementById("band2").value);
      let multiplier = parseInt(document.getElementById("multiplier").value);
      let value = ((b1 * 10) + b2) * multiplier;
      document.getElementById("resistorResult").innerText = `Resistance: ${value} Ω`;
    }

    function decodeCapacitor() {
      let code = document.getElementById("capCode").value.trim();
      if (code.length === 3 && !isNaN(code)) {
        let base = parseInt(code.slice(0, 2));
        let zeros = parseInt(code[2]);
        let value = base * Math.pow(10, zeros);
        document.getElementById("capacitorResult").innerText = `Capacitance: ${value} pF (${value/1000} nF)`;
      } else {
        document.getElementById("capacitorResult").innerText = "Invalid code";
      }
    }

    function showICInfo() {
      let ic = document.getElementById("icSelect").value;
      let info = "";
      if (ic === "555") {
        info = "555 Timer IC: Used in timers, pulse generation, oscillators.";
      } else if (ic === "741") {
        info = "741 Op-Amp: General-purpose operational amplifier.";
      } else if (ic === "4017") {
        info = "CD4017: A CMOS Decade Counter/Divider IC.";
      } else {
        info = "";
      }
      document.getElementById("icInfo").innerText = info;
    }
  </script>
</body>
</html>
