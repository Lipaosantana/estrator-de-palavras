
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Extrator de Palavras-chave</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 40px;
      background: #f0f0f0;
    }
    textarea {
      width: 100%;
      height: 200px;
      padding: 10px;
      font-size: 16px;
      resize: vertical;
    }
    button {
      padding: 10px 20px;
      margin-top: 10px;
      font-size: 16px;
    }
    .resultado {
      margin-top: 20px;
      padding: 10px;
      background: #fff;
      border: 1px solid #ccc;
    }
    .palavra {
      display: inline-block;
      background: #e0e0ff;
      margin: 4px;
      padding: 6px 10px;
      border-radius: 6px;
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
