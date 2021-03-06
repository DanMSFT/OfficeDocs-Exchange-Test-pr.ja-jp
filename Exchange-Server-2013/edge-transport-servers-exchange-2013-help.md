﻿---
title: 'エッジ トランスポート サーバー: Exchange 2013 Help'
TOCTitle: エッジ トランスポート サーバー
ms:assetid: cfff9f59-afac-447c-8297-afcebe49a52d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb124701(v=EXCHG.150)
ms:contentKeyID: 61180563
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# エッジ トランスポート サーバー

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2016-09-29_

エッジ トランスポート サーバーは、インターネットに直接接続されたすべてのメール フローを処理することにより、攻撃の範囲を最小限にします。これにより、Exchange 組織に SMTP (簡易メール転送プロトコル) 中継およびスマート ホスト サービスが提供されます。エッジ トランスポート サーバーで実行されるエージェントによって、メッセージ保護とセキュリティの追加の層が提供されます。これらのエージェントでは、スパムに対する保護を提供し、メール フローを制御するトランスポート ルールを適用します。

エッジ トランスポート サーバーは境界ネットワーク内にインストールされるので、組織の内部 Active Directory フォレストのメンバーになることはなく、Active Directory 情報へのアクセス権がありません。しかし、エッジ トランスポート サーバーでは Active Directory に存在するデータが必要になります。たとえば、メール フローにはコネクタ情報が必要で、スパム対策の受信者参照タスクには受信者情報が必要です。このデータは、Microsoft Exchange EdgeSync サービス (EdgeSync) によって、エッジ トランスポート サーバーと同期されます。EdgeSync は、Active Directory からエッジ トランスポート サーバー上の Active Directory ライトウェイト ディレクトリ サービス (AD LDS) インスタンスに受信者および構成情報の一方向のレプリケーションを確立するために、Exchange 2013 メールボックス サーバー上で実行されるプロセスの集合です。EdgeSync がコピーするのは、エッジ トランスポート サーバーがスパム対策構成タスクを実行するために必要な情報、およびエンド ツー エンドのメール フローを可能にするために必要な情報だけです。EdgeSync は、AD LDS の情報が最新の状態に維持されるように、スケジュールされた更新を実行します。

境界ネットワークには複数のエッジ トランスポート サーバーをインストールできます。エッジ トランスポート サーバーを複数展開すると、受信メッセージ フローに冗長性およびフェールオーバーの機能が提供されます。メール ドメインの MX レコードを同じ優先順位値で複数定義することで、組織に対する SMTP トラフィックを複数のエッジ トランスポート サーバー間で負荷分散することができます。複製した構成スクリプトを使用して、複数のエッジ トランスポート サーバー間での構成の一貫性を確立できます。

エッジ トランスポート サーバーの役割で、以下のメッセージ処理のシナリオを管理できます。

## インターネット メール フロー

エッジ トランスポート サーバーは、インターネットから Exchange 組織に入ってくるメッセージを受け付けます。エッジ トランスポート サーバーで処理された後、それらのメッセージが次にどこにルーティングされるかは、内部 Exchange サーバーの構成によって以下のように異なります。

  - クライアント アクセス サーバーとメールボックス サーバーが別々のコンピューターにインストールされている場合は、メールはメールボックス サーバー上のトランスポート サービスにルーティングされます。受信 SMTP メール フローは、クライアント アクセス サーバーを迂回します。

  - クライアント アクセス サーバーとメールボックス サーバーが同じコンピューターにインストールされている場合は、メールはクライアント アクセス サーバー上のフロント エンド トランスポート サービスにルーティングされてから、メールボックス サーバー上のトランスポート サービスにルーティングされます。

インターネット宛てに組織内から送信されるすべてのメッセージは、メールボックス サーバー上のトランスポート サービスによって処理された後で、エッジ トランスポート サーバーにルーティングされます。エッジ トランスポート サーバーは、外部 SMTP ドメイン用の MX リソース レコードを DNS で解決するように構成するか、DNS 解決のためにスマート ホストにメッセージを転送するように構成できます。

## スパム対策

Exchange 2013 では、スパム対策の機能により、不要な商用電子メール (スパム) をネットワーク境界でブロックするサービスが提供されます。

スパムの発信者は、さまざまな手法を使用して組織にスパムを送信します。エッジ トランスポート サーバーは、複数の層でスパムのフィルター処理と保護を提供するために連携して動作する一連のエージェントを備えているため、ユーザーがスパムを受信しないようにすることができます。コネクタでタールピット間隔を確立すると、電子メール アドレス収集の試行の効率が悪くなります。

## エッジ トランスポート ルール

エッジ トランスポート ルールは、インターネットとの間で送受信されるメッセージ フローを制御するために使用されます。エッジ トランスポート ルールは、各エッジ トランスポート サーバー上で構成され、指定された条件に一致するメッセージにアクションを適用することによって、企業ネットワークのリソースとデータを保護するために役立ちます。エッジ トランスポート ルールの条件は各データ、たとえば、メッセージの件名、本文、ヘッダー、または送信元アドレスに含まれている特定の単語またはテキスト パターン、SCL (Spam Confidence Level)、添付ファイルの種類などに基づきます。指定された条件に当てはまる場合のメッセージの処理方法はアクションによって決まります。可能なアクションには、メッセージの検疫、メッセージの破棄または拒否、他の受信者の追加、イベントのログ出力などがあります。オプションの例外は、特定のメッセージをアクションの適用対象外にします。

## アドレスの書き換え

アドレスを書き換えると、外部の受信者向けに、電子メール アドレスの外観に一貫性をもたせることができます。受信および送信メッセージ上の SMTP アドレスを変更するように、アドレスの書き換えをエッジ トランスポート サーバー上で構成します。アドレス書き換えは、新しく合併した組織で電子メール アドレスの外観に一貫性をもたせる場合に特に役立ちます。

アドレス書き換えの詳細については、「[エッジ トランスポート サーバー上でのアドレス書き換え](address-rewriting-on-edge-transport-servers-exchange-2013-help.md)」を参照してください。

