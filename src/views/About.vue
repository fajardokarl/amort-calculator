<template>
  <div class="about container">
    <div class="about__body">
      <h1>ABOUT</h1>
      <p><span>AmortCalc</span> is simple personal project recreating an old project with Vue.js. It is basically a mortgage calculator! </p>
      <p>Showcasing data validation and manipulation, and Form design on <a target="_blank" href="https://xd.adobe.com/view/db176b73-4474-4b20-6640-14c7d1d474cc-ad26/">Adobe XD</a>.</p>
    </div>

  </div>
</template>

<style scoped>
.about {
  width: 100%;
  background: white;
  border-radius: 20px;
  margin: 20px auto;
  padding: 25px;
}

.about__body h1 {
  /* font-weight: 00; */
  font-size: 40px;
  padding-bottom: .5em;
  border-bottom: 1px solid #f9f9f9;
}

.about__body p {
  font-size: 18px;
  color: var(--main-black);
}

.about__body span {
  color: var(--primary-accent);
  font-weight: 700;
  font-size: 22px;
}

.about__body a {
  color: var(--yellow-accent) !important;
  font-weight: 600;
}

.about__body a:hover {
  text-decoration: underline;
  text-decoration-color: var(--primary-accent);;
}
</style>