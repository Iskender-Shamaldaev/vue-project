<template>
  <div class="session">
    <v-popup v-if="isInfoPopupVisible" @onClose="closeInfoPopup" :dynamicContent="needlePlaceholders">
      <div v-if="selectedContent === 'Типы иглы'">
        <vNeedleForm :needlePlaceholders="needlePlaceholders"></vNeedleForm>
      </div>

      <div v-if="selectedContent === 'Иглы'">
        <vNeedleForm :needlePlaceholders="needlePlaceholders2"></vNeedleForm>
      </div>

      <div v-if="selectedContent === 'Катетеры'">
        <vNeedleForm :needlePlaceholders="needlePlaceholders3"></vNeedleForm>
      </div>

      <div v-if="selectedContent === 'Препараты'">
        <vNeedleForm :needlePlaceholders="needlePlaceholders4"></vNeedleForm>
      </div>
    </v-popup>

    <v-generic-modal v-if="isInfoPopupVisible" @onClose="closeInfoPopup" :dynamicContent="genericPlaceholders">
      <div v-if="selectedContent === 'XXX'">
        <div class="needle-sizes">
          <div v-for="(placeholder, index) in genericPlaceholders" :key="index" style="display: flex; align-items: center">
            <span class="placeholder">{{ placeholder }}</span>
          </div>
        </div>
      </div>

      <div v-if="selectedContent === 'Типы катетеров'">
        <div class="needle-sizes">
          <div v-for="(placeholder, index) in genericPlaceholders2" :key="index" style="display: flex; align-items: center">
            <span class="placeholder">{{ placeholder }}</span>
          </div>
        </div>
      </div>

      <div v-if="selectedContent === 'Путь приема'">
        <div class="needle-sizes">
          <div v-for="(placeholder, index) in genericPlaceholders3" :key="index" style="display: flex; align-items: center">
            <span class="placeholder">{{ placeholder }}</span>
          </div>
        </div>
      </div>

      <div v-if="selectedContent === 'Дозы препаратов'">
        <div class="needle-sizes">
          <div v-for="(placeholder, index) in genericPlaceholders4" :key="index" style="display: flex; align-items: center">
            <span class="placeholder">{{ placeholder }}</span>
          </div>
        </div>
      </div>

      <div v-if="selectedContent === 'Кратность приёма'">
        <div class="needle-sizes">
          <div v-for="(placeholder, index) in genericPlaceholders5" :key="index" style="display: flex; align-items: center">
            <span class="placeholder">{{ placeholder }}</span>
          </div>
        </div>
      </div>

    </v-generic-modal>

    <h3 class="session__title">Сеанс гемодиализа</h3>
    <p>No месяце:<span class="blue"> 4 </span></p>
  </div>

  <h3 class="session__title"> Назначения сеанса гемодиализа</h3>
  <p>Программа аппарата</p>
  <div>
    <button
        class="btn"
        :class="{ 'selected': selectedProgram === 'HD' }"
        @click="selectProgram('HD')"
    >
      HD
    </button>
    <button
        class="btn"
        :class="{ 'selected': selectedProgram === 'HDF' }"
        @click="selectProgram('HDF')"
    >
      HDF
    </button>
    <button
        class="btn"
        :class="{ 'selected': selectedProgram === 'UF' }"
        @click="selectProgram('UF')"
    >
      UF
    </button>
  </div>

  <p>Диализатор</p>
  <div class="div">
    <button class="btn-1">Спр. "Диализаторы"</button>
    <button class="material-icons btn-2">menu_open</button>
  </div>

  <p>Концентратор</p>
  <div class="div">
    <button class="btn-1">Спр. "Концентраторы"</button>
    <button class="material-icons btn-2">menu_open</button>
    <button class="btn-3">10 л.</button>
  </div>

  <p>Тип инъекции</p>
  <div>
    <button
        class="btn"
        :class="{ 'selected': selectedInjection === 'Игла' }"
        @click="selectInjection('Игла')"
    >
      Игла
    </button>
    <button
        class="btn"
        :class="{ 'selected': selectedInjection === 'Катетер' }"
        @click="selectInjection('Катетер')"
    >
      Катетер
    </button>

  </div>

  <div class="div">
    <button class="btn-1">Спр. "Иглы"</button>
    <button class="material-icons btn-2" @click="showPopup('Иглы')">menu_open</button>
    <button class="btn-1">Спр. "Типы иглы"</button>
    <button class="material-icons btn-2" @click="showPopup('Типы иглы')">menu_open</button>
  </div>

  <div class="div">
    <button class="btn-1">Спр. "Катетеры"</button>
    <button class="material-icons btn-2" @click="showPopup('Катетеры')">menu_open</button>
    <button class="btn-1">Спр. "Типы катетеров"</button>
    <button class="material-icons btn-2" @click="showPopup('Типы катетеров')">menu_open</button>
  </div>

  <div>

    <div class="div">
      <div>
        <span>Бикарбонат</span>
        <div class="div">
          <button class="btn-3">ХХХгр/л</button>
          <button class="material-icons btn-2" @click="showPopup('XXX')">menu_open</button>
        </div>
      </div>

      <div>
        <p>Сухой Вес</p>
        <div class="div">
          <button class="btn-3">ХХХ кг</button>
        </div>
      </div>

      <div>
        <span>Антикоагуляция</span>
        <div class="div">
          <button class="btn-3">Наименование</button>
          <button class="material-icons btn-2">menu_open</button>
        </div>
      </div>

      <div>
        <p>Объем</p>
        <div class="div">
          <button class="btn-3">ХХХ ед</button>
        </div>
      </div>

    </div>
  </div>

  <div>
    <button class="btn">Сформировать сеанс</button>
  </div>

  <div class="appointment">
    <h4>Назначения сеанса гемодиализа</h4>
    <div style="display: flex">
      <div class="div">
        <span class="material-icons">tv</span>
        <span> -Программа: {{ selectedProgram }}</span>
      </div>

      <div class="div">
        <span class="material-icons">tv</span>
        <span> -Диализатор</span>
      </div>
    </div>

    <div style="display: flex">
      <div class="div">
        <span class="material-icons">tv</span>
        <span> -Концентратор Объём</span>
      </div>

      <div class="div">
        <span class="material-icons">tv</span>
        <span>: {{ selectedInjection }}</span>
      </div>

      <div class="div">
        <span class="material-icons">tv</span>
        <span>Бикарбонат мл</span>
      </div>

    </div>

    <div style="display: flex">
      <div class="div">
        <span class="material-icons">tv</span>
        <span>- Антикоагуляция ед.</span>
      </div>

      <div class="div">
        <span class="material-icons">tv</span>
        <span>Сухой вес кг.</span>
      </div>

    </div>
  </div>

  <h3 class="session__title">Назначения после сеанса</h3>
  <span>Лекарственный препарат</span>

  <div class="div">
    <button class="btn-1">Спр. "Препараты"</button>
    <button class="material-icons btn-2" @click="showPopup('Препараты')">menu_open</button>
  </div>

  <div>
    <div class="div">
      <div>
        <span>Путь приема</span>
        <div class="div">
          <button class="btn-1" @click="showPopup('Путь приема')">Путь приема</button>
        </div>
      </div>

      <div>
        <span>Дозировка</span>
        <div class="div">
          <button class="btn-1">Спр. "Дозы препаратов"</button>
          <button class="material-icons btn-2" @click="showPopup('Дозы препаратов')">menu_open</button>
        </div>
      </div>
    </div>
  </div>

  <p>Номера сеансов:</p>
  <div>
    <button class="btn-3" v-for="number in [1, 2, 3, 4, 5, 6, 7]" :key="number">{{ number }}</button>
  </div>

  <div class="div">
    <div style="display: flex">
      <div>
        <span>Начало приёма</span>
        <div class="div btn-3">
          <span>DD.MM.YYYY</span>
          <span class="material-icons">event</span>
        </div>
      </div>

      <div>
        <span>Конец приёма</span>
        <div class="div btn-3">
          <span>DD.MM.YYYY</span>
          <span class="material-icons">event</span>
        </div>
      </div>
    </div>
  </div>

  <button class="btn">Сформировать</button>

  <p style="margin: 30px 0">Список назначений после сеансов</p>
  <v-table :data="yourData" @delete-row="deleteRow"/>

  <h3 class="session__title">Лечение на дому</h3>
  <span>Лекарственный препарат</span>

  <div class="div">
    <button class="btn-1">Спр. "Препараты"</button>
    <button class="material-icons btn-2" @click="showPopup('Препараты')">menu_open</button>
  </div>

  <div>
    <div class="div">
      <div>
        <span>Путь приема</span>
        <div class="div">
          <button class="btn-1" @click="showPopup('Путь приема')">Путь приема</button>
        </div>
      </div>

      <div>
        <span>Дозировка</span>
        <div class="div">
          <button class="btn-1">Спр. "Дозы препаратов"</button>
          <button class="material-icons btn-2" @click="showPopup('Дозы препаратов')">menu_open</button>
        </div>
      </div>
    </div>
  </div>

  <div class="div">
    <div style="display: flex">
      <div>
        <span>Кратность приёма</span>
        <div class="div">
          <button class="btn-1">Спр. "Кр-ть приема"</button>
          <button class="material-icons btn-2" @click="showPopup('Кратность приёма')">menu_open</button>
        </div>
      </div>

      <div>
        <span>Начало приёма</span>
        <div class="div btn-3">
          <span>DD.MM.YYYY</span>
          <span class="material-icons">event</span>
        </div>
      </div>

      <div>
        <span>Конец приёма</span>
        <div class="div btn-3">
          <span>DD.MM.YYYY</span>
          <span class="material-icons">event</span>
        </div>
      </div>
    </div>
  </div>

  <p>Количество дней: <span class="blue">XX</span></p>

  <div>
    <button class="btn">Добавить</button>
  </div>

  <p>Лечение на дому</p>

  <div class="appointment">
    <div>
      <span>Лекарственный препарат</span>
      <span> Перорально</span>
      <span>5 мг</span>
    </div>

    <div>
      <span>2 раза в день утром и вечером </span>
      <span> с01.01.222 по10.01.2022 </span>
      <span> 10 дней</span>
    </div>
  </div>

  <h3 class="session__title">Рекомендации</h3>

  <div>
    <form>
      <div class="recommendation">
        <input placeholder="Текст рекомендации пациенту">
        <button class="material-icons btn-2">add</button>
      </div>
      <textarea placeholder="Рекомендации лечащего врача пациенту"></textarea>
    </form>

    <div class="info">
      <span class="material-icons">event</span>
      <span>Date: DD.MM.YYYY HH:MM</span>
      <span class="material-icons">person</span>
      <span>Doctor's Full Name</span>
      <span>Position</span>
    </div>
  </div>

  <div>
    <button class="btn">Сохранить назначения</button>
  </div>
