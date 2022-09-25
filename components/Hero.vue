<template>
  <div class="hero">
    <img src="../assets/images/interstellar.jpg" alt="" />
    <div class="text-container">
      <div class="text">
        <span class="mini-heading">Una nevera llena de cine.</span>
        <h1><span>Cin</span>evera</h1>
        <a href="#movie-flex" class="button">Ver Películas</a>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  name: 'hero',
}
</script>


<style lang="scss" scoped>

$princepal: #54f6c6;
$secondary: #ffcbcb;

.hero {
  height: 60vh;
  position: relative;
  background: linear-gradient(to top,
          #233142 0%,
          #455d7a 30%,
              $secondary 80%,
              );
  border-bottom: 1px solid #2ef5c0;

    &::after{
      content: "";
      position: absolute;
      top: 0;
      left: 0;
      height: 100%;
      width: 100%;
    }


  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    opacity: 20%;
    filter: grayscale(100%);
  }

  .text-container {
    align-items: center;
    display: flex;
    height: 100%;
    justify-content: center;
    margin: 0;
    position: absolute;
    text-align: center;
    top: 0;
    width: 100%;
    z-index: 1;

    .text {
      padding: 0 16px;
      width: 100%;
      max-width: 1400px;
      margin: 0 auto;
    }

    .mini-heading {
      color: #f6f6f6;
      font-weight: 100;
      font-size: 18px;
      margin-bottom: 8px;
      font-family: 'Bodoni Moda', serif;
      font-style: italic;
      @media (min-width: 500px) {
        font-size: 24px;
      }
    }

    h1 {
      color: #fff;
      font-size: 54px;
      font-weight: 200;
      margin: 10px 0;
      text-transform: uppercase;

      @media (min-width: 500px) {
        font-size: 84px;
      }

      span {
        font-weight: 900;
      }
    }

    .button {
      font-size: 20px;

    }
  }
}
</style>
