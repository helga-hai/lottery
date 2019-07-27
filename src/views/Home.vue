<template>
  <main-layout>
    <section class="section">
      <header class="top">
        <div class="top__logo"><img :src="require(`../assets/images/logo.png`)"><h1>{{ title }}</h1></div>
        <div class="top__round round">
          <div class="top__sign-in button-s">sign-in<a href="#"></a></div>
          <div class="top__sign-out button-s">sign-out<a href="#"></a></div>
          <div class="top__drop drop button-s" @mouseover="showDropdown=true" >city<a href="#"></a></div>
          <div class="top__basket button-s">basket<a href="#"></a></div>
        </div>
        <div style="height:19px"></div>
        <transition name="fade" :duration="500">
          <div class="top__addition" v-if="showDropdown" @mouseover="showDropdown=true" @mouseleave="showDropdown=false">
            <div class="top__item"><a href="#">Kyiv</a></div>
            <div class="top__item"><a href="#">Lviv</a></div>
            <div class="top__item"><a href="#">Dnipro</a></div>
          </div>
        </transition>
      </header>

      <Ttabs :list="tabsList"/>

      <block-line @onClickLine="onClickLine" :blockId="921"  :id="921">
        <ticket-vue :num="1" @onClick="onClick"/>
        <ticket-vue :num="2" @onClick="onClick"/>
        <ticket-vue :num="3" @onClick="onClick"/>
        <ticket-vue :num="4" @onClick="onClick"/>
        <ticket-vue :num="5" @onClick="onClick"/>
        <div class="controls" slot="controls"> 
          <div v-show="error" class="error">{{ error['921'] }}</div>
          <TButton v-if="isVisibleButton" @onPopup="onPopup">Check</TButton>
          <TButton v-else disabled>Check</TButton>
        </div>
      </block-line>

      <block-line @onClickLine="onClickLine" :blockId="134" :id="134">
        <ticket-vue :num="1" @onClick="onClick"/>
        <ticket-vue :num="2" @onClick="onClick"/>
        <ticket-vue :num="3" @onClick="onClick"/>
        <ticket-vue :num="4" @onClick="onClick"/>
        <ticket-vue :num="5" @onClick="onClick"/>
        <div class="controls" slot="controls">
          <div v-show="error" class="error">{{ error['134'] }}</div>
          <TButton v-if="isVisibleButton" @click="onPopup">Check</TButton>
          <TButton v-else disabled>Check</TButton>
        </div>
      </block-line>

    </section>
    <section name="popup">
      <Popup :visible="isPopupVisible" @onClose="onCloseAction">
        <h2>{{getRandomArray()}}</h2>
      </Popup>
    </section>
  </main-layout>
</template>

<script>
import MainLayout from "@/layouts/MainLayout";
import Ttabs from "@/components/Ttabs";
import TButton from "@common/TButton";
import Popup from "@/components/common/Popup";
import TicketVue from "@/components/ticket";
import BlockLine from "@/components/BlockLine";
export default {
  name: "Home",
  components: {
    MainLayout,
    Ttabs,
    TButton,
    Popup,
    TicketVue,
    BlockLine
  },
  data() {
    return {
      title: "Play Games",
      tabsList: [
        { title: "Lorem ipsum dolor sit amet consectetur adipisicing elit. Odio itaque, eligendi ad nihil repudiandae laudantium qui delectus unde corrupti at porro, reiciendis consectetur expedita nostrum quam accusamus quaerat deserunt eum?", classNames: ["active"], to: "/" },
        { title: "Lorem, ipsum dolor sit amet consectetur adipisicing elit. Repellat temporibus nesciunt commodi error qui laboriosam at veritatis, dicta excepturi nam labore.", classNames: [], to: "/" },
        { title: "Lorem ipsum dolor sit amet consectetur adipisicing elit. At laborum officia nulla animi, beatae eligendi, dolorem repudiandae in incidunt perferendis sunt, nobis voluptas consequatur asperiores? Obcaecati qui nisi totam magni.", classNames: [], to: "/" },
        { title: "Lorem ipsum dolor sit amet consectetur adipisicing elit. Incidunt quisquam accusamus modi atque neque sint enim repellat nemo quo.", classNames: [], to: "/" }
      ],
      activeTab: 1,
      isPopupVisible: false,
      
      objLists:{},
      error: {
        '921': '',
        '134': ''
      },
      isVisibleButton: false,
      id:'',
      blockId: '',
      showDropdown: false
    };
  },
  methods: {
    onClickLine(blockIdVal){
      this.blockIdVal=blockIdVal
    },
    getRandomArray(){
        //Array(5).fill(0).map(item=>item=getArray())
        return [[1,2,3,4,5],[6,7,8,9,10],[11,12,13,14,15],[16,17,18,19,20],[16,17,18,19,20]].map(item=>item=this.getArray())
      },
    getArray(){ 
      return [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]
      .map((a) => ({sort: Math.random(), value: a}))
      .sort((a, b) => a.sort - b.sort)
      .map((a) => a.value)
      .splice(0,5)
    },
    onCloseAction(){
      this.isPopupVisible = false;
    },
    onPopup(active) {
      this.isPopupVisible = !this.isPopupVisible;
    },
    onClick({el,valueId}){
      
      const parentID = el.closest('[id]').getAttribute("id")

      if(!this.objLists['list_'+parentID]){
        this.objLists['list_'+parentID] = [[],[],[],[],[]]
      }
      
      let index = valueId-1;

      if(this.objLists['list_'+parentID][index].length<5){
        el.disabled = true;
        this.objLists['list_'+parentID][index].push(el.value);
        if(this.objLists['list_'+parentID][index].length==5){
          el.parentElement.classList.add('ready');
        }
      } else if(this.objLists['list_'+parentID][index].length==5) {
        event.preventDefault;
        this.error[parentID] = '* Необходимо выбрать всего 5 позиций в карточке';
      }

      if(this.objLists['list_'+parentID].every(item=>item.length==5)){
        this.isVisibleButton = true;
      }

    },

  },
};
</script>

