<template>
  <div id="app">
    <!-- <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div> -->
    <header id="header">
      <nav id="nav" class="container">
        <h1 class="logo">
          <a href="/" class="logo__link">AmortCalc</a>
        </h1>
        <ul>
          <li>
            <router-link to="/">Home</router-link>
          </li>
          <li>
            <router-link to="/about">About</router-link>
          </li>
        </ul>
      </nav>
    </header>
    <router-view class="container" />
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap');

:root {
  --background: #EFF3F8;
  --primary-accent: #9170A3;
  --secondary-accent: #B082C9;
  --yellow-accent: #FCD465;
  --main-black: #707070;
}

html {
  background: var(--background);
}

body {
  font-family: 'Roboto', sans-serif;
  margin: 0;
	padding: 0;
}

*, *::before, *::after {
  box-sizing: border-box;
}

a {
  text-decoration: none;
  color: #fff;
}

input[type="text"] {
  padding: 10px 5px;
  border: solid 2px var(--secondary-accent);
  border-radius: 10px;
  font-size: 14px;
  width: inherit;
}

input:focus, input:active {
  outline: none;
}

label {
  color: var(--main-black);
  margin: 2px 8px;
}

.container {
  max-width: 1364px;
}

#header {
  background: var(--secondary-accent);
}

.container  {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 0 auto;
}
 h1 {
}

#header ul  {
  list-style: none;
  display: flex;
}

#header ul li {
  margin: 5px 10px;
  color: #fff;
  font-weight: 600;
  letter-spacing: 2px;
}

#nav a.router-link-exact-active {
  color: var(--yellow-accent);
}

</style>
