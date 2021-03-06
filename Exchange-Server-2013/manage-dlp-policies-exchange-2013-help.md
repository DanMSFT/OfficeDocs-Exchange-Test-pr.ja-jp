﻿---
title: 'DLP ポリシーの管理: Exchange Online Help'
TOCTitle: DLP ポリシーの管理
ms:assetid: ba81fabd-7f7f-4ef7-968f-ce851ada9d70
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ673559(v=EXCHG.150)
ms:contentKeyID: 49896440
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# DLP ポリシーの管理

 

_**適用先:**Exchange Online, Exchange Server 2013_

Exchange 管理センター (EAC)または Exchange 管理シェルを使用して、Microsoft Exchange の既存のデータ損失防止 (DLP) ポリシーを表示、変更、または削除できます。

DLP に関連する追加の管理タスクについては、「[DLP の手順](dlp-procedures-exchange-2013-help.md)」(Exchange Server 2013) または「[DLP に関する手順](https://technet.microsoft.com/ja-jp/library/jj938003\(v=exchg.150\))」(Exchange Online) をご覧ください。

Exchange 管理シェルの詳細については、「[Exchange 2013 で Powershell を使用する (Exchange 管理シェル)](https://technet.microsoft.com/ja-jp/library/bb123778\(v=exchg.150\))」を参照してください。

## 始める前に把握しておくべき情報

  - 各手順の推定完了時間:15 ～ 60 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[メッセージング ポリシーとコンプライアンスのアクセス許可](messaging-policy-and-compliance-permissions-exchange-2013-help.md)」の「データ損失防止 (DLP)」。

  - DLP ポリシーは 3 つのモードを選択できます。
    
      -  
        **\[強制\]**   ポリシー内のルールがすべてのメッセージとサポートされているファイルの種類に対して評価されます。ポリシーの条件に適合するデータが検出された場合、メール フローを中断することができます。ポリシー内に記述されているすべての処理が実行されます。
    
      -  
        **\[ポリシー ヒントありで DLP ポリシーをテストする\]**   ポリシー内のルールがすべてのメッセージとサポートされているファイルの種類に対して評価されます。ポリシーの条件に適合するデータが検出された場合、メール フローは中断されません。つまり、メッセージはブロックされません。ポリシーのヒントが構成されている場合は、ユーザーに対して表示されます。
    
      -  
        **\[ポリシー ヒントなしで DLP ポリシーをテストする\]**   ポリシー内のルールがすべてのメッセージとサポートされているファイルの種類に対して評価されます。ポリシーの条件に適合するデータが検出された場合、メール フローは中断されません。つまり、メッセージはブロックされません。ポリシーのヒントが構成されている場合でも、ユーザーに対して表示されません。

  - DLP ポリシー内の個々のルールにそれぞれのモード設定を行えます。ポリシーのモードがそのポリシー内のルールのモードと異なる場合、ルールの設定が優先され、そのモードにしたがって評価されます。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。



## 必要な作業

## 既存の DLP ポリシーの詳細を表示する

組織に対して既に確立した既存の DLP ポリシーのルールと操作を表示することが必要な場合があります。これは、予期しないメール フローの問題が発生したり、組織が機密情報の監視方法を変更したりした場合に役に立ちます。

## EAC を使用して既存の DLP ポリシー内の詳細を表示する

1.  EAC 内で、**コンプライアンス管理** \> **データ損失防止** に移動します。

2.  ポリシーの一覧に表示されているいずれかのポリシーをダブルクリックするか、1 つのアイテムを強調表示して **\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[DLP ポリシーの編集\]** ページで、**\[ルール\]** をクリックします。


> [!TIP]
> DLP ポリシーを作成して、モードを非アクティブまたは無効のままにしておくことができます。このモードでは、ポリシーは適用されず、テストまたは適用開始前にルールに関連付けられている述語、操作、または値を変更できます。



## シェルを使用して既存の DLP ポリシー内の詳細を表示する

この例では、Employee Numbers という名前の架空の DLP ポリシーに関する情報を返しています。このコマンドは、指定した DLP ポリシーの詳細な構成を表示するために、**Format-List** コマンドレットにパイプ処理されます。

    Get-DlpPolicy "Employee Numbers" | Format-List

構文およびパラメーターの詳細については、「[Get-DlpPolicy](https://technet.microsoft.com/ja-jp/library/jj215752\(v=exchg.150\))」を参照してください。

## DLP ポリシーを変更する

既存の DLP ポリシーを変更するには、ポリシーの名前、またはポリシーの影響を制御しているルールを変更します。ルール変更の例としては、メッセージ本文への免責事項テキストの追加、特定のドメイン内で送信され、機密情報があることが検出されたメッセージに対する RMS 保護の追加などがあります。DLP ポリシー テンプレートを使用している場合、メッセージング環境用の堅牢なポリシーと法令遵守システムを設計および適用できる、Exchange 2013 のほんの 1 つの機能でしかないことに注意してください。

## EAC を使用して既存の DLP ポリシーを変更する

1.  EAC 内で、**コンプライアンス管理** \> **データ損失防止** に移動します。

2.  ポリシーの一覧に表示されているいずれかのテンプレート ベースのポリシーをダブルクリックするか、1 つのアイテムを強調表示して **\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  **\[DLP ポリシーの編集\]** ページで、**\[ルール\]** をクリックします。

4.  既存のルールを変更するには、ルールを強調表示して、**\[編集\]**![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

5.  完全にカスタマイズできる新しい空のルールを追加するには、**\[新規作成\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

6.  送信者通知に関するルール、メッセージの受信拒否に関するルール、または優先を許可するルールを追加するには、**\[新規作成\]**![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") アイコンの横にある矢印をクリックします。

7.  ルールを削除するには、ルールを強調表示して、**\[削除\]**![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン") をクリックします。

8.  **\[保存\]** をクリックして、ポリシーの変更を終了し、変更を保存します。

## シェルを使用して既存の DLP ポリシーを変更する

Exchange 管理シェルを使用して、ポリシーの操作と通知レベルを指定できます。この例では、Employee Numbers という名前の架空の DLP ポリシーのモードを設定し、操作を適用せず通知メッセージを表示しないようにしています。

    Set-DlpPolicy "Employee Numbers" -Mode Audit

構文およびパラメーターの詳細については、「[Set-DlpPolicy](https://technet.microsoft.com/ja-jp/library/jj215778\(v=exchg.150\))」を参照してください。

## DLP ポリシーを削除する

EAC を使用して DLP ポリシーを完全に削除できます。ポリシーを削除すると、そのポリシーが適用されることはなくなり、ルールも操作も保存されません。

代わりに、ポリシーの操作状態またはモードを **\[ポリシー ヒントなしで DLP ポリシーをテストする\]** に設定できます。これでメッセージ環境からの適用が停止されますが、ポリシー自身の詳細な構成設定は保持されます。これは、将来このポリシーを再度適用する必要がある場合に役に立ちます。

## EAC を使用して既存の DLP ポリシーを削除する

1.  EAC 内で、**コンプライアンス管理** \> **データ損失防止** に移動します。

2.  ポリシーの一覧から削除するポリシーを選択し、 **\[削除\]**![\[削除\] アイコン](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "[削除] アイコン") をクリックします。

## シェルを使用して既存の DLP ポリシーを変更する

この例では、Employee Numbers という名前の架空の DLP ポリシーを削除しています。

    Remove-DlpPolicy "Employee Numbers"

構文およびパラメーターの詳細については、「[Remove-DlpPolicy](https://technet.microsoft.com/ja-jp/library/jj215677\(v=exchg.150\))」を参照してください。

## 詳細情報

[データ損失防止](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[ポリシー ヒント](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)

