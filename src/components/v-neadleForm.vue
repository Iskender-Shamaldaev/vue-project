<template>
  <form>
    <div class="search">
      <input placeholder="Поиск позиции по первым символам">
      <button style="margin-left: 37px" class="material-icons">search</button>
    </div>

    <div class="add-entry">
      <input placeholder="Добавить новую запись">
      <button style="margin-left: 37px" class="material-icons">add</button>
    </div>

    <div class="needle-sizes">
      <div v-for="(placeholder, index) in needlePlaceholders" :key="index" style="display: flex; align-items: center">
        <span class="placeholder">{{ placeholder }}</span>
        <button class="material-icons">delete</button>
        <button class="material-icons">chevron_right</button>
      </div>
    </div>
  </form>
</template>

<script>
export default {
  props: {
    needlePlaceholders: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
form {
  margin-top: 20px;
}

.search,
.add-entry {
  margin-bottom: 15px;
  display: flex;
  align-items: center;
}

.needle-sizes {
  display: flex;
  flex-direction: column;
  margin-bottom: 15px;

  div {
    display: flex;
    align-items: center;
  }

  .placeholder {
    width: 300px;
    padding: 5px;
    border: 1px solid #ccc;
    margin-right: 10px;
  }
}

input {
  padding: 5px;
  width: 300px;
}
</style>
