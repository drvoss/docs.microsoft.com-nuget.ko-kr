---
title: NuGet CLI (명령줄 인터페이스) 참조
description: Nuget.exe CLI에 대 한 명령줄 참조 인덱스
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: 52aa2c533a8b67ae10455888a34a7ac9767fd0e3
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327470"
---
# <a name="nuget-cli-reference"></a>NuGet CLI 참조

Nuget CLI (명령줄 인터페이스) `nuget.exe`는 프로젝트 파일을 변경 하지 않고 패키지를 설치 하 고, 만들고, 게시 하 고, 관리 하는 nuget 기능의 전체 범위를 제공 합니다.

명령을 사용 하려면 명령 창이 나 bash 셸을 연 후 명령과 명령 및 적절 한 `nuget` 옵션 `nuget help pack` (예: pack 명령에 대 한 도움말을 보려면)을 차례로 실행 합니다.

이 설명서는 최신 버전의 NuGet CLI를 반영 합니다. 사용 중인 지정 된 버전에 대 한 정확한 세부 정보를 보려면 `nuget help` 원하는 명령에 대해를 실행 합니다.

`nuget.exe` CLI에서 기본 명령을 사용하는 방법에 대한 자세한 내용은 [nuget.exe CLI를 사용하여 패키지 설치 및 사용](../consume-packages/install-use-packages-nuget-cli.md)을 참조하세요.

## <a name="installing-nugetexe"></a>Nuget.exe 설치

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> Visual Studio의 패키지 관리자 콘솔에서 NuGet CLI를 사용할 수 있도록 설정 하려면 [콘솔에서 NUGET.EXE Cli 사용](../consume-packages/install-use-packages-powershell.md#use-the-nugetexe-cli-in-the-console)을 참조 하세요.

## <a name="availability"></a>가용성

정확한 정보는 [기능 가용성](../install-nuget-client-tools.md#feature-availability) 을 참조 하세요.

- 모든 명령은 Windows에서 사용할 수 있습니다.
- 모든 명령은, 및 `pack` `update`에 대해 지정 된 경우를 `restore`제외 하 고 Mono에서 실행 되는 nuget.exe와 작동 합니다.
- `pack` ,`restore`, ,`locals`및 명령은dotnetCLI를통해Mac및Linux에서도사용할수있습니다`push`. `delete`

## <a name="commands-and-applicability"></a>명령 및 적용 가능성

패키지 만들기, 패키지 사용 및/또는 패키지를 호스트에 게시 하는 데 사용할 수 있는 명령 및 적용 가능성:

| 일반 명령 | 적용 가능한 역할 | NuGet 버전 | Description |
| --- | --- | --- | --- |
| [pack](cli-reference/cli-ref-pack.md) | 생성 | 2.7+ | `.nuspec` 또는 프로젝트 파일에서 NuGet 패키지를 만듭니다. Mono에서 실행 하는 경우 프로젝트 파일에서 패키지를 만들 수 없습니다. |
| [push](cli-reference/cli-ref-push.md) | Publishing | 모두 | 패키지 원본에 패키지를 게시 합니다. |
| [config](cli-reference/cli-ref-config.md) | 모두 | 모두 | NuGet 구성 값을 불러오거나 설정할 수 있습니다. |
| [help or ?](cli-reference/cli-ref-help.md) | 모두 | 모두 | 명령에 대 한 도움말 정보나 도움말을 표시 합니다. |
| [locals](cli-reference/cli-ref-locals.md) | 사용 | 3.3+ | *전역 패키지*, *http 캐시*및 *임시* 폴더의 위치를 나열 하 고 해당 폴더의 내용을 지웁니다. |
| [복원(restore)](cli-reference/cli-ref-restore.md) | 사용 | 2.7+ | 사용 중인 패키지 관리 형식에서 참조 하는 모든 패키지를 복원 합니다. Mono에서 실행 하는 경우 PackageReference 형식을 사용 하 여 패키지를 복원 하는 것은 지원 되지 않습니다. |
| [setapikey](cli-reference/cli-ref-setapikey.md) | 게시, 소비 | 모두 | 패키지 원본에 액세스 하기 위한 키가 필요한 경우 지정 된 패키지 원본에 대 한 API 키를 저장 합니다. |
| [spec](cli-reference/cli-ref-spec.md) | 생성 | 모두 | Visual Studio 프로젝트에서 파일을 생성 하는 경우 토큰을 사용 하 여 파일을생성합니다.`.nuspec` |

| 보조 명령 | 적용 가능한 역할 | NuGet 버전 | Description |
| --- | --- | --- | --- |
| [add](cli-reference/cli-ref-add.md) | Publishing | 3.3+ | 계층적 레이아웃을 사용 하 여 HTTP가 아닌 패키지 원본에 패키지를 추가 합니다. HTTP 원본의 경우 *push*를 사용 합니다. |
| [delete](cli-reference/cli-ref-delete.md) | Publishing | 모두 | 패키지 원본에서 패키지를 제거 하거나 나열 취소 합니다. |
| [init](cli-reference/cli-ref-init.md) | 생성 | 3.3+ | 계층적 레이아웃을 사용 하 여 폴더의 패키지를 패키지 원본에 추가 합니다. |
| [install](cli-reference/cli-ref-install.md) | 사용 | 모두 | 패키지를 현재 프로젝트에 설치 하지만 프로젝트 또는 참조 파일을 수정 하지는 않습니다. |
| [list](cli-reference/cli-ref-list.md) | 사용량, 게시 | 모두 | 지정 된 원본의 패키지를 표시 합니다. |
| [mirror](cli-reference/cli-ref-mirror.md) | Publishing | 3\.2 이상에서 사용 되지 않음 | 패키지와 해당 종속성을 원본에서 대상 리포지토리로 미러링합니다. |
| [sources](cli-reference/cli-ref-sources.md) | 소비, 게시 | 모두 | 구성 파일에서 패키지 소스를 관리 합니다. |
| [update](cli-reference/cli-ref-update.md) | 사용 | 모두 | 프로젝트의 패키지를 사용 가능한 최신 버전으로 업데이트 합니다. Mono에서 실행 하는 경우 지원 되지 않습니다. |

여러 명령에서 다양 한 [환경 변수](cli-reference/cli-ref-environment-variables.md)를 사용 합니다.

적용 가능한 역할에의 한 NuGet CLI 명령:

| 역할 | 명령 |
| --- | --- |
| 사용 | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| 생성 | `config`, `help`, `init`, `pack`, `spec` |
| Publishing | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

예를 들어 패키지를 사용 하는 데만 관심이 있는 개발자는 NuGet 명령의 하위 집합만 이해 하면 됩니다.

> [!Note]
> 명령 옵션 이름은 대/소문자를 구분 하지 않습니다. 더 이상 사용 되지 않는 `NoPrompt` 옵션은 (로 `NonInteractive`바뀜) 및 `Verbose` (로 `Verbosity`바뀜)와 같은이 참조에 포함 되지 않습니다.
