<template>
  <div class="hello" @click="redraw">
    <h1>{{ msg }}</h1>
    <h2>Gotta Catch Em All!</h2>
    <canvas id="canvasInst" > </canvas>
  </div>
</template>

<script>
export default {
    name: 'hello',
    data() {
        return {
            msg: 'Welcome to Pokémon Center',
            ctx: {},
            base: [[0, 630], [0, 450]],
            To: [[], []],
            center: [0, 500],
            radius: 0
        };
    },
    mounted() {
        var canDom = document.querySelector('#canvasInst');
        canDom.width = '1500';
        canDom.height = '1000';
        this.ctx = canDom.getContext('2d');
        // this.drawRibbon();
        this.drawPolkaDot();
    },
    methods: {
        drawRibbon() {
            // this.draw(this.base[0], this.base[1], this.To);

            for (var i = 0; i < 17; i++) {
                this.updateTo();
                this.draw(this.base[0], this.base[1], this.To, 'rgba(0,' + (i * 16) + ',255,0.5)');
                this.base = this.getNewBase(this.base[0], this.base[1]);
            }
        },
        draw: function([x1, y1], [x2, y2], [x3, y3], color = 'hsla(300,50%,50%,1)', type = 'fill') {
            this.ctx.beginPath();
            this.ctx.moveTo(x1, y1);
            this.ctx.lineTo(x2, y2);
            this.ctx.lineTo(x3, y3);
            this.ctx[type + 'Style'] = color;
            this.ctx.closePath();
            this.ctx[type]();
        },
        RandomNumBoth(Min = 0, Max = 200) {
            var Range = Max - Min;
            var Rand = Math.random();
            var num = Min + Math.round(Rand * Range); // 四舍五入
            return num;
        },
        getNewBase([x1, y1], [x2, y2]) {
            let newbase = x1 >= x2 ? [x1, y1] : [x2, y2];
            return [newbase, this.To];
        },
        updateTo() {
            let newY = 0;
            while (1) {
                newY = this.base[1][1] + this.RandomNumBoth(-100, 100);
                if (newY > 0 && newY < 780) {
                    break;
                }
            }
            this.To = [this.base[1][0] + this.RandomNumBoth(), newY];
        },
        redraw() {
            this.ctx.clearRect(0, 0, 2000, 2000);
            this.base = [[0, 630], [0, 450]];
            this.center = [0, 500];
            // this.drawRibbon();
            this.drawPolkaDot();
        },
        drawCircle(center, radius, color) {
            this.ctx.beginPath();
            this.ctx.fillStyle = color;
            this.ctx.arc(center[0], center[1], radius, 0, 2 * Math.PI);
            this.ctx.fill();
        },
        drawPolkaDot() {
            for (var i = 0; i < 20; i++) {
                // this.drawCircle(this.center, this.radius, 'rgba(' + (i * 16) + ',255, 0,0.5)');

                this.drawCircle(this.center, this.radius, 'rgba(255,' + (i * 16) + ',0,0.5)');
                this.updateCircleParam();
            }
        },
        updateCircleParam() {
            let newY = 0;
            let newCenter;
            while (1) {
                newY = this.center[1] + this.RandomNumBoth(-100, 100);
                if (newY > 0 && newY < 780) {
                    break;
                }
            }
            newCenter = [this.center[0] + this.RandomNumBoth(this.radius, this.radius + 70), newY];
            this.radius = Math.sqrt(Math.abs(newCenter[0] - this.center[0]) * Math.abs(newCenter[0] - this.center[0]) + Math.abs(newCenter[1] - this.center[1]) * Math.abs(newCenter[1] - this.center[1])) - this.radius;
            this.center = newCenter;
        }
    }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" rel="stylesheet/scss">
    .hello {
        #canvasInst {
            // width: 100%;
            // height: 100%;
            position: absolute;
            top: 0;
            left: 0;
        }
    }
</style>
