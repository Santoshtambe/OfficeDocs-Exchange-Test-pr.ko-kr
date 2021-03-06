﻿---
title: '공용 폴더를 배포할 때의 고려 사항: Exchange 2013 Help'
TOCTitle: 공용 폴더를 배포할 때의 고려 사항
ms:assetid: 2e416eed-b88f-45db-a482-1232fd2610fa
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn957481(v=EXCHG.150)
ms:contentKeyID: 65012487
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 공용 폴더를 배포할 때의 고려 사항

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-07-12_

Exchange 2013 공용 폴더를 사용 하 여 다양 한 이점이 제공 되지만, 조직에서이 구현 하기 전에 고려 해야할 사항 있습니다.

## 공용 폴더에 대 한 배포 고려 사항

이 문서는 많은 수의 공용 폴더를 계획 하는 경우에 특히 조직 전체에서 공용 폴더를 배포 하기 전에 고려 해야할 요소를 포함 합니다. 이제 Exchange 2013 최대 1, 000만 개의 공용 폴더를 지원합니다.

  - 공용 폴더에 작업 폴더의 위치 하는 공용 폴더 사서함에 배치 되는 부하에 직접 영향을 줍니다. 예: 높은 대기 시간 또는 공용 폴더에 액세스할 수 없으면 클라이언트 연결 문제를 방지 하려면 다음을 수행 하는 것이 좋습니다.
    
      - 사서함 크기 제한의 50%를 초과 하는 공용 폴더 사서함을 사용 하지 마십시오. 이 문제가 발생 하는 경우에 새 공용 폴더 사서함에 일부 공용 폴더를 이동 하 여 Exchange 2013 서버에서 C:\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts 폴더에 있는 `Split-PublicFolderMailbox.ps1` 스크립트를 사용 하는 것이 좋습니다.
    
      - 많이 사용 하는 공용 폴더를 전용된 공용 폴더 사서함으로 이동 하는 것이 좋습니다.
    
      - 공용 폴더 계층 구조를 제공 하는에서 많이 사용 되는 공용 폴더를 제외 합니다. **Set-Mailbox** cmdlet을 사용 하 여 공용 폴더 사서함에서 *IsExcludedFromServingHierarchy* 속성을 설정 하 여이 수행할 수 있습니다.
    
      - 많은 공용 폴더를 가진 대규모 조직에 대 한 공용 폴더 계층 구조 요청에 응답의 부하를 분산 하 추가 공용 폴더 사서함을 추가 하는 것이 좋습니다.

  - 기본 공용 폴더 사서함은 사서함의 가용성을 향상 시키기 위해 DAG에 배치 합니다. 기본 공용 폴더 사서함은 신뢰할 수 있는 복사본 공용 폴더 계층 구조입니다.

  - DAG에 보조 공용 폴더 사서함을 삽입 하거나 사서함을 자주 백업 합니다.

  - 공용 폴더 사서함에 공용 폴더 콘텐츠에 액세스 하는 사용자가 가장 가까운 된 지리적 위치에 배치 합니다.

  - 에 게 근접 한 공용 폴더 사서함을 지정 하려면 사용자의 사서함에서 DefaultPublicFolderMailbox 속성을 사용 하 여 공용 폴더 계층 구조 액세스 시간을 개선 합니다. 이렇게 하면 다른 지리적 위치에 공용 폴더 사서함에서 공용 폴더 계층 구조를 검색 하는에서 해당 사용자가 되지 것입니다.

  - 50 개 이상의 보조 공용 폴더 사서함이 있는 배포의 경우에 기본 공용 폴더 사서함의 공용 폴더 콘텐츠를 저장 하지는 것이 좋습니다. 이 기본 공용 폴더 사서함이 보조 공용 폴더 사서함을 가진 계층 구조 동기화 (영문)에 집중 합니다.

  - 더이상 Exchange 2013 공용 폴더 데이터베이스를 지원합니다. 따라서 Exchange 2013 사서함이 있는 Outlook Web App 사용자가 Exchange 2010 또는 Exchange 2007 공용 폴더에 액세스할 수 없습니다. Exchange 2013 사용자가 Outlook 또는 Outlook for mac입니다. Exchange 2010 또는 Exchange 2007 공용 폴더에 액세스할 수 있습니다.

  - Outlook Web App은 지원 되지만 제한 사항과 함께 합니다. 추가 하 고 및 즐겨찾기 공용 폴더를 제거 하 고, 만들기, 편집, 게시물, 삭제 및 게시물에 회신 하기 예: 항목 수준 작업을 수행할 수 있습니다. 그러나 없습니다 만들거나 Outlook Web App에서 공용 폴더를 삭제 합니다. 또한 Outlook Web App에서 즐겨찾기 목록에만 메일, 게시, 일정 및 연락처 공용 폴더를 추가할 수 있습니다.

  - 공용 폴더 콘텐츠에 대한 전체 텍스트 검색을 수행할 수는 있지만, 여러 공용 폴더 간에 공용 폴더 콘텐츠를 검색할 수는 없으며 Exchange 검색에서는 콘텐츠를 인덱싱하지 않습니다.

  - Exchange 2013 서버에서 공용 폴더에 액세스하려면 Outlook 2007 이상을 사용해야 합니다.

  - 공용 폴더 사서함에 대해 보존 정책이 지원되지 않습니다.

