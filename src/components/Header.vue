<template>
  <div class="header-container">
    <div class="text-container">
      <div class="left">
        <h1 class="heading">COVID TRACKER</h1>
        <p>Country wise statistics about the coronavirus</p>
      </div>
      <div class="right" v-if="results != null">
        <div class="right-row">
          <div class="one-division">
            <p>Global Total Cases</p>
            <h1
              class="global-counter"
              :data-target="results.Global.TotalConfirmed"
            >
              0
            </h1>
          </div>
          <div class="one-division">
            <p>Global Total Deaths</p>
            <h1
              class="global-counter"
              :data-target="results.Global.TotalDeaths"
            >
              0
            </h1>
          </div>
          <div class="one-division">
            <p>Global Total Recovered</p>
            <h1
              class="global-counter"
              :data-target="results.Global.TotalRecovered"
            >
              0
            </h1>
          </div>
        </div>
        <div class="right-row">
          <div class="one-division">
            <p>Global New Cases</p>
            <h1
              class="global-counter"
              :data-target="results.Global.NewConfirmed"
            >
              0
            </h1>
          </div>
          <div class="one-division">
            <p>Global New Deaths</p>
            <h1 class="global-counter" :data-target="results.Global.NewDeaths">
              0
            </h1>
          </div>
          <div class="one-division">
            <p>Global New Recovered</p>
            <h1
              class="global-counter"
              :data-target="results.Global.NewRecovered"
            >
              0
            </h1>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Header",
  props: ["results"],
  mounted() {
    const counters = document.querySelectorAll(".global-counter");
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
    const counters = document.querySelectorAll(".global-counter");
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
};
</script>

<style lang="scss" scoped>
.header-container {
  min-height: calc(100vh - 65vh);
  background-color: rgb(250, 46, 46);
  display: flex;
  color: white;
  flex-direction: column;
  justify-content: center;
}
.text-container {
  width: 90%;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
}
.heading {
  margin: 0;
}

.left {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.right {
  display: flex;
  justify-content: space-between;
}

.right-row {
  margin: 0px 20px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.one-division {
  & > h1 {
    margin: 0;
  }
  & > p {
    margin: 0;
  }
}

@media screen and (max-width: 700px) {
  .one-division {
    & > h1 {
      font-size: 26px;
    }

    & > p {
      font-size: 14px;
    }
  }
}

@media screen and (max-width: 500px) {
  .text-container {
    flex-direction: column;
  }

  .left,
  .right {
    text-align: center;
  }

  .one-division {
    & > h1 {
      font-size: 22px;
    }

    & > p {
      font-size: 15px;
    }
  }
}

@media screen and (max-width: 400px) {
  .one-division {
    & > h1 {
      font-size: 18px;
    }

    & > p {
      font-size: 11px;
    }
  }
}

@media screen and (max-width: 300px) {
  .one-division {
    & > h1 {
      font-size: 14px;
    }

    & > p {
      font-size: 10px;
    }
  }
}
</style>
