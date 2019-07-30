# they-see-me-scrolling
Vue component for infinite scrolling

It will emit an event when it scrolls into view for you to hook on to.

* vertical scroll support
* horizontal scroll support
* slot for state visualization

## installation
use npm to get this into your app, from the root :

`npm i they-see-me-scrolling`

## code example
Add this component under a list of items, make sure to give it a reference.

```
<template>
    <div>
        <div v-bind="items"
            v-for="item in items"
        >
            <item :data="item"></item>
        </div>

        <they-see-me-scrolling
            ref="theyHating"
        >
            {{ this.bool ? "😎" : "🚓💨" }}
        </they-see-me-scrolling>
    </div>
</template>

<script>
    import TheySeeMeScrolling from 'they-see-me-scrolling';
    
    export default {
        ...
        components:{
            ... ,
            TheySeeMeScrolling
        },
        mounted: function(){
            this.$refs.theyHating.$on('they-see-me-scrolling', () => {
                // hook to your logic here
            });
        }
    }
</script>
```

Set up a listener for the 'they-see-me-scrolling'-event it will emit, and hook your logic to that.

## Thanks
@Chamillionaire