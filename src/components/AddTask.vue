<template>
  <form @submit="onSubmit" class="add-form">
    <div class="from-control">
      <label>Task</label>
      <input
        type="text"
        v-model="text"
        name="text"
        placeholder="Ajouter une tâche"
      />
    </div>
    <div class="from-control">
      <label>Date et heure</label>
      <input
        type="text"
        v-model="day"
        name="day"
        placeholder="Ajouter la date et l'heure"
      />
    </div>
    <div class="from-control from-control-check">
      <label>Définir un rappel</label>
      <input type="checkbox" v-model="reminder" name="reminder" />
    </div>
    <input type="submit" value="Enregistrer" class="btn btn-block" />
  </form>
</template>

<script>
export default {
  name: "AddTask",
  data() {
    return {
      text: "",
      day: "",
      reminder: false,
    };
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();
      if (!this.text) {
        alert("Ajouter une tâche SVP !");
        return;
      }
      const newTask = {
        // id: Math.floor(Math.random() * 100000),
        text: this.text,
        day: this.day,
        reminder: this.reminder,
      };
      this.$emit("add-task", newTask);
      this.text = "";
      this.day = "";
      this.reminder = false;
    },
  },
};
</script>

<style lang="scss" scoped>
.add-form {
  margin-bottom: 40px;
  .from-control {
    margin: 20px 0;
    label {
      display: block;
    }
    input {
      width: 100%;
      height: 40px;
      margin: 5px;
      padding: 3px 7px;
      font-size: 17px;
    }
    &.from-control-check {
      display: flex;
      align-items: center;
      justify-content: space-between;
      label {
        flex: 1;
      }
      input {
        flex: 2;
        height: 20px;
      }
    }
  }
}
</style>
