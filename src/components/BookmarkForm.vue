<template>
	<form class="BookmarkForm" @submit.prevent="onSubmitForm">
		<div class="BookmarkForm__content">
			<FormInput
				label="Link"
				type="url"
				v-model="url"
			/>

			<FormInput
				label="Title"
				type="text"
				v-model="title"
			/>

			<FormTextarea
				label="Summary"
				v-model="summary"
			/>

			<FormInput
				label="Tags"
				type="text"
				v-model="tagString"
			/>

			<FormCheckbox
				label="Favorite"
				v-model="isFavorite"
			/>

			<FormCheckbox
				label="To read"
				v-model="isToRead"
			/>

			<FormCheckbox
				label="Archived"
				v-model="isArchived"
			/>
		</div>

		<div class="BookmarkForm__actions">
			<Button class="BookmarkForm__action" type="submit">Save</Button>
			<Button
				v-if="$listeners.cancel"
				class="BookmarkForm__action"
				@click="$emit('cancel')"
			>
				Cancel
			</Button>

			<Button
				v-if="$listeners.delete"
				class="BookmarkForm__action"
				@click="$emit('delete')"
			>
				Delete
			</Button>
		</div>
	</form>
</template>

<script>
	import { DEFAULT_BOOKMARK_PROPERTIES } from './../store';
	import Button from './Button';
	import FormCheckbox from './FormCheckbox';
	import FormInput from './FormInput';
	import FormTextarea from './FormTextarea';

	export default {
		components: {
			Button,
			FormCheckbox,
			FormInput,
			FormTextarea,
		},
		props: {
			bookmark: {
				type: Object,
				default: () => ({ ...DEFAULT_BOOKMARK_PROPERTIES }),
			},
		},
		data: function() {
			return {
				url: this.bookmark.url || DEFAULT_BOOKMARK_PROPERTIES.url,
				title: this.bookmark.title || DEFAULT_BOOKMARK_PROPERTIES.title,
				summary: this.bookmark.summary || DEFAULT_BOOKMARK_PROPERTIES.summary,
				isFavorite: this.bookmark.isFavorite || DEFAULT_BOOKMARK_PROPERTIES.isFavorite,
				isToRead: this.bookmark.isToRead || DEFAULT_BOOKMARK_PROPERTIES.isToRead,
				isArchived: this.bookmark.isArchived || DEFAULT_BOOKMARK_PROPERTIES.isArchived,
				tagString: (this.bookmark.tags || DEFAULT_BOOKMARK_PROPERTIES.tags).join(' '),
			};
		},
		methods: {
			onSubmitForm() {
				this.$emit('submit', {
					url: this.url,
					title: this.title,
					summary: this.summary,
					isToRead: this.isToRead,
					tags: this.tagString.trim().split(' '),
				});
			},
		}
	}
</script>

<style lang="scss">
	.BookmarkForm__content + .BookmarkForm__actions {
		margin-top: 20px;
	}

	.BookmarkForm__actions {
		display: flex;
	}

	.BookmarkForm__action + .BookmarkForm__action {
		margin-left: 10px;
	}
</style>