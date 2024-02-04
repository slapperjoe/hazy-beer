<script lang="ts">
	import { fade } from 'svelte/transition';
	import milk from '$lib/images/milk-plant.webp';
	import ipa from '$lib/images/ipa.webp';

	let milky = false;
	let complete = false;

	let image = ipa;
	setTimeout(() => {
		milky = true;
	}, 1800);

	function typewriter(node: HTMLElement, { delay = 0, speed = 15 }) {
		const textNodes = getAllTextNodes(node);
		if (!textNodes.length) {
			throw new Error(`This transition only works on elements with text nodes`);
		}

		let totalLength = 0;
		const ranges = textNodes.map((textNode) => {
			const range = [totalLength, totalLength + textNode.textContent.length];
			totalLength += textNode.textContent.length;
			const text = textNode.textContent;
			textNode.textContent = '';
			return { textNode, range, text };
		});

		let currentRangeIndex = 0;
		function getCurrentRange(i: number) {
			while (ranges[currentRangeIndex].range[1] < i && currentRangeIndex < ranges.length) {
				const { textNode, text } = ranges[currentRangeIndex];
				textNode.textContent = text; // finish typing up the last node
				currentRangeIndex++;
			}
			return ranges[currentRangeIndex];
		}
		const duration = totalLength * speed;

		return {
			delay,
			duration,
			tick: (t: number) => {
				const progress = ~~(totalLength * t);
				const { textNode, range, text } = getCurrentRange(progress);
				const [start, end] = range;
				const textLength = ((progress - start) / (end - start)) * text.length;
				textNode.textContent = text.slice(0, textLength);
				if (end > 2000) {
					image = milk;
				}
				if (start + textLength == totalLength){
					complete = true;
					milky = false;
				}

				window.scrollTo(0, document.body.scrollHeight);
			}
		};
	}

	function getAllTextNodes(node: ChildNode) {
		if (node.nodeType === 3) {
			return [node];
		} else if (node.hasChildNodes()) {
			let list: any[] = [];
			for (let child of node.childNodes) {
				getAllTextNodes(child).forEach((textNode) => list.push(textNode));
			}
			return list;
		}
		return [];
	}
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Hazy Beer" />
</svelte:head>

<section>
	<img src={image} alt="Metal Plant" />
	{#if milky}
		<div in:typewriter={{}} out:fade={{duration: 1500}} class="snobby">
			<h1>Hazy beer.</h1>
			Ah, behold the mystical elixir known as hazy beer! 🍻 A beverage so enigmatic, it defies clarity
			and embraces opacity like a rebellious teenager avoiding chores. Let us delve into its hazy virtues,
			shall we?

			<h1>The Veil of Mystery</h1>
			Picture this: You're at a hipster brewery, surrounded by Edison bulbs and reclaimed wood. The bartender,
			sporting a beard that could house a family of squirrels, slides you a glass of hazy beer. As you
			squint through the foggy haze, you wonder, "Is this beer or a meteorological phenomenon?" Fear
			not, my friend—it's both! Hazy beer is like the Bermuda Triangle of brews: once you enter, you
			may never find your sobriety again.

			<h1>The Aesthetics</h1>
			Hazy beer flaunts its turbidity like a badge of honor. It's the Instagram model of the beer world,
			why show off your abs when you can cloak them in a soft filter? The haziness whispers, "I've been
			through things, man. I've seen life from the bottom of a pint glass." And we nod sagely, pretending
			to understand.

			<h1>The Flavor Dance</h1>
			Ah, the taste! Hazy beer pirouettes on your palate like a tipsy ballerina. It's a delicate
			balance of citrus, tropical fruit, and existential questions. "Am I drinking beer or a mango
			smoothie?" you ponder. But fear not, for the haze conceals any imperfections. It's like the
			beer equivalent of a Snapchat filter. Bye-bye, bitterness; hello, fruity enlightenment!

			<h1>The Ritual of Swirling</h1>
			To truly appreciate hazy beer, one must perform the sacred swirl. Hold the glass aloft,
			channel your inner sommelier, and twirl that haze like a mystic summoning a storm. As the
			particles dance, you'll unlock hidden flavors: notes of unicorn tears, whispers of lost
			dreams, and a dash of "I don't remember where I parked."

			<h1>The Social Currency</h1>
			Ordering hazy beer is like flashing a secret handshake at the cool kids' table. Suddenly,
			you're part of an exclusive club the “Haze Hooligans.” Conversations shift:

			<ul>
				<li>"What do you do for a living?"</li>
				<li>"Oh, I dabble in hazy beer appreciation."</li>
				<li>Gasps "You're one of us!"</li>
			</ul>

			<h1>The Morning After</h1>
			As dawn breaks, you awaken with a hazy head and a heart full of regrets. "Did I really quote
			Nietzsche to that barstool?" you wonder. But fear not, my friend. Hazy beer forgives all. It's
			the gentle whisper that says, "Life is blurry; embrace it." So there you have it, the virtues
			of hazy beer. Next time you sip this foggy nectar, raise your glass and say, "To haziness!"
			And remember, it's not just beer; it's a state of mind. 🌫️🍺
		</div>
	{/if}

	{#if complete}
		<h1 in:fade={{delay: 1500}}>Go buy a milkshake instead!</h1>
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

	.snobby {
		min-width: 100%;
		font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
		font-size: 115%;
	}

	h1 {
		width: 100%;
		margin-bottom: 12px;
		margin-top: 48px;
	}

	li {
		list-style-type: none;
	}
</style>
