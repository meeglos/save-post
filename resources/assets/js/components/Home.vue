<template>
	<div class="container">
		<div class="row">
			<div class="col-sm-6">
				<div class="form-group">
					<label for="title">Post Title</label>
					<input v-model="newPostTitle" id="title" type="text" class="form-control">
				</div>
				<div class="form-group">
					<label for="description">Post Description</label>
					<textarea v-model="newPostDesc" id="description" rows="1" class="form-control"></textarea>
				</div>
				<button @click="addPost(newPostTitle, newPostDesc)"
					:class="{disabled: (!newPostTitle || !newPostDesc)}"
					class="btn btn-block btn-primary">Submit</button>
			</div>
			<div class="col-sm-6">
				<ul class="list-group">
				  <li class="list-group-item d-flex justify-content-between align-items-center">
				    Cras justo odio
				    <span class="badge badge-default badge-pill">14</span>
				  </li>
				</ul>
			</div>
		</div>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				newPostTitle: "",
				newPostDesc: ""
	  		}
		},

		methods: {
	  		addPost(postName, postDesc) {
				if(!postName || !postDesc)
					return;

				axios.post('/post', {
					title: postName, description: postDesc
				}).then( response => {
			  		if(response.data) {
						this.newPostTitle = this.newPostDesc = "";
			  		}
				})
	  		},
	  	}
	}
</script>
