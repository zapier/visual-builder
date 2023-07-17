---
order: 1000
exclude: true
---

<script>
if (window.location.hash.startsWith('#ZD')) {
  window.location.assign(`${window.location.origin}/legacy/app-checks-reference${window.location.hash}`);
} else {
  window.location.assign(`${window.location.origin}/docs/integration-checks-reference${window.location.hash}`);
}
</script>
