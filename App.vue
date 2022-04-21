<template>
  <div id="form">
    <span id="title">代辦事項</span>
    <ToDoList :todos="todos" :checkTodo="checkTodo" :deleteTodo="deleteTodo" :updateTodo="updateTodo"/>
    <ToDoFooter :addTodo="addTodo" />
  </div>
</template>

<script>
import ToDoList from "./components/ToDoList.vue";
import ToDoFooter from "./components/ToDoFooter.vue";

export default {
  name: "App",
  components: { ToDoList, ToDoFooter },
  data() {
    return {
      todos: [
        { id: "001", title: "洗碗", done: false },
        { id: "002", title: "拖地", done: false },
        { id: "003", title: "倒垃圾", done: false },
        { id: "004", title: "接小孩", done: false },
      ],
      selectedTodo: null
    };
  },
  methods: {
    // 新增一個todo
    addTodo(todoObj) {
      this.todos.unshift(todoObj);
    },
    // 勾選或取消勾選
    checkTodo(id) {
      this.todos.forEach((todo) => {
        if (todo.id === id) todo.done = !todo.done;
      });
      this.sortTodo();
      this.todos.sortTodo();
    },
    // 刪除
    deleteTodo(id){
      this.todos = this.todos.filter((todo)=>{
        return todo.id !== id
      })
    },
    // 更新
    updateTodo(id,title){
    this.todos.forEach((todo) => {
        if (todo.id === id) todo.title = title  
      })
    },
    // 排序
    sortTodo() {
      let newArray= this.todos;
      this.todos = newArray.sort((a,b)=> a.done - b.done);
    },
  }
};
</script>

<style >
#form {
  max-width: 550px;
  background-color: silver;
  border: solid 2px black;
  border-radius: 20px;
  margin: auto;
  text-align: center;
  padding: 20px 30px;
}
#title {
  text-align: center;
  font-size: 25px;
  display: block;
}
.btn {
  /* border-radius: 4px; */
  border: none;
  cursor: pointer;
  padding: 0px;
  font-size: 15px;
}
.yesno{
   margin-left: 10px;
  font-size: 15px;
  padding: 2px 3px !important; 
  float: right;
  }
</style>
