<script>
    import materialStore from './material-store.js';
    export let id;
    export let name = "";
    export let price = 5;

    $: mode = id ? "edit" : "add";
    $: canSubmit = price >= 0 && name !== "";

    function submit() {
        if(!canSubmit){
            return;
        }

        if(mode == "add"){
            materialStore.add(name, price);
        }

        id = undefined;
        name = "";
        price = 5;
    }

    function cancel() {
        id = undefined;
        name = "";
        price = 5;
    }
</script>

<style>
    button{
        margin-left: 20px;
    }

    button:disabled{
        cursor: not-allowed;
    }
</style>

<form on:submit|preventDefault={submit}>
    <fieldset>
        <label for="">
            Material
        </label>
        <input bind:value={name} placeholder="Wood, Glue, Etc" type="text" id="nameField">
        <label for="">
            Price
        </label>
        <input bind:value={price} placeholder="Price" type="number" id="priceField" min="0" step="any">

        <button
            disabled={!canSubmit}
            class="float-right"
            type="submit">
            {mode}
        </button>
        {#if mode == 'edit'}
            <button
                on:click={cancel}
                class="float-right"
                type="button">
                Cancel
            </button>
        {/if}
    </fieldset>
</form>