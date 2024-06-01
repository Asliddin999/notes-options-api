<template>
    <div class="notes__item">
        <h3 class="notes__name">{{note.title}}</h3>
        <span class="notes__date">{{note.date}}</span>
        <p class="notes__descr">
            {{note.text}}
        </p>
        <div class="notes__control">
            <a href="#!" class="notes__edit" @click.prevent="$emit('edit', note)">
                <img src="@/assets/img/edit.svg" alt="">
                Редактировать
            </a>
            <a href="#!" class="notes__delete" @click.prevent="$emit('remove', note.id)">
                <img src="@/assets/img/delete.svg" alt="">
                Удалить
            </a>
        </div>
    </div>
</template>
<script>
export default {
    props: {
        note: {
            type: Object,
            default: {}
        }
    }
}
</script>