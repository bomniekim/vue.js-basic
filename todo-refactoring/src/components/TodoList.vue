<template>
  <div>
    <!-- name: css와 연관된 속성 / tag: html 태그 의미 -->
    <transition-group name="list" tag="ul">
      <span v-for="item in items" v-bind:key="item" class="list-item">{{ item }}</span>

      <!-- presentational component -->
      <!-- vscode에서는 v-for 사용 시 v-bind:key 설정 요구 -->
      <li v-for="(item, index) in propsdata" v-bind:key="item.value" class="shadow">
        <i
          class="checkBtn fas fa-check"
          v-bind:class="{ checkBtnCompleted: item.completed }"
          v-on:click="toggleComplete(item, index)"
        ></i>
        <span v-bind:class="{ textCompleted: item.completed }">
          {{
          item.value
          }}
        </span>
        <!-- v-bind를 통해 엘리먼트의 속성을 동적으로 설정 -->
        <!-- ex) 이 예시에서는 boolean의 값에 따라 클래스가 추가 or 배제 -->
        <span class="removeBtn" v-on:click="removeTodo(item, index)">
          <i class="far fa-trash-alt"></i>
        </span>
      </li>
    </transition-group>
  </div>
</template>

<script>
export default {
  props: ["propsdata"],
  methods: {
    removeTodo: function(item, index) {
      this.$emit("removeTodoItem", item, index);
    },
    toggleComplete: function(item, index) {
      this.$emit("toggleTodoItem", item, index);
    }
  }
};
</script>

<style scoped>
ul {
  list-style-type: none;
  padding-right: 0px;
  margin-top: 0;
  text-align: left;
}

li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}
.removeBtn {
  margin-left: auto;
  color: tomato;
}
.checkBtn {
  line-height: 45px;
  color: #62acde;
  margin-right: 5px;
}

.checkBtnCompleted {
  color: #b3adad;
}

.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}

/* 리스트 아이템 transition 효과 */
.list-enter-active,
.list-leave-active {
  transition: all 1s;
}
.list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
  opacity: 0;
  transform: translateY(30px);
}
</style>
