﻿---
title: '메일 흐름: Exchange 2013 Help'
TOCTitle: 메일 흐름
ms:assetid: 14df5e1a-a5f7-4b0d-ba97-f53b76f0e7e0
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa996349(v=EXCHG.150)
ms:contentKeyID: 50482576
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메일 흐름

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

Microsoft Exchange Server 2013에서 메일 흐름은 전송 파이프라인을 통해 발생합니다. *전송 파이프라인*은 조직 내부 사서함 서버의 전송 서비스에 있는 분류기에 모든 메시지를 라우팅하기 위해 함께 작동하는 서비스, 연결, 구성 요소 및 큐의 모음입니다.

모든 메일 흐름 항목의 목록은 Mail flow documentation를 참조하십시오.

새 Exchange 2013 조직에서 메일 흐름을 구성하는 방법에 대한 자세한 내용은 [메일 흐름 및 클라이언트 액세스 구성](configure-mail-flow-and-client-access-exchange-2013-help.md)을 참조하십시오.

**목차**

The transport pipeline

The Transport service on a Mailbox server

Mail flow documentation

## 전송 파이프라인

전송 파이프라인은 다음 서비스로 구성됩니다.

  - **클라이언트 액세스 서버의 프런트 엔드 전송 서비스**   이 서비스는 Exchange 2013 조직의 모든 인바운드 및 아웃바운드(선택 사항) 외부 SMTP 트래픽에 대한 상태 비저장 프록시로 작동합니다. 프런트 엔드 전송 서비스는 메시지 내용을 검사하지 않고 사서함 서버의 사서함 전송 서비스와 통신하지 않으며 메시지를 로컬로 대기시키지 않습니다.

  - **사서함 서버의 전송 서비스**   이 서비스는 이전 버전의 Exchange에 제공되던 허브 전송 서버 역할과 거의 동일합니다. 전송 서비스는 조직의 모든 SMTP 메일 흐름을 처리하고, 메시지 분류를 수행하고, 메시지 콘텐츠 검사를 수행합니다. 이전 버전의 Exchange와 달리 전송 서비스는 사서함 데이터베이스와 직접 통신하지 않습니다. 이 작업은 이제 사서함 전송 서비스에 의해 처리됩니다. 전송 서비스는 사서함 전송 서비스, 전송 서비스, 프런트 엔드 전송 서비스 및 구성에 따라 Edge 전송 서버의 전송 서비스 간에 메시지를 라우팅합니다. 사서함 서버의 전송 서비스에 대해서는 이 항목의 뒷부분에서 보다 자세히 설명합니다.

  - **사서함 서버의 사서함 전송 서비스**   이 서비스에는 다음 개별 서비스 두 개가 포함됩니다. 사서함 전송 제출 서비스 및 사서함 전송 배달 서비스. 사서함 전송 배달 서비스는 로컬 사서함 서버나 다른 사서함 서버의 전송 서비스에서 SMTP 메시지를 수신하고 Exchange RPC(원격 프로시저 호출)를 통해 로컬 사서함 데이터베이스에 연결하여 메시지를 배달합니다. 사서함 전송 제출 서비스는 RPC로 로컬 사서함 데이터베이스에 연결하여 메시지를 검색하고 SMTP를 통해 로컬 사서함 서버나 다른 사서함 서버의 전송 서비스에 메시지를 전송합니다. 사서함 전송 제출 서비스는 전송 서비스와 동일한 라우팅 토폴로지 정보에 액세스할 수 있습니다. 프런트 엔드 전송 서비스와 마찬가지로 사서함 전송 서비스도 메시지를 로컬 큐에 넣지 않습니다.

  - **Edge 전송 서버의 전송 서비스**   이 서비스는 사서함 서버의 전송 서비스와 매우 비슷합니다. 경계 네트워크에 Edge 전송 서버가 설치되어 있으면 인터넷에서 주고 받는 모든 메일이 전송 서비스 Edge 전송 서버를 통과합니다. 이 서비스에 대해서는 이 항목의 뒷부분에서 더 자세하게 설명합니다.

다음 그림에서는 Exchange 2013 전송 파이프라인의 구성 요소 간 관계를 보여줍니다.

**Exchange 2013의 전송 파이프라인 개요**

![전송 파이프라인 개요 다이어그램](images/Aa996349.6f548b64-6ac2-4e98-9098-69ad6cd9f569(EXCHG.150).gif "전송 파이프라인 개요 다이어그램")

## 외부 보낸 사람의 메시지

