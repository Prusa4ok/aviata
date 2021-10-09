<template>
  <div class="card-ticket">
    <div class="form-details text-s">
      <div class="content content__carrier">
        <img
          class="icon-iata"
          :src="'https://aviata.kz/static/airline-logos/80x80/'+ iata + '.png'"
          alt="KC"
        />
        <p class="text-m text-wb">{{ carrierName }}</p>
      </div>
      <div>
        <p class="">{{ formatedDate(departureDate).date }}</p>
        <p class="text-xl text-wb">{{ formatedDate(departureDate).time }}</p>
      </div>
      <div>
        <div class="form-from-to">
          <p class="accent-gray">{{ originCode }}</p>
          <p class="">{{ formatedTime(travelTime) }}</p>
          <p class="accent-gray">{{ destCode }}</p>
        </div>
        <img src="../../assets/images/0----0.svg" alt="from-to" />
        <p v-if="stops" class="accent-orange">с пересадкой</p>
      </div>
      <div>
        <p class="">{{ formatedDate(arriveDate).date }}<span class="text-xs accent-red">
            {{
              formatedDate(arriveDate).date === formatedDate(departureDate).date
                ? ""
                : "+1"
            }}
          </span>
        </p>
        <p class="text-xl text-wb">{{ formatedDate(arriveDate).time }}</p>
      </div>
      <a class="form-link" href="#">
        <p class="link accent-blue">Детали перелета</p>
      </a>
      <a class="form-link" href="#">
        <p class="link accent-blue">Условия тарифа</p>
      </a>
      <div  v-if="!refundable" class="content content__returnable">
        <img
          class="icon-16"
          src="../../assets/icons/icon-non-refundeble.svg"
          alt="KC"
        />
        <p class="text-s accent-dark-gray">Невозвратный</p>
      </div>
    </div>
    <div class="form-control">
      <p class="text-l">{{ amount }} ₸</p>
      <button class="btn btn__primary text-wbb text-l">Выбрать</button>
      <p class="text-s accent-dark-gray">Цена за всех пассажиров</p>
      <div class="content">
        <p class="text-s mr-6">
          {{ baggage[0].value ? "Багаж " + baggage[0].value + " кг" : "Нет багажа" }}
        </p>
        <button class="btn btn__secondary text-s text-wb accent-purple">+ Добавить багаж</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardTicket",
  props: {
    amount: {
      type: String,
      default: () => {
        return "Нет значения";
      },
    },
    arriveDate: {
      type: String,
      default: () => {
        return "Нет значения";
      }
    },
    departureDate: {
      type: String,
      default: () => {
        return "Нет значения";
      }
    },
    carrierName: {
      type: String,
      default: () => {
        return "Нет значения";
      }
    },
    iata: {
      type: String,
      default: () => {
        return "Нет значения";
      }
    },
    destCode: {
      type: String,
      default: () => {
        return "Нет значения";
      }
    },
    originCode: {
      type: String,
      default: () => {
        return "Нет значения";
      }
    },
    travelTime: {
      type: Number,
      default: () => {
        return 0;
      }
    },
    refundable: {
      type: Boolean,
      default: () => {
        return false;
      }
    },
    stops: {
      type: Number,
      default: () => {
        return false;
      }
    },
    baggage: {
    },
  },
  methods: {
    formatedDate(value) {
      let array = value.split(' ');
      const formatedTime = array.pop();
      const formatedValue = array.join(' ');
      return {
        date: formatedValue,
        time: formatedTime,
      };
    },
    formatedTime(value) {
      const minutes = (value % 3600) / 60;
      const hours = (value / 60 - minutes) / 60;
      return `${hours ? hours + " ч" : ""} ${minutes ? minutes + " м" : ""}`;
    }
  }
};
</script>

<style scoped>
.link {
  border-bottom: 1px dashed #7284e4;
  padding-bottom: 2px;
}

.card-ticket {
  width: 880px;
  background-color: #fff;
  border-radius: 4px;
  display: flex;
  overflow: hidden;
}

.form-link {
  text-decoration: none;
  width: max-content;
}

.form-details {
  padding: 40px 92px 18px 44px;
  display: grid;
  justify-items: center;
  width: 640px;
  grid-template-columns: repeat(4, auto);
  grid-template-rows: repeat(2, auto);
  row-gap: 46px;
}

.form-control {
  width: 240px;
  background-color: #f5f5f5;
  justify-content: space-between;
  display: flex;
  flex-direction: column;
  padding: 12px 20px;
}

.form-from-to {
  display: flex;
  justify-content: space-between;
}

.icon-iata {
  height: 20px;
  width: 20px;
}

.icon-16 {
  height: 16px;
  width: 16px;
}

.content {
  display: flex;
  align-items: center;
}

.content__carrier {
  grid-gap: 12px;
}

.content__returnable {
  grid-gap: 8px;
}

.text-xs {
  font-size: 10px;
}

.text-s {
  font-size: 12px;
}

.text-m {
  font-size: 14px;
}

.text-l {
  font-size: 18px;
}

.text-xl {
  font-size: 24px;
}

.text-xxl {
  font-size: 26px;
}

.text-wb {
  font-weight: 600;
}

.text-wbb {
  font-weight: 700;
}

.accent-gray {
  color: #b9b9b9;
}

.accent-dark-gray {
  color: #707276;
}

.accent-orange {
  color: #ff9900;
}

.accent-red {
  color: #ff3724;
}

.accent-blue {
  color: #7284e4;
}

.accent-purple {
  color: #5763B3;
}

.btn {
  cursor: pointer;
  transition: .1s;
  border-radius: 4px;
  border: none;
}

.btn:active {
  opacity: .5;
}

.btn__primary {
  background-color: #55BB06;
  padding: 8px 12px;
  color: #fff;
}

.btn__secondary {
  padding: 3px 8px;
  background-color: #EAF0FA;
}

.mr-6 {
  margin-right: 6px;
}
</style>
