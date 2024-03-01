<template>
    <div class="edit_post__div">
        <h3>Редактировать пост</h3>
        <label for="edit_post_title">Изменить заголовок</label>
        <input v-model="newPostTitle" type="text" name="" id="edit_post_title">
        <label for="edit_post_author">Изменить имя автора</label>
        <select v-model="newPostAuthorId" name="" id="edit_post_author">
                    <option v-for="author in this.users" :key="author.id" :value="author.id"> {{ author.name }}</option>
            </select>
        <label for="edit_post_text">Изменить текст</label>
        <textarea class="edit_post__textarea" v-model="newPostText" type="text" name="" id="edit_post_text" rows="5"></textarea>
        <div class="edit_post__div__buttons">
            <button @click="saveChanges">Сохранить изменения</button>
            <button @click="$emit('close')">Отменить изменения</button>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'EditPost',
        props: {
            postTitle: String,
            postAuthorId: Number,
            postAuthor: String,
            postText: String,
            postId: Number,
            users: Array
        },
        emits: ['changePost', 'close'],
        data() {
            return {
                newPostTitle: this.postTitle,
                newPostAuthorId: this.postAuthorId,
                newPostText: this.postText,
                postObject: {}
            }
        },
        methods: {
            saveChanges() {
                if(this.newPostTitle !== '' && this.newPostText !== '' && this.newPostAuthorId !== '') {
                    fetch(`https://jsonplaceholder.typicode.com/posts/${this.postId}`, {
                    method: 'PUT',
                    body: JSON.stringify({
                        id: this.postId,
                        title: this.newPostTitle,
                        body: this.newPostText,
                        userId: this.newPostAuthorId,
                    }),
                    headers: {
                        'Content-type': 'application/json; charset=UTF-8',
                    },
                    })
                    .then((response) => response.json())
                    .then(alert('Изменения сохранены'))
                    .catch(error => alert('Не удалось сохранить изменения', error))
                    .finally(() => {
                        this.$emit('changePost', this.newPostObject);
                        this.$emit('close')})
                }
            },
        
        },
        computed: {
            newPostObject() {
                return {
                    "userId": this.newPostAuthorId,
                    "id": this.postId,
                    "title": this.newPostTitle,
                    "body": this.newPostText
                }
            }
    }
    }
</script>

<style lang="scss">

.edit_post__div {
    display: flex;
    flex-direction: column;
    gap: 12px;
    justify-content: center;
    align-items: flex-start;
    border: 1px solid #2c3e50;
    padding: 16px;

    &__buttons {
        width: 100%;
        display: flex;
        gap: 20px;
        justify-content: center;
        align-items: center;

        & button {
            border: none;
            border-radius: 4px;
            padding: 4px 8px;

            &:hover {
                background-color: #cccccc;
            }
        }
    }
}

.edit_post__textarea {
    width: 100%;
    font-family: Avenir, Helvetica, Arial, sans-serif;
}

input {
    width: calc(100% - 32px);
}
</style>