조직 외부에서 보낸 메시지는 클라이언트 액세스 서버의 프런트 엔드 전송 서비스에 있는 수신 커넥터를 통해 전송 파이프라인으로 들어간 다음 사서함 서버의 전송 서비스로 라우팅됩니다.

경계 네트워크에 Exchange 2013 Edge 전송 서버가 설치되어 있는 경우 조직 외부에서 보낸 메시지는 Edge 전송 서버의 전송 서비스에 있는 수신 커넥터를 통해 전송 파이프라인으로 들어갑니다. 그 다음에 메시지가 이동하는 위치는 내부 Exchange 서버가 구성된 방식에 따라 달라집니다.

  - **같은 컴퓨터에 설치된 사서함 서버 및 클라이언트 액세스 서버**   이 구성에서는 클라이언트 액세스 서버가 인바운드 메일 흐름에 사용됩니다. 메일은 Edge 전송 서버의 전송 서비스에서 클라이언트 액세스 서버의 프런트 엔드 전송 서비스로 이동한 다음 사서함 서버의 전송 서비스로 이동합니다.

  - **다른 컴퓨터에 설치된 사서함 서버 및 클라이언트 액세스 서버**   이 구성에서는 인바운드 메일 흐름에 대해 클라이언트 액세스 서버가 무시됩니다. 메일은 Edge 전송 서버의 전송 서비스에서 사서함 서버의 전송 서비스로 이동됩니다.


> [!NOTE]
> 경계 네트워크에 Exchange 2010 또는 Exchange 2007 Edge 전송 서버가 설치되어 있으면 메일 흐름이 사서함 서버의 전송 서비스와 Edge 전송 서버 간에 항상 직접 수행됩니다. 자세한 내용은 <A href="use-an-exchange-2010-or-2007-edge-transport-server-in-exchange-2013-exchange-2013-help.md">Exchange 2010 또는 2007 Edge 전송 서버에서 Exchange 2013 사용</A>을 참조하십시오.



## 내부 보낸 사람의 메시지

조직 내부에서 보내는 SMTP 메시지는 다음 중 한 가지 방법으로 사서함 서버의 전송 서비스를 통해 전송 파이프라인으로 들어갑니다.

  - 수신 커넥터를 통해

  - Pickup 디렉터리나 Replay 디렉터리에서

  - 사서함 전송 서비스에서

  - 에이전트 전송을 통해

메시지는 라우팅 대상 또는 배달 그룹을 기준으로 라우팅됩니다. 자세한 내용은 [메일 라우팅](mail-routing-exchange-2013-help.md)를 참조하세요.

외부 받는 사람이 있는 메시지는 사서함 서버의 전송 서비스에서 인터넷으로 라우팅됩니다. 또는 송신 커넥터가 클라이언트 액세스 서버를 통해 아웃바운드 연결을 프록시하도록 구성되어 있는 경우 사서함 서버에서 클라이언트 액세스 서버의 프런트 엔드 전송 서비스로 라우팅된 다음 인터넷으로 라우팅됩니다. 자세한 내용은 [인터넷에 보낸 전자 메일에 대 한 송신 커넥터 만들기](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)를 참조하세요.

경계 네트워크에 Edge 전송 서버가 설치되어 있는 경우 외부 받는 사람이 있는 메시지는 클라이언트 액세스 서버의 프런트 엔드 전송 서비스를 통해 라우팅되지 않으며 사서함 서버의 전송 서비스에서 Edge 전송 서버의 전송 서비스로 라우팅됩니다.

## 사서함 서버의 전송 서비스

Exchange 2013 조직에서 보내거나 받는 모든 메시지는 먼저 사서함 서버의 전송 서비스에서 분류되어야만 라우팅 및 배달될 수 있습니다. 분류된 메시지는 대상 사서함 데이터베이스, 대상 DAG(데이터베이스 사용 가능 그룹), Active Directory 사이트, Active Directory 포리스트 또는 조직 외부의 대상 도메인으로 배달하기 위해 배달 큐에 추가됩니다.

