<template>
  <div class="box a">A</div>
  <div class="box b">B</div>
  <div class="box c">C</div>
  <div class="box d">D</div>
  <div class="padre">
    <div class="container c1">
      <p>pantalla 1</p>
    </div>
    <div class="container c2">
      <p>pantalla 2</p>
    </div>
    <div class="container c3">
      <p>pantalla 3</p>
    </div>
    <div class="container c4">
      <p>pantalla 4</p>
    </div>
  </div>
</template>

<script>
import gsap from 'gsap';
import ScrollTrigger from "gsap/ScrollTrigger";
import { onMounted } from '@vue/runtime-core'

export default{
  setup(){
    onMounted(()=>{
      gsap.registerPlugin(ScrollTrigger);
      gsap.defaults({ease:'none', duration: 2})

      gsap.to(
        '.b',
        {
          scrollTrigger:{
            trigger: '.b',
            markers:true,
            start:"-280px 50%",
            end:"470px 50%",
            toggleActions: 'play reverse play reverse'
          },
          x:-300,
          duration: .8,
          opacity: 1
        }
      )

      gsap.to(
        '.c',
        {
          scrollTrigger: {
            trigger:'.c',
            markers:true,
            start:"-100px 50%",
            end:"400px 50%",
            toggleActions: 'play reverse play reverse'
          },
          x:300,
          duration: .8,
          opacity:1
        }
      )

      gsap.to(
        '.d',
        {
          scrollTrigger: {
            trigger: '.d',
            markers:true,
            start: "-180px 50%",
            end: "360px 50%",
            scrub:1,
          },
          rotate: 360,
          x: 300,
          duration: .8,
        }
      )

      let tl = gsap.timeline({
        scrollTrigger:{
          animation:tl,
          trigger:'.padre',
          start: '100px 50%',
          end:'0 50%',
          markers:true,
          scrub:true,
          pin: true,
          anticipatePin:1,
        }
      });
      tl.from(".c2",{xPercent:-100})
        tl.from(".c3",{xPercent:100})
        tl.from(".c4",{yPercent:-100})

      scrollTrigger.create({
        animation:tl,
        trigger:'.padre',
        start: 'top top',
        end:'+= 4000',
        scrub:true,
        pin: true,
        anticipatePin:1
      })

    })
  }
}
</script>

<style scoped>
.box{
  width: 150px;
  height: 150px;
  margin: 100px 50px 400px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 60px;
}

.a{
  background-color: rgb(157, 82, 228);
}

.b{
  background-color: rgb(74, 211, 97);
  opacity: 0;
  margin-left: 1100px;
}

.c{
  background-color: rgb(236, 193, 73);
  opacity: 0;
}

.d{
  background-color: rgb(228, 82, 82);
}

.container{
  width: 100%;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.container p{
  font-size: 100px;
}

.c1{
  background-color: rgb(65, 65, 241);
}

.c2{
  background-color: rgb(238, 58, 223);
}

.c3{
  background-color: rgb(58, 238, 103);
}

.c4{
  background-color: rgb(220, 238, 58);
}
</style>
