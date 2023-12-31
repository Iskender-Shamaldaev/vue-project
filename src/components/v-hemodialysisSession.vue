<template>
  <div class="div">
    <v-popup v-if="isInfoPopupVisible" @onClose="closeInfoPopup" />

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

  <div>
    <div>
      <span>Бикарбонат</span>
      <span>Сухой Вес</span>
      <span>Антикоагуляция</span>
      <span>Объем</span>
    </div>

    <div>
      <button>ХХХгр/л</button>
      <button class="material-icons">menu_open</button>
      <button>ХХХ кг</button>
      <button>Наименование</button>
      <button class="material-icons">menu_open</button>
      <button>ХХХ ед</button>
    </div>
  </div>

  <div>
    <button>Сформировать сеанс</button>
  </div>

  <div class="appointment">
    <h4>Назначения сеанса гемодиализа</h4>
    <div>
      <span> - Программа</span>
      <span>- Диализатор</span>
    </div>

    <div>
      <span> <span></span> - Концентратор Объём</span>
      <span>- Игла/Катетер</span>
      <span>Бикарбонат мл</span>
    </div>

    <div>
      <span> <span></span>- Антикоагуляция ед.</span>
      <span>Сухой вес кг.</span>
    </div>
  </div>

  <h4>Назначения сеанса гемодиализа</h4>
  <span>Лекарственный препарат</span>

  <div>
    <button>Спр. "Препараты"</button>
    <button class="material-icons">menu_open</button>
  </div>

  <div>
    <div>
      <span>Путь приема</span>
      <span>Дозировка</span>
    </div>

    <div>
      <button>Спр. "Путь приема"</button>
      <button>Спр. "Дозы препаратов"</button>
      <button class="material-icons">menu_open</button>
    </div>
  </div>

  <p>Номера сеансов:</p>
  <div>
    <button v-for="number in [1, 2, 3, 4, 5, 6, 7]" :key="number">{{ number }}</button>
  </div>

  <div>
    <div>
      <span>Начало приёма</span>
      <span>Конец приёма</span>
    </div>

    <div>
      <button>DD.MM.YYYY</button>
      <button>DD.MM.YYYY</button>
    </div>
  </div>

  <button>Сформировать</button>
  <p>Список назначений после сеансов</p>
  <v-table :data="yourData" @delete-row="deleteRow" />
</template>

<script lang="ts">
import vPopup from './v-popup.vue'
import vTable from './v-table.vue'

export default {
  name: 'hemodialysisSession',
  components: {
    vPopup,
    vTable
  },
  data() {
    return {
      isInfoPopupVisible: false,
      yourData: [
        {
          name: 'Лекарственный препарат No1', reception: 'Перорально',
          dosage: '20мг', start: 'DD.MM.YYYY', end: 'DD.MM.YYYY', number: 1, days: 3
        },
        {
          name: 'Лекарственный препарат No2', reception: 'Внутривенно',
          dosage: "150мл", start: 'DD.MM.YYYY', end: 'DD.MM.YYYY', number: 5, days: 1
        },
        {
          name: 'Лекарственный препарат No3', reception: 'Перорально',
          dosage: '20мг', start: 'DD.MM.YYYY', end: 'DD.MM.YYYY', number: 6, days: 2
        }
      ],
    }
  },
  methods: {
    showPopup() {
      this.isInfoPopupVisible = true
    },
    closeInfoPopup() {
      this.isInfoPopupVisible = false
    },
    deleteRow(number: number) {
      this.yourData = this.yourData.filter(item => item.number !== number);
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

.appointment {
  border: 1px solid black;
  width: 500px;
}
</style>