사서함 서버의 전송 서비스는 다음 구성 요소와 프로세스로 구성됩니다.

  - **SMTP 수신**   전송 서비스에서 메시지를 받으면 메시지 콘텐츠 검사가 수행되고 전송 규칙이 적용되며 사용 가능한 경우 스팸 방지 및 맬웨어 방지 검사가 수행됩니다. SMTP 세션에는 메시지를 수락하기 전에 메시지 콘텐츠의 유효성을 검사하기 위해 특정 순서로 함께 작동되는 일련의 이벤트가 있습니다. 메시지가 SMTP 수신을 통해 완전히 전달된 후 수신 이벤트나 스팸 방지 및 맬웨어 방지 에이전트에 의해 거부되지 않으면 전송 큐에 추가됩니다.

  - **전송**   전송은 메시지를 전송 큐에 넣는 프로세스입니다. 분류기는 분류할 메시지를 한 번에 하나씩 선택합니다. 전송은 다음 세 가지 방법으로 이루어집니다.
    
      - SMTP 수신에서 수신 커넥터를 통해
    
      - Pickup 디렉터리나 Replay 디렉터리를 통해 이러한 디렉터리는 사서함 서버와 Edge 전송 서버에 있습니다. Pickup 디렉터리나 Replay 디렉터리에 복사되는 올바른 형식의 메시지 파일은 직접 전송 큐에 추가됩니다.
    
      - 전송 에이전트를 통해

  - **분류기**   분류기는 전송 큐에서 한 번에 하나의 메시지를 선택합니다. 분류기는 다음 단계를 완료합니다.
    
      - 받는 사람 확인(최상위 주소 지정, 확장 및 분기 포함)
    
      - 라우팅 확인
    
      - 콘텐츠 변환
    
    또한 조직에서 정의한 메일 흐름 규칙이 적용됩니다. 분류된 메시지는 메시지의 대상을 기반으로 하는 배달 큐에 추가됩니다. 메시지는 대상 사서함 데이터베이스, DAG, Active Directory 사이트, Active Directory 포리스트 또는 외부 도메인에 의해 대기됩니다.

  - **SMTP 송신**   메시지가 전송 서비스에서 라우팅되는 방식은 분류가 발생한 사서함 서버를 기준으로 메시지 받는 사람의 위치에 따라 다릅니다. 다음 위치 중 하나로 메시지를 라우팅할 수 있습니다.
    
      - 같은 사서함 서버의 사서함 전송 서비스
    
      - 같은 DAG의 일부분인 다른 사서함 서버의 사서함 전송 서비스
    
      - 다른 DAG, Active Directory 사이트 또는 Active Directory 포리스트에 있는 사서함 서버의 전송 서비스
    
      - 같은 사서함 서버의 송신 커넥터, 다른 사서함 서버의 전송 서비스, 클라이언트 액세스 서버의 프런트 엔드 전송 서비스 또는 경계 네트워크의 Edge 전송 서버에 있는 전송 서비스를 통해 인터넷으로 배달

## Edge 전송 서버의 전송 서비스

Edge 전송 서버의 전송 서비스 구성 요소는 사서함 서버의 전송 서비스 구성 요소와 동일합니다. 그러나 Edge 전송 서버의 각 처리 단계에서 실제로 수행되는 작업은 서로 다릅니다. 다음 목록에 작업의 차이점이 설명되어 있습니다.

  - **SMTP 수신**   Edge전송 서버가 내부 Active Directory 사이트에 구독되어 있으면 기본 수신 커넥터는 내부 사서함 서버와 인터넷에서 보내는 메일을 수락하도록 자동으로 구성됩니다. Edge 전송 서버에 인터넷 메시지가 도착하면 스팸 방지 에이전트는 연결 및 메시지 내용을 필터링하고 조직에서 메시지를 수락하는 동안 메시지 보낸 사람과 받는 사람을 식별할 수 있도록 합니다. 스팸 방지 에이전트는 기본적으로 설치되며 사용하도록 설정됩니다. 추가 첨부 파일 필터링 및 연결 필터링 기능도 사용할 수 있지만 기본 제공 맬웨어 필터링은 사용할 수 없습니다. 또한 전송 규칙은 Edge 규칙 에이전트에 의해 제어됩니다. Edge 전송 서버에서는 사서함 서버의 전송 규칙 에이전트에 비해 일부 전송 규칙 조건만 제공됩니다. 그러나 SMTP 연결과 관련하여 Edge 전송 서버에서만 사용 가능한 고유한 전송 규칙 작업도 있습니다.

  - **전송**   Edge 전송 서버에서 메시지는 보통 송신 커넥터를 통해 전송 큐로 들어갑니다. 그러나 Pickup 디렉터리 및 Replay 디렉터리도 사용할 수 있습니다.

  - **분류기**   Edge 전송 서버에서는 내부 또는 외부 받는 사람에게 배달할 메시지가 배달 큐로 직접 추가되므로 분류가 아주 간단히 진행됩니다.

  - **SMTP 송신**   Edge 전송 서버가 내부 Active Directory 사이트에 구독되어 있으면 송신 커넥터 두 개가 자동으로 만들어져 구성됩니다. 두 커넥터 중 하나는 인터넷 받는 사람에게 아웃바운드 메일을 전송하고 다른 하나는 인터넷의 인바운드 메일을 내부 받는 사람에게 전송합니다. 인바운드 메일은 구독된 Active Directory 사이트에서 사용 가능한 사서함 서버의 전송 서비스로 전송됩니다.

