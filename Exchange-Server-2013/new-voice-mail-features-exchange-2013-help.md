﻿---
title: '新しいボイス メール機能: Exchange 2013 Help'
TOCTitle: 新しいボイス メール機能
ms:assetid: 89faaa97-3485-4704-a56c-d13632f01e2a
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ649002(v=EXCHG.150)
ms:contentKeyID: 49896349
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 新しいボイス メール機能

 

_**適用先:**Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:**2016-12-09_

Microsoft Exchange Server 2013 のユニファイド メッセージング (UM) は、いくつかの機能が拡張され、アーキテクチャが変更されていますが、含まれる機能は Exchange 2010 および Exchange 2007 と同じです。ただし、ユニファイド メッセージングは、独立したサーバーの役割ではなくなりました。Exchange 2013 では、提供される音声関連機能の 1 つのコンポーネントです。

## 音声アーキテクチャの変更

Exchange 2013 の音声アーキテクチャは、Exchange 2010 および Exchange 2007 のアーキテクチャとは異なっています。Exchange UM の以前のバージョンでは、ユニファイド メッセージングに関するすべてのコンポーネントは、インストールされた UM サーバーの役割を果たすサーバーに含まれていました。Exchange 2013 では、ユニファイド メッセージング コンポーネントは、Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスを実行するクライアント アクセス サーバーと Microsoft Exchange Unified Messaging Service を実行するメールボックス サーバーに分かれています。ユニファイド メッセージングのサービスやワーカー プロセスなど、ほとんどの機能は各メールボックス サーバーにあります。Microsoft Exchange ユニファイド メッセージング呼び出しルーター サービスを実行するクライアント アクセス サーバーは、着信呼び出しをメールボックス サーバーにプロキシ処理します。詳細については、「[ボイスのアーキテクチャの変更](voice-architecture-changes-exchange-2013-help.md)」を参照してください。

## IPv6 のサポート

インターネット プロトコル Version 6 (IPv6) は、インターネット プロトコル (IP) の最新バージョンです。IPv6 は、以前のバージョンの IP である IPv4 の多くの短所を取り除くことを目的としています。Exchange 2010 と同様に、Exchange 2013 のクライアント アクセス サーバーとメールボックス サーバーは、IPv6 ネットワークを完全にサポートします。詳細については、「[ユニファイド メッセージングでの IPv6 サポート](ipv6-support-in-unified-messaging-exchange-2013-help.md)」を参照してください。

## UCMA 4.0 API のサポート

Exchange 2010 Service Pack 1 (SP1) 以降、ユニファイド メッセージングの役割は、通知とメディアに関して Unified Communications Managed API v2.0 (UCMA) に依存していました。したがって、UCMA 2.0 は Exchange 2010 UM セットアップの前提条件でした。UCMA 2.0 は、管理者が別途ダウンロードし、Exchange 2010 SP1 以降のバージョンを実行する UM サーバーに手動で展開します。

ただし、UCMA 2.0 にはいくつかの制限があります。これらの多くの短所は、Exchange 2013 に必要な UCMA 4.0 では修正されています。現在、UM サーバーは独立したサーバーの役割ではなくなり、UCMA 4.0 を必要とするのはクライアント アクセス サーバーとメールボックス サーバーです。

UCMA 4.0 は、ユニファイド メッセージングの新機能 (音声合成 (TTS) と自動音声認識 (ASR) の両方に同じバージョンの音声合成エンジンを使用するなど) をサポートします。Exchange 2013 に使用されているプラットフォーム .NET 4.0 には、1 つのインストーラー ファイルが含まれており、Exchange 2010 および Exchange 2007 UM サーバーとの下位互換性を有効にします。

Exchange 2010 SP2 および SP1 の場合、ユニファイド メッセージング サーバーに service pack をインストールする前に UCMA 2.0 のインストールが必要です。

UCMA 4.0 を使用すると、次の利点が得られます。

  - 修正プログラムとパッチが組み込まれています。

  - IPv6 をサポートしています。

  - UCMA 4.0 の展開は自動化および簡略化されています。

  - UCMA 4.0 セットアップには、Exchange 2013 に関するすべての前提条件が含まれています。

  - UCMA 4.0 により、音声認識エンジンの変換がより正確になり、複数の製品間にわたってより拡張性の高い音声プラットフォームがサポートされます。


> [!NOTE]
> UCMA 4.0 は、Exchange 2013 をインストールする際にインストールされます。UCMA 4.0 とセットアップの要件の詳細については、「<A href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 の前提条件</A>」を参照してください。UCMA の最新バージョンにアップグレードするには、まずインストールした以前のバージョンの UCMA を [アプリケーションの追加と削除] を使用してアンインストールする必要があります。



## ボイス メールのプレビューの機能強化

