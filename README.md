# Latihan & Tugas Automasi CI/CD (Standarisasi Koding)

Repository ini mengimplementasikan standarisasi kode Python dan automasi pipeline CI menggunakan **Pre-commit**, **Ruff**, **Black**, **Pytest**, **GitHub Actions**, dan **Codecov**.

## 1. Menjalankan Lint, Format Check, dan Test Secara Lokal

Aktifkan virtual environment terlebih dahulu, kemudian jalankan perintah berikut:

```bash
# Menjalankan Linter (Ruff)
ruff check .

# Memeriksa Format Kode (Black)
black --check .

# Menjalankan Unit Test beserta Laporan Coverage
pytest --cov=. --cov-report=term-missing --cov-fail-under=80
```

## 2. Ringkasan Pipeline CI

Workflow CI (`.github/workflows/ci.yml`) berjalan otomatis pada setiap `push` dan `pull_request` ke branch `main` dengan tahapan:
1. **Checkout & Setup Python 3.11** dengan caching dependensi `pip`.
2. **Install Dependencies** dari `requirements.txt`.
3. **Linting (`ruff check .`)** untuk mendeteksi error sintaks, unused import/variable, dan pelanggaran PEP 8.
4. **Format Check (`black --check .`)** untuk memastikan konsistensi gaya penulisan kode.
5. **Unit Testing & Coverage Gate (`pytest --cov=. --cov-report=xml --cov-fail-under=80`)** untuk menjalankan pengujian otomatis.
6. **Upload Coverage ke Codecov** untuk pelacakan metrik coverage pada setiap Pull Request.

## 3. Threshold Coverage & Branch Protection

- **Minimum Coverage Threshold:** **80%** (`--cov-fail-under=80`). Pipeline akan gagal secara otomatis jika total coverage berada di bawah 80%.
- **Branch Protection (`main`):** Direct push ke `main` diblokir. Setiap perubahan wajib melalui Pull Request dengan status check `quality` berstatus **Passed**.
