<template>
	<ul class="TagList" v-if="tags.length">
		<TagItem
			v-for="(tag, index) in tags"
			class="TagList__item"
			:key="index"
			:tag="tag"
		/>
	</ul>
</template>

<script>
	import TagItem from './TagItem';

	export default {
		props: {
			tags: {
				type: Array,
				default: () => [],
			},
		},
		components: {
			TagItem,
		},
	};
</script>

<style lang="scss">
	.TagList {
		display: flex;
		list-style: none;
		flex-wrap: wrap;
	}

	.TagList__item:not(:last-child) {
		margin-right: 10px;
	}
</style>
