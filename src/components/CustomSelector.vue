<template>
  <div>
    <span class="language">Язык</span>
      <div class="select-container">
        <button @click="openOptions" id ="select" :class="isDefault ? 'select-default' : 'selected' " 
                value="language" type="button">
                язык
        </button>
        <div class="options">
          <span class="item">язык</span>
          <span class="item">русский</span>
          <span class="item">английский</span>
          <span class="item">китайский</span>
          <span class="item">испанский</span>
        </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'custom-selector',
  data() {
    return {
      isDefault: true
    }
  },
  methods: {
    openOptions () {
      this. isDefault = false
      const select = document.getElementById('select');
      const optionBox = document.querySelector('.options');
      const options = [...document.querySelectorAll('.options .item')];
      let activeOption = 0;

      window.onclick = (e) => {
        if(!e.target.className.includes('select')){ 
            select.classList.remove('active') 
            optionBox.classList.remove('active')  
        } else{
            select.classList.toggle('active') 
            optionBox.classList.toggle('active') 
        }
          setValue();
      }
      options.forEach((item, i) => item.onmousemove = () => hoverOptions(i) )
      const hoverOptions = (i) => {
        options[activeOption].classList.remove('active') 
        options[i].classList.add('active') 
        activeOption = i;
      }
       window.onkeydown = (e) => {
          if(select.className.includes('active')){
              e.preventDefault();
              if(e.key === 'ArrowDown' && activeOption < options.length - 1){ 
                hoverOptions(activeOption + 1); 
              } else if(e.key === 'ArrowUp' && activeOption > 0){ 
                hoverOptions(activeOption - 1); 
              } else if(e.key === 'Enter'){ 
                select.classList.remove('active'); 
                optionBox.classList.remove('active');
                setValue(); 
              }
          }
      }
      const setValue = () => select.innerHTML = select.value = options[activeOption].innerHTML 
    }
  }
}
</script>

<style scoped lang="scss">
@import "../scss/_mixins.scss";
.language{ @include xs-size() }
.select-container{
  position: relative;
  padding-top: .4375em;
}
 .select-default, .selected{
    position: relative;
    width: 100%;
    height: 3.375em;

    border: 1px solid #DBE2EA;
    border-radius: 6px;
    box-shadow: var(--shadow);
    
    text-transform: capitalize;
    color: rgba(124, 156, 191, 1);
    background: transparent;
    text-align: left;
    padding: 0 15px;
    cursor: pointer;

    background: url("../../public/image/Dropdown.svg") 96% / 15% no-repeat;
    background-size: 15px 11.3px;
    @include xs-size();
    @include sm-size();
}
.selected{ color: rgba(44, 39, 56, 1); }

.select.active{
  border: 3px solid rgba(8, 128, 174, 1);
  color: rgba(44, 39, 56, 1);
}

.options{
    position: absolute;
    top: 65px;
    left: 0;
    z-index: 3;
    width: 100%;
    height: fit-content;
    background: #fff;
    border: 1px solid #DBE2EA;
    border-radius: 6px;
    overflow: hidden;
    display: none;
}

.options.active{ display: block; }

.options .item:first-child{ display: none;}
.options .item{
    display: block;
    color: #756F86;
    text-transform: capitalize;
    width: 100%;
    height: 2.75em;
    padding: .45em .9375em;
    line-height: 30px;
    cursor: pointer;

    @include xs-size(); 
    @include sm-size();
}

.options .item.active{ background: #EBF4F8;}
</style>