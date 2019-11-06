<template>
    <div id="app">



        <div id="wrapper" :class="[{'toggled': toggled && !this.$route.meta.hideToolbar}]">


            <div id="appContentWrapper" :class="[{'fr-no-toolbar': this.$route.meta.hideToolbar}]">


              <div class="bg-header col-md-10 col-sm-12 offset-md-1 offset-sm-0 no-padding px-5 py-2">

                <div class="container-fluid no-padding no-margin">
                  <div class="row no-padding no-margin full-width">

                    <div class="col-12 no-padding no-margin">

                        <div class="row no-padding no-margin full-width">

                          <div class="col-lg-auto col-md-12 no-padding no-margin d-block d-md-block">
                            <a href="/login" title="Password Reset Logo">
                              <img alt="This is a Logo" :src="require('@/assets/images/logo.svg')" class="header-image" />
                            </a>
                          </div>

                          <div class="col-auto d-block d-md-block no-padding no-margin icon-tray abs-right">

                            <a href="/contact" class="add-height">
                              <span class="reset-nav-icons">
                                <i class="fa fa-phone" aria-hidden="true"></i>
                              </span>
                            </a>
                            <a href="/" class="add-height">
                              <span class="reset-nav-icons">
                                <i class="fa fa-question-circle" aria-hidden="true"></i>
                              </span>
                            </a>

                          </div>

                        </div>

                    </div>
                  </div>
                </div>

              </div>



              <transition name="fade" mode="out-in">
                  <router-view :key="this.$route.fullPath"></router-view>
              </transition>



            </div>


            <footer class="col-md-10 col-sm-12 offset-md-1 offset-sm-0 bg-header py-5 text-white-50">
                <div class="container-fluid">

                    <div class="row px-5">

                        <div class="col-md-6 col-sm-12 footer-center">
                          <div class="py-2"><a href="/contact-us" class="link-white">Contact</a></div>
                          <div class="py-2"><a href="/help" class="link-white">Help</a></div>
                          <div class="py-2"><a href="/" class="link-white">Online Privacy Statement</a></div>
                        </div>

                        <div class="col-md-6 col-sm-12">
                            <div class="center"><h4 class="text-white">Secured Site <i class="fa fa-lock" aria-hidden="true"></i></h4></div>
                            <div class="center py-3">
                              <img alt="This is a Logo" :src="require('@/assets/images/logo.svg')" class="footer-image" />
                            </div>
                            <div class="d-block center">
                              <span>A division of Zions Bancorporation, N.A., Member FDIC</span>
                            </div>
                        </div>

                    </div>

                </div>

            </footer>


        </div>




        <!--
          Application View
        -->
        <notifications group="IDMMessages" position="bottom left" width="320" :duration="4000">
            <template slot="body" slot-scope="props">
                <div :class="[{ 'alert-success': (props.item.type == 'success'), 'alert-warning': (props.item.type == 'warning'), 'alert-danger': (props.item.type == 'error'), 'alert-info': (props.item.type == 'info')}, 'alert', 'alert-dismissible', 'd-flex', 'p-3', 'pr-5', 'position-relative']" role="alert">
                    <div :class="[{ 'text-success': (props.item.type == 'success'), 'text-warning': (props.item.type == 'warning'), 'text-danger': (props.item.type == 'error'), 'text-info': (props.item.type == 'info')}, 'alert-icon', 'mr-3', 'align-self-top']">
                        <i :class="[{ 'fa-check-circle': (props.item.type == 'success'), 'fa-exclamation-triangle': (props.item.type == 'warning'), 'fa-times-circle': (props.item.type == 'error'), 'fa-info-circle': (props.item.type == 'info')}, 'fa', 'fa-lg']"></i>
                    </div>
                    <div class="fr-alert-content align-self-center">
                        <p class="mb-0 text-left" v-html="props.item.text"></p>
                    </div>
                    <a class="close" @click="props.close">
                        <i class="fa fa-times"></i>
                    </a>
                </div>
            </template>
        </notifications>
    </div>
</template>

<script>
import ToolbarNotification from '@/components/utils/ToolbarNotification';
import _ from 'lodash';

export default {
    name: 'App',
    components: {
        'fr-notification': ToolbarNotification
    },
    data: function () {
        return {
            toggled: false
        };
    },
    methods: {
        onToggle () {
            this.toggled = !this.toggled;
        },
        accessIcon (icon) {
            let iconClass = 'fa fa-fw mr-3 ';

            if (icon.length) {
                iconClass = iconClass + icon;
            } else {
                iconClass = iconClass + 'fa-cube';
            }

            return iconClass;
        }
    },
    filters: {
        capitalize: function (value) {
            return _.capitalize(value);
        }
    }
};
</script>

<!--
  Main Application CSS

  lang="scss" to turn on LESS CSS
