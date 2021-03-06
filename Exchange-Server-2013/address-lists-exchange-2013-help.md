﻿---
title: '주소 목록: Exchange 2013 Help'
TOCTitle: 주소 목록
ms:assetid: 8ee2672a-3a45-4897-8cc0-fa23c374dbf9
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232119(v=EXCHG.150)
ms:contentKeyID: 50483658
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 주소 목록

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-12-02_

*주소 목록*은 받는 사람 및 기타 Active Directory 개체의 모음입니다. 각 주소 목록에는 하나 이상의 개체 유형(예: 사용자, 연락처, 그룹, 공용 폴더, 장소 및 장비 리소스)이 포함될 수 있습니다. 주소 목록을 사용하면 받는 사람 및 리소스를 구성하여 원하는 받는 사람 및 리소스를 보다 쉽게 찾을 수 있습니다. 주소 목록은 동적으로 업데이트됩니다. 따라서 조직에 받는 사람이 새로 추가되면 해당 주소 목록에 자동으로 추가됩니다.

다음 그림에 나오는 것처럼, Microsoft Outlook 같은 클라이언트 응용 프로그램에서는 Exchange가 제공하는 사용 가능한 주소 목록이 표시됩니다.

**Microsoft Office Outlook 2007에 표시되는 전체 주소 목록**

![Outlook 2007에 표시된 주소 목록](images/Bb232119.54d7729c-2e28-4863-8944-b0c37dabbbb3(EXCHG.150).gif "Outlook 2007에 표시된 주소 목록")

주소 목록은 Active Directory에 상주합니다. 따라서 네트워크에서 연결이 끊어진 모바일 사용자는 이러한 서버 쪽 주소 목록의 연결도 끊어집니다. 그러나 네트워크에서 연결이 끊어진 사용자를 위해 OAB(오프라인 주소록)를 만들 수 있습니다. 이러한 OAB는 사용자의 하드 디스크로 다운로드할 수 있습니다. 리소스를 절약하기 위해 OAB가 서버에 있는 실제 주소 목록에 포함된 정보의 하위 집합이 되는 경우도 많습니다. 자세한 내용은 [오프라인 주소록](offline-address-books-exchange-2013-help.md)를 참조하십시오.

**목차**

Default address lists

Custom address lists

Best practices for creating address lists

## 기본 주소 목록

