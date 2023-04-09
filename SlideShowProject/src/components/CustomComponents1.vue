<template>
    <div class="custom-components">
        <h1 class="titre">Display Slide 1 : Project details (static content, bullets, gh project ur,...)</h1>
        <p>- Pitch du projet: En utilisant le langage HTML/JS avec n'importe quel framework, à l'exception de PHP, tel que
            Vue.js, Jekyll, React, nodejs ou Django, vous devrez créer un diaporama qui utilise une API pour présenter les
            articles produits par l'OPT. Ce diaporama devra être responsive, c'est-à-dire s'adapter aux différents types
            d'écrans tels que tablettes, ordinateurs, télévisions et mobiles.</p> <br>
        <p>Url Github du dépôt: https://github.com/adriens/dev-to-slideshow.git</p>
        <div class="logos">
            <img src="./icons/UNC.png" alt="Logo 1" class="logoUNC" />
            <img src="./icons/OPT.png" alt="Logo 2" class="logoOPT" />
        </div>
    </div>
</template>
  

<script>
export default {
    name: 'CustomComponents1',
    props: {}
}
</script>
  
<style>
.custom-components {
    padding: 10px;
    color: black;
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    box-shadow: 10px 10px 10px rgb(62, 62, 62);
}

.logos {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 50px;
    padding: 10px;
}

.logoUNC {
    width: 80px;
    height: auto;
}

.logoOPT {
    width: 100px;
    height: auto;
}

.titre {
    text-align: center;
    font-weight: bold;
    padding-bottom: 10px;
}
</style>
