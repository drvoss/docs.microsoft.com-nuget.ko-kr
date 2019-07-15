---
title: nuget.exe CLI를 사용하여 NuGet 패키지 관리
description: nuget.exe CLI를 사용하여 NuGet 패키지를 작업하기 위한 지침입니다.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: e60bca8fe2f80b044e466db2a100d6c6d167edb7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427378"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a><span data-ttu-id="0204b-103">nuget.exe CLI를 사용하여 패키지 관리</span><span class="sxs-lookup"><span data-stu-id="0204b-103">Manage packages using the nuget.exe CLI</span></span>

<span data-ttu-id="0204b-104">CLI 도구를 사용하면 프로젝트 및 솔루션에서 NuGet 패키지를 쉽게 업데이트하고 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-104">The CLI tool allows you to easily update and restore NuGet packages in projects and solutions.</span></span> <span data-ttu-id="0204b-105">이 도구는 Windows에서 모든 NuGet 기능을 제공하며 Mono로 실행 중일 경우 Mac 및 Linux에서 대부분의 기능도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-105">This tool provides all NuGet capabilities on Windows, and also provides most features on Mac and Linux when running under Mono.</span></span>

<span data-ttu-id="0204b-106">nuget.exe CLI는 .NET Framework 프로젝트 및 SDK 스타일이 아닌 프로젝트(예: .NET Standard 라이브러리를 대상으로 하는 프로젝트)에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-106">The nuget.exe CLI is for your .NET Framework project and non-SDK-style projects (for example, one that targets .NET Standard libraries).</span></span> <span data-ttu-id="0204b-107">`PackageReference`로 마이그레이션된 SDK 스타일이 아닌 프로젝트를 사용하는 경우 대신 dotnet CLI를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-107">If you are using a non-SDK-style project that has been migrated to `PackageReference`, use the dotnet CLI instead.</span></span> <span data-ttu-id="0204b-108">NuGet CLI에는 패키지 참조에 대한 [packages.config](../reference/packages-config.md) 파일이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-108">The NuGet CLI requires a [packages.config](../reference/packages-config.md) file for package references.</span></span>

> [!NOTE]
> <span data-ttu-id="0204b-109">대부분의 시나리오에서는 PackageReference에 `packages.config`를 사용하는 [SDK 스타일이 아닌 프로젝트를 마이그레이션](../reference/migrate-packages-config-to-package-reference.md)한 다음, `nuget.exe` CLI 대신 dotnet CLI를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-109">In most scenarios, we recommend [migrating non-SDK-style projects](../reference/migrate-packages-config-to-package-reference.md) that use `packages.config` to PackageReference, and then you can use the dotnet CLI instead of the `nuget.exe` CLI.</span></span> <span data-ttu-id="0204b-110">현재 C++ 및 ASP.NET 프로젝트에는 마이그레이션이 제공되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-110">Migration is not currently available for C++ and ASP.NET projects.</span></span>

