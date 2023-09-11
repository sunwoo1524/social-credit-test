<script>
    import { onMount } from 'svelte';

    // Childs
    import Home from "./components/Home.svelte";
    import Correct from "./components/Correct.svelte";
    import Incorrect from './components/Incorrect.svelte';
    import Success from './components/Success.svelte';
    import Test1 from './components/Test1.svelte';
    import Test2 from "./components/Test2.svelte";
    import Test3 from './components/Test3.svelte';
    import Test4 from './components/Test4.svelte';

    // medias
    import RedSunInTheSky from "$lib/audios/하늘의 태양은 붉다.mp3";
    import FailTest from "$lib/audios/fail_test.mp3";
    import ChingChengHanji from "$lib/audios/chingchenghanji.mp3";
    
    let redsuninthesky;
    let fail_test_music;
    let chingchenghanji;
    
    let page;

    let credit = 0;
    let is_allow_to_get_position = false;
    let credit_added = null;
    let is_correct = null;
    let success = false;
    let page_index = 0;

    let x;
    let y;

    onMount(() => {
        navigator.geolocation.getCurrentPosition((position) =>{
            is_allow_to_get_position = true;
            x = position.coords.latitude;
            y = position.coords.longitude;
        }, ()=>{});
        redsuninthesky = new Audio(RedSunInTheSky);
        redsuninthesky.loop = true;

        fail_test_music = new Audio(FailTest);
        fail_test_music.loop = true;

        chingchenghanji = new Audio(ChingChengHanji);
        chingchenghanji.loop = true;
    });

    function slide() {
        // slide next
        page_index = page_index + 1;
        page.style.left = -page_index * 100 + "%";
        // page.style.left = -page.clientWidth * page_index + "px";
    }

    function start() {
        redsuninthesky.play();
        slide();
    }

    function correct(event) {
        credit_added = event.detail.credit;
        credit = credit + credit_added;
        is_correct = true;
        page.style.display = "none";
    }

    function next() {
        page.style.display = "flex";
        is_correct = null;
        credit_added = null;
        slide();
    }

    function fail(event) {
        redsuninthesky.pause();
        fail_test_music.play();
        page.style.display = "none";
        is_correct = false;
        credit = credit - 2147483648;
    }

    function succeed() {
        success = true;
        page.style.display = "none";
        redsuninthesky.pause();
        chingchenghanji.play();
    }
</script>

<svelte:head>
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"
        integrity="sha256-p4NxAoJBhIIN+hmNHrzRCf9tD/miZyoHS5obTRR9BMY="
        crossorigin=""/>
    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"
        integrity="sha256-20nQCchB9co0qIjJZRGuk2/Z9VM+kNiyxNV1lvTlZBo="
        crossorigin=""></script>
</svelte:head>

{#if is_allow_to_get_position}
<p class="credit">Your Social Credit: {credit}</p>
<div class="test-view" bind:this={page}>
    <div class="view">
        <Home on:next={start}></Home>
    </div>

    <div class="view">
        <Test1 on:next={correct} on:fail={fail}></Test1>
    </div>

    <div class="view">
        <Test2 on:next={correct} on:fail={fail}></Test2>
    </div>

    <div class="view">
        <Test3 on:next={correct} on:fail={fail}></Test3>
    </div>

    <div class="view">
        <Test4 on:succeed={succeed} on:fail={fail}></Test4>
    </div>
</div>
{/if}

{#if is_correct}
<Correct credit={credit_added} on:next={next}></Correct>
{:else if is_correct == false}
<Incorrect x={x} y={y}></Incorrect>
{/if}

{#if success}
<Success credit={credit}></Success>
{/if}

<footer>
    <p>记住1989年的天安门</p>
</footer>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Nanum+Myeongjo&display=swap');

    :global(*) {
        font-family: 'Nanum Myeongjo', serif;
    }

    :global(body,html) {
        width: 100%;
        height: 100%;
        overflow: hidden;
    }
    :global(body) {
        margin: 0;
        padding-top: 100px;
        background-color: red;
        color: white;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .test-view {
        display: flex;
        width: 100%;
        position: relative;
        left: 0;
        transition: left 0.15s;
    }

    .test-view .view {
        display: flex;
        flex-direction: column;
        align-items: center;
        overflow: hidden;
        flex-shrink: 0;
        width: 100%;
    }

    :global(h1) {
        font-size: 50px;
    }

    :global(p) {
        font-size: 20px;
    }

    :global(button) {
        font-size: 30px;
        background-color: rgba(0, 0, 0, 0);
        color: white;
        border: none;
        cursor: pointer;
    }

    :global(button:focus) {
        outline: 0;
    }

    @media(max-width: 650px) {
        :global(h1) {
            font-size: 30px;
        }
    }

    .credit {
        font-size: 25px;
    }

    footer {
        margin-top: 100px;
    }
</style>