<!--Каталог компонент-->
<template>
  <div class="container catalog-page">

    <div class="row">
      <div class="col-9">
        <div class="row">

          <div class="col-12 col-md-6 col-lg-4 mb-10"
               v-for="(catalogItem, catalogIndex) in catalogListArr"
               :key="catalogIndex">
            <div class="catalog-product-card catalog-product-card__mb_gutter">
              <div class="catalog-product-card__header-cart">
                <div class="catalog-product-card__article" v-if="catalogItem.article">
                  Арт. {{catalogItem.article}}
                </div>
                <div class="catalog-product-card__image">
                  <a :href="catalogItem.link">
                    <img v-if="catalogItem.image"
                         :src="catalogItem.image"
                         alt="Canon BLA bla">
                    <img v-else
                         src="../assets/img/photo.png"
                         class="catalog-product-card__image-tmp" :alt="catalogItem.title">
                  </a>
                </div>
                <div class="catalog-product-card__owned" :class="{'catalog-product-card__owned_active': catalogItem.owned}">
                  <img src="../assets/img/path-1176.png"
                       srcset="../assets/img/path-1176@2x.png 2x,
            img/path-1176@3x.png 3x"
                       title="В наличии">
                  В наличии
                </div>
                <a :href="catalogItem.link"
                   class="catalog-product-card__title"
                   :title="catalogItem.title">
                  {{catalogItem.title}}
                </a>
                <ul class="catalog-product-card__options">
                  <li v-for="(optItem, optIndex) in catalogItem.options"
                      :key="optIndex"
                      class="catalog-product-card__options-item">
                    <div class="catalog-product-card__options-text catalog-product-card__options-text_color_gray">
                      {{optItem.key}} &#8194;
                    </div>
                    <div class="catalog-product-card__options-text catalog-product-card__options-text_color_dark">
                      {{optItem.value}}
                    </div>
                  </li>
                </ul>
              </div>
              <div class="catalog-product-card__footer-cart">
                <a :href="catalogItem.link"
                   :title="catalogItem.title"
                   class="catalog-product-card__button button button_color_blue button_size_m">
                  <img src="../assets/img/cart.png"
                       srcset="../assets/img/cart@2x.png 2x,
             img/cart@3x.png 3x"
                       class="cart" alt="Купить">
                  Купить
                </a>
                <div class="cart-actions catalog-product-card__cart-actions">
                  <button @click="setInFav(catalogIndex)"
                          class="cart-actions__button cart-actions__button_fill_gray"
                          :class="{'cart-actions__button_fill_gray_active': catalogItem.inFav}">

                    <img src="../assets/img/shape.png"
                         srcset="../assets/img/shape@2x.png 2x,
             img/shape@3x.png 3x"
                         class="Shape"
                         v-if="!catalogItem.inFav">

                    <img src="../assets/img/shapeactive.png"
                         srcset="../assets/img/shapeactive@2x.png 2x,
             img/shapeactive@3x.png 3x"
                         class="Shape"
                         v-else>
                  </button>
                  <button class="cart-actions__button">
                    <img src="../assets/img/scales-26.jpg"
                         srcset="../assets/img/scales-26@2x.jpg 2x,
             img/scales-26@3x.jpg 3x"
                         class="Scales-26">
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="col-3">
        <div class="catalog-filter">
          <button @click="setFilter('filter')"
                  class="mb-10 button button_color_blue button_size_100 button_weight_300">
            Показать результат
          </button>
          <button  @click="setFilter('clear')"
            class="button button_color_gray-light button_size_100 button_weight_300 ">
            Очистить фильтр
          </button>
          <div class="catalog-filter__filter-title">
            Производитель
          </div>

          <div class="checkbox-options">
            <ul class="checkbox-options__list">
              <li v-for="(filterItem, filterIndex) in filterListArr"
                  :key = "filterIndex"
                  :class = "{'checkbox-options__option_active': filterItem.value}"
                  class="checkbox-options__option">
                <label class="checkbox-container ">
                  {{filterItem.key}}
                  <input type="checkbox" v-model="filterItem.value">
                  <span class="checkbox-container__checkmark">
                    <svg xmlns="http://www.w3.org/2000/svg" width="10" height="8" viewBox="0 0 10 8">
                        <path fill="none" fill-rule="evenodd" stroke="#FFF" stroke-linecap="round" stroke-width="2" d="M1.936 3.932L4.44 6.524l3.748-5"/>
                    </svg>
                  </span>
                </label>
              </li>

            </ul>
          </div>

        </div>

      </div>
    </div>

  </div>
</template>

