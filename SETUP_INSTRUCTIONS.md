# Student Registration Web App — Authentication & Authorization Assignment

ASP.NET Core MVC application with role-based authentication and authorization using ASP.NET Core Identity.

**Author:** Arya Bardhan Singh Chauhan
**GitHub:** https://github.com/Aryabardhansinghchauhan/Aryabardhansinghchauhan-Studentregistrationwebapp

---

## Features

### Authentication
- ASP.NET Core Identity (Individual Accounts)
- User Registration & Login
- New users auto-assigned "Student" role
- Logged-in user's email displayed in navbar
- Welcome message on successful login

### Authorization (Role-Based)
- **Admin**: CRUD courses, view all students
- **Student**: View courses, register for ONE course, view/edit own profile
- Students CANNOT: create/edit/delete courses, view other students, see student list
- URL-based access prevented via `[Authorize]` attributes

### Navigation Menu (Role-Based)
- **Anonymous**: Home, Courses, Register, Login
- **Student**: Home, Courses, Register for Course, My Profile, Logout
- **Admin**: Home, Courses, Students, Logout

### Security
- `[AllowAnonymous]` on Home and Course List
- `[Authorize(Roles = "Student")]` on Profile and Course Registration
- `[Authorize(Roles = "Admin")]` on Course CRUD and Students list
- Access Denied page for unauthorized access attempts

---

## Setup Instructions

### Prerequisites
- Visual Studio 2022 or VS Code with C# Dev Kit
- .NET 8 SDK
- SQL Server Express / LocalDB

### Steps

1. **Clone the repository**
```bash
   git clone https://github.com/Aryabardhansinghchauhan/Aryabardhansinghchauhan-Studentregistrationwebapp.git
   cd Aryabardhansinghchauhan-Studentregistrationwebapp
```

2. **Open the project** in Visual Studio (open `.csproj`) or VS Code (Open Folder)

3. **Connection string** (already configured in `appsettings.json`)

4. **Database** — nothing to do manually. Migrations run automatically at startup (`Database.Migrate()` in `DbInitializer`), which also seeds roles, the admin account, and sample courses.

5. **Run the application**
```bash
   dotnet restore
   dotnet build
   dotnet run
```
   The app launches at `https://localhost:7045` or `http://localhost:5045`.

### Default Admin Account
- **Email:** admin@studentapp.com
- **Password:** Admin@123

### Database Seeding (on first run)
- Creates "Admin" and "Student" roles
- Creates the Administrator account
- Seeds 5 sample courses (CS101, CS201, CS301, CS202, CS401)

---

## Testing Checklist

### Admin Flow
1. Login with `admin@studentapp.com` / `Admin@123`
2. Verify navbar: **Home, Courses, Students, Logout** + email shown
3. Add / Edit / Delete a course under **Courses**
4. View **Students** — list of all registered students

### Student Flow
1. Logout, click **Register**, create a new account
2. Verify welcome message and navbar: **Home, Courses, Register for Course, My Profile, Logout**
3. Register for a course → verify success message
4. Verify "Register for Course" disappears from nav once registered
5. View/edit **My Profile**
6. Logout

### Anonymous Flow
1. Verify navbar: **Home, Courses, Register, Login** only
2. View Courses without logging in
3. Try `/Profile`, `/Students`, `/Courses/Create` directly in the URL → should redirect to Login or show Access Denied

### Access Denied Test
1. Login as Student
2. Try `/Students` or `/Courses/Create` directly in URL → should show **Access Denied** page

---

## Screenshots Needed for Submission

1. Administrator Navigation
2. Student Navigation
3. Anonymous Navigation
4. Successful Login (welcome message + email in navbar)
5. Successful Course Registration
6. Access Denied page
7. Student Profile page
8. SQL Server Database (Identity + application tables via SQL Server Object Explorer / SSMS)

---

## Project Structure
StudentRegistrationWebApp/
├── Controllers/
│ ├── HomeController.cs — Home page (anonymous)
│ ├── AccountController.cs — Register, Login, Logout, AccessDenied
│ ├── CoursesController.cs — CRUD (Admin), View (all)
│ ├── StudentsController.cs — Student list (Admin only)
│ ├── ProfileController.cs — View/Edit own profile (Student only)
│ └── CourseRegistrationController.cs — Register/Drop course (Student only)
├── Data/
│ ├── ApplicationDbContext.cs — DbContext + Identity + relationships
│ └── DbInitializer.cs — Seeds roles, admin, courses on startup
├── Models/
│ ├── ApplicationUser.cs — extends IdentityUser (FullName, Phone, Address)
│ ├── Course.cs — Course entity
│ ├── CourseRegistration.cs — Student-Course 1:1 mapping
│ └── ErrorViewModel.cs
├── Views/
│ ├── Shared/_Layout.cshtml — Role-based navigation menu
│ ├── Home/Index.cshtml
│ ├── Account/ — Login, Register, AccessDenied
│ ├── Courses/ — Index, Details, Create, Edit, Delete
│ ├── Students/Index.cshtml
│ ├── Profile/ — Index, Edit
│ └── CourseRegistration/
├── Program.cs — Identity + DI + middleware + DB seed
├── appsettings.json — Connection string
└── StudentRegistrationWebApp.csproj

## Authorization Attributes Summary

| Controller | Action | Attribute | Who Can Access |
|---|---|---|---|
| Home | Index | `[AllowAnonymous]` | Everyone |
| Courses | Index, Details | `[AllowAnonymous]` | Everyone |
| Courses | Create, Edit, Delete | `[Authorize(Roles="Admin")]` | Admin only |
| Students | Index | `[Authorize(Roles="Admin")]` | Admin only |
| Profile | Index, Edit | `[Authorize(Roles="Student")]` | Student only |
| CourseRegistration | Register, Drop | `[Authorize(Roles="Student")]` | Student only |
| Account | Login, Register, AccessDenied | `[AllowAnonymous]` | Everyone |
| Account | Logout | `[Authorize]` | Authenticated users |

## Technologies
- ASP.NET Core 8 MVC
- Entity Framework Core 8
- ASP.NET Core Identity
- SQL Server (LocalDB)
- Bootstrap 5

## Troubleshooting

**"Cannot connect to LocalDB"** — Open Visual Studio Installer → Modify → ensure "SQL Server Express LocalDB" is installed.

**"No migrations found"** — Run `dotnet ef migrations add InitialCreate` then `dotnet ef database update`.

**"Access Denied on all pages after login"** — Check `AspNetRoles` table has "Admin" and "Student" rows; DbInitializer may not have seeded correctly.

**Port already in use** — Edit `Properties/launchSettings.json` and change the port numbers.