---
title: Unreal Engine 5.5 issue with NuGet
author: HUANG Cheng
date: 2024-12-10 22:05:00 +0800
categories: [Tech, Unreal Engine]
tags: [NuGet]
---

### Troubleshooting NuGet Errors in Unreal Engine 5.5 on Windows 10

#### **Introduction**

When using Unreal Engine 5.5 on Windows 10, developers may encounter NuGet-related errors during project builds. These issues can arise due to missing packages, misconfigured package sources, or file access permissions. This blog post explores the common causes of NuGet errors and provides step-by-step solutions for resolving them.

---

#### **Root Causes**

1. **Read-Only Directory Issues**
   - Unreal Engine directories like `Engine/Source/Programs/AutomationTool` may be erroneously set to read-only, preventing package restoration.

2. **Missing NuGet Packages**
   - Specific NuGet packages (e.g., `System.Data.DataSetExtensions`) may not be available in the project directory, leading to build errors.

3. **Misconfigured NuGet Package Sources**
   - The NuGet package source might be missing or incorrectly configured, causing package restore failures.

4. **Outdated or Incomplete Visual Studio Installation**
   - Missing workloads or components, such as `.NET Framework development` or `C++ Game Development`, can lead to build failures.

5. **File Access and Permissions Issues**
   - Insufficient permissions to access required directories or files during the build process.

---

#### **Solutions**

**1. Resolve Read-Only Directory Issues**
   - Navigate to the directory:
     ```
     UE_5.5/Engine/Source/Programs/AutomationTool/Mutable/RunMutableCommandlet/obj/
     ```
   - Right-click the folder, select **Properties**, and uncheck **Read-only**.
   - Apply changes to all files and subfolders.

   If the issue persists:
   - Open a terminal with administrator privileges and reattempt the operation.
   - Ensure no external processes (e.g., antivirus software) are locking the directory.

---

**2. Install Missing NuGet Packages**
   - Identify the missing packages from the error log.
   - Navigate to the affected project directory:
     ```
     UE_5.5/Engine/Source/Programs/AutomationTool/Mutable/RunMutableCommandlet/
     ```
   - Use the following command to add the missing NuGet package:
     ```
     dotnet add package <PackageName> --version <VersionNumber>
     ```
     Example:
     ```
     dotnet add package System.Data.DataSetExtensions --version 4.5.0
     ```

---

**3. Update NuGet Package Sources**
   - Open Visual Studio and navigate to:
     ```
     Tools > NuGet Package Manager > Package Manager Settings
     ```
   - Under **Package Sources**, ensure `nuget.org` is listed:
     ```
     Name: nuget.org
     Source: https://api.nuget.org/v3/index.json
     ```
   - If missing, add this source and apply changes.
   - Rebuild the project to verify the fix.

---

**4. Reinstall Visual Studio Workloads**
   - Open the Visual Studio Installer.
   - Ensure the following workloads are installed:
     - **.NET Desktop Development**
     - **C++ Game Development**
     - **C++ Desktop Development**
   - Reinstall the workloads if necessary, and include all dependencies like Windows SDK.

---

**5. Address Permissions Issues**
   - Run Visual Studio as an administrator.
   - Ensure full read/write permissions for the project directory and its subfolders.

---

**6. Clean and Rebuild the Project**
   - In Visual Studio, select **Build > Clean Solution**.
   - Manually delete the `Intermediate` and `Saved` folders in the project directory.
   - Rebuild the project to apply changes.

---

#### **Best Practices**

1. Keep your Visual Studio and Unreal Engine installations up to date.
2. Regularly clean temporary project files (`Intermediate`, `Saved`) to prevent build conflicts.
3. Use a version control system to track changes in `.csproj` and `.json` files related to NuGet configurations.
4. Validate `.NET` and NuGet package dependencies when migrating projects to newer Unreal Engine versions.

---

#### **Conclusion**

NuGet errors in Unreal Engine 5.5 can disrupt the build process but are manageable with proper troubleshooting. By addressing directory permissions, ensuring package availability, and verifying Visual Studio configurations, developers can resolve these issues effectively.

If you encounter persistent NuGet errors, consider sharing your build logs or configuration details for more specific guidance. Happy coding!