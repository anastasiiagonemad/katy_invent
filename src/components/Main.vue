<template>
    <div :class="$style.main">
        <div class="header" :class="$style['header__container']">
            <div class="header__text" :class="$style['header__title1']">
                <h1 :class="$style['title-1']">Любовь - это...</h1>
            </div>
            <div class="header__image" :class="$style['top-image']">
                <img src="/images/3.jpg" alt="pic">
            </div>
            <div class="header__text" :class="$style['header__title2']">
                <h2 :class="$style['title-2']">...совместные мечты</h2>
            </div>
        </div>

        <div class="letter block-paddings" :class="$style['letter__container']">
            <div :class="$style['letter__image']">
                <img src="/images/letter.png" alt="pic">
            </div>
            <div class="letter__text" :class="$style['letter__text']">
                <p v-html="letterText" />
            </div>
        </div>

        <div :class="$style['line__container']" class="line heart">
            <img class="heart__image" src="/images/heart.svg" alt="heart">
        </div>

        <div class=" wishes" :class="$style[' wishes__container']">
            <h2 :class="$style['wishes__container--title']">Пожелания</h2>
            <div :class="$style['wishes__container--text']">
                <div class="wishes__text" v-for="el in wishes" :key="el.id" :ref="'wishText_' + el.id"
                    :class="$style[`wishes__container--text__${el.id}`]">
                    <span>{{ el.id }}</span>
                    <p v-html="el.wish" />
                </div>
            </div>
        </div>

        <div :class="$style['info__container']">
            <div class="invent" :class="$style['invent__container']">
                <div :class="$style['invent__title']">
                    <h2>27 июня 2025</h2>
                </div>
                <div>
                    <p><span>15:20</span><br>Торжественная роспись <br>Приморский ЗАГС</p>
                </div>
                <div>
                    <p><span>17:00</span><br>Фуршет <br>Банкетный зал, 2 этаж,<br> Приморский пр. 137, к.1 СПб</p>
                </div>
            </div>
            <div class="regret" :class="$style['regret__container']">
                <div :class="$style['regret__container--content']">
                    <p :class="$style['regret__container--content__text']">Для подтверждения вашего присутствия,
                        отправьте
                        видео-кружочек в телеграм</p>
                    <a target="_blank" href="https://t.me/katrina0912">
                        <img :class="$style['regret__container--content__img']" src="/images/telegram.svg"
                            alt="telegram icon">
                    </a>
                </div>
                <img :class="$style['regret__container--paper-clip']" src="/images/paper-clip.svg" alt="pic">
            </div>
        </div>


        <div class="cheers" :class="$style['cheers__container']">
            <!-- <img src="/images/cheers-pic.jpg" alt="pic"> -->
            <img class="cheers-left" :class="$style['cheers__container--left']" src="/images/glass.svg" alt="cheers">
            <img class="cheers-right" :class="$style['cheers__container--right']" src="/images/glass.svg" alt="cheers">
            <div class="cheers-text" :class="$style['cheers__container--text']">Cheers!</div>
            </div>

            <div class="end" :class="$style['end__container']">
                <div class="end__image" :class="$style['end__container--image']">
                    <img src="/images/1.jpg" alt="pic">
                </div>
                <div class="end__text" :class="$style['end__container--text']">
                    <h2>With</h2>
                    <span>Love</span>
                </div>
                <div class="end__names" :class="$style['end__container--names']">
                    <h3>Екатерина и Сергей</h3>
                </div>
            </div>
        </div>
</template>

<script lang="ts" setup>
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

const letterText = ref('')

const fullText = `Случилось невероятное!<br>Наша безграничная любовь дала повод собрать всех родных и близких вместе.<br><br><br>Приглашаем Вас отметить этот особенный день - день нашей свадьбы!`

const wishes = [
    {id: 1, wish: 'Мы мечтаем обнять каждого гостя, поэтому с особой благодарностью примем ваши пожелания в конвертах!'},
    { id: 2, wish: 'Пусть наш праздник расцветёт букетами из роз, пионов или гортензий — искренних спутников нежности. Лишь аромат лилий, как давний знакомый, остаётся за дверью этого дня.'},
    {id: 3, wish: 'Ваша улыбка, ваш смех, ваши искренние поздравления – вот что сделает наш день по-настоящему волшебным. До встречи на празднике!'},
]


