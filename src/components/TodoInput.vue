<template>
    <div class="inputBox shadow">
        <input type= "text" v-model="newTodoItem" placeholder="Type what you have to do" v-on:keyup.enter="addTodo">
        <span class="addContainer" v-on:click="addTodo">
            <i class="addBtn fas fa-plus" aria-hidden="true"></i>
            <!-- 어썸 아이콘의 + 아이콘을 추가 -->
        </span>

        <modal v-if="showModal" @close="showModal=false">
            <h3 slot="header">경고</h3>
            <span slot="footer" @click="shwoModal=false">
                할 일을 입력하세요.
                <i class="closeModalBtn fas f-times" aria-hidden="true"></i>
            </span>
        </modal>
    </div>
</template>

<script>
import Modal from './common/Modal.vue'

export default {
    data(){
        return{
            newTodoItem: '',
            showModal: false
        }
    },
    methods: {
        addTodo: function() {
            if (this.newTodoItem !==""){ // 인풋박스 입력값이 있을 경우에만 저장
                var value = this.newTodoItem && this.newTodoItem.trim(); // input 박스 입력에 대한 앞뒤 공백 문자열 제거
                this.$emit('addTodo', value);
                this.clearInput();
            } else {
                 this.showModal = !this.showModal;
            }
        },

        clearInput(){
            this.newTodoItem = ''; // 인풋 박스의 입력 값을 초기화
        },
        },
    components: {
        Modal: Modal
    },
    }

</script>

<style scoped>
input:focus {
    outline:none;
}
.inputBox {
    background: white;
    height: 50px;
    line-height: 50px; /* 인풋 박스에 입력되는 텍스트의 중앙 정렬을 위해 사용 */
    border-radius: 5px; /* 인풋 박스의 둥근 테두리 속성 설정 */
}
.inputBox input {
    border-style: none;
    font-size: 0.9rem;
}
.addContainer {
    float: right; /* 할일 추가 버튼이 표시될 위치 정의 */
    background: linear-gradient(to right, #6478FB, #8763FB);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
    }
.addBtn {
    color: white;
    vertical-align: midlle; /* 할일 추가 아이콘의 수직 정렬 정의 */
}
</style>