<script>
  import 'core-js/fn/promise' //шёл 2018 год, IE всё ещё не подерживает промисы(
  import axios from 'axios'

  // const API_URL = 'http://aero.mramid.ru';//для build
  const API_URL = 'http://localhost:8080';//для dev

  export default {
    name: 'catalog',
    data () {
      return {
        catalogListArr: [
          {
            productId: 213123,
            article: 345656,//Артикул
            owned: true,// В наличии
            image: 'src/assets/img/product.png',// фото
            title: 'Canon PowerShot SX400 IS с улучшенной матрицей и объективом',// наименование товара
            link: '/',//ссылка на страницу товара
            options: [
              {
                key: 'Физический размер',
                value: '23.2 x 15.2 мм'
              },
              {
                key: 'Формат записи',
                value: 'RAW, JPEG, MP4 и другие'
              },
              {
                key: 'Фокусное расстояние',
                value: '18-55 мм.'
              },
            ],//Опции
            inFav: false,//в изранном
            inEq: false,// в сравнении
          },
          {
            productId: 909877,
            article: 909090,//Артикул
            owned: false,// В наличии
            image: '',// фото
            title: 'Canon 2 PowerShot SX600 IS с улучшенной матрицей и объективом',// наименование товара
            link: '/',//ссылка на страницу товара
            options: [
              {
                key: 'Физический размер',
                value: '23.2 x 15.2 мм'
              },
              {
                key: 'Формат записи',
                value: 'RAW, JPEG, MP4 и другие'
              },
              {
                key: 'Фокусное расстояние',
                value: '18-55 мм.'
              },
              {
                key: 'Автофокус',
                value: 'Есть'
              },
            ],//Опции
            inFav: false,//в изранном
            inEq: false,// в сравнении
          },
        ],
        filterListArr: [
          {
            key: 'Canon',
            value: false
          },
          {
            key: 'Olympus',
            value: false
          },
          {
            key: 'Fujifilm',
            value: false
          },
          {
            key: 'Pentax',
            value: false
          },
          {
            key: 'Nikon',
            value: false
          },
          {
            key: 'Sigma',
            value: false
          },
          {
            key: 'Panasonic',
            value: false
          },
          {
            key: 'Geleral Electrics',
            value: false
          },
          {
            key: 'Leica',
            value: false
          },
          {
            key: 'Zenit',
            value: false
          },
        ]
      }
    },
    computed: {
    },
    props: [],
    methods: {
      // запись/удаление из Избранного
      setInFav(catalogIndex){
        let payload = {
              productID: this.catalogListArr[catalogIndex].productId || '',
            };
        axios.get( API_URL + '/inFav.json', {// делаем запрос на сервер, возвращает promise
          params: {
            ...payload
          },
        })
        .then(resp => {
          const error = JSON.parse(resp.data.error);
          if(error){
            console.error('Ошибка');
          }else {
            if ( +resp.data.result.status === 200){
              console.log(`Статус: ${resp.data.result.message}`);

              this.catalogListArr[catalogIndex].inFav = JSON.parse(resp.data.result.inFav);
            }
          }
        })
        .catch(err => {
          console.error(`Ошибка на сервере ${err}`);
        });


      },
      // фильтрация
      setFilter(filterStatus){
        let filterObj = {};//параметры фильтрации, в виде объекта
        this.filterListArr.forEach(function (filterItem) {
          console.log('filterItem = ', filterItem);
          filterObj[filterItem.key] = filterItem.value; // формируем параметры фильтрации
        });

        let payload = {
          ...filterObj, // массив с фильтрами
          setFilter: filterStatus // статус фильтра (filter,clear - фильтровать, очистить)
        };

        axios.get( API_URL + '/filter.json', {// делаем запрос на сервер, возвращает promise
          params: {
            ...payload
          },
        })
        .then(resp => {
          const error = JSON.parse(resp.data.error);
          if(error){
            console.error('Ошибка');
          }else {
            if ( +resp.data.result.status === 200){
              console.log(`Статус: ${resp.data.result.message}`);

              if (resp.data.result.setFilter === 'clear' || filterStatus === 'clear'){
                this.filterListArr.forEach(function (filterItem, index) {
                  filterItem.value = false; // формируем параметры фильтрации
                });
              }

              this.$set(this, 'catalogListArr', resp.data.result.catalogListArr);


            }
          }
        })
        .catch(err => {
          console.error(`Ошибка на сервере ${err}`);
        });



      },
    },
  }
</script>

<style lang="sass">

@import "../assets/sass/vars"

.catalog-page
  margin-top: 10px
.mb-10
  margin-bottom: 10px
