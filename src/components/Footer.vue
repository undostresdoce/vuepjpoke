<template>
  <footer class="footer" role="contentinfo" aria-label="Pie de página">
    <p class="footer__text">
      By
      <a
        href="https://github.com/undostresdoce"
        target="_blank"
        rel="noopener noreferrer"
        class="footer__link"
        aria-label="Ir al perfil de GitHub de Cvmi"
      >
        Cvmi 💫
      </a>
    </p>
    <p>¡Pokémon ゲット da ze!</p>
  </footer>
</template>

<script>
export default {}
</script>

<style scoped>
.footer {
  background-color: #2a75bb;
  color: #fff;
  text-align: center;
  padding: 1rem;
  margin-top: 2rem;
  border-top: 4px solid #ffcb05;
}
.footer__text {
  font-size: 0.9rem;
}
.footer__link {
  color: #ffcb05;
  text-decoration: none;
  font-weight: bold;
}
.footer__link:hover {
  text-decoration: underline;
}
</style>
