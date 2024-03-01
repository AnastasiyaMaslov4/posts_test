<template>
    <div class="pagination_div">
        <p>Страницы:</p>
        <button v-for="page in pages" :value="page" @click="$emit('setPage', page)">{{ page }}</button>
    </div>
</template>

<script>
    export default {
        name: 'Pagination',
        props: {
            allPosts: Number,
            perPage: String
        },
        emits: ['setPage'],
        data() {
            return {
            }
        },
        computed: {
            pages() {
                let pagesArr = [];
                let total = Math.ceil(this.allPosts / this.perPage);
                for (let i = 0; i < total; i++) {
                    pagesArr.push(i+1);
                }
                return pagesArr;
            }
        }
    }
</script>

<style lang="scss">
.pagination_div {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    gap: 12px;
    margin: 20px 10%;

    & button {
        border: none;
        background-color: transparent;
        font-size: 20px;
        border-bottom: 1px solid transparent;
        transition: all 0.3s;
        
        &:hover {
            border-bottom: 1px solid #2c3e50;
        }
    }
}
</style>