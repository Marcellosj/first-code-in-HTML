# first-code-in-HTML
# this is one of my school work about geography 

!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Quiz: Natureza & Sociedade</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --verde-escuro: #1a3a2a;
    --verde-medio: #2d5a3d;
    --verde-claro: #4a8c5c;
    --dourado: #c8a951;
    --creme: #f5f0e8;
    --terra: #8b5e3c;
    --off-white: #faf8f3;
    --sombra: rgba(26,58,42,0.15);
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--verde-escuro);
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 20px;
    position: relative;
    overflow-x: hidden;
  }

  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background:
      radial-gradient(ellipse at 10% 20%, rgba(74,140,92,0.15) 0%, transparent 50%),
      radial-gradient(ellipse at 90% 80%, rgba(200,169,81,0.08) 0%, transparent 50%);
    pointer-events: none;
  }

  /* Folhas decorativas */
  .leaf {
    position: fixed;
    opacity: 0.06;
    font-size: 120px;
    pointer-events: none;
    animation: sway 8s ease-in-out infinite;
  }
  .leaf-1 { top: -20px; left: -30px; transform: rotate(20deg); animation-delay: 0s; }
  .leaf-2 { bottom: -20px; right: -30px; transform: rotate(-30deg); animation-delay: 3s; }
  .leaf-3 { top: 40%; left: -40px; transform: rotate(60deg); animation-delay: 1.5s; }

  @keyframes sway {
    0%, 100% { transform: rotate(20deg) scale(1); }
    50% { transform: rotate(25deg) scale(1.03); }
  }

  .container {
    width: 100%;
    max-width: 680px;
    position: relative;
    z-index: 1;
  }

  /* TELA INICIAL */
  .screen { display: none; animation: fadeIn 0.5s ease; }
  .screen.active { display: block; }
  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(16px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .card {
    background: var(--off-white);
    border-radius: 24px;
    padding: 48px 48px;
    box-shadow: 0 20px 60px rgba(0,0,0,0.3), 0 1px 0 rgba(255,255,255,0.5) inset;
    position: relative;
    overflow: hidden;
  }

  .card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 4px;
    background: linear-gradient(90deg, var(--verde-claro), var(--dourado), var(--verde-claro));
  }

  .badge {
    display: inline-block;
    background: var(--verde-escuro);
    color: var(--dourado);
    font-size: 11px;
    font-weight: 500;
    letter-spacing: 2.5px;
    text-transform: uppercase;
    padding: 6px 14px;
    border-radius: 20px;
    margin-bottom: 24px;
  }

  h1 {
    font-family: 'Playfair Display', serif;
    font-size: 2.6rem;
    color: var(--verde-escuro);
    line-height: 1.15;
    margin-bottom: 16px;
  }

  h1 em {
    font-style: italic;
    color: var(--verde-claro);
  }

  .intro-text {
    color: #5a6a5e;
    font-size: 1rem;
    line-height: 1.7;
    margin-bottom: 32px;
  }

  .topics {
    display: flex;
    flex-direction: column;
    gap: 10px;
    margin-bottom: 36px;
  }

  .topic-item {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 12px 16px;
    background: rgba(26,58,42,0.05);
    border-radius: 12px;
    border-left: 3px solid var(--verde-claro);
    font-size: 0.92rem;
    color: var(--verde-escuro);
  }

  .topic-icon { font-size: 1.2rem; }

  .btn-start {
    width: 100%;
    padding: 18px;
    background: var(--verde-escuro);
    color: var(--creme);
    font-family: 'DM Sans', sans-serif;
    font-size: 1rem;
    font-weight: 500;
    letter-spacing: 0.5px;
    border: none;
    border-radius: 14px;
    cursor: pointer;
    transition: all 0.25s;
    position: relative;
    overflow: hidden;
  }

  .btn-start::after {
    content: '→';
    margin-left: 8px;
    transition: transform 0.25s;
    display: inline-block;
  }

  .btn-start:hover {
    background: var(--verde-medio);
    transform: translateY(-2px);
    box-shadow: 0 8px 24px rgba(26,58,42,0.3);
  }
  .btn-start:hover::after { transform: translateX(4px); }

  /* TELA DO QUIZ */
  .quiz-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 28px;
    padding: 0 4px;
  }

  .q-counter {
    font-size: 0.85rem;
    color: var(--creme);
    opacity: 0.7;
    letter-spacing: 1px;
  }

  .q-counter span {
    color: var(--dourado);
    font-weight: 500;
    font-size: 1rem;
    opacity: 1;
  }

  .score-display {
    background: rgba(200,169,81,0.15);
    border: 1px solid rgba(200,169,81,0.3);
    color: var(--dourado);
    padding: 5px 14px;
    border-radius: 20px;
    font-size: 0.85rem;
    font-weight: 500;
  }

  .progress-bar {
    height: 3px;
    background: rgba(255,255,255,0.1);
    border-radius: 2px;
    margin-bottom: 28px;
    overflow: hidden;
  }

  .progress-fill {
    height: 100%;
    background: linear-gradient(90deg, var(--verde-claro), var(--dourado));
    border-radius: 2px;
    transition: width 0.5s ease;
  }

  .category-tag {
    display: inline-block;
    font-size: 10px;
    font-weight: 500;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--dourado);
    background: rgba(200,169,81,0.12);
    border: 1px solid rgba(200,169,81,0.25);
    padding: 4px 12px;
    border-radius: 20px;
    margin-bottom: 18px;
  }

  .question-text {
    font-family: 'Playfair Display', serif;
    font-size: 1.45rem;
    color: var(--verde-escuro);
    line-height: 1.45;
    margin-bottom: 28px;
  }

  .options {
    display: flex;
    flex-direction: column;
    gap: 10px;
    margin-bottom: 24px;
  }

  .option-btn {
    padding: 16px 20px;
    background: white;
    border: 2px solid #e8e2d9;
    border-radius: 12px;
    text-align: left;
    font-family: 'DM Sans', sans-serif;
    font-size: 0.95rem;
    color: #3a4a3e;
    cursor: pointer;
    transition: all 0.2s;
    position: relative;
    overflow: hidden;
    display: flex;
    align-items: center;
    gap: 12px;
  }

  .option-letter {
    min-width: 28px;
    height: 28px;
    background: #f0ebe3;
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 0.8rem;
    font-weight: 600;
    color: var(--verde-escuro);
    transition: all 0.2s;
  }

  .option-btn:hover:not(:disabled) {
    border-color: var(--verde-claro);
    background: rgba(74,140,92,0.04);
    transform: translateX(4px);
  }

  .option-btn:hover:not(:disabled) .option-letter {
    background: var(--verde-claro);
    color: white;
  }

  .option-btn.correct {
    border-color: #4a8c5c;
    background: rgba(74,140,92,0.08);
  }
  .option-btn.correct .option-letter {
    background: var(--verde-claro);
    color: white;
  }

  .option-btn.wrong {
    border-color: #c0392b;
    background: rgba(192,57,43,0.06);
  }
  .option-btn.wrong .option-letter {
    background: #c0392b;
    color: white;
  }

  .option-btn:disabled { cursor: default; }

  .feedback-box {
    padding: 16px 20px;
    border-radius: 12px;
    font-size: 0.9rem;
    line-height: 1.6;
    margin-bottom: 20px;
    display: none;
    animation: fadeIn 0.3s ease;
  }
  .feedback-box.show { display: block; }
  .feedback-box.acerto { background: rgba(74,140,92,0.1); border-left: 3px solid var(--verde-claro); color: var(--verde-escuro); }
  .feedback-box.erro { background: rgba(192,57,43,0.08); border-left: 3px solid #c0392b; color: #5a2020; }

  .feedback-box strong { display: block; margin-bottom: 4px; }

  .btn-next {
    width: 100%;
    padding: 16px;
    background: var(--verde-escuro);
    color: var(--creme);
    font-family: 'DM Sans', sans-serif;
    font-size: 0.95rem;
    font-weight: 500;
    border: none;
    border-radius: 12px;
    cursor: pointer;
    transition: all 0.25s;
    display: none;
  }
  .btn-next.show { display: block; animation: fadeIn 0.3s ease; }
  .btn-next:hover { background: var(--verde-medio); transform: translateY(-1px); }

  /* TELA DE RESULTADO */
  .result-header {
    text-align: center;
    margin-bottom: 32px;
  }

  .result-emoji {
    font-size: 4rem;
    display: block;
    margin-bottom: 16px;
    animation: bounce 0.6s ease;
  }

  @keyframes bounce {
    0% { transform: scale(0); }
    60% { transform: scale(1.15); }
    100% { transform: scale(1); }
  }

  .result-score {
    font-family: 'Playfair Display', serif;
    font-size: 3.5rem;
    color: var(--verde-escuro);
    font-weight: 700;
    line-height: 1;
    margin-bottom: 8px;
  }

  .result-label {
    font-size: 0.9rem;
    color: #7a8a7e;
    letter-spacing: 1px;
    text-transform: uppercase;
  }

  .result-message {
    font-family: 'Playfair Display', serif;
    font-style: italic;
    font-size: 1.2rem;
    color: var(--verde-medio);
    text-align: center;
    margin-bottom: 28px;
    padding: 0 16px;
    line-height: 1.5;
  }

  .category-scores {
    background: rgba(26,58,42,0.04);
    border-radius: 14px;
    padding: 20px;
    margin-bottom: 28px;
  }

  .cat-title {
    font-size: 0.75rem;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: #8a9a8e;
    margin-bottom: 14px;
  }

  .cat-row {
    display: flex;
    align-items: center;
    gap: 12px;
    margin-bottom: 12px;
  }

  .cat-name {
    font-size: 0.85rem;
    color: var(--verde-escuro);
    min-width: 160px;
    line-height: 1.3;
  }

  .cat-bar-wrap {
    flex: 1;
    height: 6px;
    background: rgba(26,58,42,0.1);
    border-radius: 3px;
    overflow: hidden;
  }

  .cat-bar-fill {
    height: 100%;
    background: linear-gradient(90deg, var(--verde-claro), var(--dourado));
    border-radius: 3px;
    transition: width 1s ease 0.3s;
  }

  .cat-pts {
    font-size: 0.8rem;
    color: #8a9a8e;
    min-width: 36px;
    text-align: right;
  }

  .btn-restart {
    width: 100%;
    padding: 17px;
    background: var(--verde-escuro);
    color: var(--creme);
    font-family: 'DM Sans', sans-serif;
    font-size: 1rem;
    font-weight: 500;
    border: none;
    border-radius: 14px;
    cursor: pointer;
    transition: all 0.25s;
  }
  .btn-restart:hover { background: var(--verde-medio); transform: translateY(-2px); box-shadow: 0 8px 24px rgba(26,58,42,0.3); }

  @media (max-width: 500px) {
    .card { padding: 32px 24px; }
    h1 { font-size: 2rem; }
    .question-text { font-size: 1.2rem; }
    .cat-name { min-width: 120px; }
  }
</style>
</head>
<body>

<div class="leaf leaf-1">🌿</div>
<div class="leaf leaf-2">🍃</div>
<div class="leaf leaf-3">🌱</div>

<div class="container">

  <!-- TELA INICIAL -->
  <div class="screen active" id="screen-inicio">
    <div class="card">
      <div class="badge">🌍 Quiz Ambiental</div>
      <h1>Natureza &amp; <em>Sociedade</em></h1>
      <p class="intro-text">
        Teste seus conhecimentos sobre como diferentes culturas e a sociedade moderna se relacionam com o meio ambiente. São 15 questões divididas em 3 temas.
      </p>
      <div class="topics">
        <div class="topic-item">
          <span class="topic-icon">🏙️</span>
          <span><strong>Conceito Moderno de Natureza</strong> — Como a visão ocidental contemporânea entende o mundo natural</span>
        </div>
        <div class="topic-item">
          <span class="topic-icon">⚡</span>
          <span><strong>Conflitos Ambientais</strong> — Tensões entre desenvolvimento e preservação na modernidade</span>
        </div>
        <div class="topic-item">
          <span class="topic-icon">🪶</span>
          <span><strong>Outros Povos &amp; Natureza</strong> — Visões indígenas, orientais e tradicionais sobre o meio ambiente</span>
        </div>
      </div>
      <button class="btn-start" onclick="iniciarQuiz()">Começar o Quiz</button>
    </div>
  </div>

  <!-- TELA DO QUIZ -->
  <div class="screen" id="screen-quiz">
    <div class="quiz-header">
      <div class="q-counter">Questão <span id="q-num">1</span> de 15</div>
      <div class="score-display">⭐ <span id="score-live">0</span> pts</div>
    </div>
    <div class="progress-bar">
      <div class="progress-fill" id="progress-fill" style="width:0%"></div>
    </div>
    <div class="card">
      <div class="category-tag" id="q-category">Tema</div>
      <div class="question-text" id="q-text">Pergunta aqui</div>
      <div class="options" id="q-options"></div>
      <div class="feedback-box" id="feedback-box">
        <strong id="feedback-title"></strong>
        <span id="feedback-text"></span>
      </div>
      <button class="btn-next" id="btn-next" onclick="proximaQuestao()">Próxima questão →</button>
    </div>
  </div>

  <!-- TELA DE RESULTADO -->
  <div class="screen" id="screen-resultado">
    <div class="card">
      <div class="result-header">
        <span class="result-emoji" id="result-emoji">🌿</span>
        <div class="result-score" id="result-score">0/15</div>
        <div class="result-label">questões corretas</div>
      </div>
      <div class="result-message" id="result-message"></div>
      <div class="category-scores">
        <div class="cat-title">Desempenho por tema</div>
        <div class="cat-row">
          <div class="cat-name">🏙️ Conceito Moderno</div>
          <div class="cat-bar-wrap"><div class="cat-bar-fill" id="bar-1" style="width:0%"></div></div>
          <div class="cat-pts" id="pts-1">0/5</div>
        </div>
        <div class="cat-row">
          <div class="cat-name">⚡ Conflitos Ambientais</div>
          <div class="cat-bar-wrap"><div class="cat-bar-fill" id="bar-2" style="width:0%"></div></div>
          <div class="cat-pts" id="pts-2">0/5</div>
        </div>
        <div class="cat-row">
          <div class="cat-name">🪶 Outros Povos</div>
          <div class="cat-bar-wrap"><div class="cat-bar-fill" id="bar-3" style="width:0%"></div></div>
          <div class="cat-pts" id="pts-3">0/5</div>
        </div>
      </div>
      <button class="btn-restart" onclick="reiniciar()">🔄 Jogar novamente</button>
    </div>
  </div>

</div>

<script>
const questoes = [
  // TEMA 1: Conceito Moderno de Natureza (5 questões)
  {
    tema: "🏙️ Conceito Moderno de Natureza",
    temaId: 1,
    pergunta: "Na visão ocidental moderna, qual é a principal característica da relação humano-natureza?",
    opcoes: [
      "A natureza é vista como parte integrante e inseparável da vida humana",
      "A natureza é compreendida como um recurso a ser explorado e dominado pelo ser humano",
      "A natureza é reverenciada como uma entidade sagrada e superior ao ser humano",
      "A natureza e o ser humano são considerados em perfeito equilíbrio"
    ],
    correta: 1,
    explicacao: "A modernidade ocidental construiu uma visão dualista que separa natureza e cultura, tratando o mundo natural principalmente como recurso para o desenvolvimento econômico e tecnológico."
  },
  {
    tema: "🏙️ Conceito Moderno de Natureza",
    temaId: 1,
    pergunta: "O conceito de 'serviços ecossistêmicos' reflete que tipo de relação com a natureza?",
    opcoes: [
      "Uma visão espiritual que valoriza a natureza por si mesma",
      "Uma visão biocêntrica que coloca todas as espécies em igualdade",
      "Uma visão utilitarista que quantifica os benefícios que a natureza oferece aos humanos",
      "Uma visão comunitária baseada nos saberes tradicionais indígenas"
    ],
    correta: 2,
    explicacao: "'Serviços ecossistêmicos' é um conceito tipicamente moderno que traduz funções da natureza (como polinização, filtragem da água) em valor econômico, refletindo a lógica utilitarista e de mercado."
  },
  {
    tema: "🏙️ Conceito Moderno de Natureza",
    temaId: 1,
    pergunta: "Qual filósofo influenciou profundamente a visão moderna de que o ser humano seria 'senhor e possuidor da natureza'?",
    opcoes: [
      "Jean-Jacques Rousseau",
      "René Descartes",
      "Immanuel Kant",
      "Friedrich Nietzsche"
    ],
    correta: 1,
    explicacao: "René Descartes, no século XVII, propôs a separação radical entre mente e matéria e a ideia de que a razão humana poderia dominar e controlar a natureza, fundando as bases do pensamento moderno ocidental."
  },
  {
    tema: "🏙️ Conceito Moderno de Natureza",
    temaId: 1,
    pergunta: "O que caracteriza a visão de natureza conhecida como 'biocentrismo'?",
    opcoes: [
      "Acreditar que o ser humano é o centro do universo e a medida de todas as coisas",
      "Defender que todo ser vivo possui valor intrínseco, independente de sua utilidade",
      "Priorizar o desenvolvimento econômico sustentável acima da preservação ambiental",
      "Entender a natureza apenas como paisagem para contemplação humana"
    ],
    correta: 1,
    explicacao: "O biocentrismo defende que todos os seres vivos têm valor em si mesmos, em oposição ao antropocentrismo, que coloca o ser humano como referência central de valor."
  },
  {
    tema: "🏙️ Conceito Moderno de Natureza",
    temaId: 1,
    pergunta: "A Revolução Industrial do século XIX teve qual impacto direto na relação humano-natureza?",
    opcoes: [
      "Levou as populações a viver mais próximo da natureza e valorizá-la mais",
      "Acelerou o processo de exploração da natureza como matéria-prima e energia",
      "Criou leis globais de proteção ambiental inéditas na história",
      "Reduziu o consumo de recursos naturais por meio da eficiência tecnológica"
    ],
    correta: 1,
    explicacao: "A Revolução Industrial intensificou radicalmente a exploração de carvão, minérios e florestas, consolidando a natureza como 'recurso' a serviço da produção, e iniciou a degradação ambiental em escala global."
  },

  // TEMA 2: Conflitos Ambientais na Sociedade Moderna (5 questões)
  {
    tema: "⚡ Conflitos Ambientais na Sociedade Moderna",
    temaId: 2,
    pergunta: "O que são conflitos socioambientais?",
    opcoes: [
      "Disputas exclusivamente entre países por acesso a recursos hídricos",
      "Tensões que surgem quando diferentes grupos têm interesses opostos sobre o uso e controle de um mesmo território ou recurso natural",
      "Guerras ecológicas travadas por movimentos ambientalistas radicais",
      "Conflitos internos de organizações ambientais sobre estratégias de conservação"
    ],
    correta: 1,
    explicacao: "Conflitos socioambientais envolvem populações, empresas e governos com interesses distintos sobre territórios e recursos, como comunidades ribeirinhas vs. usinas hidrelétricas, ou indígenas vs. mineradoras."
  },
  {
    tema: "⚡ Conflitos Ambientais na Sociedade Moderna",
    temaId: 2,
    pergunta: "A construção da Usina Hidrelétrica de Belo Monte, no Pará, é exemplo de qual tipo de conflito ambiental?",
    opcoes: [
      "Conflito entre diferentes espécies animais pelo mesmo habitat",
      "Conflito entre o desenvolvimento energético e os direitos de povos indígenas e ribeirinhos",
      "Disputa entre municípios pelo controle das águas do Rio Xingu",
      "Conflito entre cientistas sobre métodos de medição do impacto ambiental"
    ],
    correta: 1,
    explicacao: "Belo Monte é um caso emblemático de conflito socioambiental no Brasil: a obra deslocou comunidades indígenas e ribeirinhas, alterou o ecossistema do Xingu e gerou disputas jurídicas e protestos internacionais."
  },
  {
    tema: "⚡ Conflitos Ambientais na Sociedade Moderna",
    temaId: 2,
    pergunta: "O que é o conceito de 'injustiça ambiental'?",
    opcoes: [
      "A exploração de animais por empresas sem licença ambiental",
      "A desigualdade na distribuição dos riscos e danos ambientais, que recaem desproporcionalmente sobre populações vulneráveis",
      "A falta de punição legal para crimes contra o meio ambiente",
      "O desequilíbrio entre países ricos e pobres no mercado de carbono"
    ],
    correta: 1,
    explicacao: "Injustiça ambiental ocorre quando comunidades mais pobres, negras ou indígenas sofrem mais os impactos de lixões, indústrias poluentes e desastres ambientais do que a população em geral."
  },
  {
    tema: "⚡ Conflitos Ambientais na Sociedade Moderna",
    temaId: 2,
    pergunta: "Qual é uma consequência direta do desmatamento da Amazônia para o clima do Brasil?",
    opcoes: [
      "Aumento das chuvas em todo o território nacional",
      "Redução das temperaturas nas regiões metropolitanas",
      "Comprometimento dos 'rios voadores', afetando o regime de chuvas no Centro-Oeste e Sudeste",
      "Maior estabilidade climática devido à diminuição da umidade"
    ],
    correta: 2,
    explicacao: "A Amazônia libera enorme quantidade de vapor d'água que forma os chamados 'rios voadores', que irrigam regiões distantes do Brasil. O desmatamento compromete esse ciclo, causando secas e estiagens fora da floresta."
  },
  {
    tema: "⚡ Conflitos Ambientais na Sociedade Moderna",
    temaId: 2,
    pergunta: "O greenwashing é uma prática que consiste em:",
    opcoes: [
      "Pintar instalações industriais de verde para reduzir o impacto visual",
      "Usar práticas agrícolas sustentáveis para recuperar solo degradado",
      "Empresas que fingem ser sustentáveis usando o discurso ambiental para fins de marketing sem mudanças reais",
      "A limpeza de rios e mares feita voluntariamente por comunidades"
    ],
    correta: 2,
    explicacao: "Greenwashing é quando empresas ou governos usam a narrativa ambiental de forma enganosa para melhorar sua imagem, sem implementar mudanças genuínas em suas práticas poluentes ou predatórias."
  },

  // TEMA 3: Como outros povos enxergam a natureza (5 questões)
  {
    tema: "🪶 Outros Povos & Natureza",
    temaId: 3,
    pergunta: "Para a maioria dos povos indígenas brasileiros, qual é a relação entre seres humanos e natureza?",
    opcoes: [
      "O ser humano é superior à natureza e tem o direito de dominá-la",
      "A natureza deve ser preservada apenas para uso das gerações futuras",
      "Os seres humanos fazem parte da natureza e existe uma reciprocidade sagrada entre todos os seres",
      "A natureza é um obstáculo que deve ser superado pelo conhecimento científico"
    ],
    correta: 2,
    explicacao: "Para a maioria dos povos indígenas, humanos, animais, plantas e elementos da natureza formam uma rede de relações de reciprocidade. Não existe separação entre 'cultura' e 'natureza' como no pensamento moderno ocidental."
  },
  {
    tema: "🪶 Outros Povos & Natureza",
    temaId: 3,
    pergunta: "O conceito andino de 'Pachamama' representa:",
    opcoes: [
      "Um deus masculino do sol na cosmologia Inca",
      "A Mãe Terra como entidade viva que merece respeito, gratidão e reciprocidade",
      "Um ritual de colheita praticado no Equador moderno",
      "A luta política dos camponeses bolivianos por reforma agrária"
    ],
    correta: 1,
    explicacao: "Pachamama (Mãe Terra) é um conceito central na cosmovisão de povos andinos como quéchuas e aimarás: a Terra é um ser vivo, com quem se deve manter relação de respeito e gratidão, não de exploração."
  },
  {
    tema: "🪶 Outros Povos & Natureza",
    temaId: 3,
    pergunta: "O conceito japonês de 'Satoyama' descreve:",
    opcoes: [
      "Uma técnica de meditação zen em contato com a natureza",
      "Uma paisagem de interface entre montanha e planície onde humanos e natureza coexistem de forma integrada",
      "Um parque nacional criado no século XIX para preservação de florestas",
      "A filosofia de que a montanha é habitat exclusivo dos espíritos ancestrais"
    ],
    correta: 1,
    explicacao: "Satoyama é a zona de transição entre montanha e vale onde comunidades japonesas tradicionalmente manejavam florestas, campos e rios de forma equilibrada, sendo hoje um modelo de sustentabilidade estudado globalmente."
  },
  {
    tema: "🪶 Outros Povos & Natureza",
    temaId: 3,
    pergunta: "Na cosmovisão de muitos povos africanos, o conceito de 'Ubuntu' se relaciona com a natureza de que forma?",
    opcoes: [
      "Ubuntu é exclusivamente uma filosofia sobre relações humanas, sem relação com a natureza",
      "A ideia de interconexão ('eu sou porque nós somos') se estende à comunidade com a terra e os seres vivos",
      "Ubuntu prega o domínio humano sobre a natureza como forma de comunidade",
      "É uma crença de que a natureza deve ser protegida apenas pelos mais velhos da aldeia"
    ],
    correta: 1,
    explicacao: "Ubuntu ('eu sou porque nós somos') é uma filosofia de interdependência que em muitas tradições africanas se estende além dos humanos, incluindo a terra, os ancestrais e todos os seres vivos como parte da comunidade."
  },
  {
    tema: "🪶 Outros Povos & Natureza",
    temaId: 3,
    pergunta: "O que o pensador Ailton Krenak defende em sua obra 'Ideias para Adiar o Fim do Mundo'?",
    opcoes: [
      "A necessidade de tecnologia avançada para salvar o planeta do colapso climático",
      "A criação de mais unidades de conservação geridas pelo Estado brasileiro",
      "Uma crítica à ideia moderna de humanidade separada da natureza, propondo reencontrar nossa pertença ao mundo vivo",
      "A industrialização sustentável como solução para os problemas ambientais"
    ],
    correta: 2,
    explicacao: "Ailton Krenak, líder indígena e intelectual brasileiro, critica a visão ocidental que separa humanidade de natureza. Ele propõe que 'adiar o fim do mundo' significa resistir a essa narrativa e recuperar a ideia de que somos parte da Terra."
  }
];

let questaoAtual = 0;
let pontuacao = 0;
let acertosPorTema = { 1: 0, 2: 0, 3: 0 };

function mostrarTela(id) {
  document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
  document.getElementById(id).classList.add('active');
}

function iniciarQuiz() {
  questaoAtual = 0;
  pontuacao = 0;
  acertosPorTema = { 1: 0, 2: 0, 3: 0 };
  mostrarTela('screen-quiz');
  carregarQuestao();
}

function carregarQuestao() {
  const q = questoes[questaoAtual];
  const total = questoes.length;

  document.getElementById('q-num').textContent = questaoAtual + 1;
  document.getElementById('score-live').textContent = pontuacao;
  document.getElementById('progress-fill').style.width = (questaoAtual / total * 100) + '%';
  document.getElementById('q-category').textContent = q.tema;
  document.getElementById('q-text').textContent = q.pergunta;

  const letras = ['A', 'B', 'C', 'D'];
  const optionsEl = document.getElementById('q-options');
  optionsEl.innerHTML = '';
  q.opcoes.forEach((opcao, i) => {
    const btn = document.createElement('button');
    btn.className = 'option-btn';
    btn.innerHTML = `<span class="option-letter">${letras[i]}</span><span>${opcao}</span>`;
    btn.onclick = () => responder(i);
    optionsEl.appendChild(btn);
  });

  const fb = document.getElementById('feedback-box');
  fb.className = 'feedback-box';
  const btnNext = document.getElementById('btn-next');
  btnNext.className = 'btn-next';
  btnNext.textContent = questaoAtual === total - 1 ? 'Ver resultado 🌿' : 'Próxima questão →';
}

function responder(indice) {
  const q = questoes[questaoAtual];
  const botoes = document.querySelectorAll('.option-btn');
  botoes.forEach(b => b.disabled = true);

  const acertou = indice === q.correta;
  if (acertou) {
    pontuacao++;
    acertosPorTema[q.temaId]++;
    botoes[indice].classList.add('correct');
  } else {
    botoes[indice].classList.add('wrong');
    botoes[q.correta].classList.add('correct');
  }

  const fb = document.getElementById('feedback-box');
  document.getElementById('feedback-title').textContent = acertou ? '✅ Correto!' : '❌ Não foi dessa vez';
  document.getElementById('feedback-text').textContent = q.explicacao;
  fb.className = 'feedback-box show ' + (acertou ? 'acerto' : 'erro');

  document.getElementById('score-live').textContent = pontuacao;
  document.getElementById('btn-next').classList.add('show');
}

function proximaQuestao() {
  questaoAtual++;
  if (questaoAtual >= questoes.length) {
    mostrarResultado();
  } else {
    carregarQuestao();
  }
}

function mostrarResultado() {
  mostrarTela('screen-resultado');
  const total = questoes.length;
  const pct = pontuacao / total;

  document.getElementById('result-score').textContent = pontuacao + '/' + total;

  let emoji, msg;
  if (pct >= 0.9) {
    emoji = '🌳'; msg = '"Você carrega a floresta dentro de si — um guardião do conhecimento ambiental."';
  } else if (pct >= 0.7) {
    emoji = '🌿'; msg = '"Sua consciência ambiental está florescendo. Continue cultivando esse saber."';
  } else if (pct >= 0.5) {
    emoji = '🌱'; msg = '"Uma semente está germinando. Vale aprofundar o olhar sobre a natureza e seus povos."';
  } else {
    emoji = '🍂'; msg = '"Até a folha que cai tem seu propósito. Cada erro é um passo rumo ao entendimento."';
  }

  document.getElementById('result-emoji').textContent = emoji;
  document.getElementById('result-message').textContent = msg;

  // Barras por tema
  setTimeout(() => {
    [1, 2, 3].forEach(t => {
      const pts = acertosPorTema[t];
      document.getElementById('bar-' + t).style.width = (pts / 5 * 100) + '%';
      document.getElementById('pts-' + t).textContent = pts + '/5';
    });
  }, 200);
}

function reiniciar() {
  mostrarTela('screen-inicio');
}
</script>
</body>
</html>
