<script>
    export let option = "easy"

    function btnClickSound() {
        const audio = new Audio("./button-30.wav");
        audio.play();
    }

    function selectOption(e) {
        btnClickSound();
        option = e.target.value;
    }

</script>
<style>

    :root {
        --background-gradient: linear-gradient(30deg, #f39c12 30%, #f1c40f);
        --gray: #34495e;
        --darkgray: #2c3e50;
    }



    select {
        /* Reset Select */
        appearance: none;
        outline: 0;
        border: 0;
        box-shadow: none;
        /* Personalize */
        flex: 1;
        padding: 0 1em;
        color: #fff;
        background-color: var(--darkgray);
        background-image: none;
        cursor: pointer;
    }
    /* Remove IE arrow */
    select::-ms-expand {
        display: none;
    }
    /* Custom Select wrapper */
    .select {
        margin-top: 5px;
        position: relative;
        display: flex;
        width: 140px;
        height: 30px;
        border-radius: 15px;
        overflow: hidden;
        box-shadow: 5px 3px black;
    }
    /* Arrow */
    .select::after {
        content: '\25BC';
        position: absolute;
        top: 0;
        right: 0;
        padding: 6px;
        background-color: #2eae00;
        transition: .25s all ease;
        pointer-events: none;
    }
    /* Transition */
    .select:hover::after {
        color: #f39c12;
    }
</style>

<div class="select">
    <select on:change={selectOption} >
        <option value="easy">Easy</option>
        <option value="medium">Medium</option>
        <option value="hard">Hard</option>
    </select>
</div>