<script>
    // import { csv } from "d3-fetch";
    import { onMount } from 'svelte';
    import { get } from 'svelte/store';

    import Combobox from './components/combobox/Combobox.svelte';

    
    // VARIABLES
    let data, promise, value;
    const comboboxOptions = [
    	{ text: "Abbotsford", value: "abbotsford" },
    	{ text: "Vancouver", value: "vancouver" }
  	]

    const testFile = 'https://vs-postmedia-data.sfo2.digitaloceanspaces.com/misc/test-data-02.csv';

    // REACTIVE VARS


    // FUNCTIONS
    function init() {
        console.log('INIT!')
        
        // get data
        promise = fetch(testFile)
            .then(resolvedData => {
                console.log(resolvedData)
                data = resolvedData;
            });
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
<pre class="status">Selected: {value || ''}</pre>

{#await promise}
    <h2>Loading...</h2>
{:then resolvedData}
    <pre>{`Resolved data: ${JSON.stringify(data)}`}</pre>
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