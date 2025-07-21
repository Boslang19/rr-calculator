
<!DOCTYPE html>
<html lang="uk">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Калькулятор Risk/Reward</title>
  <style>
    body { font-family: Arial, sans-serif; background: #f0f4f8; padding: 40px; }
    .calculator { background: white; max-width: 400px; margin: auto; padding: 20px; border-radius: 10px; box-shadow: 0 0 10px rgba(0,0,0,0.1); }
    input, button { width: 100%; padding: 10px; margin-top: 10px; border-radius: 5px; border: 1px solid #ccc; }
    button { background-color: #007bff; color: white; cursor: pointer; border: none; }
    button:hover { background-color: #0056b3; }
    .result { margin-top: 20px; font-size: 18px; text-align: center; white-space: pre-line; }
    footer { text-align: center; margin-top: 30px; font-size: 14px; color: #666; }
  </style>
</head>
<body>
  <div class="calculator">
    <h2>Калькулятор Risk/Reward</h2>
    <input type="number" id="entry" placeholder="Ціна входу (Entry Price)">
    <input type="number" id="stop" placeholder="Стоп-лосс (Stop Loss)">
    <input type="number" id="target" placeholder="Тейк-профіт (Take Profit)">
    <input type="number" id="capital" placeholder="Ваш капітал (наприклад, 1000)">
    <input type="number" id="riskPercent" placeholder="Ризик на угоду (%)">
    <button onclick="calculateRR()">Розрахувати</button>
    <div class="result" id="result"></div>
  </div>
  <footer>
    Розроблено за підтримки <a href="https://gptonline.ai" target="_blank">GPТonline.ai</a>
  </footer>

  <script>
    function calculateRR() {
      const entry = parseFloat(document.getElementById('entry').value);
      const stop = parseFloat(document.getElementById('stop').value);
      const target = parseFloat(document.getElementById('target').value);
      const capital = parseFloat(document.getElementById('capital').value);
      const riskPercent = parseFloat(document.getElementById('riskPercent').value);

      if (isNaN(entry) || isNaN(stop) || isNaN(target)) {
        document.getElementById('result').textContent = 'Будь ласка, заповніть усі поля правильно.';
        return;
      }

      const risk = Math.abs(entry - stop);
      const reward = Math.abs(target - entry);
      const rr = reward / risk;

      let volumeText = '';
      if (!isNaN(capital) && !isNaN(riskPercent)) {
        const riskAmount = capital * (riskPercent / 100);
        const positionSize = riskAmount / risk;
        const positionValue = positionSize * entry;
        volumeText = `\nРозмір ризику на угоду: $${riskAmount.toFixed(2)}\nРозмір позиції: $${positionValue.toFixed(2)}`;
      }

      document.getElementById('result').textContent = `Ваш RR: ${rr.toFixed(2)} : 1${volumeText}`;
    }
  </script>
</body>
</html>
