<template>
  <div class="container">
    <!-- For profile section -->
    <div class="image">
      <img
        src="https://avatars.githubusercontent.com/u/108979458?s=400&u=f3ab83538dfb35fad4b112e818d4d4552a1dbac4&v=4"
        alt="avi"
      />
    </div>
    <div class="profile-content">
      <h2>{{ data.name }}</h2>
      <p>@{{ data.login }}</p>
      <h5>Front-End Engineer</h5>
      <section class="section">
        <div class="stat" id="repos">
          <p class="profile-figures" id="repo-fig">{{ data.public_repos }}</p>
          <h3 class="profile-details">Repositories</h3>
        </div>
        <div class="stat">
          <p class="profile-figures">{{ data.followers }}</p>
          <h3 class="profile-details">Followers</h3>
        </div>
        <div class="stat">
          <p class="profile-figures">{{ data.following }}</p>
          <h3 class="profile-details">Following</h3>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "ProfileSection",
  data() {
    return {
      data: "",
    };
  },
  mounted() {
    axios
      .get("https://api.github.com/users/Nunucodes")
      .then((response) => response.data)
      .then((data) => {
        this.data = data;
      });
  },
  profileImage:
    "https://avatars.githubusercontent.com/u/108979458?s=400&u=f3ab83538dfb35fad4b112e818d4d4552a1dbac4&v=4",
};
</script>

<style lang="scss" scoped>
@use "sass:math";

/* variables*/
$primary: #0d800d;
$background: #ffffff;
$base-gap: 30px;
$text-color: #020c18;
$breakpoint-minipc: 1500px;
$breakpoint-minitab: 800px;
$breakpoint-tablet: 1350px;
$breakpoint-miniphone: 500px;
$breakpoint-phone: 600px;

.container {
  display: flex;
  gap: $base-gap;
  align-items: center;
  background: #b7bf96;
  border: 1px solid rgba(77, 115, 248, 0.15);
  padding: $base-gap;
  border-radius: $base-gap/1;

  .image {
    width: 222px;
    height: 222px;
    padding: 5px;
    // position: relative;
    border-radius: 50%;
    background: linear-gradient(
      to bottom,
      rgb(77, 248, 105),
      rgba(77, 115, 248, 0.15)
    );

    @keyframes profile-pic {
      0% {
        background: linear-gradient(to right, #c5e90b, #86dc3d);
      }
      30% {
        background: linear-gradient(to bottom, #72cc50, #e1ff00);
      }
      50% {
        background: linear-gradient(to left, #bfd834, #86dc3d);
      }
      80% {
        background: linear-gradient(to top, #92e000, #e1ff00);
      }
      100% {
        background: linear-gradient(to right, rgb(77, 248, 105), #beed76);
      }
    }
    animation: profile-pic 4s ease-in-out infinite alternate;

    img {
      width: 100%;
      height: 100%;
      border-radius: 50%;
    }
  }

  .profile-content {
    line-height: 15px;

    h2 {
      font-family: "Merriweather";
      font-style: normal;
      font-weight: 700;
      font-size: 30px;
      color: $text-color;
    }

    p {
      font-weight: 400;
      font-size: 16px;
      color: #616161;
      font-family: "Roboto";
      line-height: 10px;
    }

    h5 {
      font-weight: 600;
      font-size: 20px;
      color: $text-color;
      line-height: 10px;
    }

    .section {
      display: flex;
      gap: $base-gap;

      .stat {
        padding: $base-gap/3;
        width: 150px;
        background: #bfd8c4;
        border-radius: 50%;
        text-align: center;
        line-height: $base-gap/3;
      }
    }
  }
}
</style>
