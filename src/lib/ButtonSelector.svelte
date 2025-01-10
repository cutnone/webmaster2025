<script lang="ts">
    let {options, selected = $bindable(0)} = $props();

    function select(index: number) {
        selected = index;
    }

</script>

<div class="btns">
    {#each options as option, i}
        <button onclick={()=>select(i)} class:left={i === 0} class:right={i === options.length-1} class:selected={i === selected}>
            {option}
        </button>
    {/each}
</div>

<style lang="scss">
    .btns {
        display: flex;
        flex-grow: 1;
    }

    button {
        border-radius: 0;
        background-color: var(--color-background);
        color: var(--color-accent);
        outline: none;
        border: 2px solid var(--color-accent);
        transition-property: color, background-color, outline-offset;
        padding: calc(.5rem - 2px) .5rem;
        flex-grow: 1;
        cursor: default;
    }

    button:not(.selected) {
        cursor: pointer;
        &:hover {
            background-color: var(--color-accent-light);
        }
    }
    
    .selected {
        background-color: var(--color-accent);
        color: var(--color-background);
    }

    .left {
        border-radius: 1rem 0 0 1rem;
    }

    .right {
        border-radius: 0 1rem 1rem 0;
    }
</style>