<template>
  <div class="card-ticket">
    <div class="form-details text-s">
      <div class="content content__carrier">
        <img
          class="icon-iata"
          src="https://aviata.kz/static/airline-logos/80x80/KC.png"
          alt="KC"
        />
        <p class="text-m text-wb">Air Astana</p>
      </div>
      <div>
        <p class="">25 ноя, вс</p>
        <p class="text-xl text-wb">23:25</p>
      </div>
      <div>
        <div class="form-from-to">
          <p class="accent-gray">ALA</p>
          <p class="">4 H 20 M</p>
          <p class="accent-gray">TSE</p>
        </div>
        <img src="../../assets/images/0----0.svg" alt="from-to" />
        <p class="accent-orange">accros shym, 1 h 50 m</p>
      </div>
      <div>
        <p class="">25 ноя, вс <span class="text-xs accent-red">+1</span></p>
        <p class="text-xl text-wb">23:25</p>
      </div>
      <a class="form-link" href="#">
        <p class="link accent-blue">Детали перелета</p>
      </a>
      <a class="form-link" href="#">
        <p class="link accent-blue">Условия тарифа</p>
      </a>
      <div class="content content__returnable">
        <img
          class="icon-16"
          src="../../assets/icons/icon-non-refundeble.svg"
          alt="KC"
        />
        <p class="text-s accent-dark-gray">Невозвратный</p>
      </div>
    </div>
    <div class="form-control"></div>
  </div>
</template>

<script>
export default {
  name: "CardTicket",
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
  display: flex;
  flex-direction: column;
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
</style>
