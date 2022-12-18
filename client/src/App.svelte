<script>
  import OpenSeadragon from "openseadragon"
  import './openseadragon-svg-overlay.js'
  import * as d3 from 'd3'
  import { onMount } from "svelte"
  
  onMount(() =>{
    let viewer = new OpenSeadragon({
        id: "view",
        prefixUrl: "//openseadragon.github.io/openseadragon/images/",
        /*tileSources: "http://flask:5000/S-14-1697-B.mrxs.dzi",*/
        /*tileSources: tileSourceFromData(dziData, dziFilesUrl),*/
        tileSources: {
          Image: {
            xmlns: "http://schemas.microsoft.com/deepzoom/2008",
            Url: "http://localhost:3000/S-14-1697-B.mrxs_files/",
            ajaxWithCredentials : false,
            crossOriginPolicy: "Anonymous",
            Format: "jpeg",
            Overlap: "1",
            TileSize: "254",
            Size: {
              Height: "203594",
              Width: "90765"
            }
          }
        },
        showNavigator: true,
        showRotationControl: true,
        animationTime: 0.5,
        blendTime: 0.1,
        constrainDuringPan: true,
        maxZoomPixelRatio: 2,
        minZoomLevel: 1,
        visibilityRatio: 1,
        zoomPerScroll: 2,
        timeout: 120000,
    });
    viewer.addHandler("open", function() {
        // To improve load times, ignore the lowest-resolution Deep Zoom
        // levels.  This is a hack: we can't configure the minLevel via
        // OpenSeadragon configuration options when the viewer is created
        // from DZI XML.
        viewer.source.minLevel = 8;
    });
    let overlay = viewer.svgOverlay();
    overlay.node().parentNode.style.pointerEvents = 'none';

    let coord_ano = 
    d3.select(overlay.node()).append("polygon")
    .attr('id','coord_ano')
    .attr('points',"0.512534,0.4032 0.644,0.409 0.66,0.571 0.505,0.55")
    .style('fill','#f00')
    .style('transition', "all ease 0.5s")
    .style("opacity", 0.5);
  })

  // Overlay Toggle
  let is_toggle = true;
  function toggle_overlay(){
    is_toggle = !is_toggle
    if (is_toggle) {
      d3.select('#coord_ano').style('opacity',0.5)
    } else {
      d3.select('#coord_ano').style('opacity',0.0)
    }
  }
  

  


</script>
<h1> Svelte OpenSeadragon </h1>
<button on:click = {toggle_overlay}>Annotation</button>
<button on:click = {toggle_overlay}>Prediction</button>
<div id=view> </div>

<style>
  #view {
    position: fixed;
    left: 10%;
    top: 20%;
    width: 80%;
    height: 70%;
  }
</style>
