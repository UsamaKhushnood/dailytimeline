<template>
  <div class="home container-fluid">
    <div class="row timeline">
      <div class="col-md-6 right-border">
        <div class="row">
          <div class="col-md-12 bottom-border">
            <h1 class="text-center blue">Records</h1>
          </div>
          <div class="col-md-12 mt-3">
            <Records />
          </div>
        </div>
      </div>
      <div class="col-md-6">
        <div class="row">
          <div class="col-md-12 bottom-border">
            <h1 class="text-center yellow">Today's Timeline</h1>
            <div
              class="plusicon"
              :class="{ rotate: addNew }"
              @click="addNew = !addNew"
            >
              <b-icon icon="plus"></b-icon>
            </div>
          </div>
          <div class="col-md-12 mt-3 container " v-show="addNew">
            <div class="input-group mb-3 w-75 mx-auto">
              <input
                type="text"
                class="form-control"
                placeholder="Add Something..."
                aria-label="Recipient's username"
                aria-describedby="button-addon2"
                v-model="newTodo"
                @keyup.enter="addNewToList"
              />
              <button
                class="btn btn-outline-primary"
                type="button"
                id="button-addon2"
                @click="addNewToList"
              >
                Add New Todo
              </button>
            </div>
          </div>
          <div class="col-md-12 mt-3 container">
            <div class="mt-3" v-for="(todo, index) in toDoList" :key="index">
              <div class="row">
                <div class="col-md-11">
                  <TodayTimeline :title="todo.title" @stopTime="consoleThis" ref="jdfklsjfklsfs"/>
                  <button @click="testingRef(index)">ref</button>
                </div>
                <div class="col-md-1 p-0">
                  <button
                    type="button"
                    class="btn btn-sm btn-outline-danger"
                    @click="del(index)"
                  >
                    <b-icon icon="trash-fill" aria-hidden="true"></b-icon>
                  </button>
                </div>
              </div>
            </div>
            <div class="text-center mt-5">
              <button
                class="btn btn-outline-success w-75 mx-auto"
                @click="saveTodaysProgress"
              >
                Save Today's progress
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Records from "@/components/Records";
import TodayTimeline from "@/components/TodayTimeline";
export default {
  name: "Home",
  components: { Records, TodayTimeline },
  data: () => ({
    addNew: false,
    newTodo: "",
    toDoList: [
      { title: "Study", undo: false },
      { title: "Work", undo: false },
      { title: "Gaming", undo: false },
    ],
  }),
  methods: {
    addNewToList() {
      this.toDoList.push({title: this.newTodo, undo: false });
      this.newTodo = "";
    },
    del(index) {
      this.toDoList.splice(index, 1);
    },
    saveTodaysProgress() {
      console.log(this.time);
    },
    consoleThis(title, time, running) {
      console.log(title, time, running);
    },
    testingRef(index) {
      this.$refs.jdfklsjfklsfs[index].start()
      console.log(this.$refs.jdfklsjfklsfs[index].start())
    }
  },
};
</script>

<style scoped>
.plusicon {
  position: absolute;
  right: 40px;
  top: 0;
  font-size: 30px;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.plusicon svg {
  transition: all 0.3s ease-in;
}

.plusicon.rotate svg {
  transform: rotate(315deg);
}
</style>
