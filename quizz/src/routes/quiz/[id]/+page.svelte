<script lang="ts">
    import QuestionText from "./components/QuestionText.svelte";
    import QuestionOption from "./components/QuestionOption.svelte";

    export let data: any;

    let currentQuestionIndex: number = 0;
    $: question = data.questions[currentQuestionIndex]
</script>

<div class="w-full">
    {currentQuestionIndex}
    {question.question}
    <button on:click={() => currentQuestionIndex += 1}>Click me</button>
    <QuestionText text={question.question}/>
    <div class="flex justify-between flex-wrap cursor-pointer">
        {#each question.options as option (question.options.id)}
        <QuestionOption option={option} answer={question.answer}/>
        {/each}
    </div>
</div>