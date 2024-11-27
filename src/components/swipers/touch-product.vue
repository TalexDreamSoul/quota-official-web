<script setup>
import { Swiper } from 'swiper'
import * as kokomi from 'kokomi.js'
import * as THREE from 'three'
import { gsap } from 'gsap'
import SliderIndex from '~/components/thisai/SliderIndex.vue'
import SliderIntro from '~/components/thisai/SliderIntro.vue'
import SliderAnnounce from '~/components/thisai/SliderAnnounce.vue'
import SliderSlogan from '~/components/thisai/SliderSlogan.vue'

const vertexShader = `
uniform float iTime;
uniform vec2 iResolution;
uniform vec2 iMouse;

varying vec2 vUv;

varying vec3 vNormal;
varying vec4 vMvPosition;
varying vec3 vPosition;

uniform vec2 uMouse;
uniform float uRandom;
uniform float uLayerId;

// transform
mat2 rotation2d(float angle){
    float s=sin(angle);
    float c=cos(angle);
    
    return mat2(
        c,-s,
        s,c
    );
}

mat4 rotation3d(vec3 axis,float angle){
    axis=normalize(axis);
    float s=sin(angle);
    float c=cos(angle);
    float oc=1.-c;
    
    return mat4(
        oc*axis.x*axis.x+c,oc*axis.x*axis.y-axis.z*s,oc*axis.z*axis.x+axis.y*s,0.,
        oc*axis.x*axis.y+axis.z*s,oc*axis.y*axis.y+c,oc*axis.y*axis.z-axis.x*s,0.,
        oc*axis.z*axis.x-axis.y*s,oc*axis.y*axis.z+axis.x*s,oc*axis.z*axis.z+c,0.,
        0.,0.,0.,1.
    );
}

vec2 rotate(vec2 v,float angle){
    return rotation2d(angle)*v;
}

vec3 rotate(vec3 v,vec3 axis,float angle){
    return(rotation3d(axis,angle)*vec4(v,1.)).xyz;
}

vec3 distort(vec3 p){
    vec3 tx1=vec3(-uMouse.x*uRandom*.05,-uMouse.y*uRandom*.02,0.);
    p+=tx1;
    
    float angle=iTime*uRandom;
    p=rotate(p,vec3(0.,1.,0.),angle);
    
    vec3 tx2=vec3(-uMouse.x*uRandom*.5,-uMouse.y*uRandom*.2,0.);
    p+=tx2;
    
    p*=(.6-uLayerId*.5);
    
    return p;
}

void main(){
    vec3 p=position;
    vec3 N=normal;
    
    p=distort(p);
    N=distort(N);
    
    gl_Position=projectionMatrix*modelViewMatrix*vec4(p,1.);
    
    vUv=uv;
    
    vNormal=N;
    vMvPosition=modelViewMatrix*vec4(p,1.);
    vPosition=p;
}
`

