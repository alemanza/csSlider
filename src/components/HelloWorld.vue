<template>
  <div class="hello">
    <header>
      <h1>CSSlider</h1>
    </header>
    <section class="wrapper">
      <div class="csslider">
        <input v-for="(card, i) in cards.length - 2"
          :key="i"
          type="radio"
          name="csslider"
          :id="`pos${i+1}`"
          :class="`cssl-input -step${i+1}`"
          :checked="i === 0"
        />

        <div class="cssl-nav">
          <label v-for="(card, i) in cards.length - 2"
            :key="i"
            :for="`pos${i+1}`"
            class="cssl-arrow"
          />
        </div>

        <div class="cssl-container">
          <div class="cssl-translation">
            
            <div class="cssl-card" v-for="(card, i) in cards" :key="i">
              <figure class="cssl-figure">
                <img class="cssl-img" :src="require(`../assets/images/${card.imgURL}.jpg`)" alt="Big Ben">
              </figure>
              <div class="cssl-content">
                <div class="cssl-text-content">
                  <h3 class="cssl-title">{{card.name}}</h3>
                  <p class="cssl-description">{{card.description}}</p>
                </div>
                <div class="cssl-subcontent">
                  <span class="cssl-rating">{{card.rating}}</span>
                  <span class="cssl-stars">
                    <span v-for="(star, e) in Math.ceil(card.rating)"
                      :key="e"
                      :class="['cssl-icon',
                          isMidStar(i) && e === Math.ceil(card.rating) -1 ? 'icon-mid-star' : 'icon-star'
                        ]"
                    />
                  </span>
                </div>
              </div>
            </div>      
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import data from '../data/cards'
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      cards: data
    }
  },
  methods: {
    isMidStar(i) {
      return this.cards[i].rating % 1 != 0
    }    
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
// Borrar
.cssl-nav {
  display: flex;
}

$containerWidth: 960px;
$itemsShow: 3;
$itemWidth: 300px;
$margins: 30px;

.csslider {
  max-width: 1200px;
  margin: auto;
  position: relative;
  .cssl-container {
    position: relative;
    margin: auto;
    width: $containerWidth;
    overflow: hidden;
    padding: 10px 20px 20px;
    &:before, &:after{
      z-index: 1;
      content: '';
      position: absolute;
      height: 100%;
      top: 0;
      width: 20px;
    }
    &:before{
      left: 0;
      background-image: linear-gradient(to left, transparent, #F5F5F5)
    }
    &:after{
      right: 0;
      background-image: linear-gradient(to right, transparent, #F5F5F5)
    }
  }
  .cssl-translation {
    display: flex;
    transition: transform .4s cubic-bezier(.19,.63,.44,1.16);
  }

  .cssl-arrow {
    transition: color .5s;
    top: calc(50% - 25px - 5px);
    height: 40px;    
    width: 40px;
    padding: 10px;
    position: absolute;
    display: none;
    z-index: 1;
    align-items: center;
    justify-content: center;
    color: #888;
    opacity: .6;
    font-size: 40px;
    font-family: 'cssl-icons';
    cursor: pointer;
    &:before {
      content: "\e902";
    }
    &:hover {
      transition-duration: 0s;
      color: #444;
    }
  }

  .cssl-card {
    box-shadow: 0 8px 20px 0 rgba(0,0,0,.1);
    border-radius: 8px;
    overflow: hidden;
    width: 300px;
    min-width: 300px;
    height: 416px;
    margin-left: 30px;
    background-color: #FFF;
    &:first-of-type {
      margin-left: 0;
    }
  }
  .cssl-img {
    width: 100%;
    display: block;
  }

  .cssl-content {
    padding: 17px 20px 20px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 116px;
    box-sizing: border-box;        
  }
  .cssl-title {
    font-size: 24px;
    color: #444;
    letter-spacing: -.03em;
    padding-bottom: 5px;
  }
  .cssl-description {
    font-size: 13px;
    color: #888;
  }
  .cssl-subcontent {
    display: flex;
    color: #FF8626;
  }
  .cssl-rating {
    font-size: 13px;
    padding-right: 5px;
    font-weight: 700;
  }
  .cssl-icon {
    font-size: 10px;
    margin-left: 3px;
  }
  .cssl-stars {
    display: flex;
    align-items: center;
  }

  .cssl-input {
    display: none;
    @for $i from 1 through 10 {
      @if $i == 1 {
        &.-step#{$i}:checked ~ {
          .cssl-container {
            transform: translateX(0);
          }
          .cssl-nav .cssl-arrow {
            &:last-of-type {
              display: flex;
              left: 0;
              transform: rotateZ(180deg);
            }
            &:nth-child(2) {
              display: flex;
              right: 0;
            }
          }
        }
      } @else {
        &.-step#{$i}:checked ~ {
          .cssl-container .cssl-translation{
            transform: translateX(calc( -#{ ($i - 1) * ($itemWidth + $margins) }) );
          }
          .cssl-nav .cssl-arrow {
            &:nth-child(#{$i - 1}) {
              display: flex;
              left: 0;
              transform: rotateZ(180deg);
            }
            &:nth-child(#{$i + 1}) {
              display: flex;
              right: 0;
            }
          }
        }
      }
      &.cssl-input:last-of-type:checked ~ {
        .cssl-nav .cssl-arrow {
          &:first-of-type {
            display: flex;
            right: 0;
          }
        }
      }
    }
  }
}
</style>
