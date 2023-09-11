<script>
    import { onMount, onDestroy } from 'svelte';
    import { browser } from '$app/environment';
    import FailEmoji from "$lib/images/fail_emoji.png";
    // import L from "leaflet";

    export let x;
    export let y;

    let mapElement;
    let map;

    onMount(async () => {
        if(browser) {
            const L = await import("leaflet");
            const map = L.map('map').setView([x, y], 13);

            L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
                maxZoom: 19,
                attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>'
            }).addTo(map);

            let marker = L.marker([x, y]).addTo(map);
        }
    });

    onDestroy(async () => {
        if(map) {
            console.log('Unloading Leaflet map.');
            map.remove();
        }
    });
</script>

<h1>INCORRECT!!!!!</h1>
<p>Credit -2147483648</p>
<img src={FailEmoji} alt="" />
<p>사형집행일: 오늘</p>
<p>지금 공안이 당신의 위치로 출동합니다.</p>
<div id="map" bind:this={mapElement}></div>

<style>
    @import 'leaflet/dist/leaflet.css';

    #map {
        width: 100%;
        max-width: 500px;
        height: 400px;
    }
</style>