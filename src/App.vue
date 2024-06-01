<template>
<!-- Options API -->
    <Header @find="search = $event"/>
    <Notes :notes="filterNotes" @remove="removeNote" @edit="editNote"/>
    <Teleport to="body">
        <Modal
            v-show="showModal"
            @showOrClose="showModal = false;curNote={}"
            @addNote="addOrChangeNote"
            :curNote="curNote"
        >
        <!-- slots -->
            <!-- <div class="hsdf">
                <a href="sdf">sdfsdf</a>
                <p>
                    Lorem ipsum dolor sit amet consectetur adipisicing elit.
                    Similique facilis nam iste illo molestias culpa.
                </p>
            </div>
            <template v-slot:modal1>
                <p>thia is slot modal1</p>
            </template>
            <template #modal2>
                <p>thia is slot modal2</p>
            </template> -->
        </Modal>
    </Teleport>
    <a href="#!" class="add__note" @click.prevent="showModal = true">
        <img src="@/assets/img/add-note.svg" alt="" />
    </a>
</template>
<script>
import "@/assets/styles/main.scss";
import Header from "./components/Header.vue";
import Notes from "./components/Notes.vue";
import Modal from "./components/Modal.vue";
export default {
    components: {
        Header,
        Notes,
        Modal,
    },
    data() {
        return {
            showModal: false,
            notes: localStorage.notes ? JSON.parse(localStorage.notes) : [],
            search: '',
            curNote: {}
        };
    },
    computed: {
        filterNotes(){
            if(this.search) {
                let se = this.search.toLowerCase();
                const filterNotes = this.notes.filter(item => {
                    const title = item.title.toLowerCase();
                    if(title.includes(se)) return item;
                });
                return filterNotes;
            }
            else return this.notes;
        }
    },
    methods: {
        addOrChangeNote(val) {
            const note = { ...val };
            note.date = new Date().toLocaleDateString();
            note.id = val.id || Date.now();
            if(val.id) {
                const idx = this.notes.findIndex(c => c.id == val.id);
                if(idx !== -1) this.notes[idx] = note;
            }
            else this.notes.push(note);
        },
        removeNote(id){
            const idx = this.notes.findIndex(c => c.id == id);
            this.notes.splice(idx, 1);
        },
        editNote(obj){
            this.curNote = obj;
            this.showModal = true;
        }
    },
    watch: {
        notes: {
            handler(){
                localStorage.setItem('notes', JSON.stringify(this.notes));
            },
            deep: true
        }
    }
};

</script>
