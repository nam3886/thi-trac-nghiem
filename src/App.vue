<template>
	<div id="app">
		<b-container class="my-5">
			<question
				:phase="phases[current]"
				:submited="submited"
				:current="current"
			/>
			<answer :phase="phases[current]" :submited="submited" />
			<b-row>
				<b-col class="text-center">
					<b-button
						class="mx-1"
						variant="primary"
						:disabled="current === 0"
						@click="current--"
					>
						&larr;
					</b-button>
					<b-button
						class="mx-1"
						variant="primary"
						:disabled="current === phases.length - 1"
						@click="current++"
					>
						&rarr;
					</b-button>
				</b-col>
			</b-row>
			<b-row class="mt-2" v-if="!submited">
				<b-col class="text-center">
					<b-button
						class="mx-1"
						variant="danger"
						@click="
							submited = true;
							current = 0;
						"
					>
						Submit
					</b-button>
				</b-col>
			</b-row>
			<b-row class="mt-4" v-if="submited">
				<b-col>
					<b-alert show class="w-100 d-flex justify-content-center">
						<div>total score: {{ totalScore() }}</div>
					</b-alert>
					<b-alert show class="w-100 d-flex justify-content-center">
						<div>
							correct: {{ countCorrect() }}/{{ phases.length }}
						</div>
					</b-alert>
				</b-col>
			</b-row>
			<pagination
				:phases="phases"
				:current="current"
				:changePagination="changePagination"
			/>
		</b-container>
	</div>
</template>

<script>
import Question from "./components/Question.vue";
import Answer from "./components/Answer.vue";
import Pagination from "./components/Pagination.vue";
export default {
	data() {
		return {
			submited: false,
			current: 0,
			phases: [
				{
					question: "1 + 1 = ?",
					answers: [1, 2, 3, 4],
					userAnswer: null,
					correctAnswer: 1,
					score: 0.5,
				},
				{
					question: "Viet Nam co bao nhieu tinh thanh?",
					answers: [64, 34, 54, 74],
					userAnswer: null,
					correctAnswer: 0,
					score: 2,
				},
				{
					question: "Vuejs version moi nhat la?",
					answers: [1, 2, 3, 4],
					userAnswer: null,
					correctAnswer: 2,
					score: 5,
				},
			],
		};
	},
	methods: {
		totalScore() {
			return this.phases.reduce(function(total, phase) {
				return phase.userAnswer === phase.correctAnswer
					? total + phase.score
					: total;
			}, 0);
		},
		countCorrect() {
			return this.phases.reduce(function(total, phase) {
				return phase.userAnswer === phase.correctAnswer
					? ++total
					: total;
			}, 0);
		},
		changePagination(index) {
			this.current = index;
		},
	},
	components: {
		Question,
		Answer,
		Pagination,
	},
};
</script>

<style></style>
