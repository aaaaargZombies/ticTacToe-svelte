<script>

	let player = "X";
	let board = new Array(9).fill("");
	
	const onClick = index => {
		if (board[index] !== "") return;
		board[index] = player;
		player = winner(lines,board) ? winner(lines,board) : player === "O" ? "X" : "O";
	}

	const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6]
  ];

	const winner = (lines, board) => {
		for (let line of lines) {
			const [a,b,c] = line;
			if (board[a] === board[b] && board[b] === board[c]) return board[a];
		}
		return null;
	}

	const draw = board => board.every(x => x !== "")

	
</script>

<style>

* {
	box-sizing: border-box;
	margin: 0px;
	padding: 0px;
}

	main {
		display:grid;
		grid-template-rows: 20vh 80vh;
		grid-gap: 10px;

	}
	main div {
		  display: flex;
  		align-items: center;
  		justify-content: center;
	}

	ul{ 
		padding:0;
		height: 100%;
		display: grid;
		grid-template-columns: 1fr 1fr 1fr;
		grid-template-rows: 1fr 1fr 1fr;
		list-style:none;
		grid-gap: 10px;
	}
	
	li {
		  display: flex;
  		align-items: center;
  		justify-content: center;
	}
	h1 { 
		font-size: 5em;
		font-style: bold;
		color: white;
	}
	
</style>

<main>

<div style="background-color: hsla({Math.random() * 360},100%,50%,50%)">
	<h1>{player} {winner(lines,board) ?"Wins!":"Play!"}</h1>
</div>

<ul>
{#each board as square, i}
<li 
	on:click={ winner(lines,board) || draw(board) ? () => board = new Array(9).fill("") : () => onClick(i)} 
	style="background-color: hsla({Math.random() * 360},100%,50%,50%)"
	>
		<h1>{square}</h1>
	</li>

{/each}
</ul>

</main>
