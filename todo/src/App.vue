<template>
  <div id="app">
    <div class="container">
      <div class = "col-md-6 offset-md-3"> <!--input 태그 사이즈 변경-->
        <h1 class="text-center mb-4">Todo 어플리케이션</h1>
        <input type="text" class="form-control mb-4" v-model="userInput" @keyup.enter="addNewTodo"> <!--mb는 마진 값-->
        
        <div class="list-group mb-4" >
          <template v-for="todo in activeTodoList"> <!--state값이 active인 항목만 넘겨줌-->
            <Todo :key="todo"
              :label="todo.label"
              @componentClick="toggleTodoState(todo)"
            />
          </template>
        </div>
          <!-- <button class="list-group-item text-left" v-for="todo in todoList" :key="todo" @click="toggleTodoState(todo)"> 2.2.0 버전 이상부터 v-for 사용할 때, key 값이 요구
            {{ todo }}
          </button> 위에서 글의 for 가시성을 위해 template을 이용해서 쓴거 -->
        <div class="text-right">
          <button type="button" class="btn btn-sm" @click="changeCurrentState('active')">할 일</button>
          <button type="button" class="btn btn-sm" @click="changeCurrentState('done')">완료</button>
          <button type="button" class="btn btn-sm" @click="changeCurrentState('all')">전체</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Todo from './components/Todo';

export default {
  name: 'app',
  data() {
    return {
      userInput: '',
      todoList: [],
      currentState: 'active'
    };
  },
  computed:{ // computed는 클래스의 getter 함수처럼 동작한다
    activeTodoList(){
      return this.todoList.filter(todo => this.currentState === 'all' || todo.state === this.currentState); // current sate값이 all인 경우나 동일한 항목만 가져옴
    }
  },
  methods: {
    changeCurrentState(state){
      this.currentState = state;
    },
    addNewTodo() {
      this.todoList.push({
        label: this.userInput,
        state: 'active'
      });
      this.userInput = '';
    },
    toggleTodoState(todo){
      todo.state = todo.state === 'active' ? 'done' : 'active';
    }
  },
  components: {
    Todo
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
