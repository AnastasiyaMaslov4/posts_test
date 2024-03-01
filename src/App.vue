<template>
  <div class="head_div">
    <h1 class="head_div__title">Посты</h1>
    <button class="head_div__new_post_btn" @click="newPost = true">Добавить новый пост</button>
  </div>
  <transition name="fade">
  <newPost v-if="this.newPost" v-on:close="this.newPost = false" v-on:newPost="addPost" :users="this.users" :posts="this.posts"></newPost>
  </transition>
  <div class="filters_div">
            <label for="postsPerPage">Количество постов на странице: </label>
            <select class="filters_div__select" v-model="perPage" name="perPage" id="postsPerPage" >
                <option value="10" selected>10</option>
                <option value="20">20</option>
                <option value="50">50</option>
                <option value="100">100</option>
                <option value="all">Все</option>
            </select>
        <div>
            <h3>Фильтры</h3>
            <div class="filters_div__filter_by">
              <div class="filters_div__filter_by__item filters_div__filter_by__item-1">
                <label for="filter_title">По названию поста:</label>
                <input v-model="FilterTitle" class="filters_div__select" type="text" name="" id="filter_title" placeholder="Введите название">
              </div>
              <div class="filters_div__filter_by__item filters_div__filter_by__item-2">
                <label for="filter_name">По имени автора:</label>
                <select v-model="filterAuthorName" @change="filterByAuthor" class="filters_div__select" name="" id="filter_name">
                    <option value="all">Все</option>
                    <option v-for="author in this.users" :key="author.id" :value="author.id" selected> {{ author.name }}</option>
                </select>
              </div>
              <button @click="showFavourite" :class="{selected : this.filterFavourite}">Показать избранное <svg viewBox="0 0 32 32" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:sketch="http://www.bohemiancoding.com/sketch/ns" fill="#000000"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <title>start-favorite</title> <desc>Created with Sketch Beta.</desc> <defs> </defs> <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd" sketch:type="MSPage"> <g id="Icon-Set" sketch:type="MSLayerGroup" transform="translate(-152.000000, -879.000000)" fill="#000000"> <path d="M168,903.21 L160.571,907.375 L161.989,898.971 L155.594,892.442 L164.245,891.317 L168,883.313 L171.722,891.317 L180.344,892.54 L174.011,899.002 L175.335,907.406 L168,903.21 L168,903.21 Z M184,891.244 L172.962,889.56 L168,879 L163.038,889.56 L152,891.244 L159.985,899.42 L158.095,911 L168,905.53 L177.905,911 L176.015,899.42 L184,891.244 L184,891.244 Z" id="start-favorite" sketch:type="MSShapeGroup"> </path> </g> </g> </g></svg></button>
            </div>
            <div class="filters_div__sort_by">
              <button :class="{selected : this.sortUp}" @click="setSort">Сортировать по возрастанию id 
                <svg viewBox="0 -0.5 29 29" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:sketch="http://www.bohemiancoding.com/sketch/ns" fill="#000000"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <title>Fill 194</title> <desc>Created with Sketch Beta.</desc> <defs> </defs> <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd" sketch:type="MSPage"> <g id="Icon-Set" sketch:type="MSLayerGroup" transform="translate(-518.000000, -205.000000)" fill="#000000"> <path d="M546,218.984 L532,218.984 C531.447,218.984 531,219.433 531,219.985 C531,220.538 531.447,220.986 532,220.986 L546,220.986 C546.553,220.986 547,220.538 547,219.985 C547,219.433 546.553,218.984 546,218.984 L546,218.984 Z M546,212.978 L538,213 C537.447,213 537,213.426 537,213.979 C537,214.532 537.447,215 538,215 L546,214.979 C546.553,214.979 547,214.532 547,213.979 C547,213.426 546.553,212.978 546,212.978 L546,212.978 Z M546,224.991 L532,224.991 C531.447,224.991 531,225.439 531,225.992 C531,226.545 531.447,226.993 532,226.993 L546,226.993 C546.553,226.993 547,226.545 547,225.992 C547,225.439 546.553,224.991 546,224.991 L546,224.991 Z M534,209 L546,209 C546.553,209 547,208.525 547,207.973 C547,207.419 546.553,206.971 546,206.971 L534,206.971 C533.447,206.971 533,207.419 533,207.973 C533,208.525 533.447,209 534,209 L534,209 Z M533.687,214.697 C534.079,214.304 534.079,213.666 533.687,213.271 L526.745,205.283 C526.535,205.073 526.258,204.983 525.984,204.998 C525.711,204.983 525.434,205.073 525.224,205.283 L518.282,213.271 C517.89,213.666 517.89,214.304 518.282,214.697 C518.674,215.091 519.31,215.091 519.701,214.697 L525,208.601 L525,233 L527,233 L527,208.636 L532.268,214.697 C532.659,215.091 533.295,215.091 533.687,214.697 L533.687,214.697 Z M546,231 L532,231 C531.447,231 531,231.446 531,231.999 C531,232.552 531.447,233 532,233 L546,233 C546.553,233 547,232.552 547,231.999 C547,231.446 546.553,231 546,231 L546,231 Z" id="Fill-194" sketch:type="MSShapeGroup"> </path> </g> </g> </g></svg>
              </button>
              <button :class="{selected : !this.sortUp}" @click="setSort">Сортировать по убыванию id
                <svg viewBox="0 -0.5 29 29" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:sketch="http://www.bohemiancoding.com/sketch/ns" fill="#000000"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <title>Fill 195</title> <desc>Created with Sketch Beta.</desc> <defs> </defs> <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd" sketch:type="MSPage"> <g id="Icon-Set" sketch:type="MSLayerGroup" transform="translate(-466.000000, -205.000000)" fill="#000000"> <path d="M494,217.014 L480,217.014 C479.447,217.014 479,217.462 479,218.015 C479,218.567 479.447,219 480,219 L494,219.016 C494.553,219.016 495,218.567 495,218.015 C495,217.462 494.553,217.014 494,217.014 L494,217.014 Z M494,211.007 L480,211.007 C479.447,211.007 479,211.455 479,212.008 C479,212.561 479.447,213 480,213 L494,213 C494.553,213 495,212.561 495,212.008 C495,211.455 494.553,211.007 494,211.007 L494,211.007 Z M494,223.021 L486,223.021 C485.447,223.021 485,223.469 485,224.021 C485,224.574 485.447,225 486,225 L494,225 C494.553,225 495,224.574 495,224.021 C495,223.469 494.553,223.021 494,223.021 L494,223.021 Z M494,229.027 L482,229.027 C481.447,229.027 481,229.476 481,230.028 C481,230.581 481.447,231.029 482,231.029 L494,231 C494.553,231 495,230.581 495,230.028 C495,229.476 494.553,229.027 494,229.027 L494,229.027 Z M480,207.002 L494,207 C494.553,207 495,206.554 495,206.001 C495,205.448 494.553,205 494,205 L480,205 C479.447,205 479,205.448 479,206.001 C479,206.554 479.447,207.002 480,207.002 L480,207.002 Z M481.687,223.303 C481.295,222.909 480.659,222.909 480.268,223.303 L475,229.364 L475,205 L473,205 L473,229.4 L467.701,223.303 C467.31,222.909 466.674,222.909 466.282,223.303 C465.89,223.697 465.89,224.335 466.282,224.729 L473.224,232.717 C473.434,232.927 473.711,233.017 473.984,233.002 C474.258,233.017 474.535,232.927 474.745,232.717 L481.687,224.729 C482.079,224.335 482.079,223.697 481.687,223.303 L481.687,223.303 Z" id="Fill-195" sketch:type="MSShapeGroup"> </path> </g> </g> </g></svg>
              </button>
            </div>
        </div>
    </div>
  <PostsList :perPage="this.perPage" :posts="this.showedPosts" :users="this.users" :appLoading="this.loading" v-on:addToFavourite="addToFavourite" v-on:deletePost="deletePost" v-on:updateCheckedPosts="setCheckedPosts" :clearCheckedPosts="this.clearCheckedPosts" :favouritePosts="this.favouritePosts" @editedPost="editPost"/>
  <Pagination :perPage="this.perPage" :allPosts="this.filteredPosts.length" v-on:setPage="changePage"></Pagination>
  <transition name="fade">
  <div class="checked_div" v-if="this.checked">
    <h2>Действие с выбранными постами</h2>
    <div class="checked_div__buttons">
      <button @click="allToFavourite">В избранное</button>
      <button @click="deleteAll">Удалить</button>
    </div>
  </div>
  </transition>