音声エンジン 11.0 と UCMA 4.0 により、音声関連サービスに対するいくつかの機能拡張が Exchange Server 2013 UM に含まれています。文章校正の生成、コア音声サービス、および複数言語のサポートが向上しています。また、Exchange Server 2013 UM では、エンド ユーザーに配信されるトランスクリプション サービスのいくつかの機能が拡張され、ボイス メールのプレビューの信頼性と正確性も向上しました。詳細については、「[ボイス メール プレビューの拡張機能](voice-mail-preview-enhancements-exchange-2013-help.md)」を参照してください。

## 拡張された呼び出し ID のサポート

以前のリリースの Exchange ユニファイド メッセージングでは、呼び出しを受けた UM サーバーは、発信者の ID を使用して呼び出し元の可能性がある ID を検索していました。この検索は、メールボックスに格納された Active Directory および UM ユーザーの個人用連絡先にまで及びました。

以前、ユーザーはボイス メール システムが Exchange または個人用連絡先の呼び出し ID から連絡先を識別できないことに悩まされることがありました。これまで、この検索には、ユーザーの Exchange メールボックス内の既定の連絡先フォルダーのみが使用されていました。しかし、Exchange Server 2013 では、ユーザーの連絡先は、ユーザーが連絡先を整理する際に複数の一意のフォルダーに追加した外部ソーシャル ネットワークまたは連絡先から集約されている可能性があります。Exchange 2013 の UM では、手動で作成されたユーザーの他の Exchange および個人用連絡先フォルダーも対象にするように検索の範囲が拡張されます。さらに、Exchange 2013 では、外部ソーシャル ネットワークからの連絡先集約をサポートし、同じ個人を参照している複数の連絡先をリンクするインテリジェンスを提供し、そのデータを使用して個人中心 (連絡先中心でなく) のビューを提供します。つまり、外部ソーシャル ネットワークから集約される連絡先は、Microsoft Outlook Web App および Outlook のユーザーのメールボックスに格納されている連絡先フォルダーに配置することができます。これらの連絡先は、ユーザーが作成する追加の連絡先フォルダーにも追加することができます。

発信者の ID の参照は、連絡先の集合体に統合されているため、外部の連絡先も検索します。**PersonID** プロパティが存在して null 以外の値に設定されている場合、そのプロパティを使用して、同じ個人に関連付けられている連絡先への重複する一致を抑制することで、発信者 ID 解決のユーザー エクスペリエンスが向上します。PersonID プロパティはどちらの結果でも同じであるため、UM はこのプロパティを 1 つの連絡先に対する一致として処理します。

## 音声プラットフォームおよび音声認識の機能拡張

Exchange Server 2013 UM では、次の機能を含む、音声プラットフォームと音声認識に対するいくつかの機能拡張が導入されています。

  - ボイス メール プレビューに対する拡張機能と正確性の向上。

  - [Microsoft Speech Platform – Runtime (Version 11.0)](https://go.microsoft.com/fwlink/p/?linkid=253196) のサポート。

  - 組織のシステム メールボックスを使用した音声認識文章校正の生成。

Exchange ユニファイド メッセージングは、静的および動的な音声認識文章校正を使用して、コマンド、グローバル アドレス一覧 (GAL) 内の連絡先の名前、およびユーザーのメールボックス内の個人連絡先の名前を認識します。現在、Exchange Server 2013 では、Microsoft Exchange Unified Messaging service を実行するすべてのメールボックス サーバーが、サーバーにインストールされたすべての UM 言語の文章校正を生成し、ディレクトリに格納します。すべてのメールボックス サーバーは、ダイヤル プラン、自動応答、およびインストールされている UM 言語の数に基づいて生成したすべての実行可能な文章校正を格納します。

文章校正ファイルは UM によって使用され、発信者が音声を使用して組織内でユーザーを検索できるようにします。このファイルは、メールボックス アシスタントによって 24 時間ごとに更新されます。Exchange 2007 および Exchange 2010 の GGG.exe コマンドを使用すると、スケジュールされた更新を待たずに手動で文章校正ファイルを更新できます。Exchange Server 2013 では、UM の ASR 文章校正生成のスケーラビリティの問題に対応するために、ユニファイド メッセージング サーバーの役割がインストールされたサーバーで音声認識 GAL の文章校正生成が行われないようになりました。その代わりに、組織の調停メールボックスをホストする Microsoft Exchange Unified Messaging Service を実行するメールボックス サーバーで、メールボックス アシスタントを使用して定期的に文章校正を格納します。GAL 音声認識文章校正ファイルは、組織の調停メールボックスに格納され、後で Exchange 組織内のすべてのメールボックス サーバーにダウンロードされます。既定では、メールボックス アシスタントは、24 時間ごとに実行されます。実行の頻度は、**Set-MailboxServer** コマンドレットを使用して調整できます。

## コマンドレットの更新

Exchange 2013 では、UM コマンドレットの多くが Exchange 2010 から持ち越されています。しかし、これらコマンドレットの一部は変更されており、新機能用に新しいコマンドレットが追加されています。詳細については、「[ユニファイド メッセージングのコマンドレットの更新](unified-messaging-cmdlet-updates-exchange-2013-help.md)」を参照してください。

