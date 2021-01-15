<template>
    <base-nav class="navbar-top navbar-dark"
              id="navbar-main"
              :show-toggle-button="false"
              expand>
        <form class="navbar-search navbar-search-dark form-inline mr-3 d-none d-md-flex ml-lg-auto">
            <div class="form-group mb-0">
                <!-- <base-input placeholder="Search"
                            class="input-group-alternative"
                            alternative=""
                            addon-right-icon="fas fa-search">
                </base-input> -->
            </div>
        </form>
        <ul class="navbar-nav align-items-center d-none d-md-flex">
            <li class="nav-item dropdown">
                <base-dropdown class="nav-link pr-0">
                    <div class="media align-items-center" slot="title">
                <span class="avatar avatar-sm rounded-circle">
                  <img alt="Image placeholder" src="data:image/png;base64,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">
                </span>
                        <div class="media-body ml-2 d-none d-lg-block">
                            <span class="mb-0 text-sm  font-weight-bold">Jessica Jones</span>
                        </div>
                    </div>

                    <template>
                        <div class=" dropdown-header noti-title">
                            <h6 class="text-overflow m-0">Welcome!</h6>
                        </div>
                        <!-- <router-link to="/profile" class="dropdown-item">
                            <i class="ni ni-single-02"></i>
                            <span>My profile</span>
                        </router-link>
                        <router-link to="/profile" class="dropdown-item">
                            <i class="ni ni-settings-gear-65"></i>
                            <span>Settings</span>
                        </router-link>
                        <router-link to="/profile" class="dropdown-item">
                            <i class="ni ni-calendar-grid-58"></i>
                            <span>Activity</span>
                        </router-link>
                        <router-link to="/profile" class="dropdown-item">
                            <i class="ni ni-support-16"></i>
                            <span>Support</span>
                        </router-link> -->
                        <div class="dropdown-divider"></div>
                        <router-link to="/profile" class="dropdown-item">
                            <i class="ni ni-user-run"></i>
                            <span>Logout</span>
                        </router-link>
                    </template>
                </base-dropdown>
            </li>
        </ul>
    </base-nav>
</template>
<script>
  export default {
    data() {
      return {
        activeNotifications: false,
        showMenu: false,
        searchQuery: ''
      };
    },
    methods: {
      toggleSidebar() {
        this.$sidebar.displaySidebar(!this.$sidebar.showSidebar);
      },
      hideSidebar() {
        this.$sidebar.displaySidebar(false);
      },
      toggleMenu() {
        this.showMenu = !this.showMenu;
      }
    }
  };
</script>
