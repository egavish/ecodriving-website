
<script>
    import { onMount, onDestroy } from 'svelte';
    import { browser } from '$app/environment';
    import ChartContainer from "./ChartContainer.svelte";
    import boston_sample from "../data/Boston"

    let mapElement;
    let map;
    $: bostonClicked = false;
    $: losangelesClicked = false;
    $: seattleClicked = false;
    $: sanfranciscoClicked = false;
    $: saltlakecityClicked = false;
    $: atlantaClicked = false;
    $: chicagoClicked = false;
    $: newyorkcityClicked = false;
    $: dallasClicked = false;
    $: houstonClicked = false;


    onMount(async () => {
        if(browser) {
            const leaflet = await import('leaflet');

            map = leaflet.map(mapElement).setView([39.5, -94.3], 4);

            leaflet.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
                attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
            }).addTo(map);

            const LeafIcon = L.Icon.extend({
                options: {
                iconSize:     [38, 95],
                shadowSize:   [50, 64],
                iconAnchor:   [22, 94],
                shadowAnchor: [4, 62],
                popupAnchor:  [-3, -76]
                }
            });
            const greenIcon = new LeafIcon({
                iconUrl: 'http://leafletjs.com/examples/custom-icons/leaf-green.png',
                shadowUrl: 'http://leafletjs.com/examples/custom-icons/leaf-shadow.png'
            })
            const markerIcon = L.icon({
                iconSize: [25, 41],
                iconAnchor: [10, 41],
                popupAnchor: [2, -40],
                // specify the path here
                iconUrl: "https://unpkg.com/leaflet@1.5.1/dist/images/marker-icon.png",
                });            
            let boston = leaflet.marker([42.36, -71.05])
            let losangeles = leaflet.marker([34.05, -118.05])
            let seattle = leaflet.marker([47.6, -122.33])
            let sanfrancisco = leaflet.marker([37.45, -122.26])
            let saltlakecity = leaflet.marker([40.76, -111.87])
            let atlanta = leaflet.marker([33.75, -84.38])
            let chicago = leaflet.marker([41.88, -87.62])
            let newyorkcity = leaflet.marker([40.718, -74.006])
            let dallas = leaflet.marker([32.77, -96.79])
            let houston = leaflet.marker([29.76, -95.37])
            boston.addTo(map).on('click', function(e){
                if (!bostonClicked) {
                    boston.setIcon(greenIcon);
                    bostonClicked = true;}
                else {
                    boston.setIcon(markerIcon);
                    bostonClicked = false;}
            }).bindTooltip("Boston", 
                {
                    permanent: true, 
                    direction: 'right'
                })
            losangeles.addTo(map).on('click', function(e){
                if (!losangelesClicked) {
                    losangeles.setIcon(greenIcon);
                    losangelesClicked = true;}
                else {
                    losangeles.setIcon(markerIcon);
                    losangelesClicked = false;}
            }).bindTooltip("Los Angeles", 
                {
                    permanent: true, 
                    direction: 'right'
                })

            seattle.addTo(map).on('click', function(e){
                if (!seattleClicked) {
                    seattle.setIcon(greenIcon);
                    seattleClicked = true;}
                else {
                    seattle.setIcon(markerIcon);
                    seattleClicked = false;}
            }).bindTooltip("Seattle", 
                {
                    permanent: true, 
                    direction: 'right'
                })
            sanfrancisco.addTo(map).on('click', function(e){
                if (!sanfranciscoClicked) {
                    sanfrancisco.setIcon(greenIcon);
                    sanfranciscoClicked = true;}
                else {
                    sanfrancisco.setIcon(markerIcon);
                    sanfranciscoClicked = false;}
            }).bindTooltip("San Francisco", 
                {
                    permanent: true, 
                    direction: 'right'
                })
            saltlakecity.addTo(map).on('click', function(e){
                if (!saltlakecityClicked) {
                    saltlakecity.setIcon(greenIcon);
                    saltlakecityClicked = true;}
                else {
                    saltlakecity.setIcon(markerIcon);
                    saltlakecityClicked = false;}
            }).bindTooltip("Salt Lake City", 
                {
                    permanent: true, 
                    direction: 'right'
                })
            atlanta.addTo(map).on('click', function(e){
                if (!atlantaClicked) {
                    atlanta.setIcon(greenIcon);
                    atlantaClicked = true;}
                else {
                    atlanta.setIcon(markerIcon);
                    atlantaClicked = false;}
            }).bindTooltip("Atlanta", 
                {
                    permanent: true, 
                    direction: 'right'
                })
            chicago.addTo(map).on('click', function(e){
                if (!chicagoClicked) {
                    chicago.setIcon(greenIcon);
                    chicagoClicked = true;}
                else {
                    chicago.setIcon(markerIcon);
                    chicagoClicked = false;}
            }).bindTooltip("Chicago", 
                {
                    permanent: true, 
                    direction: 'right'
                })
            newyorkcity.addTo(map).on('click', function(e){
                if (!newyorkcityClicked) {
                    newyorkcity.setIcon(greenIcon);
                    newyorkcityClicked = true;}
                else {
                    newyorkcity.setIcon(markerIcon);
                    newyorkcityClicked = false;}
            }).bindTooltip("New York City", 
                {
                    permanent: true, 
                    direction: 'right'
                })
            dallas.addTo(map).on('click', function(e){
                if (!dallasClicked) {
                    dallas.setIcon(greenIcon);
                    dallasClicked = true;}
                else {
                    dallas.setIcon(markerIcon);
                    dallasClicked = false;}
            }).bindTooltip("Dallas", 
                {
                    permanent: true, 
                    direction: 'right'
                })
            houston.addTo(map).on('click', function(e){
                if (!houstonClicked) {
                    houston.setIcon(greenIcon);
                    houstonClicked = true;}
                else {
                    houston.setIcon(markerIcon);
                    houstonClicked = false;}
            }).bindTooltip("Houston", 
                {
                    permanent: true, 
                    direction: 'right'
                })
            
        }
    });
    onDestroy(async () => {
        if(map) {
            console.log('Unloading Leaflet map.');
            map.remove();
        }
    });
</script>


<main>
    <section>
    <div bind:this={mapElement}></div>

    {#if bostonClicked}
    <ChartContainer type={"lineChart"} chartProps={{ chart: true, chartWidth: 640, chartHeight: 500, data: boston_sample, xVar: "adoptionRate", yVars: ["co2_reduction"]}} />
    {:else} 
    <ChartContainer type={"lineChart"} chartProps={{ chart: false, chartWidth: 640, chartHeight: 500, data: boston_sample, xVar: "adoptionRate", yVars: ["co2_reduction"]}} />
    {/if}
    </section>
</main>

<style>
    @import 'leaflet/dist/leaflet.css';
    main div {
        height: 500px;
        width: 700px;
        margin: auto;
        align-items: center;
    }

    main section {
        display: flex;
        flex-direction: row;
    }
</style>