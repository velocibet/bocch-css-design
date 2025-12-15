<script setup>
import character01 from "@/assets/yamada01.png";
import bg_character01 from "@/assets/yamada02.png";
import character02 from "@/assets/nijika01.png";
import bg_character02 from "@/assets/nijika02.png";
import character03 from "@/assets/ikuyo01.png";
import bg_character03 from "@/assets/ikuyo02.png";
import logo from "@/assets/logo.png";

const slides = [
  {
    id: 0,
    character: character01,
    bg: bg_character01,
    logo,
    nameKanji: '山田リョウ',
    ruby: 'やまだりょう',
    quote: '「バラバラな人間の個性が集まって それがひとつの音楽になるんだよ」',
    desc: '『ぼっち・ざ・ろっく!』の登場人物。4ピースバンド「結束バンド」のベース・コーラス担当。',
    rotatedText: 'YAMADA RYO',
    rotatedColor: '#2b66b2',
    stripeColor: '#2b66b2'
  },
  {
    id: 1,
    character: character02,
    bg: bg_character02,
    logo,
    nameKanji: '伊地知虹夏',
    ruby: 'いじちにじか',
    quote: '「でも私確信したの！ ぼっちちゃんがいれば夢をかなえられるって！」',
    desc: '元気いっぱいの明るい高校二年生。結束バンドのドラム担当。',
    rotatedText: 'IZICHI NIJIKA',
    rotatedColor: '#F2C94C',
    stripeColor: '#F2C94C'
  },
  {
    id: 2,
    character: character03,
    bg: bg_character03,
    logo,
    nameKanji: '喜多郁代',
    ruby: 'きたいくよ',
    quote: '「貴方を支えていけるような 立派なギタリストになるわね」',
    desc: '『ぼっち・ざ・ろっく!』の登場人物。「結束バンド」のギターボーカル担当。',
    rotatedText: 'KITA \u3000IKUYO',
    rotatedColor: '#e57373',
    stripeColor: '#e57373'
  }
];

const current = ref(0);
const layoutColor = useState('layoutColor', () => slides[0].stripeColor);

function nextSlide() {
  current.value = (current.value + 1) % slides.length;
  layoutColor.value = slides[current.value].stripeColor;
}
function prevSlide() {
  current.value = (current.value - 1 + slides.length) % slides.length;
  layoutColor.value = slides[current.value].stripeColor;
}

</script>

<template>
    <main>
    <transition name="slide-fade" mode="out-in">
      <section
        class="main-container"
        :key="slides[current].id"
        :style="{ '--stripe-color': slides[current].stripeColor }"
      >
        <!-- 배경 이미지 -->
        <img :src="slides[current].bg" class="bg-character" />

        <!-- 메인 캐릭터 -->
        <img :src="slides[current].character" class="character" />

        <!-- 로고 (같다면 고정) -->
        <img :src="slides[current].logo" class="logo" />

        <!-- 회전 텍스트 (두 개) -->
        <span class="rotated-text rotate-1"
              :style="{ '--rotate': '75deg', color: slides[current].rotatedColor }">
          {{ slides[current].rotatedText }}
        </span>

        <span class="rotated-text rotate-2"
              :style="{ '--rotate': '255deg', color: slides[current].rotatedColor }">
          {{ slides[current].rotatedText }}
        </span>

        <!-- 우측 텍스트 박스 -->
        <div class="title-container">
          <h1>
            <ruby>
              {{ slides[current].nameKanji }}
              <rt>{{ slides[current].ruby }}</rt>
            </ruby>
          </h1>
          <blockquote>{{ slides[current].quote }}</blockquote>
          <p>{{ slides[current].desc }}</p>
        </div>

        <p class="made">Made by @eu_yeo</p>

        <!-- 화살표 -->
        <div class="arrow left" @click="prevSlide">&#10094;</div>
        <div class="arrow right" @click="nextSlide">&#10095;</div>
      </section>
    </transition>
  </main>
  <!-- <main>
    <section class="main-container">
        <img :src="character01" class="character">
        <img :src="logo" class="logo">
        <img :src="bg_character01" class="bg-character">
        <span class="rotated-text rotate-1">YAMADA RYO</span>
        <span class="rotated-text rotate-2">YAMADA RYO</span>
        <div class="title-container">
            <h1>
                <ruby>
                    山田リョウ
                    <rt>やまだりょう</rt>
                </ruby>
            </h1>
            <blockquote>「バラバラな人間の個性が集まって それがひとつの音楽になるんだよ」</blockquote>
            <p>『ぼっち・ざ・ろっく!』の登場人物。4ピースバンド「結束バンド」のベース・コーラス担当。</p>
        </div>
        <p class="made">Made by @eu_yeo</p>
        <div class="arrow left">&#10094;</div>
        <div class="arrow right">&#10095;</div>
    </section>
  </main> -->
</template>

<style scoped>
@keyframes bgFlip {
  0% {
    transform: scaleX(1);
  }
  100% {
    transform: scaleX(-1);
  }
}

