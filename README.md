[index.html](https://github.com/user-attachments/files/22046664/index.html)
<!DOCTYPE html>
<html lang="it">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1" />
  <title>Carlo WebApp - Calcolatore Margine e Calcolatrice</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;600&display=swap');

    body {
      font-family: 'Open Sans', sans-serif;
      background: #f0f4f8;
      margin: 0;
      padding: 2em 1em 3em;
      display: flex;
      flex-direction: column;
      align-items: center;
      min-height: 100vh;
      color: #33475b;
    }

    h1.title {
      font-weight: 700;
      font-size: 2rem;
      color: #207cca;
      margin-bottom: 1.2rem;
      user-select: none;
      text-align: center;
      letter-spacing: 0.04em;
      text-shadow: 1px 1px 4px rgba(32, 124, 202, 0.3);
    }

    .container {
      display: flex;
      max-width: 980px;
      background: #ffffff;
      border-radius: 16px;
      box-shadow: 0 16px 40px rgba(0,0,0,0.08);
      overflow: hidden;
      gap: 30px;
      padding: 30px;
      width: 100%;
      box-sizing: border-box;
      flex-wrap: nowrap;
    }

    .calculator {
      background: #2c3e50;
      color: #ecf0f1;
      border-radius: 16px;
      width: 320px;
      height: 360px;
      display: flex;
      flex-direction: column;
      box-shadow: 0 12px 30px rgba(44, 62, 80, 0.3);
      user-select: none;
      flex-shrink: 0;
      overflow: hidden;
      padding: 20px;
      box-sizing: border-box;
    }

    .display {
      background: #1a252f;
      border-radius: 10px;
      font-size: 2rem;
      height: 50px;
      line-height: 50px;
      padding: 0 16px;
      text-align: right;
      letter-spacing: 0.05em;
      margin-bottom: 15px;
      box-shadow: inset 0 2px 5px rgba(255,255,255,0.08);
      overflow-x: auto;
      flex-shrink: 0;
      user-select: text;
    }

    .buttons {
      display: grid;
      grid-template-columns: repeat(5, 1fr);
      gap: 8px;
      flex-grow: 1;
    }

    button {
      border: none;
      border-radius: 10px;
      font-size: 1.15rem;
      font-weight: 600;
      cursor: pointer;
      transition: 0.25s ease;
      color: #fff;
      box-shadow: 0 3px 8px rgba(0,0,0,0.1);
      background: #2980b9;
      user-select: none;
      padding: 8px 0;
      min-width: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 46px;
      white-space: nowrap;
    }

    button:hover {
      background: #3498db;
      box-shadow: 0 5px 12px rgba(52, 152, 219, 0.6);
    }

    button.operator {
      background: #f39c12;
      box-shadow: 0 3px 8px rgba(243, 156, 18, 0.5);
    }

    button.operator:hover {
      background: #f1c40f;
      box-shadow: 0 5px 14px rgba(241, 196, 15, 0.65);
    }

    button.clear {
      background: #e74c3c;
      box-shadow: 0 3px 8px rgba(231, 76, 60, 0.5);
    }

    button.clear:hover {
      background: #c0392b;
      box-shadow: 0 5px 14px rgba(192, 57, 43, 0.65);
    }

    button.function {
      background: #27ae60;
      box-shadow: 0 3px 8px rgba(39, 174, 96, 0.5);
      font-size: 0.95rem;
      padding: 6px 5px;
      line-height: 1.1;
    }

    button.function:hover {
      background: #2ecc71;
      box-shadow: 0 5px 14px rgba(46, 204, 113, 0.65);
    }

    button[data-num="0"] {
      grid-column: span 2;
      font-size: 1.15rem;
      padding-left: 20px;
      padding-right: 20px;
      justify-content: flex-start;
    }

    button[data-num="."] {
      font-size: 1.25rem;
      padding: 10px 0;
    }

    .calculators {
      flex: 1;
      display: flex;
      flex-direction: column;
      gap: 30px;
      color: #2c3e50;
      min-width: 280px;
    }

    .box {
      background: #f9fbfd;
      border-radius: 16px;
      padding: 24px 28px;
      box-shadow: 0 6px 18px rgba(44, 62, 80, 0.06);
      display: flex;
      flex-direction: column;
      gap: 15px;
      transition: background-color 0.3s ease;
      min-width: 280px;
    }

    .box:hover {
      background-color: #e6f0f8;
    }

    h2, h3 {
      margin: 0;
      font-weight: 700;
      font-size: 1.8rem;
      color: #207cca;
      letter-spacing: 0.03em;
      user-select: none;
    }

    label {
      font-weight: 600;
      font-size: 1rem;
      margin-bottom: 6px;
      color: #34495e;
    }

    input {
      padding: 12px 14px;
      font-size: 1.1rem;
      border-radius: 10px;
      border: 1.8px solid #d1dfe8;
      outline-offset: 2px;
      transition: border-color 0.3s ease, box-shadow 0.3s ease;
      color: #2c3e50;
      font-weight: 600;
      font-family: 'Open Sans', sans-serif;
      min-width: 0;
    }

    input:focus {
      border-color: #2980b9;
      box-shadow: 0 0 8px #2980b9aa;
    }

    #risultato, #risultato2 {
      margin-top: 12px;
      font-weight: 700;
      font-size: 1.25rem;
      min-height: 36px;
      color: #27ae60;
      user-select: none;
      min-width: 0;
      word-break: break-word;
    }

    #risultato2 {
      color: #d35400;
    }

    /* Responsive: forzato unica colonna e dimensioni fluidi */
    @media (max-width: 900px) {
      .container {
        display: flex !important;
        flex-direction: column !important;
        max-width: 100% !important;
        padding: 15px 10px !important;
        gap: 20px !important;
      }
      .calculator {
        width: 100% !important;
        max-width: 450px;
        height: auto !important;
        padding-bottom: 15px;
      }
      .buttons {
        grid-template-columns: repeat(5, 1fr);
        gap: 6px;
      }
      button {
        height: 44px;
        font-size: 1.1rem;
        padding: 6px 0;
      }
      button.function {
        font-size: 0.9rem;
        padding: 5px 6px;
      }
      button[data-num="0"] {
        grid-column: span 2;
        padding-left: 12px;
        padding-right: 12px;
        font-size: 1.1rem;
      }
      .calculators {
        width: 100% !important;
        min-width: unset !important;
        flex-direction: column !important;
        gap: 20px !important;
      }
      .box {
        min-width: unset !important;
      }
      input {
        width: 100% !important;
      }
    }
  </style>