<span data-ttu-id="0204b-111">이 문서에서는 가장 일반적인 몇 가지 nuget.exe CLI 명령에 대한 기본 사용법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-111">This article shows you basic usage for a few of the most common nuget.exe CLI commands.</span></span> <span data-ttu-id="0204b-112">이러한 명령의 대부분의 경우, CLI 도구는 프로젝트 파일이 명령에 지정되지 않는 한 현재 디렉터리에서 프로젝트 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-112">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command.</span></span> <span data-ttu-id="0204b-113">사용할 수 있는 명령 및 전체 목록은 [nuget.exe CLI 참조](../tools/nuget-exe-cli-reference.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0204b-113">For a complete list of commands and the arguments you may use, see the [nuget.exe CLI reference](../tools/nuget-exe-cli-reference.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0204b-114">전제 조건</span><span class="sxs-lookup"><span data-stu-id="0204b-114">Prerequisites</span></span>

- <span data-ttu-id="0204b-115">`nuget.exe` CLI를 설치하려면 [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe)에서 다운로드하고, 해당 `.exe` 파일을 적합한 폴더에 저장하고, 해당 폴더를 PATH 환경 변수에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-115">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="0204b-116">패키지 설치</span><span class="sxs-lookup"><span data-stu-id="0204b-116">Install a package</span></span>

<span data-ttu-id="0204b-117">[설치](../tools/cli-ref-install.md) 명령은 지정된 패키지 소스를 사용하여 현재 폴더를 기본값으로 프로젝트에 패키지를 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-117">The [install](../tools/cli-ref-install.md) command downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span> <span data-ttu-id="0204b-118">새 패키지를 프로젝트 루트 디렉터리의 *패키지* 폴더에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-118">Install new packages into the *packages* folder in your project root directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0204b-119">`install` 명령은 프로젝트 파일이나 *packages.config*을 수정하지 않습니다. 이러한 방식으로 패키지를 디스크에만 추가하지만 프로젝트의 종속성은 변경하지 않는다는 점에서 `restore`와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-119">The `install`command does not modify a project file or *packages.config*; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="0204b-120">종속성을 추가하려면 패키지 관리자 UI 또는 Visual Studio의 콘솔을 통해 패키지를 추가하거나 *packages.config*를 수정한 다음, `install` 또는 `restore` 중 하나를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-120">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify *packages.config* and then run either `install` or `restore`.</span></span>

1. <span data-ttu-id="0204b-121">명령줄을 열고 프로젝트 파일이 포함된 디렉터리로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-121">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="0204b-122">다음 명령을 사용하여 NuGet 패키지를 *패키지* 폴더에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-122">Use the following command to install a NuGet package to the *packages* folder.</span></span>

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    <span data-ttu-id="0204b-123">`Newtonsoft.json` 패키지를 *패키지* 폴더에 설치하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-123">To install the `Newtonsoft.json` package to the *packages* folder, use the following command:</span></span>

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

<span data-ttu-id="0204b-124">또는 다음 명령을 사용하여 기존 `packages.config` 파일을 통해 NuGet 패키지를 *패키지* 폴더에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-124">Alternatively, you can use the following command to install a NuGet package using an existing `packages.config` file to the *packages* folder.</span></span> <span data-ttu-id="0204b-125">이렇게 하면 패키지가 프로젝트 종속성에 추가되지 않고 로컬로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-125">This does not add the package to your project dependencies, but installs it locally.</span></span>

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="0204b-126">특정 버전의 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="0204b-126">Install a specific version of a package</span></span>

<span data-ttu-id="0204b-127">[설치](../tools/cli-ref-install.md) 명령을 사용할 때 버전이 지정되지 않은 경우 NuGet은 패키지의 최신 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-127">If the version is not specified when you use the [install](../tools/cli-ref-install.md) command, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="0204b-128">특정 버전의 Nuget 패키지를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-128">You can also install a specific version of a Nuget package:</span></span>

```cli
nuget install <packageID | configFilePath> -Version <version>
```

<span data-ttu-id="0204b-129">예를 들어 `Newtonsoft.json` 패키지의 버전 12.0.1을 추가하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-129">For example, to add version 12.0.1 of the `Newtonsoft.json` package, use this command:</span></span>

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

<span data-ttu-id="0204b-130">`install`의 제한 사항 및 동작에 대한 자세한 내용은 [패키지 설치](#install-a-package)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0204b-130">For more information on the limitations and behavior of `install`, see [Install a package](#install-a-package).</span></span>

## <a name="remove-a-package"></a><span data-ttu-id="0204b-131">패키지 제거</span><span class="sxs-lookup"><span data-stu-id="0204b-131">Remove a package</span></span>

<span data-ttu-id="0204b-132">하나 이상의 패키지를 삭제하려면 *패키지* 폴더에서 제거할 패키지를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-132">To delete one or more packages, delete the packages you want to remove from the *packages* folder.</span></span>

<span data-ttu-id="0204b-133">패키지 다시 설치하려면 `restore` 또는 `install` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-133">If you want to reinstall packages, use the `restore` or `install` command.</span></span>

## <a name="list-packages"></a><span data-ttu-id="0204b-134">패키지 나열</span><span class="sxs-lookup"><span data-stu-id="0204b-134">List packages</span></span>

<span data-ttu-id="0204b-135">[list](../tools/cli-ref-list.md) 명령을 사용하여 지정된 소스에서 패키지 목록을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-135">You can display a list of packages from a given source using the [list](../tools/cli-ref-list.md) command.</span></span> <span data-ttu-id="0204b-136">`-Source` 옵션을 사용하여 검색을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-136">Use the `-Source` option to restrict the search.</span></span>

```cli
nuget list -Source <source>
```

<span data-ttu-id="0204b-137">예를 들어 *패키지* 폴더에 패키지를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-137">For example, list packages in the *packages* folder.</span></span>

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

<span data-ttu-id="0204b-138">검색 용어를 사용하는 경우 패키지 이름, 태그 및 패키지 설명이 검색에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-138">If you use a search term, the search includes names of packages, tags, and package descriptions.</span></span>

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a><span data-ttu-id="0204b-139">개별 패키지 업데이트</span><span class="sxs-lookup"><span data-stu-id="0204b-139">Update an individual package</span></span>

<span data-ttu-id="0204b-140">패키지 버전을 지정하지 않는 한 `install` 명령을 사용할 때 NuGet은 패키지의 최신 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-140">NuGet installs the latest version of the package when you use the `install` command unless you specify the package version.</span></span>

## <a name="update-all-packages"></a><span data-ttu-id="0204b-141">모든 패키지 업데이트</span><span class="sxs-lookup"><span data-stu-id="0204b-141">Update all packages</span></span>

<span data-ttu-id="0204b-142">[업데이트](../tools/cli-ref-update.md) 명령을 사용하여 모든 패키지를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-142">Use the [update](../tools/cli-ref-update.md) command to update all packages.</span></span> <span data-ttu-id="0204b-143">프로젝트의 모든 패키지(`packages.config` 사용)를 사용 가능한 최신 버전으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-143">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="0204b-144">`update`를 실행하기 전에 `restore`를 실행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-144">It is recommended to run `restore` before running `update`.</span></span>

```cli
nuget update
```

## <a name="restore-packages"></a><span data-ttu-id="0204b-145">패키지 복원</span><span class="sxs-lookup"><span data-stu-id="0204b-145">Restore packages</span></span>

<span data-ttu-id="0204b-146">[복원](../tools/cli-ref-restore.md) 명령을 사용하면 *패키지* 폴더에서 누락된 모든 패키지를 다운로드하고 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-146">Use the [restore](../tools/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="0204b-147">`restore`는 디스크에만 패키지를 추가하지만 프로젝트의 종속성은 변경하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-147">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="0204b-148">프로젝트 종속성을 복원하려면 `packages.config`를 수정한 다음, `restore` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-148">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="0204b-149">`restore`를 사용하여 패키지를 복원하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0204b-149">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```