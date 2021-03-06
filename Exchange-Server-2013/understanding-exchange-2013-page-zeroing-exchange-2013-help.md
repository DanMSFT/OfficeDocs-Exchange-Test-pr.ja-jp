﻿---
title: 'Exchange 2013 のページ解放について: Exchange 2013 Help'
TOCTitle: Exchange 2013 のページ解放について
ms:assetid: 0ca7b188-efbc-4c0d-bcfe-5138cffc803c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg549096(v=EXCHG.150)
ms:contentKeyID: 61633787
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 のページ解放について

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2016-12-09_

## Exchange 2013 のページ解放

*解放*とは、削除対象データにゼロかバイナリー パターンのどちらかを書き込んで削除対象データの回復をさらに困難にするセキュリティ メカニズムです。Exchange Server 2013 では、ESE データベースでそのストレージ単位としてページが使用されるため、*ページ解放*となります。ページ解放は既定で有効になっており、無効にすることはできません。ページの解放操作は、トランザクション ログ ファイルに記録されるため、データベースのすべてのコピーで同様にページが解放されます。アクティブなデータベース上でページを解放すると、データベースのパッシブ コピーが解放されます。


> [!NOTE]
> Extensible Storage Engine (ESE) には、新しい領域の割り当てに関して解放されたページの再利用の優先順位を付けるメカニズムはありません。シーケンシャルな領域割り当てが割り当てられているテーブルでは、新しいページまたは空きシーケンシャル ページの使用を優先して、断片化または解放されたページを意図的にスキップします。このアプローチでは、データベース IOP が削減されます。



Exchange 2013 のページ解放では、解放機能の実行中のサーバーに対するパフォーマンスの影響が軽減されます。これには、以下が含まれます。

  - **ストレージとネットワークの容量の最適化**   ESE は、ページ イメージ全体を記録する代わりに、ページ解放レコードをトランザクション ログ ファイルに書き込みます。このアプローチでは、ログ書き込み I/O が削減され、ログ ファイルを配布するための帯域幅要件が軽減されます。

  - **データベース ディスク I/O の最適化**   Exchange 2010 RTM 以前では、ページの解放は、バックアップ中またはスケジュールされた保守中にのみ実行され、大量のデータベース ディスク I/O が発生しました。Exchange 2010 SP1 以降 (Exchange 2013 を含む) では、ページの解放が既定で実行され、トランザクション時に行われるようになりました。多くの場合、物理的な削除の直後に解放が実行されます。この設計を使用すれば、データベースでエンジンのチェックポイントの深さ機能を利用して、ダーティ ページを一定期間データベース キャッシュ内に残すことができるため、短時間に発生する追加のページ更新による追加のデータベース書き込み I/O が発生しなくなります。この設計のお陰で、ページ解放はデータベース I/O にあまり影響しません。これが、ページ解放が既定で有効になっている理由です。

## ESE データベースでのページの解放の実装

ページ解放では、物理的に削除されたレコードにバイナリ パターンが上書きされます。ページ解放パターンは ESE エンジン操作に固有のもので、実行時操作と保守操作では異なります。次の表に、特定の実行時操作に対応したパターンを一覧表示します。

### ESE 実行時のページ解放の記述パターン

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>ESE 実行時操作</th>
<th>パターン</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>置換</p></td>
<td><p>R</p></td>
</tr>
<tr class="even">
<td><p>レコード/長い値の削除</p></td>
<td><p>D</p></td>
</tr>
<tr class="odd">
<td><p>解放されたページ領域</p></td>
<td><p>H</p></td>
</tr>
</tbody>
</table>


次の表は、ESE バックグラウンド データベース保守で実行される特定の操作に対応したパターンの一覧です。

### ESE バックグラウンド データベース保守中のページ解放の記述パターン

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>ESE バックグラウンド データベース保守操作</th>
<th>パターン</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>レコードの削除</p></td>
<td><p>D</p></td>
</tr>
<tr class="even">
<td><p>長い値の削除</p></td>
<td><p>L</p></td>
</tr>
<tr class="odd">
<td><p>部分的に使用されたページの解放されたページ領域</p></td>
<td><p>Z</p></td>
</tr>
<tr class="even">
<td><p>未使用ページの解放されたページ領域</p></td>
<td><p>U</p></td>
</tr>
</tbody>
</table>


## バックグラウンド データベース保守

バックグラウンド データベース保守は、すべてのデータベースのチェックサム計算とスキャンを連続的に実行するプロセスです。この主な機能は、データベース ページのチェックサム計算ですが、スペースのクリーンアップと、ストア クラッシュが原因でゼロに設定されなかったレコードとページの解放も処理します。バックグラウンド データベース保守では、データベースあたり毎秒約 1 MB が処理されます。タイムリーなページの解放が優先する場合、データベース サイズを減らして、クラッシュ回復事例に対してより短期間 (たとえば、24 時間) のうちにページを解放するようにできます。

