# Evidence - mobile gallery presence + mobile video upload (2026-10-06)

ONE clean final run, produced by `e2e/gallery-mobile/run_final.sh`
(build -> full automated suite -> fresh InMemory app on :5119 -> ONE Playwright
journey via `e2e/gallery-mobile/gallery_e2e.py`). No screenshots from any other
run are in this folder; the previous (section 104 keys) evidence set was
archived to `e2e/provider-keys/evidence-keys-recheck-104/` before this run.

## Automated suite (log-2-tests.txt)
- Unit: 486/486 passed. Integration: 454/454 passed (`dotnet test -m:1`),
  including the 11 new facts in
  `tests/DeChimex.IntegrationTests/Controllers/GalleryMobileSurfaceTests.cs`.

## Journey summary (log-5-journey.txt, journey-summary.json)
Environment: Development + InMemory; videos stored through the real storage
pipeline (ffmpeg present, so the H.264/fast-start re-encode path is live - the
browser-ready test clip is left untouched). All video checks report
readyState 4 with currentTime advancing (actual playback, not just markup).

## Ordered screenshots
| # | File | Shows |
|---|------|-------|
| 01 | 01-admin-owner-signed-in.png | Owner past login + forced password-change gate |
| 02 | 02-admin-gallery-index-start.png | Admin gallery index on a fresh instance (empty) |
| 03 | 03-admin-create-form-video-capable.png | Create form: media input accept lists images AND video types; no capture attribute |
| 04 | 04-admin-desktop-image-post-saved.png | Desktop image post (2 pngs) saved, tile in index |
| 05 | 05-admin-desktop-video-post-saved.png | Desktop video post (real 2 s clip) saved, video tile in index |
| 06 | 06-admin-rejected-unsupported-type.png | .exe rejected: "File type '.exe' is not allowed." |
| 07 | 07-admin-rejected-oversized-video.png | 11 MB .mp4 rejected: "File size must be between 1 byte and 10485760 bytes." |
| 08 | 08-admin-mixed-selection-normalized.png | Mixed image+video pick normalized in the strip preview (video not submitted); server-side mix rejection covered by integration tests |
| 09 | 09-public-gallery-desktop.png | Desktop /gallery: grid visible, 2/2 items, no horizontal overflow |
| 10 | 10-public-desktop-video-viewer-playing.png | Desktop viewer (restored modal) playing the uploaded video |
| 11 | 11-mobile-home-bottom-nav-gallery.png | Mobile home: Gallery entry in the six-slot bottom nav |
| 12 | 12-mobile-gallery-via-bottom-nav.png | Mobile /gallery reached by tapping the nav entry: grid 2/2, active tab, no overflow |
| 13 | 13-mobile-video-viewer-playing.png | Mobile viewer playing the desktop-uploaded video |
| 14 | 14-public-gallery-tablet-768.png | Tablet 768: grid visible, no overflow |
| 15 | 15-public-gallery-after-resize-cycle.png | Grid survives 1440 -> 390 -> 1440 resize cycle |
| 16 | 16-admin-mobile-create-form.png | Admin create form on a 390 px phone |
| 17 | 17-admin-mobile-video-picked-preview.png | Existing video picked via the file input: dark video preview card before submit |
| 18 | 18-admin-mobile-video-post-saved.png | Phone-uploaded video post saved, listed in admin index |
| 19 | 19-admin-mobile-image-post-saved.png | Phone image upload still works |
| 20 | 20-public-mobile-all-posts.png | Public mobile /gallery: all 4 posts (2 videos), no overflow |
| 21 | 21-public-mobile-uploaded-video-playing.png | Video uploaded FROM the phone plays on the public mobile page |

## Logs
- log-1-build.txt - solution build
- log-2-tests.txt - full suite results
- log-3-media.txt - generated test media (real ffmpeg H.264 clip, 11 MB oversized file, .exe)
- log-4-app.txt / log-6-app-tail.txt - fresh app instance
- log-5-journey.txt - ordered PASS lines of the journey
- journey-summary.json - machine-readable grid/video diagnostics per phase
