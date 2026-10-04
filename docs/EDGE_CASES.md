# Edge Cases Handled

Throughout the development of UrbanShift, several complex edge cases were identified and handled:

1. **Database Migration & Expiry (Render to Neon)**
   - **Issue**: Render free tier deletes databases after 90 days.
   - **Solution**: Shifted primary DB to Neon Serverless Postgres. Added `populate_dummy_data.py` to instantly recover testing environments if data loss occurs.

2. **WebSocket Stability**
   - **Issue**: Connections dropping on Render or getting mismatched imports (`wsgi` vs `asgi`).
   - **Solution**: Explicitly ordered Daphne at the top of `INSTALLED_APPS` and strictly set `ASGI_APPLICATION = 'backend.asgi.application'`.

3. **Rate Limiting (429 Errors)**
   - **Issue**: Render's automated cron jobs or rapid user clicks triggered DRF throttling.
   - **Solution**: Implemented a lightweight, unthrottled `/health/` endpoint for Render cron jobs, and separated user-facing API rate limits (`1000/day`).

4. **Image Upload Bloat**
   - **Issue**: Users uploading 15MB+ images causing server timeouts.
   - **Solution**: Handled client-side and server-side image compression, keeping uploads under 6MB before pushing to Cloudinary.

5. **Console Unicode Errors (Windows)**
   - **Issue**: Python scripts crashing on Windows CMD due to Emojis in `print()` statements.
   - **Solution**: Sanitized logging output for cross-platform compatibility in `populate_dummy_data.py`.
