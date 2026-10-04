# Developer Workflow

## Git Flow
We follow a simplified Trunk-Based Development approach:
1. `main` is the primary branch.
2. Commits are pushed directly for minor fixes, or PRs are used for large features.
3. Vercel and Render automatically deploy upon pushes to `main`.

## Local Setup
1. **Clone the Repo**
2. **Backend**:
   - `cd backend`
   - `python -m venv venv`
   - `venv\Scripts\activate` (Windows)
   - `pip install -r requirements.txt`
   - `python manage.py migrate`
   - `python manage.py runserver`
3. **Frontend**:
   - `cd frontend`
   - `npm install`
   - `npm start`

## Component Structure (React)
- **Lazy Loading**: Major routes are lazy-loaded (`React.lazy()`) in `App.js` to improve initial load time.
- **Context**: Global state like themes or auth is managed via Context API.
- **Styling**: Mixed usage of Tailwind utilities and vanilla CSS for granular control.
