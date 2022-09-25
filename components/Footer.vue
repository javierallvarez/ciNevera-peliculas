<template>
  <footer class="footer">

    <h6>Created by
      <span>
        Javier All Varez
      </span>
       · Powered by:
    </h6>
    <img src="../assets/images/blue_long_2-9665a76b1ae401a510ec1e0ca40ddcb3b0cfe45f1d51b77a308fea0845885648.svg" alt="">

  </footer>
  </template>


<script>
export default {
  name: 'Footer',
}
</script>


<style lang="scss">
  .footer{
    background: black;
    height: 10rem;
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 6px;
    margin-top: 1rem;
    color: white;
    border-top: 1px solid #2ef5c0;

    img{
      width: 18rem;
    }
    h6{
      font-size: 14px;
      font-weight: 100;
    }
    span{
      font-weight: 800;
    }
  }



</style>
