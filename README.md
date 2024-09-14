<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Online Quiz</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="quiz-container">
        <div id="question-container">
            <h2 id="question"></h2>
            <ul id="options">
                <!-- Options will be added here -->
            </ul>
        </div>
        <button id="submit-btn">Submit</button>
        <div id="results">
            <!-- Results will be displayed here -->
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>

.quiz-container {
    width: 500px;
    margin: 0 auto;
    padding: 20px;
    border: 1px solid #ccc;
}

#question-container {
    margin-bottom: 20px;
}

#options li {
    list-style: none;
    margin-bottom: 10px;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    cursor: pointer;
}

#submit-btn {
    padding: 10px 20px;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

#results {
    margin-top: 20px;
}



const questions = [
    {
        question: "What is the capital of France?",
        options: ["Berlin", "Paris", "Rome", "Madrid"],
        answer: 1 // Index of the correct answer
    },
    // Add more questions here
];

const questionContainer = document.getElementById('question-container');
const optionsList = document.getElementById('options');
const submitBtn = document.getElementById('submit-btn');
const resultsDiv = document.getElementById('results');

let currentQuestion = 0;
let score = 0;

function displayQuestion() {
    const questionData = questions[currentQuestion];
    document.getElementById('question').textContent = questionData.question;
    optionsList.innerHTML = ''; // Clear previous options
    questionData.options.forEach((option, index) => {
        const optionElement = document.createElement('li');
        optionElement.textContent = option;
        optionElement.addEventListener('click', () => checkAnswer(index));
        optionsList.appendChild(optionElement);
    });
}

function checkAnswer(selectedIndex) {
    if (selectedIndex === questions[currentQuestion].answer) {
        score++;
    }
    currentQuestion++;
    if (currentQuestion < questions.length) {
        displayQuestion();
    } else {
        showResults();
    }
}

function showResults() {
    questionContainer.style.display = 'none';
    submitBtn.style.display = 'none';
    resultsDiv.innerHTML = <h2>Your Score: ${score}/${questions.length}</h2>;
}

submitBtn.addEventListener('click', () => {
    checkAnswer(null); // If submit is clicked, consider it wrong
});

displayQuestion(); // Start with the first question
