<script>
    import CardCaroussel from "../../components/card-caroussel.svelte"

    let x = 1;
    let winner = []
    let animationStep = "slide-top-end";
    let startButtonAvaiable = false;
    let options = [
        {id: "01", data: "🐶"},
        {id: "01", data: "🐸"},
        {id: "01", data: "🦝"},
        {id: "01", data: "🐰"},
        {id: "01", data: "🐭"},
        {id: "01", data: "🐱"},
    ]

    let caroussel01 = random(0, options.length);
    let caroussel02 = random(0, options.length);
    let caroussel03 = random(0, options.length);

    function random(min, max) {
        return Math.floor(Math.random() * (max - min)) + min
    }

    function addWinner(data) {
        console.log(data)
        winner.push(data)
    }

    function startGame() {
        startButtonAvaiable = true;
        const start = setInterval(()=>{
            x++

            if(x <= 5) animationStep = "slide-top-1";
            if(x > 5 && x <= 10) animationStep = "slide-top-2";
            if(x > 10 && x <= 17) animationStep = "slide-top-3";
            if(x > 17 && x <= 20) animationStep = "slide-top-end";

            caroussel01 = random(0,options.length);
            caroussel02 = random(0,options.length);
            caroussel03 = random(0,options.length);

            if(x >= 20) {
                x = 0;
                if(caroussel01 === caroussel02 && caroussel01 === caroussel03) setTimeout(()=>{
                    addWinner(`${options[caroussel01].data} - ${options[caroussel02].data} - ${options[caroussel03].data}`)
                    window.alert("Winner!")
                }, 500)
                startButtonAvaiable=false;
                clearInterval(start)
            }
        }, 500)
    }

</script>
<style>
    .gacha-game {
       display: flex;
        align-items: center;
        justify-content: center;
    }
    .machine {
        width: 600px;
        height: 600px;
        background-color: darkgray;
        border-radius: 10px;
        padding: 20px;
    }
    .machine-screeen {
        background-color: #fff;
        height: 350px;
        border-radius: 10px;
        display: flex;
        justify-content: space-evenly;
    }

    .machine-screeen > div {
        width: 33.33%;
    }

    .machine-lever {
        position: relative;
        width: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        padding-top: 100px;
    }

    .machine-lever > button {
        border: none;
        height: 80px;
        padding: 1em 2em;
        cursor: pointer;
        background: #f22929;
        border-radius: 40px;
        border-top: 1px solid #FFF;
        box-shadow: 5px 5px black;
        transition: box-shadow 0.1s, top 0.1s;
        position: relative;
        color: white;
    }


    .machine-lever > button:active {
        top: 4px;
        box-shadow: 1px 1px black;
    }

    .rank {
        position: absolute;
        padding: 15px;
        background: white;
        border-radius: 10px;
        width: 250px;
        justify-content: flex-start;
        flex-direction: column;
        height: 250px;
        overflow-y: scroll;
        display: none;
    }

    .start-btn:disabled {
        background: #b96565;
    }

</style>
<section class="gacha-game">
    <div class="machine">
        <div class="machine-screeen">
            <div>
                <CardCaroussel bind:options={options} bind:animationStep={animationStep}  bind:optionState={caroussel01} />
            </div>
            <div>
                <CardCaroussel bind:options={options} bind:animationStep={animationStep}  bind:optionState={caroussel02} />
            </div>
            <div>
                <CardCaroussel bind:options={options} bind:animationStep={animationStep}  bind:optionState={caroussel03} />
            </div>
        </div>
        <div class="machine-lever">
            <button class="start-btn" disabled={startButtonAvaiable} on:click={startGame}>PLAY</button>
        </div>
    </div>
    <div class="rank">
        <h1>Winner games:</h1>
        {#each winner as game, i}
            <span class="rank-item">{game}</span>
        {/each}
    </div>
</section>
