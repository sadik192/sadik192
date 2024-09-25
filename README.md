<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic Tac Toe</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin-top: 50px;
        }

        .game-board {
            display: grid;
            grid-template-columns: repeat(3, 100px);
            grid-template-rows: repeat(3, 100px);
            gap: 5px;
            justify-content: center;
        }

        .cell {
            width: 100px;
            height: 100px;
            background-color: lightgray;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 2em;
            cursor: pointer;
        }

        .cell:hover {
            background-color: lightblue;
        }

        #reset-button {
            margin-top: 20px;
            padding: 10px 20px;
            font-size: 16px;
        }
    </style>
</head>
<body>
    <h1>Tic Tac Toe</h1>
    <div class="game-board">
        <div class="cell" data-index="0"></div>
        <div class="cell" data-index="1"></div>
        <div class="cell" data-index="2"></div>
        <div class="cell" data-index="3"></div>
        <div class="cell" data-index="4"></div>
        <div class="cell" data-index="5"></div>
        <div class="cell" data-index="6"></div>
        <div class="cell" data-index="7"></div>
        <div class="cell" data-index="8"></div>
    </div>
    <button id="reset-button">Reset Game</button>

    <script>
        let board = ['', '', '', '', '', '', '', '', ''];
        let currentPlayer = 'X';
        let isGameOver = false;

        const cells = document.querySelectorAll('.cell');
        const resetButton = document.getElementById('reset-button');

        cells.forEach(cell => {
            cell.addEventListener('click', handleCellClick);
        });

        resetButton.addEventListener('click', resetGame);

        function handleCellClick(e) {
            const index = e.target.getAttribute('data-index');
            
            if (board[index] === '' && !isGameOver) {
                board[index] = currentPlayer;
                e.target.textContent = currentPlayer;
                
                if (checkWin()) {
                    alert(currentPlayer + ' wins!');
                    isGameOver = true;
                } else if (board.every(cell => cell !== '')) {
                    alert('It\'s a draw!');
                    isGameOver = true;
                } else {
                    currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
                }
            }
        }

        function checkWin() {
            const winningCombinations = [
                [0, 1, 2], [3, 4, 5], [6, 7, 8], 
                [0, 3, 6], [1, 4, 7], [2, 5, 8], 
                [0, 4, 8], [2, 4, 6]
            ];

            return winningCombinations.some(combination => {
                return combination.every(index => board[index] === currentPlayer);
            });
        }

        function resetGame() {
            board = ['', '', '', '', '', '', '', '', ''];
            currentPlayer = 'X';
            isGameOver = false;
            cells.forEach(cell => cell.textContent = '');
        }
    </script>
</body>
</html>
