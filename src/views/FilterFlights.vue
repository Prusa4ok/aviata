<template>
  <div class="wrapper">
    <div class="form-filters">
      <FilterUI
        title="Опции тарифа"
        :items="filterItems.rate"
        @onChange="changeOptions"
      />
      <FilterUI
        title="Авиакомпании"
        :items="filters.carriers"
        @onChange="changeCarriers"
      />
    </div>
    <div class="form-filters">
      <card-ticket
        v-for="(ticket, index) in filteredArray"
        :key="index"
        :amount="ticket.itineraries[0][0].price.amount"
        :arriveDate="ticket.itineraries[0][0].segments[0].arr_time"
        :departureDate="ticket.itineraries[0][0].segments[0].dep_time"
        :carrierName="ticket.itineraries[0][0].segments[0].carrier_name"
        :iata="ticket.itineraries[0][0].segments[0].carrier"
        :travelTime="ticket.itineraries[0][0].traveltime"
        :refundable="ticket.itineraries[0][0].refundable"
        :stops="ticket.itineraries[0][0].segments[0].stops"
        :baggage="ticket.itineraries[0][0].segments[0].baggage_options"
        :destCode="ticket.itineraries[0][0].segments[0].dest_code"
        :originCode="ticket.itineraries[0][0].segments[0].origin_code"
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
      dataBase: [],
      filters: {
        options: {},
        carriers: {},
      },
      filteredArray: [],
    };
  },
  components: {
    FilterUI,
    CardTicket,
  },
  created() {
    this.dataBase = results.flights.slice();
    this.filteredArray = this.dataBase.slice();
    this.dataBase.forEach((item) => {
      this.filters.carriers[item.validating_carrier] =
        item.itineraries[0][0].carrier_name;
    });
  },
  methods: {
    changeOptions(value) {
      this.filters.options[value] = !this.filters.options[value];
      this.filterArray("options");
    },
    changeCarriers(value) {
      // eslint-disable-next-line no-extra-boolean-cast
      if (!!this.filters.carriers[value][0]) {
        Object.keys(this.filters.carriers).forEach((carrier) => {
          this.filters.carriers[carrier] = false;
        });
      }
      this.filters.carriers[value] = !this.filters.carriers[value];
      this.filterArray("carriers");
    },
    filterArray(element) {
      let newArray = [];

      if (element === "options") {
        const options = Object.keys(this.filters.options);
        const trueOptions = [];

        options.forEach((option) => {
          if (this.filters.options[option]) {
            trueOptions.push(option);
          }
        });
        newArray = this.dataBase.filter((item) => {
          if (trueOptions.includes("direct")) {
            if (item.itineraries[0][0].stops === 0) {
              return item;
            }
          }
          if (trueOptions.includes("baggage")) {
            if (
              item.itineraries[0][0].segments[0].baggage_options[0].value > 0
            ) {
              return item;
            }
          }
          if (trueOptions.includes("returnable")) {
            if (item.refundable) {
              return item;
            }
          }
        });
      }

      if (element === "carriers") {
        const carriers = Object.keys(this.filters.carriers);
        const trueCarriers = [];
        carriers.forEach((carrier) => {
          if (this.filters.carriers[carrier]) {
            trueCarriers.push(carrier);
          }
        });

        newArray = this.dataBase.filter((item) => {
          if (trueCarriers.includes(item.validating_carrier)) {
            return item;
          }
        });
      }

      this.filteredArray = newArray.slice();
    },
  },
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
