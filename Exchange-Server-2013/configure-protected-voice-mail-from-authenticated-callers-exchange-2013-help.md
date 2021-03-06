﻿---
title: '인증 된 호출자 로부터 보호 된 음성 메일 구성: Exchange 2013 Help'
TOCTitle: 인증 된 호출자 로부터 보호 된 음성 메일 구성
ms:assetid: f69e94a7-9768-4445-9ded-e78d732bd623
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee423560(v=EXCHG.150)
ms:contentKeyID: 52057987
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 인증 된 호출자 로부터 보호 된 음성 메일 구성

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-02-22_

수신 전화에 응답 하 고 다음 음성 메일 메시지를 암호화를 사용 하 여 보호에 적용 합니다 있는지 여부를 결정 하도록 통합 메시징을 구성할 수 있습니다. 음성 메시지를 보호 될 때:

  - Microsoft Outlook 및 Outlook Web App에서 메시지가 비공개로 표시됩니다.

  - 음성 메시지는 받는 사람만이 열 수 있습니다.

  - 받는 사람은 음성 메시지에 회신할 수 있지만 원래 음성 메시지에 포함되지 않은 사람에게는 음성 메시지를 전달할 수 없습니다.

이 설정은 전화에 응답 하지 않을 때 UM 사용이 가능한 사용자에 게 보내는 음성 메시지에 적용 됩니다. 이 설정은 발신자에 게 Outlook Voice Access를 사용 하 여 자신의 사서함에 로그인 하 고 다음 만들고 음성 메시지를 보낼 때에 적용 됩니다.

보호된 음성 메일 절차와 관련된 추가 관리 작업에 대한 자세한 내용은 [보호 된 음성 메일 절차](protected-voice-mail-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함 정책" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 인증 된 호출자 로부터 보호 된 음성 메일을 구성 하려면

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 수정하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 사서함 정책**에서 관리할 UM 사서함 정책을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 사서함 정책** 페이지에서 \> **보호 된 음성 메일**, **인증 된 호출자 로부터 보호 음성 메시지** 아래에서 다음 옵션 중 하나를 선택 합니다.
    
      - **없음**   UM 사용 가능 사용자에게 보내는 음성 메시지에 보호 기능을 적용하지 않으려면 이 설정을 사용합니다.
    
      - **비공개**   통합 메시징에서 발신자가 비공개로 표시한 음성 메시지에만 보호 기능을 적용하도록 하려면 이 설정을 사용합니다.
    
      - **모두**   통합 메시징에서 비공개로 표시되지 않은 음성 메시지를 포함하여 모든 음성 메시지에 보호 기능을 적용하도록 하려면 이 설정을 사용합니다.

4.  **저장**을 클릭합니다.

## 셸을 사용 하 여 인증 된 호출자 로부터 보호 된 음성 메일을 구성 하려면

UM 사서함 정책 `MyUMMailboxPolicy`에 있는 모든 인증 된 호출자에서 음성 메시지를 보호 하는이 예제입니다.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy ProtectAuthenticatedVoiceMail -All