## 메일 흐름 설명서

다음 표에는 Exchange 2013에서 메일 흐름에 대해 자세히 알아보고 관리하는 데 도움이 되는 항목에 대한 링크가 포함되어 있습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>항목</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-routing-exchange-2013-help.md">메일 라우팅</a></p></td>
<td><p>메일 라우팅은 메시지가 메시징 서버 간에 전송되는 방식을 설명합니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="connectors-exchange-2013-help.md">커넥터</a></p></td>
<td><p>커넥터는 Exchange 서버 간에 메시지가 전송되는 위치 및 방식을 정의합니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="domains-exchange-2013-help.md">도메인</a></p></td>
<td><p>허용 도메인은 Exchange 조직에서 사용되는 SMTP 주소 공간을 정의합니다. 원격 도메인은 외부 도메인으로 전송되는 메시지의 메시지 형식 및 인코딩 설정을 구성합니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="transport-agents-exchange-2013-help.md">전송 에이전트</a></p></td>
<td><p>전송 에이전트는 Exchange 전송 파이프라인을 통해 이동되는 메시지에 작용합니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="transport-high-availability-exchange-2013-help.md">전송 고가용성</a></p></td>
<td><p>전송 고가용성은 Exchange 2013에서 전송 중 및 배달 후에 메시지의 중복 복사본을 유지하는 방식을 설명합니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="transport-logs-exchange-2013-help.md">전송 로그</a></p></td>
<td><p>전송 로그는 메시지가 전송 파이프라인을 통해 흐를 때 메시지에 발생하는 일을 기록합니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-message-approval-exchange-2013-help.md">메시지 승인 관리</a></p></td>
<td><p>중재된 전송을 위해서는 특정 받는 사람에 보내는 메시지에 대한 승인이 필요합니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="content-conversion-exchange-2013-help.md">콘텐츠 변환</a></p></td>
<td><p>콘텐츠 변환은 외부 받는 사람에 대한 TNEF(Transport Neutral Encoding Format) 메시지 변환 옵션과 내부 받는 사람에 대한 MAPI 변환 옵션을 제어합니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="dsns-and-ndrs-in-exchange-2013-exchange-2013-help.md">Exchange 2013의 Dsn 및 Ndr</a></p></td>
<td><p>DSN(배달 상태 알림)은 메시지 보낸 사람에게 전송되는 시스템 메시지입니다(예: 배달 못 함 보고서(NDR)).</p></td>
</tr>
<tr class="even">
<td><p><a href="track-messages-with-delivery-reports-exchange-2013-help.md">배달 보고서로 메시지 추적</a></p></td>
<td><p>배달 보고서는 조직의 주소록에 있는 사용자에게 보냈거나 사용자에게서 받은 특정 제목의 전자 메일 메시지의 배달 상태를 검색하는 데 사용할 수 있는 메시지 추적 도구입니다. 조직의 특정 사서함에서 주고받은 메시지에 대한 배달 정보를 추적할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="message-size-limits-exchange-2013-help.md">메시지 크기 제한</a></p></td>
<td><p>이 항목에서는 메시지에 적용되는 크기 제한 및 개별 구성 요소 제한에 대해 설명합니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="queue-viewer-exchange-2013-help.md">큐 뷰어</a></p></td>
<td><p>Exchange 도구 상자의 큐 뷰어를 사용하여 큐 및 큐의 메시지를 보거나 작업합니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="pickup-directory-and-replay-directory-exchange-2013-help.md">Pickup 디렉터리 및 Replay 디렉터리</a></p></td>
<td><p>픽업 및 Replay 디렉터리는 메시지 파일을 전송 파이프라인에 삽입하는 데 사용됩니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="use-an-exchange-2010-or-2007-edge-transport-server-in-exchange-2013-exchange-2013-help.md">Exchange 2010 또는 2007 Edge 전송 서버에서 Exchange 2013 사용</a></p></td>
<td><p>이 항목에서는 Exchange 2013에서 이전 버전 Exchange의 Edge 전송 서버를 사용할 때 고려할 사항을 설명합니다.</p></td>
</tr>
</tbody>
</table>

