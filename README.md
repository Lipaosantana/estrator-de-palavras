<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Extrator de Palavras-chave</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      margin: 40px;
      background: linear-gradient(to right, #0f0f0f, #1e1e2f);
      color: #f0f8ff;
    }

    h1 {
      text-align: center;
      color: #4dabf7;
      margin-bottom: 30px;
      text-shadow: 1px 1px 2px #000;
    }

    textarea {
      width: 100%;
      height: 200px;
      padding: 15px;
      font-size: 16px;
      border: 2px solid #4dabf7;
      border-radius: 8px;
      resize: vertical;
      background: #101522;
      color: #f0f8ff;
      box-shadow: 0 0 10px rgba(77, 171, 247, 0.2);
    }

    button {
      background-color: #4dabf7;
      color: #000;
      border: none;
      padding: 12px 24px;
      font-size: 16px;
      border-radius: 8px;
      cursor: pointer;
      margin-top: 15px;
      transition: background-color 0.3s ease, transform 0.2s ease;
      box-shadow: 0 4px 8px rgba(0,0,0,0.3);
    }

    button:hover {
      background-color: #339af0;
      transform: scale(1.05);
    }

    .resultado {
      margin-top: 25px;
      padding: 20px;
      background: #1a1b2f;
      border: 2px solid #4dabf7;
      border-radius: 10px;
      box-shadow: 0 0 15px rgba(77, 171, 247, 0.1);
    }

    .resultado h3 {
      color: #74c0fc;
    }

    .palavra {
      display: inline-block;
      background: #4dabf7;
      color: #000;
      margin: 6px;
      padding: 8px 14px;
      border-radius: 20px;
      font-weight: bold;
      box-shadow: 0 2px 6px rgba(0,0,0,0.3);
      transition: transform 0.2s, background 0.2s;
    }

    .palavra:hover {
      transform: scale(1.1);
      background: #339af0;
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

