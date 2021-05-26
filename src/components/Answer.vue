<template>
	<b-row>
		<b-col
			class="my-2"
			cols="6"
			v-for="(answer, index) in phase.answers"
			:key="index"
		>
			<b-button
				v-if="!submited"
				class="w-100 border-secondary"
				:variant="phase.userAnswer === index ? 'primary' : 'light'"
				@click="phase.userAnswer = index"
			>
				{{ answer }}
			</b-button>
			<b-button
				v-else
				class="w-100 border-secondary"
				:class="{
					'btn-light':
						index !== phase.correctAnswer &&
						index !== phase.userAnswer,
					'btn-danger':
						index === phase.userAnswer &&
						phase.userAnswer !== phase.correctAnswer,
					'btn-success': index === phase.correctAnswer,
				}"
			>
				{{ answer }}
			</b-button>
		</b-col>
	</b-row>
</template>

<script>
export default {
	props: ["phase", "submited"],
};
</script>

<style></style>