-->
<style lang="scss">
    // For theming please see https://getbootstrap.com/docs/4.0/getting-started/theming/
    // Variable must come before bootstrap (to override them)
    // Currently variable and theming loaded through node
    @import "~bootstrap/scss/bootstrap.scss";
    @import "scss/main.scss";
    @import "scss/pw-reset.scss";
    @import "~bootstrap-vue/dist/bootstrap-vue.css";
    @import "~@fortawesome/fontawesome-free/css/all.css";

    #app {
        -webkit-transition: all 0.2s ease;
        -moz-transition: all 0.2s ease;
        -o-transition: all 0.2s ease;
        transition: all 0.2s ease;

        .container, .container-fluid {
            @media(min-width:768px) {
                padding-left: $grid-gutter-width;
                padding-right: $grid-gutter-width;
            }
        }

        .fr-main-dropdown {
            .dropdown-menu {
                padding-top: 0;
                padding-bottom: 0;
            }
        }

        #wrapper {
            height: 100%;

            #appSidebarWrapper {
                position: fixed;
                top: 0;
                width: 0;
                height: 100%;
                z-index: 2;
                margin-left: -$fr-sidebar-nav-width;
                overflow: hidden;
                background: $fr-sidebar-nav-background-color;

                -webkit-transition: all 0.2s ease;
                -moz-transition: all 0.2s ease;
                -o-transition: all 0.2s ease;
                transition: all 0.2s ease;

                a {
                    text-align: left;
                }

                .sidebar-brand-logo {
                    display: block;
                }

                .sidebar-brand-mark {
                    display: none;
                }

                @media(min-width:768px) {
                    width: $fr-sidebar-nav-minimized-width;
                    margin-left: 0;

                    .sidebar-brand-logo {
                        display: none;
                    }

                    .sidebar-brand-mark {
                        display: block;
                    }

                    .sidebar-item-text {
                        display: none;
                    }
                }
            }

            #appContentWrapper {
                // height: 100%;
                -webkit-transition: all 0.2s ease;
                -moz-transition: all 0.2s ease;
                -o-transition: all 0.2s ease;
                transition: all 0.2s ease;
                padding-left: 0;

                @media(min-width:768px) {
                    padding-left: $fr-sidebar-nav-minimized-width;
                }

                &.fr-no-toolbar {
                    @media(min-width:768px) {
                        padding-left: 0;
                    }
                }

                .fr-main-nav-toggle {
                    color: $fr-toolbar-color;
                }

                .navbar-nav {
                    .dropdown-menu {
                        position: absolute;
                        float: left;
                    }

                    .nav-link {
                        color: $fr-toolbar-color;
                    }
                }
                >.container {
                    padding-top: $grid-gutter-width;
                    padding-bottom: $grid-gutter-width * 2;
                }
            }

            &.toggled {
                #appSidebarWrapper {
                    width: $fr-sidebar-nav-width;
                    margin-left: 0;

                    .sidebar-brand-logo {
                        display: block;
                    }

                    .sidebar-brand-mark {
                        display: none;
                    }

                    @media(min-width:768px) {
                        .sidebar-brand-logo {
                            display: block;
                        }

                        .sidebar-brand-mark {
                            display: none;
                        }

                        .sidebar-item-text {
                            display: inline;
                        }
                    }
                }

                #appContentWrapper {
                    z-index: 1;
                    padding-left: $fr-sidebar-nav-width;
                    margin-right: -$fr-sidebar-nav-width;

                    @media(min-width:768px) {
                        position: relative;
                        padding-left: $fr-sidebar-nav-width;
                        margin-right: 0;

                    }
                }
            }
        }

        /* Sidebar Styles */
        .sidebar-nav {
            position: absolute;
            top: 0;
            width: $fr-sidebar-nav-width;
            margin: 0;
            padding: 0;
            list-style: none;

            li {
                a {
                    color: $fr-sidebar-nav-link-color;
                    display: block;
                    border-left: 3px solid $fr-sidebar-nav-link-border-color;
                    text-decoration: none;
                    padding: 10px 20px 10px 17px;
                    -webkit-transition: all 0.2s ease;
                    -moz-transition: all 0.2s ease;
                    -o-transition: all 0.2s ease;
                    transition: all 0.2s ease;

                    &.router-link-active {
                        color: $fr-sidebar-nav-link-hover-color;
                        background: $fr-sidebar-nav-link-active-color;
                        border-left-color: $fr-sidebar-nav-link-active-border-color;
                    }

                    &:hover {
                        color: $fr-sidebar-nav-link-hover-color;
                        background: darken($fr-sidebar-nav-link-active-color,3.0%);
                    }
                }
            }

            >.sidebar-brand {
                height: $navbar-height;
                font-size: 18px;
                line-height: 72px;
                background-color: $fr-sidebar-nav-brand-color;
                width: 100%;
                top: 0;
                -webkit-transition: all 0.2s ease;
                -moz-transition: all 0.2s ease;
                -o-transition: all 0.2s ease;
                transition: all 0.2s ease;

                a {
                    color: $fr-sidebar-nav-link-color;
                    width: 100%;
                    height: 100%;
                    padding: 0 20px 0 17px;

                    &:hover {
                        color: $fr-sidebar-nav-link-hover-color;
                        background: $fr-sidebar-nav-background-color;
                    }
                }
            }
        }
    }

    .modal-open {
        #app {
            #wrapper {
                #appSidebarWrapper {
                    z-index: 0;
                }
            }
        }
    }
</style>
