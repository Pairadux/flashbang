<script lang="ts">
    let isActive = false;
    let interval: number | null = null;

    function on_key_down(event: KeyboardEvent) {
        if (event.key === " " && interval === null) {
            event.preventDefault();
            interval = window.setInterval(() => {
                isActive = !isActive;
            }, 100); // toggle interval
        }
    }

    function on_key_up(event: KeyboardEvent) {
        if (event.key === " ") {
            event.preventDefault();
            if (interval !== null) {
                clearInterval(interval);
                interval = null;
            }
        }
    }
</script>

<svelte:window on:keydown={on_key_down} on:keyup={on_key_up} />
<div class="{isActive ? 'light' : 'dark'}">
    <p class="{isActive ? 'light' : 'dark'}">Press &lt;Space&gt;</p>
</div>

<style>

div {
    height: 100vh;
    width: 100vw;
    position: relative;
}

.light {
    background-color: white;
    color: black;
}

.dark {
    background-color: black;
    color: white;
}
p {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-family: sans-serif;
    font-size: 3rem;
    font-weight: 600;
}
</style>
