<script>
    export let optionState = 1;
    export let animationStep = "slide-top-end";
    export let options = []

</script>
<style>
    .caroussel {
        height: 100%;
        background-color: rgba(101, 97, 255, 1);
        border: 2px solid darkgray;
        display: flex;
        justify-content: center;
        align-items: center;
        position: relative;
        overflow: hidden;
    }

    .caroussel-item {
        font-size: 80px;
        color: white;
        position: absolute;
        top: 115px;
        text-shadow: 6px 6px black;
    }

    .slide-top-1 {
            animation: slide-top .1s cubic-bezier(0.600, -0.280, 0.735, 0.045) .1s infinite normal both;
    }

    .slide-top-2 {
            animation: slide-top .4s cubic-bezier(0.600, -0.280, 0.735, 0.045) .1s infinite normal both;
    }

    .slide-top-3 {
            animation: slide-top .8s cubic-bezier(0.600, -0.280, 0.735, 0.045) .1s infinite normal both;
    }


    .slide-top-end {
            animation: slide-top-end 1s cubic-bezier(0.600, -0.280, 0.735, 0.045) .4s 1 normal both;
    }

    @keyframes slide-top-end {
            0% {
                    transform: translateY(-120px);
            }
            50% {
                    transform: translateY(25px);
            }

    }

    @keyframes slide-top {
            0% {
                    transform: translateY(-120px);
            }
            50% {
                    transform: translateY(25px);
            }
            100% {
                    transform: translateY(340px);
            }
    }
</style>

<section class="caroussel">
        <div class={`caroussel-item ${animationStep}`}>{options[optionState].data}</div>
</section>