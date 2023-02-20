<template>

  <div class="wrapper">
    <div class="header">
      <h1>Документы</h1>
      <div class="manage_block">
        
        <div class="flag">
          <svg width="12" height="15" viewBox="0 0 12 15" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M11 13.8571L6 10.2857L1 13.8571V2.42857C1 2.04969 1.15051 1.68633 1.41842 1.41842C1.68633 1.15051 2.04969 1 2.42857 1H9.57143C9.95031 1 10.3137 1.15051 10.5816 1.41842C10.8495 1.68633 11 2.04969 11 2.42857V13.8571Z" stroke="#8E9CBB" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
        </div>

        <div class="header_button">
          <div class="plus">
            +
          </div>
          <div class="button_content">
            Новый тип
          </div>
        </div>

        <div class="header_button">
          <div class="plus">
            +
          </div>
          <div class="button_content">
            Новый документ
          </div>
        </div>

        
      </div>
    </div>
  
    <div class="documents_content"> 
      
      <div class="search">
        <div class="loupe">
          <svg width="17" height="17" viewBox="0 0 17 17" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M11.4142 11L15.6569 15.2426M13 7C13 10.3137 10.3137 13 7 13C3.68629 13 1 10.3137 1 7C1 3.68629 3.68629 1 7 1C10.3137 1 13 3.68629 13 7Z" stroke="#8E9CBB" stroke-width="2" stroke-linecap="round"/>
          </svg>
        </div>

        <input 
          type="search" 
          v-model="search"
          @input="handleInput"
        >
        
      </div>
      
      <draggable
        class="dragArea"
        tag="ul"
        :list="list"
        :group="{ name: 'categories' }"
        item-key="name"            
        filter=".filtered"
        @end="endCatetgoryDragHandler"
        @add="addHandler"
        @update="updateHandler"
      >            
        <template 
          #item="{ element }"              
        >
          <li 
            :class="`
              ${element.type} 
              ${element.class} 
              ${element.filtered?'filtered':''}
            `"                
            v-show="element.visible"
          >
            <p class="category_name">
              <div 
                class="slide_up"
                @click="element.open = !element.open"                  
              >
                <span v-if="!element.open">
                  <svg width="8" height="5" viewBox="0 0 8 5" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M3.53976 4.4727C3.28126 4.21408 3.28126 3.79476 3.53976 3.53614L6.87001 0.204315C7.12851 -0.0543084 7.54762 -0.054308 7.80612 0.204315C8.06462 0.462938 8.06462 0.88225 7.80612 1.14087L4.47587 4.4727C4.21737 4.73132 3.79826 4.73132 3.53976 4.4727Z" fill="#0066FF"/>
                    <path d="M4.47058 4.4727C4.72908 4.21408 4.72908 3.79476 4.47058 3.53614L1.12999 0.193967C0.871489 -0.064656 0.452377 -0.0646556 0.193876 0.193968C-0.0646252 0.452591 -0.0646252 0.871902 0.193876 1.13053L3.53447 4.4727C3.79297 4.73132 4.21208 4.73132 4.47058 4.4727Z" fill="#0066FF"/>
                  </svg>
                </span>
                <span v-if="element.open">
                  <svg width="8" height="5" viewBox="0 0 8 5" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M3.53976 0.194049C3.28126 0.452672 3.28126 0.871984 3.53976 1.13061L6.87001 4.46243C7.12851 4.72106 7.54762 4.72106 7.80612 4.46243C8.06462 4.20381 8.06462 3.7845 7.80612 3.52588L4.47587 0.194049C4.21737 -0.0645747 3.79826 -0.0645742 3.53976 0.194049Z" fill="#0066FF"/>
                    <path d="M4.47058 0.194049C4.72908 0.452672 4.72908 0.871984 4.47058 1.13061L1.12999 4.47278C0.871489 4.7314 0.452377 4.7314 0.193876 4.47278C-0.0646252 4.21416 -0.0646252 3.79485 0.193876 3.53622L3.53447 0.194049C3.79297 -0.0645747 4.21208 -0.0645742 4.47058 0.194049Z" fill="#0066FF"/>
                  </svg>
                </span>
              </div>
              
              <div class="cat_text_name">
                {{ element.name }}
              </div>
              <template v-for="dotColor in element.dots">                  
                  <div class="dot" :style="'background-color: ' + dotColor"></div>
              </template>

              <span class="notice_att">
                {{ element.notice_att }}
              </span>
              <span class="notice">
                {{ element.notice }}
              </span>
              
              <div class="manage_buttons">
                <svg width="14" height="14" viewBox="0 0 14 14" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path d="M7.70711 3.29289L10.7071 6.29289M9.33943 1.62805C9.53855 1.42894 9.77493 1.27099 10.0351 1.16323C10.2953 1.05546 10.5741 1 10.8557 1C11.1373 1 11.4161 1.05546 11.6763 1.16323C11.9364 1.27099 12.1728 1.42894 12.3719 1.62805C12.5711 1.82717 12.729 2.06356 12.8368 2.32372C12.9445 2.58388 13 2.86272 13 3.14431C13 3.42591 12.9445 3.70474 12.8368 3.9649C12.729 4.22506 12.5711 4.46145 12.3719 4.66057L5.16971 11.8628L1 13L2.13719 8.8303L9.33943 1.62805Z" stroke="#8E9CBB" stroke-width="2" stroke-linejoin="round"/>
                </svg>
                <svg width="13" height="15" viewBox="0 0 13 15" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path d="M1 3C0.447715 3 0 3.44772 0 4C0 4.55228 0.447715 5 1 5V3ZM12 5C12.5523 5 13 4.55228 13 4C13 3.44772 12.5523 3 12 3V5ZM2.92846 3.6C2.92846 4.15228 3.37618 4.6 3.92846 4.6C4.48075 4.6 4.92846 4.15228 4.92846 3.6H2.92846ZM5.21418 1V0V1ZM7.78561 1V0V1ZM8.07132 3.6C8.07132 4.15228 8.51903 4.6 9.07132 4.6C9.6236 4.6 10.0713 4.15228 10.0713 3.6H8.07132ZM6 7C6 6.44772 5.55228 6 5 6C4.44772 6 4 6.44772 4 7H6ZM4 11C4 11.5523 4.44772 12 5 12C5.55228 12 6 11.5523 6 11H4ZM9 7C9 6.44772 8.55228 6 8 6C7.44772 6 7 6.44772 7 7H9ZM7 11C7 11.5523 7.44772 12 8 12C8.55228 12 9 11.5523 9 11H7ZM1 5H12V3H1V5ZM4.92846 3.6V2.3H2.92846V3.6H4.92846ZM4.92846 2.3C4.92846 2.21689 4.96122 2.13938 5.01604 2.08395L3.59404 0.677572C3.16663 1.10973 2.92846 1.69355 2.92846 2.3H4.92846ZM5.01604 2.08395C5.0705 2.02889 5.14199 2 5.21418 2V0C4.60438 0 4.02182 0.245036 3.59404 0.677572L5.01604 2.08395ZM5.21418 2H7.78561V0H5.21418V2ZM7.78561 2C7.85779 2 7.92929 2.02889 7.98374 2.08395L9.40575 0.677572C8.97796 0.245036 8.3954 0 7.78561 0V2ZM7.98374 2.08395C8.03856 2.13938 8.07132 2.21689 8.07132 2.3H10.0713C10.0713 1.69355 9.83316 1.10973 9.40575 0.677572L7.98374 2.08395ZM8.07132 2.3V3.6H10.0713V2.3H8.07132ZM4 7V11H6V7H4ZM7 7V11H9V7H7ZM10 4V12H12V4H10ZM9 13H4V15H9V13ZM3 12V4H1V12H3ZM4 13C3.44772 13 3 12.5523 3 12H1C1 13.6569 2.34315 15 4 15V13ZM10 12C10 12.5523 9.55228 13 9 13V15C10.6569 15 12 13.6569 12 12H10Z" fill="#FF238D"/>
                </svg>
                
                <div 
                  class="move ib"
                  @click="changeMovable(element)"
                >
                  <svg 
                    v-show="element.filtered"
                    width="8" height="16" viewBox="0 0 8 16" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M4.69594 14.7086C4.30473 15.0991 3.67045 15.0991 3.27924 14.7086L0.293409 11.7296C-0.097803 11.339 -0.0978031 10.7059 0.293409 10.3153C0.684621 9.92482 1.3189 9.92482 1.71011 10.3153L4.69594 13.2944C5.08715 13.6849 5.08715 14.318 4.69594 14.7086Z" fill="#8E9CBB"/>
                    <path d="M3.30385 14.7086C3.69506 15.0991 4.32934 15.0991 4.72055 14.7086L7.70659 11.7296C8.0978 11.339 8.0978 10.7059 7.70659 10.3153C7.31538 9.92482 6.6811 9.92482 6.28989 10.3153L3.30385 13.2944C2.91264 13.6849 2.91264 14.318 3.30385 14.7086Z" fill="#8E9CBB"/>
                    <path d="M3.98759 14.0157C3.43433 14.0157 2.98583 13.5679 2.98583 13.0157V3C2.98583 2.44772 3.43433 2 3.98759 2C4.54085 2 4.98935 2.44772 4.98935 3V13.0157C4.98935 13.5679 4.54085 14.0157 3.98759 14.0157Z" fill="#8E9CBB"/>
                    <path d="M4.69594 0.292893C4.30473 -0.0976311 3.67045 -0.0976311 3.27924 0.292893L0.293409 3.27191C-0.097803 3.66243 -0.0978031 4.2956 0.293409 4.68612C0.684621 5.07664 1.3189 5.07664 1.71011 4.68612L4.69594 1.70711C5.08715 1.31658 5.08715 0.683417 4.69594 0.292893Z" fill="#8E9CBB"/>
                    <path d="M3.30385 0.292893C3.69506 -0.0976311 4.32934 -0.0976311 4.72055 0.292893L7.70659 3.27191C8.0978 3.66243 8.0978 4.2956 7.70659 4.68612C7.31538 5.07664 6.6811 5.07664 6.28989 4.68612L3.30385 1.70711C2.91264 1.31658 2.91264 0.683417 3.30385 0.292893Z" fill="#8E9CBB"/>
                  </svg>                      
                  <svg 
                    v-show="!element.filtered"
                    width="8" height="16" viewBox="0 0 8 16" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M4.69594 14.7086C4.30473 15.0991 3.67045 15.0991 3.27924 14.7086L0.293409 11.7296C-0.097803 11.339 -0.0978031 10.7059 0.293409 10.3153C0.684621 9.92482 1.3189 9.92482 1.71011 10.3153L4.69594 13.2944C5.08715 13.6849 5.08715 14.318 4.69594 14.7086Z" fill="#0066FF"/>
                    <path d="M3.30385 14.7086C3.69506 15.0991 4.32934 15.0991 4.72055 14.7086L7.70659 11.7296C8.0978 11.339 8.0978 10.7059 7.70659 10.3153C7.31538 9.92482 6.6811 9.92482 6.28989 10.3153L3.30385 13.2944C2.91264 13.6849 2.91264 14.318 3.30385 14.7086Z" fill="#0066FF"/>
                    <path d="M3.98759 14.0157C3.43433 14.0157 2.98583 13.5679 2.98583 13.0157V3C2.98583 2.44772 3.43433 2 3.98759 2C4.54085 2 4.98935 2.44772 4.98935 3V13.0157C4.98935 13.5679 4.54085 14.0157 3.98759 14.0157Z" fill="#0066FF"/>
                    <path d="M4.69594 0.292893C4.30473 -0.0976311 3.67045 -0.0976311 3.27924 0.292893L0.293409 3.27191C-0.097803 3.66243 -0.0978031 4.2956 0.293409 4.68612C0.684621 5.07664 1.3189 5.07664 1.71011 4.68612L4.69594 1.70711C5.08715 1.31658 5.08715 0.683417 4.69594 0.292893Z" fill="#0066FF"/>
                    <path d="M3.30385 0.292893C3.69506 -0.0976311 4.32934 -0.0976311 4.72055 0.292893L7.70659 3.27191C8.0978 3.66243 8.0978 4.2956 7.70659 4.68612C7.31538 5.07664 6.6811 5.07664 6.28989 4.68612L3.30385 1.70711C2.91264 1.31658 2.91264 0.683417 3.30385 0.292893Z" fill="#0066FF"/>
                  </svg>



                </div>
              </div>
            </p>                
            <Transition>
            <draggable                  
              v-if="element.open"
              class="dragArea downList"
              tag="ul"
              :list="element.items"
              :group="{ name: 'items' }"
              item-key="name"
              filter=".filtered"
              @end="endItemDragHandler"
              @add="addHandler" 
            >
              <template #item="{ element }">
                
                <li 
                  :class="`${element.type} ${element.filtered?'filtered':''}`"
                  :data-uuid="element.uuid"
                >                    
                  <p class="item_name">{{ element.name }}</p>

                  <template v-for="dotColor in element.dots">                  
                      <div class="dot" :style="'background-color: ' + dotColor"></div>
                  </template>

                  <span class="notice_att">
                  {{ element.notice_att }}
                </span>
                <span class="notice">
                  {{ element.notice }}
                </span>
                <div class="manage_buttons">
                  <svg width="14" height="14" viewBox="0 0 14 14" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M7.70711 3.29289L10.7071 6.29289M9.33943 1.62805C9.53855 1.42894 9.77493 1.27099 10.0351 1.16323C10.2953 1.05546 10.5741 1 10.8557 1C11.1373 1 11.4161 1.05546 11.6763 1.16323C11.9364 1.27099 12.1728 1.42894 12.3719 1.62805C12.5711 1.82717 12.729 2.06356 12.8368 2.32372C12.9445 2.58388 13 2.86272 13 3.14431C13 3.42591 12.9445 3.70474 12.8368 3.9649C12.729 4.22506 12.5711 4.46145 12.3719 4.66057L5.16971 11.8628L1 13L2.13719 8.8303L9.33943 1.62805Z" stroke="#8E9CBB" stroke-width="2" stroke-linejoin="round"/>
                  </svg>
                  <svg width="13" height="15" viewBox="0 0 13 15" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M1 3C0.447715 3 0 3.44772 0 4C0 4.55228 0.447715 5 1 5V3ZM12 5C12.5523 5 13 4.55228 13 4C13 3.44772 12.5523 3 12 3V5ZM2.92846 3.6C2.92846 4.15228 3.37618 4.6 3.92846 4.6C4.48075 4.6 4.92846 4.15228 4.92846 3.6H2.92846ZM5.21418 1V0V1ZM7.78561 1V0V1ZM8.07132 3.6C8.07132 4.15228 8.51903 4.6 9.07132 4.6C9.6236 4.6 10.0713 4.15228 10.0713 3.6H8.07132ZM6 7C6 6.44772 5.55228 6 5 6C4.44772 6 4 6.44772 4 7H6ZM4 11C4 11.5523 4.44772 12 5 12C5.55228 12 6 11.5523 6 11H4ZM9 7C9 6.44772 8.55228 6 8 6C7.44772 6 7 6.44772 7 7H9ZM7 11C7 11.5523 7.44772 12 8 12C8.55228 12 9 11.5523 9 11H7ZM1 5H12V3H1V5ZM4.92846 3.6V2.3H2.92846V3.6H4.92846ZM4.92846 2.3C4.92846 2.21689 4.96122 2.13938 5.01604 2.08395L3.59404 0.677572C3.16663 1.10973 2.92846 1.69355 2.92846 2.3H4.92846ZM5.01604 2.08395C5.0705 2.02889 5.14199 2 5.21418 2V0C4.60438 0 4.02182 0.245036 3.59404 0.677572L5.01604 2.08395ZM5.21418 2H7.78561V0H5.21418V2ZM7.78561 2C7.85779 2 7.92929 2.02889 7.98374 2.08395L9.40575 0.677572C8.97796 0.245036 8.3954 0 7.78561 0V2ZM7.98374 2.08395C8.03856 2.13938 8.07132 2.21689 8.07132 2.3H10.0713C10.0713 1.69355 9.83316 1.10973 9.40575 0.677572L7.98374 2.08395ZM8.07132 2.3V3.6H10.0713V2.3H8.07132ZM4 7V11H6V7H4ZM7 7V11H9V7H7ZM10 4V12H12V4H10ZM9 13H4V15H9V13ZM3 12V4H1V12H3ZM4 13C3.44772 13 3 12.5523 3 12H1C1 13.6569 2.34315 15 4 15V13ZM10 12C10 12.5523 9.55228 13 9 13V15C10.6569 15 12 13.6569 12 12H10Z" fill="#FF238D"/>
                  </svg>
                  <div 
                    class="move ib"
                    @click="changeMovable(element)"
                  >
                  <svg 
                    v-show="element.filtered"
                    width="8" height="16" viewBox="0 0 8 16" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M4.69594 14.7086C4.30473 15.0991 3.67045 15.0991 3.27924 14.7086L0.293409 11.7296C-0.097803 11.339 -0.0978031 10.7059 0.293409 10.3153C0.684621 9.92482 1.3189 9.92482 1.71011 10.3153L4.69594 13.2944C5.08715 13.6849 5.08715 14.318 4.69594 14.7086Z" fill="#8E9CBB"/>
                    <path d="M3.30385 14.7086C3.69506 15.0991 4.32934 15.0991 4.72055 14.7086L7.70659 11.7296C8.0978 11.339 8.0978 10.7059 7.70659 10.3153C7.31538 9.92482 6.6811 9.92482 6.28989 10.3153L3.30385 13.2944C2.91264 13.6849 2.91264 14.318 3.30385 14.7086Z" fill="#8E9CBB"/>
                    <path d="M3.98759 14.0157C3.43433 14.0157 2.98583 13.5679 2.98583 13.0157V3C2.98583 2.44772 3.43433 2 3.98759 2C4.54085 2 4.98935 2.44772 4.98935 3V13.0157C4.98935 13.5679 4.54085 14.0157 3.98759 14.0157Z" fill="#8E9CBB"/>
                    <path d="M4.69594 0.292893C4.30473 -0.0976311 3.67045 -0.0976311 3.27924 0.292893L0.293409 3.27191C-0.097803 3.66243 -0.0978031 4.2956 0.293409 4.68612C0.684621 5.07664 1.3189 5.07664 1.71011 4.68612L4.69594 1.70711C5.08715 1.31658 5.08715 0.683417 4.69594 0.292893Z" fill="#8E9CBB"/>
                    <path d="M3.30385 0.292893C3.69506 -0.0976311 4.32934 -0.0976311 4.72055 0.292893L7.70659 3.27191C8.0978 3.66243 8.0978 4.2956 7.70659 4.68612C7.31538 5.07664 6.6811 5.07664 6.28989 4.68612L3.30385 1.70711C2.91264 1.31658 2.91264 0.683417 3.30385 0.292893Z" fill="#8E9CBB"/>
                  </svg>                      
                  <svg 
                    v-show="!element.filtered"
                    width="8" height="16" viewBox="0 0 8 16" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M4.69594 14.7086C4.30473 15.0991 3.67045 15.0991 3.27924 14.7086L0.293409 11.7296C-0.097803 11.339 -0.0978031 10.7059 0.293409 10.3153C0.684621 9.92482 1.3189 9.92482 1.71011 10.3153L4.69594 13.2944C5.08715 13.6849 5.08715 14.318 4.69594 14.7086Z" fill="#0066FF"/>
                    <path d="M3.30385 14.7086C3.69506 15.0991 4.32934 15.0991 4.72055 14.7086L7.70659 11.7296C8.0978 11.339 8.0978 10.7059 7.70659 10.3153C7.31538 9.92482 6.6811 9.92482 6.28989 10.3153L3.30385 13.2944C2.91264 13.6849 2.91264 14.318 3.30385 14.7086Z" fill="#0066FF"/>
                    <path d="M3.98759 14.0157C3.43433 14.0157 2.98583 13.5679 2.98583 13.0157V3C2.98583 2.44772 3.43433 2 3.98759 2C4.54085 2 4.98935 2.44772 4.98935 3V13.0157C4.98935 13.5679 4.54085 14.0157 3.98759 14.0157Z" fill="#0066FF"/>
                    <path d="M4.69594 0.292893C4.30473 -0.0976311 3.67045 -0.0976311 3.27924 0.292893L0.293409 3.27191C-0.097803 3.66243 -0.0978031 4.2956 0.293409 4.68612C0.684621 5.07664 1.3189 5.07664 1.71011 4.68612L4.69594 1.70711C5.08715 1.31658 5.08715 0.683417 4.69594 0.292893Z" fill="#0066FF"/>
                    <path d="M3.30385 0.292893C3.69506 -0.0976311 4.32934 -0.0976311 4.72055 0.292893L7.70659 3.27191C8.0978 3.66243 8.0978 4.2956 7.70659 4.68612C7.31538 5.07664 6.6811 5.07664 6.28989 4.68612L3.30385 1.70711C2.91264 1.31658 2.91264 0.683417 3.30385 0.292893Z" fill="#0066FF"/>
                  </svg>
                  
                  </div>
                </div>
                </li>
              </template>
            </draggable>
            </Transition>

          </li>
        </template>

      </draggable>

    </div> 

</div> 

</template>

<script>
import draggable from "vuedraggable";
import { v4 as uuidv4 } from "uuid";

export default {
name: "documents",
display: "docs",  
components: {
draggable
},
methods: {
updateHandler(event) {    },
endCatetgoryDragHandler(event) {
  let newIndex = event.newDraggableIndex,
      element = this.list[newIndex];
  element.filtered = true;
},
endItemDragHandler(event) {
  
  let node = event.item,
    uuid = node.dataset.uuid;      
  console.log('uuid: ', uuid);

  let parentCatInd;
  
  this.list.every((cat,curCatInd) => {        
      let iterateCat = true;        
      cat.items.every((item,itemInd) => {
        if (item.uuid == uuid) { 
          parentCatInd = curCatInd;            
          iterateCat = false;            
          return false;
        }
        return true;
      });
      return iterateCat;        
  });

  let itemNewIndex = event.newDraggableIndex,
      item = this.list[ parentCatInd ].items[itemNewIndex];
  item.filtered = true;
  

},
addHandler(event ){},
changeMovable(element) {      
  element.filtered = !element.filtered;      
},
handleInput(event) {      
  let searchName = event.target.value;      
  this.list.map(category=>{
        
        let catName = category.name;
        category.visible = false;            
        catName = catName.toLowerCase();            
        if ( catName.includes( searchName )) category.visible = true;
        
        category.items.map((item) => {            
          let itemName = item.name;
          itemName = itemName.toLowerCase();            
          if ( itemName.includes( searchName )) {
            category.visible = true;
            item.visible = true;
          }
        });
  });
}
},  
data() {
return {
  search: '',
  enabled: true,      
  list: [
    {
      uuid: uuidv4(),
      class:'',
      type: 'category',
      filtered: true,
      visible: true,
      open: 0,
      name: "Обязательные для всех",
      dots: ['#FF238D', '#FFB800', '#FF8D23'],
      notice_att: '',
      notice: 'Документы, обязательные для всех сотрудников без исключения',
      items: [
        {
          uuid: uuidv4(),
          type: 'item',
          filtered: true,
          visible: true,
          name: "Паспорт",
          dots: ['#00C2FF'],
          notice_att: 'Обязательный',
          notice: 'Для всех',
          items: []
        },
        {
          uuid: uuidv4(),
          type: 'item',
          name: "Инн  ",
          filtered: true,
          visible: true,
          dots: [],
          notice_att: 'Обязательный',
          notice: 'Для всех',
          items: []
        }
      ]
    },
    {
      uuid: uuidv4(),
      class: '',
      type: 'category',
      open: 0,
      name: "Обязательные для трудоустройства",
      filtered: true,
      visible: true,
      dots: [],
      notice_att: '',
      notice: 'Документы, без которых невозможно трудоустройство человека на какую бы то ни было должность в компании вне зависимости от граж',
      items: []
    },
    {
      uuid: uuidv4(),
      class: '',
      type: 'category',
      open: 0,
      name: "Специальные",
      filtered: true,
      visible: true,
      dots: [],
      notice_att: '',
      notice: '',
      items: []
    },
    {
      uuid: uuidv4(),
      class: 'root_category',
      type: 'category',
      open: 1,
      name: "root",
      filtered: true,
      visible: true,
      dots: [],
      notice_att: '',
      notice: '',
      items: [
        {
          uuid: uuidv4(),
          type: 'item',
          open: 1,
          name: "Тестовое задание кандидата",
          filtered: true,
          visible: true,
          dots: [],
          notice_att: '',
          notice: 'Россия, Белоруссия, Украина, администратор филиала, повар-сушист, повар-пиццмейкер, повар горячего цеха',
          items: []
        },
        {
          uuid: uuidv4(),
          type: 'item',
          name: "Трудовой договор",
          filtered: true,
          visible: true,
          dots: [ '#0066FF', '#8E9CBB'],
          notice_att: '',
          notice: '',
          items: []
        },
        {
          uuid: uuidv4(),
          type: 'item',
          name: "Мед. книжка",
          filtered: true,
          visible: true,
          dots: [],
          notice_att: '',
          notice: '',
          items: []
        }
      ]
    }
  ]

};
},
watch: {
    list: {
        handler: function(newList, oldList) {
            // console.log('oldList: ', oldList);
            // console.log('newList: ', newList);
        },
        deep: true
    }
},
computed: {}
};
</script>

<style scoped>
h1 {
font-size: 22px;
font-weight: 500;
}
.wrapper {
padding: 30px 10px;
}
.documents_content {
margin-top: 30px;
}
ul {
padding: 0;
margin: 0;
list-style-type: none;
}
li, ul {
cursor: pointer;
list-style-type: none;
}
.category .category_name {
padding: 10px 5px;
padding-left: 20px;
font-size: 15px;
font-weight: 900;
}

.item_name {
display: inline-block;
margin: 5px;
}

.item {
padding: 0px 5px; 
padding-left: 20px;   
margin-left: 20px;
}

.category .category_name, .item {
border: 1px solid #DFE4EF;
display: flex;
align-items: center;
}  


.rootFolder {
margin-top: 20px;
}

.rootFolder .item {
margin-left: 0px;
}

.slide_up {
display: inline-block;
padding: 7px;
padding-top: 6px;
padding-bottom: 8px;
border: 1px solid #DFE4EF;
color: #0066FF;
border-radius: 20px;
margin-right: 10px;
line-height: 5px;
}

.header {
display: flex;
}

.manage_block{
margin-left: auto;    
display: flex;
text-align: center;
}

.flag, .header_button {
cursor: pointer;
}

.flag {
display: inline-block;
padding: 10px 12px;
border: 1px solid #DFE4EF;
color: #0066FF;
border-radius: 20px;
margin-right: 10px;
line-height: 5px;
}

.header_button {        
padding: 10px 15px;
padding-top: 14px;
border: 1px solid #DFE4EF;    
border-radius: 20px;
margin-right: 10px;
line-height: 14px;
display: flex;
text-align: center;
}


.plus, .button_content {
  display: flex;
  text-align: center;
  line-height: 5px;      
}

.plus {
  color: #0066FF;
  font-size: 30px;
  margin-right: 10px;
}

.button_content {
  font-size: 15px;
  font-weight: 500;
}


.v-enter-active, .v-leave-active {
transition: opacity 0.5s ease;
}

.v-enter-from, .v-leave-to {
opacity: 0;
}

.downList {
min-height: 50px;
}

.notice_att, .notice {
display: inline-block;
margin: 5px;
font-size: 11px;
}
.notice_att {
color: #FF238D;
}

.notice {
color: #8E9CBB;
}
.dot {
display: inline-block;
width: 8px;
height: 8px;
margin: 3px;
border-radius: 5px;    
}

.cat_text_name, .item_name {
display: inline-block;
margin-right: 10px;    
}

.cat_text_name {
font-size: 15px;
font-weight: 500;
}
.item_name {
font-weight: 400;
font-size: 13px;
}

.manage_buttons {
margin-left: auto;
}

.manage_buttons svg {
margin: 8px;
}

.search {
display: flex;
text-align: center;
width: 564px;
margin: 30px;
margin-left: 0;
border-bottom: 1px solid #BFC9E0;    
}
.search input {
border: none;
font-style: italic; 
font-size: 15px;
padding: 10px 20px;
width: 100%;
}

.search .loupe {
display: inline-block;
cursor: pointer;    
padding: 5px;
position: relative;
margin-top: 5px;
}

input:focus{
  outline: none;
}

.root_category {
padding-top: 20px;
}

.root_category .category_name {
display: none;
}

.root_category .item {
margin-left: 0;
}
.ib{
display: inline-block;
}


.category .category_name, .item{
box-shadow: 0px 3px 16px rgba(0, 102, 255, 0.7);
}

.filtered .category_name, .filtered {
box-shadow: none;
}



</style>
