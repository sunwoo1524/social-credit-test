<script>
    import China from "$lib/images/china.svg";
    import USA from "$lib/images/usa.png";
    import Korea from "$lib/images/korea.svg";
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

        if (index == "3") {
            next();
        } else {
            fail();
        }
    }
</script>

<h1>1. 최고의 나라는 무엇인 가요?</h1>

<div class="options">
    <button on:click={checkAnswer} class="option" data-index="1">
        <span>1. 미국</span>
        <img src={USA} alt="미국" />
    </button>
    <button on:click={checkAnswer} class="option" data-index="2">
        <span>2. 한국</span>
        <img src={Korea} alt="한국" />
    </button>
    <button on:click={checkAnswer} class="option" data-index="3">
        <span>3. 중화인민공화국</span>
        <img src={China} alt="중화인민공화국" />
    </button>
</div>

<style>
    .options {
        display: flex;
    }

    span {
        font-size: 20px;
        margin-bottom: 5px;
    }

    .options .option img {
        width: 150px;
    }

    .options .option {
        display: flex;
        flex-direction: column;
        margin: 0 30px;
    }

    @media(max-width: 650px) {
        .options {
            flex-direction: column;
        }

        .options .option {
            margin: 30px 0;
        }
    }
</style>