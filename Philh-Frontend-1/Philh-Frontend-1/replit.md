# PhilHarvest Corporation

A Philippine agricultural supply chain and marketplace platform connecting Filipino farmers with buyers across the country.

## Run & Operate

- `pnpm --filter @workspace/philharvest run dev` — run the frontend (dev, auto-assigned port)
- `pnpm --filter @workspace/philharvest run typecheck` — typecheck the frontend
- No backend or database — this is a fully static frontend with mock data

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- Frontend: React 18 + Vite + Tailwind CSS
- UI: shadcn/ui components
- Routing: wouter (`WouterRouter` with `BASE_URL` for Replit proxy)
- Charts: recharts
- Forms: react-hook-form + zod
- State: React useState (no external state manager)
- Data: static mock data in `src/data/mockData.ts`

## Where things live

```
artifacts/philharvest/src/
  App.tsx               — All ~44 routes
  index.css             — CSS custom properties (earth-tone palette)
  data/mockData.ts      — All mock data (products, orders, users, etc.)
  types/index.ts        — Shared TypeScript types
  layouts/
    PublicLayout.tsx    — Navbar + Footer wrapper for public pages
    DashboardLayout.tsx — Role-based sidebar for all 4 portal roles
  components/shared/    — Navbar, Footer, ProductCard, StatusBadge, StatsCard, EmptyState, RoleSwitcher
  pages/
    public/             — 8 pages: Home, Marketplace, ProductDetail, About, Contact, Login, Register, ForgotPassword
    customer/           — 10 pages: Dashboard, Browse, Cart, Checkout, Orders, OrderTracking, Wishlist, Reviews, Notifications, Profile
    seller/             — 11 pages: Dashboard, Products, ProductForm, Inventory, Orders, Reports, Messages, Shipments, ReviewsPage, Profile
    logistics/          — 8 pages: Dashboard, Deliveries, Tracking, Drivers, Routes, ProofOfDelivery, DeliveryHistory, Notifications
    admin/              — 8 pages: Dashboard, Users, Products, Orders, Logistics, Reports, Content, Settings
```

## Architecture decisions

- Frontend-only, no backend integration — all data from `src/data/mockData.ts`
- Five user roles (Public, Customer, Seller, Logistics, Admin) with separate portal routing
- `RoleSwitcher` floating pill (bottom-right) uses `localStorage("demoRole")` for demo navigation between portals
- `DashboardLayout` reads `demoRole` from localStorage to show the correct sidebar and user info
- Earth/brown color palette using CSS custom properties: primary = brown, secondary = green, accent = golden yellow

## Product

PhilHarvest is a B2B/B2C agricultural marketplace for the Philippines with five distinct portals:
- **Public**: Browse marketplace, product listings, company info
- **Customer**: Cart, orders, wishlist, tracking, reviews
- **Seller/Farmer**: Product management, inventory, orders, sales reports, messaging
- **Logistics**: Shipment tracking, driver management, route planning, proof of delivery
- **Admin**: User management, product monitoring, analytics, content management, system settings

## User preferences

- Earth-tone color palette (brown primary, green secondary, golden yellow accent)
- Philippine context: Peso (₱) currency, Philippine regions, Filipino product names
- shadcn/ui components throughout
- No emojis in UI (unless in mock data strings)
- data-testid attributes on all interactive elements

## Gotchas

- `BASE_URL` must be set for wouter routing on Replit's proxy (handled in App.tsx)
- Port is injected via workflow env `PORT` — never hardcode a port in vite.config.ts
- Mock data is the single source of truth — editing `src/data/mockData.ts` affects all pages
- `User.status` type is `"active" | "suspended" | "pending"` (not "inactive")

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
