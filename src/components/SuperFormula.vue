<template>
    <div class="super-formula-container">
        <svg viewBox="0 0 500 500" xmlns="http://www.w3.org/2000/svg">

            <polygon :points="points" />

        </svg>
    </div>
</template>

<script>
/* eslint-disable */
export default {
    name: 'SuperFormula',
    data() {

        return {
          points : null
        }

    },
    props: {

    },
    mounted(){
      
        function superFormula(){

            const N1 = 1,
                  N2 = 1,
                  N3 = 1,
                  A  = 1,
                  B  = 1,
                  C  = 1;
            function superShape( angle ){

                let r = 1;
                return r;
              
            }
            function createPoints(){

                let points = [];
                for ( let angle = 0; angle < 2 * Math.PI; angle += 0.1 ){

                    const R = superShape( angle );
                    const POINT = {
                        x: R * Math.cos( angle ) * 100 + 100,
                        y: R * Math.sin( angle ) * 100 + 100
                    };
                    points.push( POINT );
                  
                }
                return points; 

            }

            function convertPoints( points ){

              const POINTS = points;
              const MAP_POINTS = POINTS.map( point => {
                const STR_POINT = `${point.x},${point.y}`;
                return STR_POINT;
              })
              console.log( MAP_POINTS.join(' ') )
              return MAP_POINTS.join(' ');
            }
            return convertPoints( createPoints() );
        };

        this.points = superFormula();

    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
