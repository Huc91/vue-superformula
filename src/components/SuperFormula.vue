<template>
    <div class="super-formula-container">
        <svg viewBox="0 0 500 500" xmlns="http://www.w3.org/2000/svg">

            <polygon
            :points="points"
            fill="none"
            stroke="black"
            />

        </svg>
    </div>
</template>

<script>
/* eslint-disable */
function superFormula(x = 1, y = 1, shapeCount = 1, size){

    const N1 = y,
          N2 = y,
          N3 = y,
          A  = 1,
          B  = 1,
          C  = 1,
          M  = x;
    function superShape( angle ){

        const T1 = Math.pow( ( Math.abs( Math.cos( M * angle / 4 ) / A ) ), N2 );
        const T2 = Math.pow( ( Math.abs( Math.sin( M * angle / 4 ) / B ) ), N3 );
        let r = Math.pow( ( T1 + T2 ), ( 1 / N1 ) );
        return r;

    }
    function createPoints(){

        let points = [];
        for ( let angle = 0; angle < 2 * shapeCount * Math.PI ; angle += 0.01 ){

            const R = superShape( angle );

            if ( Math.abs( R ) === 0 ){

                const POINT = {
                    x: 0,
                    y: 0
                };
                points.push( POINT );

            } else {

                const MY_R = 1 / R;
                const POINT = {
                  x: MY_R * Math.cos( angle ) * size.radius + size.offset,
                  y: MY_R * Math.sin( angle ) * size.radius + size.offset
                };
                points.push( POINT );

            }


        }
        return points;

    }

    function convertPoints( points ){

      const POINTS = points;
      const MAP_POINTS = POINTS.map( point => {

        const STR_POINT = `${point.x},${point.y}`;
        return STR_POINT;

      })
      return MAP_POINTS.join(' ');

    }
    return convertPoints( createPoints() );
}
export default {
    name: 'SuperFormula',
    data() {

        return {

        }

    },
    computed:{

      pointsFromMouse(){
        return superFormula( ( this.mouseX / 150 ), ( 150 / this.mouseY ), this.shapeCount, this.size );
      },
      pointsFromGyro(){
        return superFormula( ( this.deviceOrientation.gamma / 6 ), ( this.deviceOrientation.beta / 6 ), this.shapeCount, this.size );
      },
      points(){
          if (this.deviceOrientation.hasOrientation)
            return this.pointsFromGyro;
          else
            return this.pointsFromMouse;
      },

    },
    props: {
      mouseX: {
        type: Number,
        default: 0,
      },
      mouseY: {
        type: Number,
        default: 0,
      },
      deviceOrientation: {
          type: Object,
          default: () => {},
      },
      shapeCount: {
        type: Number,
        default: 1,
      },
      size: {
        type: Object,
        default: { radius: 50, offset: 100 },
      }
    },
    mounted(){ 

    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
