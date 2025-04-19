# University Stock Club Website - Project Plan (Shadcn Style)

## 1. Project Goal

To create a modern, fast, and easy-to-maintain website for the university stock club using a clean, Shadcn-inspired component style. The site will feature a public-facing landing page, event listings, and articles, plus a secure admin dashboard for content management.

## 2. Technology Stack

*   **Frontend Framework:** SvelteKit
*   **UI Components:** **shadcn-svelte** (Utilizing its components and philosophy - copy/paste structure)
*   **Styling:** Tailwind CSS (Configured for shadcn-svelte and the specified color scheme)
*   **Backend & Database:** Supabase (PostgreSQL DB, Auth, Storage)
*   **Frontend Hosting:** Vercel / Netlify / Cloudflare Pages (Choose one)
*   **Version Control:** Git (e.g., GitHub, GitLab)
*   **Domain:** Custom Domain (to be purchased)

## 3. Architecture Overview

*   **Frontend:** SvelteKit application using **shadcn-svelte components** for UI elements, styled with Tailwind CSS. Hosted statically/serverlessly.
*   **Backend:** Supabase handles database, auth, storage.
*   **Data Flow:** SvelteKit app interacts directly with Supabase API via `supabase-js`. Public pages fetch read-only data; Admin pages (protected by Supabase Auth) perform CRUD operations.
*   **Rendering:** SSG/SSR for public content, CSR for dynamic parts and admin dashboard, managed by SvelteKit.

## 4. Project Structure (SvelteKit)

├── static/
├── src/
│ ├── app.html
│ ├── app.css # Global CSS / Tailwind base directives & CSS Variables
│ ├── hooks.server.js
│ ├── lib/
│ │ ├── components/
│ │ │ ├── ui/ # Copied shadcn-svelte components (Button, Card, Input etc.)
│ │ │ ├── shared/ # Composed components (Navbar, Footer using ui/ components)
│ │ │ ├── landing/ # Landing page specific composed sections
│ │ │ ├── events/ # Event specific composed sections/cards
│ │ │ ├── articles/ # Article specific composed sections/cards
│ │ │ └── admin/ # Admin dashboard specific composed sections/forms
│ │ ├── stores/
│ │ ├── utils/ # Utility functions & Shadcn utils (cn)
│ │ └── supabaseClient.js
│ ├── routes/ # (Structure remains the same as previous plan)
│ │ ├── +layout.svelte
│ │ ├── +page.svelte
│ │ ├── events/ ...
│ │ ├── articles/ ...
│ │ └── admin/ ...
│ └── service-worker.js
├── tests/
├── tailwind.config.js # Tailwind CSS configuration (KEY for colors/theme)
├── postcss.config.js
├── svelte.config.js
├── package.json
└── README.md


## 5. Core Features

*(Remains the same as previous plan: Content Management, Auth, DB Storage, Responsiveness, Routing)*

## 6. Styling Approach & Color Palette (60-30-10 Rule)

