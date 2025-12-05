# CollabSphere---System-to-support-learning-using-project-based-learning-method

we propose CollabSphere — a system designed to support project management and real-time collaboration in Project-Based Learning environments. CollabSphere unifies tools such as video conferencing, group chat, task boards, whiteboards, and diagramming into one seamless workspace. This system aims to help students and lecturers streamline communication, improve project tracking, enhance teamwork, and create an engaging environment for hands-on learning and project development. CollabSphere also provides an evaluating system that recognizes project members’ contributions.


KEY FEATURES

🎓 Academic & Project Governance

- Syllabus Management – Staff imports files to automatically create and organize subjects and syllabuses.

- Project Approval Workflow – Lecturers submit projects; Head Departments review, approve, or deny them before assignment.

- Class Organization – Automated class creation and member assignment (Lecturers/Students) via file import.

- Milestone Planning – Lecturers define project objectives and milestones based on the subject syllabus.


🚀 Team Workspace & Execution

- Agile Task Board – Create sprints, manage cards, tasks, and subtasks within a unified team workspace.

- Checkpoint System – Leaders create checkpoints; members submit entries and mark completion to track progress.

- Resource Hub – Centralized management for sharing files, docs, and slides between lecturers and teams.

- Contribution Tracking – Monitor real-time progress and percentage of contribution for every team member.


🎨 Real-time Collaboration

- Interactive Whiteboard – Multi-user drawing and brainstorming tool with instant synchronization.

- Live Doc Editor – Collaborative text editor for writing reports and documents simultaneously.

- Video Meetings – High-quality video/audio calls with screen sharing and flexible join options.

- Persistent Chat – Real-time messaging system for both in-meeting and out-of-meeting team communication.


📊 Evaluation & Assessment

- Performance Grading – Lecturers evaluate and give feedback on team checkpoints and final project outcomes.

- Peer Review System – Team members evaluate and provide feedback on each other’s contributions and answers.

- Milestone Q&A – Lecturers create questions; students answer and receive specific feedback.


🤖 AI-Powered Assistance

- Smart Planning – AI generates project goals, timelines, and milestones based on syllabus data.

- Intelligent Advisor – AI chatbot assists with idea brainstorming, solution suggestions, and progress analysis.


🔔 Notifications

- Real-time Alerts – Instant updates for new resources, message receipts, and completed milestones.
  
- Email Integration – Automated emails for system reports, team assignments, and evaluation results.


  📁 Project Structure
collabsphere/
├── app/                                # Next.js App Router (Routing chính)
│   ├── (auth)/                         # Nhóm route xác thực (Login, Register)
│   │   ├── sign-in/[[...sign-in]]/     # Trang đăng nhập
│   │   ├── sign-up/[[...sign-up]]/     # Trang đăng ký
│   │   └── layout.tsx                  # Layout riêng cho Auth (không có sidebar)
│   │
│   ├── (root)/                         # Nhóm route chính (Đã đăng nhập)
│   │   ├── page.tsx                    # Landing page / Dashboard tổng
│   │   ├── admin/                      # Khu vực Admin (Quản lý User, System)
│   │   ├── staff/                      # Khu vực Staff (Import data, xếp lớp)
│   │   ├── projects/                   # Danh sách & Quản lý đề tài (Lecturer/Head)
│   │   ├── classes/                    # Danh sách lớp học
│   │   │
│   │   ├── workspace/[teamId]/         # KHÔNG GIAN LÀM VIỆC NHÓM (Core Feature)
│   │   │   ├── page.tsx                # Dashboard nhóm
│   │   │   ├── board/                  # Kanban Board (Quản lý Task)
│   │   │   ├── whiteboard/             # Vẽ Real-time (Socket.IO)
│   │   │   ├── meeting/                # Video Call (WebRTC/Jitsi)
│   │   │   └── settings/               # Cài đặt nhóm
│   │   │
│   │   └── layout.tsx                  # Layout chính (Sidebar, Header, Socket Provider)
│   │
│   ├── api/                            # API Routes (Webhooks, upload, proxy)
│   │   ├── upload/                     # Route xử lý upload file (Cloudinary/S3)
│   │   ├── socket/                     # Route khởi tạo Socket.IO (nếu dùng chung server)
│   │   └── ai/                         # Route gọi AWS Bedrock/OpenAI
│   │
│   ├── globals.css                     # Global styles (Tailwind directives)
│   └── layout.tsx                      # Root Layout
│
├── components/                         # Reusable UI components
│   ├── ui/                             # Shadcn UI / Base components (Button, Input...)
│   ├── shared/                         # Components dùng chung (Navbar, Sidebar, Loader)
│   ├── forms/                          # Các form phức tạp (CreateProject, SubmitTask)
│   │
│   ├── features/                       # MODULE HÓA CÁC CHỨC NĂNG LỚN (Quan trọng)
│   │   ├── workspace/                  # TaskCard, Column, FilterBar
│   │   ├── whiteboard/                 # Canvas, Toolbar, CursorOverlay
│   │   ├── meeting/                    # VideoGrid, ControlBar, ChatBox
│   │   ├── chat/                       # ChatBubble, MessageInput
│   │   └── evaluation/                 # RubricForm, PeerReviewModal
│   │
│   └── providers/                      # Context Providers
│       ├── theme-provider.tsx
│       ├── socket-provider.tsx         # Quản lý kết nối Real-time
│       └── modal-provider.tsx          # Quản lý các popup
│
├── lib/                                # Server-side utilities & Logic
│   ├── actions/                        # SERVER ACTIONS (Thay thế API controllers)
│   │   ├── auth.actions.ts             # Login logic
│   │   ├── user.actions.ts             # CRUD User
│   │   ├── project.actions.ts          # Tạo/Duyệt đề tài
│   │   ├── workspace.actions.ts        # Drag-drop task, update status
│   │   ├── ai.actions.ts               # Logic gọi AI gợi ý
│   │   └── stream.actions.ts           # Token cho Video Call
│   │
│   ├── database/                       # Kết nối Database (nếu code full Next.js)
│   │   ├── models/                     # Mongoose Models / Prisma Schema
│   │   └── mongoose.ts                 # DB connection
│   │
│   ├── validations/                    # Zod Schemas (Validate dữ liệu đầu vào)
│   │   ├── project.validation.ts
│   │   └── task.validation.ts
│   │
│   └── utils.ts                        # Helper functions (cn, formatDate...)
│
├── hooks/                              # Custom React hooks
│   ├── use-socket.ts                   # Hook lắng nghe sự kiện socket
│   ├── use-draw.ts                     # Logic vẽ bảng trắng
│   ├── use-webrtc.ts                   # Logic xử lý MediaStream
│   └── use-debounce.ts                 # Tối ưu performance search
│
├── types/                              # TypeScript definitions
│   ├── index.d.ts                      # Global types
│   └── socket.d.ts                     # Type cho sự kiện Socket
│
├── public/                             # Static assets
│   ├── images/
│   └── icons/
│
├── middleware.ts                       # Xử lý Protected Routes (Chặn chưa login)
├── next.config.js
└── tailwind.config.ts
