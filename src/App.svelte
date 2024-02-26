<script lang="ts">
  import "./app.css";

  $: {
    const winner = calculateWinner(board);
    if (winner) {
      alert(`Winner: ${winner}`);
      board = Array(9).fill(null);
    }
  }

  let next = "X";
  let board = Array(9).fill(null);

  const tour = (i: number) => {
    if (board[i] === null) {
      board[i] = next;
      next = next === "X" ? "O" : "X";
    }
  };

  const calculateWinner = (squares: string[]) => {
    const lines = [
      [0, 1, 2],
      [3, 4, 5],
      [6, 7, 8],
      [0, 3, 6],
      [1, 4, 7],
      [2, 5, 8],
      [0, 4, 8],
      [2, 4, 6],
    ];
    for (let i = 0; i < lines.length; i++) {
      const [a, b, c] = lines[i];
      if (
        squares[a] &&
        squares[a] === squares[b] &&
        squares[a] === squares[c]
      ) {
        return squares[a];
      }
    }

    if (squares.every((cell) => cell !== null)) {
      alert("Draw");
      board = Array(9).fill(null);
    }

    return null;
  };
</script>

<main class="h-screen flex flex-col pb-32 justify-center items-center">
  <div class="text-center pb-12">
    <h1 class="text-4xl font-bold mb-4">Kółko i krzyżyk</h1>
    <p class="text-lg">Tura: {next}</p>
  </div>
  <div class="grid grid-cols-3 grid-rows-3 gap-2">
    {#each board as cell, i}
      <button class="w-16 h-16 border-2 border-black" on:click={() => tour(i)}>
        {cell || " "}
      </button>
    {/each}
  </div>
</main>