*   **UI Library:** Utilize `shadcn-svelte`. Install the CLI (`npx shadcn-svelte@latest init`) and add components as needed (`npx shadcn-svelte@latest add button card input ...`). This copies component source code into `src/lib/components/ui`.
*   **Theme:** White Theme (Light Mode Only initially, unless Dark Mode is planned).
*   **Color Palette (60-30-10):**
    *   **60% Dominant (Backgrounds):** White (`#FFFFFF` or similar) / Very Light Gray (`#F9FAFB` - Gray 50?). Used for main page backgrounds, card backgrounds. Configure as `background` and `card` colors in Tailwind theme/CSS variables.
    *   **30% Secondary (Supporting Elements):** Light Gray (`#E5E7EB` - Gray 200? or `#F3F4F6` - Gray 100?). Used for borders, subtle dividers, input backgrounds, secondary card backgrounds, hover states. Configure as `border`, `input`, `muted` colors.
    *   **10% Accent (Highlights):** **Green** (Choose a specific shade, e.g., Tailwind's `green-600` or `emerald-600`). Used for primary buttons, links, active states, key icons, special highlights (like the Investment Club card border/badge). Configure as `primary` color. Ensure good contrast, especially for text on this green (`primary-foreground` should likely be white).
*   **Tailwind Configuration (`tailwind.config.js` & `app.css`):**
    *   Follow `shadcn-svelte` setup instructions precisely for configuring colors using CSS variables. Define your White/Gray/Green palette using the variable names it expects (`--background`, `--foreground`, `--card`, `--primary`, `--accent`, `--muted`, etc.) in `app.css`.
    *   The `tailwind.config.js` will then reference these CSS variables.
*   **Component Styling:** Leverage the pre-styled `shadcn-svelte` components. Apply additional Tailwind utility classes for layout (Flexbox, Grid), spacing (`p-`, `m-`, `gap-`), and specific overrides *when necessary*. Avoid deep custom styling that breaks the Shadcn consistency.
*   **Typography:** Use Tailwind's font utilities. Configure a clean sans-serif font (like `Inter` or system fonts) in `tailwind.config.js`. Use `@tailwindcss/typography` plugin for nicely formatted article/event content.
*   **Responsiveness:** Built-in with Tailwind utilities (`sm:`, `md:`, etc.). Ensure `shadcn-svelte` components adapt well or compose them within responsive layouts.

## 7. Page Layout Plans (Conceptual Sections - Shadcn Style)

*(Focus on using `shadcn-svelte` components)*

### 7.1. Landing Page (`/`)

*   **Overall:** Clean, structured layout using cards and clear buttons.
*   **Sections:**
    *   **Hero Section:**
        *   **Content:** Headline, Sub-headline.
        *   **Components:** `<h1>`, `<p>`, `<Button variant="primary" size="lg">Join Us</Button>` (using the Green accent).
        *   **Layout:** Centered text over white/light gray background.
    *   **Brief About:** Simple text block.
    *   **Featured Activities Section:**
        *   **Content:** Section Title. Grid layout (`grid grid-cols-1 md:grid-cols-3 gap-4`).
        *   **Components:** Use `<Card>` components from `shadcn-svelte` for each activity.
            *   **Seminar/IDX Cards:** Standard `<Card>` (likely `bg-card` which is White/v.light gray) with `<CardHeader>`, `<CardContent>`, `<CardFooter>` containing a `<Button variant="secondary">Learn More</Button>` (using Gray).
            *   **Investment Club Card (Special):** Same `<Card>` structure, but visually distinct. Apply Tailwind classes: `border-primary` (Green border), potentially a `<Badge variant="default">Featured</Badge>` (using Green accent). The button inside could be `<Button variant="primary">Enroll Now</Button>`.
    *   **Article Highlights Section:**
        *   **Content:** Section Title. Grid of `<Card>` components.
        *   **Components:** Each card uses `<CardHeader>` (Title), `<CardContent>` (Excerpt), `<CardFooter>` with `<Button variant="outline" asChild><a href="/articles/...">Read More</a></Button>`.
    *   **Final Call to Action Section:**
        *   **Content:** Compelling text, `<Button variant="primary" size="lg">Become a Member</Button>`.
        *   **Layout:** Distinct background (e.g., `bg-muted` - Light Gray), centered.

### 7.2. Events Page (`/events`)

*   **Overall:** Clean grid or list using Cards.
*   **Sections:**
    *   **Page Header:** `<h1>Events</h1>`.
    *   **Filter/View Options (Optional):** `<Tabs>` or `<ToggleGroup>` components.
    *   **Event Listing:** Grid of `<Card>` components (reusable Event Card structure). Each card contains event info and a `<Button variant="secondary" asChild><a href="/events/...">View Details</a></Button>`.
    *   **Pagination (If needed):** Use `<Pagination>` component if available or build simple buttons.

### 7.3. Single Event Page (`/events/[id]`)

*   **Overall:** Detailed view using standard text elements and potentially cards for metadata.
*   **Sections:**
    *   **Event Header:** `<h1>{event.name}</h1>`.
    *   **Details Block:** Use simple `div`s with Flexbox/Grid and icons (e.g., Calendar, MapPin icons from `lucide-svelte`). Maybe a small `<Card>` for key details.
    *   **Full Description:** Rendered content area (potentially using `@tailwindcss/typography` styles via `prose`).
    *   **Registration CTA:** `<Button variant="primary">Register Now</Button>`.

### 7.4. Articles Page (`/articles`)

*   **Overall:** Similar structure to Events page, using Cards.
*   **Sections:**
    *   **Page Header:** `<h1>Articles</h1>`.
    *   **Filter/Search (Optional):** `<Input type="search" placeholder="Search articles..." />`.
    *   **Article Listing:** Grid of `<Card>` components (reusable Article Preview Card). Each with Title, Excerpt, Meta, `<Button variant="outline" asChild><a href="/articles/...">Read More</a></Button>`.
    *   **Pagination (If needed):** `<Pagination>` component.

### 7.5. Single Article Page (`/articles/[slug]`)

*   **Overall:** Focus on readability.
*   **Sections:**
    *   **Article Header:** `<h1>{article.title}</h1>`.
    *   **Metadata:** `<p className="text-muted-foreground">By {author} on {date}</p>`.
    *   **Featured Image (Optional).**
    *   **Article Body:** `<div>` with the `prose` class applied for typography styling.
    *   **Social Share Buttons (Optional):** Small `<Button variant="ghost" size="icon">` components with social icons.

### 7.6. Admin Dashboard (`/admin/*`)

*   **Overall:** Functional interface using `shadcn-svelte` form and data display components.
*   **Layout:** Sidebar navigation (`div` with links) + Main content area.
*   **Pages/Views:**
    *   **Login:** `<Card>` containing a form with `<Label>`, `<Input type="email">`, `<Input type="password">`, `<Button type="submit" variant="primary">Login</Button>`.
    *   **Manage Articles/Events:**
        *   **Components:** `<Table>` component (`<TableHeader>`, `<TableRow>`, `<TableHead>`, `<TableBody>`, `<TableCell>`) to display items. Action buttons (`<Button variant="outline" size="sm">Edit</Button>`, `<Button variant="destructive" size="sm">Delete</Button>`) within the table or use a `<DropdownMenu>` for actions. A `<Button variant="primary">Add New</Button>` typically placed above the table.
    *   **Add/Edit Forms:** Use `<form>` with `<Label>`, `<Input>`, `<Textarea>`, `<Select>`, `<Checkbox>`, `<DatePicker>` (if needed and available/added) components from `shadcn-svelte`. Use `<Button type="submit" variant="primary">Save</Button>`. Maybe wrap forms in a `<Card>`.

## 8. Next Steps

1.  Initialize SvelteKit project.
2.  Setup Git repository.
3.  **Install and initialize `shadcn-svelte` CLI.**
4.  **Configure Tailwind CSS & CSS variables in `app.css` for the White/Gray/Green theme.**
5.  Setup Supabase project.
6.  Install `supabase-js` and setup client.
7.  **Start adding required `shadcn-svelte` components (`ui/`) via CLI.**
8.  Develop base layout (`+layout.svelte`) using composed components (e.g., `Navbar`, `Footer` built from `ui/` components).
9.  Build pages and features section by section, composing UI from `shadcn-svelte` components and adding logic.
10. Implement Supabase data fetching/mutations and Auth guards for `/admin`.
11. Configure hosting and deploy.