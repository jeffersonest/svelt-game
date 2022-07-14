<script>
    import CardCaroussel from "../../components/card-caroussel.svelte"

    let audio;
    let x = 1;
    let rankDisplay, playersDisplay = 'none';
    let music = false;
    let winners = [];
    let players = [];
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


    function showWinners() {
        rankDisplay = rankDisplay === 'flex' ? 'none' : 'flex';
        playersDisplay = 'none';
        btnClickSound();
    }

    function playSound() {
        if(music === false){
            btnClickSound();
            audio = new Audio("./kawai-kitsune-kevin-macleod-main.mp3");
            audio.play();
            music = true;
        } else {
            audio.pause();
            music = false;
        }



    }

    function showPlayers() {
        playersDisplay = playersDisplay === 'flex' ? 'none' : 'flex';
        rankDisplay = 'none';
        btnClickSound();
    }

    function random(min, max) {
        return Math.floor(Math.random() * (max - min)) + min
    }

    function btnClickSound() {
        const audio = new Audio("./button-30.wav");
        audio.play();
    }

    function addWinner(data) {
        winners = [...winners, data]
    }

    function startGame() {
        startButtonAvaiable = true;
        btnClickSound();
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
        background-color: #f9b660;
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
        padding-top: 0;
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

    .start-btn:disabled {
        background: #b96565;
    }

    .menu {
        display: flex;
        height: 70px;
        align-items: center;
        justify-content: flex-end;
    }

    .winners-btn, .players-btn, .music-btn {
        height: 30px;
        cursor: pointer;
        border: none;
        padding: 5px 10px;
        background: #2eae00;
        border-radius: 40px;
        border-top: 1px solid #FFF;
        box-shadow: 5px 5px black;
        transition: box-shadow 0.1s, top 0.1s;
        position: relative;
        color: white;
        font-weight: bolder;
        margin-left: 15px;
    }

    .menu > button:active {
        top: 4px;
        box-shadow: 1px 1px black;
    }

    .rank, .players {
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
        margin: 0 auto;
    }

    .rank > span > h1 {
        text-align: center;
    }

    .players > span > h1 {
        text-align: center;
    }

    .rank-item, .players-item {
        padding-top: 10px;
    }

    .rank-close, .players-close {
        position: absolute;
        right: 15px;
        top: 10px;
        color: red;
        cursor: pointer;
        font-weight: bolder;
        padding: 5px;
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
        <div class="menu">
            <button class="music-btn" on:click={playSound}>Music 🔊</button>
            <button class="players-btn" on:click={showPlayers}>Players</button>
            <button class="winners-btn" on:click={showWinners}>winners</button>
        </div>
        <div class="machine-lever">
            <button class="start-btn" disabled={startButtonAvaiable} on:click={startGame}>PLAY</button>
        </div>
    </div>
    <div class="rank" style="display: {rankDisplay}">
        <span class="rank-close" on:click={showWinners}>X</span>
        <span>
            <h1>Winners</h1>
        </span>
        {#each winners as winner, i}
            <span class="rank-item">{i + 1} - {winner}</span>
        {/each}
    </div>
    <div class="players" style="display: {playersDisplay}">
        <span class="players-close" on:click={showPlayers}>X</span>
        <span>
            <h1>Players</h1>
        </span>
        {#each players as player, i}
            <span class="players-item">{i + 1} - {player}</span>
        {/each}
    </div>
</section>
