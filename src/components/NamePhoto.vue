<template>
    <div
      class="name-photo-container d-inline-flex align-items-center"
      @click="$emit('click', $event)"
    >
      <div
        class="image"
        :class="gender === 'female' ? 'female-list' : 'male-list'"
        v-if="photo"
      >
        <img class="auth-img" :src="photo" :alt="name || ''" />
      </div>
      <div v-else class="fleet-image-text">{{ name_chip }}</div>
      <div class="name-photo-name-desc d-flex flex-column ml-1">
        <div class="name-extra" v-if="extra">{{ extra }}</div>
        <div class="name-photo-name">{{ name }}</div>
        <div class="name-photo-desc text-muted" v-if="description">
          {{ description }}
        </div>
        <div class="contact-icons d-flex justify-content-start" v-if="email || phone || address">
          <!-- Email -->
          <v-tooltip bottom v-if="email">
            <template v-slot:activator="{ on, attrs }">
              <v-btn
                fab
                x-small
                elevation="0"
                class="btnInit m-1"
                v-bind="attrs"
                v-on="on"
                :href="`mailto:${email}`"
                @click.stop
              >
                <v-icon class="icon" color="#04092152">
                  mdi-email-outline
                </v-icon>
              </v-btn>
            </template>
            <span> {{ email }} </span>
          </v-tooltip>
    
          <!-- Phone -->
          <v-tooltip bottom v-if="phone">
            <template v-slot:activator="{ on, attrs }">
              <v-btn
                fab
                x-small
                elevation="0"
                class="btnInit m-1"
                v-bind="attrs"
                v-on="on"
                :href="`tel:${phone}`"
                @click.stop
              >
                <v-icon class="icon" color="#04092152">
                  mdi-phone-outline
                </v-icon>
              </v-btn>
            </template>
            <span> {{ phone }} </span>
          </v-tooltip>
  
          <!-- Address -->
          <v-tooltip bottom v-if="address">
            <template v-slot:activator="{ on, attrs }">
              <v-btn
                fab
                x-small
                elevation="0"
                class="btnInit m-1"
                v-bind="attrs"
                v-on="on"
                @click.stop
              >
                <v-icon class="icon" color="#04092152">
                  mdi-home-outline
                </v-icon>
              </v-btn>
            </template>
            <span> {{ address }} </span>
          </v-tooltip>
        </div>
      </div>
    </div>
  </template>

  <script>
  export default {
    props: {
      name: {
        type: String,
        required: true,
      },
      photo: {
        type: String,
        default: () => "",
      },
      description: {
        type: String,
        default: () => "",
      },
      gender: {
        type: String,
        default: () => "male",
      },
      iconOnly: {
        type: Boolean,
        default: () => false,
      },
      phone: {
        type: String,
        default: () => "",
      },
      email: {
        type: String,
        default: () => "",
      },
      extra: {
        type: String,
        default: () => "",
      },
      address: {
        type: String,
        default: () => "",
      },
     
    },
    computed: {
      name_chip() {
        return this.name
          .split(" ")
          .filter((n) => n.trim() != "")
          .map((n) => n.substring(0, 1))
          .join("")
          .substring(0, 2)
          .toUpperCase();
      },
    },
  };
  </script>
  
  <style lang="scss" scoped>
  $theme-colors: (
    "fleet": #4a469c,
    "white": white,
    "purple": #924ac7,
    "light_info": transparentize(#d0ddf4, 0.5),
    "light_gray": darken(#ffffff, 10%),
    "light_blue": #f0f7fc,
  );
  
  .auth-img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 50%;
  }
  
  .image {
    position: relative;
    width: 46px;
    height: 46px;
    margin-right: 10px;
    border-radius: 50%;
  }
  .icon {
    width: 10.05px;
    height: 7.537px
  }
  .name-photo-container {
    display: flex;
    align-items: center;
    cursor: pointer;
  
    > .fleet-image-text {
      width: 3.5rem;
      height: 3.5rem;
      border-radius: 50%;
      outline: none;
      border: 1px solid darken(#ffffff, 10%);
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 1.5rem;
      background: map-get($theme-colors, "fleet");
      color: white;
    }
  
    .name-photo-name-desc {
      display: flex;
      flex-direction: column;
      margin-left: 0.5rem;
  
      .name-extra {
        font-size: 0.8rem;
        color: map-get($theme-colors, "light_gray");
      }
  
      .name-photo-name {
        font-size: 1.1rem;
      }
  
      .name-photo-desc {
        color: map-get($theme-colors, "light_gray");
        font-size: 0.9rem;
      }
  
      .contact-icons {
        display: flex;
        margin-top: 0.5rem;
  
        .btnInit {
          border: 1px solid #d0ddf4;
          background-color: white !important;
          width: 25px !important;
          height: 25px !important;
          margin: 0px 4px 0px 4px;
        }
      }
    }
  
    @media (max-width: 768px) {
      .name-photo-name-desc {
        .name-photo-name,
        .name-photo-desc,
        .name-extra {
          font-size: 0.9rem;
        }
  
        .contact-icons {
          .btnInit {
            width: 20px !important;
            height: 20px !important;
          }
        }
      }
    }
  }
  
  .male-list {
    border: 3px solid #1a73eb;
    border-radius: 50%;
    position: relative;
  }
  
  .male-list:before {
    content: "";
    width: 34px;
    height: 20px;
    position: absolute;
    transform: rotate(4deg); 
    right: -30px;
    top: 0;
    background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACEAAAAfCAYAAABplKSyAAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAAyhpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADw/eHBhY2tldCBiZWdpbj0i77u/IiBpZD0iVzVNME1wQ2VoaUh6cmVTek5UY3prYzlkIj8+IDx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IkFkb2JlIFhNUCBDb3JlIDUuNi1jMTQ1IDc5LjE2MzQ5OSwgMjAxOC8wOC8xMy0xNjo0MDoyMiAgICAgICAgIj4gPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4gPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIgeG1sbnM6eG1wPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvIiB4bWxuczp4bXBNTT0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL21tLyIgeG1sbnM6c3RSZWY9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9zVHlwZS9SZXNvdXJjZVJlZiMiIHhtcDpDcmVhdG9yVG9vbD0iQWRvYmUgUGhvdG9zaG9wIENDIDIwMTkgKE1hY2ludG9zaCkiIHhtcE1NOkluc3RhbmNlSUQ9InhtcC5paWQ6MDdGMjg4ODQ3RDREMTFFQTkxRTdBODgyMDU2MUYyOUIiIHhtcE1NOkRvY3VtZW50SUQ9InhtcC5kaWQ6MDdGMjg4ODU3RDREMTFFQTkxRTdBODgyMDU2MUYyOUIiPiA8eG1wTU06RGVyaXZlZEZyb20gc3RSZWY6aW5zdGFuY2VJRD0ieG1wLmlpZDowN0YyODg4MjdENEQxMUVBOTFFN0E4ODIwNTYxRjI5QiIgc3RSZWY6ZG9jdW1lbnRJRD0ieG1wLmRpZDowN0YyODg4MzdENEQxMUVBOTFFN0E4ODIwNTYxRjI5QiIvPiA8L3JkZjpEZXNjcmlwdGlvbj4gPC9yZGY6UkRGPiA8L3g6eG1wbWV0YT4gPD94cGFja2V0IGVuZD0iciI/PjoR2k4AAAFPSURBVHjaYvz//z/DQAMmhkEARh0BAyzUMki65I0BkPLHowQkf+Bpj8hEdAlGaiRMoAMCgNR6IpUbAh1ygRbRkUCC2ge0ShMNQPyRCHUPgaHwgSaOgAZvATmhQO3cAXLIBwJqDtDMEdCcsR+IBQYkJIAOACXK80Q4gDaOADoAlCDn40qEWNIOdaMD6IAFQKoeh3QitHD6iM9RZJeYQMsFoAWTAxZpkKUBMB8D1TogJUacuYekEhPqgP1QX2JzgAN6aUjVCgyaA+7jcMBFIFYgxwFEOwJaN+DKghuhIfCB3PTFQmQWxJUDFgItT6A0mzMRcMAEPA4opIYD8IYENAvG48qCQAcsoFmjhlY5gOjoQKoDcOUAqjsAW0hsAGJ5PA74wEADwEREVbuQlg7AFhIF0KjQp2YWJAQwim1owgSl/A3UzAEkOWK0BzbiHQEQYAAC3X3BeInQVwAAAABJRU5ErkJggg==)
    no-repeat !important;
    background-size: 50% !important;
  }
    
  .female-list {
    border-color: #ff6a80 !important;
    border: 3px solid #ff6a80 !important;
    border-radius: 50%;
    position: relative;
  }
  
  .female-list:before {
    content: "";
    width: 24px;
    height: 20px;
    position: absolute;
    transform: rotate(-1deg);
    right: 1px;
    bottom: -23px;
    top: auto;
    background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABQAAAAWCAYAAADAQbwGAAAAAXNSR0IArs4c6QAAAPJJREFUOBHtVcERgjAQvMvw8Ikd0IF04FiOfsQO0oHhpT8txRIogRJ4+tG4RBMETIA33kzmcre5HbLcAdOA6Z1MceRCmmL4nE9ShUpECDSYpgw+JaYE66gzWRN7bZiQQPRtd5AHbAxhoLwP/Qn7mkzNzFBD/ozWHqOV/NSL0cjvsbNwgU1lA+eZSuzzCIevGKkVlt/aWGhSUgGi2M80GVkKPKGaXOYrAJe5jPmC+IdeGUksyYMOJKiwofMLKljJqq2OQ5uN3sobCNcu86QNn5Hz2Awbe8yVy5ZcEL8Vd4KoE/dDRltp80+J6xar32T/UJN5ASp3L2cjZH/2AAAAAElFTkSuQmCC)
      no-repeat;
    background-size: 35%;
  }
  </style>
  