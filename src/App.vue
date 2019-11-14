<template lang="html">
  <div class="container">
    <div class="row pt-5 pb-5">
      <div class="col-8">
        <h2>{{ title }}</h2>
      </div>
    </div>
    <div class="row">
      <div class="col-8">
        <div class="input-group mb-3">
          <input @keyup.enter="addTask()" v-model="formInput" type="text" class="form-control" aria-label="Recipient's username" aria-describedby="basic-addon2">
          <div class="input-group-append">
            <button @click="addTask()" class="btn btn-outline-secondary" type="button">
              Создать
            </button>
          </div>
        </div>
      </div>
    </div>
    <div v-for="(value, index) in tasks" v-bind:key="index" class="row pt-3">
      <div class="col-8">
        <div :class="value.state ? 'alert alert-success' : 'alert alert-warning' ">
          <div class="row">
            <div class="col-3 text-left">
              <i @click="editTask(index)" class="far fa-edit fa-2x"></i>
            </div>
            <div class="col-6 text-truncate" :style="value.state ? 'text-decoration: line-through' : null">
              {{ value.data }}
            </div>
            <div class="col-3 text-right">
              <i @click="deleteTask(index)" class="far fa-trash-alt fa-2x mr-2"></i>
              <i @click="checkTask(index)" class="far fa-check-square fa-2x ml-2"></i>
            </div>
          </div>
          <div v-if="value.edited" class="row p-4">
            <div class="col-12">
              <div class="input-group mb-3">
                <input v-on:input="editInput=$event.target.value" @keyup.enter="editTask(index)" type="text" class="form-control" aria-describedby="basic-addon2">
                <div class="input-group-append">
                  <button @click="editTask(index)" class="btn btn-outline-secondary" type="button">
                    Сохранить
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: 'My cool task manager',
      formInput: null,
      formInputEdited: null,
      tasks: []
    }
  },
  computed: {
    editInput: {
      get() {
        return this.formInputEdited;
      },
      set(val) {
        console.log(val);
        this.formInputEdited = val;
      }
    }
  },
  methods: {
    addTask() {
      this.tasks.push({
        data: this.formInput,
        state: false,
        edited: false,
      })
      this.formInput = null;
    },
    deleteTask(index) {
      this.tasks.splice(index, 1)
    },
    checkTask(index) {
      this.tasks[index].state = !this.tasks[index].state
    },
    editTask(index) {
      this.tasks[index].data = this.editInput;
      this.tasks[index].edited = !this.tasks[index].edited;
    }
  }
}
</script>

<style lang="css" scoped>
</style>
