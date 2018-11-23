<template>
  <div class="container">
    <div class="col1">
      <h1>MARWEN AYARI</h1>
      <h3>ENTREPRENEUR, <br>JAVASCRIPT DEVELOPER</h3>
      <a href="https://www.linkedin.com/in/marwenayari/" target="_blank"><img src="../assets/linkedin.png" alt=""></a>
      <a href="https://github.com/marwenayari" target="_blank"><img src="../assets/github-sign.png" alt=""></a>
    </div>
    <div class="col2">
      <img src="../assets/marwenayari.png" alt="">
    </div>
  </div>
</template>

<script>
const THREE = require('three');

export default {
  name: 'HelloWorld',
  props: {
  },
  data : function(){
    return{
      camera: null,
      scene: null, 
      renderer: null,
      geometry: null, 
      material: null, 
      mesh: null,
      circleColor : Math.random() * 0x42b983 + 0x42b983,
    }
  },
  created : function (){
    this.init();
    this.animate();
  },
  methods : {
    init : function() {
    this.camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 1, 10000 );
    this.camera.position.z = 1000;

    this.scene = new THREE.Scene();

    this.renderer = new THREE.WebGLRenderer( { antialias: true } );
    this.renderer.setSize( window.innerWidth, window.innerHeight );
    this.renderer.setClearColor(0xf9f9f9);
    document.body.appendChild( this.renderer.domElement );

    this.camera.lookAt(new THREE.Vector3(0,0,0));

        this.geometry = new THREE.CircleGeometry( 0.5, 32);
        //this.material = new THREE.MeshBasicMaterial( { color: this.circleColor} );
    
        for ( var i = 0; i < 150; i ++ ) {

          this.circleColor = Math.random() * 0x42b983 + 0x42b983;
          this.material = new THREE.MeshBasicMaterial( { color: this.circleColor} );
          var circle = new THREE.Mesh( this.geometry, this.material );
          circle.position.x = Math.random() * 2500 - 1500;
          circle.position.y = Math.random() * 2500 - 1500;
          circle.position.z = Math.random() * 2500 - 1500;
          circle.scale.x = circle.scale.y = Math.random() * 12 + 5;
          this.scene.add( circle );

          this.geometry.vertices.push( new THREE.Vector3( circle.position ) );
        }
          
          //var line = new THREE.Line( this.geometry, new THREE.LineBasicMaterial( { color: 0xfffffff, opacity: 1 } ) );
          //this.scene.add( line );

    },
    animate : function() {
    requestAnimationFrame( this.animate );

    this.renderer.render( this.scene, this.camera );
    document.addEventListener( 'mousemove', this.onMouseMove, false );

    },
    onMouseMove : function(event){
      var mouseX = (event.clientX - window.innerWidth/2) / window.innerWidth/2;
      var mouseY = (event.clientY - window.innerHeight/2) / window.innerHeight/2;
      this.camera.position.x = Math.sin(mouseX * Math.PI) * 1000;
      this.camera.position.y = - Math.sin(mouseY * Math.PI) * 1000;
      this.camera.lookAt(new THREE.Vector3(0,0,0));
      this.renderer.render( this.scene, this.camera );
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.container{
  margin: calc(50vh - 100px) 0 0;
  color: #42b983;
  position: absolute;
  width: 100%;
}
.container h1{
  margin: 0;
}
.container h3{
  margin: 0;
  color: black;
}
.col1, .col2{
  width: 50%;
  float: left;
}
.col1{
  margin-top: 35px;
}
.container .col1 img{
  width: 32px;
  margin: 5px;
}
.container .col2 img{
  object-fit: cover; 
  width: 200px;
  height: 200px;
  border: 2px solid #fff;
  border-radius: 50%;
}
canvas{
  bottom: 0;
}
</style>
