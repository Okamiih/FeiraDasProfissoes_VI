const scenarios = [
    {
        text: "Um funcionário envia um relatório sem revisar os dados.",
        options: [
            "O funcionário fez um bom trabalho.",
            "O funcionário deve revisar os dados antes de enviar.",
            "Não é importante revisar os dados."
        ],
        correct: 1
    },
    {
        text: "Um gerente ignora as opiniões da equipe ao tomar uma decisão.",
        options: [
            "As opiniões da equipe são sempre desnecessárias.",
            "O gerente deve considerar as opiniões da equipe.",
            "O gerente é quem sabe o que é melhor."
        ],
        correct: 1
    },
    {
        text: "Um departamento não comunica as mudanças de procedimento.",
        options: [
            "A comunicação é fundamental em uma empresa.",
            "Não há necessidade de comunicar mudanças.",
            "Mudanças não afetam o trabalho do dia a dia."
        ],
        correct: 0
    },
    {
        text: "Um funcionário não respeita os prazos estabelecidos.",
        options: [
            "Os prazos não são importantes.",
            "Cumprir prazos é essencial para a produtividade.",
            "Os prazos podem ser ignorados."
        ],
        correct: 1
    },
    {
        text: "Uma equipe não realiza reuniões para alinhar os objetivos.",
        options: [
            "Reuniões não trazem resultados.",
            "Alinhar objetivos é importante para o sucesso do time.",
            "Reuniões são uma perda de tempo."
        ],
        correct: 1
    },
    {
        text: "Um gerente não fornece feedback aos seus colaboradores.",
        options: [
            "Feedback é fundamental para o desenvolvimento.",
            "Feedback pode ser dispensado.",
            "Os colaboradores não precisam de feedback."
        ],
        correct: 0
    },
    {
        text: "Um projeto é iniciado sem um planejamento adequado.",
        options: [
            "Planejamento é opcional.",
            "Todo projeto deve ter um planejamento.",
            "Projetos podem ser executados sem planejamento."
        ],
        correct: 1
    },
    {
        text: "Um funcionário não organiza seu tempo e tarefas.",
        options: [
            "Organização não é necessária.",
            "Organizar o tempo é essencial para a eficiência.",
            "Não importa como as tarefas são realizadas."
        ],
        correct: 1
    },
    {
        text: "Uma empresa não realiza avaliações de desempenho.",
        options: [
            "Avaliações de desempenho ajudam a melhorar a equipe.",
            "Avaliações não têm impacto.",
            "É desnecessário avaliar o desempenho dos colaboradores."
        ],
        correct: 0
    },
    {
        text: "Um colaborador não conhece a missão e visão da empresa.",
        options: [
            "Conhecer a missão e visão não é importante.",
            "Todos devem conhecer a missão e visão da empresa.",
            "Missão e visão são apenas palavras."
        ],
        correct: 1
    }
];

let currentScenario = 0;
let correctCount = 0;
let incorrectCount = 0;

const scenarioText = document.getElementById("scenario-text");
const optionsContainer = document.getElementById("options-container");
const nextButton = document.getElementById("next-button");
const resultText = document.getElementById("result");
const correctCountDisplay = document.getElementById("correct-count");
const incorrectCountDisplay = document.getElementById("incorrect-count");

function loadScenario() {
    const scenario = scenarios[currentScenario];
    scenarioText.textContent = scenario.text;
    optionsContainer.innerHTML = "";

    scenario.options.forEach((option, index) => {
        const div = document.createElement("div");
        div.classList.add("option");
        div.textContent = option;
        div.addEventListener("click", () => checkAnswer(index));
        optionsContainer.appendChild(div);
    });

    nextButton.classList.add("hidden");
    resultText.classList.add("hidden");
}

function checkAnswer(selectedIndex) {
    const scenario = scenarios[currentScenario];
    if (selectedIndex === scenario.correct) {
        correctCount++;
        resultText.textContent = "Correto! Você identificou o erro.";
    } else {
        incorrectCount++;
        resultText.textContent = "Incorreto! Tente novamente.";
    }

    correctCountDisplay.textContent = correctCount;
    incorrectCountDisplay.textContent = incorrectCount;

    nextButton.classList.remove("hidden");
    resultText.classList.remove("hidden");
}

nextButton.addEventListener("click", () => {
    currentScenario++;
    if (currentScenario < scenarios.length) {
        loadScenario();
    } else {
        // Mensagem final com base no desempenho
        scenarioText.textContent = "Você completou o jogo!";
        optionsContainer.innerHTML = "";

        if (correctCount > 7) {
            resultText.textContent = "Parabéns! Você acertou mais de 7. Pegue sua recompensa!";
        } else {
            resultText.textContent = "Parabéns! Você concluiu o jogo. Pegue sua recompensa!";
        }

        nextButton.classList.add("hidden");
        resultText.classList.remove("hidden");
    }
});

// Load the first scenario on page load
loadScenario();
