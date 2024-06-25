<script>
export default {
  data() {
    return {
      inserireNome: "",
      Nomeplayer: "",
      sceltaUtente: "",
      computerChoice: '',
      player: [
        {
          nome: this.Nomeplayer,
          punteggio: 0,
        }
      ],
      pc: [
        {
          nome: "pc",
          punteggio: 0
        }
      ]
    }
  },
  methods: {
    generateComputerChoice() {
      const choices = ['sasso', 'carta', 'forbice'];
      const randomIndex = Math.floor(Math.random() * choices.length);
      this.computerChoice = choices[randomIndex];
      document.querySelector(".animazione").classList.remove("animazionedisplay");
      document.querySelector(".animazione").classList.add("animate");


      setTimeout(() => {
        if (this.sceltaUtente === "sasso" && this.computerChoice === "carta") {
          this.pc[0].punteggio++;
          document.querySelector(".esito").innerHTML = "HAI PERSO"
        } else if (this.sceltaUtente === "sasso" && this.computerChoice === "forbice") {
          this.player[0].punteggio++;
          document.querySelector(".esito").innerHTML = "HAI VINTO"
        } else if (this.sceltaUtente === "carta" && this.computerChoice === "sasso") {
          this.player[0].punteggio++;
          document.querySelector(".esito").innerHTML = "HAI VINTO"
        } else if (this.sceltaUtente === "carta" && this.computerChoice === "forbice") {
          this.pc[0].punteggio++;
          document.querySelector(".esito").innerHTML = "HAI PERSO"
        } else if (this.sceltaUtente === "forbice" && this.computerChoice === "sasso") {
          this.pc[0].punteggio++;
          document.querySelector(".esito").innerHTML = "HAI PERSO"
        } else if (this.sceltaUtente === "forbice" && this.computerChoice === "carta") {
          this.player[0].punteggio++;
          document.querySelector(".esito").innerHTML = "HAI VINTO"
        } else if (this.sceltaUtente === "sasso" && this.computerChoice === "sasso") {
          document.querySelector(".esito").innerHTML = "PAREGGIO"
        }
        else if (this.sceltaUtente === "carta" && this.computerChoice === "carta") {
          document.querySelector(".esito").innerHTML = "PAREGGIO"
        }
        else if (this.sceltaUtente === "forbice" && this.computerChoice === "forbice") {
          document.querySelector(".esito").innerHTML = "PAREGGIO"
        }
        document.querySelector(".animazione").classList.add("animazionedisplay");
        document.querySelector(".scelta").classList.remove("computer")
        setTimeout(() => {
          document.querySelector(".scelta").classList.add("computer")
        }, 1800)
      }, 3000);
    },
    removeclass() {
      document.querySelector(".play").classList.add("removedisplay");
      document.querySelector(".displaynonne").classList.remove("mino");

    },
    addplayer() {
      this.nomeplayer = this.inserireNome;
      document.querySelector(".nome").classList.add("removedisplay")
    }
  }
}

</script>
<template>
  <header>
  </header>

  <main>
    <h1 class="titolo">Benvenuto/a in sasso carta forbice</h1>
    <div class="play container">
      <img src="/Morra-cinese.webp" alt="">
      <i @click="removeclass()" class="fa-solid fa-circle-play">play</i>
    </div>
    <div class="mino displaynonne container text-center">
      <div class="prova off d-flex felxxato">
        <div class="row col-12 col-md-6">
          <div class="media">
            <h1>Nome player:{{ inserireNome }}
            </h1>
            <h2 v-for="players in player">il tuo punteggio: {{ players.punteggio }}</h2>
            <div class="nome mt-4">
              <input type="text" placeholder="inserisci il tuo nome" v-model="inserireNome">
              <button class="btn btn-success mx-2" @click="addplayer">salva nome</button>
            </div>
          </div>
        </div>
        <div class="row col-12 col-md-6">
          <div class="pc">
            <h1>Nome:PC</h1>
            <h2 v-for="pcs in pc">punteggio PC: {{ pcs.punteggio }}</h2>
          </div>
        </div>
        <!-- <div class="animazione animazionedisplay text-center container mt-3 mb-3">
        <div class="sasso animate">
          <img src="/pugno.jpg" alt="">
        </div>
        <div class="carta">
          <i class="fa-regular fa-hand"></i>
        </div>
        <div class="forbice">
          <i class="fa-solid fa-hand-scissors" style="color: #f8c4c4;"></i>
        </div>
      </div> -->

      </div>
      <div>
        <input class="mt-2 mb-2"type="text" id="sasso" v-model="sceltaUtente" placeholder="Sasso/Carta/Forbice?">
        <button class="btn btn-success mt-1" @click="generateComputerChoice">Genera scelta del computer</button>
        <p class="computer scelta colore">Scelta del computer: {{ computerChoice }}
        <p class="esito"></p>
        </p>
      </div>

      <div class="animazione animazionedisplay text-center container mt-4 mb-3">
        <div class="sasso animate">
          <img src="/pugno.jpg" alt="">
        </div>
        <div class="carta">
          <i class="fa-regular fa-hand"></i>
        </div>
        <div class="forbice">
          <i class="fa-solid fa-hand-scissors" style="color: #f8c4c4;"></i>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
h1 ,h2{
  color: black;
}
.colore{
  color: red;
  font-size: 20px;
}
main{
  background-color: bisque;
  height: 100vh;
}
.media , .pc{
border: 2px solid black;
margin-top: 10px;
margin-bottom: 10px;
padding: 10px;
box-shadow: 1px 1px 2px 2px lightgreen;
}
@media only screen and (max-width: 500px) {
  .prova {}
}

.animate img {
  width: 40px;
}

.computer {
  display: none;
}

.carta i,
.forbice i {
  font-size: 40px;
}

.animazionedisplay {
  display: none;
}

.animate {
  animation: sasso-anim 3s ease-in-out infinite;
}


@keyframes sasso-anim {
  0% {
    transform: scale(1);
  }

  50% {
    transform: scale(1.2);
  }

  100% {
    transform: scale(1);
  }
}

.carta {
  animation: carta-anim 3s ease-in-out infinite;
}

@keyframes carta-anim {
  0% {
    transform: translateX(0);
  }

  50% {
    transform: translateX(20px);
  }

  100% {
    transform: translateX(0);
  }
}

/* Animazione Forbice */
.forbice {
  animation: forbice-anim 3s ease-in-out infinite;
}

@keyframes forbice-anim {
  0% {
    transform: rotate(0deg);
  }

  50% {
    transform: rotate(45deg);
  }

  100% {
    transform: rotate(0deg);
  }
}

.mino {
  display: none;
}

.felxxato {
  justify-content: space-around;
  flex-wrap: wrap;
}

.off {
  display: none;
}
.play{
  color: green;
}

.play i {
  font-size: 100px;
  text-align: center;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.play img {
  height: 80vh;
  width: 100%;
  position: relative;

}

.play i:hover {
  color: green;
  cursor: pointer;
}

.titolo {
  text-align: center;
}

.removedisplay {
  display: none;
}
</style>
