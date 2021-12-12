<template>
  <div id="lm">
		<div class="card">
			<div class="flex-group container">
				<div>
					<button @click="increment" title="Plus one">+</button>
					<input v-model="absoluteUnit" type="number" />
					<button @click="decrement" title="Minus one">-</button>
				</div>

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
				<span
					class="number"
					v-html="format(absoluteUnit * unitOfMeasurement / unit.value)"
				/>
				<span class="label">
					{{ unit.title }}
					<sup
						class="asterisk"
						v-if="(!isMetric && unit.metric) || (isMetric && ! unit.metric)"
					>*</sup>
				</span>
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
		fractions: [128, 64, 32, 16, 10, 8, 6, 5, 4, 3, 2],
		unitOfMeasurement: 3,
		absoluteUnit: 2,
	}),

	methods: {
		//Does some nice formatting on the number, if it's a decimal, to make it a little more readable and limit it to 10 total characters
		format(num) {
			num = Number(num)

			const formattedNum = parseInt(num) === num ? num : num.toString().substring(0, 10)

			if (this.isConvertibleToFraction(formattedNum)) {
				return this.convertToFraction(formattedNum)
			} else if (this.isMetric) {
				return parseInt(num) === num ? num : num.toFixed(3)
			}

			return formattedNum
		},

		increment() {
			this.absoluteUnit += 1
		},

		decrement() {
			this.absoluteUnit -= 1
		},

		isConvertibleToFraction(number) {
			// Need special cases to handle imperfect division
			if ([3, 6].includes(Math.round(1 / number))) {
				return true
			}
	
			if (this.fractions.includes(1 / number)) {
				return true
			}

			return false
		},

		convertToFraction(number) {
			let whichFraction

			this.fractions.forEach((fraction) => {
				if (Math.round(1 / number) === fraction) {
					whichFraction = fraction 
				} 
			})

			if (whichFraction) {
				return `<span class="fraction"><sup>1</sup>/<sub>${whichFraction}</sub></span>`
			}
			
			return null
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


<style lang="scss">
#lm {
	margin: auto;
	width: 100%;
	padding: 1.5rem;

	span {
		text-align: center;
		font-size: 1.25rem;
		display: flex;
		align-items: center;
		color: var(--accent);
		margin-bottom: 0.3em;
		left: 0;
	}

	.fraction {
		display: inline-block;
		position: relative;
		top: -0.5rem;
		color: inherit;
	}

	.asterisk {
		position: absolute;
		margin-right: -1ch;
		top: 0;
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
			background: var(--accent);
			width: 100vw;
			max-width: unset;
			margin: -1.5rem calc(50% - 50vw) 1rem;
			padding: 1rem 1.5rem 1rem;
			border-radius: 0;

			input {
				font-size: 1.75em;
				padding: 0;
				height: auto;
				width: 100%;
				color: var(--dark);
			}

			.flex-group {
				padding-bottom: 0;
				border-bottom: 0;
				position: relative;
				margin: auto;
				align-items: center;

				&::after {
					content: '';
					width: 1rem;
					height: 1rem;
					background: var(--accent);	
					position: absolute;
					left: calc(50% - 0.5rem);
					bottom: calc(-1.5rem + 1px);
					transform: rotate(135deg);
					clip-path: polygon(0 0, 100% 100%, 100% 0%);
				}
			}
		}

		select,
		input {
			font-size: 1rem;
			background: var(--background);
			color: inherit;
		}

		select {
			padding: 0.25rem 0.5rem;
			border-radius: .25rem;
			border: 1px solid currentColor;
			color: var(--dark);
			font-weight: 600;
		}

		button {
			font-weight: bold;
			font-size: 1.5rem;
			line-height: 1;
			color: var(--bright);
			background: transparent;
			border: 0;
			position: relative;
			left: -0.25rem;
		}

		.flex-group {
			display: flex;
			justify-content: space-between;
			align-items: flex-end;
			grid-template-columns: 1fr max-content;
			grid-template-rows: 1fr;
			padding-bottom: 0.5rem;
			border-bottom: 1px solid var(--accent);

			.label {
				text-align: right;
				font-size: 1.25rem;
				position: relative;
				line-height: 1;
				display: inline-block;
				color: inherit;
				margin: 0;
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
				color: var(--bright);
			}
		}

		.number {
			margin: 0.75rem 0 -1.25rem;
			height: 2.2em;
			overflow: visible;
		}
	}
}
</style>