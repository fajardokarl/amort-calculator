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
  --primary-accent: #844db1;
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

input {
  padding: 10px 8px;
  border: solid 2px var(--secondary-accent);
  border-radius: 10px;
  font-size: 14px;
  width: inherit;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

input[type=number] {
  -moz-appearance: textfield;
}

input:focus, input:active {
  outline: none;
}

label {
  color: var(--main-black);
  margin: 2px 8px;
  white-space: nowrap;
}

.container {
  max-width: 1200px;
}

#header {
  background: rgb(132,77,177);
  background: -moz-linear-gradient(90deg, rgba(132,77,177,1) 0%, rgba(176,130,192,1) 100%);
  background: -webkit-linear-gradient(90deg, rgba(132,77,177,1) 0%, rgba(176,130,192,1) 100%);
  background: linear-gradient(90deg, rgba(132,77,177,1) 0%, rgba(176,130,192,1) 100%);
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr="#844db1",endColorstr="#b082c0",GradientType=1);
}

.container  {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 0 auto;
}
.logo {
  margin: auto 10px;
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

@media screen and (max-width: 767px) {
  label {
    font-size: 13px;
  }

  .hide {
    display: none;
  }
}
</style>
