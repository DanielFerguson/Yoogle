<template>
  <div class="flex flex-col lg:flex-row h-full">
    <div class="w-full lg:w-5/12 h-100">
      <img
        class="h-full object-cover object-center rounded-tl-lg rounded-bl-lg"
        :src="result.thumbnail"
        alt="Title Here"
      />
    </div>

    <div class="w-full lg:w-7/12 p-6 text-white">
      <a
        :href="'https://www.youtube.com/channel/' + result.channelId"
        class="flex items-center"
      >
        <img
          class="rounded-lg h-10 w-10"
          :src="result.channelThumbnail"
          alt="Title"
        />
        <span class="ml-4">{{ result.channelTitle }}</span>
      </a>

      <div class="flex mt-4 items-center">
        <h3 class="text-2xl font-bold">{{ result.title }}</h3>

        <!-- TODO(dan): Implement when hitting a caption result -->
        <!-- <div class="ml-auto">3:06 - 3:10</div> -->
      </div>

      <p v-if="hitProperty == null">
        <!-- TODO(dan): Replace with the snippet result when searching -->
        {{ result.description.substring(0, 120) + "..." }}
      </p>
      <p v-else-if="hitProperty && hitProperty.key == 'captions'">
        <em>"<span v-html="hitProperty.content.content.value"></span>"</em>
      </p>

      <a
        :href="watchURL"
        class="inline-block mt-4 ml-auto px-4 py-2 mr-2 border border-white rounded-lg hover:bg-white hover:text-gray-900 cursor-pointer transition-default"
      >
        Watch Now
      </a>
    </div>
  </div>
</template>

<script>
export default {
  props: ["result", "query"],

  computed: {
    // Check which property was hit with matchLevel 'full'
    hitProperty() {
      if (this.result == null) return null;

      var property = null;

      Object.keys(this.result._highlightResult).forEach(key => {
        if (key == "captions") {
          this.result._highlightResult[key].forEach(caption => {
            if (caption.content.matchLevel == "full")
              property = { key: "captions", content: caption };
          });
        }

        if ((key == "channelTitle") | (key == "description")) {
          if (this.result._highlightResult[key].matchLevel == "full")
            property = key;
        }
      });

      return property;
    },

    hitTime() {
      if (
        (this.hitProperty == null) |
        (this.query == null) |
        (this.query == "")
      )
        return null;

      const regex = /(\<mark\>)|(\<\/mark\>)+/gi;

      let startTime = 0;

      if (
        this.result.captions.find(content =>
          content.content.replaceAll(regex, "").includes(this.query)
        ) != undefined
      ) {
        const startTime = this.result.captions.find(content =>
          content.content.replaceAll(regex, "").includes(this.query)
        ).start;
      }

      return this.convertTimedeltaToSeconds(startTime);
    },

    watchURL() {
      let url = "https://youtube.com/watch?v=" + this.result.videoID;

      if (this.hitTime >= 1) url += "&t=" + this.hitTime;

      return url;
    }
  },

  methods: {
    convertTimedeltaToSeconds(delta) {
      if (delta == 0) return 0;

      let hours = delta.split(":")[0];
      let minutes = delta.split(":")[1];
      let seconds = delta.split(":")[2].split(",")[0];

      return (
        parseFloat(seconds) +
        parseFloat(minutes) * 60 +
        parseFloat(hours) * 60 * 60
      );
    }
  }
};
</script>
