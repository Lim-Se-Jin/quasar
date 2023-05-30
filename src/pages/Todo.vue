<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-primary">
      <q-input
        v-model="newTask"
        @keyup.enter="addTask"
        class="col"
        bg-color="white"
        filled
        aria-placeholder="Add task"
        dense
        >
        <template v-slot:append>
          <q-btn @click="addTask" round dense flat icon="add"></q-btn>
        </template>
      </q-input>
    </div>

    <!--list-->
      <q-list class="bg-white" separator bordered>
       <q-item
        v-for="item in tasks"
        :key="item.title"
        @click="item.done = item.done == 'Y' ? 'N' : 'Y'"
        :class="{ 'done bg-blue-1': item.done == 'Y' }"
        v-ripple
        clickable
        >
        <q-item-section avatar>
          <q-checkbox
            v-model="item.done"
            color="primary"
            class="no-pointer-event"
            true-value="Y"
            false-value="N"
            dense
          ></q-checkbox>
      </q-item-section>
      <q-item-section>
        <q-item-label>{{ item.title }}</q-item-label>
      </q-item-section>
      <q-item-section v-if="item.done=='Y'" sied>
        <q-btn
          flat
          round
          dense
          color="primary"
          icon="edit"
          @click.stop="openDialog(item)"
        >
        </q-btn>
    </q-item-section>
    <q-item-section v-if="item.done == 'Y'" side>
      <q-btn
        flat
        round
        dense
        color="red"
        icon="delete"
        @click.stop="removeItem(item.id)"
      ></q-btn>
  </q-item-section>
    </q-item>
  </q-list>
  <dialog-custom ref="dialog" :edit-task="editTask" :origin="origin" @onInput="editTodo">
  </dialog-custom>
  </q-page>
</template>

<script>
import useTodoStore from '/src/stores/todo';
import { mapActions, mapState } from 'pinia';
import DialogCustom from "components/DialogCustom.vue"

export default{
  name:"Todo",
  title:"Todo list",
  components:{DialogCustom},
  data() {
    return {
      newTask: "",
      editTask:null,
      origin:null,
    };
  },
  mounted(){
    this.listTodo();
  },
  computed:{
    ...mapState(useTodoStore, ["tasks"])
  },
  methods:{
    ...mapActions(useTodoStore, ["insertTodo", "removeTodo","listTodo","editTodo"]),
    //추가
    async addTask(){
      if(this.newTask){
        //store action 저장
        this.insertTodo(this.newTask);
        await this.$q.notify({
          message:`${this.newTask} 추가하셨습니다`,
          icon:"home",
          color:"primary",
        });
      }else{
        await this.$q.notify({
          message:`내용은 필수입력입니다.`,
          icon:"warning",
          color:"red",
        });
        }
      },
      removeItem(id) {
          this.removeTodo(id);
          this.newTask="";
      },
      openDialog(item){
        this.$refs.dialog.dialog = true;
        this.editTask = item;
        this.origin = this.editTask.title;
      },
    },
  };
</script>

<style lang ="scss">
.done{
  .q-item_label{
    text-decoration: line-through;
    color: #bbb;
  }
}
.no-tasks{
  opacity: 0.5;
}
</style>
