<template>
<div class="icozogqfvdetwohsdglrbswgrejoxbdj" v-if="hide" @click="hide = false">
	<div>
		<b><fa :icon="faExclamationTriangle"/> {{ $t('sensitive') }}</b>
		<span>{{ $t('clickToShow') }}</span>
	</div>
</div>
<div class="kkjnbbplepmiyuadieoenjgutgcmtsvu" v-else>
	<i><fa :icon="faEyeSlash" @click="hide = true"/></i>
	<a
		:href="video.url"
		rel="nofollow noopener"
		target="_blank"
		:style="imageStyle"
		:title="video.name"
	>
		<fa :icon="faPlayCircle"/>
	</a>
</div>
</template>

<script lang="ts">
import Vue from 'vue';
import { faPlayCircle } from '@fortawesome/free-regular-svg-icons';
import { faExclamationTriangle, faEyeSlash } from '@fortawesome/free-solid-svg-icons';
import i18n from '../i18n';

export default Vue.extend({
	i18n,
	props: {
		video: {
			type: Object,
			required: true
		}
	},
	data() {
		return {
			hide: true,
			faPlayCircle,
			faExclamationTriangle,
			faEyeSlash
		};
	},
	computed: {
		imageStyle(): any {
			return {
				'background-image': `url(${this.video.thumbnailUrl})`
			};
		}
	},
	created() {
		this.hide = this.video.isSensitive && !this.$store.state.device.alwaysShowNsfw;
	},
});
</script>

<style lang="scss" scoped>
.kkjnbbplepmiyuadieoenjgutgcmtsvu {
	position: relative;

	> i {
		display: block;
		position: absolute;
		border-radius: 6px;
		background-color: var(--fg);
		color: var(--accentLighten);
		font-size: 14px;
		opacity: .5;
		padding: 3px 6px;
		text-align: center;
		cursor: pointer;
		top: 12px;
		right: 12px;
	}

	> a {
		display: flex;
		justify-content: center;
		align-items: center;

		font-size: 3.5em;
		overflow: hidden;
		background-position: center;
		background-size: cover;
		width: 100%;
		height: 100%;
	}
}

.icozogqfvdetwohsdglrbswgrejoxbdj {
	display: flex;
	justify-content: center;
	align-items: center;
	background: #111;
	color: #fff;

	> div {
		display: table-cell;
		text-align: center;
		font-size: 12px;

		> b {
			display: block;
		}
	}
}
</style>
