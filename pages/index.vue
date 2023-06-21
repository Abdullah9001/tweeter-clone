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
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="text-lg text-blue mr-4 svg-icon-short"
              viewBox="0 0 512 512"
            >
              <path
                d="M448 80c8.8 0 16 7.2 16 16V415.8l-5-6.5-136-176c-4.5-5.9-11.6-9.3-19-9.3s-14.4 3.4-19 9.3L202 340.7l-30.5-42.7C167 291.7 159.8 288 152 288s-15 3.7-19.5 10.1l-80 112L48 416.3l0-.3V96c0-8.8 7.2-16 16-16H448zM64 32C28.7 32 0 60.7 0 96V416c0 35.3 28.7 64 64 64H448c35.3 0 64-28.7 64-64V96c0-35.3-28.7-64-64-64H64zm80 192a48 48 0 1 0 0-96 48 48 0 1 0 0 96z"
              />
            </svg>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="text-lg text-blue mr-4 svg-icon-short"
              viewBox="0 0 512 512"
            >
              <path
                d="M0 96C0 60.7 28.7 32 64 32H448c35.3 0 64 28.7 64 64V416c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V96zM48 368v32c0 8.8 7.2 16 16 16H96c8.8 0 16-7.2 16-16V368c0-8.8-7.2-16-16-16H64c-8.8 0-16 7.2-16 16zm368-16c-8.8 0-16 7.2-16 16v32c0 8.8 7.2 16 16 16h32c8.8 0 16-7.2 16-16V368c0-8.8-7.2-16-16-16H416zM48 240v32c0 8.8 7.2 16 16 16H96c8.8 0 16-7.2 16-16V240c0-8.8-7.2-16-16-16H64c-8.8 0-16 7.2-16 16zm368-16c-8.8 0-16 7.2-16 16v32c0 8.8 7.2 16 16 16h32c8.8 0 16-7.2 16-16V240c0-8.8-7.2-16-16-16H416zM48 112v32c0 8.8 7.2 16 16 16H96c8.8 0 16-7.2 16-16V112c0-8.8-7.2-16-16-16H64c-8.8 0-16 7.2-16 16zM416 96c-8.8 0-16 7.2-16 16v32c0 8.8 7.2 16 16 16h32c8.8 0 16-7.2 16-16V112c0-8.8-7.2-16-16-16H416zM160 128v64c0 17.7 14.3 32 32 32H320c17.7 0 32-14.3 32-32V128c0-17.7-14.3-32-32-32H192c-17.7 0-32 14.3-32 32zm32 160c-17.7 0-32 14.3-32 32v64c0 17.7 14.3 32 32 32H320c17.7 0 32-14.3 32-32V320c0-17.7-14.3-32-32-32H192z"
              />
            </svg>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="text-lg text-blue mr-4 svg-icon-short"
              viewBox="0 0 512 512"
            >
              <path
                d="M32 32c17.7 0 32 14.3 32 32V400c0 8.8 7.2 16 16 16H480c17.7 0 32 14.3 32 32s-14.3 32-32 32H80c-44.2 0-80-35.8-80-80V64C0 46.3 14.3 32 32 32zm96 96c0-17.7 14.3-32 32-32l192 0c17.7 0 32 14.3 32 32s-14.3 32-32 32l-192 0c-17.7 0-32-14.3-32-32zm32 64H288c17.7 0 32 14.3 32 32s-14.3 32-32 32H160c-17.7 0-32-14.3-32-32s14.3-32 32-32zm0 96H416c17.7 0 32 14.3 32 32s-14.3 32-32 32H160c-17.7 0-32-14.3-32-32s14.3-32 32-32z"
              />
            </svg>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="text-lg text-blue mr-4 svg-icon-short"
              viewBox="0 0 512 512"
            >
              <path
                d="M464 256A208 208 0 1 0 48 256a208 208 0 1 0 416 0zM0 256a256 256 0 1 1 512 0A256 256 0 1 1 0 256zm177.6 62.1C192.8 334.5 218.8 352 256 352s63.2-17.5 78.4-33.9c9-9.7 24.2-10.4 33.9-1.4s10.4 24.2 1.4 33.9c-22 23.8-60 49.4-113.6 49.4s-91.7-25.5-113.6-49.4c-9-9.7-8.4-24.9 1.4-33.9s24.9-8.4 33.9 1.4zM144.4 208a32 32 0 1 1 64 0 32 32 0 1 1 -64 0zm192-32a32 32 0 1 1 0 64 32 32 0 1 1 0-64z"
              />
            </svg>

            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="text-lg text-blue mr-4 svg-icon-short"
              height="1em"
              viewBox="0 0 448 512"
            >
              <path
                d="M128 0c13.3 0 24 10.7 24 24V64H296V24c0-13.3 10.7-24 24-24s24 10.7 24 24V64h40c35.3 0 64 28.7 64 64v16 48V448c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V192 144 128C0 92.7 28.7 64 64 64h40V24c0-13.3 10.7-24 24-24zM400 192H48V448c0 8.8 7.2 16 16 16H384c8.8 0 16-7.2 16-16V192zM329 297L217 409c-9.4 9.4-24.6 9.4-33.9 0l-64-64c-9.4-9.4-9.4-24.6 0-33.9s24.6-9.4 33.9 0l47 47 95-95c9.4-9.4 24.6-9.4 33.9 0s9.4 24.6 0 33.9z"
              />
            </svg>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="text-lg text-blue mr-4 svg-icon-short-l"
              height="1em"
              viewBox="0 0 384 512"
            >
              <path
                d="M215.7 499.2C267 435 384 279.4 384 192C384 86 298 0 192 0S0 86 0 192c0 87.4 117 243 168.3 307.2c12.3 15.3 35.1 15.3 47.4 0zM192 128a64 64 0 1 1 0 128 64 64 0 1 1 0-128z"
              />
            </svg>
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
  font-family: sans-serif;
}
.svg-icon {
  margin-left: 1rem;
  fill: #1d9bf0;
}

.svg-img {
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
.svg-icon-short {
  width: 18px;
  fill: #1d9bf0;
}

.svg-icon-short-l {
  fill: #8ecdf7;
}
</style>