클라이언트 응용 프로그램을 사용하여 받는 사람 정보를 찾으려는 경우 사용 가능한 주소 목록에서 선택할 수 있습니다. GAL(전체 주소 목록)을 비롯한 여러 주소 목록이 기본으로 만들어집니다. Exchange에는 다음 기본 주소 목록이 포함되어 있습니다. 이러한 주소 목록은 새 사용자, 연락처, 그룹 또는 장소가 조직에 추가되면 자동으로 채워집니다.

  - **모든 연락처**   이 주소 목록에는 조직에서 메일 사용이 가능한 모든 연락처가 포함됩니다. 메일 사용 가능 연락처는 외부 전자 메일 주소가 있는 받는 사람입니다. 조직의 모든 사용자가 메일 사용이 가능한 연락처 정보를 사용할 수 있게 하려면 해당 연락처를 GAL에 포함시켜야 합니다. 메일 연락처에 대한 자세한 내용은 [받는 사람](recipients-exchange-2013-help.md)를 참조하십시오.

  - **모든 메일 그룹**   이 주소 목록에는 조직의 메일 사용 가능 보안 그룹, 메일 그룹 및 동적 메일 그룹과 같은 메일 사용 가능 그룹이 포함되어 있습니다. 메일 사용 가능 그룹은 메시지 및 다른 정보를 대량으로 전자 메일로 보낼 수 있도록 만들어진 받는 사람의 목록입니다. 전자 메일 메시지가 메일 사용 가능 그룹으로 전송되면 해당 목록의 모든 구성원이 메시지의 복사본을 받습니다. 메일 사용이 가능한 그룹에 대한 자세한 내용은 [받는 사람](recipients-exchange-2013-help.md)를 참조하십시오.

  - **모든 장소**   이 주소 목록에는 조직에서 장소로 지정된 모든 리소스가 포함됩니다. 장소는 클라이언트 응용 프로그램에서 모임 요청을 전송하여 예약할 수 있는 조직의 리소스입니다. 장소에 연결된 사용자 계정은 사용할 수 없습니다. 리소스 사서함에 대한 자세한 내용은 [받는 사람](recipients-exchange-2013-help.md)를 참조하십시오.

  - **모든 사용자**   이 주소 목록에는 조직에서 메일 사용이 가능한 모든 사용자가 포함됩니다. 메일 사용이 가능한 사용자는 Exchange 조직 외부의 사용자를 나타냅니다. 메일이 사용 가능한 각 사용자에게는 외부 전자 메일 주소가 있습니다. 메일 사용 가능 사용자에게 전송되는 모든 메시지는 이 외부 전자 메일 주소로 라우팅됩니다. Active Directory 로그온 자격 증명을 갖고 있으며 리소스에 액세스할 수 있다는 점을 제외하면 메일 사용이 가능한 사용자는 메일 연락처와 유사합니다. 메일 사용이 가능한 사용자에 대한 자세한 내용은 [받는 사람](recipients-exchange-2013-help.md)를 참조하십시오.

  - **기본 전체 주소 목록**   이 주소 목록에는 조직의 메일 사용이 가능한 사용자, 연락처, 그룹 또는 장소가 모두 포함됩니다. Exchange는 설치 중에 다양한 기본 주소 목록을 만듭니다. 가장 친숙한 주소 목록은 GAL입니다. 기본적으로 GAL에는 Exchange 조직의 모든 받는 사람이 포함됩니다. 즉, Active Directory가 설치되어 있는 Exchange 포리스트의 모든 사서함 사용 가능 개체 또는 메일 사용 가능 개체가 GAL에 나열됩니다. 편리한 사용을 위해 GAL은 전자 메일 주소가 아닌 이름별로 구성됩니다. 자세한 내용은 [전체 주소 목록 만들기](create-a-global-address-list-exchange-2013-help.md)를 참조하십시오.

  - **공용 폴더**   이 주소 목록에는 조직의 모든 공용 폴더가 포함됩니다. 액세스 권한에 따라 폴더를 보거나 사용할 수 있습니다. 공용 폴더는 Exchange를 실행하는 컴퓨터에 저장됩니다. Exchange 2013의 공용 폴더에 대한 자세한 내용은 [공용 폴더](public-folders-exchange-2013-help.md)를 참조하십시오. Exchange Online의 공용 폴더에 대한 자세한 내용은 [Office 365 및 Exchange Online의 공용 폴더](https://technet.microsoft.com/ko-kr/library/jj200758\(v=exchg.150\))를 참조하십시오.

## 사용자 지정 주소 목록

Exchange 조직은 수천 명의 받는 사람을 포함할 수 있습니다. 모든 받는 사람을 기본 주소 목록에 포함시키면 목록이 너무 커질 수 있습니다. 이러한 문제를 피하려면 조직의 사용자들이 원하는 대상을 보다 쉽게 찾을 수 있도록 사용자 지정 주소 목록을 만들 수 있습니다.

예를 들어 두 개의 큰 부서와 하나의 Exchange 조직이 있는 회사가 있습니다. 이 회사의 Fourth Coffee 부서에서는 커피 원두를 수입하여 판매하고 Contoso, Ltd. 부서에서는 보험 정책을 처리합니다. 대부분의 일상 업무에서 Fourth Coffee의 직원들은 Contoso, Ltd.의 직원들과 의사 소통을 하지 않습니다. 따라서 직원들이 해당 부서에만 속하는 받는 사람을 보다 쉽게 찾을 수 있도록 Fourth Coffee와 Contoso, Ltd.에 대해 각각 하나씩 두 개의 새로운 사용자 지정 주소 목록을 만들 수 있습니다. 소속 부서의 받는 사람을 검색할 때 이러한 사용자 지정 주소 목록을 사용하면 직원들은 자신의 부서에 해당되는 주소 목록만 선택하면 됩니다. 그러나 받는 사람이 속한 부서를 잘 모르는 경우에는 두 부서의 받는 사람이 모두 들어 있는 GAL 내에서 검색할 수 있습니다.

계층적 주소 목록이라고 하는 주소 목록 하위 범주를 만들 수도 있습니다. 예를 들어, Manchester의 모든 받는 사람을 포함하는 주소 목록을 하나 만들고 Stuttgart의 모든 받는 사람이 포함되는 다른 주소 목록을 하나 만들 수 있습니다.

## 주소 목록 작성을 위한 유용한 정보

주소 목록은 사용자를 위한 유용한 도구이지만 주소 목록을 잘못 계획하면 혼란을 가져올 수 있습니다. 사용자에게 실용적인 주소 목록을 만들려면 다음 정보를 고려하십시오.

  - 사용자가 받는 사람을 검색할 목록을 정확히 모를 정도로 너무 많은 주소 목록을 만들지 않도록 합니다.

  - 주소 목록을 통해 사용자가 GAL에서 주소를 더욱 쉽게 찾을 수 있어야 합니다.

  - 사용자가 주소 목록을 가볍게 살펴 봤을 때 목록에 포함되어 있는 받는 사람 유형을 즉시 알 수 있도록 주소 목록의 이름을 지정합니다. 주소 목록의 이름을 지정하기 어려우면 적은 수의 목록을 만들고 사용자에게 GAL을 사용하여 조직의 모든 사람을 찾을 수 있다는 사실을 알려줍니다.
    

    > [!NOTE]
    > Exchange Online에서는 기본적으로 주소 목록 역할이 어떤 역할 그룹에도 할당되지 않습니다. 주소 목록 역할이 필요한 cmdlet을 사용하려면 역할 그룹에 이 역할을 추가해야 합니다. 자세한 내용은 <A href="manage-role-groups-exchange-2013-help.md">역할 그룹 관리</A> 항목의 "역할 그룹에 역할 추가" 섹션을 참조하세요.



Exchange 2013에서 주소 목록을 만드는 방법에 대한 자세한 내용은 [주소 목록 만들기](create-an-address-list-exchange-2013-help.md)를 참조하십시오. Exchange Online에서 주소 목록을 만드는 방법에 대한 자세한 내용은 [Exchange Online에서 주소 목록 관리](https://technet.microsoft.com/ko-kr/library/jj983798\(v=exchg.150\))를 참조하십시오.

