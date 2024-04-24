<script>
    export let reverse = false

    const imgCol = 7;
    const imgRow = 6;

    let imgFrame = 0;
    let frameCoord = [0, 0];

    setInterval(() => {
        imgFrame++;
        if (imgFrame +3 >= imgCol * imgRow) {
            imgFrame = 0
        }
        frameCoord = [imgFrame % imgCol, Math.floor(imgFrame / imgCol)]
    },300)
</script>

<div class="cowboy {reverse ? 'reverse' : ''}" style="background-position: -{frameCoord[0]}em -{frameCoord[1]}em" />

<style>
    .cowboy {
        background-image: url('spriesheet-complete.png');
        background-size: 7em 6em;
        image-rendering: pixelated;
        font-size: 120px;
        width: 1em;
        height: 1em;
    }
    .reverse {
        transform: scaleX(-1);
    }
</style>