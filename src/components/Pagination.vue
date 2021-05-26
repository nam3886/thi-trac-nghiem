<template>
	<b-row class="justify-content-center mt-2">
		<b-col class="text-center">
			<b-button
				v-for="(phase, index) in phases"
				:key="index"
				class="mx-1"
				:variant="current === index ? 'primary' : 'outline-primary'"
				@click="changePagination(index)"
				:disabled="current === index"
			>
				{{ index + 1 }}
			</b-button>
		</b-col>
	</b-row>
</template>

<script>
export default {
	props: ["phases", "current", "changePagination"],
};
</script>

<style></style>
