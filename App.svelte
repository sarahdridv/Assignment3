<script>
  import { scaleOrdinal } from 'd3-scale'
  import { schemePaired } from 'd3-scale-chromatic'
  import { munis } from './munis.js'
  import { Graphic, PolygonLayer, fitScales } from '@snlab/florence'
  import DataContainer from '@snlab/florence-datacontainer'
  
  const munisContainer = new DataContainer(munis)
  const geoScales = fitScales(munisContainer.domain("$geometry"))

</script>

<div class="graph">
  <div class="main-chart">
    <Graphic
      {...geoScales}
      flipY
      >
      <PolygonLayer 
      geometry={munisContainer.column("$geometry")}/>
      
    </Graphic>
  </div>
</div>

<style>

</style>