<template>
    <div>
        <link href="https://fonts.googleapis.com/css?family=Raleway:200,100,400" rel="stylesheet" type="text/css" />
        <h1>Blog Posts | 
            <span class="txt-rotate">&nbsp;1</span>
        </h1>
    </div>
</template>

<script>
export default {
    data() {
        return {
            categoryString: ''
        }
    },
    props: {
        categories: {
            type: Array,
            required: true
        },
        animateDuration: {
            type: Number,
            default: 1000
        }
    },
    mounted() {
        this.$nextTick().then(() => {
            var TxtRotate = function(el, toRotate, period) {
                this.toRotate = toRotate;
                this.el = el;
                this.loopNum = 0;
                this.period = parseInt(period, 10) || 2000;
                this.txt = '';
                this.tick();
                this.isDeleting = false;
            };

            TxtRotate.prototype.tick = function() {
                var i = this.loopNum % this.toRotate.length;
                var fullTxt = this.toRotate[i];

                if (this.isDeleting) {
                    this.txt = fullTxt.substring(0, this.txt.length - 1);
                } else {
                    this.txt = fullTxt.substring(0, this.txt.length + 1);
                }

                this.el.innerHTML = '<span class="wrap">'+this.txt+'</span>';

                var that = this;
                var delta = 300 - Math.random() * 100;

                if (this.isDeleting) { delta /= 2; }

                if (!this.isDeleting && this.txt === fullTxt) {
                    delta = this.period;
                    this.isDeleting = true;
                } else if (this.isDeleting && this.txt === '') {
                    this.isDeleting = false;
                    this.loopNum++;
                    delta = 500;
                }

                setTimeout(function() {
                    that.tick();
                }, delta);
            };
        
            var elements = document.getElementsByClassName('txt-rotate');

            var toRotate = JSON.stringify(this.categories);
            var period = this.animateDuration;

            if (toRotate) { new TxtRotate(elements[0], JSON.parse(toRotate), period); }
        })
    }
}
</script>

<style lang="scss">


.txt-rotate {
    text-align: center;
    text-transform: uppercase;
    color: $color-pacific;
    
    > .wrap { 
        border-right: 0.08em solid #666 
    }
}
</style>