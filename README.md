````markdown
# 🩸 Blood Donation Info Crawler

A Rust-powered data crawler that extracts educational content about **blood donation**, **blood types**, and related topics from trusted health organizations:

- [RedCrossBlood.org](https://www.redcrossblood.org)  
- [OneBlood.org](https://www.oneblood.org)

The crawler transforms the content into clean, structured **Markdown** files (`.md`) for use in documentation, offline reading, or integration into knowledge bases and static websites.

## 📌 Features

- Crawls official RedCross and OneBlood pages
- Automatically follows valid internal content links
- Converts HTML pages to Markdown with readable formatting
- Skips noisy tags: `<script>`, `<style>`, `<header>`, `<footer>`
- Uses headless Chromium for full JS support
- Automatically names output files based on the page URL
- Saves files in the `docs/` directory

## 🛠 Tech Stack

| Crate            | Purpose                                         |
|------------------|-------------------------------------------------|
| `chromiumoxide`  | Headless browser automation (Chromium)          |
| `htmd`           | HTML-to-Markdown converter                      |
| `tokio`          | Asynchronous runtime                            |
| `futures`        | Stream processing                               |
| `serde`          | Serialization / Deserialization (if extended)   |

## 🚀 Getting Started

### Prerequisites

- Rust (install via [rustup.rs](https://rustup.rs/))
- Google Chrome or Chromium (for the headless browser backend)

### Installation

```bash
git clone https://github.com/yourusername/data-crawler.git
cd data-crawler
cargo build --release
````

### Usage

```bash
cargo run --release
```

On execution, the crawler will:

1. Launch a headless Chromium browser.
2. Visit RedCross and OneBlood target pages.
3. Extract main content, convert to Markdown.
4. Save `.md` files under `./docs/`.

## 📂 Output Structure

After running, your `docs/` folder will contain files like:

```
docs/
├── what_is_blood.md
├── donation_process.md
├── why_donate_blood.md
├── blood_types_o_positive.md
└── eligibility_requirements.md
```

Filenames are derived from URL slugs, sanitized (`-` → `_`, `/` → `_`).

## 📸 Sample Markdown Output

**docs/why\_donate\_blood.md**

```markdown
# Why Donate Blood?

Every 2 seconds someone in the U.S. needs blood.

Donating blood can save lives, and it only takes about an hour. There are multiple donation types:

- **Whole blood**  
- **Platelets**  
- **Plasma**  

Visit [RedCrossBlood.org](https://www.redcrossblood.org) for full details.
```

## ✏️ Customization

* **Output directory**: change `let output_dir = PathBuf::from("./docs");` in `main.rs`.
* **CSS selectors**: adjust link selectors in the crawling loops:

  * RedCross: `"ul.rcb-secondary-links-container li a"`
  * OneBlood: `"ul.cmp__list__dropdown li a"`, `"ul.cmp-list__container li a"`, `"div.cmp-teaser__action-container a"`
* **Skipped tags & handlers**: modify `HtmlToMarkdown::builder()` setup.

## ⚠️ Known Limitations

* Breaking changes if site structure updates
* No deduplication/caching: re-runs will overwrite existing files
* Images remain as Markdown placeholders (`![alt]`) without downloading
* No CLI flags—logic is hardcoded in `main.rs`

## 👨‍💻 Author

**Nguyen Huynh Nhat Anh**
🔗 [GitHub](https://github.com/Lunarcd)

## 🤝 Contributing

Contributions, suggestions, and pull requests are welcome!
Please fork the repository and submit an issue or PR for review.

```
```