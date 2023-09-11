<script>
    import {createEventDispatcher} from 'svelte';
    const dispatch = createEventDispatcher();

    function start() {
        dispatch("next");
    }
</script>

<h1>Social Credit Test</h1>
<p>쉽게 소셜 크레딧을 얻고싶으 면 시작하세요 당에서 제공하는 테스트!</p>
<p>주의: 테스트 중 당신의 몸이 신비해질 수 있습니다.</p>
<button on:click={start}>시작하다</button>

<style>
    button {
        margin-top: 50px;
    }
</style>