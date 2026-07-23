<<<<<<< HEAD
# Student Registration Web App — Authentication & Authorization Assignment

ASP.NET Core MVC application with role-based authentication and authorization using ASP.NET Core Identity.

**Author:** Arya Bardhan Singh Chauhan

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

## Setup Instructions

### Prerequisites
- Visual Studio 2022 or VS Code with C# Dev Kit
- .NET 8 SDK
- SQL Server Express / LocalDB

### Steps

1. **Clone the repository**
```bash
   git clone https://github.com/Aryabardhansinghchauhan/Aryabardhansinghchauhan-Studentregistrationwebapp.git
```

2. **Open the project** in Visual Studio or VS Code

3. **Connection string** (already configured in `appsettings.json`)

4. **Database** — nothing to do manually. Migrations run automatically at startup and seed roles, admin account, and sample courses.

5. **Run the application**
```bash
   dotnet run
```

### Default Admin Account
- **Email:** admin@studentapp.com
- **Password:** Admin@123

### Database Seeding
On first run, the app automatically:
- Creates "Admin" and "Student" roles
- Creates the Administrator account
- Seeds 5 sample courses (CS101, CS201, CS301, CS202, CS401)

## Authorization Attributes Summary

| Controller | Action | Role Required |
|---|---|---|
| Home | Index | Anonymous (all) |
| Courses | Index, Details | Anonymous (all) |
| Courses | Create, Edit, Delete | Admin |
| Students | Index | Admin |
| Profile | Index, Edit | Student |
| CourseRegistration | Register, Drop | Student |
| Account | Login, Register, AccessDenied | Anonymous |
| Account | Logout | Authenticated |

## Technologies
- ASP.NET Core 8 MVC
- Entity Framework Core 8
- ASP.NET Core Identity
- SQL Server (LocalDB)
- Bootstrap 5
=======
# Aryabardhansinghchauhan-Studentregistrationwebapp
>>>>>>> b998149bc0fe4fd9e80386d80cd7c47eeacfe77b
