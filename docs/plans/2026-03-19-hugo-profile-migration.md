# Hugo Profile Migration Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Replace deprecated Wowchemy/Hugo Academic with hugo-profile theme for a clean personal portfolio site with a custom vertical timeline for work experience.

**Architecture:** Single-page portfolio using hugo-profile v4 theme installed as a Hugo module. All content (bio, experience, education, projects, contact) is configured in a single `hugo.yaml` file. A custom CSS vertical timeline replaces the theme's default experience layout. Deployed via GitHub Actions to GitHub Pages using the modern `actions/deploy-pages` approach.

**Tech Stack:** Hugo 0.157+ (extended), hugo-profile theme, GitHub Actions, GitHub Pages

---

### Task 1: Create feature branch and clean up Wowchemy files

**Files:**
- Delete: `go.mod`, `go.sum` (if exists), `theme.toml`, `update_wowchemy.sh`
- Delete: `config/` directory (replaced by single `hugo.yaml`)
- Delete: `content/home/` (widget-based pages, replaced by hugo.yaml config)
- Delete: `content/authors/` (bio moves to hugo.yaml)
- Delete: `content/publication/` (dropping academic sections)
- Delete: `content/event/` (dropping academic sections)
- Delete: `content/slides/` (dropping academic sections)
- Delete: `content/post/` (dropping blog for now)
- Delete: `data/` directory (Wowchemy data files)
- Delete: `assets/` directory (Wowchemy assets)
- Delete: `public/` directory (build output, should be gitignored)
- Keep: `content/project/` (reference for project data migration)
- Keep: `static/uploads/` (resume PDF, GPG key)
- Keep: `images/` (if contains useful assets)
- Keep: `.github/` (will be updated in Task 6)
- Keep: `content/privacy.md`, `content/terms.md` (legal pages)

**Step 1: Create feature branch**

```bash
git checkout -b feat/hugo-profile-migration
```

**Step 2: Delete Wowchemy-specific files and directories**

```bash
rm -f go.mod go.sum theme.toml update_wowchemy.sh
rm -rf config/ content/home/ content/authors/
rm -rf content/publication/ content/event/ content/slides/ content/post/
rm -rf data/ assets/ public/
```

**Step 3: Commit the cleanup**

```bash
git add -A
git commit -m "chore: remove Wowchemy theme and widget-based content"
```

---

### Task 2: Set up hugo-profile theme via Hugo module

**Files:**
- Create: `go.mod`
- Create: `hugo.yaml` (main config, initially minimal)

**Step 1: Initialize Go module**

```bash
hugo mod init github.com/darkamaul/darkamaul.github.io
```

This creates a new `go.mod` file.

**Step 2: Create minimal `hugo.yaml` with theme import**

Create `hugo.yaml` at the project root:

```yaml
baseURL: "https://darkamaul.github.io"
languageCode: "en-us"
title: "Alexis Challande"

module:
  imports:
    - path: github.com/gurusabarish/hugo-profile

outputs:
  home:
    - "HTML"
    - "RSS"
    - "JSON"

enableRobotsTXT: true

markup:
  goldmark:
    renderer:
      unsafe: true

params:
  title: "Alexis Challande"
  description: "Security Engineer - Personal Website"
  favicon: "/fav.png"
  animate: true
  useBootstrapCDN: false

  theme:
    defaultTheme: "light"

  navbar:
    align: ms-auto
    brandName: "Alexis Challande"
    disableSearch: true
    stickyNavBar:
      enable: true
      showOnScrollUp: true
    menus:
      disableAbout: false
      disableExperience: false
      disableEducation: false
      disableProjects: false
      disableAchievements: true
      disableContact: false
```

**Step 3: Fetch the theme module**

```bash
hugo mod get -u
```

**Step 4: Verify Hugo can build (empty site, no errors)**

```bash
hugo --minify --gc 2>&1 | head -20
```

Expected: Build succeeds (may warn about missing content, but no errors).

**Step 5: Commit**

```bash
git add hugo.yaml go.mod go.sum
git commit -m "feat: add hugo-profile theme via Hugo modules"
```

---

### Task 3: Add hero, about, and contact sections to hugo.yaml

**Files:**
- Modify: `hugo.yaml`

**Data source:** Content migrated from `content/authors/alexis/_index.md` and `content/home/contact.md` (already deleted but captured in this plan).

**Step 1: Add hero section to `params` in `hugo.yaml`**

