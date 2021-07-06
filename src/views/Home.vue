<template>
	<div class="home">
		<div class="featured-card">
			<router-link to="/movie/tt0409591">
				<img
					src="https://m.media-amazon.com/images/M/MV5BMTE5NzIwMGUtYTE1MS00MDUxLTgyZjctOWVkZDAxM2M4ZWQ4XkEyXkFqcGdeQXVyNjc2NjA5MTU@._V1_SX300.jpg"
					alt="Naruto Poster"
					class="featured-image"
				/>
				<div class="detail">
					<h3>Naruto</h3>
					<p>
						Donec rutrum congue leo eget malesuada. Donec rutrum congue leo eget
						malesuada. Cras ultricies ligula sed magna dictum porta.
					</p>
				</div>
			</router-link>
		</div>
		<form @submit.prevent="searchMovies()" class="search-box">
			<input
				type="text"
				placeholder="What are you looking for?"
				v-model="search"
			/>
			<input type="submit" value="Search" />
		</form>
		<div class="movie-list">
			<div class="movie" v-for="movie in movies" :key="movie.imdbID">
				<router-link :to="'/movie/' + movie.imdbID" class="movie-link">
					<div class="product-image">
						<img :src="movie.Poster" alt="Movie Poster" />
						<div class="type">{{ movie.Type }}</div>
					</div>
					<div class="detail">
						<p class="year">{{ movie.Year }}</p>
						<h3>{{ movie.Title }}</h3>
					</div>
				</router-link>
			</div>
		</div>
	</div>
</template>

<script>
	import { ref } from "vue";
	// @ is an alias to /src

	export default {
		name: "Home",
		components: {},
		setup() {
			const search = ref("");
			const movies = ref([]);
			const searchMovies = () => {
				if (search.value != "") {
					// console.log(
					// 	`http://www.omdbapi.com/?apikey=${process.env.VUE_APP_APIKEY}`
					// );
					fetch(
						`http://www.omdbapi.com/?apikey=${process.env.VUE_APP_APIKEY}&s=${search.value}`
					)
						.then((response) => response.json())
						.then((data) => {
							movies.value = data.Search;
							search.value = "";
						});
				}
			};
			return {
				search,
				movies,
				searchMovies,
			};
		},
	};
</script>