const fragmentShader = `
uniform float iTime;
uniform vec2 iResolution;
uniform vec2 iMouse;

varying vec2 vUv;

varying vec3 vNormal;
varying vec4 vMvPosition;
varying vec3 vPosition;

uniform sampler2D uTexture;
uniform vec3 uLightPosition;
uniform vec3 uLightColor;
uniform float uRandom;
uniform vec2 uMouse;

// transform
mat2 rotation2d(float angle){
    float s=sin(angle);
    float c=cos(angle);
    
    return mat2(
        c,-s,
        s,c
    );
}

mat4 rotation3d(vec3 axis,float angle){
    axis=normalize(axis);
    float s=sin(angle);
    float c=cos(angle);
    float oc=1.-c;
    
    return mat4(
        oc*axis.x*axis.x+c,oc*axis.x*axis.y-axis.z*s,oc*axis.z*axis.x+axis.y*s,0.,
        oc*axis.x*axis.y+axis.z*s,oc*axis.y*axis.y+c,oc*axis.y*axis.z-axis.x*s,0.,
        oc*axis.z*axis.x-axis.y*s,oc*axis.y*axis.z+axis.x*s,oc*axis.z*axis.z+c,0.,
        0.,0.,0.,1.
    );
}

vec2 rotate(vec2 v,float angle){
    return rotation2d(angle)*v;
}

vec3 rotate(vec3 v,vec3 axis,float angle){
    return(rotation3d(axis,angle)*vec4(v,1.)).xyz;
}

// lighting
float saturate(float a){
    return clamp(a,0.,1.);
}

float diffuse(vec3 n,vec3 l){
    float diff=saturate(dot(n,l));
    return diff;
}

float specular(vec3 n,vec3 l,float shininess){
    float spec=pow(saturate(dot(n,l)),shininess);
    return spec;
}

float blendSoftLight(float base,float blend){
    return(blend<.5)?(2.*base*blend+base*base*(1.-2.*blend)):(sqrt(base)*(2.*blend-1.)+2.*base*(1.-blend));
}

vec3 blendSoftLight(vec3 base,vec3 blend){
    return vec3(blendSoftLight(base.r,blend.r),blendSoftLight(base.g,blend.g),blendSoftLight(base.b,blend.b));
}

// distort
vec2 distort(vec2 p){
    vec2 m=uMouse;
    
    p.x-=(uRandom-m.x*.8)*.5;
    p.y-=uRandom*.1-iTime*.1;
    
    p.x-=.25;
    p.y-=.5;
    p=rotate(p,uRandom);
    p*=2.;
    return p;
}

vec3 distortNormal(vec3 p){
    p*=vec3(-1.*uRandom*15.,-1.*uRandom*15.,30.5);
    return p;
}

// lighting
vec4 lighting(vec3 tex,vec3 normal){
    vec4 viewLightPosition=viewMatrix*vec4(uLightPosition,0.);
    vec3 N=normalize(normal);
    vec3 L=normalize(viewLightPosition.xyz);
    
    vec3 dif=tex*uLightColor*diffuse(N,L);
    
    vec3 C=-normalize(vMvPosition.xyz);
    vec3 R=reflect(-L,N);
    
    vec3 spe=uLightColor*specular(R,C,500.);
    
    vec4 lightingColor=vec4(dif+spe,.5);
    
    vec3 softlight=blendSoftLight(tex,spe);
    float dotRC=dot(R,C);
    float theta=acos(dotRC/length(R)*length(C));
    float a=1.-theta*.3;
    
    vec4 col=vec4(tex,a*.01)+vec4(softlight,.02)+(lightingColor*a);
    return col;
}

void main(){
    vec2 p=vUv;
    vec3 N=vNormal;
    
    p=distort(p);
    
    N=distortNormal(N);
    
    vec4 tex=texture2D(uTexture,p);
    
    vec4 col=tex;
    
    col=lighting(tex.xyz,N);
    
    gl_FragColor=col;
}
`

const vertexShader2 = `
uniform float iTime;
uniform vec2 iResolution;
uniform vec2 iMouse;

varying vec2 vUv;

void main(){
    vec3 p=position;
    gl_Position=projectionMatrix*modelViewMatrix*vec4(p,1.);
    
    vUv=uv;
}
`

const fragmentShader2 = `
uniform float iTime;
uniform vec2 iResolution;
uniform vec2 iMouse;

uniform sampler2D tDiffuse;

varying vec2 vUv;

uniform float uRGBShift;

vec4 RGBShift(sampler2D t,vec2 rUv,vec2 gUv,vec2 bUv){
    vec4 color1=texture2D(t,rUv);
    vec4 color2=texture2D(t,gUv);
    vec4 color3=texture2D(t,bUv);
    vec4 color=vec4(color1.r,color2.g,color3.b,color2.a);
    return color;
}

highp float random(vec2 co)
{
    highp float a=12.9898;
    highp float b=78.233;
    highp float c=43758.5453;
    highp float dt=dot(co.xy,vec2(a,b));
    highp float sn=mod(dt,3.14);
    return fract(sin(sn)*c);
}

void main(){
    vec2 p=vUv;
    
    vec4 col=vec4(0.);
    
    // RGB Shift
    float n=random(p+mod(iTime,1.))*.1+.5;
    vec2 offset=vec2(cos(n),sin(n))*.0025*uRGBShift;
    vec2 rUv=p+offset;
    vec2 gUv=p;
    vec2 bUv=p-offset;
    col=RGBShift(tDiffuse,rUv,gUv,bUv);
    
    gl_FragColor=col;
}
`

class Fragment extends kokomi.Component {
  constructor(base, config = {}) {
    super(base)

    const { material, points } = config

    this.points = kokomi.polySort(points)

    // const geometry = new THREE.PlaneGeometry(0.1, 0.1, 16, 16);

    const shape = kokomi.createPolygonShape(this.points, {
      scale: 0.01,
    })
    const geometry = new THREE.ExtrudeGeometry(shape, {
      steps: 1,
      depth: 0.0001,
      bevelEnabled: true,
      bevelThickness: 0.0005,
      bevelSize: 0.0005,
      bevelSegments: 1,
    })
    geometry.center()

    const matClone = material.clone()
    matClone.uniforms.uRandom.value = THREE.MathUtils.randFloat(0.1, 1.1)

    const mesh = new THREE.Mesh(geometry, matClone)
    this.mesh = mesh

    const uj = new kokomi.UniformInjector(this.base)
    this.uj = uj
  }

  addExisting() {
    this.base.scene.add(this.mesh)
  }

