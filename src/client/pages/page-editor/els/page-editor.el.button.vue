<template>
<x-container @remove="() => $emit('remove')" :draggable="true">
	<template #header><fa :icon="faBolt"/> {{ $t('_pages.blocks.button') }}</template>

	<section class="xfhsjczc">
		<mk-input v-model="value.text"><span>{{ $t('_pages.blocks._button.text') }}</span></mk-input>
		<mk-switch v-model="value.primary"><span>{{ $t('_pages.blocks._button.colored') }}</span></mk-switch>
		<mk-select v-model="value.action">
			<template #label>{{ $t('_pages.blocks._button.action') }}</template>
			<option value="dialog">{{ $t('_pages.blocks._button._action.dialog') }}</option>
			<option value="resetRandom">{{ $t('_pages.blocks._button._action.resetRandom') }}</option>
			<option value="pushEvent">{{ $t('_pages.blocks._button._action.pushEvent') }}</option>
			<option value="callAiScript">{{ $t('_pages.blocks._button._action.callAiScript') }}</option>
		</mk-select>
		<template v-if="value.action === 'dialog'">
			<mk-input v-model="value.content"><span>{{ $t('_pages.blocks._button._action._dialog.content') }}</span></mk-input>
		</template>
		<template v-else-if="value.action === 'pushEvent'">
			<mk-input v-model="value.event"><span>{{ $t('_pages.blocks._button._action._pushEvent.event') }}</span></mk-input>
			<mk-input v-model="value.message"><span>{{ $t('_pages.blocks._button._action._pushEvent.message') }}</span></mk-input>
			<mk-select v-model="value.var">
				<template #label>{{ $t('_pages.blocks._button._action._pushEvent.variable') }}</template>
				<option :value="null">{{ $t('_pages.blocks._button._action._pushEvent.no-variable') }}</option>
				<option v-for="v in aoiScript.getVarsByType()" :value="v.name">{{ v.name }}</option>
				<optgroup :label="$t('_pages.script.pageVariables')">
					<option v-for="v in aoiScript.getPageVarsByType()" :value="v">{{ v }}</option>
				</optgroup>
				<optgroup :label="$t('_pages.script.enviromentVariables')">
					<option v-for="v in aoiScript.getEnvVarsByType()" :value="v">{{ v }}</option>
				</optgroup>
			</mk-select>
		</template>
		<template v-else-if="value.action === 'callAiScript'">
			<mk-input v-model="value.fn"><span>{{ $t('_pages.blocks._button._action._callAiScript.functionName') }}</span></mk-input>
		</template>
	</section>
</x-container>
</template>

<script lang="ts">
import Vue from 'vue';
import { faBolt } from '@fortawesome/free-solid-svg-icons';
import i18n from '../../../i18n';
import XContainer from '../page-editor.container.vue';
import MkSelect from '../../../components/ui/select.vue';
import MkInput from '../../../components/ui/input.vue';
import MkSwitch from '../../../components/ui/switch.vue';

export default Vue.extend({
	i18n,

	components: {
		XContainer, MkSelect, MkInput, MkSwitch
	},

	props: {
		value: {
			required: true
		},
		aoiScript: {
			required: true,
		},
	},

	data() {
		return {
			faBolt
		};
	},

	created() {
		if (this.value.text == null) Vue.set(this.value, 'text', '');
		if (this.value.action == null) Vue.set(this.value, 'action', 'dialog');
		if (this.value.content == null) Vue.set(this.value, 'content', null);
		if (this.value.event == null) Vue.set(this.value, 'event', null);
		if (this.value.message == null) Vue.set(this.value, 'message', null);
		if (this.value.primary == null) Vue.set(this.value, 'primary', false);
		if (this.value.var == null) Vue.set(this.value, 'var', null);
		if (this.value.fn == null) Vue.set(this.value, 'fn', null);
	},
});
</script>

<style lang="scss" scoped>
.xfhsjczc {
	padding: 0 16px 0 16px;
}
</style>
