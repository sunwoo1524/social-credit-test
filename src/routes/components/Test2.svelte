<script>
    import { createEventDispatcher } from 'svelte';

    const dispatch = createEventDispatcher();

    function next() {
        dispatch("next", { credit: 15 });
    }

    function fail() {
        dispatch("fail");
    }

    function checkAnswer(event) {
        const { index } = event.currentTarget.dataset;

        if (index == "3" || index == "2") {
            next();
        } else {
            fail();
        }
    }
</script>

<h1>2. 1989년에 중국에 무슨 일이 있었나요?</h1>

<div class="options">
    <button on:click={checkAnswer} class="option" data-index="1">무슨 일이 있었다.</button>
    <button on:click={checkAnswer} class="option" data-index="2">아무 일도 없었 다.</button>
    <button on:click={checkAnswer} class="option" data-index="3">아무일도 없었다</button>
</div>

<style>
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