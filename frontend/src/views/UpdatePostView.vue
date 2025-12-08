<script>
    export default {
        name: "UpdatePostData",
        // data: () => {
        //     return {
        //         // postDesc: fetch("http://localhost:3000/post/", {
        //         //     method
        //         // }),
        //     }
        // },
        props: {
            // id: String
        },
        methods: {
            updatePost: function() {
                fetch("http://localhost:3000/post", {
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    method: "PUT",
                    credentials: "include",
                    body: JSON.stringify(
                        {
                            postBody: this.postDesc
                        }
                    )
                }).then(() => location.assign("/"))
            }
        }
    }
</script>

<template>
        <div class="post_input">
            <!-- <label for="post_input">Post body</label>
            <textarea
                name="fbody"
                id="post_input"
                placeholder="textarea"
                required
                v-model="postDesc"
            ></textarea> -->
        </div>
        <!-- <input type="submit" id="submit_button" @click="updatePostPost" value="Add"/> -->
</template>