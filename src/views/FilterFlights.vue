<template>
  <div class="wrapper">
    <div class="form-filters">
      <FilterUI
        title="Опции тарифа"
        :items="filterItems.rate"
      />
      <FilterUI
        title="Авиакомпании"
        :items="results.airlines"
      />
    </div>
    <div class="form-filters"      
    >
      <card-ticket
        v-for="(ticket, index) in results.flights"
        :key="index"
        
        :amount="ticket.itineraries[0][0].price.amount"
        :departureDate="ticket.itineraries[0][0].segments[0].dep_time"
        :carrierName="ticket.itineraries[0][0].segments[0].carrier_name"
        :iata="ticket.itineraries[0][0].segments[0].carrier"
      />
    </div>
  </div>
</template>

<script>
import FilterUI from "../sharing/components/FilterUI.vue";
import CardTicket from "../sharing/components/CardTicket.vue";
import results from "../sharing/data/results.json";
import filterItems from "../sharing/data/filtersData.json";

export default {
  name: "filterFlights",
  data() {
    return {
      results,
      filterItems,
    };
  },
  components: {
    FilterUI,
    CardTicket,
  },
  created() {
    console.log(typeof(results.airlines));
  }
};
</script>

<style>
.wrapper {
  width: auto;
  max-width: 100vw;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  grid-gap: 20px;
  padding-top: 100px;
}

.form-filters {
  display: flex;
  flex-direction: column;
  grid-gap: 12px;
}
</style>
