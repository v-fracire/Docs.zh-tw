<span data-ttu-id="2e902-101">執行身分識別 scaffolder:</span><span class="sxs-lookup"><span data-stu-id="2e902-101">Run the Identity scaffolder:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="2e902-102">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2e902-102">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="2e902-103">從**方案總管 中**，以滑鼠右鍵按一下專案 >**新增** > **新的 Scaffold 項目**。</span><span class="sxs-lookup"><span data-stu-id="2e902-103">From **Solution Explorer**, right-click on the project > **Add** > **New Scaffolded Item**.</span></span>
* <span data-ttu-id="2e902-104">從左窗格的**新增 Scaffold**對話方塊中，選取**識別** > **新增**。</span><span class="sxs-lookup"><span data-stu-id="2e902-104">From the left pane of the **Add Scaffold** dialog, select **Identity** > **ADD**.</span></span>
* <span data-ttu-id="2e902-105">在**新增身分識別** 對話方塊中，選取您想要的選項。</span><span class="sxs-lookup"><span data-stu-id="2e902-105">In the **ADD Identity** dialog, select the options you want.</span></span>
  * <span data-ttu-id="2e902-106">選取現有的版面配置頁面，或您配置的檔案就會覆寫不正確的標記。</span><span class="sxs-lookup"><span data-stu-id="2e902-106">Select your existing layout page, or your layout file will be overwritten with incorrect markup.</span></span> <span data-ttu-id="2e902-107">選取現有的 _Layout.cshtml 檔案時，它是**不**覆寫。</span><span class="sxs-lookup"><span data-stu-id="2e902-107">When an existing _Layout.cshtml file is selected, it is **not** overwritten.</span></span>

 <span data-ttu-id="2e902-108">例如`~/Pages/Shared/_Layout.cshtml`Razor 頁面`~/Views/Shared/_Layout.cshtml`MVC 專案</span><span class="sxs-lookup"><span data-stu-id="2e902-108">For example `~/Pages/Shared/_Layout.cshtml` for Razor Pages `~/Views/Shared/_Layout.cshtml` for MVC projects</span></span>
* <span data-ttu-id="2e902-109">若要使用現有的資料內容，請選取至少一個檔案，以覆寫。</span><span class="sxs-lookup"><span data-stu-id="2e902-109">To use your existing data context, select at least one file to override.</span></span> <span data-ttu-id="2e902-110">您必須選取至少一個檔案，以加入您的資料內容。</span><span class="sxs-lookup"><span data-stu-id="2e902-110">You must select at least one file to add your data context.</span></span>
  * <span data-ttu-id="2e902-111">選取您的資料內容類別。</span><span class="sxs-lookup"><span data-stu-id="2e902-111">Select your data context class.</span></span>
  * <span data-ttu-id="2e902-112">選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="2e902-112">Select **ADD**.</span></span>
* <span data-ttu-id="2e902-113">若要建立新的使用者內容，並可能是建立自訂的使用者身分識別：</span><span class="sxs-lookup"><span data-stu-id="2e902-113">To create a new user context and possibly create a custom user class for Identity:</span></span>
  * <span data-ttu-id="2e902-114">選取**+** 按鈕以建立新**資料內容類別**。</span><span class="sxs-lookup"><span data-stu-id="2e902-114">Select the **+** button to create a new **Data context class**.</span></span>
  * <span data-ttu-id="2e902-115">選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="2e902-115">Select **ADD**.</span></span>

<span data-ttu-id="2e902-116">注意： 如果您要建立新的使用者內容，您沒有選擇要覆寫的檔案。</span><span class="sxs-lookup"><span data-stu-id="2e902-116">Note: If you're creating a new user context, you don't have to select a file to override.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="2e902-117">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="2e902-117">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="2e902-118">如果先前未安裝 ASP.NET scaffolder，請立即安裝：</span><span class="sxs-lookup"><span data-stu-id="2e902-118">If you have not previously installed the ASP.NET scaffolder, install it now:</span></span>

```cli
dotnet tool install -g dotnet-aspnet-codegenerator
```

<span data-ttu-id="2e902-119">封裝將參考加入至[Microsoft.VisualStudio.Web.CodeGeneration.Design](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.CodeGeneration.Design/)至專案 (\*.csproj) 檔案。</span><span class="sxs-lookup"><span data-stu-id="2e902-119">Add a package reference to [Microsoft.VisualStudio.Web.CodeGeneration.Design](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.CodeGeneration.Design/) to the project (\*.csproj) file.</span></span> <span data-ttu-id="2e902-120">在專案目錄中，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="2e902-120">Run the following command in the project directory:</span></span>

```cli
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet restore
```

<span data-ttu-id="2e902-121">執行下列命令來列出識別 scaffolder 選項：</span><span class="sxs-lookup"><span data-stu-id="2e902-121">Run the following command to list the Identity scaffolder options:</span></span>

```cli
dotnet aspnet-codegenerator identity -h
```

<span data-ttu-id="2e902-122">在專案資料夾中，執行身分識別 scaffolder 與您想要的選項。</span><span class="sxs-lookup"><span data-stu-id="2e902-122">In the project folder, run the Identity scaffolder with the options you want.</span></span> <span data-ttu-id="2e902-123">例如，若要設定的預設 UI 身分識別和檔案的最小數目，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="2e902-123">For example, to setup identity with the default UI and the minimum number of files, run the following command.</span></span> <span data-ttu-id="2e902-124">使用正確的完整的名稱的 DB 內容：</span><span class="sxs-lookup"><span data-stu-id="2e902-124">Use the correct fully qualified name for your DB context:</span></span>

```cli
dotnet aspnet-codegenerator identity -dc MyWeb.Data.ApplicationDbContext --files Account.Register
```

-------------