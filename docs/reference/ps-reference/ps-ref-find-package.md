---
title: NuGet 찾기-패키지 PowerShell 참조
description: Visual Studio의 NuGet 패키지 관리자 콘솔에서 패키지 찾기 PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4118b5a38f80a2300b3945738315d56bda096f9a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384635"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (Visual Studio의 패키지 관리자 콘솔)

*버전 3.0 이상; 이 항목에서는 Windows의 Visual Studio에서 [패키지 관리자 콘솔](../../consume-packages/install-use-packages-powershell.md) 내의 명령을 설명 합니다. 일반 PowerShell 찾기-패키지 명령의 경우 [Powershell PackageManagement 참조](/powershell/module/packagemanagement/?view=powershell-6)를 참조 하세요.*

패키지 원본에서 지정 된 ID 또는 키워드를 사용 하 여 원격 패키지 집합을 가져옵니다.

## <a name="syntax"></a>구문

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --- | --- |
| Id &lt;키워드&gt; | 하다 패키지 소스를 검색할 때 사용할 키워드입니다. 패키지 ID가 키워드와 일치 하는 패키지만 반환 하려면-ExactMatch을 사용 합니다. 키워드를 지정 하지 않으면 `Find-Package`에서 다운로드 한 상위 20 개 패키지의 목록이 나-First로 지정 된 수를 반환 합니다. -Id는 선택 사항이 며 작동 하지 않습니다. |
| 소스 | 검색할 패키지 원본에 대 한 URL 또는 폴더 경로입니다. 로컬 폴더 경로는 절대 경로 이거나 현재 폴더에 대 한 상대 경로일 수 있습니다. 생략 하는 경우 `Find-Package`는 현재 선택 된 패키지 소스를 검색 합니다. |
| AllVersions | 최신 버전 뿐 아니라 각 패키지의 사용 가능한 모든 버전을 표시 합니다. |
| First | 목록의 처음부터 반환할 패키지 수입니다. 기본값은 20입니다. |
| 건너뛰기 | 표시 된 목록에서 첫 번째 &lt;int&gt; 패키지를 생략 합니다.  |
| IncludePrerelease | 결과에 시험판 패키지를 포함 합니다. |
| ExactMatch | 대/소문자를 구분 하는 패키지 ID로&gt; &lt;키워드를 사용 하도록 지정 합니다. |
| StartWith | 패키지 ID가&gt;&lt;키워드로 시작 하는 패키지를 반환 합니다. |

이러한 매개 변수는 파이프라인 입력 또는 와일드 카드 문자를 허용 하지 않습니다.

## <a name="common-parameters"></a>일반 매개 변수

`Find-Package`는 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable와 같은 [일반적인 PowerShell 매개 변수](https://go.microsoft.com/fwlink/?LinkID=113216)를 지원 합니다.

## <a name="examples"></a>예

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```
