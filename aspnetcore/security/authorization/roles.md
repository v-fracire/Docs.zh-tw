---
title: ASP.NET Core 中的角色為基礎的授權
author: rick-anderson
description: 了解如何將角色傳遞至 Authorize 屬性來限制 ASP.NET Core 控制器和動作的存取。
ms.author: riande
ms.date: 10/14/2016
uid: security/authorization/roles
ms.openlocfilehash: 59753b90d3196b0bc16d4963f45b995f5108bc8b
ms.sourcegitcommit: d99a8554c91f626cf5e466911cf504dcbff0e02e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/31/2018
ms.locfileid: "39356671"
---
# <a name="role-based-authorization-in-aspnet-core"></a>ASP.NET Core 中的角色為基礎的授權

<a name="security-authorization-role-based"></a>

建立身分識別時它可能屬於一個或多個角色。 比方說，Tracy 可能隸屬於系統管理員和使用者角色中，儘管 Scott 可能只屬於使用者角色。 建立及管理這些角色的方式取決於備份存放區的授權程序。 角色會公開給開發人員逐步[IsInRole](/dotnet/api/system.security.principal.genericprincipal.isinrole)方法[ClaimsPrincipal](/dotnet/api/system.security.claims.claimsprincipal)類別。

::: moniker range=">= aspnetcore-2.0"

> [!IMPORTANT]
> 本主題**不**適用於 Razor 頁面。 Razor Pages 支援[IPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter)並[IAsyncPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.iasyncpagefilter)。 如需詳細資訊，請參閱 [Razor 頁面的篩選條件方法](xref:razor-pages/filter)。

::: moniker-end

## <a name="adding-role-checks"></a>新增角色檢查

以角色為基礎的授權檢查是宣告式&mdash;開發人員將其內嵌控制器或動作的控制器內的程式碼內指定目前使用者必須是成員的存取要求的資源角色。

例如，下列程式碼的限制任何動作的存取權`AdministrationController`對使用者是誰的成員`Administrator`角色：

```csharp
[Authorize(Roles = "Administrator")]
public class AdministrationController : Controller
{
}
```

您可以為以逗號分隔清單指定多個角色：

```csharp
[Authorize(Roles = "HRManager,Finance")]
public class SalaryController : Controller
{
}
```

此控制器會只可存取的使用者是成員的`HRManager`角色或`Finance`角色。

如果您套用多個屬性，則必須指定; 的所有角色的成員存取的使用者。下列範例會要求使用者必須是兩者的成員`PowerUser`和`ControlPanelUser`角色。

```csharp
[Authorize(Roles = "PowerUser")]
[Authorize(Roles = "ControlPanelUser")]
public class ControlPanelController : Controller
{
}
```

您可以進一步限制存取，藉由套用在動作層級的其他角色授權屬性：

```csharp
[Authorize(Roles = "Administrator, PowerUser")]
public class ControlPanelController : Controller
{
    public ActionResult SetTime()
    {
    }

    [Authorize(Roles = "Administrator")]
    public ActionResult ShutDown()
    {
    }
}
```

在先前的程式碼片段成員的`Administrator`角色或`PowerUser`角色可以存取控制器並`SetTime`動作，但只有成員`Administrator`角色可以存取`ShutDown`動作。

您也可以鎖定的控制站，但允許匿名、 未經驗證存取個別的動作。

```csharp
[Authorize]
public class ControlPanelController : Controller
{
    public ActionResult SetTime()
    {
    }

    [AllowAnonymous]
    public ActionResult Login()
    {
    }
}
```

<a name="security-authorization-role-policy"></a>

## <a name="policy-based-role-checks"></a>原則為基礎的角色檢查

角色需求也可以使用新的原則語法，其中的開發人員會在啟動原則註冊授權服務組態的一部分來表示。 這通常發生在`ConfigureServices()`在您*Startup.cs*檔案。

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();

    services.AddAuthorization(options =>
    {
        options.AddPolicy("RequireAdministratorRole", policy => policy.RequireRole("Administrator"));
    });
}
```

原則會套用使用`Policy`屬性上的`AuthorizeAttribute`屬性：

```csharp
[Authorize(Policy = "RequireAdministratorRole")]
public IActionResult Shutdown()
{
    return View();
}
```

如果您想要指定多個允許的角色的需求，則您可以指定它們做為參數`RequireRole`方法：

```csharp
options.AddPolicy("ElevatedRights", policy =>
                  policy.RequireRole("Administrator", "PowerUser", "BackupAdministrator"));
```

此範例會授權使用者屬於`Administrator`，`PowerUser`或`BackupAdministrator`角色。
