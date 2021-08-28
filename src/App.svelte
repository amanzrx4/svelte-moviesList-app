<script>
    import MovieInput from './MovieInput.svelte';
    import MovieList from './MovieList.svelte';
    import Search from './search.svelte';

    let movies = localStorage.getItem('movies')
        ? JSON.parse(localStorage.getItem('movies'))
        : [];

    const submitMovie = (movie) => {
        const updatedMovies = [...movies, movie];
        localStorage.setItem('movies', JSON.stringify(updatedMovies));
        movies = updatedMovies;
    };

    const clearSearch = () => {
        movies = localStorage.getItem('movies')
            ? JSON.parse(localStorage.getItem('movies'))
            : [];
    };

    const search = (searchTerm) => {
        const tempMovies = localStorage.getItem('movies')
            ? JSON.parse(localStorage.getItem('movies'))
            : [];
        movies = tempMovies.filter((m) =>
            m.title.toLowerCase().includes(searchTerm.toLowerCase())
        );
    };
</script>

<div class="main">
    <h1>Movie journel</h1>
    <Search
        on:search={(e) => search(e.detail.searchTerm)}
        on:clearSearch={clearSearch}
    />
    <MovieInput on:submitMovie={(e) => submitMovie(e.detail.movie)} />
    <MovieList {movies} />
</div>

<style>
    .main {
        width: 500px;
        max-width: 100%;
        padding: 1em;
        margin: auto;
        text-align: center;
    }

    h1 {
        color: #ff3e00;
        text-transform: uppercase;
        font-size: 4em;
        font-weight: 100;
    }
</style>