</template>

<script>
import Pagination from './components/Pagination.vue';
import PostsList from './components/PostsList.vue'
import newPost from './components/newPost.vue'

export default {
  name: 'App',
  components: {
    PostsList,
    newPost,
    Pagination
  },
  data() {
    return {
      newPost: false,
      perPage: '10',
      page: 1,
      FilterTitle: '',
      filter_favourite: false,
      filterAuthorName: 'all',
      filterFavourite: false,
      sortUp: true,
      posts: [],
      filteredPosts: [],
      users: [],
      checkedPosts: [],
      clearCheckedPosts: false,
      favouritePosts: [],
      loading: true,
      newPostObject: {}
    }
  },
  methods: {
    getData() {
      Promise.all([fetch('https://jsonplaceholder.typicode.com/posts').then(response => response.json()).then(json => this.posts = json), 
      fetch('https://jsonplaceholder.typicode.com/users').then(response => response.json()).then(json => this.users = json)])
      .catch((error) => {
        console.log(error);
        alert(`Не удалось загрузить данные`)})
        .finally(() => {this.loading = false});
    },
    showFavourite() {
      this.filterFavourite = !this.filterFavourite;
    },
    setSort() {
      this.sortUp = !this.sortUp;
    },
    addPost(post) {
      this.newPost = false;
      this.posts.push(post);
    },
    setCheckedPosts(arr) {
      this.checkedPosts = arr;
      this.clearCheckedPosts = false;
    },
    addToFavourite(postId) {
      let post = this.posts.find(post => post.id === postId);
      if(!this.favouritePosts.includes(post)) this.favouritePosts.push(post);
      else this.favouritePosts.splice(this.favouritePosts.indexOf(post),1);
    },
    allToFavourite() {
      this.checkedPosts.forEach(id => {
        this.addToFavourite(id)
      })
      this.checkedPosts = [];
      this.clearCheckedPosts = true;
    },
    deletePost(postId) {
      let post = this.posts.find(post => post.id === postId);
      this.posts.splice(this.posts.indexOf(post), 1);
    },
    deleteAll() {
      this.checkedPosts.forEach(id => {
          this.deletePost(id)
      });
      this.checkedPosts = [];
      this.clearCheckedPosts = true;
    },
    changePage(pageNum) {
      this.page = Number(pageNum);
    },
    editPost(newPost) {
      let oldPost = this.posts.find(post => post.id === newPost.id);
      this.posts.splice(this.posts.indexOf(oldPost), 1, newPost);
    }
  },
  computed: {
    showedPosts() {
      let result = this.posts;
      if(this.FilterTitle !== '') result = result.filter(post => post.title.includes(`${this.FilterTitle}`));
      if(this.filterAuthorName !== 'all') result = result.filter(post => post.userId == this.filterAuthorName);
      if(this.filterFavourite) result = result.filter(post => this.favouritePosts.includes(post));
      if(!this.sortUp) result = result.reverse();
      this.filteredPosts = result;
      if(this.perPage === 'all') return result;
      else return result.slice((this.perPage * (this.page - 1)), (this.perPage * this.page));
    },
    checked() {
      if(this.checkedPosts.length !== 0) return true;
      else return false;
    }
  },
  created() {
    this.getData();
    this.perPage = localStorage.getItem('postsPerPage') ? localStorage.getItem('postsPerPage') : '10';
  }
}
</script>

