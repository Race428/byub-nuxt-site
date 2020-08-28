<template>
  <div class="radio-page">
    <div class="radio-page-header">
      <h1>Stations</h1>
      <input v-model="state" placeholder="Search By State" />
      <input v-model="number" placeholder="Number of Stations" type="number" />
    </div>
    <!-- <button @click="getChannels">Get Channels</button> -->
    <table class="channel-table" v-if="channels.length > 0">
      <thead>
        <tr>
          <th></th>
          <th></th>
          <th>Station Name</th>
          <th>Station URL</th>
          <th></th>
        </tr>
      </thead>
      <tbody>

        <tr class="desktop-table" v-for="(station, index) in channels" :key="index">
          <td>{{index + 1}}</td>
          <td class="station-logo">
            <img :src="station.favicon" alt="station logo" />
          </td>

          <td class="station-name">{{station.name}}</td>
          <td>
            <a :href="station.homepage" target="_blank">Visit Homepage</a>
          </td>
          <td>
            <audio controls>
              <source :src="station.url" type="audio/ogg" />
              <source :src="station.url" type="audio/mpeg" />Your browser does not support the audio element.
              <!-- <source src="http://cdn.byub.org/byuradio/byuradio_mp3" type="audio/mp3" /> -->
              <!-- <source src="http://cdn.byub.org/byuradio/byuradio_mp3" type="audio/mpeg" />Your browser does not support the audio element. -->
            </audio>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
const RadioBrowser = require("radio-browser");

export default {
  name: "Stations",

  mounted() {
    const promise = this.getChannels().then((res) => {
      this.channels = res;
    });
  },

  data() {
    return {
      channels: [],
      state: "utah",
      number: 30,
    };
  },

  watch: {
    // channels(newVal, oldVal) {
    //   console.log("new val", newVal);
    // },
    state(newVal, oldVal) {
      const promise = this.getChannels().then((res) => {
        this.channels = res;
      });
    },
    number(newVal, oldVal) {
      const promise = this.getChannels().then((res) => {
        this.channels = res;
      });
    },
  },

  methods: {
    async getChannels() {
      let filter = {
        limit: +this.number, // list max 5 items
        by: "bystateexact", // search in tag
        searchterm: this.state,
      };

      var channels = await RadioBrowser.getStations(filter);

      return channels;
    },
  },
};
</script>
<style lang="scss" scoped>
.radio-page {
  width: 100%;
  // background: blue;
  border-left: 1px solid black;
  border-right: 1px solid black;
  border-top: 1px solid black;
  overflow: auto;
  position: relative;
  display: flex;
  flex-direction: column;
  .radio-page-header {
    display: flex;
    flex-direction: column;
    min-height: 150px;
    background: white;
    position: sticky;
    top: 0;
    z-index: 100;
    align-items: flex-start;
    justify-content: space-evenly;
    width: 70%;
    background: white;
    margin: 0 auto;
    input {
      width: 250px;
      height: 50px;
      outline: none;
      border: none;
      border: 0.5px solid lightgray;
      border-radius: 5px;
      font-size: 1.2em;
      font-weight: bold;
    }
  }

  .channel-table {
    width: 70%;
    height: auto;
    position: relative;
    box-sizing: border-box;
    margin: 0 auto;

    thead {
      box-sizing: border-box;
      z-index: 100;
      pointer-events: none;
      tr {
        height: 100px;
        th {
          background: white;
          position: sticky;
          z-index: 100;
          box-sizing: border-box;
          // height: 100px;
          padding: 0;
          margin: 0;
          // min-height: 100px;
          // max-height: 100px;
          max-width: 150px;

          // text-align: left;
        }
      }
    }

    th {
      background: white;
      position: sticky;
      top: 150px;
      // z-index: 100;
      box-sizing: border-box;
      height: 100px;
      padding: 0;
      // text-align: left;
    }
    tr {
      transition: 0.1s ease-in-out;
      // text-align: left;
      cursor: pointer;
      z-index: 1;
    }
    .station-name {
      color: rgb(20, 82, 255);
    }
    a {
      // text-decoration: none;
      color: black;
      margin: 0;
      padding: 0;
      height: 100%;
    }

    tr:hover {
      opacity: 0.8;
    }

    th,
    td {
      text-align: left;
      border-bottom: 1px solid #ddd;
      box-sizing: border-box;
      height: 70px !important;

      img {
        height: 100%;
        max-width: 100%;
      }
    }

   

    .station-logo {
      // max-width: 50px !important;
      display: flex;
      justify-content: center;
      align-items: center;
      img {
        object-fit: contain;
      }
    }
  }
}

@media only screen and (max-width: 624px) {
  .radio-page {
    // width: 100%;
    // // background: blue;
    // border-left: 1px solid black;
    // border-right: 1px solid black;
    // border-top: 1px solid black;
    // overflow: auto;
    // position: relative;
    // display: flex;
    // flex-direction: column;
    .radio-page-header {
      // display: flex;
      // flex-direction: column;
      // min-height: 150px;
      // background: white;
      // position: sticky;
      // top: 0;
      // z-index: 100;
      // align-items: flex-start;
      // justify-content: space-evenly;
      width: 100%;
      background: white;
      padding: 0 5%;      
      input {
        width: 250px;
        height: 50px;
        outline: none;
        border: none;
        border: 0.5px solid lightgray;
        border-radius: 5px;
        font-size: 1.2em;
        font-weight: bold;
      }
    }

    .channel-table {
      width: 70%;
      height: auto;
      position: relative;
      box-sizing: border-box;
      margin: 0 auto;

      thead {
        box-sizing: border-box;
        z-index: 100;
        pointer-events: none;
        tr {
          height: 100px;
          th {
            background: white;
            position: sticky;
            z-index: 100;
            box-sizing: border-box;
            // height: 100px;
            padding: 0;
            margin: 0;
            // min-height: 100px;
            // max-height: 100px;
            max-width: 150px;

            // text-align: left;
          }
        }
      }

      th {
        background: white;
        position: sticky;
        top: 150px;
        // z-index: 100;
        box-sizing: border-box;
        height: 100px;
        padding: 0;
        // text-align: left;
      }
      tr {
        transition: 0.1s ease-in-out;
        // text-align: left;
        cursor: pointer;
        z-index: 1;
      }
      .station-name {
        color: rgb(20, 82, 255);
      }
      a {
        // text-decoration: none;
        color: black;
        margin: 0;
        padding: 0;
        height: 100%;
      }

      tr:hover {
        opacity: 0.8;
      }

      th,
      td {
        text-align: left;
        border-bottom: 1px solid #ddd;
        box-sizing: border-box;
        height: 70px !important;

        img {
          height: 100%;
          max-width: 100%;
        }
      }

      tr,
      td {
        // max-width: 150px !important;
        // display: flex;
        // flex-wrap: wrap;
      }

      .station-logo {
        // max-width: 50px !important;
        display: flex;
        justify-content: center;
        align-items: center;
        img {
          object-fit: contain;
        }
      }
    }
  }
}
</style>