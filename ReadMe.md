# 🎛️ WinSettings (.NET 4.7.2 & 4.8 Edition / Signed)

[![NuGet version (BlueByte.WinSettings)](https://img.shields.io/nuget/v/BlueByte.WinSettings.svg?style=flat-square)](https://www.nuget.org/packages/BlueByte.WinSettings/)


## 🔥 What's New

🎯 **Targeted .NET Framework 4.7.2 and 4.8**  
📦 **Embedded key dependencies** for easier distribution  
🔐 **Signed assemblies** for strong-naming and GAC support

This fork builds upon the original work and focuses on compatibility with newer legacy .NET Framework projects.

---

## 🙏 Acknowledgement

All credit goes to the original author of this library.  
This fork simply **retargets the frameworks**, **signs the DLL**, and **packages dependencies**.

---

## 📚 Overview

**WinSettings** is a .NET class library that makes it super easy to save and retrieve app settings in Windows.

It includes 3 powerful settings classes:

- 📝 `IniSettings` – Stores settings in an INI file  
- 📄 `XmlSettings` – Stores settings in an XML file  
- 🧱 `RegistrySettings` – Stores settings in the Windows Registry  

You can even create your own custom storage backend! 🔧

Just derive from one of the built-in classes and define your public properties.  
Call `Load()` to read, and `Save()` to persist your settings.

Encryption and property exclusion is supported with simple attributes:
- 🔐 `[EncryptedSetting]`
- 🚫 `[ExcludedSetting]`

---

## Examples

```csharp
public class MySettings : RegistrySettings
{
    public string EmailHost { get; set; }
    public int EmailPort { get; set; }

    [EncryptedSetting]
    public string UserName { get; set; }

    [EncryptedSetting]
    public string Password { get; set; }

    [ExcludedSetting]
    public DateTime Created { get; set; }

    public MySettings(string companyName, string applicationName, RegistrySettingsType settingsType)
        : base(companyName, applicationName, settingsType, "Password123")
    {
        EmailHost = string.Empty;
        EmailPort = 0;
        UserName = string.Empty;
        Password = string.Empty;
        Created = DateTime.Now;
    }
}

public class MySettings : IniSettings
{
    public string EmailHost { get; set; }
    public int EmailPort { get; set; }

    [EncryptedSetting]
    public string UserName { get; set; }

    [EncryptedSetting]
    public string Password { get; set; }

    [ExcludedSetting]
    public DateTime Created { get; set; }

    public MySettings(string filename)
        : base(filename, "Password123")
    {
        EmailHost = string.Empty;
        EmailPort = 0;
        UserName = string.Empty;
        Password = string.Empty;
        Created = DateTime.Now;
    }
}


public class MySettings : XmlSettings
{
    public string EmailHost { get; set; }
    public int EmailPort { get; set; }

    [EncryptedSetting]
    public string UserName { get; set; }

    [EncryptedSetting]
    public string Password { get; set; }

    [ExcludedSetting]
    public DateTime Created { get; set; }

    public MySettings(string filename)
        : base(filename, "Password123")
    {
        EmailHost = string.Empty;
        EmailPort = 0;
        UserName = string.Empty;
        Password = string.Empty;
        Created = DateTime.Now;
    }
}
```
## ⚙️ Custom Settings Backend
You can create your own storage backend by inheriting from the base Settings class and overriding:

```OnSaveSettings(List<Setting> settings)```

```OnLoadSettings(List<Setting> settings)```

This allows complete flexibility to store settings in any custom format or storage location you want.
