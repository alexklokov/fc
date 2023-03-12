<template>
  
  <Header />
    
  <main>
    
    <div class="page-header">
      <h1>Футбольный клуб <img src="http://fc-tambov.ru/upfiles/championat/team_logos/1.png"> «Тамбов»</h1>
    </div>
    
    <Match :source="source"/>
      
    <MatchTable :source="source" />
      
    <Players :source="source" />
      
    <News :source="source"/>
      
    <Videos :source="source" />
      
  </main>
  
  <Footer />
    
</template>


<script>

import Header from "@/components/Header.vue"
import Match from "@/components/Match.vue"
import MatchTable from "@/components/MatchTable.vue"
import Players from "@/components/Players/Players.vue"
import News from "@/components/News/News.vue"
import Videos from "@/components/Videos/Videos.vue"
import Footer from "@/components/Footer.vue"

export default {
  data() {
    return {
      source: 'http://127.0.0.1:5000'
    }
  },
  components: {
    Header, Match, MatchTable, Players, News, Videos, Footer, 
  },
};
</script>

<style lang="sass">

$text-color: #00205b

$select-border: #777
$select-focus: blue
$select-arrow: $select-border

*,
*::before,
*::after
  box-sizing: border-box

body
  background: linear-gradient(180deg, rgba(0,49,139,1) 0%, rgba(0,27,78,1) 10%)
  margin: 0
  padding: 0

#app 
  font-family: Avenir, Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  color: $text-color

main
  padding-top: 100px
  max-width: 1200px
  margin: 0 auto
  width: 100%

.page-header
  display: flex
  justify-content: center
  align-items: center
  gap: 10px
  margin: 0 auto
  text-align: center
  
  img 
    height: max-content
  
  
  @media (max-width: 800px)
    width: 600px
    text-align: center
    
  @media (max-width: 640px)
    width: 100%
    
    img
      height: 80px
  
h1
  font-size: 60px
  color: white
  display: flex
  align-items: center
  gap: 50px
  @media (max-width: 1080px)
    flex-direction: column
    gap: 20px
  @media (max-width: 800px)
    font-size: 50px
    
  @media (max-width: 640px)
    font-size: 30px
  
  
h2
  color: white
  font-size: 50px
  text-align: center
  @media (max-width: 800px)
    font-size: 30px
    
  
.nbutton
  padding: 10px 20px
  border-radius: 6px
  border: solid 2px white
  color: white
  width: max-content 
  cursor: pointer
  transition-duration: .2s
  
  &:hover
    background: white
    color: #00205b

select
  appearance: none
  background-color: transparent
  border: none
  padding: 0 1em 0 0
  margin: 0
  width: 100%
  font-family: inherit
  font-size: inherit
  cursor: inherit
  line-height: inherit
  outline: none
  
  &::-ms-expand
    display: none
    
.nselect
   width: 100%
   min-width: 15ch
   max-width: 30ch
   border: 1px solid white
   border-radius: 0.25em
   padding: 10px 20px
   
   cursor: pointer
   line-height: 1.1
   background-color: transparent
   color: white
   display: grid
   grid-template-areas: "select"
   align-items: center
   
   
   select, &::after
    grid-area: select
    color: white
    
   &::after
    content: ""
    width: 0.8em
    height: 0.5em
    background-color: white
    clip-path: polygon(100% 0%, 0 0%, 50% 100%)
    justify-self: end
   
</style>
