<template>
	<div class="post_input">
		<label for="post_input">Post body</label>
		<textarea
			name="fbody"
			id="post_input"
			placeholder="textarea"
			required
			v-model="postBody"
		></textarea>
	</div>
	<input type="submit" id="submit_button" @click="updatePost" value="Update" />
</template>

<script>
export default {
	name: "UpdatePostData",
	data: function () {
		return {
			postBody: "Loading...",
			postCreated: new Date(),
		};
	},
	props: {
		id: String,
	},
	methods: {
		updatePost: function () {
			fetch(`http://localhost:3000/post/${this.id}`, {
				headers: {
					"Content-Type": "application/json",
				},
				method: "PUT",
				credentials: "include",
				body: JSON.stringify({
					postBody: this.postBody,
				}),
			}).then(() => location.assign("/"));
		},
	},
	mounted() {
		fetch(`http://localhost:3000/post/${this.id}`, {
			credentials: "include",
		})
			.then((response) => response.json())
			.then((data) => {
				this.postBody = data.body;
				// this.postCreated = data.created_at;
			})
			.catch((err) => console.log(err.message));
	},
};
</script>
