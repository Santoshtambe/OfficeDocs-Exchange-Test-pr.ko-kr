﻿---
title: '데이터베이스 가용성 그룹에 대한 클러스터 이름 개체 미리 준비: Exchange 2013 Help'
TOCTitle: 데이터베이스 가용성 그룹에 대한 클러스터 이름 개체 미리 준비
ms:assetid: 51ebf2f6-8a02-44ef-a489-ca361cb0f63a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff367878(v=EXCHG.150)
ms:contentKeyID: 50483101
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 데이터베이스 가용성 그룹에 대한 클러스터 이름 개체 미리 준비

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-08-14_

컴퓨터 계정 만들기 제한 된이 이거나 기본 컴퓨터 컨테이너 이외의 컨테이너에서 컴퓨터 계정을 만들어지는 수 사전 준비 환경에서 클러스터 개체 (CNO) 이름을 지정 하 고 사용 권한을 할당 하 여 CNO를 프로 비전 합니다. CNO 미리 준비 컴퓨터 개체에 대 한 Windows의 사용 권한 변경으로 인해 Windows Server 2012 및 Windows Server 2012 R2 DAG 구성원에 대 한 필수 이기도 합니다. Windows Server 2012를 실행 하는 사서함 서버 또는 Windows Server 2012 r 2를 사용 하 여 데이터베이스 가용성 그룹 (DAG)를 배포할 때 미리 준비 하 고 클러스터 관리 액세스 포인트가 없는 DAG를 배포 하는 경우가 아니면 CNO를 프로 비전 해야 합니다. 클러스터 관리 액세스 포인트가 없는 Dag CNOs;를 사용 하지 않는 따라서 미리 준비에 대 한 필요 하지 않은 이러한 Dag 합니다.

CNO에 대한 컴퓨터 계정을 만들거나 사용하지 않도록 설정한 후 다음을 수행합니다.

  - DAG에 추가하려는 첫 번째 사서함 서버의 컴퓨터 계정에 대한 컴퓨터 계정의 모든 권한 할당

  - Exchange Trusted Subsystem USG(유니버설 보안 그룹)에 대한 컴퓨터 계정의 모든 권한 할당

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분

  - Active Directory에 컴퓨터 개체를 만들 수 있는 권한이 있는 계정을 사용해야 합니다.

  - 다음 단계를 완료한 후 Active Directory 복제가 발생할 수 있는 시간을 허용합니다. 개체가 복제된 후에는 DAG에 첫 번째 구성원을 추가할 수 있습니다.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## CNO 미리 준비

1.  Active Directory 사용자 및 컴퓨터를 엽니다.

2.  포리스트 노드를 확장합니다.

3.  새 계정을 만들 OU(조직 구성 단위)를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 선택한 다음 **컴퓨터**를 선택합니다.

4.  **새 개체 - 컴퓨터**에서 **컴퓨터 이름** 상자에 CNO의 컴퓨터 계정 이름을 입력합니다. 이 이름은 DAG에 사용할 이름입니다. **확인**을 클릭하여 계정을 만듭니다.

5.  새 컴퓨터 계정을 마우스 오른쪽 단추로 클릭한 다음 **계정 사용 안 함**을 클릭합니다. **예**를 클릭하여 비활성화 작업을 확인한 다음 **확인**을 클릭합니다.

## CNO에 권한 할당

1.  Active Directory 사용자 및 컴퓨터를 엽니다.

2.  고급 기능이 사용할 수 없도록 설정된 경우 **보기**를 클릭하고 **고급 기능**을 클릭하여 고급 기능을 사용하도록 설정합니다.

3.  새 컴퓨터 계정을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.

4.  **\<컴퓨터 이름\> 속성**의 **보안** 탭에서 **추가**를 클릭하여 DAG에 추가할 첫 번째 노드에 대한 컴퓨터 계정을 추가하거나 Exchange Trusted Subsystem USG를 추가합니다.
    
      - Exchange Trusted Subsystem을 추가하려면 **선택할 개체 이름을 입력하십시오.** 필드에 **Exchange Trusted Subsystem**을 입력합니다. USG를 추가하려면 **확인**을 클릭합니다. Exchange Trusted Subsystem USG를 선택하고 **Exchange Trusted Subsystem에 대한 권한** 필드의 **허용** 열에서 **모든 권한**을 선택합니다. **확인**을 클릭하여 권한 설정을 저장합니다.
    
      - DAG에 추가할 첫 번째 노드의 컴퓨터 계정을 추가하려면 **개체 유형**을 클릭합니다. **개체 유형** 대화 상자에서 **기본 제공 보안 주체**, **그룹** 및 **사용자** 확인란 선택을 취소합니다. **컴퓨터** 확인란을 선택한 다음 **확인**을 클릭합니다. **선택할 개체 이름을 입력하십시오.** 필드에서 DAG에 추가할 첫 번째 사서함 서버의 이름을 입력한 다음 **확인**을 클릭합니다. 첫 번째 노드의 컴퓨터 계정을 선택하고 **\<NodeName\>에 대한 권한** 필드의 **허용** 열에서 **모든 권한**을 선택합니다. **확인**을 클릭하여 권한 설정을 저장합니다.

## 작동 여부는 어떻게 확인합니까?

CNO가 성공적으로 만들어졌는지 확인하려면 다음을 수행합니다.

1.  Active Directory 사용자 및 컴퓨터를 엽니다.

2.  포리스트 노드를 확장합니다.

3.  계정을 만든 OU를 열고 계정이 나열되는지 확인합니다.

