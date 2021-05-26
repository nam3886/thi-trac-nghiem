<template>
	<b-row>
		<b-col>
			<b-alert
				show
				class="w-100"
				:variant="
					!submited
						? 'primary'
						: phase.userAnswer === phase.correctAnswer
						? 'success'
						: 'danger'
				"
			>
				<span class="question">Question {{ current + 1 }}:</span>
				{{ phase.question }} ({{ phase.score }}đ)
			</b-alert>
		</b-col>
	</b-row>
</template>

<script>
export default {
	props: ["phase", "submited", "current"],
};
</script>

<style scoped>
.question {
	margin-right: 1rem;
	text-decoration: underline;
}
</style>
