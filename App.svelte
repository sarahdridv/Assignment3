<script>
  import { scaleLinear } from 'd3-scale'
  import { csvParse, autoType } from 'd3-dsv'
  import { Graphic, PointLayer, XAxis, YAxis } from '@snlab/florence'
  import DataContainer from '@snlab/florence-datacontainer'

  let geodata
  let scaleX
  let scaleY
  let done = false

  async function loadCSV (url) {
    const response = await fetch(url)
    const data = await response.text()
    const dataParsed = csvParse(data, autoType)
    geodata = new DataContainer(dataParsed)
    scaleX = scaleLinear().domain(geodata.domain('EL_AV_ALS'))
    scaleY = scaleLinear().domain(geodata.domain('E_WR_P_00'))
    done = true
  }
  loadCSV('data/Geography.csv')
 
</script>

<div class="graph">
  <div class="main-chart">
    <Graphic
      {scaleX}
      {scaleY}
      >
      <PointLayer 
      x={geodata.column('EL_AV_ALS')}
      y={geodata.column('E_WR_P_00')}
      fill={'blue'}/>
    </Graphic>
  </div>
</div>

<style>
</style>