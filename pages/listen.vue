<template>
<div class="audio-container">
 <audio controls>
              <source src="http://cdn.byub.org/byuradio/byuradio_mp3" type="audio/ogg" />
              <source src="http://cdn.byub.org/byuradio/byuradio_mp3" type="audio/mpeg" />Your browser does not support the audio element.
              <!-- <source src="http://cdn.byub.org/byuradio/byuradio_mp3" type="audio/mp3" /> -->
              <!-- <source src="http://cdn.byub.org/byuradio/byuradio_mp3" type="audio/mpeg" />Your browser does not support the audio element. -->
            </audio>
</div>            
</template>
<script>
export default {
  name: "Listen",
};
</script>
<style lang="scss" scoped>

.audio-container{ 
display: flex;
justify-content: center;
width: 100%;
height: 70px;
align-items: center;
audio { 
    width: 50%; 
    margin: 0;
    padding: 0;
}
}
</style>