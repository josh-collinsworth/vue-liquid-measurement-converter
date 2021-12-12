<template>
  <div id="lm">
		<div class="card">
			<div class="flex-group container">
				<input v-model="absoluteUnit" type="number">

				<select v-model="unitOfMeasurement">
					<option 
						v-for="unit in units"
						:value="unit.value"
						:key="unit.value"
					>
						{{ unit.title }}
					</option>
				</select>
			</div>
		</div>

		<div
			v-for="unit in filteredUnits"
			class="card"
			:key="unit.title"
		>
			<div class="flex-group container">
				<span class="number">{{ format(absoluteUnit * unitOfMeasurement / unit.value) }}</span>
				<label for="ml">
					{{ unit.title }}
					<sup v-if="(!isMetric && unit.metric) || (isMetric && ! unit.metric)">*</sup>
				</label>
			</div>
		</div>

		<div class="container card footnote">
			* Rounded; not precise
		</div>
	</div>
</template>

<script>
export default {
  name: 'MeasurementsTable',
  data: () => ({
		units: [
			{
				title: 'TSP',
				value: 0.5
			},
			{
				title: 'ML',
				value: 0.1014420675,
				metric: true,
			},
			{
				title: 'TBSP',
				value: 1.5
			},
			{
				title: 'Oz',
				value: 3
			},
			{
				title: 'Cup',
				value: 24
			},
			{
				title: 'Pint',
				value: 48
			},
			{
				title: 'Quart',
				value: 96
			},
			{
				title: 'Liter',
				value: 101.4420675,
				metric: true,
			},
			{
				title: 'Gallon',
				value: 384
			},
		],
		unitOfMeasurement: 3,
		absoluteUnit: 1,
	}),

	methods: {
		//Does some nice formatting on the number, if it's a decimal, to make it a little more readable and limit it to 10 total characters
		format(num) {
			num = Number(num)

			if (this.isMetric) {
				return parseInt(num) === num ? num : num.toFixed(3)
			}
			return parseInt(num) === num ? num : num.toString().substring(0, 10)
		}
	},

	computed: {
		filteredUnits() {
			return this.units.filter(unit => unit.value != this.unitOfMeasurement)
		},

		isMetric() {
			return this.unitOfMeasurement.toString().includes('4420675')
		},
	}
}
</script>


<style scoped lang="scss">
#lm {
	margin: auto;
	width: 100%;
	padding: 1.5rem;

	span {
		text-align: center;
		font-size: 1.25rem;
		display: flex;
		align-items: center;
		color: var(--lightGray);
		margin-bottom: 0.3em;
		left: 0;
	}

	sup {
		float: right;
		margin-right: -1ch;
		padding-top: .1em;
	}

	.footnote {
		margin-top: 0.75rem;
		font-size: .75rem;
	}

	.card {
		display: grid;
		border-radius: 0.25rem;
		align-items: center;

		&:first-of-type {
			margin-bottom: 2rem;
			background: var(--darkBlue);
			width: 100vw;
			max-width: unset;
			margin: -1.5rem calc(50% - 50vw) 2rem;
			padding: 1.5rem 1.5rem 1.5rem;
			border-radius: 0;

			input {
				font-size: 1.75em;
				padding: 0;
				height: 1em;
				width: calc(100% - 1rem);
				color: var(--yellow);
			}

			.flex-group {
				padding-bottom: 0;
				border-bottom: 0;
				position: relative;
				margin: auto;

				&::after {
					content: '';
					width: 1rem;
					height: 1rem;
					background: var(--darkBlue);	
					position: absolute;
					left: calc(50% - 0.5rem);
					bottom: calc(-2rem + 1px);
					transform: rotate(135deg);
					clip-path: polygon(0 0, 100% 100%, 100% 0%);
				}
			}
		}

		h2 {
			font-size: 2rem;
			font-weight: bold;
			text-align: center;
			margin: 0 0 1em;
		}

		select,
		input {
			font-size: 1rem;
			background: #f4f4f4;
			color: inherit;
		}

		select {
			padding: 0.25rem 0.5rem;
			border-radius: .25rem;
			border: 1px solid currentColor;
			color: var(--darkBlue);
			font-weight: 600;

			&:focus {
				outline: 2px solid var(--yellow);
			}
		}

		.flex-group {
			display: grid;
			align-items: baseline;
			justify-content: space-between;
			align-items: center;
			grid-template-columns: 1fr max-content;
			grid-template-rows: 1fr;
			border-bottom: 1px solid var(--lightGray);

			label {
				text-align: right;
				font-size: 1.25rem;
				position: relative;
			}
		}

		.number,
		input {
			font-family: "Martel", serif;
			border: none;
			text-align: left;
			display: inline-block;
			font-size: 1.25rem;
			background: transparent;
			width: 60vw;
			box-shadow: none;
			color: inherit;

			@media (min-width: 440px) {
				width: auto;
			}

			&:focus + label {
				color: var(--yellow);
			}
		}

		.number {
			margin: .25rem 0;
		}
	}
}
</style>