```yaml
  hero:
    enable: true
    intro: "Hi, my name is"
    title: "Alexis."
    subtitle: "Security Engineer"
    content: >-
      Security Engineer and Doctor in Cybersecurity.
      Interested in binary analysis, reverse engineering,
      and Android security.
    image: /images/avatar.jpg
    bottomImage:
      enable: false
    button:
      enable: true
      name: "Resume"
      url: /uploads/challande-cv.pdf
      download: true
      newPage: true
    socialLinks:
      fontAwesomeIcons:
        - icon: fab fa-github
          url: https://github.com/DarkaMaul
        - icon: fab fa-linkedin
          url: https://www.linkedin.com/in/alexis-challande/
        - icon: fab fa-x-twitter
          url: https://twitter.com/DarkaMaul
        - icon: fas fa-graduation-cap
          url: https://scholar.google.fr/citations?user=FbVm3psAAAAJ
```

**Step 2: Add about section to `params` in `hugo.yaml`**

```yaml
  about:
    enable: true
    title: "About Me"
    image: "/images/avatar.jpg"
    content: |-
      Alexis Challande obtained his PhD at Quarkslab in October 2022.
      His research interests include 1-day detection applied to embedded
      systems, AOSP security, and graph theories applied to binary analysis.
      His PhD was conducted in the GRACE team at the Laboratoire
      d'Informatique de l'Ecole Polytechnique (LiX).
    skills:
      enable: true
      title: "Areas of expertise:"
      items:
        - "Binary Analysis"
        - "Reverse Engineering"
        - "Android Security"
        - "IDA Scripting"
        - "Vulnerability Detection"
        - "Graph Theory"
```

**Step 3: Add contact section to `params` in `hugo.yaml`**

```yaml
  contact:
    enable: true
    content: >-
      Feel free to reach out if you have questions or just want to say hi.
    btnName: Mail me
    btnLink: mailto:alexis@challande.eu

  footer:
    socialNetworks:
      github: https://github.com/DarkaMaul
      linkedin: https://www.linkedin.com/in/alexis-challande/
      twitter: https://twitter.com/DarkaMaul
```

**Step 4: Copy avatar image to the right location**

If an avatar image exists in the old content, copy it. Otherwise, create a placeholder:

```bash
mkdir -p static/images
# Copy existing avatar if available, or add one manually later
```

**Step 5: Build and verify**

```bash
hugo server -D
```

Open http://localhost:1313 and verify hero, about, and contact sections render.

**Step 6: Commit**

```bash
git add hugo.yaml static/images/
git commit -m "feat: add hero, about, and contact sections"
```

---

### Task 4: Add experience section with vertical timeline

**Files:**
- Modify: `hugo.yaml` (experience data)
- Create: `assets/css/custom.css` (vertical timeline styles)
- Create: `layouts/partials/sections/experience.html` (override theme partial)

hugo-profile's default experience layout is a list, not a vertical timeline. We override the theme's experience partial with a custom one.

**Step 1: Add experience data to `params` in `hugo.yaml`**

```yaml
  experience:
    enable: true
    title: "Work Experience"
    items:
      - company: "Quarkslab"
        companyUrl: "https://www.quarkslab.com/"
        jobs:
          - name: "Security Engineer"
            date: "Sep 2019 - Dec 2022"
            content: |-
              Part of the Automated Analysis team, working on:

              - Detection of 1-day vulnerabilities in Android phones (PhD research)
              - Android Application Analysis
              - Tooling development
              - IDA Plugin development

      - company: "ANSSI"
        companyUrl: "https://www.ssi.gouv.fr/"
        jobs:
          - name: "Master Internship"
            date: "Mar 2018 - Aug 2018"
            content: |-
              Worked on the identification of cryptographic code
              in binary code.

      - company: "AXA CS"
        jobs:
          - name: "Apprentice in Cybersecurity"
            date: "Sep 2015 - Aug 2016"
            content: |-
              Worked in the Cybersecurity Team on the implementation
              of ISO 2700X norms.
```

**Step 2: Find the theme's experience partial path**

```bash
hugo mod vendor
find _vendor -name "experience*" -path "*/layouts/*"
```

This reveals the theme's experience template path. We'll override it by creating the same path under `layouts/`.

**Step 3: Create the custom experience partial**

Create `layouts/partials/sections/experience.html`. This overrides the theme's default. The exact template structure depends on what the theme's partial looks like (found in Step 2). The custom version should:

1. Keep the same Go template variables the theme uses
2. Replace the HTML structure with a vertical timeline layout
3. Use the same `experience.items` data from `hugo.yaml`

The HTML structure for the vertical timeline:

