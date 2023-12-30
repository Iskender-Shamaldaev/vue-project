<template>
  <div class="div">
    <v-popup
        v-if="isInfoPopupVisible"
        @onClose="closeInfoPopup"
    />


    <h3>Сеанс гемодиализа</h3>
    <p>No месяце:<span> 4 </span></p>
  </div>
  <h3> Назначения сеанса гемодиализа</h3>
  <p>Программа аппарата</p>
  <div>
    <button>HD</button>
    <button>HDF</button>
    <button>UF</button>
  </div>
  <p>Диализатор</p>
  <div>
    <button>Спр. "Диализаторы"</button>
    <button class="material-icons" @click="showPopup">menu_open</button>
  </div>
  <p>Концентратор</p>
  <div>
    <button>Спр. "Концентраторы"</button>
    <button class="material-icons">menu_open</button>
    <button>10 л.</button>
  </div>
  <p>Тип инъекции</p>
  <div>
    <button>Игла</button>
    <button>Катетер</button>
  </div>
  <div>
    <button>Спр. "Иглы"</button>
    <button class="material-icons">menu_open</button>
    <button>Спр. "Типы иглы"</button>
    <button class="material-icons">menu_open</button>
  </div>
  <div>
    <button>Спр. "Катетеры"</button>
    <button class="material-icons">menu_open</button>
    <button>Спр. "Типы катетеров"</button>
    <button class="material-icons">menu_open</button>
  </div>
</template>

<script lang="ts">
import vPopup from '../components/popup/v-popup.vue'

export default {
  name: 'hemodialysisSession',
  components: {
    vPopup
  },
  data() {
    return {
      isInfoPopupVisible: false
    }
  },
  methods: {
    showPopup() {
      this.isInfoPopupVisible = true
    },
    closeInfoPopup() {
      this.isInfoPopupVisible = false
    },
  },
}
</script>

<style scoped>
.div {
  display: flex;
  align-items: center;
  justify-content: space-around;
}
</style>