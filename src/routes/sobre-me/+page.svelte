<script>
  import Button from "../../components/Button.svelte";
  import { page } from "$app/stores";
  import { onMount } from "svelte";

  let routeName;
  let cleanedRouteName;

  $: {
    $page.url.pathname;
    routeName = $page.url.pathname;
    cleanedRouteName = routeName.replace(/\//g, "");
  }

  onMount(() => {
    routeName = $page.url.pathname;
    cleanedRouteName = routeName.replace(/\//g, "");
  });
</script>

<Button />
<h3><a class="home-link" href="/">home</a>/{cleanedRouteName}</h3>
<section>
  <h2>Sobre Nosotros</h2>
  <p>
    Somos una empresa comprometida con la innovación y la excelencia en el
    desarrollo de software. Nuestro equipo está formado por profesionales
    apasionados por la tecnología y dedicados a brindar soluciones creativas y
    eficientes para nuestros clientes.
  </p>
</section>
<section>
  <h2>Nuestra Misión</h2>
  <p>
    Nuestra misión es proporcionar productos y servicios de alta calidad que
    impulsen el éxito de nuestros clientes. Nos esforzamos por crear soluciones
    innovadoras que generen un impacto positivo en la comunidad y contribuyan al
    avance tecnológico.
  </p>
</section>
<section>
  <h2>Nuestro Equipo</h2>
  <p>
    En nuestro equipo, valoramos la diversidad, la colaboración y el aprendizaje
    continuo. Estamos comprometidos con el crecimiento personal y profesional de
    nuestros miembros, promoviendo un ambiente de trabajo inclusivo y
    estimulante.
  </p>
</section>

<style>
  * {
    font-family: monospace;
    font-size: 18px;
  }

  .home-link {
    background: tan !important;
    font-size: 18px !important;
  }
</style>
