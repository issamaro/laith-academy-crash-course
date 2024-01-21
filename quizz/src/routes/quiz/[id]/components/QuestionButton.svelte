<script lang=ts>
    export let handleSubmit: () => void;
</script>

<div class="text-center">
    <button class="bg-blue-900 text-white font-bold p-4 rounded px-16" on:click={handleSubmit}>
        Submit
    </button>
</div>