# All Printable — home page

The marketing front door at **all-printable.com**. One page, plus redirects for
everything that used to live here.

```
docs/
  index.html          the home page
  404.html            points anything missing at the app
  CNAME robots.txt sitemap.xml
  assets/             the css, js and one preview image the page needs
  <40 directories>    one-line redirect stubs, see below
```

The printables themselves — seven makers, six category pages, 26 landing pages
and `/pro/` — live in **[all-printable-app-www]** and publish to
**app.all-printable.com**. That repo holds the product specs (`features/`), the
generators (`tools/`) and the Firestore rules.

[all-printable-app-www]: https://github.com/ptk-studio/all-printable-app-www

## The redirect stubs

Forty directories here contain nothing but a redirect to the same path on
`app.all-printable.com`. They exist because those URLs were indexed and linked:
deleting them would have thrown away the search rankings the landing pages were
built to earn.

Each stub is a 200 response carrying `rel=canonical` to the new URL, an instant
`meta refresh`, and a `location.replace` — the closest a GitHub Pages site can
get to a 301, since it cannot set response headers. They also work with
JavaScript off.

They can be deleted once search engines have followed them and the traffic has
moved, which takes months rather than weeks. Check Search Console before doing
it.

## Sign-in is not here

A Firebase auth session belongs to one origin, so signing in on
`all-printable.com` would leave you signed out on `app.all-printable.com`. The
header's "Sign in" is a link to the app, where the real control lives.

`all-printable.com` stays in the Firebase authorized-domains list anyway — drop
it and the OAuth redirect breaks if this page ever needs auth again.

## Run it

Any static server, or open `docs/index.html` directly:

```sh
cd docs && python3 -m http.server 8000
```

The home page's category cards are rendered from `assets/js/registry.js`, which
is still the catalogue's source of truth — it is duplicated in the app repo. If
you add a printable there, the counts here go stale until you copy it across.
