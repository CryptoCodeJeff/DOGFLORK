<script lang="ts">
  import CA from './CA.svelte'
  import { onMount } from 'svelte'
  import Svg from './Svg.svelte'

  let flip: boolean = true
  let scrollY: number = 0
  let currentSection: number = 0

  const sections = 8 // Número total de secciones

  const flipTimings = [
    { time: 1000, value: false },
    { time: 1400, value: true },
    { time: 1600, value: false },
    { time: 1800, value: true },
  ]

  const executeRandomSequence = () => {
    // Barajar los elementos del arreglo de forma aleatoria
    const shuffledTimings = flipTimings.sort(() => Math.random() - 0.5)

    // Ejecutar la secuencia de valores
    shuffledTimings.forEach(({ time, value }) => {
      setTimeout(() => {
        flip = value
      }, time)
    })
  }

  onMount(() => {
    const intervalSeconds = 10 // Tiempo en segundos
    setInterval(executeRandomSequence, intervalSeconds * 1000)

    document.body.style.minHeight = `${window.innerHeight * sections}px`

    console.log('Website created by: Scripted - https://x.com/cryptocodejeff')
  })

  const scrollEffect = () => {
    currentSection = Math.min(Math.floor(scrollY / window.innerHeight), sections - 1)
  }
</script>

<style lang="scss">
  @use 'src/sass/mixins.scss' as *;

  .hero {
    position: relative;
    align-items: center;
    flex-direction: column;
    justify-content: center;
    display: flex;
    height: 100vh;

    .socials {
      position: absolute;
      display: flex;
      gap: 30px;
      top: 20px;
      z-index: 9;
    }

    h1 {
      margin-top: -30vh;
      font-size: 130px;
      font-weight: bold;
      text-align: center;

      @include notDesktop {
        font-size: 70px;
      }
    }

    h2 {
      font-size: 40px;
      color: #612c04;
      margin-top: -50px;

      @include notDesktop {
        font-size: 30px;
        margin-top: -10px;
      }
    }
  }

  .flex {
    display: flex;
    justify-content: center;
    gap: 30px;
  }

  h3 {
    text-align: center;
    font-weight: bold;
    padding: 40px 0;
    font-size: 40px;
    color: #612c04;
  }

  .section {
    transition: 0.5s ease;
    position: fixed;
    top: 0px;
    margin: auto;
    left: 0;
    right: 0;
    opacity: 0;

    &.active {
      opacity: 1;
      z-index: 9;
    }
  }

  .chancla {
    position: fixed;
    bottom: -80px;

    @include notDesktop {
      display: none;
    }
  }

  .text {
    padding: 0 20px;
  }
  .text p {
    font-size: 20px;

    @include notDesktop {
      margin-top: -10px;
    }
  }

  .times {
    width: fit-content;

    display: grid;
    align-items: center;
    justify-content: center;
    grid-template-columns: 150px 120px;

    div {
      font-size: 24px;
    }

    b {
      font-size: 20px;
    }
  }

  .logo {
    position: fixed;
    bottom: 0px;
    right: 20%;

    display: none;

    animation: motionDog 1s 1s;
    transform-origin: bottom center;

    &.active {
      display: block;
    }
  }

  a {
    text-decoration: underline;
    color: #612c04;
  }

  .card {
    border: 3px solid #612c04;
    border-radius: 10px;
    background-color: rgb(253, 241, 232);
    padding: 20px;

    h4 {
      color: #612c04;
      font-size: 25px;
      padding-bottom: 20px;

      font-weight: bold;
      text-align: center;
    }
  }

  .col {
    display: flex;
    flex-direction: column;
    gap: 20px;
    justify-content: center;
    align-items: center;
  }

  .cards {
    display: flex;
    gap: 20px;

    @include notDesktop {
      flex-direction: column;
    }
  }

  .tokenomics {
    .cards {
      justify-content: center;
    }
    .card {
      width: 250px;

      @include notDesktop {
        width: 100%;
      }

      p {
        font-size: 60px;
        text-align: center;
      }

      &.hide {
        @include notDesktop {
          display: none;
        }
      }
    }
  }

  .bye {
    padding: 10vh 0;
    z-index: -1 !important;

    img {
      position: fixed;
      bottom: 0;
    }
  }

  @keyframes motionDog {
    0% {
      transform: rotateZ(-10deg);
    }
    20% {
      transform: rotateZ(10deg);
    }
    40% {
      transform: rotateZ(-10deg);
    }
    60% {
      transform: rotateZ(10deg);
    }
    80% {
      transform: rotateZ(-10deg);
    }
    100% {
      transform: rotateZ(0deg);
    }
  }
</style>

