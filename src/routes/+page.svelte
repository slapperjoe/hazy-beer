<script lang='ts'>
	import { fade } from 'svelte/transition';
	import milk from '$lib/images/milk-plant.webp';

	let milky = false;
	let para = 1;
	let tickend = [0];
	setTimeout(()=>{milky = true;}, 1000);

	function typewriter(node, { speed = 2 }) {
		const valid = node.childNodes.length === 1 && node.childNodes[0].nodeType === Node.TEXT_NODE;

		if (!valid) {
			throw new Error(`This transition only works on elements with a single text node child`);
		}

		const text = node.textContent;
		const duration = text.length / (speed * 0.01);

		//if (Number(node.childNodes.attr.para) >= para){

			return {
				duration,
				tick: (t) => {
					const i = Math.trunc(text.length * (t));
					if (i == text.length){
						tickend.push(t)
					}
					node.textContent = text.slice(0, i);
				}
			};
		//}
	};
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Hazy Beer" />
</svelte:head>

<section>
	<img src={milk} alt="Metal Plant"/>
	<h1>
		Hazy beer.
	</h1>
	{#if milky}
	<div transition:typewriter para="1">	
	Ah, behold the mystical elixir known as hazy beer! 🍻 A beverage so enigmatic, it defies clarity and embraces opacity like a rebellious teenager avoiding chores. Let us delve into its hazy virtues, shall we? 
	</div>
	<h1 transition:typewriter para="2">The Veil of Mystery</h1> 
	<div transition:typewriter para="3">	
	Picture this: You’re at a hipster brewery, surrounded by Edison bulbs and reclaimed wood. The bartender, sporting a beard that could house a family of squirrels, slides you a glass of hazy beer. As you squint through the foggy haze, you wonder, “Is this beer or a meteorological phenomenon?” Fear not, my friend—it’s both! Hazy beer is like the Bermuda Triangle of brews: once you enter, you may never find your sobriety again. 
	</div>
	<h1>The Aesthetics</h1>
<div transition:typewriter para="3">	
Hazy beer flaunts its turbidity like a badge of honor. It’s the Instagram model of the beer world—why show off your abs when you can cloak them in a soft filter? The haziness whispers, “I’ve been through things, man. I’ve seen life from the bottom of a pint glass.” And we nod sagely, pretending to understand. 
</div>
<h1>The Flavor Dance</h1> 
<div transition:typewriter para="4">	
Ah, the taste! Hazy beer pirouettes on your palate like a tipsy ballerina. It’s a delicate balance of citrus, tropical fruit, and existential questions. “Am I drinking beer or a mango smoothie?” you ponder. But fear not, for the haze conceals any imperfections. It’s like the beer equivalent of a Snapchat filter—bye-bye, bitterness; hello, fruity enlightenment! 
</div>
<h1>The Ritual of Swirling</h1> 
<div transition:typewriter para="5">	
To truly appreciate hazy beer, one must perform the sacred swirl. Hold the glass aloft, channel your inner sommelier, and twirl that haze like a mystic summoning a storm. As the particles dance, you’ll unlock hidden flavors: notes of unicorn tears, whispers of lost dreams, and a dash of “I don’t remember where I parked.” 
</div>
<h1>The Social Currency</h1> 
<div transition:typewriter para="6">	
Ordering hazy beer is like flashing a secret handshake at the cool kids’ table. Suddenly, you’re part of an exclusive club—the “Haze Hooligans.” Conversations shift: 

    “What do you do for a living?” 

    “Oh, I dabble in hazy beer appreciation.” 

    Gasps “You’re one of us!” 
	
<h1>The Morning After</h1> 
<div transition:typewriter para="7">	
As dawn breaks, you awaken with a hazy head and a heart full of regrets. “Did I really quote Nietzsche to that barstool?” you wonder. But fear not, my friend. Hazy beer forgives all. It’s the gentle whisper that says, “Life is blurry; embrace it.” 

So there you have it—the virtues of hazy beer. Next time you sip this foggy nectar, raise your glass and say, “To haziness!” And remember, it’s not just beer; it’s a state of mind. 🌫️🍺 
</div>
	
	{/if}


</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

	h1 {
		width: 100%;
	}

	h2 {
		margin-top: -14px;
	}

</style>
