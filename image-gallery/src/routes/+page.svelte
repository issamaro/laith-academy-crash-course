<script lang="ts">
    import axios from "axios";
    import {onMount} from "svelte";
    import {fade, fly} from "svelte/transition"
    let term = "";
    let photos: {
        id: string;
        alt_description: string;
        urls: {regular: string};
    }[] = [];
    const fetchData = async () => {
        const response = await axios.get(`https://api.unsplash.com/search/photos?page=1&query=${term || "building"}&client_id=t6IgLkpPQ_CIjIkOyQa6kpW_9ZwRDBGwsSovERefN60`);
        photos = response.data.results;
    };

    onMount(() => {
        fetchData();
    });

    const handleSearch = async () => {
        if (!term) return;
        await fetchData();
        term = "";
    };
</script>


<div class="container">
    <div class="header">
        <h1>Image Gallery</h1>
        <div class="input-container">
            <input class ="input" type="text" bind:value={term}/>
            <button class="button" on:click={handleSearch}>Search</button>
        </div>
    </div>
    <div class="photos">
        {#each photos as photo, i (photo.id)}
        <img alt={photo.alt_description} class="image" in:fly={{y: 700, duration: 1200, delay: i * 26}} out:fade={{duration: i * 20}} src={photo.urls.regular} >
        {/each}
    </div>
</div>

<style>
    .image {
        width: 400px;
        height: 250px;
        margin: 5px;
    }
    .photos {
        display: flex;
        flex-wrap: wrap;
    }
    .container {
        width: 1230px;
        margin: 0 auto;
    }
    .header {
        text-align: center;
        font-size: 20px;
    }
    .input {
        padding: 10px;
        width: 400px;
        border-radius: 10px;
        outline: none;
        border: 1px solid gray;
        font-size: 20px;
    }
    .button {
        padding: 10px;
        font-size: 20px;
        background-color: rgb(187, 187, 187);
        border-radius: 10px;
        border: none;
        color: white;
    }
    .input-container {
        margin-bottom: 40px;
    }
</style>
