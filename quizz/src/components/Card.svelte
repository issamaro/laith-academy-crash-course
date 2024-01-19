<script lang="ts">
    import {imageKeys} from "../images";
    import {goto} from "$app/navigation";
    interface Quiz {
        id: number;
        name: string;
        imageUrl: keyof typeof imageKeys;
        questions: {
            id: number;
            question: string;
            options: {
                id: number;
                label: string;
                text: string;
            }[];
            answer: string;
        }[];
    };
    export let quiz: Quiz;
</script>

<button
class="quizz-card shadow w-[260px] rounded overflow-hidden cursor-pointer m-3"
on:click={() => goto(`/quiz/${quiz.id}`)} >
    <img alt="hello" class="h-44" src={imageKeys[quiz.imageUrl]}>
    <div class="flex items-center justify-between py-3 px-2">
        <h1 class="font-bold">{quiz.name}</h1>
        <p>{quiz.questions.length} question{`${quiz.questions.length > 1 ? "s" : ""}`}</p>
    </div>
</button>