```html
{{ if .experience.enable }}
<section id="experience" class="py-5">
  <div class="container">
    <h2 class="mb-4">
      {{ if .experience.title }}
        {{ .experience.title }}
      {{ else }}
        Experience
      {{ end }}
    </h2>
    <div class="timeline">
      {{ range .experience.items }}
      <div class="timeline-item">
        <div class="timeline-dot"></div>
        <div class="timeline-content">
          {{ range .jobs }}
          <h4>{{ .name }}</h4>
          {{ end }}
          <h5>
            {{ if .companyUrl }}
              <a href="{{ .companyUrl }}" target="_blank">{{ .company }}</a>
            {{ else }}
              {{ .company }}
            {{ end }}
          </h5>
          {{ range .jobs }}
          <span class="timeline-date">{{ .date }}</span>
          {{ if .content }}
          <div class="timeline-description">
            {{ .content | markdownify }}
          </div>
          {{ end }}
          {{ end }}
        </div>
      </div>
      {{ end }}
    </div>
  </div>
</section>
{{ end }}
```

> **Note:** The exact Go template code will need to be adapted to match the theme's context variables (e.g., `.Site.Params.experience` vs `.experience`). Inspect the vendored theme partial first.

**Step 4: Create custom CSS for the vertical timeline**

Create `assets/css/custom.css`:

```css
.timeline {
  position: relative;
  padding: 1rem 0;
  margin-left: 1rem;
}

.timeline::before {
  content: '';
  position: absolute;
  left: 0;
  top: 0;
  bottom: 0;
  width: 2px;
  background: var(--bs-primary, #007bff);
}

.timeline-item {
  position: relative;
  padding-left: 2rem;
  padding-bottom: 2rem;
}

.timeline-item:last-child {
  padding-bottom: 0;
}

.timeline-dot {
  position: absolute;
  left: -6px;
  top: 0.25rem;
  width: 14px;
  height: 14px;
  border-radius: 50%;
  background: var(--bs-primary, #007bff);
  border: 2px solid var(--bs-body-bg, #fff);
}

.timeline-content h4 {
  margin-bottom: 0.1rem;
  font-size: 1.1rem;
}

.timeline-content h5 {
  font-size: 0.95rem;
  font-weight: normal;
  color: var(--bs-secondary-color, #6c757d);
  margin-bottom: 0.25rem;
}

.timeline-content h5 a {
  color: var(--bs-primary, #007bff);
  text-decoration: none;
}

.timeline-date {
  display: inline-block;
  font-size: 0.85rem;
  color: var(--bs-secondary-color, #6c757d);
  margin-bottom: 0.5rem;
}

.timeline-description {
  margin-top: 0.5rem;
}

.timeline-description ul {
  padding-left: 1.2rem;
}
```

**Step 5: Wire custom CSS into the theme**

Check if hugo-profile supports a `customCSS` param or if we need to override the `head` partial. The typical approach is to create `layouts/partials/custom-head.html`:

```html
<link rel="stylesheet" href="{{ "css/custom.css" | absURL }}">
```

Or use Hugo Pipes if available. Verify with:

```bash
grep -r "custom" _vendor/github.com/gurusabarish/hugo-profile/layouts/ | grep -i "css\|head\|style"
```

**Step 6: Build and verify the timeline renders**

```bash
hugo server -D
```

Open http://localhost:1313 and verify the experience section shows a vertical timeline.

**Step 7: Commit**

```bash
git add hugo.yaml layouts/ assets/css/
git commit -m "feat: add experience section with custom vertical timeline"
```

---

### Task 5: Add education and projects sections

**Files:**
- Modify: `hugo.yaml`

**Step 1: Add education data to `params` in `hugo.yaml`**

```yaml
  education:
    enable: true
    items:
      - title: "PhD in Binary Analysis"
        school:
          name: "Ecole Polytechnique"
          url: "https://www.polytechnique.edu"
        date: "2019 - 2022"
      - title: "Master in Digital Security"
        school:
          name: "Eurecom"
          url: "https://www.eurecom.fr"
        date: "2016 - 2018"
      - title: "BSc in Computer Science"
        school:
          name: "University Pierre & Marie Curie"
          url: "https://www.sorbonne-universite.fr"
        date: "2012 - 2015"
```

**Step 2: Add projects data to `params` in `hugo.yaml`**

Migrated from `content/project/`:

```yaml
  projects:
    enable: true
    items:
      - title: Quokka
        content: >-
          A Fast and Accurate Binary Exporter.
        image: /images/projects/quokka.png
        badges:
          - "Reverse Engineering"
          - "IDA Plugin"
        links:
          - icon: fab fa-github
            url: https://github.com/quarkslab/quokka
          - icon: fas fa-book
            url: https://quarkslab.github.io/quokka/

      - title: BGraph
        content: >-
          A tool for binary analysis using graph theory.
        badges:
          - "Binary Analysis"
          - "Graph Theory"
        links:
          - icon: fab fa-github
            url: https://github.com/quarkslab/bgraph

      - title: AOSP Dataset
        content: >-
          Dataset for Android Open Source Project analysis.
        badges:
          - "Android"
          - "Security"
```

