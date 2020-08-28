<template>
  <div class="sidebar-ad-container">

  </div>
</template>
<script>
export default {

data(){ 
    return { 
        ads: []
    }
}


};
</script>
<style lang="scss" scoped>

.sidebar-ad-container{ 
    width: 300px;
    height: 100%;
    background: blue;
    position: absolute;
    right: 0;
    display: flex;
    flex-direction: column;
}
</style>