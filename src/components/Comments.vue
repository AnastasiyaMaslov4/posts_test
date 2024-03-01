<template>
    <transition name="fade" appear>
    <div class="comment_div">
        <p class="comment_div__name"><span class="bold">Имя отправителя:</span> {{ name }}</p>
        <p class="comment_div__mail"><span class="bold">E-mail:</span> {{ email }}</p>
        <p class="comment_div__text"><span class="bold">Комментарий:</span> <span v-html="this.htmltext"></span></p>
    </div>
    </transition>
</template>

<script>
    export default {
        name: 'Comments',
        props: {
            name: String,
            email: String,
            text: String
        },
        computed: {
        htmltext() {
            return this.text.replace(/\n\r?/g, '<br>');
        }
    }
    }
</script>

<style lang="scss" scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
.comment_div {
    border: 1px solid rgb(235, 235, 235);;
    display: flex;
    flex-direction: column;
    gap: 16px;
    justify-content: center;
    align-items: flex-start;
    text-align: left;
    padding: 12px;

    &__name, &__mail, &__text {
        margin: 0;
        padding: 0;
    }
}

.bold {
    font-weight: bold;
}
</style>