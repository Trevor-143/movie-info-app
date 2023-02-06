<template>
  <div class="app">
    <main>
      <router-view />
    </main>
    <footer>
      <h3>&copy 2023</h3>
      <p>This application is powered by the Advanced Movie Search api on rapidapi.com</p>
    </footer>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@100;200;300;400;500;600;700;800;900&display=swap');

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: 'poppins', sans-serif;
}
body {
  background-color: black;
  color: #fff;
  /* margin-bottom: 150px; */
}
a {
  text-decoration: none;
}
footer {
  /* position: fixed; */
  height: 150px;
  /* bottom: 0; */
  /* left: 0; */
  /* right: 0; */
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: black;
  
}
footer p {
  max-width: 400px;
  text-align: center;
  padding: 10px 0;
}

</style>
