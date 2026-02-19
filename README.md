# Plextech Curriculum

A Jekyll-based static course website for the Plextech engineering curriculum at UC Berkeley. Designed for GitHub Pages deployment.

## Local Development

### Prerequisites

- Ruby 3.2+ (3.3.x recommended; matches GitHub Pages)
- Bundler (`gem install bundler`)

### Setup

```bash
bundle install
bundle exec jekyll serve
```

Open [http://localhost:4000](http://localhost:4000) in your browser.

### Live reload during development

```bash
bundle exec jekyll serve --livereload
```

## Deployment

Push to the `main` branch of a GitHub repository with GitHub Pages enabled. The site will build and deploy automatically.

## Project Structure

```
├── _config.yml          # Jekyll configuration
├── _layouts/
│   └── default.html     # Base page layout
├── _includes/
│   ├── header.html      # Navigation bar
│   └── footer.html      # Site footer
├── assets/
│   └── css/
│       └── main.css     # All styles
├── index.md             # Home page
├── schedule.md          # Weekly schedule
├── curriculum.md        # Curriculum modules
├── staff.md             # Staff & office hours
├── resources.md         # Links & references
├── announcements.md     # Course announcements
├── Gemfile              # Ruby dependencies
└── README.md
```

## Customization

- **Colors:** Edit CSS custom properties in `assets/css/main.css` (`:root` block)
- **Content:** Edit any `.md` file directly — uses standard Markdown + HTML
- **Navigation:** Update `_includes/header.html`
- **Config:** Update `_config.yml` for site title, semester, email, etc.
