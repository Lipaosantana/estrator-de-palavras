<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Extrator de Palavras-chave</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      margin: 40px;
      background: linear-gradient(to right, #f8f9fa, #e9ecef);
      color: #333;
    }

    h1 {
      text-align: center;
      color: #2c3e50;
    }

    textarea {
      width: 100%;
      height: 200px;
      padding: 15px;
      font-size: 16px;
      border: 2px solid #6c757d;
      border-radius: 8px;
      resize: vertical;
      background: #ffffff;
      box-shadow: 0 0 5px rgba(0,0,0,0.1);
    }

    button {
      background-color: #4a69bd;
      color: white;
      border: none;
      padding: 12px 24px;
      font-size: 16px;
      border-radius: 8px;
      cursor: pointer;
      margin-top: 15px;
      transition: background-color 0.3s ease;
    }

    button:hover {
      background-color: #3b53a3;
    }

    .resultado {
      margin-top: 25px;
      padding: 20px;
      background: #ffffff;
      border: 2px solid #ced4da;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0,0,0,0.05);
    }

    .palavra {
      display: inline-block;
      background: #a29bfe;
      color: white;
      margin: 6px;
      padding: 8px 14px;
      border-radius: 20px;
      font-weight: bold;
      box-shadow: 0 2px 4px rgba(0,0,0,0.1);
      transition: transform 0.2s;
    }

    .palavra:hover {
      transform: scale(1.1);
      background: #6c5ce7;
    }
  </style>
</head>
<body>
  <h1>Extrator de Palavras-chave</h1>
  <textarea id="texto" placeholder="Cole seu texto aqui..."></textarea>
  <br>
  <button onclick="extrairPalavrasChave()">Extrair</button>
  <div class="resultado" id="resultado"></div>

  <script>
    const stopwords = [
      'de', 'a', 'o', 'que', 'e', 'do', 'da', 'em', 'um', 'para', 'com', 'não', 'uma', 'os', 'no', 'se', 'na',
      'por', 'mais', 'as', 'dos', 'como', 'mas', 'foi', 'ao', 'ele', 'das', 'tem', 'isso', 'são', 'sua', 'ou', 'ser',
      'quando', 'muito', 'há', 'nos', 'já', 'está', 'eu', 'também', 'só', 'pelo', 'pela', 'até', 'isso', 'seu', 'sua',
      'me', 'te', 'nos', 'lhe', 'eles', 'elas', 'meu', 'minha', 'teu', 'tua', 'nosso', 'nossa', 'deles', 'delas'
    ];

    function extrairPalavrasChave() {
      const texto = document.getElementById('texto').value.toLowerCase();
      const palavras = texto.match(/\b[\wáéíóúãõç]+\b/g);
      const contagem = {};

      palavras?.forEach(palavra => {
        if (!stopwords.includes(palavra) && palavra.length > 2) {
          contagem[palavra] = (contagem[palavra] || 0) + 1;
        }
      });

      const resultadoDiv = document.getElementById('resultado');
      resultadoDiv.innerHTML = '<h3>Palavras-chave encontradas:</h3>';

      const palavrasOrdenadas = Object.entries(contagem)
        .sort((a, b) => b[1] - a[1])
        .slice(0, 20);

      palavrasOrdenadas.forEach(([palavra, freq]) => {
        const span = document.createElement('span');
        span.className = 'palavra';
        span.textContent = `${palavra} (${freq})`;
        resultadoDiv.appendChild(span);
      });
    }
  </script>
</body>
</html>

