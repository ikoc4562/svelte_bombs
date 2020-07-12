<script>
	import {beforeUpdate, afterUpdate, onMount} from 'svelte'
	let attempts=0;
	let bombs=new Array(30);
	let randomNum;
	let interval;

	onMount(()=>{
		interval=setInterval(()=>{
			randomNum=Math.floor(Math.random()*bombs.length)
		},1000)
	})

	afterUpdate(()=>{
		if (attempts==10){
			clearInterval(interval);
			alert('You Lost');
		}
		if (bombs.length==0){
			alert('You won');
		}
	})

	function handleClick(index) {

		if (index==randomNum){
			bombs=[...bombs.slice(0,index),...bombs.slice(index+1)];
		}
		else {
			attempts++;
		}

	}
</script>

<style>
	.bomb{
		width: 40px;
		cursor: pointer;
	}
	.container{
		width: 30%;
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
	}

</style>

<h2>Bomb games</h2>
Attempts : {attempts}

<div class="container">
{#each bombs as _,i}
<div on:click={()=>handleClick(i)}>
	<img src="bomb.png" class="bomb" style="opacity: {randomNum==i?'':'0.3'}">
	</div>
{/each}
</div>


