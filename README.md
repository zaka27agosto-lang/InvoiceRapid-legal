# Páginas legales — InvoiceRapid PRO

Carpeta lista para publicar. Contiene **solo** los documentos legales públicos:

- `index.html`
- `privacy-policy.html`
- `terms.html`
- `cookies.html`
- `account-deletion.html`  ← la que exige Google Play (Data safety)

> No incluye nada del código ni documentos internos (`docs/` sí los tiene; no
> publiques `docs/`).

## Por qué hay que publicarlas

El repositorio de la app es **privado** y **GitHub Pages no está activado**
(`has_pages = false`). GitHub Pages en repos privados requiere plan de pago, por
eso las URLs antiguas (`https://zaka27agosto-lang.github.io/InvoiceRapid/...`)
devuelven **404**. Google Play rechazó el enlace de eliminación de cuenta por eso.

Opciones (**elige una**). En todas, el enlace de eliminación quedará como
`https://<tu-dominio>/account-deletion.html`.

---

## Opción A (recomendada) — GitHub Pages en un repo PÚBLICO nuevo

No hace falta ninguna cuenta nueva (ya tienes GitHub) y es gratis también para
apps comerciales. Solo se publican estos HTML, sin código.

```bash
cd legal-pages
git init
git add .
git commit -m "Legal pages for InvoiceRapid"
git branch -M main
# Crea ANTES el repo público en GitHub, p.ej. InvoiceRapid-legal
git remote add origin https://github.com/zaka27agosto-lang/InvoiceRapid-legal.git
git push -u origin main
```

Luego, en GitHub: **Settings → Pages → Source: Deploy from a branch → `main` / `/(root)` → Save**.

URL resultante (tarda ~1 min):

```
https://zaka27agosto-lang.github.io/InvoiceRapid-legal/account-deletion.html
```

## Opción B — Netlify Drop (arrastrar y soltar)

1. Entra en https://app.netlify.com/drop
2. Arrastra la carpeta `legal-pages`.
3. Te da una URL estable tipo `https://nombre.netlify.app`. Puedes renombrarla
   en Site settings.

Netlify permite uso comercial en su plan gratuito.

## Opción C — Vercel

Válido, pero el plan **Hobby es solo para uso no comercial**; para una app
comercial su ToS pide el plan Pro. Úsalo solo si asumes eso.

---

## Después de publicar (imprescindible)

1. **Google Play Console → App content → Data safety → Seguridad de los datos**:
   sustituye la URL de eliminación de cuenta por la nueva
   (`https://<tu-dominio>/account-deletion.html`) y guarda/revisa.
2. **App (`app.config.ts`)**: las URLs internas se leen de variables de entorno.
   Para que los enlaces "online" de la app funcionen, define en el build:

   ```
   LEGAL_PRIVACY_URL=https://<tu-dominio>/privacy-policy.html
   LEGAL_TERMS_URL=https://<tu-dominio>/terms.html
   LEGAL_COOKIES_URL=https://<tu-dominio>/cookies.html
   LEGAL_DELETION_URL=https://<tu-dominio>/account-deletion.html
   ```

   Si no se definen, la app usa los valores por defecto de `app.config.ts`
   (actualmente apuntan a las URLs rotas de GitHub Pages).

## Comprobación

Abre en el navegador la URL de `account-deletion.html` y verifica que carga
(no 404) y que los enlaces del menú (Privacidad, Términos, Cookies) también.
