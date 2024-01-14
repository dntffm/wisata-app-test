# Wisata App Test

## Tech and Stack
- Vuetify

  Vuetify strictly adheres to the Material Design guidelines. Wisata app requires a design language that aligns with Material Design principles, Vuetify might be a good fit.

- Nuxt 3

  Vuetify, being designed specifically for Vue.js, works well with Nuxt.js. You can easily integrate Vuetify components into your Nuxt.js project, ensuring a cohesive and visually appealing user interface.
- Vercel

  Easy deploy Nuxt project (and the others frontend project) into the cloud environtment using vercel

## Setup

Clone the project into your local:
``` Https
git clone https://github.com/dntffm/wisata-app-test.git
cd wisata-app-test

Make sure to install the dependencies:

```bash
# npm
npm install

# pnpm
pnpm install

# yarn
yarn install

# bun
bun install
```

## Development Server

Start the development server on `http://localhost:3000`:

```bash
# npm
npm run dev

# pnpm
pnpm run dev

# yarn
yarn dev

# bun
bun run dev
```

## Production

Build the application for production:

```bash
# npm
npm run build

# pnpm
pnpm run build

# yarn
yarn build

# bun
bun run build
```

Locally preview production build:

```bash
# npm
npm run preview

# pnpm
pnpm run preview

# yarn
yarn preview

# bun
bun run preview
```

## Implemented Page Route
```
# /stays/{property-slug}/?checkin={checkinDate}&number_of_room={numberOfRoom}&checkout={checkoutDate}&guest_per_room={guestPerRoom}
# example: http://localhost:3000/stays/the-langham-jakarta-9001948244/?guest_per_room=2&number_of_room=1&checkin=2024-06-25&checkout=2024-06-26
```