<style lang="scss">

.block {
  width: 795px;
  margin: 0 auto;
  &__line {
    border: 2px solid #92acf1;
    border-radius: 4px;
    padding: 4px;
    display: grid;
    grid-template-columns: 153px 153px 153px 153px 153px;
    grid-template-rows: 1fr;
    align-items: center;
    grid-gap: 5px;
    margin: 50px 0 10px;
  }
}
.ready {
    border: 2px solid #ef8787;
    border-radius: 4px;
    box-shadow: 1px 1px 3px 1px #ccc;
}
.ticket {
  display: grid;
  grid-template-rows: 30px 30px 30px 30px 30px;
  grid-template-columns: 34px 34px 34px 34px;
  grid-gap: 3px;
  justify-items: center;
  padding: 2px;
  &__item {
    border:1px solid grey;
    width:34px;
    height:30px;
    line-height:30px;
    color: grey;
    cursor: pointer;
    background: transparent;
    &[disabled] {
        background-image: url(data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz48c3ZnIHZlcnNpb249IjEuMSIgaWQ9ItCh0LvQvtC5XzEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeG1sbnM6eGxpbms9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGxpbmsiIHg9IjBweCIgeT0iMHB4IiB2aWV3Qm94PSIwIDAgMzQgMzAiIHN0eWxlPSJlbmFibGUtYmFja2dyb3VuZDpuZXcgMCAwIDM0IDMwOyIgeG1sOnNwYWNlPSJwcmVzZXJ2ZSI+PHN0eWxlIHR5cGU9InRleHQvY3NzIj4uc3Qwe3N0cm9rZTojMDAwMDAwO3N0cm9rZS13aWR0aDoyO308L3N0eWxlPjxwYXRoIGNsYXNzPSJzdDAiIGQ9Ik01LjgsMi44QzE1LjUsOC4zLDIyLjYsMTcuMywzMC41LDI1Yy0zLjUsMy42LTUuNy0zLjEtOC40LTQuOWMtNS41LTYtMTEuMi0xMi0xOC41LTE1LjhMNS44LDIuOEw1LjgsMi44eiIvPjxwYXRoIGNsYXNzPSJzdDAiIGQ9Ik0yOC4zLDIuNWMtNS41LDcuMS0xMS42LDEzLjYtMTguMSwxOS44Yy0wLjksMi41LTkuMSw4LjItNC4zLDNjNi41LTYuOSwxMy41LTEzLjQsMTkuMi0yMUMyNS44LDMuMiwyNy4zLDMuMSwyOC4zLDIuNUwyOC4zLDIuNXoiLz48L3N2Zz4=);
    }
  }
}
.num-01 {
	background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAJwAAACiCAMAAACDFlSiAAAALVBMVEW/1PnD1/rI2vnM3frR3/rU4vvY5fvh6/zk7f3p7/3w9P3z9/73+v78/P/////saHenAAAAwklEQVR42u3ZMRKCQBBFwQFUlhXm/se1isADmPiDfifo/FUHBwcHBwcHBwcHBwcHBwcHBwcHBwcHBwcHBwcHBwcHBwcHBwcH91v73RmJm3U3I3FbMG5ULm5WLm4uubijKhV3PSsWdyyVijseVam4pSoX90VtwbgxY3Hru2Nx+9WpuNfZnYlbx9WdibuDg4ODg4ODg4ODg4OD8yHg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODg/tEHfQpSul960p4AAAAASUVORK5CYII=);
}
.num-02 {
	background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAJwAAACiCAMAAACDFlSiAAAAM1BMVEW/1PnD1/rI2vnM3frR3/rU4vvY5fvd6Pzh6/zk7f3p7/3s8v7w9P3z9/73+v78/P////8n58QyAAABVUlEQVR4Ae3Zu27EIBBGYS42S4wx8/5Pm0QaZC2Ki1T7F+eUU33iIgqCCQcOHDhw4MCBAwcOHDhw4MCBAwcOHDhw4MCBAwcOHDhw4MCBAwcOHDhw/+9s9afW9XBtD7NYuhTuTOGtfejgXmEtdhHcYnPdpYFr4a+yBi5NT3rVuofZoYBrjolf9tuYvKSAK45p5mUfdAFcXM9Yc9zxedxwSn2efA53lW2LvqueDs47h+LKPV/fUxFXHDcEcd1t2fRwIzvuEMTdD4QergSvyeFu225quJGnLQ013G2L3ZRwq00M1+NiU8GtNjHcbcuX6eBW2zAx3G0rZmK4sdiUcCNPWzU5XJm2l8nh2rRtpodLE5e3tw4B3BEeqgK4JIzrQRhXlXGbMi6o4vgkAQcOHLjnwIEDBw4cOHDgwIEDBw4cOHDgwIEDBw4cOHDgwIEDBw4cOHDgwH0DNVEJeeU9Az8AAAAASUVORK5CYII=);
}
.num-03 {
	background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAJwAAACiCAMAAACDFlSiAAAAM1BMVEW/1PnD1/rI2vnM3frR3/rU4vvY5fvd6Pzh6/zk7f3p7/3s8v7w9P3z9/73+v78/P////8n58QyAAABgUlEQVR42u3ZwZLCIBCEYWAJGQgB3/9pt6yQxSQHa299+Pskt6/EybTqXsIBBw4cOHDgwIEDBw4cOHDgwIEDBw4cOHDgwIEDBw4cOHDgwIEDBw4cuP+nFjMruyCuJe+O+LVp4frqPuKzEq7/uGuSEG7apk4FZ+6ZTQTXz1EIq6W/1yK4/HmV7bziTQM3OMtxqgO3SuD60OzjHI5jlMA1W97vnT/PUQU3hbXccIsO7nnLWRE3Fpnvcri5ZE2tz1VbvNj6mkmKi/82p84XwZoeBi6Wrof7rJtquHYpdGq4rb168QKL/3u7q3q42ZmiIG4ObVPEpbMLK+Js4AzclwGo2Zbo5yWuQjh/f65Flc/ctIS5KISmNd96+eJOrQCuDYyvF6srCrjZMdNWSzwPQee3kmeqyOKv7pkiU5mKf9iEyuYeLrRQtWp6CZNmXe4Lzp5TjDFZ5U8ScODAgQMHDhw4cODAgQMHDhw4cODAgQMHDhw4cODAgQMHDhw4cODAgQP3zi8TeAyaRgCbKgAAAABJRU5ErkJggg==);
}
.num-04 {
	background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAJwAAACiCAMAAACDFlSiAAAAM1BMVEW/1PnD1/rI2vnM3frR3/rU4vvY5fvd6Pzh6/zk7f3p7/3s8v7w9P3z9/73+v78/P////8n58QyAAABB0lEQVR42u3ZsW6DQBRE0YVAjA327v9/rRVj6TVJkxSZ4tyK8khP2iloIzg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4OLjftm+vInH3dpaI63Mw7tJycUfLxfU5GLe2XNzecnF9CsYtLRd3bbm4x5SKq6OuibjtNG1bGq72fhmJuI+XaHrE4WrvryMNV3u/jjRc7f3U43B11H0E4vY6ahau9n7uibj3JhwjEHc7MZeRhqu9n/bj7LOdfX3f/xt3tJ9b4ODggnD9qNKekuq7RxgODg7OTxI4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODi4P/UEteoJz8YWEgIAAAAASUVORK5CYII=);
}
.num-05 {
	background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAJwAAACiCAMAAACDFlSiAAAAM1BMVEW/1PnD1/rI2vnM3frR3/rU4vvY5fvd6Pzh6/zk7f3p7/3s8v7w9P3z9/73+v78/P////8n58QyAAABYUlEQVR42u3ZW46EMAxEURsChDzI7H+1oxGgTBMWUGrd+uTrSJHj2NiPcMCBAwcOHDhw4MCBAwcOHDhw4MCBAwcOHDhw4MCBAwcOHDhw4MCBAwfue3ApjKkquGBjigrOhXGHCeOKMi4q4xZl3HRyDsV7rp0217uEez0ESdx+4qIkbj1xSRI3n7ha9zWEELMUzs7MdsVjk8FVGzJVFVyyMV5FcJu96jRwwd4yNQmc35ytlLzanaiAOz4x9ba6Aq6VPYbZy1C8WXH6uk92VcTlCxcEcX2ikByqwX0D7ig5xiX1h4BQQfiTkmSukt5aj+eHJIDbL8vyGP+9qfTWfozVhRp/b1c2pX+vEm8SuOb2kiwy4GQbs8msXdNgW4V2wmX6oHmS2qa32Hm+HnKr/rpvIYQlZv5DgAMHDhw4cODAgQMHDhw4cODAgQMHDhw4cODAgQMHDhw4cODAgQMHDhy4v/wCiowIKor9UAwAAAAASUVORK5CYII=);
}
.controls {
  display:grid;
  grid-template-rows:1fr;
  grid-template-columns: 3fr 1fr;
  justify-content: space-evenly;
  .btn {
    grid-column: end;
  }
}
.error {
  color: $errorColor;
  font-size: 12px;
  text-align: left;
  padding-left: 10px;
  padding-top: 5px;
}
.top {
  display:grid;
  grid-template-rows:1fr;
  grid-template-columns: 2fr 4fr;
  align-items: center;
  &__logo {
    img {
      width:190px;
    }
  }
  &__round {
    overflow: hidden;
    display: grid;
    grid-template-rows: 1fr;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    border-radius: 33px;
  }
  &__addition {
    //grid-column-start: 2;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    justify-items: center;
  }
  &__item {
    display:inline-block;
    text-align:center;
    &:first-child {
      justify-self: end;
    }
    &:last-child {
      justify-self: start;
    }
    a {
      color: $tone-blue;
      text-decoration: none;
    }
  }
  &__sign-in {
    background-color: $tone-blue;
    height: 50px;
    color: $color_white;
    line-height: 50px;
    font-size: $fs_md;
    font-weight: bold;
    letter-spacing: 0.4px;
    border: 0;
    outline: none;
    border-top-left-radius: 29px;
    border-bottom-left-radius: 29px;
    user-select: none;
  }
  &__sign-out {
    background-color: $tone-blue;
    height: 50px;
    color: $color_white;
    line-height: 50px;
    font-size: $fs_md;
    font-weight: bold;
    letter-spacing: 0.4px;
    border: 0;
    outline: none;
    user-select: none;
  }
  &__drop {
    background-color: $tone-blue;
    height: 50px;
    color: $color_white;
    line-height: 50px;
    font-size: $fs_md;
    font-weight: bold;
    letter-spacing: 0.4px;
    border: 0;
    outline: none;
    user-select: none;
    transition:all .3s;
    position: relative;
    &:hover .drop__wrap{
      display:block; 
       visibility: visible;
        opacity: 1;
        z-index: 1;
        transform: translateY(0%);
        transition-delay: 0s, 0s, 0.3s;
    }

  }
  &__basket {
    background-color: $tone-blue;
    height: 50px;
    color: $color_white;
    line-height: 50px;
    font-size: $fs_md;
    font-weight: bold;
    letter-spacing: 0.4px;
    border: 0;
    outline: none;
    border-top-right-radius: 29px;
    border-bottom-right-radius: 29px;
    user-select: none;
  }

}
.section {
  max-width: 834px;
  margin:0 auto;
}


