<template>
    <div ref="container" class="new_marquee" :style="boxConfig">
        <div
            ref="animation"
            :class="['animation', direction]"
            :style="{ animationDuration: moveSpeed + 's' }"
        >
            <div class="package">
                <slot name="childList"></slot>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        direction: {
            type: String,
            default: 'up'
        },
        speed: {
            type: Number,
            default: 0
        }
    },
    data() {
        return {
            containerHeight: 'auto',
            containerWidth: 'auto',
            moveSpeed: 0
        };
    },
    computed: {
        boxConfig() {
            let style = {};
            if (this.direction === 'left' || this.direction === 'right') {
                style = { width: this.containerWidth + 'px' };
            } else {
                style = { height: this.containerHeight + 'px' };
            }
            return style;
        }
    },
    mounted() {
        this.checkNodeRender();
    },
    methods: {
        checkNodeRender() {
            const direction =
                this.direction === 'left' || this.direction === 'right'
                    ? 'clientWidth'
                    : 'clientHeight';
            this.containerSizeHandle(direction);
        },
        containerSizeHandle(direction) {
            const containerSize = this.$refs.container[direction];
            const animationSize = this.$refs.animation[direction];
            if (animationSize > 0) {
                this.containerWidth = containerSize;
                this.containerHeight = containerSize;
                this.newNode();
                this.countSpeed(direction);
            } else {
                setTimeout(() => {
                    this.checkNodeRender();
                }, 300);
            }
        },
        newNode() {
            const father = this.$refs.animation;
            const newNode = father.firstChild.cloneNode(true);
            father.appendChild(newNode);
        },
        countSpeed(direction) {
            const size = this.$refs.animation[direction];
            if (this.speed === 0) {
                return (this.moveSpeed = size / 30);
            }
            if (this.speed > 0) {
                this.moveSpeed = size / 30 / this.speed;
            } else {
                this.moveSpeed = (size * Math.abs(this.speed)) / 30;
            }
        }
    }
};
</script>

<style lang="scss" scoped>
.new_marquee {
    overflow: hidden;
    .animation {
        position: relative;
        width: 100%;
    }
    .up {
        animation: roll-up 0s linear infinite normal;
    }
    .down {
        animation: roll-up 0s linear infinite normal;
        animation-direction: reverse;
    }
    .left {
        display: flex;
        animation: roll-left 0s linear infinite normal;
    }
    .right {
        display: flex;
        animation: roll-left 0s linear infinite normal;
        animation-direction: reverse;
    }
}
@keyframes roll-up {
    0% {
        -webkit-transform: translateY(0);
        transform: translateY(0);
    }
    100% {
        -webkit-transform: translateY(-50%);
        transform: translateY(-50%);
    }
}
@keyframes roll-left {
    0% {
        -webkit-transform: translateX(0);
        transform: translateX(0);
    }
    100% {
        -webkit-transform: translateX(-50%);
        transform: translateX(-50%);
    }
}
</style>
