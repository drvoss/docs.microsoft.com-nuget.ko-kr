---
title: 서명 된 패키지
description: NuGet 패키지 서명에 대 한 요구 사항입니다.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 7384e8b30cb2ec5fe53ea0fe485858bc1f7b3c43
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231255"
---
# <a name="signed-packages"></a>서명된 패키지

*NuGet 4.6.0 + 및 Visual Studio 2017 버전 15.6 이상*

NuGet 패키지에는 변조 된 콘텐츠에 대 한 보호를 제공 하는 디지털 서명이 포함 될 수 있습니다. 이 서명은 패키지의 실제 원본에도 신뢰성 증명을 추가 하는 x.509 인증서에서 생성 됩니다.

서명 된 패키지는 가장 강력한 종단 간 유효성 검사를 제공 합니다. NuGet 서명에는 다음과 같은 두 가지 유형이 있습니다.
- **작성자 서명**. 작성자 서명은 패키지가 전송 되는 리포지토리 또는 전송 방법에 관계 없이 패키지가 서명 된 이후 패키지가 수정 되지 않았음을 보장 합니다. 또한 작성자 서명 된 패키지는 서명 인증서를 미리 등록 해야 하기 때문에 nuget.org 게시 파이프라인에 추가 인증 메커니즘을 제공 합니다. 자세한 내용은 [인증서 등록](#signature-requirements-on-nugetorg)을 참조 하세요.
- **리포지토리 서명**. 리포지토리에 서명 되었는지 여부에 관계 없이 리포지토리의 **모든** 패키지에 대 한 무결성 보장을 제공 합니다 .이는 해당 패키지가 서명 된 원본 리포지토리와 다른 위치에서 가져오는 경우에도 마찬가지입니다.   

작성자 서명 된 패키지를 만드는 방법에 대 한 자세한 내용은 [패키지 서명](../create-packages/Sign-a-package.md) 및 [nuget sign 명령](../reference/cli-reference/cli-ref-sign.md)을 참조 하세요.

> [!Important]
> 패키지 서명은 현재 Windows에서 nuget.exe를 사용 하는 경우에만 지원 됩니다. [서명 된 패키지의 확인은 현재 Windows의 nuget.exe 또는 Visual Studio를 사용 하는 경우에만 지원 됩니다](../reference/cli-reference/cli-ref-verify.md) .

## <a name="certificate-requirements"></a>인증서 요구 사항

패키지 서명에는 코드 서명 인증서가 필요 합니다 .이 인증서는 `id-kp-codeSigning` 목적 [[RFC 5280 섹션 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]에 유효한 특수 한 인증서 형식입니다. 또한 인증서에는 RSA 공개 키 길이가 2048 비트 이상 이어야 합니다.

## <a name="timestamp-requirements"></a>타임 스탬프 요구 사항

서명 된 패키지에는 서명 인증서의 유효 기간을 초과 하 여 서명 유효성을 보장 하기 위해 RFC 3161 타임 스탬프가 포함 되어야 합니다. 타임 스탬프에 서명 하는 데 사용 되는 인증서는 `id-kp-timeStamping` 목적 [[RFC 5280 섹션 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]에 대해 유효 해야 합니다. 또한 인증서에는 RSA 공개 키 길이가 2048 비트 이상 이어야 합니다.

추가 기술 세부 정보는 [패키지 서명 기술 사양](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub)에서 찾을 수 있습니다.

## <a name="signature-requirements-on-nugetorg"></a>NuGet.org의 서명 요구 사항

nuget.org에는 서명 된 패키지를 수락 하기 위한 추가 요구 사항이 있습니다.

- 기본 서명은 작성자 서명 이어야 합니다.
- 기본 서명에 유효한 타임 스탬프가 하나 있어야 합니다.
- 작성자 서명 및 해당 타임 스탬프 시그니처의 x.509 인증서입니다.
  - RSA 공개 키 2048 비트 이상 이어야 합니다.
  - Nuget.org에 대 한 패키지 유효성 검사 시 현재 UTC 시간 당 유효 기간 내에 있어야 합니다.
  - Windows에서 기본적으로 신뢰 되는 신뢰할 수 있는 루트 인증 기관에 연결 해야 합니다. 자체 발급 된 인증서로 서명 된 패키지는 거부 됩니다.
  - 은 (는) 용도에 맞게 유효 해야 합니다. 
    - 작성자 서명 인증서가 코드 서명에 유효 해야 합니다.
    - 타임 스탬프 인증서는 타임 스탬프에 유효 해야 합니다.
  - 서명 시 해지 해서는 안 됩니다. (이는 제출 시 knowable 되지 않을 수 있으므로 nuget.org는 주기적으로 해지 상태를 재확인 합니다.)
  
  
## <a name="related-articles"></a>관련 문서

- [NuGet 패키지 서명](../create-packages/Sign-a-Package.md)
- [패키지 트러스트 영역 관리](../consume-packages/installing-signed-packages.md)
