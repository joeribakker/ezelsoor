<template>
	<form class="BookmarkUrlForm" @submit.prevent="handleSubmitBookmark({ url: url })">
		<FormInput
			class="BookmarkUrlForm__input"
			ref="input"
			placeholder="Enter new bookmark link"
			type="url"
			required
			v-model:value="url"
		/>

		<Button
			class="BookmarkUrlForm__action"
			type="submit"
			variant="text"
		>
			Add
		</Button>

		<Button
			class="BookmarkUrlForm__action"
			variant="text"
			@click="isBookmarkDetailsDialogOpen = true"
		>
			Details...
		</Button>

		<Modal v-if="isBookmarkDetailsDialogOpen">
			<BookmarkForm
				:bookmark="{ url: url }"
				@submit="handleSubmitBookmark"
				@cancel="isBookmarkDetailsDialogOpen = false"
			/>
		</Modal>
	</form>
</template>

<script>
	import BookmarkForm from './BookmarkForm.vue';
	import Button from './Button.vue';
	import FormInput from './FormInput.vue';
	import Modal from './Modal.vue';

	export default {
		components: {
			BookmarkForm,
			Button,
			FormInput,
			Modal,
		},
		emits: ['submit'],
		data: function() {
			return {
				url: '',
				isBookmarkDetailsDialogOpen: false,
			};
		},
		methods: {
			handleSubmitBookmark(bookmark) {
				this.$emit('submit', bookmark);
				this.isBookmarkDetailsDialogOpen = false;
				this.resetForm();
				this.$refs.input.focus();
			},
			resetForm() {
				this.url = '';
			},
		},
	};
</script>

<style lang="scss">
	.BookmarkUrlForm {
		display: flex;
		align-items: center;
	}

	.BookmarkUrlForm__input {
		flex-grow: 1;
	}

	.BookmarkUrlForm__action {
		margin-left: 20px;
	}
</style>
