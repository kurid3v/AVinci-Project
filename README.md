# AVinci - AI-Powered Literature Learning Platform

<div align="center">
  <h3>📚 Nền tảng học tập và sáng tạo được hỗ trợ bởi AI</h3>
  <p>Giúp giáo viên giao bài tập văn học và học sinh nhận phản hồi tức thì được hỗ trợ bởi Google Gemini AI</p>
</div>

---

## 📋 Mục đích dự án

AVinci là một nền tảng giáo dục được xây dựng để:
- **Giáo viên**: Tạo bài tập, quản lý lớp học, chấm điểm bài tiểu luận
- **Học sinh**: Nộp bài tập, nhận phản hồi chi tiết từ AI, theo dõi tiến độ học tập
- **Admin**: Quản lý hệ thống, người dùng, và giám sát toàn bộ hoạt động

---

## 🔄 Luồng hoạt động

### 1. **Xác thực & Đăng nhập**
```
Người dùng → Trang Đăng nhập/Đăng ký → Xác thực thông tin đăng nhập
→ Lưu session → Chuyển hướng đến Dashboard
```

- Hai role chính: **Giáo viên**, **Học sinh**, **Admin**
- Session được quản lý thông qua `SessionContext`

### 2. **Quản lý bài tập (Giáo viên)**
```
Giáo viên → Dashboard → Tạo bài tập mới → Gán lớp học → Lưu vào cơ sở dữ liệu
```

**Thông tin bài tập:**
- Tiêu đề, mô tả
- Loại bài: Tiểu luận, phân tích, đọc hiểu
- Tiêu chí chấm điểm (Criteria)
- Lớp học được gán (Classroom IDs)
- Thời hạn nộp bài

### 3. **Nộp bài & Chấm điểm (Học sinh)**
```
Học sinh → Xem bài tập → Nộp bài văn bản
→ AI Gemini phân tích → Nhận phản hồi chi tiết
→ Điểm số & nhận xét được lưu
```

**Quy trình chấm điểm:**
1. Học sinh viết tiểu luận
2. Gửi bài tập
3. AI Gemini phân tích theo tiêu chí được định nghĩa
4. Trả về:
   - Điểm số (0-100)
   - Phân tích từng tiêu chí
   - Nhận xét chi tiết
   - Gợi ý cải thiện

### 4. **Lịch sử & Theo dõi**
```
Học sinh → Xem lịch sử nộp bài → Xem chi tiết từng bài
→ Theo dõi điểm số theo thời gian
```

### 5. **Quản lý Lớp học**
```
Giáo viên → Tạo lớp học → Thêm học sinh
→ Gán bài tập cho lớp
```

---

## 📁 Cấu trúc dự án

```
AVinci/
├── app/                      # Next.js App Router
│   ├── (main)/              # Main layout cho authenticated users
│   │   ├── dashboard/       # Dashboard chính
│   │   ├── problems/        # Quản lý bài tập
│   │   ├── exams/          # Quản lý kỳ thi
│   │   ├── submissions/     # Xem bài nộp
│   │   ├── classrooms/      # Quản lý lớp học
│   │   ├── admin/           # Admin panel
│   │   └── profile/         # Hồ sơ người dùng
│   ├── api/                 # API Routes
│   │   ├── auth/           # Login, signup
│   │   ├── problems/       # CRUD bài tập
│   │   ├── submissions/    # CRUD bài nộp
│   │   ├── exams/          # CRUD kỳ thi
│   │   ├── gemini/         # Gọi Gemini AI
│   │   └── users/          # Quản lý người dùng
│   ├── login/              # Trang đăng nhập
│   ├── signup/             # Trang đăng ký
│   ├── layout.tsx          # Root layout
│   ├── page.tsx            # Landing page
│   └── actions.ts          # Server actions
├── components/              # React components
│   ├── icons/              # Icon SVG components
│   └── ...                 # UI components
├── context/                # React Context
│   ├── SessionContext.tsx  # Quản lý session
│   └── DataContext.tsx     # Quản lý dữ liệu global
├── lib/                    # Utility functions
│   ├── db.ts              # Database queries
│   ├── gemini.ts          # Gemini AI integration
│   ├── session.ts         # Session helpers
│   └── data.ts            # Data processing
├── data/                  # JSON data files
│   ├── users.json         # Dữ liệu người dùng
│   ├── problems.json      # Dữ liệu bài tập
│   ├── submissions.json   # Dữ liệu bài nộp
│   ├── exams.json         # Dữ liệu kỳ thi
│   └── classrooms.json    # Dữ liệu lớp học
├── styles/                # Global styles
├── types.ts               # TypeScript types
├── package.json           # Dependencies
├── tsconfig.json          # TypeScript config
├── tailwind.config.ts     # Tailwind CSS config
└── vite.config.ts         # Vite config
```

---

## 🚀 Hướng dẫn setup