onMounted(() => {
    gsap.registerPlugin(ScrollTrigger)

    let index = 0
    let typingInterval: number | undefined

    ScrollTrigger.create({
        trigger: '.letter',
        start: 'top 5%',
        once: true,
        onEnter: () => {
            typingInterval = window.setInterval(() => {
                if (index < fullText.length) {
                    letterText.value += fullText[index]
                    index++
                } else {
                    clearInterval(typingInterval)
                }
            }, 40)
        }
    })

    gsap.fromTo('.header__image', {
       scale: 1
    },
    {
        scale: 1.5,
        scrollTrigger: {
            trigger: '.header',
            start: 'top 5%',
            end: 'center top',
            scrub: 'true',
            toggleActions: 'play none none none'
        }
    });

    gsap.fromTo('.header__text', {
       opacity: 1
    },
    {
        opacity: 0,
        scrollTrigger: {
            trigger: '.header__text',
            start: 'top',
            end: 'center',
            scrub: 'true',
            toggleActions: 'play none none none'
        }
    });

    gsap.fromTo('.letter', {
       opacity: 1
    },
    {
        opacity: 0,
        scrollTrigger: {
            trigger: '.letter',
            start: 'center',
            end: 'bottom',
            scrub: 'true',
            toggleActions: 'play none none none',
        }
    });

    // gsap.fromTo('.invent', {
    //    opacity: 1
    // },
    // {
    //     opacity: 0,
    //     scrollTrigger: {
    //         trigger: '.invent',
    //         start: 'top',
    //         end: 'bottom',
    //         scrub: 'true',
    //         toggleActions: 'play none none none',
    //     }
    // });

    gsap.fromTo('.line', {
       opacity: 1,
       scale: 1
    },
    {
        opacity: 0,
        scale: 0.2,
        scrollTrigger: {
            trigger: '.line',
            start: 'center 10%',
            end: 'bottom',
            scrub: 'true',
            toggleActions: 'play none none none'
        }
    });

    gsap.fromTo('.heart__image', 
    {
        y: '-30%'
    },
    {
        y: '0%', 
        scrollTrigger: {
            trigger: '.heart',
            start: 'top 15%',
            end: 'center',
            scrub: 'true',
            toggleActions: 'play none none none'
        }
    });

    gsap.fromTo('.cheers-left', {
      x:0,
      y: 0,
      rotate: 0
    },
    {
        x: 118,
        y: 400,
        rotate:50,
        scrollTrigger: {
            trigger: '.cheers',
            start: 'top top',
            end: 'center top',
            scrub: 'true',
            toggleActions: 'play none none none'
        }
    });

    gsap.fromTo('.cheers-right', {
      x:0,
      y: 0,
      rotate: 0
    },
    {
        x: -118,
        y: 400,
        rotate: -50,
        scrollTrigger: {
            trigger: '.cheers',
            start: 'top top',
            end: 'center top',
            scrub: 'true',
            toggleActions: 'play none none none'
        }
    });

    gsap.fromTo('.cheers-text', {
      opacity: 0,
    },
    {   
        opacity: 1,
        scrollTrigger: {
            trigger: '.cheers',
            start: 'center 10%',
            end: 'bottom 100%',
            scrub: 'true',
            toggleActions: 'play none none none'
        }
    });
})
</script>

<style lang="scss" scoped>
.block-paddings {
    margin: 20vw 0;
    height: 100vh;
}

.cursor {
  display: inline-block;
  width: 1px;
  background-color: black;
  animation: blink 1s step-end infinite;
}

@keyframes blink {
  from, to {
    background-color: transparent;
  }
  50% {
    background-color: black;
  }
}
</style>

<style lang="scss" module>

.main {
    overflow: hidden;
}

.header__container {
    height: 85vh;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}
.bg-text {
    position: relative;
    z-index: 1;
    overflow: hidden;
    &-back {
        font-family: 'special';
        font-size: 9.5vw;
        transform: rotate(5deg);
        color: rgb(183, 9, 9);
        margin: 0;
        padding: 0;
        padding: 5vw 0;
        position: relative;
        left: -60px;
        width: 150vw;
    }
}

