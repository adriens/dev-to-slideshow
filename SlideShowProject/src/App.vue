<template>
  <div class="slide-show">
    <SlideShow :slideMatrix="slideMatrix" />
  </div>
</template>

<script>
import SlideShow from "./components/SlideShow.vue";
export default {
  name: "App",
  components: {
    SlideShow,
  },
  data: function () {
    return {
      slideMatrix: [[
        {
          img:
            "https://images.unsplash.com/photo-1679978677453-9452668cb867?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDF8NnNNVmpUTFNrZVF8fGVufDB8fHx8&auto=format&fit=crop&w=500&q=60",
          component: "CustomComponents1",
        },
        {
          img:
            "https://images.unsplash.com/photo-1679946026929-454c89c3af10?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDR8NnNNVmpUTFNrZVF8fGVufDB8fHx8&auto=format&fit=crop&w=500&q=60",
          component: "CustomComponents2",
        }],
      [{
        img:
          "https://images.unsplash.com/photo-1679936167452-18a6119f4006?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDJ8NnNNVmpUTFNrZVF8fGVufDB8fHx8&auto=format&fit=crop&w=500&q=60",
        component: "CustomComponents3",
      },
      {
        img:
          "https://images.unsplash.com/photo-1678058785885-44fad0ac4441?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDZ8NnNNVmpUTFNrZVF8fGVufDB8fHx8&auto=format&fit=crop&w=500&q=60",
        component: "CustomComponents4",
      }
      ]],
    };
  },
};
</script>

<style>
.slide-show {
  width: 100%;
  height: 100vh;
  background-color: aquamarine;
}
</style>
