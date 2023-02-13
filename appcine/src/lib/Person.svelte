<script>
    let person_name = null;
    let person = null;
    let message = null;
    async function getPerson() {
        const res = await fetch(
            `http://localhost:8000/artist/name/${person_name}`
        );
        const data = await res.json();
        if (res.ok) {
            person = data;
            message = null;        
        } else {
            person = null;
            message = `ID ${person_name} ${res.statusText}`;
        }
    }
    </script>
    
    <input bind:value={person_name} type="text" placeholder="person name">
    <button on:click={getPerson}>
    find
    </button>
    
    <div class="table">
        {#if person !== null}
            <img
                src="https://image.tmdb.org/t/p/w185{person.image}"
                alt="imagem do artista"
                width="100"
                height="100"
            />
            <p>ID: {person.id}</p>
            <p>Name: {person.name}</p>
            <p>Popularity: {person.popularity}</p>
            <p class='desc'>{person.biography}</p>
        {:else if message !== null}
            <p class='error'>{message}</p>
        {/if}
    </div>
    
    <style>
    .error{
        color: #e35a5a;
    }
    .table{
        display: grid;
        grid-template-columns: 1fr 1fr 1fr 1fr;
        border: 1px solid #ccc;
        padding: 10px;
    }
    .table .desc{
        color: #646cff;
        grid-column: 1/4;
    }
    </style>