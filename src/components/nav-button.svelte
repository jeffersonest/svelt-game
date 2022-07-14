<script>
    const { link, text } = $$props
</script>
<style>
    .text-decorated {
        padding: 5px 10px;
        margin: 0 15px;
        background-color: #6561ff;
    }
    .text-decorated >  a {
        text-decoration: none;
        color: white;
    }
</style>
<span class="text-decorated">
    <a href={link}>{text}</a>
</span>