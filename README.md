# RKix Storage Center

RKix Storage Center là dashboard quản lý dự án, repository và không gian lưu trữ tập trung với giao diện tối kiểu IBM Cloud/GitHub Enterprise/Vercel. Ứng dụng hiện dùng React + Vite ở frontend, Express ở backend và một JSON runtime store để mô phỏng dữ liệu.

## Tính năng chính

- Dashboard tổng quan dự án, dung lượng, backup và hoạt động gần đây.
- Project Storage Explorer với cây thư mục/file, tạo mới, đổi tên, di chuyển, xóa và dọn Trash.
- Quản lý project theo trạng thái `Active`, `Development`, `Testing`, `Maintenance`, `Archived`.
- Storage analytics theo danh mục, loại file và lịch sử tăng trưởng.
- Backup Center với thao tác backup/restore mô phỏng.
- Archive Center tạo ZIP archive mô phỏng cho nhiều project.
- Git integration mô phỏng clone/pull/push/branch và kiểm tra kết nối repository.
- Notification, audit log và Gemini-powered AI Assistant.

## Tech stack

| Lớp | Công nghệ |
| --- | --- |
| Frontend | React 19, TypeScript, Vite, Tailwind CSS v4, Recharts, lucide-react, motion |
| Backend | Node.js, Express, TypeScript, tsx, esbuild |
| AI | `@google/genai` qua endpoint `/api/ai/chat` |
| Runtime data | `data_store.json` sinh tự động khi chạy server |

## Cấu trúc thư mục

```text
.
├── .github/                    # CI workflow và PR template
├── docs/                       # Tài liệu phát triển, kiến trúc, API
├── src/
│   ├── components/             # Component UI có thể tái sử dụng
│   ├── App.tsx                 # UI shell và client-side flows chính
│   ├── index.css               # Tailwind theme và global styles
│   ├── main.tsx                # React bootstrap
│   └── types.ts                # TypeScript interfaces dùng chung
├── server.ts                   # Express API + Vite/static serving
├── vite.config.ts              # Vite config
├── package.json                # Scripts và dependencies
└── .env.example                # Mẫu biến môi trường
```

## Bắt đầu nhanh

```bash
npm ci
cp .env.example .env
npm run dev
```

Mở `http://localhost:3000` để sử dụng ứng dụng.

> AI Assistant chỉ hoạt động khi `GEMINI_API_KEY` trong `.env` là khóa hợp lệ.

## Scripts

| Lệnh | Mục đích |
| --- | --- |
| `npm run dev` | Chạy Express server với Vite middleware. |
| `npm run lint` | Type-check dự án bằng `tsc --noEmit`. |
| `npm run build` | Build frontend và bundle production server. |
| `npm run start` | Chạy bundle production từ `dist/server.cjs`. |
| `npm run clean` | Xóa output build. |

## Tài liệu dành cho developer

- [Development Guide](docs/DEVELOPMENT.md): cách cài đặt, chạy, kiểm tra và workflow local.
- [Architecture Overview](docs/ARCHITECTURE.md): thành phần hệ thống, luồng dữ liệu và hướng mở rộng.
- [API Reference](docs/API.md): danh sách endpoint backend hiện có.
- [Contributing](CONTRIBUTING.md): chuẩn đóng góp, checklist PR và quy ước commit.

## Roadmap đề xuất

### Phase 1

- Authentication và authorization theo role.
- Tách API route khỏi `server.ts`.
- Thêm validation request body.
- Thêm test tự động cho helper/API critical path.

### Phase 2

- PostgreSQL schema và migration.
- Object storage S3/MinIO cho file thật.
- Backup/restore thật thay vì mô phỏng.
- Search fuzzy và filter nâng cao.

### Phase 3

- GitHub/GitLab OAuth App integration.
- Notification realtime.
- AI Assistant có tool/action an toàn.
- Observability: structured logs, metrics và health checks.

## Ghi chú bảo mật

- Không commit `.env`, secret, `data_store.json`, `dist`, `node_modules` hoặc log.
- Endpoint AI phụ thuộc `GEMINI_API_KEY`; hãy cấu hình qua secret manager khi triển khai.
- JSON runtime store chỉ phù hợp demo/local, chưa phù hợp production multi-user.
