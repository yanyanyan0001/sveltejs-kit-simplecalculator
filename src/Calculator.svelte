<script>

import { onMount } from 'svelte';
import { fetchResult } from '$lib/api';

let expression = '';
let result = null;


//this handleClick function appends the clicked button's text to the expression.
const handleClick = (event) => {
  expression += event.target.innerText;
};
// this evaluateExpression sends a POST request to the server-side route /api/calculate with the expression as the request body. 
const evaluateExpression = async () => {
 result = await fetchResult(expression);
};


//The onMount function adds an event listener for keydown events when the component mounts.
onMount(() => {
  document.addEventListener('keydown', handleKeyDown);
  });


//this function handleKeyDown listens for key events, allowing users to input numbers and operators using the keyboard. Pressing Enter triggers evaluateExpression, and pressing Escape clears the expression and result
const handleKeyDown = (event) => {
const key = event.key;
 if (key.match(/[0-9.+\-*/]/)) {
  expression += key;
 } else if (key === 'Enter') {
evaluateExpression();
 } else if (key === 'Escape') {
  expression = '';
   result = null;
 }
};
 </script>

<style>
.calculator {
display: grid;
grid-template-columns: repeat(4, 1fr);
grid-gap: 5px;
max-width: 300px;
margin: 0 auto;
}

input {
grid-column: span 4;
height: 40px;
font-size: 18px;
text-align: right;
padding: 5px;
}
button {
  height: 40px;
  font-size: 18px;
}
</style>

 <div>
  <input type="text" bind:value={expression} readonly             
<div>
<button on:click={handleClick}>1</button>
<button on:click={handleClick}>2</button>
<button on:click={handleClick}>3</button>
<button on:click={handleClick}>+</button>
<button on:click={handleClick}>4</button>
<button on:click={handleClick}>5</button>
<button on:click={handleClick}>6</button>
<button on:click={handleClick}>-</button>
<button on:click={handleClick}>7</button>
<button on:click={handleClick}>8</button>
<button on:click={handleClick}>9</button>
<button on:click={handleClick}>*</button>
<button on:click={handleClick}>0</button>
<button on:click={handleClick}>.</button>
<button on:click={handleClick}>/</button>
<button on:click={evaluateExpression}>=</button>
<button on:click={() => (expression = '')}>C</button>
</div>
{#if result !== null}
  <p>Result: {result}</p>
 {/if}
 </div>

 <!--The Calculator.svelte component handles user input and displays the expression and result.-->
