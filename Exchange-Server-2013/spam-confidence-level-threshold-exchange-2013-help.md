﻿---
title: 'Spam Confidence Level のしきい値: Exchange 2013 Help'
TOCTitle: Spam Confidence Level のしきい値
ms:assetid: 0009b4af-be6d-41d2-98bc-b5487272c74a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Aa995744(v=EXCHG.150)
ms:contentKeyID: 49895204
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Spam Confidence Level のしきい値

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2016-11-17_


> [!NOTE]
> 2016 年 11 月 1 日に Microsoft は、Exchange と Outlook の SmartScreen フィルターのスパム定義の更新を停止しました。既存の SmartScreen スパム定義はそのままですが、その効果は時間とともに低下する可能性があります。詳しくは、「<A href="https://go.microsoft.com/fwlink/p/?linkid=835894">Outlook と Exchange での SmartScreen サポートの廃止</A>」をご覧ください。



Microsoft Exchange Server 2013 では、SCL (Spam Confidence Level) しきい値に応じて、固有の動作を定義できます。たとえば、コンテンツ フィルター エージェントを実行している Exchange サーバーで、メッセージの拒否、削除、または検疫用にさまざまなしきい値を定義できます。

コンテンツ フィルター エージェントでこの SCL のしきい値を構成することと、ユーザーのメールボックスで SCL 迷惑メール フォルダーを構成することを組み合わせると、より包括的で厳密なスパム対策戦略を実施するために役立ちます。Exchange 2013 に備わる、より厳密で詳細なこの SCL のしきい値調整機能は、Exchange 組織全体に対するスパム対策ソリューションの展開と維持にかかる全体的なコストの削減に貢献できます。

コンテンツ フィルター エージェントは、他のスパム対策エージェントが受信メッセージを処理をした後の、スパム対策サイクルの終わりごろに SCL レベルを割り当てます。コンテンツ フィルター エージェントより前に受信メッセージを処理する他のスパム対策エージェントの多くは、メッセージに対してどのように作用するかが決まっています。たとえば、エッジ トランスポート サーバー上で、接続フィルター エージェントは、リアルタイム ブロック リストに記載されている IP アドレスから送信されたメッセージをすべて拒否します。送信者フィルター エージェントと受信者フィルター エージェントも、同様に確定的な方法でメッセージを処理します。

Exchange 2013 では、これらの確定的なスパム対策エージェントが最初にメッセージを処理するため、コンテンツ フィルター エージェントで処理する必要があるメッセージの数が大幅に減少しています。スパム対策エージェントがメッセージを処理する順序の詳細については、「[スパム対策保護](anti-spam-protection-exchange-2013-help.md)」を参照してください。

コンテンツ フィルターは厳密で確定的な処理ではないため、コンテンツ フィルター エージェントが異なる SCL 値に対して実行する動作を調整できることが重要です。SCL のしきい値の構成を注意して調整することで、以下のもののサイズや数を最小限にすることができます。

  - スパム検疫用の格納域のサイズ

  - 誤って検疫場所に移動される正当な電子メール メッセージの数

  - Microsoft Outlook ユーザーの迷惑メール フォルダーに入った正当な電子メール メッセージの数

  - Outlook ユーザーの受信トレイまたは迷惑メール フォルダーに入った不快感を与えるスパム電子メール メッセージの数

  - Outlook ユーザーの受信トレイに入ったスパム電子メール メッセージの数

## SCL しきい値アクション

