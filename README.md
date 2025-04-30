# Claude MCP Sticky Notes 📝

Proyek ini adalah contoh implementasi **Model Context Protocol (MCP)** menggunakan `FastMCP`, yang memungkinkan Claude AI mengakses dan memanipulasi catatan (notes) seperti sticky notes. Server MCP ini bisa dijalankan langsung atau diintegrasikan ke aplikasi Claude Desktop.

## 🚀 Fitur
- Tambahkan catatan (sticky notes)
- Baca semua catatan yang tersimpan
- Ambil catatan terbaru
- Dapatkan ringkasan catatan melalui prompt AI

## 📦 Requirements

- Python ≥ 3.10
- [uv](https://github.com/astral-sh/uv) sebagai pengganti pip
- [MCP SDK](https://github.com/modelcontextprotocol/python-sdk)
- Aplikasi Claude (desktop) — jika ingin menginstal server MCP ke Claude

## 🔧 Instalasi

### 1. Clone repositori ini

```bash
git clone https://github.com/farenhas/claude-mcp-notes.git
cd claude-mcp-notes
```

### 2. Tambahkan MCP SDK dan dependensi

```bash
uv add "mcp[cli]"
```

## ▶️ Menjalankan Server

### Opsi 1: Jalankan langsung (tanpa Claude Desktop)

```bash
uv run mcp run main.py
```

### Opsi 2: Jalankan dengan MCP Inspector (debug GUI)

```bash
uv run mcp dev main.py
```

### Opsi 3: Install ke Claude Desktop App

> Pastikan Claude Desktop App sudah terinstal dan terbuka.

```bash
uv run mcp install main.py
```

> Kamu akan melihat pesan seperti:
```
INFO     Successfully installed AI Sticky Notes in Claude app
```

## 📂 Struktur File

```
.
├── main.py         # Server MCP utama
├── notes.txt       # File penyimpanan catatan
└── README.md       # Dokumentasi
```

## 📌 Konsep Utama MCP yang Digunakan

- `@mcp.tool()` → Menyediakan fungsi yang bisa dipanggil oleh Claude (mis. `add_note`, `read_notes`)
- `@mcp.resource()` → Mengizinkan Claude mengakses resource tertentu (mis. catatan terakhir)
- `@mcp.prompt()` → Membuat prompt yang bisa disusun untuk dimasukkan ke dalam konteks Claude

## ✨ Contoh Fungsi

```python
@mcp.tool()
def add_note(message: str) -> str:
    ...
```

```python
@mcp.resource("notes://latest")
def get_latest_note() -> str:
    ...
```

```python
@mcp.prompt()
def note_summary_prompt() -> str:
    ...
```
