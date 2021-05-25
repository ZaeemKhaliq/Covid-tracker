<template>
  <Header :results="results" />
  <router-view :result="results" />

  <Footer />
</template>

<script>
import Header from "./components/Header";
import Footer from "./components/Footer";

export default {
  name: "App",
  components: {
    Header,
    Footer,
  },
  data() {
    return {
      results: null,
    };
  },
  created() {
    const load = async () => {
      var requestOptions = {
        method: "GET",
        redirect: "follow",
      };

      // try {
      //   const data = await fetch(
      //     "https://covid-19-data.p.rapidapi.com/country?name=pakistan",
      //     {
      //       method: "GET",
      //       headers: {
      //         "x-rapidapi-key":
      //           "0351fcf876msha342a604f121c6ep1f7672jsnd551e8dd4b29",
      //         "x-rapidapi-host": "covid-19-data.p.rapidapi.com",
      //       },
      //     }
      //   );
      //   result.value = await data.json();
      //   console.log(result);
      // } catch (err) {
      //   console.log(err.message);
      // }

      try {
        const data = await fetch(
          "https://api.covid19api.com/summary",
          requestOptions
        );

        this.results = await data.json();
        console.log(this.results);
      } catch (err) {
        console.log(err.message);
      }
    };

    load();
  },
};
</script>

<style lang="scss">
#app {
  font-family: "Roboto", sans-serif;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  min-height: 100vh;
}

body {
  margin: 0;
}
</style>
