<template>
    <div class="posts_list__item" :class="{ posts_list__item_favourite: this.favourite}">
        <div class="posts_list__item__main">
        <h1 class="posts_list__item__title">Заголовок: {{title}}</h1>
        <h3 class="posts_list__item__title">Автор: {{ author }}</h3>
        <p class="posts_list__item__text">Текст: <span v-html="this.htmltext"></span></p>
        <div class="posts_list__item__bottom">
        <div class="posts_list__item__buttons">
            <button title="Комментарии" @click="showComments" class="posts_list__item__buttons__btn" :class="{ posts_list__item__buttons__btn_active: this.commentsActive }">
                <svg viewBox="-0.5 0 32 32" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:sketch="http://www.bohemiancoding.com/sketch/ns" fill="#000000"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <title>comments</title> <desc>Created with Sketch Beta.</desc> <defs> </defs> <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd" sketch:type="MSPage"> <g id="Icon-Set" sketch:type="MSLayerGroup" transform="translate(-257.000000, -255.000000)" fill="#000000"> <path d="M259,266.5 C259,261.254 263.753,257 270,257 C274.973,257 280,261.254 280,266.5 C280,271.747 276.075,276 270,276 C269.107,276 267.244,275.898 266.413,275.725 L263,278 L263,274.456 C260.561,272.477 259,269.834 259,266.5 L259,266.5 Z M266.637,277.736 C267.414,277.863 269.181,278 270,278 C277.18,278 282,272.657 282,266.375 C282,260.093 275.977,255 270,255 C262.811,255 257,260.093 257,266.375 C257,270.015 258.387,273.104 261,275.329 L261,281 L266.637,277.736 L266.637,277.736 Z M283.949,264.139 C283.968,264.425 284,264.709 284,265 C284,265.636 283.938,266.259 283.849,266.874 C285.195,268.45 286,270.392 286,272.5 C286,275.834 284.008,278.761 281,280.456 L281,284 L277.587,281.725 C276.756,281.898 275.893,282 275,282 C272.41,282 271.034,281.222 269.154,279.929 C268.609,279.973 268.059,280 267.5,280 C267.102,280 266.712,279.972 266.32,279.949 C268.701,282.276 271.149,283.75 275,283.75 C275.819,283.75 276.618,283.676 277.395,283.549 L283,287 L283,281.329 C286.04,279.246 288,276.015 288,272.375 C288,269.131 286.439,266.211 283.949,264.139 L283.949,264.139 Z M275.5,268 C276.329,268 277,267.329 277,266.5 C277,265.672 276.329,265 275.5,265 C274.671,265 274,265.672 274,266.5 C274,267.329 274.671,268 275.5,268 L275.5,268 Z M263.5,268 C264.329,268 265,267.329 265,266.5 C265,265.672 264.329,265 263.5,265 C262.671,265 262,265.672 262,266.5 C262,267.329 262.671,268 263.5,268 L263.5,268 Z M269.5,268 C270.329,268 271,267.329 271,266.5 C271,265.672 270.329,265 269.5,265 C268.671,265 268,265.672 268,266.5 C268,267.329 268.671,268 269.5,268 L269.5,268 Z" id="comments" sketch:type="MSShapeGroup"> </path> </g> </g> </g></svg>
            </button>
            <button title="Редактировать" @click="editPost" class="posts_list__item__buttons__btn" :class="{ posts_list__item__buttons__btn_active: this.editActive }">
                <svg viewBox="0 0 32 32" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:sketch="http://www.bohemiancoding.com/sketch/ns" fill="#000000"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <title>new</title> <desc>Created with Sketch Beta.</desc> <defs> </defs> <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd" sketch:type="MSPage"> <g id="Icon-Set" sketch:type="MSLayerGroup" transform="translate(-516.000000, -99.000000)" fill="#000000"> <path d="M527.786,122.02 L522.414,125.273 C521.925,125.501 521.485,125.029 521.713,124.571 L524.965,119.195 L527.786,122.02 L527.786,122.02 Z M537.239,106.222 L540.776,109.712 L529.536,120.959 C528.22,119.641 526.397,117.817 526.024,117.444 L537.239,106.222 L537.239,106.222 Z M540.776,102.683 C541.164,102.294 541.793,102.294 542.182,102.683 L544.289,104.791 C544.677,105.18 544.677,105.809 544.289,106.197 L542.182,108.306 L538.719,104.74 L540.776,102.683 L540.776,102.683 Z M524.11,117.068 L519.81,125.773 C519.449,126.754 520.233,127.632 521.213,127.177 L529.912,122.874 C530.287,122.801 530.651,122.655 530.941,122.365 L546.396,106.899 C547.172,106.124 547.172,104.864 546.396,104.088 L542.884,100.573 C542.107,99.797 540.85,99.797 540.074,100.573 L524.619,116.038 C524.328,116.329 524.184,116.693 524.11,117.068 L524.11,117.068 Z M546,111 L546,127 C546,128.099 544.914,129.012 543.817,129.012 L519.974,129.012 C518.877,129.012 517.987,128.122 517.987,127.023 L517.987,103.165 C517.987,102.066 518.902,101 520,101 L536,101 L536,99 L520,99 C517.806,99 516,100.969 516,103.165 L516,127.023 C516,129.22 517.779,131 519.974,131 L543.817,131 C546.012,131 548,129.196 548,127 L548,111 L546,111 L546,111 Z" id="new" sketch:type="MSShapeGroup"> </path> </g> </g> </g></svg>
            </button>
            <button title="Удалить" @click="deletePost()" class="posts_list__item__buttons__btn">
                <svg viewBox="-3 0 32 32" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:sketch="http://www.bohemiancoding.com/sketch/ns" fill="#000000"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <title>trash</title> <desc>Created with Sketch Beta.</desc> <defs> </defs> <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd" sketch:type="MSPage"> <g id="Icon-Set" sketch:type="MSLayerGroup" transform="translate(-259.000000, -203.000000)" fill="#000000"> <path d="M282,211 L262,211 C261.448,211 261,210.553 261,210 C261,209.448 261.448,209 262,209 L282,209 C282.552,209 283,209.448 283,210 C283,210.553 282.552,211 282,211 L282,211 Z M281,231 C281,232.104 280.104,233 279,233 L265,233 C263.896,233 263,232.104 263,231 L263,213 L281,213 L281,231 L281,231 Z M269,206 C269,205.447 269.448,205 270,205 L274,205 C274.552,205 275,205.447 275,206 L275,207 L269,207 L269,206 L269,206 Z M283,207 L277,207 L277,205 C277,203.896 276.104,203 275,203 L269,203 C267.896,203 267,203.896 267,205 L267,207 L261,207 C259.896,207 259,207.896 259,209 L259,211 C259,212.104 259.896,213 261,213 L261,231 C261,233.209 262.791,235 265,235 L279,235 C281.209,235 283,233.209 283,231 L283,213 C284.104,213 285,212.104 285,211 L285,209 C285,207.896 284.104,207 283,207 L283,207 Z M272,231 C272.552,231 273,230.553 273,230 L273,218 C273,217.448 272.552,217 272,217 C271.448,217 271,217.448 271,218 L271,230 C271,230.553 271.448,231 272,231 L272,231 Z M267,231 C267.552,231 268,230.553 268,230 L268,218 C268,217.448 267.552,217 267,217 C266.448,217 266,217.448 266,218 L266,230 C266,230.553 266.448,231 267,231 L267,231 Z M277,231 C277.552,231 278,230.553 278,230 L278,218 C278,217.448 277.552,217 277,217 C276.448,217 276,217.448 276,218 L276,230 C276,230.553 276.448,231 277,231 L277,231 Z" id="trash" sketch:type="MSShapeGroup"> </path> </g> </g> </g></svg>
            </button>
            <button title="В избранное" @click="addToFavourite" class="posts_list__item__buttons__btn">
                <svg viewBox="0 0 32 32" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:sketch="http://www.bohemiancoding.com/sketch/ns" fill="#000000"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <title>start-favorite</title> <desc>Created with Sketch Beta.</desc> <defs> </defs> <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd" sketch:type="MSPage"> <g id="Icon-Set" sketch:type="MSLayerGroup" transform="translate(-152.000000, -879.000000)" fill="#000000"> <path d="M168,903.21 L160.571,907.375 L161.989,898.971 L155.594,892.442 L164.245,891.317 L168,883.313 L171.722,891.317 L180.344,892.54 L174.011,899.002 L175.335,907.406 L168,903.21 L168,903.21 Z M184,891.244 L172.962,889.56 L168,879 L163.038,889.56 L152,891.244 L159.985,899.42 L158.095,911 L168,905.53 L177.905,911 L176.015,899.42 L184,891.244 L184,891.244 Z" id="start-favorite" sketch:type="MSShapeGroup"> </path> </g> </g> </g></svg>
            </button>
        </div>
        <div class="posts_list__item__checkbox">
            <label for="post_checkbox" class="posts_list__item__checkbox__title">Отметить пост</label>
            <input type="checkbox" id="post_checkbox" @click="checkPost" v-model="this.checked">
        </div>
        </div>
      </div>
    </div>
    <div v-if="this.commentsActive" class="comments_list">
        <Comments v-for="comment in comments" :name="comment.name" :email="comment.email" :text="comment.body"/>
    </div>
    <transition name="fade" appear>
    <EditPost v-if="this.editActive" :postTitle="this.title" :postAuthor="this.author" :postAuthorId="this.authorId" :postText="this.text" :postId="this.postId" :users="this.users" @changePost="changePost" @close="editPost"/>
    </transition>
  </template>
  
  <script>
