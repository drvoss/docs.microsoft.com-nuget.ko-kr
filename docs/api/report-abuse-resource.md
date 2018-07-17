---
title: 보고서 남용 URL 서식 파일을 NuGet API
description: 보고서 남용 URL 서식 파일에는 클라이언트를 신고 링크는 해당 UI에 표시할 수 있습니다.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 15cf0953391489d9dd9b5d609c3f4c8f66748f19
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31818469"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="971bc-103">보고서 남용 URL 서식 파일</span><span class="sxs-lookup"><span data-stu-id="971bc-103">Report abuse URL template</span></span>

<span data-ttu-id="971bc-104">특정 패키지에 대 한 신고 하기 위해 사용자가 사용할 수 있는 URL을 작성 하는 클라이언트에 대 한 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="971bc-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="971bc-105">패키지 소스에서 패키지 원본에 남용 보고서를 위임 하려면 모든 클라이언트 경험 (도 제 3 자)를 사용 하도록 설정 하려는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="971bc-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="971bc-106">패키지 콘텐츠를 가져오기 위해 사용 되는 리소스는는 `ReportAbuseUriTemplate` 에서 리소스를 찾을 [서비스 인덱스](service-index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="971bc-106">The resource used for fetching package content is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="971bc-107">버전 관리</span><span class="sxs-lookup"><span data-stu-id="971bc-107">Versioning</span></span>

<span data-ttu-id="971bc-108">다음 `@type` 값이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="971bc-108">The following `@type` values are used:</span></span>

<span data-ttu-id="971bc-109">@type 값</span><span class="sxs-lookup"><span data-stu-id="971bc-109">@type value</span></span>                       | <span data-ttu-id="971bc-110">노트</span><span class="sxs-lookup"><span data-stu-id="971bc-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="971bc-111">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="971bc-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="971bc-112">초기 릴리스</span><span class="sxs-lookup"><span data-stu-id="971bc-112">The initial release</span></span>
<span data-ttu-id="971bc-113">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="971bc-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="971bc-114">별칭 `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="971bc-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="971bc-115">URL 템플릿</span><span class="sxs-lookup"><span data-stu-id="971bc-115">URL template</span></span>

<span data-ttu-id="971bc-116">다음 API에 대 한 URL의 값은 고 `@id` 앞에서 언급 한 리소스 중 하나가 지정 된 연결 된 속성 `@type` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="971bc-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="971bc-117">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="971bc-117">HTTP methods</span></span>

<span data-ttu-id="971bc-118">웹 페이지를 지원 해야 하지는 않지만 클라이언트는 사용자를 위해 보고서 남용 URL로 요청을,는 `GET` 메서드를 쉽게 웹 브라우저에서 열 수를 클릭 한 URL을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="971bc-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="971bc-119">URL 구성</span><span class="sxs-lookup"><span data-stu-id="971bc-119">Construct the URL</span></span>

<span data-ttu-id="971bc-120">알려진된 패키지 ID 및 버전을 지정 된, 클라이언트 구현에서 URL을 구성 웹 인터페이스에 액세스 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="971bc-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="971bc-121">클라이언트 구현에서 모든 필요한 남용 보고서를 URL에 웹 브라우저를 열고 수 있도록 사용자에 게이 구성 된 URL (또는 클릭할 수 있는 링크) 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="971bc-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="971bc-122">남용 보고서 양식 구현 서버 구현에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="971bc-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="971bc-123">값은 `@id` 다음 자리 표시자 토큰 중 하나를 포함 하는 URL 문자열:</span><span class="sxs-lookup"><span data-stu-id="971bc-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="971bc-124">URL 자리 표시자</span><span class="sxs-lookup"><span data-stu-id="971bc-124">URL placeholders</span></span>

<span data-ttu-id="971bc-125">이름</span><span class="sxs-lookup"><span data-stu-id="971bc-125">Name</span></span>        | <span data-ttu-id="971bc-126">형식</span><span class="sxs-lookup"><span data-stu-id="971bc-126">Type</span></span>    | <span data-ttu-id="971bc-127">필수</span><span class="sxs-lookup"><span data-stu-id="971bc-127">Required</span></span> | <span data-ttu-id="971bc-128">노트</span><span class="sxs-lookup"><span data-stu-id="971bc-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="971bc-129">string</span><span class="sxs-lookup"><span data-stu-id="971bc-129">string</span></span>  | <span data-ttu-id="971bc-130">아니요</span><span class="sxs-lookup"><span data-stu-id="971bc-130">no</span></span>       | <span data-ttu-id="971bc-131">패키지 ID를 신고 하기에 대 한</span><span class="sxs-lookup"><span data-stu-id="971bc-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="971bc-132">string</span><span class="sxs-lookup"><span data-stu-id="971bc-132">string</span></span>  | <span data-ttu-id="971bc-133">아니요</span><span class="sxs-lookup"><span data-stu-id="971bc-133">no</span></span>       | <span data-ttu-id="971bc-134">패키지 버전에 대 한 신고를</span><span class="sxs-lookup"><span data-stu-id="971bc-134">The package version to report abuse for</span></span>

<span data-ttu-id="971bc-135">`{id}` 및 `{version}` 서버 구현에 의해 해석 하는 값은 대/소문자 구분 및 버전 정규화 되는 여부에 민감한 하지 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="971bc-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="971bc-136">예를 들어 nuget.org의 보고서 남용 서식 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="971bc-136">For example, nuget.org's report abuse template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

<span data-ttu-id="971bc-137">클라이언트 구현에서 NuGet.Versioning 4.3.0에 대 한 링크를 보고서 남용 양식으로 표시 하는 경우 것은 다음 URL을 생성 하 고 사용자에 게 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="971bc-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse