<script lang="ts">
    export let option: { id: number; label: string; text: string };
    export let selectedOption: null | string;
    export let handleChangeOption: (label: string) => void;
    export let showCorrectAnswer: boolean;
    export let answer: string;
</script>

<button
    class={`${selectedOption === option.label ? "bg-yellow-200" : "bg-gray-200"}
    rounded w-[49%] text-center p-2 mb-4 py-5
    ${showCorrectAnswer && (answer === option.label) ? "bg-green-200" : "bg-red-200"}
    `}
    on:click={() => handleChangeOption(option.label)}
    >{option.text}
</button>