</template>

<script lang="ts">
import vPopup from './v-popup.vue';
import vTable from './v-table.vue';
import vNeedleForm from './v-neadleForm.vue';
import vGenericModal from './v-genericModal.vue';

export default {
  name: 'hemodialysisSession',
  components: {
    vPopup,
    vTable,
    vNeedleForm,
    vGenericModal
  },
  data() {
    return {
      isInfoPopupVisible: false,
      selectedProgram: '',
      selectedInjection: '',
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
      needlePlaceholders: ["Венозные", "Артериальные"],
      needlePlaceholders2: ["Игла размер No1", "Игла размер No2", "Игла размер No3", "Игла размер No4"],
      needlePlaceholders4: ["Лекарственный препарат No1", "Лекарственный препарат No2", "Лекарственный препарат No3", "Лекарственный препарат No4"],
      needlePlaceholders3: ["Катетер No1", "Катетер No2", "Катетер No3", "Катетер No4"],
      genericPlaceholders2: ["Катетер Фолея", "Катетер Малеко", "Катетер Пеццера", "Катетер Тиманна",
      "Катетер Нелатона"],
      genericPlaceholders: ["граммов", "литров"],
      genericPlaceholders3: ["Перорально", "Внутривенно", "Аретериально"],
      genericPlaceholders4: [" мкг ", " мл ", " мг/кг "],
      genericPlaceholders5: ["1 раз в день", "2 раза в день ", "3 раза в день "],
      selectedContent: '',
    }
  },
  methods: {
    showPopup(content) {
      this.selectedContent = content;
      this.isInfoPopupVisible = true;
    },
    closeInfoPopup() {
      this.isInfoPopupVisible = false;
    },
    deleteRow(number: number) {
      this.yourData = this.yourData.filter(item => item.number !== number);
    },
    selectProgram(program) {
      this.selectedProgram = program;
    },
    selectInjection(program) {
      this.selectedInjection = program;
    },
  },
}
</script>

<style lang="scss" scoped>
.session {
  display: flex;
  align-items: baseline;

  &__title {
    margin: 10px 250px 25px 0;
  }
}

.div {
  display: flex;
  align-items: center;
  margin: 5px 5px 5px 0;
}

.appointment {
  border: 1px solid #ddd;
  width: 63%;
  padding: 10px;
  margin: 25px 0;
}

.blue {
  color: rgba(5, 99, 120, 0.85);
}

form {
  margin-bottom: 20px;
}

.recommendation {
  display: flex;
  align-items: center;
}

input {
  width: 59%;
  padding: 3px;
  margin-right: 10px;
}

textarea {
  width: 63%;
  height: 100px;
}

.info {
  display: flex;
  align-items: center;
  margin-top: 20px;
}

.info span {
  margin-right: 10px;
}
</style>
