# Palanguzhi-
Traditional Tamil game inspired app”
export default function PalanguzhiGame() { const initialBoard = [5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 0, 0];

const [board, setBoard] = React.useState(initialBoard); const [player, setPlayer] = React.useState(1); const [message, setMessage] = React.useState("Player 1's turn");

const pitsPerPlayer = 6; const player1Store = 12; const player2Store = 13;

const isPlayerPit = (index) => { if (player === 1) return index >= 0 && index < 6; return index >= 6 && index < 12; };

const handlePitClick = (index) => { if (!isPlayerPit(index)) return; if (board[index] === 0) return;

let newBoard = [...board];
let stones = newBoard[index];
newBoard[index] = 0;

let current = index;

while (stones > 0) {
  current = (current + 1) % 12;
  newBoard[current] += 1;
  stones--;
}

setBoard(newBoard);
const nextPlayer = player === 1 ? 2 : 1;
setPlayer(nextPlayer);
setMessage(`Player ${nextPlayer}'s turn`);

};

const resetGame = () => { setBoard(initialBoard); setPlayer(1); setMessage("Player 1's turn"); };

return ( <div className="min-h-screen bg-amber-100 flex flex-col items-center justify-center p-6"> <div className="bg-white rounded-3xl shadow-2xl p-8 max-w-4xl w-full"> <h1 className="text-4xl font-bold text-center text-amber-700 mb-2"> Palanguzhi Game </h1>

<p className="text-center text-gray-600 mb-8">
      Traditional Tamil Strategy Game
    </p>

    <div className="text-center mb-6">
      <span className="bg-amber-500 text-white px-4 py-2 rounded-full text-lg font-semibold">
        {message}
      </span>
    </div>

    <div className="space-y-6">
      <div className="grid grid-cols-6 gap-4">
        {board
          .slice(6, 12)
          .reverse()
          .map((stones, idx) => {
            const actualIndex = 11 - idx;
            return (
              <button
                key={actualIndex}
                onClick={() => handlePitClick(actualIndex)}
                className="bg-orange-200 hover:bg-orange-300 transition-all rounded-2xl h-24 flex flex-col items-center justify-center shadow-lg"
              >
                <span className="text-2xl font-bold text-amber-900">
                  {stones}
                </span>
                <span className="text-sm text-gray-700 mt-1">
                  Pit {actualIndex + 1}
                </span>
              </button>
            );
          })}
      </div>

      <div className="grid grid-cols-6 gap-4">
        {board.slice(0, 6).map((stones, idx) => (
          <button
            key={idx}
            onClick={() => handlePitClick(idx)}
            className="bg-yellow-200 hover:bg-yellow-300 transition-all rounded-2xl h-24 flex flex-col items-center justify-center shadow-lg"
          >
            <span className="text-2xl font-bold text-amber-900">
              {stones}
            </span>
            <span className="text-sm text-gray-700 mt-1">
              Pit {idx + 1}
            </span>
          </button>
        ))}
      </div>
    </div>

    <div className="flex justify-center mt-8">
      <button
        onClick={resetGame}
        className="bg-amber-600 hover:bg-amber-700 text-white px-6 py-3 rounded-2xl text-lg font-semibold shadow-lg"
      >
        Restart Game
      </button>
    </div>

    <div className="mt-8 bg-amber-50 rounded-2xl p-5">
      <h2 className="text-xl font-bold text-amber-700 mb-3">
        How to Play
      </h2>
      <ul className="list-disc pl-5 text-gray-700 space-y-2">
        <li>Each pit starts with 5 shells.</li>
        <li>Players take turns selecting pits from their side.</li>
        <li>The shells are distributed one-by-one counterclockwise.</li>
        <li>The player with the most collected shells wins.</li>
      </ul>
    </div>
  </div>
</div>

); }
