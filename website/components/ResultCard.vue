<template>
  <div class="flex flex-col lg:flex-row h-full">
    <div class="w-full lg:w-5/12 h-full">
      <img
        class="bg-cover bg-center rounded-tl-lg rounded-bl-lg"
        :style="`background-image: url('${'/img.png'}')`"
        src="/img.png"
        alt="Title Here"
      />
    </div>

    <div class="w-full lg:w-7/12 p-6 text-white">
      <a href="#" class="flex items-center">
        <img class="rounded-lg" src="/thumbnail.png" alt="Title" />
        <span class="ml-4">FriendlyJordies</span>
      </a>

      <div class="flex mt-4 items-center">
        <h3 class="text-2xl font-bold">Video Title</h3>
        <div class="ml-auto">3:06 - 3:10</div>
      </div>

      <p>
        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer rhoncus
        arcu <mark>sit amet euismod pretium</mark>. Suspendisse molestie, risus
        ac tincidunt malesuada…
      </p>

      <a
        href="#"
        class="inline-block mt-4 ml-auto px-4 py-2 mr-2 border border-white rounded-lg hover:bg-white hover:text-gray-900 cursor-pointer transition-default"
      >
        Watch Now
      </a>
    </div>
  </div>
</template>
