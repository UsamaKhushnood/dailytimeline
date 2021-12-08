<template>
  <div class="home container-fluid">
    <div class="row timeline">
      <div class="col-md-6 right-border">
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
            <div class="input-group w-75 mx-auto mb-0">
              <input
                type="text"
                class="form-control"
                placeholder="...new_task"
                aria-label="Recipient's username"
                aria-describedby="button-addon2"
                v-model="newTodo"
                @keyup.enter="addNewToList"
              />
              <button
                class="btn btn-outline-primary"
                type="button"
                id="button-addon2"
                style="border-radius: 0 4px 4px 0;"
                @click="addNewToList"
              >
                Add
              </button>
            </div>
            <div class="w-75 mx-auto mt-1">
              <p class="font-weight-lighter f-12">
                <span class="font-weight-bolder yellow">Pro Tip:</span> Hit
                Enter to Add Task.
              </p>
            </div>
          </div>
          <div class="col-md-12 mt-3 container timelineOverflow">
            <div v-if="toDoList.length !== 0">
              <div class="mt-3" v-for="(todo, index) in toDoList" :key="index">
                <div class="row">
                  <div class="col-md-11">
                    <TodayTimeline
                      :title="todo.title"
                      @stopTime="consoleThis"
                      @currentlyStart="setCurrentlyStart"
                      :index="index"
                      ref="timerRef"
                    />
                  </div>
                  <div class="col-md-1 p-0 align-items-center d-flex">
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
            </div>
            <div class="noTask" v-else>
              <div class="text-center w-100">
                <img
                  src="@/assets/icons/no-task.png"
                  width="150px"
                  class="mb-4"
                  style="margin-left: 30px;"
                />
                <p class="mb-0 text-capitalize yellow">
                  Get a clear view of the day ahead
                </p>
                <p class="text-muted">
                  All your tasks that are due today will show up here.
                </p>
              </div>
            </div>
          </div>
          <div class="position-relative w-100" v-if="toDoList.length !== 0">
            <div class="d-flex justify-content-end px-4 mt-5">
              <button
                class="btn btn-primary mt-3 mr-2"
                @click="saveTodaysProgress"
              >
                Check In
              </button>
              <button class="btn btn-primary mt-3 " @click="saveTodaysProgress">
                Save Today's Progress
              </button>
            </div>
          </div>
        </div>
      </div>
      <div class="col-md-6 ">
        <div class="row">
          <div class="col-md-12 bottom-border">
            <h1 class="text-center yellow">Notes</h1>
          </div>
          <div class="col-md-12 mt-3">
            <!-- code goes here  -->
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
// import Records from "@/components/Records";
import TodayTimeline from "@/components/TodayTimeline";
export default {
  name: "Home",
  components: { TodayTimeline },
  data: () => ({
    addNew: true,
    newTodo: null,
    isActiveTask: null,
    currentlyStart: null,
    toDoList: [
      { title: "Study", undo: false },
      { title: "Work", undo: false },
      { title: "Gaming", undo: false },
    ],
  }),
  methods: {
    addNewToList() {
      if (this.newTodo == null || this.newTodo.trim() === "") {
        return;
      }
      this.toDoList.push({ title: this.newTodo, undo: false });
      this.newTodo = null;
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
    setCurrentlyStart(id) {
      this.currentlyStart = id;
    },
    stopOther(oldTimerIndex) {
      if (oldTimerIndex === null) {
        return;
      }
      this.$refs.timerRef[oldTimerIndex].stop();
    },
  },
  computed: {},
  watch: {
    currentlyStart(newVal, oldVal) {
      console.log("watchers magic", "new value:", newVal, "old value:", oldVal);
      this.stopOther(oldVal);
    },
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

.noTask {
  height: 250px;
  display: flex;
  align-items: center;
  justify-items: center;
}

.timelineOverflow {
  max-height: calc(100vh - 400px);
  overflow-y: auto;
}
</style>