**Step 3: Copy project images**

```bash
mkdir -p static/images/projects
# Copy quokka featured image if it exists
cp content/project/quokka/featured.png static/images/projects/quokka.png 2>/dev/null || true
```

**Step 4: Clean up old project content directory**

```bash
rm -rf content/project/
```

**Step 5: Build and verify**

```bash
hugo server -D
```

**Step 6: Commit**

```bash
git add hugo.yaml static/images/projects/
git add -A  # captures deleted content/project/
git commit -m "feat: add education and projects sections"
```

---

### Task 6: Update GitHub Actions workflow

**Files:**
- Modify: `.github/workflows/publish.yml`

Replace the old Wowchemy-era workflow with the modern Hugo + GitHub Pages approach.

**Step 1: Replace `.github/workflows/publish.yml` with:**

```yaml
name: Deploy Hugo site to GitHub Pages

on:
  push:
    branches: [master]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-latest
    env:
      HUGO_VERSION: "0.157.0"
    steps:
      - name: Install Hugo CLI
        run: |
          wget -O ${{ runner.temp }}/hugo.deb \
            https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.deb
          sudo dpkg -i ${{ runner.temp }}/hugo.deb

      - name: Checkout
        uses: actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4.2.2
        with:
          fetch-depth: 0

      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@f156874f8191504dae5b037505266ed5dda6c382 # v5

      - name: Install Node.js dependencies
        run: "[[ -f package-lock.json || -f npm-shrinkwrap.json ]] && npm ci || true"

      - name: Build with Hugo
        env:
          HUGO_CACHEDIR: ${{ runner.temp }}/hugo_cache
          HUGO_ENVIRONMENT: production
          TZ: Europe/Paris
        run: hugo --minify --gc --baseURL "${{ steps.pages.outputs.base_url }}/"

      - name: Upload artifact
        uses: actions/upload-pages-artifact@a753861a5debcf57bf8b404356158c8e1e33150c # v3
        with:
          path: ./public

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@9dbe3824824f8a1377b8e298bafde1a50ede43e5 # v4
```

**Step 2: Verify workflow syntax**

```bash
actionlint .github/workflows/publish.yml
```

**Step 3: Commit**

```bash
git add .github/workflows/publish.yml
git commit -m "feat: update GitHub Actions to modern Hugo + Pages deployment"
```

---

### Task 7: Clean up remaining files and finalize

**Files:**
- Delete: `content/privacy.md`, `content/terms.md` (unless you want to keep them)
- Delete: `images/` directory (if not used by new theme)
- Delete: `scripts/` directory (if it only contained Wowchemy scripts)
- Modify: `README.md` (brief update)
- Create: `.gitignore` (add `public/`, `resources/`, `_vendor/`)

**Step 1: Check what remains and clean up**

```bash
ls -la content/
ls -la scripts/
ls -la images/
```

Delete anything that's no longer referenced.

**Step 2: Ensure `.gitignore` includes build artifacts**

```
public/
resources/
_vendor/
.hugo_build.lock
```

**Step 3: Final local build and review**

```bash
hugo --minify --gc
hugo server
```

Walk through every section:
- [ ] Hero renders with name, title, social links, resume download
- [ ] About section shows bio and skills
- [ ] Experience shows vertical timeline with 3 positions
- [ ] Education shows 3 degrees
- [ ] Projects shows 3 projects with links
- [ ] Contact shows email button
- [ ] Dark/light mode toggle works
- [ ] Resume PDF downloads correctly
- [ ] Mobile responsive layout works

**Step 4: Commit**

```bash
git add -A
git commit -m "chore: clean up remaining files and finalize migration"
```

---

### Task 8: Open Pull Request

**Step 1: Push branch and create PR**

```bash
git push -u origin feat/hugo-profile-migration
gh pr create --title "Migrate from Wowchemy to hugo-profile" --body "$(cat <<'EOF'
## Summary

- Replace deprecated Wowchemy/Hugo Academic theme with hugo-profile
- Single-page portfolio: hero, about, experience (vertical timeline), education, projects, contact
- Custom vertical timeline CSS for work experience section
- Modern GitHub Actions deployment (actions/deploy-pages@v4)
- Hugo upgraded from 0.95 to 0.157

## Test plan

- [ ] Verify `hugo server` renders all sections correctly
- [ ] Verify vertical timeline displays experience chronologically
- [ ] Verify resume PDF download works
- [ ] Verify dark/light mode toggle
- [ ] Verify mobile responsive layout
- [ ] Verify GitHub Actions build succeeds
- [ ] Verify deployed site matches local preview

Generated with Claude Code
EOF
)"
```
