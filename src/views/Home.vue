<template>
  <div class="home">
    <VideoWrapper :videos="videos" :viewport="viewportWidth" title="" />
  </div>
</template>

<script>
// @ is an alias to /src

import VideoWrapper from "@/components/VideoWrapper.vue";
import { onMounted, reactive, toRefs } from "vue";

import EventService from "@/services/EventService.js";

export default {
  name: "Home",
  components: {
    VideoWrapper
  },
  setup() {
    const state = reactive({
      viewportWidth: 10,
      videos: []
    });

    EventService.getVideos()
      .then(response => {
        state.videos = response.data;
      })
      .catch(err => {
        console.log("There was something wrong," + err);
      });

    onMounted(() => {
      let viewWidth = document.documentElement.clientWidth;
      if (viewWidth >= 1824) {
        state.viewportWidth = 10;
      } else if (viewWidth >= 1224) {
        state.viewportWidth = 9;
      } else if (viewWidth >= 768) {
        state.viewportWidth = 8;
      } else if (viewWidth >= 321) {
        state.viewportWidth = 7;
      }
    });

    const checkViewport = () => {
      //
      window.addEventListener("resize", function() {
        let viewWidth = document.documentElement.clientWidth;
        if (viewWidth >= 1824) {
          state.viewportWidth = 10;
        } else if (viewWidth >= 1224) {
          state.viewportWidth = 9;
        } else if (viewWidth >= 768) {
          state.viewportWidth = 8;
        } else if (viewWidth >= 321) {
          state.viewportWidth = 7;
        }
      });
    };
    checkViewport();
    return { ...toRefs(state) };
  }
};
</script>

<style scope>
@media only screen and (min-width: 321px) {
  .home {
    width: 95%;
    height: 100%;
    margin: 0 auto;
  }
}
@media only screen and (min-width: 768px) {
  .home {
    width: 95%;
    height: 100%;
    margin: 0 auto;
  }
}
@media only screen and (min-width: 1224px) {
  .home {
    width: 95%;
    height: 100%;
    margin: 0 auto;
  }
}
@media only screen and (min-width: 1824px) {
  .home {
    width: 95%;
    height: 100%;
    margin: 0 auto;
  }
}
</style>
