<script>
    import RangeSlider from "svelte-range-slider-pips";
    import  LeafletMap from './LeafletMap.svelte';
    import List from './List.svelte';
    import weddings from "../data/weddings";
    import ChartContainer from "./ChartContainer.svelte";
    import sample_boston from "../data/Boston"
    import Description from "./Description.svelte";

    let fullyEV = false;
    let ecoEV = false;
    let num = [50];
    // let placeholder = "What do you need to do?";
    let todo_text = "";
    let todos = [
		'Learn Svelte',
		'Finish Lab'
    ];

    function add() {
        todos = todos.concat(todo_text);
        todo_text = "";
    }
    // $: bostonGraph = bostonClicked;

</script>


<main>
    <h1>What if the traffic light was always green for you and the planet?</h1>
    
    <!-- <input
            placeholder={placeholder}
		bind:value={todo_text}
	>
    <button on:click={add}> -->
        
    <!-- </button> -->
    <div id='slider'><RangeSlider bind:values={num} all='label'suffix='%' pipstep=10 pips/></div>
    
    <p>Percent Connected Intersections</p>

    <p><input type=checkbox bind:checked={ecoEV}>
        All eco-driving vehicles are electric.</p>
    <p><input type=checkbox bind:checked={fullyEV}>
        Fully electric vehicle environment. </p>

    {#if fullyEV}
        <p>All vehicles in the scenario are electric vehicles. {num}% of intersections are connected.</p>
    {:else if ecoEV}
        <p>All eco-driving vehicles in the scenario are electric. The portion of other vehicles that are electric aligns with current and predicted rates of electrification. {num}% of intersections are connected.</p>
    {:else}
        <p>{num}% of intersections are connected.</p>
    {/if}
    <p>Select Cities:</p>
    <LeafletMap></LeafletMap>
    <Description/>
    <List />


</main>


<style global>
    @import url('https://fonts.googleapis.com/css2?family=Nunito:wght@300;400;700&display=swap');
    * {
        margin: 0;
        padding: 0;
        border: 0;
        outline: 0;
        font-size: 100%;
        vertical-align: baseline;
        background: aliceblue;
        color: #03312E;
    }
    main {
        text-align: center;
        font-family: 'Nunito', sans-serif;
        background-color: aliceblue;
        margin: 0;
    }

    h1 {
        font-size: 50px;
        font-weight: 300;
        color: #03312E;

    }

    main div {
        width: 50%;
        margin: auto;
    }
</style>