バックグラウンド データベース保守は継続的なプロセスのため、その開始と完了に対して何のイベントも関連付けられていません。パフォーマンス カウンターの値を読み取ることによって、バックグラウンド データベース保守の進捗を追跡できます。

  - MSExchange Database -\> Instances -\> Database Maintenance Duration

このカウンターは、前回指定されたデータベースの保守が完了してから経過した秒数を示します。

## ESE データベース ページの解放のプロセス

次の表に、データベースの削除のシナリオ、およびページ解放機能が実行される時点について説明します。

### ESE バックグラウンド データベース保守

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>データベースの削除のシナリオ</th>
<th>データベース データを解放するための ESE プロセスと期間</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>シナリオ 1: 単一アイテムの回復が無効であり、ユーザーが回復可能なアイテム フォルダーからアイテムを削除します。</p></li>
<li><p>シナリオ 2: 単一アイテムの回復が無効であり、回復可能なアイテムの保存期間が 0 に設定されています。</p></li>
<li><p>シナリオ 3: 単一アイテムの回復が有効であり、削除済みアイテムの保存期間に基づいてアイテムの有効期限が決まります。</p></li>
</ul></td>
<td><p>非同期のスレッドは、バイナリ パターンを削除されたデータに上書きします。この操作はレコード削除の数ミリ秒以内に実行されます。非同期の解放作業がまだ終っていないうちに、ストア プロセスがクラッシュした場合 (またはバージョン ストアが増大したため、バージョン ストアのクリーンアップがキャンセルされた場合) は、バックグラウンド データベース保守でデータベースの該当するセクションが処理されたときに解放が完了します。</p></td>
</tr>
<tr class="even">
<td><p>ビューのシナリオ: Outlook/Outlook Web App フォルダー ビュー (スレッド ビューなど) のアイテムの有効期限</p></td>
<td><p>バックグラウンド データベース保守でデータベースのこのセクションが処理されたときに、データ解放が実行されます。</p></td>
</tr>
<tr class="odd">
<td><p>メールボックスの移動/メールボックスの削除のシナリオ: ソース メールボックスの削除 (メールボックスが収集から削除される期限)</p></td>
<td><p>バックグラウンド データベース保守でデータベースのこのセクションが処理されたときに、データ解放が実行されます。</p></td>
</tr>
</tbody>
</table>


## ページの解放動作を監視する

次の 2 つの ESE カウンターを表示することによって、ページ解放機能を評価または監視できます。

  - MSExchange Database-\>Database Maintenance Pages Zeroed:パフォーマンス カウンターの起動後に、データベース エンジンによって解放されたページ数を示します

  - MSExchange Database-\>Database Maintenance Pages Zeroed/sec:解放されたページの割合を示します。


> [!NOTE]
> これらのカウンターを有効にする方法については、「<A href="https://go.microsoft.com/fwlink/p/?linkid=101194">拡張された ESE パフォーマンス カウンタを有効にする方法</A>」を参照してください。



ページの解放はデータベース保守機能であるため、ランタイム トランザクション用のページの解放とバックグラウンド データベース保守によるページの解放の両方に関連するパフォーマンス情報がこれらのカウンターに含まれています。

## ページ解放を使用しないメールボックス データの種類

次のメールボックス データの種類にはページ解放機能がありません。

  - メールボックス データベース トランザクション ログ (.log)
    
    トランザクション ログを削除した場合 (バックアップまたは循環ログによる切り詰めのため)、削除されたログ ファイルを保存している NTFS ファイル システム内のブロックを解放するプロセスはありません。NTFS が新たに作成されるログ用にこの空き領域をすぐ再活用する可能性もありますが、その保証はありません。

  - コンテンツ インデックス カタログ ファイル
    
    Exchange 2013 では、検索インデックス処理機能に Search Foundation が使用されます。検索インデックス カタログは、メールボックス データベース ファイルと同じボリュームに格納されている数十のファイルから構成されています。メッセージがメールボックス データベースから物理的に削除されても、検索カタログ内の関連付けられているコンテンツはすぐには削除されません。コンテンツの削除が行われるのは、Search Foundation が多数の小さなカタログ ファイルを単一のより大きなファイルにシャドウ結合またはマスター結合するときです。マスター結合が完了すると、小さいカタログ ファイルが削除されます。削除されたカタログ ファイルを保存しているブロックを解放するプロセスはありません。

