<script>
    import {createEventDispatcher, onMount} from 'svelte';

    import SmileChinese from "$lib/images/smile_chinese.png";
    import YeaSound from "$lib/audios/yea.mp3";

    let yea_sound;

    export let credit;

    const dispatch = createEventDispatcher();

    function next() {
        yea_sound.pause();
        dispatch("next");
    }

    onMount(() => {
        yea_sound = new Audio(YeaSound);
        yea_sound.play();
        setTimeout(next, 2000);
    })
</script>

<h1>Correct!</h1>
<p>Credit +{credit}</p>
<img src={SmileChinese} alt="correct!" />