<style lang="scss">
body {
  margin: 0;
}

#app {
  margin: 0;
  padding: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.head_div {
  width: 80%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 0 auto;

    &__new_post_btn {
    border: none;
    border-radius: 4px;
    background-color: #c55445;
    color: #fff;
    transition: background-color 0.3s;
    padding: 12px;

    &:hover {
      background-color: #e76b5a;
    }
  }
}

.filters_div {
  background-color: #dbdbdb;
  padding: 20px 10%;
  margin-bottom: 20px;

  &__filter_by {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    gap: 12px;
    margin-bottom: 20px;

    &__item {
      display: flex;
      flex-wrap: nowrap;
      justify-content: center;
      align-items: center;
      gap: 4px;

      &-1{
        flex-grow: 2;
      }
    }

    & button {
      height: 32px;
      display: flex;
      flex-wrap: nowrap;
      justify-content: center;
      gap: 4px;
      align-items: center;
      border-radius: 4px;
      transition: background-color 0.3s;
      padding: 4px;

      & svg {
        width: 16px;
        height: 16px;
      }

      &:hover {
        background-color: #cccccc;
      }
    }
  }

  &__select {
    border: none;
    border-radius: 4px;
    padding: 4px 12px;

    &:active {
      outline: none;
    }
  }

  &__sort_by {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    gap: 12px;

    & button {
      transition: background-color 0.3s;
      height: 32px;
      display: flex;
      flex-wrap: nowrap;
      justify-content: center;
      gap: 4px;
      align-items: center;
      border-radius: 4px;
      padding: 12px;

      & svg {
        width: 16px;
        height: 16px;
      }

      &:hover {
        background-color: #cccccc;
      }
    }
  }

  & button {
    border: none;
  }
}

.selected {
  background-color: #6ca3da;

    &:hover {
      background-color: #4a84be;
    }
}

.checked_div {
  position: fixed;
  bottom: 40px;
  left: 10%;
  width: 80%;
  background-color: #fff;
  box-shadow: 0 5px 10px gray;

  &__buttons {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 12px;
    margin-bottom: 20px;

    & button {
      border: none;
      padding: 12px;
    }
  }
}
</style>
