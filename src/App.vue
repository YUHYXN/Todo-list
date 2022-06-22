<template>
  <div class="container">
    <h2 class="name">To-Do List</h2>
    <form @submit.prevent="onSubmit">
      <!-- submit 뒤에 .prevent 를 이벤트 모디파이라고 부름 -->
      <div class="d-flex">
        <div class="flex-grow-1 mr-2">
          <!--  v-bind: 이걸 그냥 : 로 생략할 수 있다 -->
          <!-- <div v-bind:class="nameClass">{{ name }}</div> -->
          <input class="form-control" type="text" v-model="todo" placeholder="Type new to-do" />
        </div>
        <div>
          <button class="btn btn-primary" type="submit">Add</button>
          <!-- v-on: 이건 @ 이거랑 똑같으니까 v-on:click = @click 으로 생략 가능하다. -->
        </div>
      </div>
      <div v-show="hasError" style="color: red">This field cannot be empty</div>
    </form>
    <!-- v-for를 사용할 땐 key 바인딩을 꼭 사용해줘야 한다. -->
    <div class="card mt-2" v-for="todo in todos" :key="todo.id">
      <div class="card-body p-2">
        <div class="form-check">
          <input type="checkbox" class="form-check-input" v-model="todo.completed" />
          <label class="form-check-label" for="">{{ todo.subject }}</label>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import {ref} from "vue"

export default {
  setup() {
    const todo = ref("")
    const todos = ref([
      // {id: 1, subject: "노트북 팔기"},
      // {id: 2, subject: "노트북 사기"}
    ])
    const hasError = ref(false)
    // const type = ref("number")
    // const nameClass = ref("name")
    // ref 안에는 {}이 들어가도되고 숫자가 들어가도된다.

    // const greeting = (name) => {
    //   return "Hello, " + name
    // }

    // const greet = greeting(name)
    const onSubmit = () => {
      if (todo.value === "") {
        hasError.value = true
      } else {
        // e.preventDefault()
        // name.value = "CODER"
        // type.value = "text"
        // // ref를 사용하면 보통 .value를 붙여서 사용한다 (숫자,스트링), 단 {} 오브젝트나 []어레이를 사용할때는 리액티브 reactive를 임폴트해서 사용한다.
        // // import {reactive} from "vue"
        // // const name = reactive ({ id : 1 })
        // // name.id = 2; 뭐 이런식으로 사용 가능하다. 근데 ref를 쓰려면 name.value.id 로 해야한다.
        todos.value.push({
          id: Date.now(),
          subject: todo.value,
          completed: false
        })
        hasError.value = false
      }
    }

    return {
      todo,
      todos,
      onSubmit,
      hasError
    }
  }
}
</script>

<style>
.name {
  color: blue;
  font-size: 2rem;
  font-weight: 600;
}
</style>
