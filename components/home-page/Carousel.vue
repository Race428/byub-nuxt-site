<template>
  <!-- <div> -->
  <div class="carousel-wrapper">
    <div class="carousel">
      <div class="carousel__button--next"></div>
      <div class="carousel__button--prev"></div>
      <img
        v-for="(image, index) in images"
        :key="index"
        class="carousel__photo"
        :class="[index == currentPhotoIndex ? 'initial' : '']"
        :src="image.src"
      />

      <div @click="moveNext" class="carousel__button--next"></div>
      <div @click="movePrev" class="carousel__button--prev"></div>
    </div>
    <div class="button-container">
      <button
        v-for="(image, index) in images"
        :key="index"
        @click="moveCarouselTo(index)"
        :class="[index == slide ? 'active-button' : '']"
      ></button>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      currentPhotoIndex: 0,
      images: [
        {
          src:
            "https://s3.amazonaws.com/byuradio/content/images/banneritems/46aa8471-4740-4fa1-b012-29603b66ec17.jpg",
        },
        {
          src:
            "https://s3.amazonaws.com/byuradio/content/images/banneritems/a7a1c031-9920-4f7c-9693-a33c26514d88.jpg",
        },
        {
          src:
            "https://s3.amazonaws.com/byuradio/content/images/banneritems/4b826734-96c0-4f92-82bd-93b8cc6d6b66.jpg",
        },
        {
          src:
            "https://s3.amazonaws.com/byuradio/content/images/banneritems/cb9bfe87-0d54-49e3-a207-9430974f217c.jpg",
        },
      ],

      totalImages: 0,
      moving: false,
      slide: 0,
      imagesHTML: [],
    };
  },

  mounted() {
    var imagesClassName = "carousel__photo";
    this.imagesHTML = document.getElementsByClassName(imagesClassName);
    this.totalImages = this.imagesHTML.length;
    this.slide = 0;
    this.moving = false;
    this.imagesHTML[this.totalImages - 1].classList.add("prev");
    this.imagesHTML[0].classList.add("active");
    this.imagesHTML[1].classList.add("next");

    // var next = document.getElementsByClassName("carousel__button--next")[0];

    // var prev = document.getElementsByClassName("carousel__button--prev")[0];
    // next.addEventListener("click", this.moveNext);
    // prev.addEventListener("click", this.movePrev);
    // console.log("next button" , next)
  },

  watch: {
    moving(newVal, oldVal) {
      console.log("new val ", newVal);
      console.log("old val ", oldVal);
    },
  },
  methods: {
    moveNext() {
      console.log("this moving", this.moving);
      this.moving = false;
      // Check if moving
      if (!this.moving) {
        // If it's the last slide, reset to 0, else +1
        if (this.slide === this.totalImages - 1) {
          this.slide = 0;
        } else {
          this.slide++;
        }
        // Move carousel to updated slide
        this.moveCarouselTo(this.slide);
      }
    },

    movePrev() {
      console.log("this moving", this.moving);
      // Check if moving
      if (!this.moving) {
        // If it's the first slide, set as the last slide, else -1
        if (this.slide === 0) {
          this.slide = this.totalImages - 1;
        } else {
          console.log("inside the else in move prev");
          this.slide--;
        }

        // Move carousel to updated slide
        this.moveCarouselTo(this.slide);
      }
    },

    disableInteraction() {
      console.log("interaction was diabled");
      // Set 'moving' to true for the same duration as our transition.
      // (0.5s = 500ms)

      this.moving = true;

      // setTimeout runs its function once after the given time
      setTimeout(function () {
        this.moving = false;
        console.log("set time out ran and should be false", this.moving);
        this.images = [];
        console.log(this.images);
      }, 500);
    },

    moveCarouselTo(slide) {
      this.slide = slide;
      console.log("inside move carosel to ", slide);
      var imagesClassName = "carousel__photo";
      console.log("this moving in caroslute move to", this.moving);
      // Check if carousel is moving, if not, allow interaction
      if (!this.moving) {
        // temporarily disable interactivity
        this.disableInteraction();
        // Update the "old" adjacent slides with "new" ones
        var newPrevious = slide - 1,
          newNext = slide + 1,
          oldPrevious = slide - 2,
          oldNext = slide + 2;
        console.log("before all ifs", this.totalImages);
        // Test if carousel has more than three items
        if (this.totalImages - 1 > 2) {
          console.log("inside first if");

          // Checks and updates if the new slides are out of bounds
          if (newPrevious <= 0) {
            console.log("inside first if second");

            oldPrevious = this.totalImages - 1;
          } else if (newNext >= this.totalImages - 1) {
            console.log("inside else if");

            oldNext = 0;
          }
          // Checks and updates if slide is at the beginning/end
          if (slide === 0) {
            console.log("inside slide is 0");

            newPrevious = this.totalImages - 1;
            oldPrevious = this.totalImages - 2;
            oldNext = slide + 1;
          } else if (slide === this.totalImages - 1) {
            console.log("inside else slide");

            newPrevious = slide - 1;
            newNext = 0;
            oldNext = 1;
          }
          // Now we've worked out where we are and where we're going,
          // by adding/removing classes we'll trigger the transitions.
          // Reset old next/prev elements to default classes\
          var imagesClassName = "carousel__photo";
          console.log("inside adding class anmes ", imagesClassName);
          this.imagesHTML[oldPrevious].className = imagesClassName;
          this.imagesHTML[oldNext].className = imagesClassName;
          // Add new classes
          this.imagesHTML[newPrevious].className = imagesClassName + " prev";
          this.imagesHTML[slide].className = imagesClassName + " active";
          this.imagesHTML[newNext].className = imagesClassName + " next";
          this.moving = false;
        }
      }
    },
  },
};
</script>
<style lang="scss" scoped>
.carousel-wrapper {
  overflow: hidden;
  width: 100%;
  padding: 0 25%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.carousel-wrapper * {
  box-sizing: border-box;
}

.carousel {
  transform-style: preserve-3d;
}

.carousel__photo {
  opacity: 0;
  position: absolute;
  top: 0;
  width: 100%;
  margin: auto;
  padding: 1rem 4rem;
  z-index: 100;
  transition: transform 0.5s, opacity 0.5s, z-index 0.5s;
}
.carousel__photo.initial,
.carousel__photo.active {
  opacity: 1;
  position: relative;
  z-index: 900;
}

.carousel__photo.prev,
.carousel__photo.next {
  z-index: 800;
}
.carousel__photo.prev {
  transform: translateX(-100%); /* Move 'prev' item to the left */
}
.carousel__photo.next {
  transform: translateX(100%); /* Move 'next' item to the right */
}

.carousel__button--prev,
.carousel__button--next {
  position: absolute;
  top: 50%;
  width: 3rem;
  height: 3rem;
  background-color: #fff;
  transform: translateY(-50%);
  border-radius: 50%;
  cursor: pointer;
  z-index: 1001; /* Sit on top of everything */
  border: 1px solid black;
}
.carousel__button--prev {
  left: 0;
}
.carousel__button--next {
  right: 0;
}
.carousel__button--prev::after,
.carousel__button--next::after {
  content: " ";
  position: absolute;
  width: 10px;
  height: 10px;
  top: 50%;
  left: 54%;
  border-right: 2px solid black;
  border-bottom: 2px solid black;
  transform: translate(-50%, -50%) rotate(135deg);
}
.carousel__button--next::after {
  left: 47%;
  transform: translate(-50%, -50%) rotate(-45deg);
}

.button-container {
  button {
    height: 20px;
    width: 20px;
    outline: none;
    border: 1px solid lightgray;
    margin: 10px;
    border-radius: 50%;
    cursor: pointer;
    transition: 0.1s ease-in-out;
  }
  button:hover {
    background: #304a65;
  }
  .active-button {
    background: #304a65;
  }
}

@media only screen and (max-width: 624px) {
  .carousel-wrapper {
    padding: 0 2% !important;
  }

  .carousel__photo {
    padding: 1rem 1rem;
  }
  .carousel__button--prev,
  .carousel__button--next {
    width: 3rem;
    height: 3rem;
  }
  .carousel__button--prev {
    left: 10px;
  }
  .carousel__button--next {
    right: 10px;
  }
}
 

</style>