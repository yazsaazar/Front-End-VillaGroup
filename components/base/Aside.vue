<template lang="">
  <aside
    class="sidenav navbar navbar-vertical navbar-expand-xs border-0 border-radius-xl my-3 fixed-start ms-3"
    id="sidenav-main"
  >
    <div class="sidenav-header">
      <i
        class="fas fa-times p-3 cursor-pointer text-secondary opacity-5 position-absolute end-0 top-0 d-none d-xl-none"
        aria-hidden="true"
        id="iconSidenav"
      ></i>
      <a
        class="navbar-brand m-0"
        href=" https://demos.creative-tim.com/soft-ui-dashboard-pro/pages/dashboards/default.html "
        target="_blank"
      >
        <span class="ms-1 font-weight-bold">Sistema de Resguardos</span>
      </a>
    </div>
    <hr class="horizontal dark mt-0" />
    <div
      class="collapse navbar-collapse w-auto h-auto"
      id="sidenav-collapse-main"
    >
      <ul class="navbar-nav">
        <li class="nav-item">
          <a
            data-bs-toggle="collapse"
            href="#dashboardsExamples"
            class="nav-link"
            aria-controls="dashboardsExamples"
            role="button"
            aria-expanded="false"
          >
            <div
              class="icon icon-shape icon-sm shadow border-radius-md bg-white text-center d-flex align-items-center justify-content-center me-2"
            >
            <svg
            width="12px"
            height="12px"
            viewBox="0 0 512 512"
            version="1.1"
            xmlns="http://www.w3.org/2000/svg"
            xmlns:xlink="http://www.w3.org/1999/xlink"
          >
            <title>computer</title>
            <g
              stroke="none"
              stroke-width="1"
              fill="none"
              fill-rule="evenodd"
            >
              <g
                fill="#000000"
              >
                <path
                  d="M448,0 L64,0 C28.648,0 0,28.648 0,64 L0,320 L0,512 L512,512 L512,320 L512,64 C512,28.648 483.352,0 448,0 Z M464,464 L48,464 L48,336 L464,336 L464,464 Z M464,288 L48,288 L48,96 L464,96 L464,288 Z"
                ></path>
              </g>
            </g>
          </svg>

            </div>
            <span class="nav-link-text ms-1">Recursos</span>
          </a>
          <div class="collapse" id="dashboardsExamples">
            <ul class="nav ms-4 ps-3">

              <li class="nav-item">
                <a
                  class="nav-link"
                  data-bs-toggle="collapse"
                  aria-expanded="false"
                  href="#vrExamples"
                >
                  <span class="sidenav-mini-icon"> E </span>
                  <span class="sidenav-normal">
                    Equipos <b class="caret"></b
                  ></span>
                </a>
                <div class="collapse" id="vrExamples">
                  <ul class="nav nav-sm flex-column">

                    <li class="nav-item">
                      <nuxtLink class="nav-link" to="/equipos/tipos">
                        <span class="sidenav-mini-icon"> T </span>
                        <span class="sidenav-normal"> Tipos </span>
                      </nuxtLink>
                    </li>

                    <li class="nav-item">
                      <nuxtLink class="nav-link" to="/equipos/equipos">
                        <span class="sidenav-mini-icon"> E </span>
                        <span class="sidenav-normal"> Equipos </span>
                      </nuxtLink>
                    </li>


                  </ul>
                </div>
              </li>
              <li class="nav-item">
                <nuxtLink class="nav-link" to="/recursos/resguardos">
                  <span class="sidenav-mini-icon"> R </span>
                  <span class="sidenav-normal"> Resguardos </span>
                </nuxtLink>
              </li>

              <li class="nav-item">
                <nuxtLink class="nav-link" to="/recursos/dictamenes">
                  <span class="sidenav-mini-icon"> D </span>
                  <span class="sidenav-normal"> Dictamenes </span>
                </nuxtLink>
              </li>

            </ul>
          </div>
        </li>
        <li class="nav-item mt-3">
          <h6
            class="ps-4 ms-2 text-uppercase text-xs font-weight-bolder opacity-6"
          >
            Administración
          </h6>
        </li>

        <li class="nav-item">
          <a
            data-bs-toggle="collapse"
            href="#pagesExamples"
            class="nav-link"
            aria-controls="pagesExamples"
            role="button"
            aria-expanded="false"
          >
            <div
              class="icon icon-shape icon-sm shadow border-radius-md bg-white text-center d-flex align-items-center justify-content-center me-2"
            >
            <svg
            xmlns="http://www.w3.org/2000/svg"
            width="12px"
            height="12px"
            viewBox="0 0 24 24"
            fill="none"
            stroke="#000000"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          >
            <path
              d="M12 2c2.76 0 5 2.24 5 5s-2.24 5-5 5-5-2.24-5-5 2.24-5 5-5zM12 14s-8 4.5-8 8h16c0-3.5-8-8-8-8z"
            ></path>
          </svg>

            </div>
            <span class="nav-link-text ms-1">Ubicación y personal</span>
          </a>
          <div class="collapse" id="pagesExamples">
            <ul class="nav ms-4 ps-3">
              <li class="nav-item">
                <a
                  class="nav-link"
                  data-bs-toggle="collapse"
                  aria-expanded="false"
                  href="#profileExample"
                >
                  <span class="sidenav-mini-icon"> U </span>
                  <span class="sidenav-normal">
                    Ubicación <b class="caret"></b
                  ></span>
                </a>
                <div class="collapse" id="profileExample">
                  <ul class="nav nav-sm flex-column">
                    <li class="nav-item">
                      <nuxtLink class="nav-link" to="/ubicacion/resorts">
                        <span class="sidenav-mini-icon"> R </span>
                        <span class="sidenav-normal"> Resorts </span>
                      </nuxtLink>
                    </li>

                    <li class="nav-item">
                      <nuxtLink class="nav-link" to="/ubicacion/departamentos">
                        <span class="sidenav-mini-icon"> D </span>
                        <span class="sidenav-normal"> Departamentos </span>
                      </nuxtLink>
                    </li>

                    <li class="nav-item">
                      <nuxtLink class="nav-link" to="/ubicacion/areas">
                        <span class="sidenav-mini-icon"> A </span>
                        <span class="sidenav-normal"> Areas </span>
                      </nuxtLink>
                    </li>
                  </ul>
                </div>
              </li>
              <li class="nav-item">
                <a
                  class="nav-link"
                  data-bs-toggle="collapse"
                  aria-expanded="false"
                  href="#usersExample"
                >
                  <span class="sidenav-mini-icon"> P </span>
                  <span class="sidenav-normal">
                    Personal <b class="caret"></b
                  ></span>
                </a>
                <div class="collapse" id="usersExample">
                  <ul class="nav nav-sm flex-column">

                    <li class="nav-item">
                      <nuxtLink class="nav-link" to="/personal/colaboradores">
                        <span class="sidenav-mini-icon"> C </span>
                        <span class="sidenav-normal"> Colaboradores </span>
                      </nuxtLink>
                    </li>

                    <li class="nav-item">
                      <nuxtLink class="nav-link" to="/personal/usuarios">
                        <span class="sidenav-mini-icon"> U </span>
                        <span class="sidenav-normal"> Usuarios </span>
                      </nuxtLink>
                    </li>
                  </ul>
                </div>
              </li>
            </ul>
          </div>
        </li>
      </ul>
    </div>
  </aside>
</template>

