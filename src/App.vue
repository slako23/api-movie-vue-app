<template>
    <header>
      <router-link to="/">
      <h1><span>Amadi</span>Flix</h1>
    </router-link>
  </header>
  <main>
    <router-view/>
  </main>
</template>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans', sans-serif;
  &::selection {
    background: transparentize(#FF0000, 0.5);
  }
}
body {
  background-color: #000;
}
a {
  text-decoration: none;
}
header {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px 16px;
  background-color: #000;
  box-shadow: 0px 0px 6px rgba(0, 0, 0, 0.1);
  border-bottom: 2px solid #FF0000;
  h1 {
    color: #FFF;
    font-size: 28px;
    span {
      color: #FF0000;
    }
  }
}
</style>
