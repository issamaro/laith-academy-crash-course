<script lang="ts">
    export let answer: string;
    export let option: {id: number, label: string, text: string};
    const handleOption = () => {
        option.text = option.label === answer ? "good answer boy!" : "loser";
    };
</script>
<button class="bg-gray-200 rounded w-[49%] text-center p-2 mb-4 py-5" on:click={handleOption}>{option.text}</button>