img {
    user-select: none;
    -webkit-user-drag: none;
}

.main-container {
    height: 80vh;
    --s: var(--stripe-color);
    background: linear-gradient(
        75deg,
        transparent 0%,
        transparent 30%,
        var(--s) 30%,
        var(--s) 70%,
        transparent 70%
    );

    --stripe-offset: 33vw;
    background-size: 100% 100%;
    background-position: calc(50% + var(--stripe-offset)) center;
    background-repeat: no-repeat;
    position: relative;
    display: flex;
    justify-content: center;
    align-items: flex-end;
    color:#fff;
    overflow: hidden;
}

.character {
    position: absolute;
    bottom: 0;
    left: 38%;
    height: 70vh;
    width: auto;
    z-index: 2;
}

.logo {
    position: absolute;
    width: 7vw;
    height: auto;
    bottom: 10px;
    left: 10px;
}

.bg-character {
    position: absolute;
    bottom: -25%;
    left: 0;
    height: 100vh;
    width: auto;
    opacity: 0.3;
    animation: bgFlip 0.5s forwards;
    transform: scaleX(-1)
}

.rotated-text {
    position: absolute;
    top: 39%;

    font-family: SHRIMP;
    white-space: nowrap;
    
    font-size: 13vh;
    user-select: none;
}

.rotate-1 {
    left: 45%;
    color: transparent;
    -webkit-text-stroke: 1px #ffffff;

    transform: rotate(75deg);
}

.rotate-2 {
    left: 38%;
    transform: rotate(255deg);
    color: #2b66b2;
}

.title-container {
    position: absolute;
    top: 25%;
    right: 10%;
    width: 15%;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: flex-start;
}

.title-container h1 {
    font-size: 32px;
    font-family: GenEiGothicN-Heavy;
}

h1 ruby rt {
    font-family: GenEiGothicN-Regular;
}

.title-container p {
    font-family: GenEiGothicN-ExtraLigh;
    margin-top: 5%;
}

.title-container blockquote {
    font-family: GenEiGothicN-Regular;
}

blockquote {
    width: 100%;
    margin: 0;
    padding: 5%;
}

.made {
    font-family: GenEiGothicN-ExtraLigh;
    position: absolute;
    bottom: 10px;
    right: 5px;
    color: white;
}

.arrow {
    position: absolute;
    display: flex;
    justify-content: center;
    align-items: center;
    top: 50%;
    width: 40px;
    height: 40px;
    transform: translateY(-50%);
    font-size: 100%;
    color: white;
    background-color: rgba(0,0,0,0.3);
    padding: 10px;
    border-radius: 50%;
    cursor: pointer;
    user-select: none;
    transition: background-color 0.3s;
    z-index: 5;
}

.arrow:hover {
    background-color: rgba(0,0,0,0.6);
}

.arrow.left {
    left: 20px;
}

.arrow.right {
    right: 20px;
}

.slide-fade-enter-active, .slide-fade-leave-active {
  transition: opacity 600ms ease, transform 600ms ease;
}

/* entering: start 상태 */
.slide-fade-enter-from {
  opacity: 0;
  transform: translateX(30px) scale(0.995);
}
.slide-fade-enter-from .character { opacity: 0; transform: translateX(60px) scale(1.02); }
.slide-fade-enter-from .bg-character { opacity: 0; transform: translateX(80px) scale(1.02); }
.slide-fade-enter-from .rotated-text { opacity: 0; transform: translateX(40px) rotate(var(--rotate)); }
.slide-fade-enter-from .title-container { opacity: 0; transform: translateX(50px); }

/* entering: end 상태 */
.slide-fade-enter-to {
  opacity: 1;
  transform: translateX(0) scale(1);
}
.slide-fade-enter-to .character { opacity: 1; transform: translateX(0) scale(1); }
.slide-fade-enter-to .bg-character { opacity: 0.3; transform: translateX(0) scale(1); }
.slide-fade-enter-to .rotated-text { opacity: 1; transform: translateX(0) rotate(var(--rotate)); }
.slide-fade-enter-to .title-container { opacity: 1; transform: translateX(0); }

/* leaving: start 상태 (현재 화면) */
.slide-fade-leave-from { opacity: 1; transform: translateX(0); }
.slide-fade-leave-from .character { opacity: 1; transform: translateX(0); }
.slide-fade-leave-from .rotated-text { opacity: 1; transform: translateX(0) rotate(var(--rotate)); }

/* leaving: end 상태 (사라질 때) */
.slide-fade-leave-to {
  opacity: 0;
  transform: translateX(-30px) scale(0.995);
}
.slide-fade-leave-to .character { opacity: 0; transform: translateX(-60px) scale(0.98); }
.slide-fade-leave-to .bg-character { opacity: 0; transform: translateX(-80px) scale(0.98); }
.slide-fade-leave-to .rotated-text { opacity: 0; transform: translateX(-40px) rotate(var(--rotate)); }
.slide-fade-leave-to .title-container { opacity: 0; transform: translateX(-50px); }

</style>