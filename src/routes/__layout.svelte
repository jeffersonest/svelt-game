<script>
    import NavButton from '../components/nav-button.svelte'
</script>
<style>
       .main {
              padding: 15px;
       }
</style>
<nav>
       <NavButton link="/" text="Home" />
       <NavButton link="/gacha" text="Gacha" />
</nav>
<div class="main">
       <slot ></slot>
</div>