SCL のしきい値アクションを調整して、スパムである危険性がより高いメッセージに対して実行するコンテンツ フィルターの動作を段階的に強めることができます。この新しい機能を理解するためには、さまざまな SCL のしきい値の動作と、それらがどのように実装されているかを理解しておくと役に立ちます。

  - **SCL による削除のしきい値**   特定のメッセージの SCL 値が SCL による削除のしきい値以上の場合、コンテンツ フィルター エージェントはそのメッセージを削除します。送信側のシステムや送信者にメッセージが削除されたことを伝えるプロトコル レベルの通信はありません。メッセージの SCL 値が SCL による削除のしきい値より小さい場合、コンテンツ フィルター エージェントはそのメッセージを削除しません。代わりに、その SCL 値は SCL による拒否のしきい値と比較されます。

  - **SCL による拒否のしきい値**   特定のメッセージの SCL 値が SCL による拒否のしきい値以上の場合、コンテンツ フィルター エージェントはそのメッセージを削除し、送信側のシステムに拒否応答を送信します。拒否応答はカスタマイズできます。場合によっては、メッセージの元の送信者に配信不能レポート (NDR) が送信されます。メッセージの SCL 値が SCL による削除のしきい値や SCL による拒否のしきい値より小さい場合、コンテンツ フィルター エージェントはそのメッセージの削除や拒否を行いません。代わりに、その SCL 値は SCL による検疫のしきい値と比較されます。

  - **SCL による検疫のしきい値**   特定のメッセージの SCL 値が SCL による検疫のしきい値以上の場合、コンテンツ フィルター エージェントはそのメッセージを検疫メールボックスに送ります。電子メール管理者は、検疫メールボックスを定期的に調べる必要があります。メッセージの SCL 値が、削除、拒否、および検疫の SCL のしきい値より小さい場合、コンテンツ フィルター エージェントはそのメッセージの削除、拒否、または検疫を行いません。代わりに、コンテンツ フィルター エージェントはそのメッセージを適切なメールボックス サーバーに送信します。このサーバーでは、そのメッセージについて、受信者ごとの SCL 迷惑メール フォルダーのしきい値が評価されます。

  - **SCL 迷惑メール フォルダーのしきい値**   特定メッセージの SCL 値が SCL 迷惑メール フォルダーしきい値を超えると、メッセージがユーザーの迷惑メール フォルダーに配信されます。メッセージの SCL 値が、SCL による削除、拒否、検疫、および迷惑メール フォルダーのしきい値より小さい場合、サーバーはメッセージをユーザーの受信トレイに配信します。

コンテンツ フィルター エージェントおよび迷惑メール フォルダーでは、SCL しきい値が別々の方法で処理されます。コンテンツ フィルター エージェントは、構成した SCL のしきい値に基づいて動作します。迷惑メール フォルダーは、構成した SCL しきい値に 1 を加えた値に基づいて動作します。たとえば、コンテンツ フィルター エージェントの削除アクションで SCL 値 8 を構成すると、SCL 値 8 以上のすべてのメッセージが削除されます。ただし、SCL しきい値を 4 にして迷惑メール フォルダーを構成した場合、SCL が 5 以上であるすべてのメッセージは迷惑メール フォルダーに移動します。

たとえば、SCL による削除のしきい値を 8、SCL による拒否のしきい値を 7、SCL による検疫のしきい値を 6、SCL 迷惑メール フォルダーのしきい値を 4 に設定している場合、SCL が 5 以下のメッセージはすべてユーザーのメールボックスに配信されます。SCL 値が 5 のメッセージは、ユーザーの迷惑メール フォルダーに入れられます。SCL 値が 4 以下のメッセージは、ユーザーの受信トレイに入れられます。

