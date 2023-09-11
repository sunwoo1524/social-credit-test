<script>
    import { createEventDispatcher } from 'svelte';
    import Xi from "$lib/images/시진핑핑이.webp";

    const dispatch = createEventDispatcher();

    function next() {
        dispatch("next", { credit: 15 });
    }

    function fail() {
        dispatch("fail");
    }

    function checkAnswer(event) {
        const { index } = event.currentTarget.dataset;

        if (index == "2") {
            next();
        } else {
            fail();
        }
    }
</script>

<h1>3. 이 사진은 누구의 사진입니 까?</h1>

<img src={Xi} alt="" width="200" />

<div class="options">
    <button on:click={checkAnswer} class="option" data-index="1">핑핑이</button>
    <button on:click={checkAnswer} class="option" data-index="2">위대한 우리의 지도자, 시진핑 주석</button>
    <button on:click={checkAnswer} class="option" data-index="3">곰돌이 푸</button>
</div>

<style>
    img {
        margin-bottom: 50px;
    }

    .options {
        display: flex;
    }

    .options .option {
        display: flex;
        flex-direction: column;
        margin: 0 30px;
        font-size: 20px;
        margin-bottom: 5px;
    }
</style>