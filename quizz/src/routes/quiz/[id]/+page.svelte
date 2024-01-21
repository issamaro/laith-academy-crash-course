<script lang="ts">
    import QuestionText from "./components/QuestionText.svelte";
    import QuestionOption from "./components/QuestionOption.svelte";
    import QuestionButton from "./components/QuestionButton.svelte";
    import { answers, type Answer } from "../../../store";

    export let data: any;

    let selectedOption: null | string = null;
    let currentQuestionIndex: number = 0;
    let answersValue: Answer[];
    let showCorrectAnswer: boolean = false;

    const handleChangeOption = (label: string) => {
        if (showCorrectAnswer) return;
        selectedOption = label;
    };

    const handleSubmit = () => {
        if (!selectedOption) return;
        showCorrectAnswer = true;
        answers.update((currentState) => {
            const updatedAnswerState = currentState;
            updatedAnswerState[currentQuestionIndex].isCorrect =
                selectedOption === question.answer;
            return updatedAnswerState;
        });
    };

    answers.subscribe((value) => {
        answersValue = value;
    });
    $: question = data.questions[currentQuestionIndex];
</script>

<div class="w-full">
    <QuestionText text={question.question} />
    <div class="flex justify-between flex-wrap cursor-pointer">
        {#each question.options as option (option.id)}
            <QuestionOption
                {option}
                {selectedOption}
                {handleChangeOption}
                {showCorrectAnswer}
                answer={question.answer}
            />
        {/each}
    </div>
    <QuestionButton {handleSubmit} />
</div>
