<script>
    // import { csv } from "d3-fetch";
    import { onMount } from 'svelte';
    // import { get } from 'svelte/store';

    import Chart from './components/chart/Chart.svelte';
    import Combobox from './components/combobox/Combobox.svelte';

    
    // VARIABLES
    let data = [];
    let response, value;

    // COMBOBOX
    const comboboxOptions = [
    	{ text: "Abbotsford", value: "abbotsford" },
    	{ text: "Vancouver", value: "vancouver" }
  	]

    // FETCH
    const url = 'https://api.coindesk.com/v1/bpi/currentprice.json';

  
    // REACTIVE VARS
    // $: <some var>

    // FUNCTIONS
    async function init() {
        // get data
        try {
            await fetch(url)
                .then(response => response.json())
                .then(resolveData => {
                    // PROCESS DATA HERE
                    data = resolveData;
                })
        } catch(err) {
            console.log(`Error: ${err}`)
        }
    }

    onMount(init);
</script>


<!-- HTML -->
<header>
    <h1>VS SvelteKit Template</h1>
    <p class="subhead">Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
</header>

<!-- Combobox to pick city -->
<Combobox bind:value
    label=''
    name='city'
    placeholder='Pick a city...'
    options={comboboxOptions}
/>
<pre class="status">CBOX value: {value || ''}</pre>



<!-- FETCH DATA -->
{#await response}
    <h3>Loading data...</h3>
{:then resolveData}
    {console.log(data)}
    <Chart data={data} value={value} />
{/await}




<footer>
    <p class="note">NOTE: tk.</p>
    <p class="source">Source:  <a href="https:vancouversun.com" target="_blank">TK</a></p>
</footer>

<style>
    @import '../css/normalize.css';
    @import '../css/fonts.css';
    @import '../css/colors.css';
    @import './+page.css';
</style>