<div class="hero">
  <div class="socials">
    <a href="https://t.me/+EEfHmPhxXNJmNjMx" target="_blank">
      <Svg name="telegram" width="50" height="50" />
    </a>
    <a href="https://x.com/dogflork" target="_blank">
      <Svg name="twitter" width="50" height="50" />
    </a>
    <a href="https://www.youtube.com/@arenosol" target="_blank">
      <Svg name="youtube" width="50" height="50" />
    </a>

    <!--
    <a href="">
      <Svg name="pump" />
    </a>

    <a href="">
      <Svg name="dexscreener" />
    </a>
    -->
  </div>

  <h1>DOGFLORK</h1>
  <h2 reveal>Meet Flork's playful dog</h2>
</div>

<div class="images g-wrapper">
  <img class="chancla" src="/assets/flork-chancla.png" alt="" width="400px" />

  <img class="logo" class:active={flip} src="/assets/logo.png" alt="" width="200px" />
  <img class="logo" class:active={!flip} src="/assets/flipped.png" alt="" width="200px" />
</div>

<div class:active={currentSection === 1} class="section launch">
  <h3>Launchday</h3>
  <div class="flex">
    <div class="text">
      <p>$DogFlork will be launched at <b>20:30 UTC</b> on <a href="https://pump.fun">pump.fun</a>.</p>

      <p>The token will be created during a livestream on <a href="https://www.youtube.com/@arenosol">YouTube</a>.</p>

      <br />
      <br />
      <p><b>✔︎ FAIR LAUNCH!! No presales❌ No whitelists❌</b></p>
      <br />
      <p><b>✔︎ Team supply 1.5% for marketing purposes</b></p>
      <br />
      <p><b>✔︎ DOGFLORK is a memecoin created and led by the community</b></p>
    </div>
  </div>
</div>

<div class:active={currentSection === 2} class="section">
  <h3>Schedule</h3>
  <div class="flex">
    <div class="times card">
      <b>UTC</b>
      <div>20:30 PM</div>

      <b>CEST</b>
      <div>15:30 PM</div>

      <b>COLOMBIA</b>
      <div>15:30 PM</div>

      <b>PERU</b>
      <div>15:30 PM</div>

      <b>REP. DOM.</b>
      <div>16:30 PM</div>

      <b>MEXICO</b>
      <div>17:30 PM</div>

      <b>ARGENTINA</b>
      <div>17:30 PM</div>

      <b>ESPAÑA</b>
      <div>21:30 PM</div>
    </div>
  </div>
</div>

<div class:active={currentSection === 3} class="section how-to-buy">
  <h3>How to buy</h3>

  <div class="g-wrapper">
    <div class="cards">
      <div class="card">
        <h4>Method Sniper</h4>

        <p>Follow our detailed tutorial with GMGN</p>

        <div class="col">
          <a href="https://youtu.be/G2_tE0IDLvg" target="_blank">
            <Svg name="youtube" width="60" height="60"></Svg>
          </a>
        </div>
      </div>

      <div class="card">
        <h4>Method pump.fun</h4>

        <p>1 - Connect your wallet in <a href="https://pump.fun">pump.fun</a></p>
        <p>2 - Copy the OFFICIAL contract</p>
        <p>3 - Select an amount of SOL you want to trade</p>
        <p>4 - Click "place trade"</p>
      </div>

      <div class="card hide">
        <h4>Method Jupiter</h4>

        <p>1 - Connect your wallet in <a href="https://jup.ag/">jup.ag</a></p>
        <p>2 - Copy the OFFICIAL contract</p>
        <p>3 - Select an amount of SOL you want to trade</p>
        <p>4 - Click "Swap"</p>
      </div>
    </div>
  </div>
</div>

<div class:active={currentSection === 4} class="section tokenomics">
  <h3>Tokenomics</h3>

  <div class="g-wrapper">
    <div class="cards">
      <div class="card">
        <h4>Total Supply</h4>

        <p>1B</p>
      </div>

      <div class="card">
        <h4>Taxes</h4>

        <p>0%</p>
      </div>
    </div>
  </div>
</div>

<div class:active={currentSection === 5} class="section address">
  <h3>Contract address</h3>

  <div class="g-wrapper">
    <CA />
  </div>
</div>

<div class:active={currentSection === 6} class="section bye">
  <h3>Welcome to the $DOGFLORK community <br /> 🐶❤️</h3>

  <img src="/assets/footer.png" alt="" width="100%" style="right: 0%; bottom: 0px;" />
</div>

<a href="/es" style="position: fixed; right: 10px; bottom: 10px;">Español</a>

<svelte:window bind:scrollY on:scroll={scrollEffect} />
