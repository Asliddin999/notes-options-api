<template>
    <transition name="modal">
        <div class="modal" @click="clean">
            <div class="modal__content" @click.stop>
                <!-- <slot name="modal1">
                    modal1
                </slot> -->
                <h3 class="modal__title">{{curNote.id ? 'Изменить' : 'Добавить'}} заметку</h3>
                <form class="modal__form" @submit.prevent="send">
                    <input type="text" placeholder="Title" class="modal__input" required v-model="user.title">
                    <textarea class="modal__input modal__area" placeholder="Content" required v-model="user.text"></textarea>
                    <div class="modal__control">
                        <a href="#!" class="modal__cancel" @click.prevent="clean">Отмена</a>
                        <button class="modal__btn">{{curNote.id ? 'Изменить' : 'Добавить'}}</button>
                    </div>
                </form>
                <!-- <slot>
                    Ничего не передано
                </slot>
                
                <slot name="modal2">
                    modal2
                </slot> -->
            </div>
        </div>
    </transition>
</template>
<script>
export default {
    data(){
        return {
            user: {
                title: '',
                text: '',
            }
        }
    },
    methods: {
        clean() {
            for (const key in this.user) this.user[key] = '';
            this.$emit('showOrClose'); 
        },
        send(){
            const note = {...this.user};
            note.id = this.curNote.id || null;
            this.$emit('addNote', note);
            this.clean();
        }
    },
    props: {
        curNote: {
            type: Object,
            default: {}
        }
    },
    watch: {
        curNote(){
            if(this.curNote.id) {
                this.user.title = this.curNote.title;
                this.user.text = this.curNote.text;
            }
        }
    }
}
</script>