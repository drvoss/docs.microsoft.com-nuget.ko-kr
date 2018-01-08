---
title: "NuGet CLI 사양 명령을 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 85611449-87e6-489b-8c6c-fe1d7be76c13
description: "Nuget.exe 사양 명령에 대 한 참조"
keywords: "nuget 사양 참조, 사양 명령"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c32b23e66c8eb4db1c8fa6dc615589219c00239f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="spec-command-nuget-cli"></a>명령 (NuGet CLI) 사양

**적용 대상:** 패키지 만들기가 &bullet; **지원 되는 버전:** 모든

생성 된 `.nuspec` 새 패키지에 대 한 파일입니다. 프로젝트 파일을 같은 폴더에서 실행 되는 경우 (`.csproj`, `.vbproj`, `.fsproj`), `spec` 만듭니다는 토큰화 된 `.nuspec` 파일입니다. 자세한 내용은 참조 하십시오. [패키지를 만드는](../create-packages/creating-a-package.md)합니다.

## <a name="usage"></a>용도

```
nuget spec [<packageID>] [options]
```

여기서 `<packageID>` 에 저장 하는 선택적 패키지 식별자는 `.nuspec` 파일입니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| AssemblyPath | 메타 데이터에 사용할 어셈블리의 경로를 지정 합니다. |
| 강제 | 모든 기존 덮어씁니다 `.nuspec` 파일입니다. |
| ForceEnglishOutput | *(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| 비 대화형 | 사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *세부 (2.5 이상)*합니다. |

또한 참조 [환경 변수](cli-ref-environment-variables.md)

## <a name="examples"></a>예제

```
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```