  update() {
    this.uj.injectShadertoyUniforms(this.mesh.material.uniforms)
    gsap.to(this.mesh.material.uniforms.uMouse.value, {
      x: this.base.interactionManager.mouse.x,
    })
    gsap.to(this.mesh.material.uniforms.uMouse.value, {
      y: this.base.interactionManager.mouse.y,
    })

    const lp = this.base.clock.elapsedTime * 0.01
    this.mesh.material.uniforms.uLightPosition.value.copy(
      new THREE.Vector3(Math.cos(lp), Math.sin(lp), 10),
    )
  }
}

class FragmentGroup extends kokomi.Component {
  constructor(base, config = {}) {
    super(base)

    const { material, layerId = 0, polygons } = config

    const g = new THREE.Group()
    this.g = g

    const frags = polygons.map((points, i) => {
      const frag = new Fragment(this.base, {
        material,
        points,
      })
      frag.addExisting()
      const firstPoint = frag.points[0]
      frag.mesh.position.set(
        firstPoint.x * 0.01,
        firstPoint.y * -0.01,
        THREE.MathUtils.randFloat(-3, -1),
      )
      frag.mesh.material.uniforms.uLayerId.value = layerId
      g.add(frag.mesh)
      return frag
    })

    this.g.position.z = 2 - 1.5 * layerId

    this.frags = frags
  }

  addExisting() {
    this.base.scene.add(this.g)
  }
}

function generatePolygons(config = {}) {
  const { gridX = 10, gridY = 20, maxX = 9, maxY = 9 } = config

  const polygons = []

  for (let i = 0; i < gridX; i++) {
    for (let j = 0; j < gridY; j++) {
      const points = []
      let edgeCount = 3
      const randEdgePossibility = Math.random()
      if (randEdgePossibility > 0 && randEdgePossibility <= 0.2)
        edgeCount = 3
      else if (randEdgePossibility > 0.2 && randEdgePossibility <= 0.55)
        edgeCount = 4
      else if (randEdgePossibility > 0.55 && randEdgePossibility <= 0.9)
        edgeCount = 5
      else if (randEdgePossibility > 0.9 && randEdgePossibility <= 0.95)
        edgeCount = 6
      else if (randEdgePossibility > 0.95 && randEdgePossibility <= 1)
        edgeCount = 7

      let firstPoint = {
        x: 0,
        y: 0,
      }
      let angle = THREE.MathUtils.randFloat(0, 2 * Math.PI)
      for (let k = 0; k < edgeCount; k++) {
        if (k === 0) {
          firstPoint = {
            x: (i % maxX) * 10,
            y: (j % maxY) * 10,
          }
          points.push(firstPoint)
        }
        else {
          // random polar
          const r = 10
          angle += THREE.MathUtils.randFloat(0, Math.PI / 2)
          const anotherPoint = {
            x: firstPoint.x + r * Math.cos(angle),
            y: firstPoint.y + r * Math.sin(angle),
          }
          points.push(anotherPoint)
        }
      }
      polygons.push(points)
    }
  }

  return polygons
}

class FragmentWorld extends kokomi.Component {
  constructor(base, config = {}) {
    super(base)

    const { material } = config

    const fgsContainer = new THREE.Group()
    this.base.scene.add(fgsContainer)
    fgsContainer.position.copy(new THREE.Vector3(-0.36, 0.36, 0.1))

    // fragment groups
    const polygons = generatePolygons()

    const fgs = [...Array(2).keys()].map((item, i) => {
      const fg = new FragmentGroup(this.base, {
        material,
        layerId: i,
        polygons,
      })
      fg.addExisting()
      fgsContainer.add(fg.g)
      return fg
    })
    this.fgs = fgs

    // clone group for infinite loop
    const fgsContainer2 = new THREE.Group().copy(fgsContainer.clone())
    fgsContainer2.position.y = fgsContainer.position.y - 1

    const totalG = new THREE.Group()
    totalG.add(fgsContainer)
    totalG.add(fgsContainer2)
    this.totalG = totalG

    // anime
    this.floatDistance = 0
    this.floatSpeed = 1
    this.floatMaxDistance = 1
    this.isDashing = false
  }

  addExisting() {
    this.base.scene.add(this.totalG)
  }

  update() {
    this.floatDistance += this.floatSpeed

    const y = this.floatDistance * 0.001
    if (y > this.floatMaxDistance)
      this.floatDistance = 0

    if (this.totalG)
      this.totalG.position.y = y
  }

  speedUp() {
    gsap.to(this, {
      floatSpeed: 50,
      duration: 4,
      ease: 'power2.in',
    })
  }

  speedDown() {
    gsap.to(this, {
      floatSpeed: 1,
      duration: 6,
      ease: 'power3.inOut',
    })
  }

