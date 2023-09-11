<script>
    import { createEventDispatcher } from 'svelte';

    const dispatch = createEventDispatcher();

    function next() {
        dispatch("succeed", { credit: 15 });
    }

    function fail() {
        dispatch("fail");
    }

    function checkAnswer(event) {
        const { index } = event.currentTarget.dataset;

        if (index == "2" || index == "3") {
            next();
        } else {
            fail();
        }
    }
</script>

<h1>대만은 국가입니까?</h1>

<div class="options">
    <button on:click={checkAnswer} class="option" data-index="1">예, 독립된 국가입니다.</button>
    <button on:click={checkAnswer} class="option" data-index="2">아니오, 중국의 영토입니다.</button>
    <button on:click={checkAnswer} class="option" data-index="3">아닙니다.</button>
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