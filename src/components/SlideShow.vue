<template>
    <div class="slide-show-container">
        <transition :name="transitionName" mode="out-in">
            <div :key="currentRow + '-' + currentColumn" class="slide-wrapper">
                <template v-if="slideMatrix[currentRow][currentColumn].img">
                    <img :src="slideMatrix[currentRow][currentColumn].img" alt="Slide" class="slide-image" />
                </template>
                <template v-else>
                    <div class="slide-color"></div>
                </template>

                <div class="custom-component-wrapper">
                    <component :is="slideMatrix[currentRow][currentColumn].component" />
                </div>
            </div>
        </transition>

        <div class="nav-buttons">
            <template v-for="(direction, index) in ['left', 'up', 'down', 'right']">
                <button class="arrow-button" @click="changeSlide(direction)">
                    <div class="arrow-icon-container">
                        <svg viewBox="0 0 24 24" class="arrow-icon" :key="index">
                            <path :d="arrowPath(direction)" />
                        </svg>
                    </div>
                </button>
            </template>
        </div>

        <div class="progress-bar">
            <div class="progress" :style="{ width: progressPercentage + '%' }"></div>
        </div>
    </div>
</template>
  
<script>
import CustomComponents1 from "./CustomComponents1.vue"
import CustomComponents2 from "./CustomComponents2.vue"
import CustomComponents3 from "./CustomComponents3.vue"
import CustomComponents4 from "./CustomComponents4.vue"
export default {
    name: "SlideShow",
    components: {
        CustomComponents1,
        CustomComponents2,
        CustomComponents3,
        CustomComponents4,
    },
    props: {
        slideMatrix: Array,
    },
    data() {
        return {
            currentRow: 0,
            currentColumn: 0,
            transitionName: "slide-left",
            autoplay: true,
        };
    },
    mounted() {
        this.init();
        window.addEventListener("keydown", this.handleKeydown);
    },
    beforeUnmount() {
        window.removeEventListener("keydown", this.handleKeydown);
    },
    computed: {
        progressPercentage() {
            const totalSlides = this.slideMatrix.flat().length;
            const currentIndex = this.currentRow * this.slideMatrix[0].length + this.currentColumn;
            return ((currentIndex + 1) / totalSlides) * 100;
        },
    },
    methods: {
        init() {
            this.startAutoplay();
        },
        changeSlide(direction) {
            this.stopAutoplay();
            switch (direction) {
                case "left":
                    this.currentRow = 0;
                    this.currentColumn =
                        (this.currentColumn - 1 + this.slideMatrix[this.currentRow].length) %
                        this.slideMatrix[this.currentRow].length;
                    this.transitionName = "slide-left";
                    break;
                case "right":
                    this.currentRow = 0;
                    this.currentColumn = (this.currentColumn + 1) % this.slideMatrix[this.currentRow].length;
                    this.transitionName = "slide-right";
                    break;
                case "up":
                    this.currentRow =
                        (this.currentRow - 1 + this.slideMatrix.length) % this.slideMatrix.length;
                    this.transitionName = "slide-up";
                    break;
                case "down":
                    this.currentRow = (this.currentRow + 1) % this.slideMatrix.length;
                    this.transitionName = "slide-down";
                    break;
            }
            this.startAutoplay();
        },
        arrowPath(direction) {
            switch (direction) {
                case 'left':
                    return "M15.41 7.41L14 6l-6 6 6 6 1.41-1.41L10.83 12z";
                case 'up':
                    return "M7.41 15.41L12 10.83l4.59 4.58L18 14l-6-6-6 6z";
                case 'down':
                    return "M7.41 8.59L12 13.17l4.59-4.58L18 10l-6 6-6-6z";
                case 'right':
                    return "M10 6L8.59 7.41 13.17 12l-4.58 4.59L10 18l6-6z";
                default:
                    return "";
            }
        },
        handleKeydown(event) {
            switch (event.key) {
                case "ArrowLeft":
                    this.changeSlide("left");
                    break;
                case "ArrowRight":
                    this.changeSlide("right");
                    break;
                case "ArrowUp":
                    this.changeSlide("up");
                    break;
                case "ArrowDown":
                    this.changeSlide("down");
                    break;
            }
        },
        startAutoplay() {
            if (this.autoplay) {
                this.interval = setInterval(() => {
                    this.changeSlide("right");
                }, 5000);
            }
        },
        stopAutoplay() {
            clearInterval(this.interval);
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
    width: 100vw;
    height: 100vh;
}

.slide-wrapper {
    position: relative;
    width: 100vw;
    height: 100vh;
}

.slide-color {
    background-color: rgb(45, 45, 45);
    position: absolute;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
}

.slide-image {
    position: absolute;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    object-fit: cover;
}

.nav-buttons {
    position: absolute;
    bottom: 20px;
    right: 20px;
    display: flex;
    flex-direction: column;
    gap: 5px;
    z-index: 1;
}

.arrow-button {
    border: none;
    background: transparent;
    cursor: pointer;
    padding: 5px;
    outline: none;
}

.arrow-icon {
    color: #42affa;
    fill: currentColor;
    width: 75px;
    height: 75px;
}

.arrow-button.up {
    border: none;
    background: transparent;
    bottom: 100%;
    left: 50%;
    transform: translate(100px, -100%);
}

.arrow-button.down {
    border: none;
    background: transparent;
    top: 100%;
    left: 50%;
    transform: translate(100px, -100%);
}

.arrow-button.left {
    border: none;
    background: transparent;
    right: 100%;
    top: 50%;
    transform: translate(100px, -50%);
}

.arrow-button.right {
    border: none;
    background: transparent;
    left: 100%;
    top: 50%;
    transform: translate(-100px, -50%);
}

.custom-component-wrapper {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 50%;
    height: 60%;
    border: 2px solid #000000;
    border-radius: 10px;
    background-color: rgba(255, 255, 255);
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 1rem;
}

.progress-bar {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 4px;
    background-color: rgba(255, 255, 255, 0.5);
}

.progress {
    height: 100%;
    background-color: #007bff;
    transition: width 0.5s ease;
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

  