<template>
	<Header />
	<main>
		<router-view />
	</main>
</template>

<script>
	import Header from "@/components/Header.vue";
	// @ is an alias to /src

	export default {
		name: "App",
		components: {
			Header,
		},
	};
</script>
