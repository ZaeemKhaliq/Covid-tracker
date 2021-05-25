<template>
  <div class="home">
    <div class="main-container" v-if="result != null">
      <div class="country-selector">
        <h1>Select Country</h1>
        <form>
          <select class="dropdown" @change="handleChange" :value="country">
            <option
              v-for="country in result.Countries"
              :key="country.id"
              :value="country.CountryCode"
              >{{ country.Country }}</option
            >
          </select>
        </form>
      </div>
      <div class="country-division">
        <div class="country">
          <p>COUNTRY</p>
          <h1 v-for="item in returnCountry" :key="item.id">
            {{ item.CountryCode == country ? item.Country : null }}
          </h1>
        </div>
        <div class="update">
          <p>LAST UPDATED:</p>
          <div v-for="item in returnCountry" :key="item.id">
            <h1 v-if="item.CountryCode == country">
              {{ item.Date }}
            </h1>
          </div>
        </div>
      </div>

      <div class="stats-division">
        <div class="stats-first">
          <div class="one-division">
            <p>TOTAL CONFIRMED CASES</p>
            <div v-for="item in returnCountry" :key="item.id">
              <h1
                class="counter"
                :data-target="item.TotalConfirmed"
                v-if="item.CountryCode == country"
              >
                0
              </h1>
            </div>
          </div>

          <div class="one-division">
            <p>TOTAL RECOVERED CASES</p>
            <div v-for="item in returnCountry" :key="item.id">
              <h1
                class="counter"
                :data-target="item.TotalRecovered"
                v-if="item.CountryCode == country"
              >
                0
              </h1>
            </div>
          </div>

          <div class="one-division">
            <p>TOTAL DEATH CASES</p>
            <div v-for="item in returnCountry" :key="item.id">
              <h1
                class="counter"
                :data-target="item.TotalDeaths"
                v-if="item.CountryCode == country"
              >
                0
              </h1>
            </div>
          </div>
        </div>

        <div class="stats-second">
          <div class="one-division">
            <p>NEW CONFIRMED CASES</p>
            <div v-for="item in returnCountry" :key="item.id">
              <h1
                class="counter"
                :data-target="item.NewConfirmed"
                v-if="item.CountryCode == country"
              >
                0
              </h1>
            </div>
          </div>

          <div class="one-division">
            <p>NEW RECOVERED CASES</p>
            <div v-for="item in returnCountry" :key="item.id">
              <h1
                class="counter"
                :data-target="item.NewRecovered"
                v-if="item.CountryCode == country"
              >
                0
              </h1>
            </div>
          </div>

          <div class="one-division">
            <p>NEW DEATH CASES</p>
            <div v-for="item in returnCountry" :key="item.id">
              <h1
                class="counter"
                :data-target="item.NewDeaths"
                v-if="item.CountryCode == country"
              >
                0
              </h1>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div v-else class="main-container">
      <h1 :style="{ textAlign: 'center' }">LOADING DATA...</h1>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import PakIcon from "../assets/pakistan.svg";

export default {
  name: "Home",
  data() {
    return {
      icon: PakIcon,
      country: "PK",
    };
  },
  props: ["result"],

  mounted() {
    console.log("Component Mounted!");

    const counters = document.querySelectorAll(".counter");
    const speed = 200;

    counters.forEach((counter) => {
      const updateCount = () => {
        const target = +counter.getAttribute("data-target");
        const count = +counter.innerText;

        const inc = target / speed;

        if (count < target) {
          counter.innerText = Math.ceil(count + inc);
          setTimeout(updateCount, 1);
        } else {
          counter.innerText = target;
        }
      };

      updateCount();
    });
  },
  updated() {
    console.log("Component Updated!");

    const counters = document.querySelectorAll(".counter");
    const speed = 200;

    counters.forEach((counter) => {
      counter.innerText = 0;

      const updateCount = () => {
        const target = +counter.getAttribute("data-target");
        const count = +counter.innerText;

        const inc = target / speed;

        if (count < target) {
          counter.innerText = Math.ceil(count + inc);
          setTimeout(updateCount, 1);
        } else {
          counter.innerText = target;
        }
      };

      updateCount();
    });
  },
  methods: {
    handleChange(e) {
      this.country = e.target.value;
      console.log(this.country);
    },
  },
  computed: {
    returnCountry() {
      console.log(
        this.result.Countries.filter((item) => item.CountryCode == this.country)
      );

      return this.result.Countries.filter(
        (item) => item.CountryCode == this.country
      );
    },
  },
};
</script>

<style lang="scss" scoped>
.home {
  min-height: calc(100vh - 50vh);
  display: flex;
}

.main-container {
  width: 90%;
  height: auto;
  margin: 50px auto;
  align-self: center;
}

.country-selector {
  text-align: center;
  margin-bottom: 1rem;

  & > h1 {
    margin: 0;
  }
}

.dropdown {
  width: 10rem;
  height: 2rem;
  font-size: 1rem;
  margin: 8px 0;
}

.country-division {
  border-bottom: 1px solid black;
  display: flex;
  justify-content: space-between;
}

.country {
  & > p {
    margin: 0;
    font-size: 14px;
    color: rgba(0, 0, 0, 0.7);
    font-weight: 500;
  }

  & > h1 {
    margin: 0;
  }
}

.flag-icon {
  width: 25px;
  height: 25px;
}

.update {
  & > p {
    margin: 0;
    font-size: 14px;
    color: rgba(0, 0, 0, 0.7);
    text-align: right;
    font-weight: 500;
  }

  h1 {
    margin: 0;
    font-size: 1rem;
  }
}

.stats-division {
  margin-top: 1rem;
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  height: 10rem;
}

.stats-first,
.stats-second {
  display: flex;
  justify-content: space-between;
}

.one-division {
  width: 10rem;
  margin: 0;
  display: inline-block;

  & > p {
    margin: 0;
    font-size: 14px;
    color: rgba(0, 0, 0, 0.7);
    font-weight: 500;
  }
}

.counter {
  margin: 0;
}

@media screen and (max-width: 500px) {
  .country {
    & > p {
      font-size: 10px;
    }
    & > h1 {
      font-size: 18px;
    }
  }

  .update {
    & > p {
      font-size: 10px;
    }
    h1 {
      font-size: 14px;
      text-align: right;
    }
  }

  .one-division {
    & > p {
      font-size: 10px;
    }
  }

  .counter {
    font-size: 18px;
  }
}
</style>
