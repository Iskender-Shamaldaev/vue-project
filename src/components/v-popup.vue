<template>
  <div class="popup_wrapper" ref="popup_wrapper">
    <div class="v-popup">

      <div class="v-popup__header">
        <span>Лекарственные препараты</span>
        <button class="close_modal" @click="onClosePopup">Закрыть</button>
      </div>

      <div class="v-popup__content">
        <slot></slot>
        <form>
          <input placeholder="Поиск позиции по первым символам">
          <button class="material-icons">search</button>
          <input placeholder="Добавить новую запись">
          <button class="material-icons">add</button>
          <input placeholder="Игла размер No1">
          <input placeholder="Игла размер No2">
          <input placeholder="Игла размер No3">
          <input placeholder="Игла размер No4">
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
    justify-content: space-between;
    align-items: center;
  }

  &__content {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
}
</style>