</head>
<body>
  <h1 class="title">Carlo WebApp</h1>
  <div class="container" role="main">
    <div class="calculator" aria-label="Calcolatrice">
      <div class="display" id="calcDisplay" aria-live="polite" aria-atomic="true">0</div>
      <div class="buttons">
        <button class="clear" id="clear" aria-label="Pulisci tutto">C</button>
        <button class="operator" data-op="/" aria-label="Divisione">÷</button>
        <button class="operator" data-op="*" aria-label="Moltiplicazione">×</button>
        <button class="operator" data-op="-" aria-label="Sottrazione">−</button>
        <button class="operator" data-op="+" aria-label="Addizione">+</button>

        <button data-num="7" aria-label="7">7</button>
        <button data-num="8" aria-label="8">8</button>
        <button data-num="9" aria-label="9">9</button>
        <button class="function" id="btnPercent" aria-label="Percentuale">%</button>
        <button class="function" id="btnMargine" aria-label="Inserisci margine">Marg</button>

        <button data-num="4" aria-label="4">4</button>
        <button data-num="5" aria-label="5">5</button>
        <button data-num="6" aria-label="6">6</button>
        <button class="function" id="btnCosto" aria-label="Inserisci costo">Costo</button>
        <button class="function" id="btnSell" aria-label="Inserisci prezzo di vendita">Sell</button>

        <button data-num="1" aria-label="1">1</button>
        <button data-num="2" aria-label="2">2</button>
        <button data-num="3" aria-label="3">3</button>
        <button id="equals" style="grid-column: span 1; background: #27ae60;" aria-label="Risultato">=</button>
        <button data-num="0" style="grid-column: span 2;" aria-label="0">0</button>
        <button data-num="." aria-label="Punto decimale">.</button>
      </div>
    </div>
    
    <div class="calculators" aria-label="Calcolatori margine e prezzo di vendita">
      <div class="box">
        <h2>Calcolatore Margine</h2>
        <label for="costo">Costo articolo (€):</label>
        <input type="number" id="costo" step="0.01" min="0" placeholder="Inserisci il costo" />
        <label for="prezzo">Prezzo di vendita (€):</label>
        <input type="number" id="prezzo" step="0.01" min="0" placeholder="Inserisci il prezzo di vendita" />
        <div id="risultato"></div>
      </div>

      <div class="box">
        <h3>Calcolatore Prezzo di Vendita</h3>
        <label for="costo2">Costo articolo (€):</label>
        <input type="number" id="costo2" step="0.01" min="0" placeholder="Inserisci il costo" />
        <label for="margine">Margine desiderato (%) :</label>
        <input
          type="number"
          id="margine"
          step="0.01"
          min="0"
          max="99.99"
          placeholder="Inserisci il margine desiderato"
        />
        <div id="risultato2"></div>
      </div>
    </div>
  </div>

