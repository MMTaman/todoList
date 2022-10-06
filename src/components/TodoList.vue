<template>
      <div class="container">
            <div class="card">
                  <div class="box">
                        <h1>Todo App</h1>
                        <div class="data">
                              <input
                                    type="text"
                                    placeholder="What's Up!"
                                    v-model="onetask"
                              />
                              <button @click="adding">&plus;</button>
                        </div>
                        <table>
                              <tr
                                    v-for="(task, index) in tasks"
                                    :key="index"
                                    @click="task.stat = !task.stat"
                              >
                                    <td
                                          class="name"
                                          :class="{
                                                finished: task.stat === true,
                                          }"
                                    >
                                          {{ task.main }}
                                    </td>
                                    <td class="right">
                                          <label>
                                                <button
                                                      @click="deleting(index)"
                                                >
                                                      &minus;
                                                </button>
                                          </label>
                                          <input
                                                type="checkbox"
                                                class="checker"
                                                v-if="task.stat === true"
                                                checked
                                          />
                                          <input
                                                type="checkbox"
                                                class="checker"
                                                v-else-if="task.stat === false"
                                          />
                                    </td>
                              </tr>
                        </table>
                  </div>
            </div>
      </div>
</template>

<script>
export default {
      name: "TodoList",
      mounted() {
            this.tasks.splice(0, 1);
      },
      data() {
            return {
                  onetask: "",
                  tasks: [{}],
            };
      },
      methods: {
            adding() {
                  if (this.onetask.length === 0) return;

                  this.tasks.push({
                        main: this.onetask,
                        stat: false,
                  });
                  this.onetask = "";
            },
            deleting(index) {
                  this.tasks.splice(index, 1);
            },
      },
};
</script>

<style scoped lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;700;800&display=swap");
* {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: "Poppins", sans-serif;
}

body {
      display: flex;
      justify-content: center;
      align-items: center;
      flex-wrap: wrap;
      min-height: 100vh;
}

body .container {
      display: flex;
      justify-content: center;
      align-items: center;
      flex-wrap: wrap;
      max-width: 1200px;
}

body .container .card {
      position: relative;
      min-width: 440px;
      height: 520px;
      box-shadow: inset 5px 5px 5px rgba(0, 0, 0, 0.2),
            inset -5px -5px 15px rgba(255, 255, 255, 0.1),
            5px 5px 15px rgba(0, 0, 0, 0.3),
            -5px -5px 15px rgba(255, 255, 255, 0.1);
      border-radius: 15px;
      margin: 20px;
      transition: 0.5s;
}

body .container .card .box {
      position: absolute;
      top: 20px;
      left: 20px;
      right: 20px;
      bottom: 20px;
      background: #2d0320;
      border-radius: 15px;
      display: flex;
      flex-direction: column;
      align-items: center;
      overflow: hidden;
}

body .container .card .box .content {
      padding: 20px;
      text-align: center;
}

.data {
      display: flex;
      flex-direction: row;
      align-items: center;
}

table {
      border-collapse: collapse;
      width: -webkit-fill-available;
      margin: 20px;
      table-layout: fixed;
}

tr {
      display: flex;
      flex-direction: row;
      justify-content: space-between;
      padding: 8px;
      margin: 8px;
      border-radius: 8px;
      background-color: #eeeeee;
      cursor: pointer;
}

.name {
      padding: 2px;
}
.right {
      display: flex;
      flex-direction: row;
      align-items: center;
}
input {
      border: none;
      background: #eeeeee;
      padding: 8px;
      margin-right: 8px;
      border-radius: 5px;
}

input:focus {
      outline: 2px #cd5d67 solid;
      border-radius: 5px;
}

button {
      position: relative;
      background-color: #cd5d67;
      border: none;
      border-radius: 50%;
      padding: 15px;
      margin: 10px;
      width: 50px;
      height: 50px;
      font-size: 18px;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      box-shadow: 0 10px 10px rgba(0, 0, 0, 0.1);
      cursor: pointer;
      transition: all 0.2s cubic-bezier(0.68, -0.55, 0.265, 1.55);
      font-size: 3rem;
}

button:hover {
      background-color: #eeeeee;
      color: #2d0320;
}

.right button {
      width: 10px;
      height: 10px;
      font-size: 1.5rem;
      margin: 0 25px 0 0;
}

.checker {
      // -webkit-appearance: none;
      width: 1.25rem;
      height: 1.25rem;
      border: 1px solid hsl(0, 0%, 85%);
      border-radius: 1px;
      vertical-align: sub;
      outline: none;

      &:checked {
            background-color: hsl(0, 0%, 40%);
            border-color: hsl(0, 0%, 40%);

            & + label {
                  text-decoration: line-through;
                  color: hsl(0, 0%, 70%);
                  font-weight: 600;
                  background-color: hsl(0, 0%, 97%);
            }

            tr:focus &,
            tr:hover & {
                  box-shadow: 0 0 0 3px hsl(0, 0%, 85%);
                  border-color: hsl(0, 0%, 40%);
            }
      }
}

.finished {
      text-decoration: line-through;
}
</style>
