<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Grade Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #121212;
            color: #e0e0e0;
        }
        .container {
            max-width: 600px;
            margin: 50px auto;
            padding: 20px;
            background: #1e1e1e;
            border-radius: 8px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.4);
        }
        h1 {
            text-align: center;
            margin-bottom: 20px;
            color: #bb86fc;
        }
        .form-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 5px;
            color: #a0a0a0;
        }
        input[type="text"] {
            width: 100%;
            padding: 10px;
            box-sizing: border-box;
            border: 1px solid #333;
            border-radius: 4px;
            background-color: #2a2a2a;
            color: #e0e0e0;
        }
        button {
            width: 100%;
            padding: 10px;
            border: none;
            border-radius: 4px;
            background-color: #bb86fc;
            color: #121212;
            font-size: 16px;
            cursor: pointer;
            margin-bottom: 10px;
            transition: background-color 0.3s ease;
        }
        button:hover {
            background-color: #9c66f7;
        }
        .results {
            margin-top: 20px;
            text-align: center;
        }
        .results h3 {
            color: #bb86fc;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Grade Calculator</h1>
        <div id="gradeInputs">
            <div class="form-group">
                <label for="grade1">Grade 1 (percentage or fraction):</label>
                <input type="text" id="grade1">
            </div>
        </div>
        <button id="addGrade">Add Another Grade</button>
        <button id="calculate">Calculate Average</button>
        <button id="dropLowest">Drop Lowest Grade</button>

        <div class="results">
            <h3>Results:</h3>
            <p id="output">No grades entered yet.</p>
        </div>
    </div>

    <script>
        let gradeInputs = document.getElementById("gradeInputs");
        let grades = [];

        document.getElementById("addGrade").addEventListener("click", () => {
            const newGradeDiv = document.createElement("div");
            newGradeDiv.classList.add("form-group");
            const newGradeInput = document.createElement("input");
            newGradeInput.type = "text";
            newGradeInput.placeholder = `Grade ${grades.length + 2} (percentage or fraction)`;
            gradeInputs.appendChild(newGradeDiv);
            newGradeDiv.appendChild(newGradeInput);
        });

        document.getElementById("calculate").addEventListener("click", () => {
            const inputs = gradeInputs.querySelectorAll("input");
            grades = [];

            inputs.forEach(input => {
                const value = input.value.trim();

                if (value.includes("/")) {
                    const [numerator, denominator] = value.split("/").map(Number);
                    if (!isNaN(numerator) && !isNaN(denominator) && denominator !== 0) {
                        grades.push((numerator / denominator) * 100);
                    }
                } else {
                    const percentage = parseFloat(value);
                    if (!isNaN(percentage)) {
                        grades.push(percentage);
                    }
                }
            });

            if (grades.length > 0) {
                const average = grades.reduce((a, b) => a + b, 0) / grades.length;
                document.getElementById("output").textContent = `Average Grade: ${average.toFixed(2)}%`;
            } else {
                document.getElementById("output").textContent = "Please enter valid grades.";
            }
        });

        document.getElementById("dropLowest").addEventListener("click", () => {
            if (grades.length > 1) {
                const lowest = Math.min(...grades);
                grades = grades.filter(grade => grade !== lowest);
                const average = grades.reduce((a, b) => a + b, 0) / grades.length;
                document.getElementById("output").textContent = `Lowest grade dropped. New Average: ${average.toFixed(2)}%`;
            } else {
                document.getElementById("output").textContent = "Not enough grades to drop the lowest.";
            }
        });
    </script>
</body>
</html>

<!---
random1203/random1203 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
