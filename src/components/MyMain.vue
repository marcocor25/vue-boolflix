<template>
  <div class="container">
    <figure class="logo">
      <img src="../assets/img/Boolflix.svg" />
    </figure>
    <div class="input-wrapper">
      <input type="search" placeholder="Cerca film e serie tv..." />
      <button>Cerca</button>
    </div>
    <ul class="film-container">
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
      <li>Test</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "MyMain",
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.container {
  width: 60vw;
  height: 100vh;
  padding: 20px 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
  border: 2px dashed yellow;

  .logo {
    width: 200px;
    filter: drop-shadow(3px 3px 1px black);
  }

  .input-wrapper {
    width: 500px;
    display: flex;
    gap: 5px;

    input {
      flex-grow: 1;
      height: 30px;
      padding: 0 5px;
      border-radius: 5px;
      border: 1px solid #555;
      color: currentColor;
      background: #222;

      &:focus-visible {
        outline: none;
      }
    }

    button {
      padding: 0 10px;
      border-radius: 5px;
      border: 1px solid #555;
      color: currentColor;
      background: #222;
    }
  }

  .film-container {
    width: 500px;
    overflow: auto;
    border: 2px dashed blue;
  }
}
</style>
