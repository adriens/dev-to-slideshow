<template>
    <div class="slide-show-container">
        <transition :name="transitionName" mode="out-in">
            <img :src="slideData[currentSlide].img" :key="currentSlide" alt="Slide" class="slide-image" />
        </transition>
        <div class="nav-buttons">
            <button @click="changeSlide('left')">Gauche</button>
            <button @click="changeSlide('up')">Haut</button>
            <button @click="changeSlide('down')">Bas</button>
            <button @click="changeSlide('right')">Droite</button>
        </div>
    </div>
</template>
  
<script>
export default {
    name: "SlideShow",
    props: {
        slideData: Array,
    },
    data() {
        return {
            currentSlide: 0,
            transitionName: "slide-left",
        };
    },
    methods: {
        changeSlide(direction) {
            switch (direction) {
                case "left":
                    this.currentSlide =
                        (this.currentSlide - 1 + this.slideData.length) %
                        this.slideData.length;
                    this.transitionName = "slide-left";
                    break;
                case "right":
                    this.currentSlide = (this.currentSlide + 1) % this.slideData.length;
                    this.transitionName = "slide-right";
                    break;
                case "up":
                    this.currentSlide =
                        (this.currentSlide - 1 + this.slideData.length) %
                        this.slideData.length;
                    this.transitionName = "slide-up";
                    break;
                case "down":
                    this.currentSlide = (this.currentSlide + 1) % this.slideData.length;
                    this.transitionName = "slide-down";
                    break;
            }
        },
    },
};
</script>
  
<style>
.slide-show-container {
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100vh;
}

.slide-image {
    max-width: 100%;
    max-height: 100vh;
    object-fit: cover;
}

.nav-buttons {
    margin-top: 10px;
    display: flex;
    gap: 5px;
}

.slide-left-enter-active,
.slide-right-enter-active,
.slide-up-enter-active,
.slide-down-enter-active {
    transition: all 0.3s ease;
}

.slide-left-leave-active,
.slide-right-leave-active,
.slide-up-leave-active,
.slide-down-leave-active {
    transition: all 0.3s ease;
}

.slide-left-enter,
.slide-left-leave-to {
    transform: translateX(100%);
}

.slide-left-leave,
.slide-left-enter-to {
    transform: translateX(-100%);
}

.slide-right-enter,
.slide-right-leave-to {
    transform: translateX(-100%);
}

.slide-right-leave,
.slide-right-enter-to {
    transform: translateX(100%);
}

.slide-up-enter,
.slide-up-leave-to {
    transform: translateY(100%);
}

.slide-up-leave,
.slide-up-enter-to {
    transform: translateY(-100%);
}

.slide-down-enter,
.slide-down-leave-to {
    transform: translateY(-100%);
}

.slide-down-leave,
.slide-down-enter-to {
    transform: translateY(100%);
}
</style>

  