.container
  width: 1280px

.catalog-product-card
  background: #ffffff
  display: flex
  flex-direction: column
  justify-content: space-between
  height: 100%
  &__article
    color: $gray
    display: flex
    justify-content: flex-end
    padding-right: 24.9px
    margin-top: 20px
    font-family: $default-font
    font-size: 11.8px
    font-weight: 300
  &__image
    display: flex
    align-items: center
    justify-content: center
    margin-top: 15px
    padding: 0 15px
    min-height: 200px
    img
      max-width: 100%
      height: auto
  &__image-tmp
    max-width: 100px!important
  &__owned
    color: $green
    display: flex
    align-items: center
    padding-left: 35.8px
    margin-top: 25.3px
    font-size: 12.8px
    font-weight: 300
    line-height: 16px
    opacity: 0
    img
      margin-right: 7.9px
    &_active
      opacity: 1
  &__title
    margin-top: 5px
    font-weight: 500
    font-size: 17.8px
    color: $dark
    display: inline-block
    padding: 0 54px 0 31.8px
    transition: all .3s ease
    height: 66px
    overflow: hidden
    &:hover
      color: $blue
      text-decoration: none
  &__options
    list-style: none
    margin: 17px 0px 0px
    padding: 0 54px 30px 31.8px
  &__options-item
    display: flex
  &__options-text
    font-size: 11.8px
    line-height: 1.86
    font-weight: 300
    &_color
      &_gray
        color: $gray-darker
      &_dark
        color: $dark-lighter
  &__footer-cart
    margin-top: 38px
    margin-bottom: 31px
    padding-right: 10px
    display: flex
    align-items: center
    justify-content: space-between
  &__button
    margin-left: 33.8px

.button
  display: inline-flex
  justify-content: center
  align-items: center
  padding: 8px 5px
  border: none
  background: #ffffff
  cursor: pointer
  min-height: 35px
  &_color
    &_blue
      background: $blue
      color: #ffffff
      font-size: 14px
      &:hover, &:focus
        color: #ffffff
        text-decoration: none
        background: darken($blue, 5)
    &_gray-light
      background: $gray-light
      color: $dark
      font-size: 14px
      &:hover, &:focus
        text-decoration: none
        color: $dark
        background: darken($gray-light, 5)
  &_size
    &_m
      min-width: 100px
    &_100
      width: 100%
  &_weight
    &_300
      font-weight: 300
    &_500
      font-weight: 500
    &_700
      font-weight: 700
  .cart
    margin-right: 10px
.cart-actions
  &__button
    background: transparent
    border: none
    display: inline-flex
    justify-content: center
    align-items: center
    cursor: pointer
    height: 24px
    &_fill
      &_gray
        &_active
          &>svg path
            fill: $gray

.catalog-filter
  background: #ffffff
  padding: 28px
  &__filter-title
    color: $dark
    font-size: 17px
    font-family: $default-font
    margin-top: 26px
    margin-bottom: 15px
.checkbox-options
  &__list
    margin: 0px
    list-style: none
    padding: 0px
    display: flex
    flex-wrap: wrap
  &__option
    max-width: 50%
    width: 50%
    margin-bottom: 10px
    &_active
      .checkbox-container
        color: $blue

.checkbox-container
  display: block
  position: relative
  padding-left: 25px
  cursor: pointer
  font-size: 14px
  -webkit-user-select: none
  -moz-user-select: none
  -ms-user-select: none
  user-select: none
  margin-bottom: 0px
  &:hover input ~ .checkbox-container__checkmark
    box-shadow: inset 0 2px 2px 0 rgba(0, 0, 0, 0.07)
    background-color: #ffffff
  input
    position: absolute
    opacity: 0
    cursor: pointer
    &:checked ~ .checkbox-container__checkmark
      background-color: $blue
      border-color: transparent
      &:after
        display: block
  &__checkmark
    position: absolute
    top: 0
    left: 0
    height: 14px
    width: 14px
    box-shadow: inset 0 2px 2px 0 rgba(0, 0, 0, 0.07)
    background-color: #ffffff
    border: solid 1px #d7d7d7
    display: flex
    align-items: center
    justify-content: center
    /*&:after*/
      /*content: ""*/
      /*position: absolute*/
      /*display: none*/
      /*left: 3px*/
      /*top: 0px*/
      /*width: 7px*/
      /*height: 10px*/
      /*border: solid white*/
      /*border-width: 0 2px 2px 0*/
      /*-webkit-transform: rotate(45deg)*/
      /*-ms-transform: rotate(45deg)*/
      /*transform: rotate(45deg)*/

</style>
