<template>
    <div ref="theySeeMeScrolling">
        <slot></slot>
    </div>
</template>

<script>
    export default {
        name: "TheySeeMeScrolling",

        data() {
            return {
                theyHating: false,
                position: {
                    top: 0,
                    left: 0,
                    bottom: 0,
                    right: 0
                }
            }
        },

        created () {
            window.addEventListener('scroll', this.setPosition);
            window.addEventListener('resize', this.setPosition);
        },

        destroyed () {
            window.removeEventListener('scroll', this.setPosition);
            window.removeEventListener('resize', this.setPosition);
        },

        methods: {
            setPosition: function() {
                const position = {
                    x: 0,
                    y: 0
                };

                let el = this.$refs.theySeeMeScrolling;

                while (el.offsetParent) {
                    // for all elements with a parent
                    position.x += (el.offsetLeft - el.scrollLeft + el.clientLeft);
                    position.y += (el.offsetTop - el.scrollTop + el.clientTop);

                    el = el.offsetParent;
                }

                // deal with browser quirks with body/window/document and page scroll
                let xScroll = el.scrollLeft || document.documentElement.scrollLeft;
                let yScroll = el.scrollTop || document.documentElement.scrollTop;

                position.x += (el.offsetLeft - xScroll + el.clientLeft);
                position.y += (el.offsetTop - yScroll + el.clientTop);

                this.position = {
                    top: position.y,
                    bottom: position.y + this.$refs.theySeeMeScrolling.clientHeight,
                    left: position.x,
                    right: position.x + this.$refs.theySeeMeScrolling.clientWidth
                }
            }
        },
        
        watch:{
            theyHating: function (newState, oldState) {
                if(
                    newState !== oldState &&
                    newState === true
                ){
                    this.$emit('they-see-me-scrolling');
                }
            },
            position: function (newState, oldState) {
                this.theyHating =
                    (oldState.top !== newState.top &&
                        newState.top > 0 &&
                        newState.top < window.innerHeight) ||
                    (oldState.bottom !== newState.bottom &&
                        newState.bottom > 0 &&
                        newState.bottom < window.innerHeight) ||
                    (oldState.left !== newState.left &&
                        newState.left > 0 &&
                        newState.left < window.innerWidth) ||
                    (oldState.right !== newState.right &&
                        newState.right > 0 &&
                        newState.right < window.innerWidth)
            }
        }
    }
</script>

<style scoped>

</style>