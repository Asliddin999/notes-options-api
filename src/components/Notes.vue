<template>
    <div class="notes">
        <div class="container">
            <div class="notes__nav">
                <h3 class="notes__title">{{notes.length ? 'Все заметки' : 'Нет заметок'}}</h3>
                <button class="notes__checker" @click="grid = !grid">
                    <img src="@/assets/img/list.svg" alt="" v-if="grid">
                    <img src="@/assets/img/grid.svg" alt="" v-else>
                    <span>{{grid ? 'Список' : 'Сетка'}}</span>
                </button>
            </div>
            <transition-group 
                tag="div" 
                class="notes__grid" 
                :class="{column: !grid}" 
                name="notes" appear>
                <OneNote v-for="note in notes" 
                    :key="note.id"
                    :note="note"
                    @remove="$emit('remove', note.id)"
                    @edit="$emit('edit', note)"/>
            </transition-group>
        </div>
    </div>
</template>
<script>
import OneNote from './OneNote.vue';
export default {
    components: { OneNote },
    data(){
        return {
            grid: true
        }
    },
    props: {
        notes: {
            type: Array,
            default: []
        }
    }
}
</script>