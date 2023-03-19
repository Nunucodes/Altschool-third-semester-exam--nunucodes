<template>
  <div class="repos-container">
    <div class="repos">
      <p @click="redirectToHome" class="btn">Back</p>
      <h1>{{ repo.name }}</h1>
      <p class="desc">{{ repo.description }}</p>
      <div class="space">
        <p><i class="fa-solid fa-code"></i> Language</p>
        <p class="details">{{ repo.language }}</p>
      </div>
      <div class="space">
        <p><i class="fa-solid fa-eye"></i> Visiblity</p>
        <p class="details">{{ repo.visibility }}</p>
      </div>
      <div class="space">
        <p><i class="fa-solid fa-calendar-days"></i> Created At</p>
        <p class="details">{{ repo.created_at }}</p>
      </div>
      <p>
        Link: <a class="links" :href="repo.html_url"> {{ repo.html_url }}</a>
      </p>
    </div>
  </div>
  <div class="backdrop-filter"></div>
</template>
<script>
export default {
  data() {
    return {
      repo: {},
    };
  },
  async created() {
    await new Promise((resolve) => setTimeout(resolve, 1000));
    const response = await fetch(
      `https://api.github.com/repositories/${this.$route.params.id}`
    );
    const data = await response.json();
    this.repo = data;
  },
  methods: {
    redirectToHome() {
      this.$router.push("/");
    },
  },
  mounted() {},
};
</script>

<style lang="scss" scoped>
@use "sass:math";

/* variables*/
$primary: #0d800d;
$base-gap: 30px;
$text-color: #020c18;
$background: #ffffff;
$breakpoint-miniphone: 500px;

.repos-container {
  display: flex;
  justify-content: center;
  align-items: center;
  opacity: 0;
  margin: 30vh 0;
  @keyframes repo-animation {
    0% {
      transform: translateY(30px);
      opacity: 0;
    }
    50% {
      transform: translateY(10px);
      opacity: 0.5;
    }
    100% {
      transform: translateY(0px);
      opacity: 1;
    }
  }
  animation: repo-animation 2s ease-in 1.2s 1 forwards;
  animation: name duration timing-function delay iteration-count direction
    fill-mode;

  .repos {
    background-color: $background;
    padding: $base-gap * 1.5 $base-gap;
    border-radius: 6px;
    border: 1px solid rgba(77, 115, 248, 0.15);

    .btn {
      cursor: pointer;
      color: $primary;
      font-weight: 600;
      font-size: 20px;
      text-align: right;
    }

    h1 {
      font-weight: 600;
      font-size: 20px;
      text-align: center;
      color: $text-color;
      margin: 30px 0;
    }

    .desc {
      text-align: center;
      color: #616161;
    }

    .space {
      display: flex;
      justify-content: space-between;

      .fa-code,
      .fa-eye,
      .fa-calendar-days {
        color: $primary;
        font-size: 18px;
      }

      .details {
        font-weight: 600;
        font-size: 16px;
      }
      // .backdrop-filter {
      //   height: 100vh;
      //   position: absolute;
      //   border: 1px solid blue;
      //   background-color: brown;
      //   top: 0;
      //   z-index: 10;
      // }

      @media (max-width: $breakpoint-miniphone) {
        justify-content: center;
        gap: $base-gap/3;
      }
    }

    .links {
      text-decoration: none;
      color: $primary;
      font-size: 17px;

      &:hover {
        text-decoration: underline;
      }
    }
  }
}
</style>
