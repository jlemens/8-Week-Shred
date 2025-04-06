<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stage Ready: 8 Weeks to Shred</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f0f2f5;
            margin: 0;
            padding: 20px;
            color: #333;
        }

        .game-container {
            max-width: 800px;
            margin: 0 auto;
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        h1 {
            text-align: center;
            color: #2c3e50;
            margin-bottom: 10px;
        }

        h2.subtitle {
            text-align: center;
            color: #2c3e50;
            margin-top: -10px;
            margin-bottom: 30px;
        }

        .goals-container {
            background-color: #f8f9fa;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 20px;
            border: 2px solid #2ecc71;
        }

        .goals-container h2 {
            color: #2c3e50;
            margin-top: 0;
        }

        .goal-item {
            display: flex;
            align-items: center;
            margin: 10px 0;
        }

        .goal-icon {
            margin-right: 10px;
            font-size: 1.2em;
        }

        .stats-container {
            background-color: #f8f9fa;
            padding: 20px;
            border-radius: 8px;
            margin-bottom: 20px;
        }

        .stats {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 10px;
        }

        .stats p {
            margin: 5px 0;
            font-size: 1.3em;  /* Increased from 1.1em */
        }

        .stat-value {
            font-size: 28px;  /* Increased from 24px */
            font-weight: bold;
            color: #202124;
        }

        .choices-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-bottom: 20px;
        }

        .workout-choices {
            order: 1;
        }

        .diet-choices {
            order: 2;
        }

        .diet-choices, .workout-choices {
            background-color: #f8f9fa;
            padding: 20px;
            border-radius: 8px;
        }

        .options {
            display: grid;
            grid-template-columns: 1fr;
            gap: 10px;
        }

        button {
            padding: 12px;
            border: none;
            border-radius: 5px;
            background-color: #3498db;
            color: white;
            cursor: pointer;
            font-size: 1em;
            transition: all 0.3s ease;
        }

        button:hover {
            background-color: #2980b9;
        }

        button:disabled {
            background-color: #95a5a6;
            cursor: not-allowed;
        }

        button.selected {
            background-color: #2ecc71;
            transform: scale(1.02);
        }

        .run-button {
            display: block;
            width: 200px;
            margin: 20px auto;
            padding: 15px;
            font-size: 1.2em;
            background-color: #e74c3c;
        }

        .run-button:hover {
            background-color: #c0392b;
        }

        .play-again-button {
            display: none;
            width: 200px;
            margin: 20px auto;
            padding: 15px;
            font-size: 1.2em;
            background-color: #2ecc71;
        }

        .play-again-button:hover {
            background-color: #27ae60;
        }

        .feedback-container {
            background-color: #f8f9fa;
            padding: 20px;
            border-radius: 8px;
            min-height: 100px;
        }

        #feedback {
            margin-top: 10px;
            line-height: 1.5;
            font-size: 1.2em;  /* Increased size */
        }

        #additionalFeedback {
            margin-top: 10px;
            color: #e74c3c;
            font-weight: bold;
        }

        .goal {
            font-weight: bold;
            color: #2ecc71;
        }

        .warning {
            color: #e74c3c;
        }

        .warning-message {
            color: #e74c3c;
            font-weight: bold;
            margin-top: 10px;
            padding: 10px;
            background-color: #fde8e8;
            border-radius: 5px;
            border-left: 4px solid #e74c3c;
            font-size: 1.2em;  /* Increased size */
        }

        .selection-status {
            text-align: center;
            margin: 10px 0;
            font-weight: bold;
            font-size: 1.2em;  /* Increased size */
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.5);
            z-index: 1000;
        }

        .modal-content {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            max-width: 500px;
            width: 90%;
            text-align: center;
        }

        .modal h2 {
            color: #2c3e50;
            margin-bottom: 15px;
        }

        .modal p {
            margin-bottom: 20px;
            line-height: 1.5;
            font-size: 1.2em;  /* Increased size */
        }

        .modal button {
            margin: 10px;
            padding: 10px 20px;
        }

        @keyframes statChange {
            0% { transform: scale(1); }
            50% { transform: scale(1.2); color: #2ecc71; }
            100% { transform: scale(1); }
        }

        @keyframes statChangeDecrease {
            0% { transform: scale(1); }
            50% { transform: scale(1.2); color: #2ecc71; }
            100% { transform: scale(1); }
        }

        @keyframes statChangeIncrease {
            0% { transform: scale(1); }
            50% { transform: scale(1.2); color: #e74c3c; }
            100% { transform: scale(1); }
        }

        @keyframes weekChange {
            0% { transform: scale(1); }
            50% { transform: scale(1.2); color: #2ecc71; }
            100% { transform: scale(1); }
        }

        .stat-changed {
            animation: statChange 1s ease-in-out;
        }

        .stat-changed-decrease {
            animation: statChangeDecrease 1s ease-in-out;
        }

        .stat-changed-increase {
            animation: statChangeIncrease 1s ease-in-out;
        }

        .week-changed {
            animation: weekChange 1s ease-in-out;
        }

        @media (min-width: 768px) {
            .choices-container {
                grid-template-columns: 1fr 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="game-container">
        <h1>💪 Stage Ready: 8 Weeks to Shred 💪</h1>
        <h2 class="subtitle">Can you coach Tony to success?</h2>
        
        <div class="goals-container">
            <h2>🏆 Tony's Competition Goals</h2>
            <div class="goal-item">
                <span class="goal-icon">🎯</span>
                <span>Body Fat: Less than 10%</span>
            </div>
            <div class="goal-item">
                <span class="goal-icon">💪</span>
                <span>Muscle Mass: At least 105 lbs</span>
            </div>
            <div class="goal-item">
                <span class="goal-icon">⏱️</span>
                <span>Time: 8 Weeks</span>
            </div>
        </div>

        <div class="stats-container">
            <h2>Current Stats</h2>
            <div class="stats">
                <p>Week: <span id="week">0</span>/8</p>
                <p>Weight: <span id="weight">200</span> lbs</p>
                <p>Body Fat: <span id="bodyFat">15.5</span>%</p>
                <p>Muscle Mass: <span id="muscleMass">110</span> lbs</p>
            </div>
        </div>

        <div class="selection-status" id="selectionStatus">
            Select a diet and workout option to begin
        </div>

        <div class="choices-container">
            <div class="workout-choices">
                <h2>Workout Options</h2>
                <div class="options">
                    <button onclick="makeChoice(1, 'workout')">High Lifting, High Cardio</button>
                    <button onclick="makeChoice(2, 'workout')">Normal Lifting, High Cardio</button>
                    <button onclick="makeChoice(3, 'workout')">Normal Lifting and Normal Cardio</button>
                    <button onclick="makeChoice(4, 'workout')">Normal Lifting, No Cardio</button>
                    <button onclick="makeChoice(5, 'workout')">No Lifting, No Cardio</button>
                </div>
            </div>

            <div class="diet-choices">
                <h2>Diet Options</h2>
                <div class="options">
                    <button onclick="makeChoice(1, 'diet')">High Calorie Diet</button>
                    <button onclick="makeChoice(2, 'diet')">Slightly More Than Normal</button>
                    <button onclick="makeChoice(3, 'diet')">Normal Calorie Diet</button>
                    <button onclick="makeChoice(4, 'diet')">Slightly Less Than Normal</button>
                    <button onclick="makeChoice(5, 'diet')">Low Calorie Diet</button>
                </div>
            </div>
        </div>

        <button class="run-button" onclick="runWeek()" disabled>Run Week</button>
        <button class="play-again-button" onclick="resetGame()">Play Again</button>

        <div class="feedback-container">
            <h2>Progress</h2>
            <div id="feedback"></div>
            <div id="additionalFeedback"></div>
        </div>
    </div>

    <div id="resultModal" class="modal">
        <div class="modal-content">
            <h2 id="modalTitle">Week Complete!</h2>
            <p id="modalMessage"></p>
            <div style="margin-top: 20px;">
                <button onclick="closeModal()">Continue</button>
                <button onclick="resetGame()" class="play-again-button" style="display: none;">Play Again</button>
            </div>
        </div>
    </div>

    <script>
        class Game {
            constructor() {
                this.week = 0;
                this.weight = 200;
                this.bodyFat = 15.5;
                this.muscleMass = 110;
                this.dietChoice = null;
                this.workoutChoice = null;
                this.feedback = [];
                this.lastDietChoice = null;
                this.lastWorkoutChoice = null;
                this.dietEffectMultiplier = 1;
                this.workoutEffectMultiplier = 1;
                this.consecutiveNormalWorkouts = 0;
                this.usedLowCalorie = false;
                this.lowCalorieCount = 0;
                this.metabolismSlowed = false;
                this.metabolismWarningShown = false;
                this.previousBodyFat = 15.5;
            }
    
            applyDietEffects(choice) {
                switch(choice) {
                    case 1: return { fat: 1.8, muscle: 0.6 };
                    case 2: return { fat: 0.9, muscle: 0.3 };
                    case 3: return { fat: 0.2, muscle: 0.0 };
                    case 4: return { fat: -0.7, muscle: -0.4 };
                    case 5: return { fat: -0.9, muscle: -0.9 };
                }
            }
    
            applyWorkoutEffects(choice) {
                switch(choice) {
                    case 1: return { fat: -1.9, muscle: -1.9 };
                    case 2: return { fat: -1.2, muscle: -1.5 };
                    case 3: return { fat: -0.0, muscle: 0.0 };
                    case 4: return { fat: 0.7, muscle: 0.3 };
                    case 5: return { fat: 1.0, muscle: 0.0 };
                }
            }
    
            makeChoice(choice, type) {
                const buttons = document.querySelectorAll(`.${type}-choices button`);
                buttons.forEach(btn => btn.classList.remove('selected'));
    
                const selectedButton = buttons[choice - 1];
                selectedButton.classList.add('selected');
    
                if (type === 'diet') {
                    if (this.lastDietChoice === choice) {
                        this.dietEffectMultiplier = 1;
                    } else if (this.lastDietChoice !== null) {
                        this.dietEffectMultiplier = 0.5;
                    }
                    this.lastDietChoice = choice;
                    this.dietChoice = choice;
                } else {
                    if (this.lastWorkoutChoice === choice) {
                        this.workoutEffectMultiplier = 1;
                    } else if (this.lastWorkoutChoice !== null) {
                        this.workoutEffectMultiplier = 0.5;
                    }
                    this.lastWorkoutChoice = choice;
                    this.workoutChoice = choice;
                }
    
                this.updateSelectionStatus();
    
                if (this.dietChoice && this.workoutChoice) {
                    document.querySelector('.run-button').disabled = false;
                }
            }
    
            runWeek() {
                if (!this.dietChoice || !this.workoutChoice) return;
                this.previousBodyFat = this.bodyFat;
    
                const previousStats = {
                    weight: this.weight,
                    bodyFat: this.bodyFat,
                    muscleMass: this.muscleMass
                };
    
            
    
                if (this.dietChoice === 5) {
                    this.usedLowCalorie = true;
                    this.lowCalorieCount++;
                    
                    if (this.lowCalorieCount >= 3 && !this.metabolismSlowed) {
                        this.metabolismSlowed = true;
                        this.metabolismWarningShown = true;
                        let feedback = document.getElementById('additionalFeedback');
                        feedback.innerHTML = '<div class="warning-message">⚠️ Warning: Tony\'s metabolism has slowed down due to prolonged low-calorie dieting. His body is conserving energy, making fat loss more difficult.</div>';
                    } else if (this.metabolismSlowed) {
                        let feedback = document.getElementById('additionalFeedback');
                        feedback.innerHTML = '<div class="warning-message">⚠️ Warning: Tony\'s metabolism has slowed down due to prolonged low-calorie dieting. His body is conserving energy, making fat loss more difficult.</div>';
                    }
                }
    
                const dietEffects = this.applyDietEffects(this.dietChoice);
                const workoutEffects = this.applyWorkoutEffects(this.workoutChoice);
    
                if (this.workoutChoice === 3) {
                    this.consecutiveNormalWorkouts++;
                } else {
                    this.consecutiveNormalWorkouts = 0;
                }
    
                let totalFatChange = (dietEffects.fat * this.dietEffectMultiplier) + 
                                   (workoutEffects.fat * this.workoutEffectMultiplier);
    
                let totalMuscleChange = (dietEffects.muscle * this.dietEffectMultiplier) + 
                                      (workoutEffects.muscle * this.workoutEffectMultiplier);
    
                if (this.metabolismSlowed) {
                    if (totalFatChange < 0) totalFatChange *= 0.5;
                    if (totalMuscleChange < 0) totalMuscleChange *= 0.5;
                }
    
                this.bodyFat += totalFatChange;
                this.muscleMass += totalMuscleChange;
    
                const weightFromFat = totalFatChange * 2;
                const weightFromMuscle = totalMuscleChange;
                this.weight += weightFromFat + weightFromMuscle;
    
                this.weight = Math.max(0, this.weight);
                this.bodyFat = Math.max(0, this.bodyFat);
                this.muscleMass = Math.max(0, this.muscleMass);
    
                this.week++;
                this.updateUI();
                this.animateStats(previousStats);
                
                this.dietChoice = null;
                this.workoutChoice = null;
                document.querySelectorAll('button').forEach(btn => btn.classList.remove('selected'));
                document.querySelector('.run-button').disabled = true;
                this.updateSelectionStatus();
    
                this.showResultModal();
    
                if (this.week >= 8) {
                    document.querySelector('.run-button').style.display = 'none';
                }
            }
    
            animateStats(previousStats) {
                const stats = ['weight', 'bodyFat', 'muscleMass'];
                stats.forEach(stat => {
                    const element = document.getElementById(stat);
                    const currentValue = parseFloat(element.textContent);
                    const previousValue = previousStats[stat];
                    
                    if (stat === 'muscleMass') {
                        element.classList.add('stat-changed');
                    } else {
                        if (currentValue < previousValue) {
                            element.classList.add('stat-changed-decrease');
                        } else if (currentValue > previousValue) {
                            element.classList.add('stat-changed-increase');
                        } else {
                            element.classList.add('stat-changed');
                        }
                    }
    
                    setTimeout(() => {
                        element.classList.remove('stat-changed', 'stat-changed-decrease', 'stat-changed-increase');
                    }, 1000);
                });
    
                const weekElement = document.getElementById('week');
                weekElement.classList.add('week-changed');
                setTimeout(() => {
                    weekElement.classList.remove('week-changed');
                }, 1000);
            }
    
            updateSelectionStatus() {
                const status = document.getElementById('selectionStatus');
                if (!this.dietChoice && !this.workoutChoice) {
                    status.textContent = "Select a diet and workout option to begin";
                } else if (this.dietChoice && !this.workoutChoice) {
                    status.textContent = "Diet selected. Now select a workout option";
                } else if (!this.dietChoice && this.workoutChoice) {
                    status.textContent = "Workout selected. Now select a diet option";
                } else {
                    status.textContent = "Both options selected. Click 'Run Week' to proceed";
                }
            }
    
            showResultModal() {
                const modal = document.getElementById('resultModal');
                const modalTitle = document.getElementById('modalTitle');
                const modalMessage = document.getElementById('modalMessage');
                const playAgainButton = modal.querySelector('.play-again-button');
                const continueButton = modal.querySelector('button:not(.play-again-button)');
    
                if (this.week === 8) {
                    if (this.bodyFat <= 10 && this.muscleMass >= 105) {
                        modalTitle.textContent = "🎉 Congratulations!";
                        if (this.usedLowCalorie) {
                            modalMessage.textContent = "Tony won the competition, but his morale was low throughout the process due to the strict diet. Maybe next time we can find a more balanced approach!";
                        } else {
                            modalMessage.textContent = "Tony is stage-ready! You've found the perfect balance between weight loss and maintaining strength!";
                        }
                    } else {
                        modalTitle.textContent = "😔 Keep Trying";
                        modalMessage.textContent = "Tony needs more work to be competition-ready. Remember, finding the right routine and sticking with it is key!";
                    }
                    playAgainButton.style.display = "inline-block";
                    continueButton.style.display = "none";
                } else if (this.week % 2 === 0) {
                    modalTitle.textContent = "Progress Check: Week " + this.week;
                    
                    if (this.bodyFat > this.previousBodyFat) {
                        const warningMessages = [
                            "❌ Tony's body fat is increasing! This won't help him get stage-ready.",
                            "⚠️ We're moving in the wrong direction - body fat should be decreasing!",
                            "🚫 This approach isn't working - Tony's body fat is going up instead of down.",
                            "⚠️ Warning: Body fat increase detected. We need to change strategy.",
                            "❌ This isn't competition prep - body fat is moving in the wrong direction!"
                        ];
                        modalMessage.textContent = warningMessages[Math.floor(Math.random() * warningMessages.length)];
                    } else if (this.consecutiveNormalWorkouts >= 2) {
                        modalMessage.textContent = "Tony's responding well to this consistent routine!";
                    } else if (this.workoutEffectMultiplier < 1) {
                        modalMessage.textContent = "Tony might do better with a more consistent training schedule.";
                    } else if (this.bodyFat > 15) {
                        modalMessage.textContent = "Tony's still carrying some extra weight. Consider adjusting the approach.";
                    } else if (this.muscleMass < 105) {
                        modalMessage.textContent = "Watch out! Tony's losing some strength. Maybe adjust the intensity?";
                    } else {
                        modalMessage.textContent = "Good progress! Keep going with what's working.";
                    }
                    playAgainButton.style.display = "none";
                    continueButton.style.display = "inline-block";
                } else {
                    return;
                }
    
                modal.style.display = "block";
            }
    
            updateUI() {
                document.getElementById('week').textContent = this.week;
                document.getElementById('weight').textContent = this.weight.toFixed(1);
                document.getElementById('bodyFat').textContent = this.bodyFat.toFixed(1);
                document.getElementById('muscleMass').textContent = this.muscleMass.toFixed(1);
    
                let feedback = `Week ${this.week} Complete!\n`;
                
                if (this.week === 8) {
                    if (this.bodyFat <= 10 && this.muscleMass >= 105) {
                        feedback += "🎉 Congratulations! Tony is stage-ready!";
                    } else {
                        feedback += "😔 Tony needs more work to be competition-ready.";
                    }
                } else {
                    if (this.bodyFat <= 10) {
                        feedback += "Body fat is at target level.";
                    } else if (this.muscleMass < 105) {
                        feedback += "Muscle mass is below target.";
                    } else if (this.workoutEffectMultiplier < 1) {
                        feedback += "Training consistency could be improved.";
                    } else {
                        feedback += "Keep working.";
                    }
                }
    
                document.getElementById('feedback').textContent = feedback;
    
                let additionalFeedback = document.getElementById('additionalFeedback');
                
                // Check for metabolism warning first (highest priority)
                if (this.metabolismSlowed) {
                    additionalFeedback.innerHTML = '<div class="warning-message">⚠️ Warning: Tony\'s metabolism has slowed down due to prolonged low-calorie dieting. His body is conserving energy, making fat loss more difficult.</div>';
                } 
                // Then check for the specific workout/diet combination
                else if (this.workoutChoice === 2 && this.dietChoice === 4) {
                    additionalFeedback.innerHTML = '<div class="warning-message" style="color: red;">⚠️ Tony is losing muscle mass due to working hard and not eating enough.</div>';
                } else {
                    additionalFeedback.textContent = '';
                }
            }
    
            reset() {
                this.week = 0;
                this.weight = 200;
                this.bodyFat = 15.5;
                this.muscleMass = 110;
                this.dietChoice = null;
                this.workoutChoice = null;
                this.lastDietChoice = null;
                this.lastWorkoutChoice = null;
                this.dietEffectMultiplier = 1;
                this.workoutEffectMultiplier = 1;
                this.consecutiveNormalWorkouts = 0;
                this.usedLowCalorie = false;
                this.lowCalorieCount = 0;
                this.metabolismSlowed = false;
                this.metabolismWarningShown = false;
                this.previousBodyFat = 15.5;
                this.updateUI();
                this.updateSelectionStatus();
                document.querySelector('.run-button').style.display = 'block';
                document.querySelector('.play-again-button').style.display = 'none';
                document.querySelector('.run-button').disabled = true;
                document.getElementById('additionalFeedback').textContent = '';
                closeModal();
            }
        }
    
        const game = new Game();
    
        function makeChoice(choice, type) {
            game.makeChoice(choice, type);
        }
    
        function runWeek() {
            game.runWeek();
        }
    
        function resetGame() {
            game.reset();
        }
    
        function closeModal() {
            document.getElementById('resultModal').style.display = "none";
        }
    
        window.onclick = function(event) {
            const modal = document.getElementById('resultModal');
            if (event.target == modal) {
                closeModal();
            }
        }
    </script>
</body>
</html>
