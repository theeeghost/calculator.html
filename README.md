<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Calculatrice Moderne</title>
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-900 flex items-center justify-center min-h-screen">
  <div class="bg-gray-800 p-6 rounded-2xl shadow-2xl w-80">
    <div id="display" class="bg-black text-white text-3xl text-right px-4 py-6 rounded-xl mb-6 min-h-[72px]">0</div>
    <div class="grid grid-cols-4 gap-4 text-white text-xl">
      <button onclick="clearDisplay()" class="col-span-2 bg-red-500 hover:bg-red-600 py-3 rounded-xl">C</button>
      <button onclick="deleteLast()" class="bg-yellow-500 hover:bg-yellow-600 py-3 rounded-xl">⌫</button>
      <button onclick="append('/')" class="bg-blue-600 hover:bg-blue-700 py-3 rounded-xl">÷</button>

      <button onclick="append('7')" class="bg-gray-700 hover:bg-gray-600 py-3 rounded-xl">7</button>
      <button onclick="append('8')" class="bg-gray-700 hover:bg-gray-600 py-3 rounded-xl">8</button>
      <button onclick="append('9')" class="bg-gray-700 hover:bg-gray-600 py-3 rounded-xl">9</button>
      <button onclick="append('*')" class="bg-blue-600 hover:bg-blue-700 py-3 rounded-xl">×</button>

      <button onclick="append('4')" class="bg-gray-700 hover:bg-gray-600 py-3 rounded-xl">4</button>
      <button onclick="append('5')" class="bg-gray-700 hover:bg-gray-600 py-3 rounded-xl">5</button>
      <button onclick="append('6')" class="bg-gray-700 hover:bg-gray-600 py-3 rounded-xl">6</button>
      <button onclick="append('-')" class="bg-blue-600 hover:bg-blue-700 py-3 rounded-xl">−</button>

      <button onclick="append('1')" class="bg-gray-700 hover:bg-gray-600 py-3 rounded-xl">1</button>
      <button onclick="append('2')" class="bg-gray-700 hover:bg-gray-600 py-3 rounded-xl">2</button>
      <button onclick="append('3')" class="bg-gray-700 hover:bg-gray-600 py-3 rounded-xl">3</button>
      <button onclick="append('+')" class="bg-blue-600 hover:bg-blue-700 py-3 rounded-xl">+</button>

      <button onclick="append('0')" class="col-span-2 bg-gray-700 hover:bg-gray-600 py-3 rounded-xl">0</button>
      <button onclick="append('.')" class="bg-gray-700 hover:bg-gray-600 py-3 rounded-xl">.</button>
      <button onclick="calculate()" class="bg-green-500 hover:bg-green-600 py-3 rounded-xl">=</button>
    </div>
  </div>

  <script>
    let display = document.getElementById('display');

    // Ajout du support clavier
    document.addEventListener('keydown', function(event) {
      const key = event.key;
      if ('0123456789'.includes(key)) {
        append(key);
      } else if (key === '+' || key === '-' || key === '*' || key === '/') {
        append(key);
      } else if (key === 'Enter' || key === '=') {
        calculate();
        event.preventDefault();
      } else if (key === 'Backspace') {
        deleteLast();
        event.preventDefault();
      } else if (key === 'Escape' || key.toLowerCase() === 'c') {
        clearDisplay();
        event.preventDefault();
      } else if (key === '.') {
        append('.');
      }
    });

    function append(char) {
      if (display.textContent === '0') {
        display.textContent = char;
      } else {
        display.textContent += char;
      }
    }

    function clearDisplay() {
      display.textContent = '0';
    }

    function deleteLast() {
      if (display.textContent.length > 1) {
        display.textContent = display.textContent.slice(0, -1);
      } else {
        display.textContent = '0';
      }
    }

    function calculate() {
      try {
        display.textContent = eval(display.textContent.replace('×', '*').replace('÷', '/'));
      } catch {
        display.textContent = 'Erreur';
      }
    }
  </script>
</body>
</html>
