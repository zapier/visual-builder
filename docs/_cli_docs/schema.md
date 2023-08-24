---
# Note - this page current serves the Zapier CLI tooling which links to a page that no longer has content. This script is a redirect to the Github schema docs. We can remove this after all Zapier versions no longer make references to the old docs link here. Related ticket: https://zapierorg.atlassian.net/browse/PDE-4180
order: 1000
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
