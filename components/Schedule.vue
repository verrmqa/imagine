<template>
  <section class="schedule">    
    <div class="wrapper">
    <div class="block-heading">      
      <img class="schedule-img" src="~/static/schedule.png" alt="">
      <!-- <div class="line"></div> -->
      <!-- <p>
        The eyes of the Fair are on the future — not in the sense of peering toward the unknown nor attempting to foretell the events of tomorrow and the shape of things to come
      </p> -->
      </div>
    </div>
  
   <div class="scroller-wrapper">
      <div ref="scroller"  class="scroller schedule-items">
        <div class="schedule-item" v-for="item in items" :key="item.id">
          <div class="schedule-item-date">{{item.date}}</div>
          <div class="schedule-item-time">{{item.time}}</div>
          <div class="schedule-item-name">{{item.name}}</div>
          <button class="schedule-item-button">Записаться</button>
          <!-- <div class="schedule-item-line"></div>           -->
        </div>
      </div>
   </div>
    
  </section>
</template>
<script>
export default {
  mounted: function() {
    Draggable.create(this.$refs.scroller, {
      type: 'scrollLeft',
      edgeResistance: 0.75,
      throwProps: true,
    });
    const buttons = document.querySelectorAll('.schedule-item-button');
    const self = this;
    buttons.forEach(function (element) {
      element.addEventListener('click', function () {        
          self.$emit('scrollToForm');
          console.log('emit');
      });
    });
  },
  components: {},
  data: function() {
    return {
      items: [
        {
          id: 1,
          date: '27 мая',
          time: '14:00 - 20:00',
          name: `
          Москва, Третьяковская галерея. 
          Малый Толмачевский переулок 6, стр.1`,
        },
        // {
        //   id: 2,
        //   date: '1 июля',
        //   time: '19:00',
        //   name: 'Ты герой',
        // },
        // {
        //   id: 3,
        //   date: '8 июля',
        //   time: '19:00',
        //   name: 'Проекция мечты',
        // },
      ],
    };
  },
};
</script>

<style lang="scss">
@import '~/assets/scss/_vars.scss';
.scroller-wrapper {
  display: flex;
  justify-content: flex-end;
  overflow: hidden;
  position: relative;
}
.schedule-item {
  transition: 300ms ease;
  opacity: 0.6;
  position: relative;
  padding-right: 292px;
  max-width: 272px;
  @media #{$tabletScreen} {
    padding-right: 40px;
  }
  &:last-child {
    padding-right: 232px;
    .schedule-item-line {
      right: 0px;
    }
    @media #{$tabletScreen} {
      padding-right: 50px;
    }
  }
  &-line {
    position: absolute;
    top: 24px;
    right: 60px;
    width: 172px;
    height: 1px;
    background: black;
    @media #{$tabletScreen} {
      display: none;
    }
  }
  &-date {
    @extend %p;
    font-size: 36px;
    margin-bottom: 12px;
  }
  &-time {
    @extend %p;
    font-size: 16px;
  }
  &-name {
    @extend %p;
    font-size: 16px;
  }
  &-button {
    @extend %p;
    transition: 300ms ease;
    cursor: pointer;
    font-size: 15px;
    text-transform: uppercase;
    padding: 14px 27px;
    background: none;
    border: 1px solid white;
    border-bottom: 1px solid black;
    letter-spacing: 2.5px;
    margin-top: 34px;
    &:hover {
      border: 1px solid black;
    }
  }
  &:hover {
    opacity: 1;
  }
}

.schedule-items {
  width: 100%;
  padding-left: calc(50% - 500px);  
  padding-bottom: 30px;
  @media screen and (max-width:1200px) {
    padding-left: 16px;  
  }
  @media #{$tabletScreen} {
    padding-left: 16px;
  }
  &::-webkit-scrollbar {
    display: none;
  }
  > div {
    display: flex !important;
    justify-content: center;
  }
}
.schedule {
  padding-top: 60px;
   @media #{$tabletScreen} {
    padding-top: 80px;
    .block-heading {
      margin-bottom: 32px;
    }
  }
}
.schedule-img {
  width: 268px;
   @media #{$tabletScreen} {
      margin-left: -20px;
  }
   
}
</style>