.round {

  a {
    color: #ffffff;
    text-decoration: none;
    width: 100%;
    height: 100%;
    position: absolute;
    left: 0;
    z-index: 4;
  }
  .button-s {
    display: inline-block;
    position: relative;
    transition: color 0.5s;
    &:first-child {
      width: 400px;
      width:inherit;
    }
    &:before {
      content: "";
      position: absolute;
      z-index: 0;
      background: #c8d5e469;
      height: 150px;
      width: 200px;
      border-radius: 50%;
      z-index:2
    }
    &:hover{
      color:#000000;
    }
    &:nth-child(1):before {
      top: 190%;
      left: -109%;
      transition: all 0.7s;
      z-index:2
    }
    &:nth-child(1):hover:before {
      top: -40px;
      left: -40px;
    }
    &:nth-child(2):before {
      left: -30px;
      bottom: 100%;
      transition: all 0.7s;
      z-index:2
    }
    &:nth-child(2):hover:before {
      bottom: -50px;
    }
    &:nth-child(3):before {
      top: 66px;
      left: -43%;
      transition: all 0.7s;
      z-index:2
    }
    &:nth-child(3):hover:before {
      top: -30px;
      left: -30px;
    }
    &:nth-child(4):before {
      left: -30px;
      bottom: 100%;
      transition: all 0.7s;
      z-index:2
    }
    &:nth-child(4):hover:before {
      bottom: -20px;
    }
  }

}

</style>
