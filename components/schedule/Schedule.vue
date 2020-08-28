<template>
  <div class="schedule-container">
    <div class="schedule-header">
      <div class="header">
        <h1>ON AIR SCHEDULE</h1>
        <p>View Full Schedule</p>
      </div>
      <div class="header-content live">
        <img
          src="https://s3.amazonaws.com/byuradio/content/images/shows/brbsn/brbsn_thumb.jpg"
          alt="byu sports nation"
        />
        <section>
          <div class="on-air-link">
            <a href="/listen">
              <h3>ON AIR</h3>
            </a>
          </div>

          <a href="//www.byuradio.org/show/21cd2aa7-ebee-444d-8cdc-2111295d90f7/byu-sports-nation">
            <h1>BYU Sports Nation</h1>
          </a>

          <a
            href="//www.byuradio.org/episode/2045bb16-3729-4bdd-955f-18a92b8dfca7/byu-sports-nation-byu-sports-nation-aug-27"
          >
            <h2>BYU Sports Nation Aug 27</h2>
          </a>

          <p>BYU Sports Nation gives you a daily insider's look at BYU Sports.</p>
        </section>
      </div>

      <div class="schedule-header" v-for="(event, index) in scheduleEvents" :key="index">
        <div class="header-content">
          <img :src="event.img" alt="event image" />
          <section>
            <h3>{{event.time}}</h3>
            <h1 class="on-air">{{event.title}}</h1>

            <a
              href="//www.byuradio.org/episode/2045bb16-3729-4bdd-955f-18a92b8dfca7/byu-sports-nation-byu-sports-nation-aug-27"
            >
              <h2 class="on-air">{{event.header}}</h2>
            </a>

            <p class="on-air">{{event.content}}</p>
          </section>
          <!-- <section >
        <div class="schedule-event">
          <img :src="event.img" alt="event title" />
          <div class="event-contnet"></div>
        </div>
          </section>-->
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      scheduleEvents: [
        {
          time: "11:00am",
          title: "Finding Center",
          header: "Scriptures: A Tool for Navigation and Understanding",
          content: `Scriptures: A Tool for Navigation and Understanding Today's episode begins with Todd B. Parker for "True Doctrine, Understood, Changes Attitudes and Behavior." Then, Mary Anne Prater shares her devotional speech "Using Spiritual Maps to Navigate Through Life."`,
          img:
            "https://s3.amazonaws.com/byuradio/content/images/shows/brfct/brfct_thumb.jpg",
        },
        {
          time: "12:00pm",
          title: "Constant Wonder",
          header: "The End of Everything: The Death of the Universe",
          content:
            "Katie Mack theorizes about the many ways in which the universe could end. Paul Sutter investigates strange ways to die in space to showcase the power of the cosmos.",
          img:
            "https://s3.amazonaws.com/byuradio/content/images/shows/brwon/brwon_thumb.jpg",
        },
        {
          time: "1:00pm",
          title: "Constant Wonder",
          header: "Red Cloud: The American Hero Who Beat the American Army",
          content:
            "Tom Clavin tells the story of Red Cloud, the only Native American leader to ever defeat the US Army. Megan Kate Nelson explains what Westerners thought of the Civil War. Author Margaret Guroff on the history of the modern bicycle.",
          img:
            "https://s3.amazonaws.com/byuradio/content/images/shows/brwon/brwon_thumb.jpg",
        },
        {
          time: "2:00pm",
          title: "Top of Mind with Julie Rose",
          header: "March on Washington, Telehealth, How You Say It",
          content: `
William P. Jones of Univ of Minnesota on March on Washington. Christopher Palmer of Massachusetts Institue of Technology on rent control. Phillip Phan of Johns Hopkins Univ on telehealth. Katherine Kinzler of Univ of Chicago on her book "How You Say It: Why You Talk the Way YouDo and What It Says About You". Farzan Sasangohar of Texas A&M Univ on how architecture can help with PTSD.`,
          img:
            "https://s3.amazonaws.com/byuradio/content/images/shows/brtop/brtop_thumb.jpg",
        },
        {
          time: "4:00pm",
          title: "Top of Mind with Julie Rose",
          header: "March on Washington, Telehealth, How You Say It",
          content: `William P. Jones of Univ of Minnesota on March on Washington. Christopher Palmer of Massachusetts Institue of Technology on rent control. Phillip Phan of Johns Hopkins Univ on telehealth. Katherine Kinzler of Univ of Chicago on her book "How You Say It: Why You Talk the Way YouDo and What It Says About You". Farzan Sasangohar of Texas A&M Univ on how architecture can help with PTSD.`,
          img:
            "https://s3.amazonaws.com/byuradio/content/images/shows/brtop/brtop_thumb.jpg",
        },
      ],
    };
  },
};
</script>
<style lang="scss" scoped>
.schedule-container {
  display: flex;
  flex-direction: column;
  width: 66%;
  margin: auto;
  .schedule-header {
    min-height: 200px;
    width: 100%;
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    justify-content: center;
    border-bottom: 1px solid lightgrey;
    padding: 10px 0;

    .header {
      display: flex;
      background: #095c71;
      justify-content: space-between;
      align-items: center;
      padding: 0 5px;
      height: 40px;
      h1 {
        color: #b0b0b0;
        font-size: 1.2em;
        text-transform: uppercase;
      }
      p {
        color: #b0b0b0;
        font-weight: bold;
      }
    }
    .header-content {
      display: flex;
      align-items: flex-start;

      img {
        height: calc(200px - 40px);
        width: auto;
      }

      section {
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        height: 70%;
        margin: auto 10px;

        h3 {
          width: 90px;
          color: #0e3c52;
          font-size: 1.5em;
          //   margin: 5px 0;
        }
        h1 {
          color: black;
        }
      }
      a {
        color: black;
        text-decoration: none;
      }
      h2 {
        font-size: 0.7em;
        color: black;
        font-size: 1.1em;

        line-height: 1.9rem;
        margin-bottom: 8px;
      }

      p {
        color: #929497;
      }
    }

    .schedule-event {
      width: 100%;
      min-height: 200px;
      height: auto;
      //   max-height: 200px;
      display: flex;
      background: red;

      img {
        height: 100%;
        width: auto;
      }

      h3 {
        border: 1px solid red;
        width: 90px;
        color: red;
        font-size: 1.5em;
        margin: 5px 0;
      }
    }
    a {
      color: white;
      text-decoration: none;
    }
    h2 {
      font-size: 0.7em;
      color: #636466;
      font-size: 1.1em;

      line-height: 1.9rem;
      margin-bottom: 8px;
    }

    p {
      color: #929497;
    }
  }

  .live {
    background: black !important;
    h3 {
      border: 1px solid red;
      color: red !important;
    }
    h2,
    h1 {
      color: white !important;
      margin-top: 5px;
    }
    p {
      color: #929497;
    }
  }
}

