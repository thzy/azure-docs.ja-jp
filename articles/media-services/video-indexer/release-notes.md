---
title: Azure Media Services Video Indexer リリース ノート | Microsoft Docs
description: 常に最新の開発情報を把握していただけるよう、この記事では Azure Media Services Video Indexer の最新の更新情報を提供します。
services: media-services
documentationcenter: ''
author: Juliako
manager: femila
editor: ''
ms.service: media-services
ms.subservice: video-indexer
ms.workload: na
ms.topic: article
ms.date: 01/07/2020
ms.author: juliako
ms.openlocfilehash: 88effd58e807d39e5915aa41425ecf2e8ca8e3cc
ms.sourcegitcommit: f53cd24ca41e878b411d7787bd8aa911da4bc4ec
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75832306"
---
# <a name="azure-media-services-video-indexer-release-notes"></a>Azure Media Services Video Indexer リリース ノート

>URL `https://docs.microsoft.com/api/search/rss?search=%22Azure+Media+Services+Video+Indexer+release+notes%22&locale=en-us` をコピーして、お使いの RSS フィード リーダーに貼り付け、更新内容を確認するためにこのページに再度アクセスするタイミングに関する通知を受け取るようにしてください。

常に最新の開発情報を把握していただけるよう、この記事では以下に関する情報を提供します。

* 最新のリリース
* 既知の問題
* バグの修正
* 非推奨の機能

## <a name="december-2019"></a>2019 年 12 月

### <a name="update-transcript-with-the-new-api"></a>新しい API を使用して音声テキストを更新する

