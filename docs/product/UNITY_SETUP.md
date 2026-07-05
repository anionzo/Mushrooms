# Cài Unity 6 LTS trên Windows 11 (cho dự án desktop idle)

Hướng dẫn cho stack trong `DESKTOP_IDLE_SIM_ARCHITECTURE.md`: **Unity 6 LTS**, **URP 2D**, **Windows standalone**.

---

## Cách nhanh nhất (khuyến nghị)

### Bước 1 — Unity Hub

1. Tải **Unity Hub**: https://unity.com/download  
   Hoặc terminal (PowerShell **Run as Administrator**):

```powershell
winget install --id Unity.UnityHub -e --accept-package-agreements --accept-source-agreements
```

2. Mở **Unity Hub** → đăng nhập tài khoản Unity (miễn phí Personal nếu doanh thu/doanh nghiệp dưới ngưỡng license).

### Bước 2 — Cài Unity Editor 6 LTS

Trong Hub → **Installs** → **Install Editor** → chọn **Unity 6** (dòng **6000.x LTS** khi có).

**Modules bắt buộc tick thêm:**

| Module | Vì sao |
| --- | --- |
| **Microsoft Visual Studio Community** (hoặc đã có VS 2022) | Debug C# |
| **Windows Build Support (IL2CPP)** | Build .exe Windows thương mại |
| **Documentation** (tùy chọn) | Offline docs |

**Modules nên có:**

- **Windows Build Support (Mono)** — build nhanh khi dev  
- **WebGL** — chỉ nếu sau này cần demo browser (không bắt buộc desktop)

**Không cần** Android/iOS trừ khi bạn mở rộng mobile companion sau.

### Bước 3 — Tạo project khớp kiến trúc

Hub → **Projects** → **New project**:

- Template: **2D (URP)** hoặc **2D** rồi chuyển sang URP trong Project Settings  
- Unity version: **6000.x LTS**  
- Tên ví dụ: `MushroomDesktop`  
- Vị trí: ví dụ `E:\CODE\Game\MushroomDesktop` (repo game tách khỏi harness `Mushrooms` hoặc monorepo tùy bạn)

Sau khi tạo, trong **Package Manager** cài/kiểm tra:

- **Universal RP**  
- **Input System** (khuyến nghị thay Input Manager cũ)  
- **Addressables**  
- **Localization** (khi tới milestone i18n)  
- **Test Framework** (cho EditMode/PlayMode)

### Bước 4 — Visual Studio / Rider

- **Visual Studio 2022 Community** + workload **Game development with Unity**  
  Hoặc `winget install Microsoft.VisualStudio.2022.Community` rồi thêm workload trong Installer.  
- Hoặc **JetBrains Rider** (`winget install JetBrains.Rider`).

Unity Hub → **Preferences** → **External Tools** → chọn editor bạn dùng, bật **Generate .csproj**.

---

## Cài Editor bằng winget (không qua Hub UI)

Có gói **Unity 6000** trên winget (phiên bản cụ thể thay đổi theo winget):

```powershell
winget install --id Unity.Unity.6000 -e --accept-package-agreements --accept-source-agreements
```

**Lưu ý:** Gói winget thường chỉ cài editor; **module IL2CPP / docs** có thể vẫn cần thêm qua **Unity Hub** → Installs → ⚙ → **Add modules**.

---

## Unity Hub CLI (tự động hóa / CI)

Sau khi có Hub, có thể cài phiên bản từ dòng lệnh (đường dẫn mặc định):

```powershell
& "${env:ProgramFiles}\Unity Hub\Unity Hub.exe" -- --headless help
```

Ví dụ cài editor (thay `6000.0.XXf1` bằng version Hub hiển thị):

```powershell
& "${env:ProgramFiles}\Unity Hub\Unity Hub.exe" -- --headless install `
  --version 6000.0.52f1 `
  --module windows-il2cpp `
  --module windows-mono `
  --module documentation
```

Danh sách module: xem [Unity Hub CLI](https://docs.unity3d.com/hub/manual/HubCLI.html).

---

## Kiểm tra sau khi cài

```powershell
# Hub
Test-Path "${env:ProgramFiles}\Unity Hub\Unity Hub.exe"

# Editor (đường dẫn thay theo version)
Get-ChildItem "C:\Program Files\Unity\Hub\Editor" -ErrorAction SilentlyContinue
```

Trong Unity: **Help → About Unity** → đúng **6000.x** và template **URP 2D** hoạt động.

---

## Agent / Codex có “cài hộ” được không?

| Việc | Agent có thể |
| --- | --- |
| Viết doc, script, checklist | Có |
| Chạy `winget install Unity.UnityHub` | Có **nếu** terminal có quyền admin, winget hoạt động, bạn chấp nhận license |
| Tải vài GB Unity Editor | Có thể **lâu** (timeout, mạng, UAC) |
| Đăng nhập Unity account / kích hoạt license | **Bạn** phải làm trong Hub (lần đầu) |
| Tick module IL2CPP trong UI | Thường **bạn** hoặc Hub CLI với đúng `--module` |

---

## Liên kết repo harness với project Unity

1. Giữ `E:\CODE\Game\Mushrooms` làm **docs/harness** (kiến trúc, stories).  
2. Tạo `E:\CODE\Game\MushroomDesktop` làm **Unity project** theo folder structure trong architecture doc.  
3. Ghi decision: `docs/decisions/` — “Unity 6 LTS + repo path”.  
4. (Tùy chọn) Submodule hoặc copy `docs/product/DESKTOP_IDLE_SIM_ARCHITECTURE.md` sang `MushroomDesktop/Docs/`.

---

## Sự cố thường gặp

- **Hub không mở:** Cài lại Hub; tắt proxy VPN; chạy Hub as admin một lần.  
- **Thiếu IL2CPP khi build:** Hub → Editor → Add modules → Windows Build Support (IL2CPP).  
- **License:** Personal → Hub → Settings → License management.  
- **Dung lượng:** Editor + 1 platform ~ **5–10 GB**; đủ SSD trống trước khi cài.