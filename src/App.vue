<template>
  <div id="app">
    <h1>Aplikasi Management Tugas</h1>
    <footer>&copy;Betralino</footer>
    <div class="input-container">
      <input type="text" v-model="newTask" placeholder="Tambahkan tugasmu" />
      <button @click="addTask" class="addTask">Tambah</button>
    </div>
    <div class="list-container">
      <ol>
        <fieldset>
          <legend style="text-align: center;">List Tugas</legend>
          <li v-for="(task, index) in filteredTasks" :key="index">
            <span :class="{ 'completed': task.completed }">{{ task.name }}</span>
            <div class="button-container">
              <button @click="toggleTask(index)">
                {{ task.completed ? 'Batal' : 'Selesai' }}
              </button>
              <button @click="removeTask(index)">Hapus</button>
            </div>
          </li>
        </fieldset>
      </ol>
    </div>
    <button class="buttonshow" @click="showOnlyCompleted = !showOnlyCompleted">
      {{ showOnlyCompleted ? 'ShowNotCompleted' : 'Show Completed' }}
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: [],
      newTask: '',
      showOnlyCompleted: false
    };
  },
  computed: {
    filteredTasks() {
      if (this.showOnlyCompleted) {
        return this.tasks.filter(task => task.completed);
      } else {
        return this.tasks;
      }
    }
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push({
          name: this.newTask,
          completed: false
        });
        this.newTask = '';
      }
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },
    toggleTask(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
    }
  }
};
</script>

<style scoped>
#app {
  background-color: #333;
  margin: auto;
  padding: 10px;
  max-width: 700px;
  display: flex;
  flex-direction: column;
  align-items: center; /* Mengatur posisi elemen secara horizontal (horizontal alignment) menjadi tengah */
  justify-content: center; /* Mengatur posisi elemen secara vertikal (vertical alignment) menjadi tengah */
  min-height: 100vh; /* Menyediakan tinggi minimum sesuai dengan tinggi viewport untuk memastikan konten tetap di tengah saat konten sedikit */
}

#app h1 {
  text-align: center;
  color: white;
  font-family: 'Courier New', Courier, monospace;
}

#app footer{
  color: white;
}

.input-container {
  text-align: center;
  margin-bottom: 10px;
}

#app input[type=text] {
  height: 40px;
  width: 200px;
  border-radius: 10px;
  font-family:monospace;
  padding-right: 5px;
}

#app .addTask{
  height: 50px;
  width: 60px;
  background-color: turquoise;
  border-radius: 10px;
  margin: 10px;
}


#app ol {
  list-style-type:armenian;
  padding: 0;
  margin: 0;
}

#app li {
  padding: 5px;
  align-items: center;
  display: flex;
  color: white;
}

.completed {
  text-decoration: line-through;
  color: red;
}

#app .buttonshow{
  height: 40px;
  background-color: aquamarine;
  border-radius: 5px;
}

#app .list-container button{
  margin: 5px;
  height: 40px;
  background-color: aqua;
}

#app .list-container{
}
</style>