<script>
  (function () {
    const display = document.getElementById("calcDisplay");
    let current = "0";
    let operator = null;
    let operand = null;
    let resetDisplay = false;

    function updateDisplay() {
      display.textContent = current;
    }

    function inputNumber(num) {
      if (resetDisplay || current === "0") {
        current = num;
        resetDisplay = false;
      } else {
        current += num;
      }
      updateDisplay();
    }

    function inputOperator(op) {
      if (operator && !resetDisplay) {
        calculate();
      } else {
        operand = parseFloat(current);
      }
      operator = op;
      resetDisplay = true;
    }

    function calculate() {
      if (operator === null) return;
      let currentNum = parseFloat(current);
      switch (operator) {
        case "+":
          operand += currentNum;
          break;
        case "-":
          operand -= currentNum;
          break;
        case "*":
          operand *= currentNum;
          break;
        case "/":
          if (currentNum === 0) {
            alert("Errore: divisione per zero");
            return;
          }
          operand /= currentNum;
          break;
      }
      current = operand.toString();
      operator = null;
      resetDisplay = true;
      updateDisplay();
    }

    document.querySelectorAll("[data-num]").forEach(button => {
      button.addEventListener("click", () => {
        inputNumber(button.getAttribute("data-num"));
      });
    });

    document.querySelectorAll(".operator").forEach(button => {
      button.addEventListener("click", () => {
        inputOperator(button.getAttribute("data-op"));
      });
    });

    document.getElementById("equals").addEventListener("click", () => {
      calculate();
    });

    document.getElementById("clear").addEventListener("click", () => {
      current = "0";
      operator = null;
      operand = null;
      resetDisplay = false;
      updateDisplay();

      ["costo", "prezzo", "costo2", "margine"].forEach(id => {
        const el = document.getElementById(id);
        if (el) el.value = "";
      });
      document.getElementById("risultato").innerHTML = "";
      document.getElementById("risultato2").innerHTML = "";
    });

    function insertAndReset(fieldId, recalc) {
      let val = parseFloat(current);
      if (!isNaN(val)) {
        document.getElementById(fieldId).value = val.toFixed(2);
        if (typeof recalc === "function") recalc();
        current = "0";
        resetDisplay = true;
        updateDisplay();
      }
    }

    document.getElementById("btnMargine").addEventListener("click", () => {
      insertAndReset("margine", calcolaPrezzoVendita);
    });

    document.getElementById("btnPercent").addEventListener("click", () => {
      insertAndReset("margine", calcolaPrezzoVendita);
    });

    document.getElementById("btnCosto").addEventListener("click", () => {
      let val = parseFloat(current);
      if (!isNaN(val)) {
        document.getElementById("costo").value = val.toFixed(2);
        document.getElementById("costo2").value = val.toFixed(2);
        calcolaMargine();
        calcolaPrezzoVendita();
        current = "0";
        resetDisplay = true;
        updateDisplay();
      }
    });

    document.getElementById("btnSell").addEventListener("click", () => {
      insertAndReset("prezzo", calcolaMargine);
    });

    updateDisplay();
  })();

  function calcolaMargine() {
    let costo = parseFloat(document.getElementById("costo").value) || 0;
    let prezzo = parseFloat(document.getElementById("prezzo").value) || 0;
    let margineValore = prezzo - costo;
    let marginePercent = prezzo > 0 ? (margineValore / prezzo) * 100 : 0;
    document.getElementById("risultato").innerHTML =
      `<b>Margine assoluto:</b> ${margineValore.toFixed(2)} € <br>
       <b>Margine percentuale:</b> ${marginePercent.toFixed(2)} %`;
  }
  document.getElementById("costo").addEventListener("input", calcolaMargine);
  document.getElementById("prezzo").addEventListener("input", calcolaMargine);

  function calcolaPrezzoVendita() {
    let costo2 = parseFloat(document.getElementById("costo2").value) || 0;
    let margine = parseFloat(document.getElementById("margine").value) || 0;
    let prezzoVendita =
      margine < 100 && margine > 0 ? costo2 / (1 - margine / 100) : 0;
    document.getElementById("risultato2").innerHTML =
      margine >= 100
        ? "<span style='color:#a00;'>Il margine percentuale deve essere inferiore a 100%.</span>"
        : `<b>Prezzo di vendita consigliato:</b> ${prezzoVendita.toFixed(2)} €`;
  }
  document
    .getElementById("costo2")
    .addEventListener("input", calcolaPrezzoVendita);
  document
    .getElementById("margine")
    .addEventListener("input", calcolaPrezzoVendita);
</script>
</body>
</html>
