﻿---
title: 'ユーザーがボイス メールのトランスクリプトを表示できるようにする: Exchange Online Help'
TOCTitle: ユーザーがボイス メールのトランスクリプトを表示できるようにする
ms:assetid: c5192e05-905c-440f-beec-1f697edc15b3
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Ff629381(v=EXCHG.150)
ms:contentKeyID: 51407572
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ユーザーがボイス メールのトランスクリプトを表示できるようにする

 

_**適用先:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

ボイス メール プレビューは、ユニファイド メッセージング (UM) からボイス メール メッセージを受信する際に使用できる機能です。ボイス メール プレビューによって録音をテキスト形式にできるようになり、既存の UM ボイス メールの機能が向上しました。ボイス メール テキストは、MicrosoftOutlook Web App、Outlook 2010 およびそれ以降のバージョン、およびサポートされるその他の電子メール プログラムの電子メール メッセージに表示されます。詳細については、「[Microsoft の音声認識技術](http://go.microsoft.com/fwlink/p/?linkid=187348)」を参照してください。

## 特定の電子メール プログラムを使用する必要がありますか?

いいえ。ボイス メール プレビューは、モバイル プログラムなどすべての電子メール プログラムのメッセージ本文のテキストに含まれます。他の電子メール プログラムを使用して音声メッセージを受信することもできますが、Outlook と Outlook Web App の方が便利です。たとえば Outlook 2010 以降のバージョンの場合、ボイス メール プレビュー テキストの特定の単語をクリックすると、その単語から音声メッセージのオーディオ再生が開始されます。これは、音声メッセージの特定の部分を聞く場合に便利です。

## 特定のボイス メール メッセージを検索できますか?

はい。ボイス メール プレビュー テキストの単語と語句は自動的にインデックス化されるため、音声メッセージが検索結果に表示されます。Outlook 2010 以降のバージョンや Outlook Web App では、**\[オーディオ ノート\]** ボックスを使用して音声メッセージに関するテキストを追加することもできます。これらのメモは検索にも含まれるため、メッセージを簡単に見つけることができます。

## この機能が "ボイス メール プレビュー" と呼ばれるのはなぜですか?

ユーザーの期待に見あう表現をすることは重要です。ボイス メール プレビューでは、必ずしも発信者の音声メッセージと同じテキストが生成されるわけではありません。実際には不正確な点がよく見られます。トランスクリプションと呼ぶためには、より正確である必要があります。プレビューという言葉は、メッセージを読む人が音声の主旨を理解できるということを意味します。この呼び方が、この機能の実際の性能に近いものです。

## ボイス メール プレビュー テキストの正確性に影響を与える要因は何でしょうか?

ボイス メール プレビュー テキストの正確性は多くの要素によって決まるものであり、これらの要素を制御できない場合もあります。ただし、次のような場合はボイス メール プレビュー テキストの正確性が向上する可能性が高くなります。

  - 発信者がスラング、技術的な専門用語、一般的でない単語や語句などを含まない簡単な音声メッセージを残した場合。

  - 発信者が、ボイス メール システムによって容易に認識および変換される言語を使用している。一般的に、発信者の話し方が早すぎず、声が小さすぎず、強いなまりがなければ、残された音声メッセージから、より正確な文や語句が生成されます。

  - 音声メッセージにバックグラウンド ノイズやエコーが含まれておらず、音声の欠落がない場合。

## ボイス メール プレビューではどの言語を使用できますか?

ボイス メール プレビュー テキストは、次の言語で使用できます。

  - 英語 (米国) (en-US)

  - 英語 (カナダ) (en-CA)

  - フランス語 (フランス) (fr-FR)

  - イタリア語 (it-IT)

  - ポーランド語 (pl-PL)

  - ポルトガル語 (ポルトガル) (pt-PT)

  - スペイン語 (スペイン) (es-ES)

社内展開またはハイブリッド展開の UM を導入している場合は、UM 言語パックを [Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/?linkid=266542)からダウンロードできます。

社内展開またはハイブリッド展開をしている場合、UM 言語パックをインストールすると、ダイヤル プランおよび自動応答を選択した言語で構成できるようになります。オンラインのお客様は、UM 言語パックをインストールする必要はありません。多くの企業で、UM ダイヤル プランは 1 つだけです。UM は既定のダイヤル プラン言語でボイス メール プレビューを作成しようとしますが、既定の言語がボイス メール プレビューをサポートしていない場合は作成に失敗します。UM ダイヤル プランでボイス メール プレビューの作成を構成できるのは、一度に 1 つの言語のみです。

en-US 以外の言語でボイス メール プレビューを使用できるよう UM を構成する場合は、以下の手順に従ってください。

1.  使用する言語でボイス メール プレビューがサポートされていることを確認します。

2.  社内展開またはハイブリッド展開を行っている場合は、適切な UM 言語パックをダウンロードしてからインストールします。言語パックをダウンロードしてインストールしても、ダイヤル プランの既定言語は構成されません。

3.  ボイス メール プレビューで使用する言語でダイヤル プランを構成します。詳細については、「[ダイヤル プランの既定言語を設定する](set-the-default-language-on-a-dial-plan-exchange-2013-help.md)」を参照してください。

ボイス メール プレビューにより、サポートされている言語でテキストを表示する方法は、送信される音声メッセージの種類によって異なります。次の 2 種類があります。

  - **ユーザーが電話に応答しない場合に録音される音声メッセージ**
    
    これらのメッセージに関して、どの言語がボイス メール プレビューで使用されるかは、発信者が使用する言語とその言語がサポートされているかどうかによって決まります。たとえば、発信者がイタリア語で音声メッセージを残した場合、ダイヤル プランでイタリア語が構成されていれば、ボイス メール プレビュー テキストがイタリア語で表示されます。ただし発信者が日本語でメッセージを残した場合、日本語は使用できないため、メッセージにボイス メール プレビュー テキストは含まれません。

  - **Outlook Voice Access ユーザーが送信する音声メッセージ**
    
    Outlook Voice Access のユーザーによって送信されたメッセージの場合、ボイス メール プレビューに使用される言語は、ボイス メールの管理者によって決定されます。そのため、ボイス メールのプレビュー テキストはボイス メール システムと同じ言語になります。ただし、ボイス メール プレビューでサポートされていない言語を話す発信者が Outlook Voice Access を使用してメッセージを残した場合、ボイス メール プレビュー テキストはメッセージに含まれません。Outlook Voice Access の詳細については、「[Outlook Voice Access の設定](setting-up-outlook-voice-access-exchange-2013-help.md)」を参照してください。

## UM はボイス メール プレビューの正確性を認識していますか?

音声メッセージに含まれるボイス メール プレビューごとに信頼レベルが判定されています。ボイス メール システムでは、録音の音声が単語、数、および語句と一致するかどうかが測定されます。簡単に一致した場合は、信頼レベルは高くなります。通常は、信頼レベルが高いほど正確です。

信頼レベルが一定の値より低いと判定された場合は、ボイス メール プレビュー テキストの上に **\[ボイス メール プレビュー (精度: 低)\]** という語句が追加されます。信頼レベルが低い場合は、ボイス メール プレビュー テキストが正確でない可能性が高くなります。

ユニファイド メッセージングでは、自動音声認識 (ASR) を使用してプレビューの信頼性を計算していますが、単語の正誤を判定する方法はありません。

しかし、UM ではボイス メール プレビューの正確性を向上させようとしており、たとえば、発信者の電話番号 (利用可能な場合) を、ユーザーの個人用連絡先や組織のアドレス帳、ソーシャル ネットワークの連絡先と照合しようとします。UM で一致が検出されると、録音音声に対して ASR を実行する際に使用される標準の名前と単語のリストに、発信者の名前が追加されます。

## ボイス メール プレビューは完全に正確でなくても使用できますか?

ボイス メール プレビューの場合、プレビューを丁寧に一語ずつ読もうとしない方が良いかもしれません。代わりに、名前、電話番号、および "お電話ください" や "お話があります" など、電話した目的がわかる語句を探すようにしてください。

ボイス メール プレビューは、メッセージを正確に書き取ったものではありませんが、次のような内容について判断することはできます。

  - この音声メッセージは自分の仕事に関係あるか。

  - この音声メッセージは重要か。

  - 発信者は電話番号を残しているか。その番号は、手元にある発信者の番号とは別のものであるか。

  - この音声メッセージは発信者にとって緊急のものか。

  - 会議を退出して発信者に電話をかける必要があるか。

  - 依頼を確認する電話を待っていたが、これがその確認電話であるか。

## ボイス メール プレビューのオンとオフを切り替えることができますか?

はい。ボイス メール プレビューが有効になっている場合、ユーザーは Outlook 2010 またはそれ以降のバージョン、あるいは Outlook Web App を使用してボイス メール プレビューのオンとオフを切り替えることができます。ただし、ダイヤル プラン言語でボイス メール プレビューがサポートされており、その言語の UM 言語パックがインストールされている必要があります。

ボイス メール プレビューの設定は Outlook 2010 またはそれ以降のバージョン、あるいは Outlook Web App のどちらを使用している場合でも同じですが、アクセス方法は異なります。

**Outlook Web App**

Outlook Web App でボイス メール プレビューの設定にアクセスするには、**\[設定\]** \> **\[電話\]** \> **\[ボイス メール\]** の順にクリックします。設定は、**\[ボイス メール\]** ページの **\[ボイス メール プレビュー\]** で行うことができます。

既定では、ユニファイド メッセージングが利用可能な場合、ボイス メール プレビューのオプションは両方とも有効になります。UM ダイヤル プランがボイス メール プレビューをサポートする UM 言語パックを使用するように構成されていると、次のような場合にユニファイド メッセージングによってユーザーのボイス メール プレビューが作成されます。

  - ユーザーが電話に応答せず、発信者がボイス メール メッセージを残した場合。

  - UM が有効なユーザーが Outlook Voice Access にサインインし、1 人または複数の受信者への音声メッセージを録音した場合。

発信者が音声メッセージを残し、**\[受信した音声メッセージのプレビュー テキストを含める\]** がオンになっていると、電子メール メッセージにボイス メール プレビューが作成され、添付のオーディオ ファイルが受信者のメールボックスに送信されます。ダイヤル プランで構成されている言語でボイス メール プレビューがサポートされていなかったり、ボイス メール プレビューをボイス メール メッセージに入れたくない場合は、このオプションを無効にできます。

ユーザーが Outlook Voice Access にサインインして他のユーザーに音声メッセージを送信する場合は、**\[Outlook Voice Access で送信する音声メッセージにプレビュー テキストを含める\]** チェックボックスをオフにすることもできます。たとえば、ボイス メール プレビューがサポートしていない言語で音声メッセージを送る場合や、メッセージが長すぎるためにボイス メール プレビューを音声メッセージに含めたくない場合などに、この設定を適用します。

