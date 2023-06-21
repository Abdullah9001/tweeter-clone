<template>
  <div id="app" class="flex container h-screen w-full">
    <!-- side nav -->
    <div
      class="lg:w-1/5 border-r border-slate-200 px-2 lg:px-6 py-2 flex flex-col justify-between"
    >
      <div>
        <button
          class="h-12 w-12 hover:bg-lightblue text-3xl rounded-full text-blue"
        >
          <svg
            class="svg-icon"
            xmlns="http://www.w3.org/2000/svg"
            height="1em"
            viewBox="0 0 512 512"
          >
            <!--! Font Awesome Free 6.4.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. -->
            <path
              d="M459.37 151.716c.325 4.548.325 9.097.325 13.645 0 138.72-105.583 298.558-298.558 298.558-59.452 0-114.68-17.219-161.137-47.106 8.447.974 16.568 1.299 25.34 1.299 49.055 0 94.213-16.568 130.274-44.832-46.132-.975-84.792-31.188-98.112-72.772 6.498.974 12.995 1.624 19.818 1.624 9.421 0 18.843-1.3 27.614-3.573-48.081-9.747-84.143-51.98-84.143-102.985v-1.299c13.969 7.797 30.214 12.67 47.431 13.319-28.264-18.843-46.781-51.005-46.781-87.391 0-19.492 5.197-37.36 14.294-52.954 51.655 63.675 129.3 105.258 216.365 109.807-1.624-7.797-2.599-15.918-2.599-24.04 0-57.828 46.782-104.934 104.934-104.934 30.213 0 57.502 12.67 76.67 33.137 23.715-4.548 46.456-13.32 66.599-25.34-7.798 24.366-24.366 44.833-46.132 57.827 21.117-2.273 41.584-8.122 60.426-16.243-14.292 20.791-32.161 39.308-52.628 54.253z"
            />
          </svg>
        </button>
        <div>
          <button
            v-for="tab in tabs"
            :key="tab"
            @click="id = tab.id"
            :class="`focus:outline-none hover:text-blue flex items-center py-2 px-4 bg-lightblue-hover rounded-full mr-auto mb-3 ${
              id === tab.id ? 'text-blue' : ''
            }`"
          >
            <img :src="`${tab.src}`" class="text-3xl mr-4 svg-img" />
            <p class="text-lg font-semibold text-left hidden lg:block">
              {{ tab.title }}
            </p>
          </button>
        </div>
        <button
          class="text-white bg-blue rounded-full font-semibold focus:outline-none w-12 h-12 lg:h-auto lg:w-full p-3 bg-darkblue"
        >
          <p class="hidden tweet lg:block">Tweet</p>
        </button>
      </div>
      <div class="lg:w-full relative">
        <button
          @click="dropdown = true"
          class="flex items-center w-full hover:bg-lightblue rounded-full p-2 focus:outline-none"
        >
          <img
            src="profile.png"
            class="w-10 h-10 rounded-full border border-lighter"
          />
          <div class="hidden lg:block ml-4">
            <p class="text-sm font-bold leading-tight">Abdullah Jubayer</p>
            <p class="text-sm leading-tight">@ajStyle</p>
          </div>
          <i class="hidden lg:block fas fa-angle-down ml-auto text-lg"></i>
        </button>
        <div
          v-if="dropdown === true"
          class="absolute bottom-0 left-0 w-64 rounded-lg shadow-md border-lightest bg-white mb-16"
        >
          <button
            @click="dropdown = false"
            class="p-3 flex items-center w-full hover:bg-lightest p-2 focus:outline-none"
          >
            <img
              src="profile.png"
              class="w-10 h-10 rounded-full border border-lighter"
            />
            <div class="ml-4">
              <p class="text-sm font-bold leading-tight">Abdullah Jubayer</p>
              <p class="text-sm leading-tight">@ajStyle</p>
            </div>
            <i class="fas fa-check ml-auto test-blue"></i>
          </button>
          <button
            @click="dropdown = false"
            class="w-full text-left hover:bg-lightest border-t border-lighter p-3 test-sm focus:outline-none"
          >
            Add an existing account
          </button>
          <button
            @click="dropdown = false"
            class="w-full text-left hover:bg-lightest border-t border-lighter p-3 test-sm focus:outline-none"
          >
            Log out @Abdullah
          </button>
        </div>
      </div>
    </div>
    <!-- tweets -->
    <div class="w-full md:w-1/2 h-full overflow-y-scroll">
      <div
        class="px-5 py-3 border-b border-slate-200 flex items-center justify-between"
      >
        <h1 class="text-xl font-bold">Home</h1>
        <i class="far fa-star text-xl text-blue"></i>
      </div>
      <div class="px-5 py-3 border-b-8 border-slate-200 flex">
        <div class="flex-none">
          <img
            src="profile.png"
            class="flex-none w-12 h-12 rounded-full border border-slate-200 cursor-pointer"
          />
        </div>
        <form v-on:submit.prevent="addNewTweet" class="w-full px-4 relative">
          <textarea
            v-model="tweet.content"
            placeholder="What's up?"
            class="mt-3 pb-3 w-full focus:outline-none"
          />
          <div class="flex items-center cursor-pointer">
            <i class="text-lg text-blue mr-4 far fa-image"></i>
            <i class="text-lg text-blue mr-4 fas fa-film"></i>
            <i class="text-lg text-blue mr-4 far fa-chart-bar"></i>
            <i class="text-lg text-blue mr-4 far fa-smile"></i>
          </div>
          <button
            type="submit"
            class="h-10 px-4 text-white font-semibold bg-blue bg-darkblue focus:outline-none rounded-full absolute bottom-0 right-0"
          >
            Tweet
          </button>
        </form>
      </div>
      <div class="flex flex-col-reverse">
        <div
          v-for="tweet in tweets"
          :key="tweet"
          class="w-full p-4 border-b bg-lighter-hover flex cursor-pointer"
        >
          <div class="flex-none mr-4">
            <img src="profile.png" class="h-12 w-12 rounded-full flex-none" />
          </div>
          <div class="w-full">
            <div class="flex items-center w-full">
              <p class="font-semibold">Abdullah Jubayer</p>
              <p class="text-sm text-dark ml-2">@ajStyle</p>
              <p class="text-sm text-dark ml-2">1 sec</p>
              <i class="fas fa-angle-down text-dark ml-auto"></i>
            </div>
            <p class="py-2">
              {{ tweet.content }}
            </p>
            <div class="flex items-center justify-between w-full">
              <div class="flex items-center text-sm text-dark">
                <i class="far fa-comment mr-3"></i>
                <p>0</p>
              </div>
              <div class="flex items-center text-sm text-dark">
                <i class="fas fa-retweet mr-3"></i>
                <p>0</p>
              </div>
              <div class="flex items-center text-sm text-dark">
                <i class="fas fa-heart mr-3"></i>
                <p>1</p>
              </div>
              <div class="flex items-center text-sm text-dark">
                <i class="fas fa-share-square mr-3"></i>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div
        v-for="follow in following"
        :key="follow"
        class="w-full p-4 border-b bg-lighter-hover flex cursor-pointer"
      >
        <div class="flex-none mr-4">
          <img
            :src="`${follow.src}`"
            class="h-12 w-12 rounded-full flex-none"
          />
        </div>
        <div class="w-full">
          <div class="flex items-center w-full">
            <p class="font-semibold">{{ follow.name }}</p>
            <p class="text-sm text-dark ml-2">{{ follow.handle }}</p>
            <p class="text-sm text-dark ml-2">{{ follow.time }}</p>
            <i class="fas fa-angle-down text-dark ml-auto"></i>
          </div>
          <p class="py-2">
            {{ follow.tweet }}
          </p>
          <div class="flex items-center justify-between w-full">
            <div class="flex items-center text-sm text-dark">
              <i class="far fa-comment mr-3"></i>
              <p>{{ follow.comments }}</p>
            </div>
            <div class="flex items-center text-sm text-dark">
              <i class="fas fa-retweet mr-3"></i>
              <p>{{ follow.retweets }}</p>
            </div>
            <div class="flex items-center text-sm text-dark">
              <i class="fas fa-heart mr-3"></i>
              <p>{{ follow.like }}</p>
            </div>
            <div class="flex items-center text-sm text-dark">
              <i class="fas fa-share-square mr-3"></i>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- trending -->
    <div
      class="md:block hidden w-1/3 h-full border-l border-slate-200 py-2 px-6 overflow-y-scroll relative"
    >
      <input
        class="pl-12 rounded-full w-full p-2 bg-lighter text-sm mb-4"
        placeholder="Search Twitter"
      />
      <i
        class="fas fa-search absolute left-0 top-0 mt-5 ml-12 text-sm text-light"
      ></i>
      <div class="w-full rounded-lg bg-lightest">
        <div class="flex items-center justify-between p-3">
          <p class="text-lg font-bold">Trends for You</p>
          <i class="fas fa-cog text-lg text-blue"></i>
        </div>
        <button
          v-for="trend in trending"
          :key="trend"
          class="w-full flex justify-between bg-lighter-hover p-3 border-t border-slate-200"
        >
          <div>
            <p class="text-xs text-left leading-tight text-dark">
              {{ trend.top }}
            </p>
            <p class="font-semibold text-sm text-left leading-tight">
              {{ trend.title }}
            </p>
            <p class="text-left text-sm leading-tight text-dark">
              {{ trend.bottom }}
            </p>
          </div>
          <i class="fas fa-angle-down text-lg text-dark"></i>
        </button>
        <button
          class="p-3 w-full bg-lighter-hover text-left text-blue border-t border-slate-200"
        >
          Show More
        </button>
      </div>
      <div class="w-full rounded-lg bg-lightest my-4">
        <div class="p-3">
          <p class="text-lg font-bold">Who to Follow</p>
        </div>
        <button
          v-for="friend in friends"
          :key="friend"
          class="w-full flex bg-lighter-hover p-3 border-t border-slate-200"
        >
          <img
            :src="`${friend.src}`"
            class="w-12 h-12 rounded-full border border-slate-200"
          />
          <div class="hidden lg:block ml-4">
            <p class="text-sm font-bold leading-tight">{{ friend.name }}</p>
            <p class="text-sm leading-tight">{{ friend.handle }}</p>
          </div>
          <button
            class="ml-auto text-sm text-blue py-1 px-4 rounded-full border-2 border-blue"
          >
            Follow
          </button>
        </button>
        <button
          class="p-3 w-full bg-lighter-hover text-left text-blue border-t border-slate-200"
        >
          Show More
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  components: {},
  data() {
    return {
      tabs: [
        { src: "house-solid.svg", title: "Home", id: "home" },
        { src: "magnifying-glass-solid.svg", title: "Explore", id: "explore" },
        {
          src: "bell-regular.svg",
          title: "Notifications",
          id: "notifications",
        },
        { src: "envelope-regular.svg", title: "Messages", id: "messages" },
        { src: "clipboard-regular.svg", title: "Lists", id: "lists" },
        { src: "bookmark-regular.svg", title: "Bookmarks", id: "bookmarks" },
        { src: "certificate-solid.svg", title: "Verified", id: "Verified" },
        { src: "user-regular.svg", title: "Profile", id: "profile" },
        { src: "ellipsis-solid.svg", title: "More", id: "more" },
      ],
      id: "home",
      dropdown: false,
      trending: [
        {
          top: "Trending in TX",
          title: "Gigi",
          bottom: "Trending with: Rip Gigi",
        },
        { top: "Music", title: "We Won", bottom: "135K Tweets" },
        { top: "Pop", title: "Blue Ivy", bottom: "40k tweets" },
        { top: "Trending in US", title: "Denim Day", bottom: "40k tweets" },
        { top: "Trending", title: "When Beyonce", bottom: "25.4k tweets" },
      ],
      friends: [
        { src: "elon.jpg", name: "Elon Musk", handle: "@teslaBoy" },
        { src: "monk.jpg", name: "Adrian Monk", handle: "@detective:)" },
        { src: "kevin.jpg", name: "Kevin Hart", handle: "@miniRock" },
      ],
      following: [
        {
          src: "elon.jpg",
          name: "Elon Musk",
          handle: "@teslaBoy",
          time: "20 min",
          tweet: "Should I just quarantine on mars??",
          comments: "1,000",
          retweets: "550",
          like: "1,000,003",
        },
        {
          src: "kevin.jpg",
          name: "Kevin Hart",
          handle: "@miniRock",
          time: "55 min",
          tweet: "Should me and the rock do another sub-par movie together????",
          comments: "2,030",
          retweets: "50",
          like: "20,003",
        },
        {
          src: "elon.jpg",
          name: "Elon Musk",
          handle: "@teslaBoy",
          time: "1.4 hr",
          tweet: "Haha just made a flame thrower. Shld I sell them?",
          comments: "100,000",
          retweets: "1,000,002",
          like: "5,000,003",
        },
        {
          src: "elon.jpg",
          name: "Elon Musk",
          handle: "@teslaBoy",
          time: "1.4 hr",
          tweet: "Just did something crazyyyyyyy",
          comments: "100,500",
          retweets: "1,000,032",
          like: "5,000,103",
        },
      ],
      tweets: [{ content: "It is so nice outside!" }],
      tweet: { content: "" },
    };
  },
  methods: {
    addNewTweet() {
      let newTweet = {
        content: this.tweet.content,
      };
      this.tweets.push(newTweet);
    },
  },
};
</script>

<style>
::-webkit-scrollbar {
  display: none;
}
#app {
  font-family: Arial, Helvetica, sans-serif;
}
.svg-icon {
  margin-left: 1rem;
  fill: #1d9bf0;
}

.svg-img {
  fill: none;
  width: 22px;
  height: 22px;
}

.bg-lighter {
  background-color: #eff3f4;
  cursor: pointer;
}

.bg-lightest {
  background-color: #f7f9f9;
}

.bg-lighter-hover:hover {
  background-color: #eff1f1;
}

.bg-darkblue {
  background-color: #1d9bf0;
}

.bg-darkblue:hover {
  background-color: #1a8cd8;
}

.cursor-pointer {
  cursor: pointer;
}

.bg-lightblue-hover:hover {
  background-color: #e7e7e8;
}
</style>
