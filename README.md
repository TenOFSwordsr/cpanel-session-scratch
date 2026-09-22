# cPanel Login Scratch

A throwaway folder of artifacts from probing a cPanel/WHM login flow, not a real project. It holds a
captured login page, the JSON the login endpoint returned, a curl-written session cookie, and a
mis-named cookie jar. Useful only as evidence of a manual authentication test against a hosting
control panel; there is no reusable code and no source to build.

**Suggested repo name:** `cpanel-login-scratch`
**Stack:** Captured HTML/JSON artifacts from a `curl`/HTTP session (cPanel Jupiter theme)
**Status:** data only
**Last modified:** 2026-08-24

## What it does

Nothing on its own - these are outputs from one interactive login attempt:

- `login_page.html` (46 KB) - the cPanel login form as served by the host, `<title>cPanel Login</title>`,
  with the Jupiter-theme assets and a `/login/` form action.
- `login_result.json` - the JSON response to a login `POST`: `status: 1` (success), a `security_token`
  of the form `/cpsess##########`, and a `redirect` into `/cpsess##########/frontend/jupiter/index.html`.
- `cp.jar` - despite the `.jar` name this is not a Java archive: it is a Netscape HTTP cookie file
  written by libcurl, holding a `cpsession` cookie for `nphost3.unitedhost.com`.
- `token.txt` - a 2-byte stub, effectively an empty/placeholder token file.

## Layout

```
login_page.html     captured cPanel sign-in page
login_result.json   login POST response (security token + redirect)
cp.jar              mis-named curl cookie jar (cpsession cookie)
token.txt           2-byte empty token stub
```

## Notes

- **Contains a live session secret.** `cp.jar` carries a `cpsession` cookie value and
  `login_result.json` a `cpsess` security token for `nphost3.unitedhost.com`. Both are usable
  authentication material. Do not publish this folder as-is; delete the cookie/token or the whole
  folder before any public push.
- The `.jar` extension is wrong - it is a cookie jar, not a Java/Android archive, and will not open
  as one.
- No credentials (username/password) are stored in these files themselves, only the resulting session
  artifacts. The panel host suggests this was a personal hosting account rather than one of the
  developer's own codebases.
- Recommend simply deleting this folder rather than publishing it.