[Update-Video-Index](https://api-portal.videoindexer.ai/docs/services/Operations/operations/Update-Video-Index?&pattern=update) API を使用して、音声テキストの特定のセクションを更新します。

### <a name="fix-account-configuration-from-the-video-indexer-portal"></a>Video Indexer ポータルからアカウント構成を修正する

次のような問題を解決するために、Media Services 接続構成を更新できるようになりました。 

* Azure Media Services のリソースが正しくない
* パスワードの変更
* Media Services リソースがサブスクリプション間で移動された  

アカウント構成を修正するには、Video Indexer ポータルで、(所有者として) [設定] > [アカウント] タブの順に移動します。

### <a name="configure-the-custom-vision-account"></a>Custom Vision アカウントを構成する

Video Indexer ポータルを使用して、有料アカウントで Custom Vision アカウントを構成します (以前は API でのみサポートされていました)。 これを行うには、Video Indexer ポータルにサインインし、[モデルのカスタマイズ] > [アニメーション化されたキャラクター] > [構成] の順に選択します。 

### <a name="scenes-shots-and-keyframes--now-in-one-insight-pane"></a>シーン、ショット、キーフレーム - 1 つの分析情報ウィンドウに表示されるようになりました

シーン、ショット、およびキーフレームは、使用とナビゲーションを容易にするために 1 つの分析情報に結合されるようになりました。 目的のシーンを選択すると、そこに含まれるショットとキーフレームが表示されます。 

### <a name="notification-about-a-long-video-name"></a>長いビデオ名に関する通知

ビデオ名が 80 文字より長い場合、Video Indexer はアップロード時に状況を説明するエラーを表示します。

### <a name="streaming-endpoint-is-disabled-notification"></a>ストリーミング エンドポイントが無効になっているという通知

ストリーミング エンドポイントが無効になっている場合、Video Indexer には、プレーヤー ページに状況を説明するエラーが表示されます。

### <a name="error-handling-improvement"></a>エラー処理の改善

現在のインデックスの再作成の変更が誤って上書きされるのを防ぐために、ビデオにアクティブにインデックスが作成された場合は、[ビデオのインデックスを再作成](https://api-portal.videoindexer.ai/docs/services/Operations/operations/Re-Index-Video? https://api-portal.videoindexer.ai/docs/services/Operations/operations/Re-Index-Video?) API と[ビデオ インデックス](https://api-portal.videoindexer.ai/docs/services/Operations/operations/Update-Video-Index?) API から状態コード 409 が返されるようになりました。

## <a name="november-2019"></a>2019 年 11 月
 
* 韓国語のカスタム言語モデルのサポート

    Video Indexer では、API とポータルの両方で韓国語 (`ko-KR`) のカスタム言語モデルがサポートされるようになりました。 
* 音声テキスト変換 (STT) でサポートされる新しい言語

    Video Indexer API では、アラビア語 (レバント) (ar-SY)、英語 (英国) 言語 (en-GB)、および英語 (オーストラリア) 言語 (en-AU) の STT がサポートされるようになりました。
    
    動画のアップロードでは、zh-HANS が zh-CN に置き換えられています。どちらもサポートされていますが、zh-CN の方がより正確であるため、推奨されています。
    
## <a name="october-2019"></a>2019 年 10 月
 
* ギャラリーでアニメーション化された文字を検索する

    アニメーション化された文字のインデックスを作成すると、アカウントのビデオ ギャラリーで検索できるようになりました。 詳細については、[アニメーション化された文字の認識](animated-characters-recognition.md)に関する記事を参照してください。

## <a name="september-2019"></a>2019 年 9 月
 
IBC 2019 で発表されたさまざまな進化:
 
* アニメーション文字の認識 (パブリック プレビュー)

    Custom Vision との統合で、アニメーション コンテンツでグループを検出したり、文字を認識したりできるようになりました。 詳細については、「[アニメーション キャラクターの検出](animated-characters-recognition.md)」を参照してください。
* 複数言語の識別 (パブリック プレビュー)

    オーディオ トラックに含まれる複数の言語からセグメントを検出し、それに基づいて多言語のトランスクリプトを作成します。 初回サポート:英語、スペイン語、ドイツ語、フランス語。 詳細については、「[複数言語のコンテンツを自動的に識別および文字起こしする](multi-language-identification-transcription.md)」を参照してください。
* 人と場所に関して名前付きのエンティティを抽出する

    自然言語処理 (NLP) を使用して、音声および視覚テキストからブランド、場所、および人物を抽出します。
* 編集タイプでショットを分類する

    クローズアップ、ミディアムショット、ツーショット、屋内、屋外など、編集タイプでショットにタグを付けます。詳細については、「[編集ショット タイプの検出](scenes-shots-keyframes.md#editorial-shot-type-detection)」を参照してください。
* トピック推論の機能強化 - 現在のレベル 2
    
    トピック推論モデルでは、さらに細かな IPTC 分類に対応できるようになりました。 詳しくは、「[Azure Media Services の AI を活用した新たなイノベーション](https://azure.microsoft.com/blog/azure-media-services-new-ai-powered-innovation/)」をお読みください。

## <a name="august-2019"></a>2019 年 8 月
 
### <a name="video-indexer-deployed-in-uk-south"></a>英国南部でデプロイされる Video Indexer

Video Indexer 有料アカウントを英国南部リージョンで作成できるようになりました。

### <a name="new-editorial-shot-type-insights-available"></a>利用可能になった新しい編集ショット タイプ分析情報

ビデオ ショットに追加された新しいタグにより、コンテンツ作成ワークフローで使用される次のような一般的な編集語句を識別するための "ショット タイプ" が提供されます: 超クローズアップ、クローズアップ、ワイド、中程度、2 ショット、屋外、室内、左の顔、右の顔 (JSON で使用可能)。

### <a name="new-people-and-locations-entities-extraction-available"></a>利用可能になった新しい人と場所のエンティティ抽出

Video Indexer では、ビデオの OCR と文字起こしからの自然言語処理 (NLP) により、名前付きの場所と人が識別されます。 Video Indexer では、機械学習アルゴリズムを使用して、特定の場所 (エッフェル塔など) や人 (John Doe など) などのビデオでの言及が認識されます。

### <a name="keyframes-extraction-in-native-resolution"></a>ネイティブ解像度でのキーフレームの抽出

Video Indexer によって抽出されたキーフレームを、ビデオの元の解像度で使用できます。
 
### <a name="ga-for-training-custom-face-models-from-images"></a>GA になった画像からのカスタム顔モデルのトレーニング

画像からの顔のトレーニングが、プレビュー モードから GA になりました (API およびポータルで利用可能)。

> [!NOTE]
> "プレビューから GA" への移行に関連する価格への影響はありません。

### <a name="hide-gallery-toggle-option"></a>ギャラリー非表示の切り替えオプション

ユーザーは、ポータルからギャラリー タブを非表示にすることができます (サンプル タブの非表示と同様)。
 
### <a name="maximum-url-size-increased"></a>URL の最大サイズの拡大

ビデオのインデックス作成時にサポートされる URL クエリ文字列が (2048 文字ではなく) 4096 文字になります。
 
### <a name="support-for-multi-lingual-projects"></a>多言語プロジェクトのサポート

異なる言語でインデックス付けされた複数のビデオに基づいて、プロジェクトを作成できるようになりました (API のみ)。

## <a name="july-2019"></a>2019 年 7 月

### <a name="editor-as-a-widget"></a>ウィジェットとしてのエディター

Video Indexer AI エディターが、お客様のアプリケーションに埋め込むためのウィジェットとして提供されています。

### <a name="update-custom-language-model-from-closed-caption-file-from-the-portal"></a>ポータルでクローズド キャプション ファイルからカスタム言語モデルを更新する

お客様は、ポータルのカスタマイズ ページから、言語モデルの入力として VTT、SRT、TTML の各ファイル形式を指定できます。

## <a name="june-2019"></a>2019 年 6 月

### <a name="video-indexer-deployed-to-japan-east"></a>Video Indexer を東日本にデプロイ

Video Indexer 有料アカウントを東日本リージョンで作成できるようになりました。

### <a name="create-and-repair-account-api-preview"></a>アカウントの作成および修復 API (プレビュー)

[Azure Media Service の接続エンドポイントまたはキーを更新](https://api-portal.videoindexer.ai/docs/services/Operations/operations/Update-Paid-Account-Azure-Media-Services?&groupBy=tag)できる新しい API が追加されました。

### <a name="improve-error-handling-on-upload"></a>アップロードでのエラー処理の向上 

基になる Azure Media Services アカウントの構成に誤りがある場合には、説明のメッセージが返されます。

### <a name="player-timeline-keyframes-preview"></a>プレーヤー タイムラインのキーフレーム プレビュー 

プレーヤーのタイムライン上の各時間に対するイメージ プレビューを表示できるようになりました。

### <a name="editor-semi-select"></a>エディターの半選択

エディターで特定の分析情報期間を選択した結果として選択されるすべての分析情報のプレビューを表示できるようになりました。

## <a name="may-2019"></a>2019 年 5 月

### <a name="update-custom-language-model-from-closed-caption-file"></a>クローズド キャプション ファイルからのカスタム言語モデルの更新

[カスタム言語モデルの作成](https://api-portal.videoindexer.ai/docs/services/Operations/operations/Create-Language-Model?&groupBy=tag)および[カスタム言語モデルの更新](https://api-portal.videoindexer.ai/docs/services/Operations/operations/Update-Language-Model?&groupBy=tag) API は、言語モデルの入力として、VTT、SRT、および TTML ファイル形式をサポートするようになりました。

[ビデオ トランスクリプトの更新 API](https://api-portal.videoindexer.ai/docs/services/Operations/operations/Update-Video-Transcript?&pattern=transcript) を呼び出すと、トランスクリプトが自動的に追加されます。 ビデオに関連付けられたトレーニング モデルも自動的に更新されます。 使用する言語モデルをカスタマイズおよびトレーニングする方法については、「[Video Indexer で言語モデルをカスタマイズする](customize-language-model-overview.md)」を参照してください。

### <a name="new-download-transcript-formats--txt-and-csv"></a>新しいダウンロード トランスクリプト形式 – TXT と CSV

Video Indexer は、既にサポートされているクローズド キャプション形式 (SRT、VTT、TTML) に加えて、TXT および CSV 形式でのトランスクリプトのダウンロードをサポートするようになりました。

## <a name="next-steps"></a>次のステップ

[概要](video-indexer-overview.md)
