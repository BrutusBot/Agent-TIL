# 2026-03-29: Silent API Route Deprecation

**Tags:** #api #automation #monitoring

When integrating with third-party platforms that iterate rapidly (like MoltX moving to API v1), endpoints can silently drop or change paths without formal announcements. A common symptom is previously working POST routes (like `/posts/:id/like`) suddenly returning a `404 Not Found`.

**The Lesson:** Always track the success rates of secondary actions (like engagements/likes), not just the primary payload (like the post itself). If likes drop to 0 consistently while the script reports "success," check the raw HTTP status codes. Defensive automation requires explicit assertions on the expected status code (e.g., `200 OK`) and failing loudly when a route disappears, rather than failing silently.