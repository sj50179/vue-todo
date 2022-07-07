<template>
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" v-on:keypress.enter="addTodo">
        <span class="addContainer" v-on:click="addTodo">
            <i class="addBtn fa-solid fa-plus" aria-hidden="true"></i>
        </span>

        <TodoModal v-if="showModal" @close="showModal = false">
            <h3 slot="header">
                경고!
            </h3>
            <div slot="body">
                아무것도 입력하지 않으셨습니다. <br />
                할 일을 입력하세요.
            </div>
            <div slot="footer">
                <i class="closeModalBtn fa-solid fa-xmark" @click="showModal = false">CLOSE</i>
            </div>

        </TodoModal>
    </div>
</template>

<script>
import TodoModal from './common/TodoModal.vue'

export default {
    data() {
        return {
            newTodoItem: '',
            showModal: false
        }
    },
    methods: {
        addTodo() {
            if (this.newTodoItem !== '') {
                // this.$emit('이벤트 이름', 인자1, 인자2, ...)
                this.$emit('addTodoItem', this.newTodoItem)
                this.clearInput();
            }
            else {
                this.showModal = !this.showModal;
            }
        },
        clearInput() {
            this.newTodoItem = '';
        }
    },
    components: {
        TodoModal
    }
}
</script>

<style scoped>
input:focus {
    outline: none;
}

.inputBox {
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
}

.inputBox input {
    border-style: none;
    font-size: 0.9rem;
}

.addContainer {
    float: right;
    background: linear-gradient(to right, #6478FB, #8763FB);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
}

.addBtn {
    color: white;
    vertical-align: middle;
}
.closeModalBtn {
    color: #42b983;
}
</style>