### Yêu cầu hệ thống
- **Node.js**: v18 trở lên
- **npm** hoặc **yarn**
- **Gemini API Key**: Lấy từ [Google AI Studio](https://aistudio.google.com/app/apikey)

### 1. Clone repository
```bash
git clone https://github.com/kurid3v/AVinci-Project.git
cd AVinci-Project
```

### 2. Cài đặt dependencies
```bash
npm install
```

### 3. Cấu hình environment
Tạo file `.env.local` trong thư mục gốc:

```bash
GEMINI_API_KEY=your_gemini_api_key_here
NEXT_PUBLIC_API_URL=http://localhost:3000
```

**Lấy Gemini API Key:**
1. Truy cập [Google AI Studio](https://aistudio.google.com/app/apikey)
2. Nhấp "Create API Key"
3. Copy API key và dán vào `.env.local`

### 4. Chạy ứng dụng (Development)
```bash
npm run dev
```

Ứng dụng sẽ chạy tại `http://localhost:3000`

### 5. Build cho Production
```bash
npm run build
npm start
```

---

## 📊 Các loại người dùng & Quyền hạn

### 👨‍🏫 Giáo viên (Teacher)
- ✅ Tạo, sửa, xoá bài tập
- ✅ Tạo và quản lý lớp học
- ✅ Gán bài tập cho lớp
- ✅ Xem bài nộp của học sinh
- ✅ Xem phân tích AI về bài nộp
- ✅ Quản lý kỳ thi

### 👨‍🎓 Học sinh (Student)
- ✅ Xem danh sách bài tập
- ✅ Nộp bài tập
- ✅ Nhận phản hồi từ AI
- ✅ Xem lịch sử nộp bài
- ✅ Tham gia vào lớp học
- ✅ Theo dõi điểm số

### 👨‍💼 Admin
- ✅ Quản lý toàn bộ người dùng
- ✅ Xem tất cả bài tập và bài nộp
- ✅ Quản lý lớp học
- ✅ Xem báo cáo hệ thống
- ✅ Giả lập người dùng khác (Impersonation)

---

## 🧪 Dữ liệu test

Ứng dụng có sẵn dữ liệu test trong thư mục `/data`:

**Tài khoản test:**
- **Teacher**: `teacher` / `password123`
- **Student**: `student` / `password123`
- **Admin**: `admin` / `password123`

---

## 🛠️ Công nghệ sử dụng

| Công nghệ | Phiên bản | Mục đích |
|-----------|----------|---------|
| Next.js | 14.2.5 | Framework React & Server-side rendering |
| React | 18 | UI Library |
| TypeScript | 5 | Type safety |
| Tailwind CSS | 3.4.1 | Styling |
| Google Gemini API | 1.24.0 | AI-powered analysis & feedback |
| PostCSS | 8 | CSS processing |

---

## 🤖 Tích hợp Google Gemini AI

### Chức năng AI:

1. **Phân tích tiểu luận**
   - Kiểm tra chất lượng viết
   - Đánh giá cấu trúc bài luận
   - Phân tích ngữ pháp và từ vựng

2. **Chấm điểm tự động**
   - Dựa trên tiêu chí được định nghĩa
   - Tính toán điểm số (0-100)

3. **Phản hồi chi tiết**
   - Nhận xét theo từng tiêu chí
   - Gợi ý cải thiện cụ thể
   - Điểm mạnh và điểm yếu

### API endpoint:
```
POST /api/gemini
```

**Request body:**
```json
{
  "essay": "Nội dung bài luận...",
  "criteria": ["Cấu trúc", "Ngữ pháp", "Nội dung"],
  "problemType": "essay"
}
```

---

## 📝 Các API chính

### Authentication
- `POST /api/auth/login` - Đăng nhập
- `POST /api/auth/signup` - Đăng ký

### Problems (Bài tập)
- `GET /api/problems` - Lấy danh sách bài tập
- `POST /api/problems` - Tạo bài tập mới
- `GET /api/problems/[problemId]` - Lấy chi tiết bài tập
- `PUT /api/problems/[problemId]` - Cập nhật bài tập
- `DELETE /api/problems/[problemId]` - Xoá bài tập

### Submissions (Bài nộp)
- `GET /api/submissions` - Lấy danh sách bài nộp
- `POST /api/submissions` - Nộp bài mới
- `GET /api/submissions/[submissionId]` - Lấy chi tiết bài nộp
- `PUT /api/submissions/[submissionId]` - Cập nhật bài nộp

### Exams (Kỳ thi)
- `GET /api/exams` - Lấy danh sách kỳ thi
- `POST /api/exams` - Tạo kỳ thi mới

### Users
- `GET /api/users` - Lấy danh sách người dùng
- `PUT /api/users/[userId]` - Cập nhật thông tin người dùng

---

## 🔒 Security

- Session-based authentication
- Password hashing
- Server-side validation
- CSRF protection (via Next.js)
- Environment variables cho API keys

---

## 📱 Responsive Design

Ứng dụng tối ưu cho:
- 📱 Mobile devices
- 💻 Tablets
- 🖥️ Desktop

Sử dụng Tailwind CSS để đảm bảo responsive design

---

## 🐛 Troubleshooting

### Lỗi: "Gemini API key không hợp lệ"
- Kiểm tra `.env.local` có chứa `GEMINI_API_KEY` không
- Xác nhận API key từ [Google AI Studio](https://aistudio.google.com/app/apikey)

### Lỗi: "Port 3000 đang được sử dụng"
```bash
# Chạy ở port khác
npm run dev -- -p 3001
```

### Dữ liệu không cập nhập
- Clear browser cache (Ctrl+Shift+Delete)
- Restart development server
- Kiểm tra Network tab trong DevTools

---

## 📚 Tài liệu thêm

- [Next.js Documentation](https://nextjs.org/docs)
- [Google Gemini API](https://ai.google.dev/docs)
- [Tailwind CSS](https://tailwindcss.com/docs)
- [React Documentation](https://react.dev)

---

## 👥 Đội phát triển

- **Project**: AVinci
- **Repository**: [AVinci-Project](https://github.com/kurid3v/AVinci-Project)

---

## 📄 License

Dự án này được phát triển cho mục đích giáo dục.

---

## 🤝 Đóng góp

Nếu bạn muốn đóng góp cho dự án, vui lòng:

1. Fork repository
2. Tạo branch mới cho feature (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

**Đã cập nhập lần cuối**: December 1, 2025
