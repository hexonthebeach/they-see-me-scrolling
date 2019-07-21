<template>
    <div ref="theySeeMeScrolling"></div>
</template>

<script>
    export default {
        name: "TheySeeMeScrolling",

        data() {
            return {
                theyHating: false
            }
        },

        created () {
            window.addEventListener('scroll', this.handleScroll);
            window.addEventListener('resize', this.handleScroll);
        },

        destroyed () {
            window.removeEventListener('scroll', this.handleScroll);
            window.removeEventListener('resize', this.handleScroll);
        },

        methods: {
            handleScroll: function () {
                /* they hating when they see me scrolling */
                this.theyHating = window.innerHeight > this.getPosition().y
            },

            getPosition: function() {
                let position = {
                    x: 0,
                    y: 0
                };

                let el = this.$refs.theySeeMeScrolling;

                while (el.offsetParent) {
                    // for all elements with a parent
                    position.x += (el.offsetLeft - el.scrollLeft + el.clientLeft);
                    position.y += (el.offsetTop - el.scrollTop + el.clientTop);

                    el = el.offsetParent
                }

                // deal with browser quirks with body/window/document and page scroll
                let xScroll = el.scrollLeft || document.documentElement.scrollLeft;
                let yScroll = el.scrollTop || document.documentElement.scrollTop;

                position.x += (el.offsetLeft - xScroll + el.clientLeft);
                position.y += (el.offsetTop - yScroll + el.clientTop);

                return position;
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
            }
        }
    }
</script>

<style scoped>

</style>