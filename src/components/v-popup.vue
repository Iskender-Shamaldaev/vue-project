<template>
  <div class="popup_wrapper" ref="popup_wrapper">
    <div class="v-popup">

      <div class="v-popup__header">
        <strong>Лекарственные препараты</strong>
        <button class="close_modal btn" @click="onClosePopup">Закрыть</button>
      </div>

      <div class="v-popup__content">
        <slot></slot>
        <form>
          <div class="search">
            <input placeholder="Search by first characters">
            <button style="margin-left: 27px" class="material-icons">search</button>
          </div>

          <div class="add-entry">
            <input placeholder="Add a new entry">
            <button style="margin-left: 27px" class="material-icons">add</button>
          </div>

          <div class="needle-sizes">
            <div style="display: flex; align-items: center">
              <input placeholder="Needle size No1">
              <button class="material-icons">delete</button>
              <button class="material-icons">chevron_right</button>
            </div>

            <div style="display: flex; align-items: center">
              <input placeholder="Needle size No2">
              <button class="material-icons">delete</button>
              <button class="material-icons">chevron_right</button>
            </div>

            <div style="display: flex; align-items: center">
              <input placeholder="Needle size No3">
              <button class="material-icons">delete</button>
              <button class="material-icons">chevron_right</button>
            </div>

            <div style="display: flex; align-items: center">
              <input placeholder="Needle size No4">
              <button class="material-icons">delete</button>
              <button class="material-icons">chevron_right</button>
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
export default {
  name: "v-popup",
  props: {
    onClose: Function,
  },
  data() {
    return {}
  },
  methods: {
    onClosePopup() {
      this.$emit('onClose')
    },
  },
  mounted() {
    let vm = this;
    document.addEventListener('click', function (item) {
      if (item.target === vm.$refs['popup_wrapper']) {
        vm.onClosePopup();
      }
    })
  },
}

</script>

<style lang="scss" scoped>
.popup_wrapper {
  background: rgba(64, 64, 64, .4);
  display: flex;
  justify-content: center;
  position: absolute;
  right: 0;
  left: 0;
  bottom: 0;
  top: 0;
}

.v-popup {
  padding: 16px;
  position: fixed;
  top: 50px;
  width: 400px;
  border: 1px solid #9e9c9c;
  background: #ffffff;
  box-shadow: 0 0 17px 0 #e7e7e7;
  z-index: 10;

  &__header {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: flex-start;
  }

  &__content {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  form {
    margin-top: 20px;
  }

  .search,
  .add-entry, {
    margin-bottom: 15px;
    display: flex;
    align-items: center;
  }

  .needle-sizes {
    display: flex;
    flex-direction: column;
    margin-bottom: 15px;
  }

  input {
    padding: 5px;
    width: 300px;
  }
}
</style>