  async dash(duration = 5000, cb) {
    if (this.isDashing)
      return

    this.isDashing = true

    this.speedUp()

    await kokomi.sleep(duration)

    if (cb)
      cb()

    this.speedDown()
  }

  changeTexture(name) {
    this.fgs.forEach((fg) => {
      fg.frags.forEach((frag) => {
        const tex = this.base.am.items[name]
        tex.wrapS = THREE.RepeatWrapping
        tex.wrapT = THREE.RepeatWrapping
        frag.mesh.material.uniforms.uTexture.value = tex
      })
    })
  }
}

class Sketch extends kokomi.Base {
  create() {
    this.camera.position.set(0, 0, 1.5)
    this.camera.fov = 10
    this.camera.near = 0.01
    this.camera.far = 10000
    this.camera.updateProjectionMatrix()

    const resourceList = [
      {
        name: 'tex1',
        type: 'texture',
        path: 'https://s2.loli.net/2022/11/19/cqOho3ZKCXfTdzw.jpg',
      },
      {
        name: 'tex2',
        type: 'texture',
        path: 'https://s2.loli.net/2022/11/20/8E6yHP9kAawc7Wr.jpg',
      },
    ]

    const am = new kokomi.AssetManager(this, resourceList)
    this.am = am
    am.on('ready', async () => {
      const tex = am.items.tex1
      tex.wrapS = THREE.RepeatWrapping
      tex.wrapT = THREE.RepeatWrapping

      const uj = new kokomi.UniformInjector(this)

      const material = new THREE.ShaderMaterial({
        vertexShader,
        fragmentShader,
        side: THREE.DoubleSide,
        transparent: true,
        uniforms: {
          ...uj.shadertoyUniforms,
          uTexture: {
            value: tex,
          },
          uLightPosition: {
            value: new THREE.Vector3(-0.2, -0.2, 3),
          },
          uLightColor: {
            value: new THREE.Color('#eeeeee'),
          },
          uRandom: {
            value: THREE.MathUtils.randFloat(0.1, 1.1),
          },
          uMouse: {
            value: new THREE.Vector2(0.5, 0.5),
          },
          uLayerId: {
            value: 0,
          },
        },
      })

      // fragment world
      const fw = new FragmentWorld(this, {
        material,
      })
      fw.addExisting()
      this.fw = fw

      // postprocessing
      const ce = new kokomi.CustomEffect(this, {
        vertexShader: vertexShader2,
        fragmentShader: fragmentShader2,
        uniforms: {
          uRGBShift: {
            value: 1,
          },
        },
      })
      ce.addExisting()
    })
  }
}

function createSketch() {
  const sketch = new Sketch('#sketch2', {
    hello: false,
  })
  sketch.create()
  return sketch
}

onMounted(() => {
  createSketch()
})
</script>

<template>
  <div class="TouchProduct" h-full>
    <div id="sketch2" />

    <div class="Major-Title display">
      科塔锐意 | 直达、立即
    </div>
    <div class="Major-Title show">
      科塔锐意 | 直达、立即
    </div>

    <div class="Major-Button">
      <button @click="$router.push('/touch')">
        敬请期待
      </button>
    </div>
  </div>
</template>

<style>
#sketch2 {
  position: absolute;

  top: 0;
  left: 0;

  width: 100%;
  height: 100%;

  background-color: white;
}

.Major-Button {
  position: absolute;

  left: 50%;
  bottom: 30%;

  transform: translate(-50%, -50%);
}

.TouchProduct .Major-Button button:hover {
  background-color: #212121;
  color: #fff;
  border: 1px solid #262626;

  border-radius: 1rem;
}

.TouchProduct .Major-Button button {
  padding: 0.5rem 0.75rem;

  color: #000;
  background-color: #21212150;
  border: 1px solid #262626;
  border-radius: 0.75rem;

  font-size: 16px;
  cursor: pointer;
  backdrop-filter: blur(18px);

  transition: all 0.2s ease-in-out;
}

.Major {
  position: relative;

  width: 100%;
  height: 720px;
}

.Major-Desc h1 {
  font-weight: 600;
}

.Major-Desc p {
  opacity: 0.75;

  max-width: 80%;

  font-size: 1.5rem;
}

.Major-Title.display {
  z-index: 1;

  opacity: 0.75;
  mix-blend-mode: difference;
  transform: translate(-50%, 0);
}

.Major-Title.show {
  opacity: 0.5;
  /* mix-blend-mode: difference; */
  transform: translate(-50%, 0);
  /* mix-blend-mode: difference; */
}

.Major-Title {
  position: absolute;
  display: flex;

  top: 30%;
  left: 50%;

  width: 50%;

  align-items: center;
  justify-content: center;
  flex-direction: column;

  font-size: 2rem;

  color: #212121;
  transform: translate(-50%, -50%);
}
</style>
