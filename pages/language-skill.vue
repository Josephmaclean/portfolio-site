<template>
  <main
    class="bg-black-pearl fixed top-0 left-0 right-0 bottom-0 w-full h-full"
  >
    <div class="flex justify-between">
      <nuxt-link to="/">
        <img
          src="@/assets/svg/maclean_logo.svg"
          alt="Maclean Logo"
          class="mt-10 ml-14"
        />
      </nuxt-link>

      <div class="flex mt-10 mr-14">
        <a
          href="https://blog.josephmaclean.dev/"
          target="_blank"
          rel="noopener noreferrer"
        >
          <button
            class="bg-black-pearl text-body-bold text-white px-6 py-4 btn-regular"
          >
            go to blog
          </button>
        </a>
        <!-- <a
          href="@/assets/pdf/joseph-maclean-arhin-resume.pdf"
          download="Joseph_Maclean_Arhin_Resume.pdf"
        > -->
        <button
          class="btn-outline bg-black-pearl border-white border-2 text-body-bold text-white px-6 py-2"
        >
          download my resume
        </button>
        <!-- </a> -->
      </div>
    </div>

    <div class="skills w-102 mx-auto mt-36">
      <skill-set-tabs>
        <skill-set-tab src="python_logo.svg" :selected="true">
          <h1 class="text-10xl leading-36 text-white">python</h1>
          <p class="mt-10 ff-monaco text-white">
            Ah, what more can I say about
            <span class="text-yellow">python</span>. With
            <span class="text-peach">this</span>
            <span class="text-yellow">beautiful</span> language, I can scrape
            the <span class="text-blue">web</span>, build
            <span class="text-purple">powerful</span>
            <span class="text-peach">APIs</span>, etc.
            <span class="text-yellow">Python</span> me the
            <span class="text-purple">power</span> of superhuman
            <span class="text-peach">strength</span> to tackle the
            <span class="text-peach">unknown</span> and the complicated
          </p>
        </skill-set-tab>
        <skill-set-tab src="typescript_logo.svg">
          <h1 class="text-10xl leading-36 text-white">
            type <br />
            Script
          </h1>
          <p class="mt-10 ff-monaco text-white">
            Be it translating ui designs into
            <span class="text-yellow">front-end</span> applications using
            <span class="text-blue">react</span> or
            <span class="text-green">vue</span> , or building
            <span class="text-blue">backend</span>
            <span class="text-peach">applications</span> with the help of
            <span class="text-purple">express js</span> and/or other libraries,
            <span class="text-yellow">typescript</span> gives me the super
            <span class="text-peach">power</span> of
            <span class="text-purple">flexibility</span>
          </p>
        </skill-set-tab>
        <skill-set-tab src="swift_logo.svg">
          <h1 class="text-10xl leading-36 text-white">swift⚡️</h1>
          <span class="mt-10 ff-monaco text-white">
            With <span class="text-peach">Swift</span>, I have the speed of the
            Flash. The elegance of <span class="text-blue">swift</span> means
            its my favorite language to develop iOS
            <span class="text-purple">applications</span> in (sorry
            <span class="text-blue">dart </span>).
          </span>
          <h4 class="text-white ff-sora text-3xl mt-24">Projects</h4>
          <div class="relative">
            <div class="flex mt-8">
              <p class="ff-sora text-white mr-4">myCrd</p>
              <a
                target="_blank"
                href="https://apps.apple.com/us/app/mycrd/id1558675666"
              >
                <img :src="require('@/assets/svg/external_link.svg')" alt="" />
              </a>
            </div>
            <p
              class="ff-monaco text-white"
              @mouseover="paragraphHovered"
              @mouseleave="hoverRemoved"
            >
              Providing an easy and secure way to store, manage and exchange
              business cards.
            </p>
            <img
              ref="projectCover"
              class="absolute -bottom-1 invisible left-3/4"
              src="@/assets/png/myCrd-cover.png"
              alt=""
              srcset=""
            />
          </div>
        </skill-set-tab>
      </skill-set-tabs>
      <social-media />
    </div>
  </main>
</template>

<script lang="ts">
import Vue from 'vue'
import gsap, { Power2 } from 'gsap'

export default Vue.extend({
  transition: 'intro',
  data() {
    return {
      swiftProjects: [
        {
          name: 'myCrd',
          description:
            'Providing an easy and secure way to store, manage and exchange business cards.',
          url: 'http://',
        },
      ],
    }
  },
  methods: {
    paragraphHovered(): void {
      const coverPhoto = this.$refs.projectCover
      gsap.to(coverPhoto, {
        duration: 0.7,
        y: -30,
        autoAlpha: 1,
        ease: Power2.easeOut,
      })
    },

    hoverRemoved(): void {
      const coverPhoto = this.$refs.projectCover
      gsap.to(coverPhoto, {
        duration: 0.5,
        autoAlpha: 0,
        y: 30,
      })
    },
  },
})
</script>

<style lang="scss">
$t-duration: 800ms;
$t-delay: 300ms;

.intro-enter-active,
.intro-leave-active {
  transition-duration: $t-duration * 2;

  &::before,
  &::after {
    content: '';
    position: fixed;
    top: 0;
    left: 0;
    z-index: 2;
    display: block;
    width: 100%;
    height: 50%;
    transition-property: opacity, transform;
    transition-timing-function: ease-in-out;
  }

  &::before {
    background-color: #2e2e2e;
  }

  &::after {
    top: 50%;
    background-color: #2e2e2e;
  }
}

.intro-leave {
  &::before,
  &::after {
    transform: scaleX(0);
  }
}

.intro-leave-active {
  &::before {
    transition-duration: $t-duration;
  }

  &::after {
    transition-duration: $t-duration - $t-delay;
    transition-delay: $t-delay;
  }
}

.intro-leave-to {
  &::before,
  &::after {
    transform: scale(1);
    transform-origin: left;
  }
}

.intro-enter {
  &::before,
  &::after {
    transform: scaleX(1);
  }
}

.intro-enter-active {
  &::before {
    transition-duration: $t-duration;
  }

  &::after {
    transition-duration: $t-duration - $t-delay;
    transition-delay: $t-delay;
  }
}

.intro-enter-to {
  &::before,
  &::after {
    transform: scaleX(0);
    transform-origin: right;
  }
}
</style>