@media only screen and (max-width: 624px) {
 .schedule-container {
  flex-direction: column;
  width: 100%;
  .schedule-header {
    // min-height: 200px;
    // width: 100%;
    // box-sizing: border-box;
    // display: flex;
    // flex-direction: column;
    // justify-content: center;
    // border-bottom: 1px solid lightgrey;
    // padding: 10px 0;

    .header {
      // display: flex;
      // background: #095c71;
      // justify-content: space-between;
      // align-items: center;
      // padding: 0 5px;
      // height: 40px;
      // h1 {
      //   color: #b0b0b0;
      //   font-size: 1.2em;
      //   text-transform: uppercase;
      // }
      // p {
      //   color: #b0b0b0;
      //   font-weight: bold;
      // }
    }
    .header-content {
      // display: flex;
      align-items: flex-start;

      img {
        height: calc(200px - 40px);
        width: auto;
      }

      section {
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        height: 70%;
        margin: auto 10px;

        h3 {
          width: 90px;
          color: #0e3c52;
          font-size: 1.3em;
          //   margin: 5px 0;
        }
        h1 {
          color: black;
        }
      }
      a {
        color: black;
        text-decoration: none;
      }
      h2 {
        font-size: 1em;
        color: black;
        font-size: 1.1em;

        line-height: 1.9rem;
        margin-bottom: 8px;
      }

      p {
        color: #929497;
      }
    }

    .schedule-event {
      width: 100%;
      min-height: 200px;
      height: auto;
      //   max-height: 200px;
      display: flex;
      background: red;

      img {
        height: 100%;
        width: auto;
      }

      h3 {
        border: 1px solid red;
        width: 90px;
        color: red;
        font-size: 1.5em;
        margin: 5px 0;
      }
    }
    a {
      color: white;
      text-decoration: none;
    }
    h2 {
      font-size: 0.7em;
      color: #636466;
      font-size: 1.1em;

      line-height: 1.9rem;
      margin-bottom: 8px;
    }

    p {
      color: #929497;
    }
  }

  .live {
    background: black !important;
    h3 {
      border: 1px solid red;
      color: red !important;
    }
    h2,
    h1 {
      color: white !important;
      margin-top: 5px;
    }
    p {
      color: #929497;
    }
  }
}
}
</style>