import Comments from './Comments.vue'
import EditPost from './EditPost.vue'

  export default {
    name: 'Post',
    data() {
        return {
            comments: [],
            commentsActive: false,
            editActive: false,
            checked: false
        }
    },
    props: {
      title: String,
      author: String,
      authorId: Number,
      text: String,
      postId: Number,
      favourite: Boolean,
      checkedPosts: Array,
      users: Array
    },
    components: {
        Comments,
        EditPost,
    },
    emits: ['favourited', 'delete', 'checkPost', 'editedPost'],
    methods: {
        getComments() {
            fetch(`https://jsonplaceholder.typicode.com/posts/${this.postId}/comments`)
                .then(response => response.json())
                .then(json => this.comments = json);
        },
        showComments() {
            this.getComments();
            this.commentsActive = !this.commentsActive;
        },
        editPost() {
            this.editActive = !this.editActive;
        },
        changePost(post) {
            this.$emit('editedPost', post);
        },
        addToFavourite() {
            this.$emit('favourited');
        },
        deletePost() {
            if(confirm('Удалить этот пост?')) {
                fetch(`https://jsonplaceholder.typicode.com/posts/${this.postId}`, {
                method: 'DELETE',
            }).then(this.$emit('delete'));
            }            
        },
        checkPost() {
            this.$emit('checkPost', this.postId);
        }

    },
    watch: {
        checkedPosts(newValue) {
            if(!newValue.includes(this.postId)) this.checked = false;
        },
    },
    computed: {
        htmltext() {
            return this.text.replace(/\n\r?/g, '<br>');
        }
    }
  }
  </script>

  <style scoped lang="scss">
    .fade-enter-active,
    .fade-leave-active {
        transition: opacity 0.5s ease;
    }

    .fade-enter-from,
    .fade-leave-to {
        opacity: 0;
    }
  .posts_list__item {
    position: relative;
    border: 2px solid rgb(235, 235, 235);
    padding: 20px 16px 20px 16px;

    &__main {
        width: 100%;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: flex-start;
        text-align: left;
    }

    &__text {
        margin-bottom: 20px;
    }

    &__title {
        margin-bottom: 0;
    }

    &__bottom {
        width: 100%;
        display: flex;
        flex-wrap: wrap;
        flex-flow: row wrap;
        justify-content: space-around;
        align-items: center;
        row-gap: 16px;
    }

    &__buttons {
        display: flex;
        gap: 12px;
        justify-content: center;
        align-items: center;

        &__btn {
            width: 32px;
            height: 32px;
            border: none;
            border-radius: 20%;
            background-color: rgb(235, 235, 235);
            transition: background-color 0.3s;

            &:hover {
                background-color: rgb(206, 206, 206);
            }

            &_active {
                background-color: #6ca3da;

                &:hover {
                    background-color: #4a84be;
                }
            }
        }
    }

    &__checkbox {
        display: flex;
        align-items: center;

        & input {
            width: 32px;
            height: 32px;
            border-radius: 4px;
        }
    }

    &_favourite {
       background-color: #f1dfa4;
    }
  }

  .comments_list {
    display: flex;
    flex-direction: column;
    gap: 12px;
    padding-left: 40px;
  }
    
  </style>
  