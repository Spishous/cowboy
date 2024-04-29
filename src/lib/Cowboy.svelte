<script lang="ts">
    import animations from './animation.json';
    const animationsCowboy = animations['cowboy'] as Animation
    type Animation = {
        imgCol: number,
        imgRow: number,
        default: string,
        animations: AnimeSection[]
    }
    type AnimeSection = {
        [key: string]: {
            frame: number[],
            speed: number,
            loop: boolean
        }
    }
    export let name = 'cowboy'
    export let skinID = 0
    export let reverse = false
    let alreadyDrawn = false
    let alreadyFired = false
    let victoryCount = 0
    let animationName = 'idle'
    let gameover = false
    let _currentFrame = 0
    let _looper: number | undefined = undefined
    let _frameCoord = [0, 0]
    let _animationsSection = animationsCowboy.animations[skinID] as AnimeSection
    startAnimation()
    
    function startAnimation(anime: string | null = null) {
        if (anime) animationName = anime
        stopAnimation()
        _currentFrame = 0
        _looper = setInterval(() => {
            _currentFrame = (_currentFrame + 1) % _animationsSection[animationName].frame.length
            _frameCoord = getFrameCoord(_currentFrame, animations['cowboy'])
            if (!_animationsSection[animationName].loop && isAnimationAtEnd()) {
                switch (animationName) {
                    case 'shoot':
                        idle()
                        break
                    default:
                        clearInterval(_looper)
                        break
                }
            }
        }, 600 / _animationsSection[animationName].speed)
    }

    function getFrameCoord(frame: number, currentAnimations: Animation) {
        const offset: number = currentAnimations.animations[skinID][animationName].frame[frame]
        return [offset % currentAnimations.imgCol, Math.floor(offset / currentAnimations.imgCol)]
    }

    function stopAnimation() {
        if (_looper) clearInterval(_looper)
    }

    function isAnimationAtEnd() {
        return _currentFrame == _animationsSection[animationName].frame.length - 1
    }

    export function shoot() {
        if (!alreadyFired) {
            alreadyFired = true
            startAnimation('shoot')
        }
    }

    export function draw() {
        if (!alreadyDrawn) {
            alreadyDrawn = true
            startAnimation('draw')
        }
    }

    export function die() {
        gameover = true
        startAnimation('die')
    }

    export function idle() {
        startAnimation('idle')
    }

    export function reload() {
        alreadyFired = false
        alreadyDrawn = false
        gameover = false
        idle()
    }

</script>
<span style="display: none">{name}</span>
<div class="cowboy {reverse ? 'reverse' : ''}" style="background-position: -{_frameCoord[0]}em -{_frameCoord[1]}em" />

<style>
    .cowboy {
        background-image: url('/spriesheet-complete.png');
        background-size: 7em 6em;
        image-rendering: pixelated;
        font-size: 180px;
        width: 1em;
        height: 1em;
        position: relative;
    }
    .cowboy::after {
        content: '';
        position: absolute;
        top: 100%;
        left: 0;
        right: 10%;
        width: .3em;
        margin: auto;
        height: 4px;
        background-color: rgba(31, 29, 27, 0.425);
    }
    .reverse {
        transform: scaleX(-1);
    }
</style>