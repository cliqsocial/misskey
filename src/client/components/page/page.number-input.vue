<template>
<div>
	<mk-input class="kudkigyw" v-model="v" type="number">{{ script.interpolate(value.text) }}</mk-input>
</div>
</template>

<script lang="ts">
import Vue from 'vue';
import MkInput from '../ui/input.vue';

export default Vue.extend({
	components: {
		MkInput
	},
	props: {
		value: {
			required: true
		},
		script: {
			required: true
		}
	},
	data() {
		return {
			v: this.value.default,
		};
	},
	watch: {
		v() {
			this.script.aoiScript.updatePageVar(this.value.name, this.v);
			this.script.eval();
		}
	}
});
</script>

<style lang="scss" scoped>
.kudkigyw {
	display: inline-block;
	min-width: 300px;
	max-width: 450px;
	margin: 8px 0;
}
</style>
