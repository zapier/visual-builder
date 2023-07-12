---
order: 1000
exclude: true
---

<script>
(function() {
  var fallbackUrl = 'https://github.com/zapier/zapier-platform/blob/master/packages/schema/docs/build/schema.md';
  var hash = window.location.hash;
  var hashParts, newAnchor, version;
  if (hash) {
    hashParts = window.location.hash.split('@');
    if (hashParts.length === 2) {
      newAnchor = hashParts[0];
      version = hashParts[1];
      window.location.assign(`https://github.com/zapier/zapier-platform/blob/zapier-platform-schema@${version}/packages/schema/docs/build/schema.md${newAnchor}`);
    } else {
      window.location.assign(fallbackUrl);
    }
  } else {
    window.location.assign(fallbackUrl);
  }
})();
</script>