.title-1 {
    padding-left: 30px;
    padding-bottom: 50px;
}

.title-2 {
    font-family: 'special';
    padding-top: 50px;
    margin-right: 3vw;
    display: flex;
    justify-content: flex-end;
    animation: startEffect 5s ease-in-out forwards;
}


.top-image {
    background: url('/images/loveyou.png') no-repeat center;
    background-size: cover;
    position: relative;
    z-index: 2;
    display: flex;
    justify-content: center;
    animation: startEffect 5s ease-in-out forwards;
    img {
        object-fit: cover;
        width: 350px;
        height: auto;
        transform: rotate(5deg);
        @media screen and (max-width: 550px) {
            width: 50%;
        }
    }
}

@keyframes startEffect {
    from{opacity: 0;}
    to{opacity: 1;}
}

.letter {
    &__container {
        position: relative;
        display: flex;
        justify-content: center;
        align-items: center;
        // height: 100vh;
    }

    &__image {
        position: relative;
        img {
            width: 100%;
        }
    }

    &__text {
        width: 55%;
        position: absolute;
        transform: translate(-50%, -50%);

        top: 41%;
        left: 50%;
        p {
            font-size: 4vw;
        }
    }
}

.info__container {
    margin: 100px 0;
    display: flex;
    flex-direction: column;
    gap: 50px;
}

.invent__container {
    display: flex;
    justify-content: start;
    align-items: center;
    flex-direction: column;
    text-align: center;
    h2 {
        font-family:'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
        color: rgb(183, 9, 9);
        font-size: 10vw;
        font-weight: 100;
    }
    p {
        font-size: 5vw;
    }
    span {
        font-size: 8vw;
    }
}

.line__container {
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    background: url('/images/2.jpg');
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;

    img {
        display: flex;
        justify-content: center;
        align-items: center;
        width: 40px;
        height: 100%;
        animation: heartBeat 0.9s infinite;
    }
    
}

.wishes__container {
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: start;
    align-items: center;
    &--title {
        text-align: center;
        font-family: 'names';
        color: rgb(183, 9, 9);
    }
    &--text {
        display: flex;
        flex-direction: column;
        justify-content: start;

        &__1, &__2, &__3 {
            display: flex;
            flex-direction: column;
            justify-content: center;
            margin: 10px 6vw;

            span {
                font-size: 10vw;
            }
            p {
                font-size: 4.5vw;
            }
        }
        &__2 {
            text-align: end;
        }
        &__3 {
            text-align: center;
        }
    }
}

.regret__container {
    position: relative;
    // height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: start;
    align-items: center;

    &--content {
        background: white;
        margin: 0 30px;
        padding: 20px;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: space-between;
        text-align: center;
        border-radius: 24px;
        p {
            font-size: 5vw;
        }
        img {
            width: 15vw;
        }
    }
    &--paper-clip {
        position: absolute;
        right: 30px;
        top: 0;
        width: 5vw;
    }
}

.cheers__container {
    position: relative;
    height: 80vh;
    display: flex;
    justify-content: space-between;
    align-items: start;
    // height: 100%;
    // img {
    //     transform: rotate(10deg);
    //     width: 70%;
    //     height: auto;
    //     padding: 60px;
    // }

    &--left, &--right {
        width: 100px;
    }

    &--text {
        font-family: 'names';
        font-size: 20vw;
        position: absolute;
        bottom: 100px;
        left: 25%;
        transform: rotate(-20deg);
    }
}

.end__container {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 100vh;
    // margin-top: 100px;
    &--image {
        img {
            width: 50%;
            height: 50vh;
            object-fit: cover;
        }
    }
    &--text {
        position: relative;
        text-align: end;
        margin-right: 15vw;
        h2 {
            font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
            font-weight: 600;
            font-size: 10vw;
        }
        span {
            font-family: 'names';
            font-size: 15vw;
            position: absolute;
            top: 20px;
            right: -10px;
        }
    }
    &--names {
        // margin-top: 100px;
        text-align: center;
        h3 {
            font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
            font-weight: 100;
        }
    }
}

@keyframes heartBeat {
    from {
        opacity: 0;
        scale: 1;
    }
    to {
        opacity: 1;
        scale: 1.3
    }
}</style>