SCL 削除、拒否、検閲、および迷惑メール フォルダーの設定は、次の場所で構成できます。

  - **コンテンツ フィルター エージェント構成 (トランスポート サーバーごとの SCL 構成)** **Set-ContentFilterConfig** コマンドレットを使用して、コンテンツ フィルター エージェントを実行している Exchange サーバー上で SCL 削除、拒否、および検閲しきい値を有効または無効にします。時間が経過し、スパム対策のログ記録やレポート機能によって提供されるスパムの機能と測定値を分析するときに、必要に応じてこれらの SCL のしきい値の構成をさらに調整することができます。
    
    次の表に、**Set-ContentFilterConfig** コマンドレットで使用できる SCL パラメーターを示します。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>パラメーター</th>
    <th>説明</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLDeleteEnabled</em></p></td>
    <td><p>このパラメーターは、メッセージの SCL 値が <em>SCLDeleteThreshold</em> パラメーターで指定された値と同じかそれ以上の場合、配信不能レポート (NDR) なしでメッセージを削除することを有効または無効にします。このパラメーターの有効な入力値は、<code>$true</code> または <code>$false</code> です。</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLDeleteThreshold</em></p></td>
    <td><p>このパラメーターの有効な入力値は、0 ～ 9 の整数です。このパラメーターの値は、他の SCL しきい値パラメーターより大きい必要があります。このパラメーターは、<em>SCLDeleteEnabled</em> パラメーターの値が <code>$true</code> である場合のみ意味を持ちます。</p></td>
    </tr>
    <tr class="odd">
    <td><p><em>SCLRejectEnabled</em></p></td>
    <td><p>このパラメーターは、メッセージの SCL 値が <em>SCLRejectThreshold</em> パラメーターで指定された値と同じかそれ以上の場合、NDR なしでメッセージを拒否することを有効または無効にします。このパラメーターの有効な入力値は、<code>$true</code> または <code>$false</code> です。</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLRejectThreshold</em></p></td>
    <td><p>このパラメーターの有効な入力値は、0 ～ 9 の整数です。このパラメーターの値は、<em>SCLDeleteThreshold</em> パラメーターより小さくて、他の SCL しきい値パラメーターよりも大きい必要があります。このパラメーターは <em>SCLRejectEnabled</em> パラメーターの値が <code>$true</code> の場合のみ意味を持ちます。</p></td>
    </tr>
    <tr class="odd">
    <td><p><em>SCLQuarantineEnabled</em></p></td>
    <td><p>このパラメーターは、メッセージの SCL 値が <em>SCLQuarantineThreshold</em> パラメーターで指定された値と同じかそれ以上の場合、スパム検疫メールボックスにメッセージを送信することを有効または無効にします。このパラメーターの有効な入力値は、<code>$true</code> または <code>$false</code> です。</p>
    <p>スパム検疫メールボックスの詳細については、「<a href="spam-quarantine-exchange-2013-help.md">スパム検疫</a>」を参照してください。</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLQuarantineThreshold</em></p></td>
    <td><p>このパラメーターの有効な入力値は、0 ～ 9 の整数です。このパラメーターの値は、<em>SCLRejectThreshold</em> パラメーターより小さくて、<strong>Set-OrganizationConfig</strong> または <strong>Set-Mailbox</strong> コマンドレットの <em>SCLJunkThreshold</em> パラメーターよりも大きい必要があります。このパラメーターは、<em>SCLQuarantineThreshold</em> パラメーターの値が <code>$true</code> である場合のみ意味を持ちます。</p></td>
    </tr>
    </tbody>
    </table>


  - **組織構成設定 (組織全体 SCL 構成)** **Set-OrganizationConfig** コマンドレットを使用して、組織内のすべてのメールボックスに SCL 迷惑メール フォルダーしきい値を設定します。
    
    次の表に、**Set-OrganizationConfig** コマンドレットで使用できる SCL パラメーターを示します。SCLJunkThreshold の使用例については、「[メールボックスにおけるスパム対策設定の構成](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md)」を参照してください。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>パラメーター</th>
    <th>説明</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLJunkThreshold</em></p></td>
    <td><p>このパラメーターには、受信者のメールボックスの迷惑メッセージ フォルダーにメッセージを移動するために超える必要がある SCL 値を指定します。このパラメーターの有効な入力値は、0 ～ 9 の整数です。このパラメーターの値は、他の SCL しきい値パラメーターより小さい必要があります。たとえば、値 4 を指定する場合、SCL 値が 5 以上のメッセージがユーザーの迷惑メール フォルダーに移動します。</p></td>
    </tr>
    </tbody>
    </table>


  - **ユーザーのメールボックス (受信者ごとの SCL 構成)** **Set-Mailbox** コマンドレットを使用して、個々のメールボックスに対して受信者ごとの SCL による削除、拒否、検疫、および迷惑メール フォルダーのしきい値を有効または無効にして設定します。個々のメールボックスに対して SCL 迷惑メール フォルダーしきい値を有効または無効にするために、**Set-Mailbox** コマンドレットのみを使用できます。受信者ごとの SCL による削除、拒否、および検疫のしきい値は、Active Directory に格納され、Microsoft Exchange EdgeSync サービスによって購読済みエッジ トランスポート サーバーにレプリケートされます。受信者ごとの SCL のしきい値の構成は、トランスポート サーバーごとの SCL 構成が設定されている場合でも、コンテンツ フィルター エージェントによって使用されます。したがって、受信者ごとの SCL のしきい値を設定した場合、コンテンツ フィルター エージェントは特定のユーザーについて、コンテンツ フィルター エージェントの SCL 構成ではなく、受信者ごとの SCL のしきい値を使用します。例については、「[メールボックスにおけるスパム対策設定の構成](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md)」を参照してください。
    

    > [!NOTE]
    > 配布グループを介して受信したメールの受信者ごとの SCL のしきい値は適用されません。

    
    **Set-ContentFilterConfig** および **Set-OrganizationConfig** コマンドレットで使用できる **Set-Mailbox** コマンドレット上で、同じ SCL パラメーターが利用可能です。
    
      - *SCLDeleteEnabled*
    
      - *SCLDeleteThreshold*
    
      - *SCLRejectEnabled*
    
      - *SCLRejectThreshold*
    
      - *SCLQuarantineEnabled*
    
      - *SCLQuarantineThreshold*
    
      - *SCLJunkThreshold*
    
    ただし、**Set-Mailbox** コマンドレット上のすべての SCL パラメーターが値 `$null` も受け付けます。メールボックスへの SCL 設定が空 (`$null`) の場合、対応するコンテンツ フィルター エージェント設定または組織構成設定がメールボックスに適用されます。メールボックスへの SCL 設定の値が `$true` または `$false` である場合、メールボックスへの設定がコンテンツ フィルター エージェントまたは組織構成上の対応する組織全体の設定を上書きします。
    
    次の表に、**Set-Mailbox** コマンドレットでのみ使用できる SCL パラメーターを示します。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>パラメーター</th>
    <th>説明</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLJunkEnabled</em></p></td>
    <td><p>このパラメーターは、メッセージの SCL 値が <em>SCLQuarantineThreshold</em> パラメーターで指定された値より大きい場合、ユーザーの迷惑メール フォルダーにメッセージを配信することを有効または無効にします。このパラメーターの有効な入力値は、<code>$true</code>、<code>$false</code>、または <code>$null</code> です。</p>
    <p>迷惑メール フィルターは、既定で組織内のすべてのユーザー メールボックスで有効化されています。既定では、すべてのユーザー メールボックスの <strong>Set-MailboxJunkEmailConfiguration</strong> コマンドレットで <em>Enabled</em> パラメーターが値 <code>$true</code> に設定されます。</p></td>
    </tr>
    </tbody>
    </table>
    
    SCL しきい値の構成の詳細については、「[メールボックスにおけるスパム対策設定の構成](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md)」を参照してください。

## SCL しきい値の監視

**get-AntispamSCLHistogram.ps1** など `%ExchangeInstallPath%Scripts` フォルダーにあるいくつかの組み込みスクリプトを使用して、フィルター結果データを収集できます。直ちに調整する必要があるとデータが示している場合は、SCL のしきい値を再構成します。それ以外の場合は、データを収集してスパムのレポートを分析し、調整が必要かどうかを判断します。

