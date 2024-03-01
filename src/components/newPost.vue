<template>
     <div class="new_post__div">
        <h2>Добавить новый пост</h2>
        <div class="new_post__div__inputs">
            <label for="new_post_author">Выбрать автора</label>
            <select v-model="newPostAuthor" name="" id="new_post_author">
                    <option value="">Не выбрано</option>
                    <option v-for="author in this.users" :key="author.id" :value="author.id" selected> {{ author.name }}</option>
            </select>
            <label for="new_post_title">Заголовок</label>
            <input v-model="newPostTitle" type="text" name="" id="new_post_title" placeholder="Введите название">
            <label for="new_post_text">Текст</label>
            <textarea class="new_post__div__inputs_text" v-model="newPostText" name="" id="new_post_text" rows="10" placeholder="Введите текст"></textarea>
        </div>
        <div class="new_post__div__buttons">
            <button @click="saveChanges" class="new_post__div__buttons_save">Сохранить пост</button>
            <button @click="$emit('close')" class="new_post__div__buttons_close">Закрыть без сохранения</button>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'newPost',
        data() {
            return {
                newPostTitle: '',
                newPostText: '',
                newPostAuthor: '',
            }
        },
        props: {
            users: Array,
            posts: Array
        },
        emits: ['close', 'newPost'],
        methods: {
            saveChanges() {
                if(this.newPostTitle !== '' && this.newPostText !== '' && this.newPostAuthor !== ''){
                fetch('https://jsonplaceholder.typicode.com/posts', {
                    method: 'POST',
                    body: JSON.stringify({
                        title: this.newPostTitle,
                        body: this.newPostText,
                        userId: Number(this.newPostAuthor),
                    }),
                    headers: {
                        'Content-type': 'application/json; charset=UTF-8',
                    },
                    })
                    .then(response => response.json())
                    .catch((error) => {
                        alert('Не удалось сохранить пост');
                        console.log(error);
                    })
                    .finally(this.$emit('newPost', this.newPostObj));
                }
                else {
                    alert('Заполните все поля')
                }

            },
        },
        computed: {
            newPostObj() {
                let lastId = this.posts[this.posts.length - 1].id;
                return {
                    "userId": this.newPostAuthor,
                    "id": lastId + 1,
                    "title": this.newPostTitle,
                    "body": this.newPostText
                }
            }
        }
    }
</script>

<style lang="scss" scoped>
.new_post__div {
    position: fixed;
    left: 10%;
    width: 80%;
    background-color: #fff;
    z-index: 5;
    box-shadow: 0 5px 10px gray;

    &__inputs {
        width: 100%;
        display: flex;
        flex-direction: column;
        gap: 20px;
        align-items: flex-start;
        padding: 0 40px;
        margin-bottom: 40px;

        & input {
            width: calc(100% - 80px);
            font-family: Avenir, Helvetica, Arial, sans-serif;
        }

        &_text {
            width: calc(100% - 80px);
            font-family: Avenir, Helvetica, Arial, sans-serif;
        }
    }

    &__buttons {
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 20px;
        margin-bottom: 40px;

        &_save {
            color: #fff;
            background-color: #4a84be;
            border: none;
            border-radius: 4px;
            transition: background-color 0.3s;
            padding: 12px;

            &:hover {
                background-color: #6ca3da;
            }
        }

        &_close {
            color: #fff;
            background-color: #c55445;
            border: none;
            border-radius: 4px;
            transition: background-color 0.3s;
            padding: 12px;

            &:hover {
                background-color: #e76b5a;
            }
        }
    }
}
</style>