# AI Discoverability & SEO Frameworks

UrbanShift is optimized not just for human users and traditional search engines, but also for AI Agents (LLMs). This document explains the applied optimization strategies.

## 1. SEO (Search Engine Optimization)
- **Implementation**: We implemented standard SEO practices in `frontend/public/index.html`.
- **Features**: Meta title, description, viewport tags, accessibility tags, and a traditional `sitemap.xml` mapping all public routes.

## 2. AEO (Answer Engine Optimization) & GEO (Generative Engine Optimization)
- **Goal**: Help Generative AI tools (like ChatGPT, Perplexity, Gemini) extract direct answers from our site.
- **Implementation**: 
  - Added JSON-LD Structured Data to `index.html`. It explicitly defines the `WebSite`, `Organization`, and `Person` (Author) schemas.
  - Generative engines use these schemas to confidently answer questions like "Who created UrbanShift?" or "What is UrbanShift?".

## 3. LLMO (Large Language Model Optimization)
- **Goal**: Make the site structure friendly for web-browsing agents.
- **Implementation**: Created `frontend/public/llms.txt`. This is an emerging standard file that provides a concise, markdown-formatted summary of the platform's purpose, tech stack, and core features specifically written for AI parsers.

## 4. AISEO (AI Search Optimization)
- **Implementation**: Combined usage of `robots.txt`, clear semantic HTML structure (in React components), and optimized meta tags to ensure that when AI bots crawl the site, they are guided away from private dashboards and focused on public content.

## 5. E-E-A-T (Experience, Expertise, Authoritativeness, Trustworthiness)
- **Goal**: Satisfy Google's Quality Rater Guidelines.
- **Implementation**: 
  - **Authoritativeness & Trust**: Explicitly linking the Author ("Shubham Raj - Full Stack Developer") using the `<meta name="author">` and `<link rel="author">` tags.
  - **Expertise**: Connecting the author entity to the organization entity in the JSON-LD graph. Consistency across platforms ensures the identity index remains strong.
