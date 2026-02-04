# windows-regisry
#windows registry complete guid from basic to advance

What is the Windows Registry?

The Windows Registry is a centralized hierarchical database used by Windows to store configuration settings and options for the operating system, hardware, users, and applications. Instead of every program keeping its settings in random files, Windows keeps most critical settings in one structured place called the Registry. Whenever Windows starts, a user logs in, a device is plugged in, or an application runs, Windows reads from and writes to the Registry to know how it should behave.

In simple words:
👉 The Registry is Windows’ memory of how everything should work.


e Windows Registry is divided into five main logical sections called hives.


---

### **HKEY_LOCAL_MACHINE (HKLM)**

HKEY_LOCAL_MACHINE contains configuration data that applies to the **entire computer**, regardless of which user is logged in. This hive controls how Windows itself behaves: system startup, device drivers, services, installed software, security settings, and hardware-related configurations. When Windows boots, a large portion of HKLM is loaded into memory because the operating system depends on it to function correctly. Since changes here affect every user, Windows usually requires **administrator privileges** to modify HKLM. For example, when a program is installed “for all users,” its settings are written under `HKLM\Software`. Similarly, all Windows services and drivers are defined under `HKLM\SYSTEM\CurrentControlSet\Services`. From a security perspective, HKLM is very powerful: malware that gains admin access often modifies this hive to achieve system-wide persistence or to load malicious drivers. In simple terms, HKLM is the **core system brain** of Windows.

---

### **HKEY_CURRENT_USER (HKCU)**

HKEY_CURRENT_USER stores configuration settings for the **currently logged-in user only**. Everything related to a user’s personal environment—desktop appearance, Explorer behavior, application preferences, keyboard and mouse settings—lives here. This hive is loaded when the user logs in and unloaded when they log out, which means it is dynamic and user-specific. Programs commonly write their per-user settings under `HKCU\Software`, allowing different users on the same machine to have different configurations. Unlike HKLM, most changes to HKCU do **not** require administrator privileges, which makes it a popular location for both legitimate applications and user-level malware. For example, startup programs that run only for one user are often placed in `HKCU\Software\Microsoft\Windows\CurrentVersion\Run`. Conceptually, HKCU represents the **preferences, habits, and environment of one user** on the system.

---

### **HKEY_CLASSES_ROOT (HKCR)**

HKEY_CLASSES_ROOT defines how Windows handles **file types, protocols, and COM objects**. When you double-click a file, right-click to see a context menu, or launch an application through a file extension, Windows consults HKCR to decide what action to take. This hive tells Windows which program opens `.txt`, `.exe`, `.pdf`, and other file types, and it also stores information about registered COM and ActiveX components. Internally, HKCR is not an independent hive; it is a **merged view** of `HKLM\Software\Classes` (system-wide associations) and `HKCU\Software\Classes` (user-specific overrides). This means a user can override system defaults without changing HKLM. Because HKCR controls execution behavior, attackers sometimes abuse it to hijack file associations or COM objects to run malicious code. In essence, HKCR is the **decision-maker that controls what happens when you interact with files and objects in Windows**.

---

### **HKEY_USERS (HKU)**

HKEY_USERS contains the registry data for **all user accounts** that exist on the system, including those that are not currently logged in. Each user is represented by a long identifier called a **Security Identifier (SID)**, and under each SID is that user’s registry hive. When a user logs in, Windows maps that user’s SID from HKU to HKCU, which means `HKCU` is simply a shortcut to the relevant SID inside HKU. This hive also includes a `.DEFAULT` key, which defines default settings used before any user logs in or when creating new user profiles. HKU is particularly important for administrators and forensic analysts because it allows inspection or modification of settings for multiple users from one place. From a security standpoint, attackers with sufficient privileges may modify other users’ registry data here to persist across accounts. Simply put, HKU is the **container that stores registry data for every user on the machine**.

---

### **HKEY_CURRENT_CONFIG (HKCC)**

HKEY_CURRENT_CONFIG stores information about the **current hardware configuration** that Windows is using at that moment. This includes settings related to display devices, printers, and other hardware-dependent configurations. Unlike other hives, HKCC is dynamic and reflects the active hardware profile rather than being a permanent storage location. Internally, it is derived from data in `HKLM\SYSTEM`, specifically from the currently selected hardware profile. If hardware changes or Windows boots with a different profile, the contents of HKCC can change accordingly. This hive is mostly used by Windows and device drivers rather than by applications or users, and it is rarely targeted by malware. Conceptually, HKCC represents the **hardware context Windows is currently operating in**.

---



* **HKLM** defines how the *computer* works
* **HKCU** defines how the *current user* experiences that computer
* **HKCR** defines how Windows *reacts to files and objects*
* **HKU** stores *all users’ data* in one place
* **HKCC** reflects the *active hardware setup*


