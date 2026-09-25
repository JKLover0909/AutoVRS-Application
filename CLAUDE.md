# CLAUDE.md

Guidance for Claude Code (and similar agents) working in this repository.

## What this repo is

**AutoVRS** — hệ thống kiểm tra PCB tự động bằng AI (Automatic Visual Recognition System). Monorepo gồm 4 phần độc lập:

```
App/           # Flutter frontend (Windows/iOS/Android/Linux/macOS) — xem ARCHITECTURE_ANALYSIS.md
BE-AutoVRS/    # Backend Python: AI Detection API (8082), PLC Gateway (8083), SICK Camera stream (8999)
CameraApp/     # SimpleCameraViewer.exe — công cụ xem camera độc lập (đã build sẵn, không phải build cache)
Test/5173/     # Ảnh mẫu PCB (.bmp) để test AI detection — giữ nguyên, không phải rác
```

Đọc `ARCHITECTURE_ANALYSIS.md` (root) và `BE-AutoVRS/README.md` trước khi sửa sâu — đã có tài liệu kiến trúc chi tiết sẵn.

## Đã sửa ngày 2026-09-25 — lưu ý quan trọng

`.gitignore` (3200+ dòng, có sẵn rule `**/build/` cho Flutter) **bị lưu sai encoding UTF-16LE** nên toàn bộ rule không hoạt động — khiến 217 file build cache của Flutter (`App/build/`, ~331MB) và cache Python (`__pycache__/`, 19 file) bị track nhầm vào git từ trước. Đã sửa lại `.gitignore` sang UTF-8 và untrack các file trên. **Khi sửa `.gitignore` sau này, đảm bảo lưu bằng UTF-8** (không dùng PowerShell `>`/`Set-Content` mặc định — chúng lưu UTF-16LE trên Windows PowerShell 5.1).

## Ràng buộc

- `CameraApp/*.exe`, `*.dll` là binary phân phối chủ đích (không phải build output lẫn vào) — không tự ý xóa/untrack.
- Backend cần môi trường conda + model AI (`.onnx`/`.pt`) thật, không chạy được trong môi trường agent — chỉ kiểm tra syntax.
- Nhiều README con (`BE-AutoVRS/README.md`, `PLC_GATEWAY_README.md`, `DEFECT_TYPES.md`...) — đọc README gần nhất với phần đang sửa thay vì chỉ đọc root.
