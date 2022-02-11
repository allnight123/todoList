<template>
  <v-container>
    <v-layout row wrap>
      <v-flex xs12 text-xs-center>
        <h1>투두 리스트</h1>
        <p>
          전체할일 : {{ todoList.length }} / 완료된 할일: {{ countDone }} / 남은
          할일: {{ todoList.length - countDone }}
        </p>
      </v-flex>
      <v-flex xs6 pa-2>
        <List
          :todoList="todoList"
          @statusControl="statusControl"
          @listDelete="listDelete"
        />
      </v-flex>
      <v-flex xs6 pa-2>
        <ListAdd 
          @listAdd="listAdd" 
          @listEdit="listEdit" 
        />
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import List from "./List";
import ListAdd from "./ListAdd";

export default {
  components: {
    List,
    ListAdd,
  },

  data() {
    return {
      todoList: [],
    };
  },
  computed: {
    countDone() {
      let count = 0;
      this.todoList.forEach((list) => {
        if (list.status === "done") count++;
      });
      return count;
    },
  },

  methods: {
    listAdd(memo) {
      console.log("받았어!");
      this.todoList.push({ memo: memo, status: "created" });
    },

    listEdit(memo, index) {
      console.log("수정할거 받았어!");
      this.todoList[index].memo = memo;
    },

    statusControl(index, status) {
      console.log(index, status);
      this.todoList[index].status = status;
    },

    listDelete(index) {
      this.todoList.splice(index, 1);
      //                   번호,갯수
      //            splice는 지우는 명령어
      //                        갯수의 숫자가 2 라면 인덱스 번호로 부터 2개를 삭제한다.
    },
  },
};
</script>