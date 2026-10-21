# portfolio-cms

A self-hosted Strapi 4 CMS on PostgreSQL, with Cloudinary media storage and a JWT-based users plugin, set up for Railway.

**Status:** Starter. The repo is a standard Strapi 4.26 project with its config files and dependencies, but `src/api` holds no content types, and the admin customisation files are examples only.

## The problem

The repo gives a content backend for a portfolio: a Strapi admin for editing content, a PostgreSQL database, and Cloudinary for images. The code is Strapi's own scaffold with its configuration filled in. No portfolio content models are defined in the repo.

## What it does

- Connects Strapi to PostgreSQL through `config/database.js` (`client: 'postgres'`).
- Stores uploaded media on Cloudinary through `@strapi/provider-upload-cloudinary`, configured in `config/plugins.js`.
- Enables the users and permissions plugin with a JWT secret read from the environment.
- Allows Cloudinary image and media sources in the Content Security Policy (`config/middlewares.js`).
- Adds an i18n plugin for content localisation.

## How it's built

- Strapi 4.26.0 on Node, with configuration split into `config/*.js` files.
- Environment variables drive the database, the JWT secret and the Cloudinary provider.
- `extensions/users-permissions/config/jwt.js` overrides the users plugin's JWT settings.
- Content types go in `src/api/`, which is currently empty except for a placeholder.

## Running it locally

```bash
pnpm install
pnpm develop    # Strapi dev server with admin UI
pnpm build      # build the admin panel
pnpm start      # run the built app
```

Open `/admin` after the first start to create the admin user.

## What's left

- No content types exist in `src/api/`, so the CMS has no portfolio data model yet.
- `src/admin/app.example.js` and `webpack.config.example.js` are examples only and are not wired in.
- A stray `phase2-scan.txt` is committed at the root with no documented purpose.
- No tests.
- Media is lost on redeploy unless the Cloudinary variables are set, because Railway's filesystem is ephemeral.
