<template>
  <footer class="footer px-4">
    <div class="row align-items-center justify-content-lg-between">
      <div class="col-lg-6">
        <div class="copyright text-center text-lg-left text-muted">
          © {{ year }}
          <a
            href="https://mechlintech.com/"
            class="font-weight-bold ml-1"
            target="_blank"
            >Mechlin Software Technologies </a
          >
        </div>
      </div>
      <div class="col-lg-6">
        <ul
          class="nav nav-footer justify-content-center justify-content-lg-end"
        >
          <li class="nav-item">
            <a
              href="https://mechlintech.com/#about"
              class="nav-link"
              target="_blank"
              >About Us</a
            >
          </li>
          <li class="nav-item">
            <a
              href="https://www.creative-tim.com/#contact"
              class="nav-link"
              target="_blank"
              >Contact</a
            >
          </li>
          <li class="nav-item">
            <a
              href="https://mechlintech.com/#portfolio"
              class="nav-link"
              target="_blank"
              >Protfolio</a
            >
          </li>
          <li class="nav-item">
            <a
              href="http://blog.creative-tim.com/#services"
              class="nav-link"
              target="_blank"
              >Services</a
            >
          </li>
        </ul>
      </div>
    </div>
  </footer>
</template>
<script>
export default {
  data() {
    return {
      year: new Date().getFullYear(),
    };
  },
};
</script>
<style></style>
