<script>
    let tema = 'dark'
    let className = 'bi bi-sun-fill'
    function toggle() {
        if (tema === 'dark') {
            tema = 'light'
            className = 'bi bi-moon-fill'
            
        }
        else {
            tema = 'dark'
            className = 'bi bi-sun-fill'
        }
        console.log(tema);
        document.body.className = tema;
    }
</script>
<main>
    <div>
        <!-- svelte-ignore a11y-click-events-have-key-events -->
        <!-- svelte-ignore a11y-no-static-element-interactions -->
        <i class={className} on:click={toggle}></i>
    </div>
</main>

<style>
    i {
        color: white;
        font-size: 27px;
        float: right;
        margin-top: 2vh;
        display: block;
        margin-right: 4%;
    }
</style>