<template>
	<div class="tag-container">
		<h4>{{ heading }}</h4>
		<TagComponent
			v-for="tag in getTags()"
			:key="tag.id"
			:tag-name="tag.text"
			:tag-id="tag.id"
			:tag-type="type"
		/>
	</div>
</template>

<script>
	import TagComponent from './TagComponent.vue'

	export default {
		components: {
			TagComponent
		},
		props: {
			type: {
				required: true,
				type: String,
				default: 'type'
			},
			heading: {
				required: true,
				type: String,
				default: 'heading'
			}
		},
		data() {
			return {
				tags: []
			}
		},
		created() {},
		methods: {
			getTags() {
				const key =
					'db' + this.type.charAt(0).toUpperCase() + this.type.slice(1) + 'Tags'

				return this.$store.state[key]
			}
		}
	}
</script>

<style scoped>
	.tag-container > h4 {
		font-size: 1.5rem;
		line-height: 1.5;
		margin-bottom: 1rem;
	}

	.tag-container:not(:last-child) {
		padding-bottom: 2rem;
	}

	@media screen and (max-width: 1024px) {
		.tag-container {
			width: auto;
		}
	}
</style>
