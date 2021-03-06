---
title: コマーシャル マーケットプレースの課金 | Azure Marketplace
description: この記事では、コマーシャル マーケットプレースでの商取引に関連したトピックについて説明します。
author: MaggiePucciEvans
manager: evansma
ms.author: evansma
ms.service: marketplace
ms.topic: guide
ms.date: 12/12/2019
ms.openlocfilehash: a483f143b70a4969114c078b3b0a6f960c4b6b41
ms.sourcegitcommit: 3dc1a23a7570552f0d1cc2ffdfb915ea871e257c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/15/2020
ms.locfileid: "75976071"
---
# <a name="commercial-marketplace-billing"></a>コマーシャル マーケットプレースの課金

この記事では、コマーシャル マーケットプレースでの商取引に関連したトピックについて説明します。

- [Marketplace 公開オプション](#marketplace-publishing-options)
- [販売の概要](#transact-general-overview)
- [販売の課金モデル](#transact-billing-models)

## <a name="marketplace-publishing-options"></a>Marketplace 公開オプション

コマーシャル マーケットプレースでは、公開元に対して複数の公開オプションが用意されています。

### <a name="list-and-trial-publishing-options"></a>リストと試用版の公開オプション

公開元は、リスト、試用版、およびライセンス持ち込み (BYOL) の公開オプションをキャンペーンとユーザー獲得の目的に活用できます。 これらのオプションでは、Microsoft は公開元のソフトウェア ライセンス トランザクションに直接関与しません。また、関連付けられているトランザクション料金はありません。 ソフトウェア ライセンス トランザクションのすべての側面 (受注、調達、使用状況測定、課金、請求、支払い、収集を含むが、これらに限定されない) について、公開元がサポートを担当します。 リストと試用版の公開オプションを使用する場合、お客様から収集された公開元ソフトウェア ライセンス料金の 100% を公開元が受け取ります。

### <a name="transact-publishing-option"></a>取引の公開オプション

リストと試用版の公開オプションに加えて、公開元は取引の公開オプションを使用できます。 このオプションでは、Microsoft のグローバルに使用可能なコマース機能を利用し、公開元に代わって Microsoft がクラウド マーケットプレース上のトランザクションをホストできるようになります。

## <a name="transact-general-overview"></a>販売の概要

取引の公開オプションを使用する場合、Microsoft は、顧客の Azure サブスクリプションに対して、サード パーティ製ソフトウェアの販売と、特定の種類のオファーのデプロイを有効にします。 公開元は、課金モデルとオファーの種類を選択するときに、インフラストラクチャ料金の課金と、公開元自身のソフトウェア ライセンス料金を考慮する必要があります。

取引の公開オプションは、次のオファーの種類に対して現在サポートされています: 仮想マシン、Azure アプリケーション、SaaS アプリ。

![Azure Marketplace での取引](./media/transact-amp.png)

### <a name="billing-infrastructure-costs"></a>インフラストラクチャ コストの課金

#### <a name="for-virtual-machines-and-azure-applications"></a>仮想マシンと Azure アプリケーションの場合

仮想マシンと Azure アプリケーションでは、Azure インフラストラクチャの使用料金は、顧客の Azure サブスクリプションに対して課金されます。 インフラストラクチャの使用料は、顧客の請求書上にソフトウェア プロバイダーのライセンス料金とは別に価格が設定され、提示されます。

#### <a name="for-saas-apps"></a>SaaS アプリの場合

SaaS アプリの場合、公開元は Azure インフラストラクチャの使用料金とソフトウェアのライセンス料金を 1 つのコスト項目として処理する必要があります。 これは定額料金として顧客に提示されます。 Azure インフラストラクチャの使用量は、パートナーが直接管理し、パートナーに直接課金されます。 実際のインフラストラクチャの使用料金は、顧客には提示されません。 公開元は、Azure インフラストラクチャの使用料金をソフトウェア ライセンス料金にバンドルするように選択することが一般的です。 ソフトウェア ライセンス料金は従量制ではなく、消費量ベースでもありません。

## <a name="transact-billing-models"></a>販売の課金モデル

使用されるトランザクション オプションによって、公開元のソフトウェア ライセンス料金は次のように提示されます。

- *Free*:ソフトウェア ライセンスに対する課金は発生しません。
- "*ライセンス持ち込み (BYOL)* ": ソフトウェア ライセンスに適用される料金は、公開元とお客様の間で直接管理されます。 Microsoft は、Azure インフラストラクチャの使用料金のみを管理します。 (仮想マシンと Azure アプリケーションのみ。)
- *従量課金制*: ソフトウェア ライセンス料金は、使用されている Azure インフラストラクチャに基づいて、時間あたりのコア (vCPU) ごとの価格レートとして提示されます。 このモデルは仮想マシンと Azure アプリケーションのみに適用されます。
- "*サブスクリプションの料金*": ソフトウェア ライセンス料金は、定額またはシートごとに課金された毎月または毎年の基本料金として提示されます。 このモデルは、SaaS アプリと Azure アプリケーション - マネージド アプリのみに適用されます。
- "*無料試用版ソフトウェア*":30 日または 90 日間のソフトウェア ライセンスに対する課金は発生しません。

### <a name="free-and-bring-your-own-license-byol-pricing"></a>無料とライセンス持ち込み (BYOL) の価格

トランザクションの無料またはライセンス持ち込みのトランザクション オファーを公開するとき、ご自身のソフトウェア ライセンス料金について、Microsoft が販売トランザクションを促進する役割を果たすことはありません。 リストと試用版の公開オプションと同様に、ソフトウェア ライセンス料金の 100% を公開元が受け取ります。

### <a name="pay-as-you-go-and-subscription-site-based-pricing"></a>従量課金制とサブスクリプション (サイトベース) の価格

従量課金制またはサブスクリプションによるトランザクション オファーを公開する場合、Microsoft によって、ソフトウェア ライセンスの購入、返却、チャージバックを処理するためのテクノロジとサービスが提供されます。 このシナリオでは、公開元はこれらの目的のために Microsoft が代理として機能することを承認します。 公開元は Microsoft がソフトウェア ライセンス トランザクションを促進することを許可する一方、販売者、プロバイダー、ディストリビューター、ライセンサーとして指定された立場を維持します。

Microsoft は、顧客が公開元のソフトウェアを注文し、ライセンスを取得して使用できるようにします。ただし、その使用には Microsoft の Commercial Marketplace と公開元の使用許諾契約の両方の条件が適用されます。 公開元は、オファーを作成するときに自身の使用許諾契約を用意するか、または[標準契約](https://docs.microsoft.com/azure/marketplace/standard-contract)を選択する必要があります。

### <a name="free-software-trials"></a>無料のソフトウェア試用版

販売の公開シナリオの場合、公開元はソフトウェア ライセンスを 30 日または 90 日間無料で使用できるようにすることができます。 この割引の範囲に、パートナー ソリューションを使用することによって発生する Azure インフラストラクチャの使用コストは含まれません。

### <a name="private-offers"></a>プライベート オファー

オファーを収益化するためのオファーの種類と課金モデルを使用する以外にも、公開元は、交渉済みの取引固有の価格またはカスタム構成を持つプライベート オファーを販売できます。 プライベート オファーは、3 つの取引の公開オプションのすべてによってサポートされています。

このオプションにより、公開されているオファリングより高いか、または低い価格設定が可能になります。 プライベート オファーは、あるオファーに対する割引または特典を追加するために使用することもできます。 プライベート オファーは、単一または複数の顧客の Azure サブスクリプションをオファー レベルのホワイトリストに追加することによって、それらの顧客に対して使用可能にすることができます。

### <a name="examples"></a>例

#### <a name="pay-as-you-go"></a>従量課金制

* 従量課金制オプションを有効にした場合、コスト構造は次のようになります。

|ライセンス コスト  | 1\.00 ドル/時間  |
|---------|---------|
|Azure 使用コスト (D1/1 コア)    |   0\.14 ドル/時間     |
|*顧客は Microsoft から請求されます*    |  *1.14 ドル/時間*       |

* このシナリオでは、Microsoft は公開された VM イメージの使用に対して 1 時間あたり 1.14 ドルを請求します。

|Microsoft からの請求額  | 1\.14 ドル/時間  |
|---------|---------|
|Microsoft は、ライセンス コストの 80% をパブリッシャーに支払います|   0\.80 ドル/時間     |
|Microsoft は、ライセンス コストの 20% を受け取ります  |  0\.20 ドル/時間       |
|Microsoft は、Azure 使用コストの 100% を受け取ります | 0\.14 ドル/時間 |

### <a name="bring-your-own-license-byol"></a>ライセンス持ち込み (BYOL)

* BYOL オプションを有効にした場合、コスト構造は次のようになります。

|ライセンス コスト  | ライセンス料金は公開元によって交渉および請求されます  |
|---------|---------|
|Azure 使用コスト (D1/1 コア)    |   0\.14 ドル/時間     |
|*顧客は Microsoft から請求されます*    |  *0.14 ドル/時間*       |

* このシナリオでは、Microsoft は公開された VM イメージの使用に対して 1 時間あたり 0.14 ドルを請求します。

|Microsoft からの請求額  | 0\.14 ドル/時間  |
|---------|---------|
|Microsoft は、Azure の使用コストを受け取ります    |   0\.14 ドル/時間     |
|Microsoft は、ライセンス コストの 0% を受け取ります   |  0\.00 ドル/時間       |

### <a name="saas-app-subscription"></a>SaaS アプリ サブスクリプション

このオプションは、Microsoft 経由で販売するように構成する必要があり、月単位または年単位で定額またはユーザーごとに価格を設定できます。

• SaaS オファーに対して Microsoft 経由で販売するオプションを有効にした場合、コスト構造は次のようになります。

|ライセンス コスト       | 1 か月あたり $100.00  |
|--------------|---------|
|Azure 使用コスト (D1/1 コア)    | 顧客ではなく公開元に直接課金されます |
|*顧客は Microsoft から請求されます*    |  *1 か月あたり $100.00 (注: 公開元は、ライセンス料金の中で、発生したパススルー インフラストラクチャ コストを考慮する必要があります)*  |

* このシナリオでは、Microsoft はソフトウェア ライセンスに $100.00 を課金し、公開元に $80.00 を支払います。
* Marketplace サービス手数料減額の対象となっているパートナーは、2019 年 5 月から 2020 年 6 月まで、SaaS オファーに対するトランザクション料金の減額が表示されます。 このシナリオでは、Microsoft はソフトウェア ライセンスに $100.00 を課金し、公開元に $90.00 を支払います。

|Microsoft からの請求額  | 1 か月あたり $100.00  |
|---------|---------|
|Microsoft は、ライセンス コストの 80% をパブリッシャーに支払います <br> \* Microsoft は、すべての対象となる SaaS アプリのライセンス コストの 90% を支払います   |   1 か月あたり $80.00 <br> \* 1 か月あたり $90.00    |
|Microsoft は、ライセンス コストの 20% を受け取ります <br> \* Microsoft は、すべての対象となる SaaS アプリのライセンス コストの 10% を受け取ります。  |  1 か月あたり $20.00 <br> \* $10.00     |

**Marketplace サービス料金の減額:** 自身の Commercial Marketplace で公開する特定の SaaS 製品の場合、Microsoft は、Marketplace サービス料金を 20% から 10% に減額します (Microsoft 発行元契約の説明に従う)。  製品が対象となるには、少なくとも 1 つの製品を、IP 共同販売準備完了または IP 共同販売優先のどちらかとして、マイクロソフトが指定する必要があります。 その月の Marketplace サービス料金の減額を受け取るには、前のカレンダー月の月末までに少なくとも 5 営業日適格性を満たす必要があります。 Marketplace サービス料金の減額は、VM、マネージド アプリ、または Commercial Marketplace から入手できる他の製品には適用されません。  Marketplace サービス料金の減額は、対象となるオファーと、2019 年 5 月 1日から 2020 年 6 月 30日までにマイクロソフトが収集したライセンス料金に利用できます。  その後は、Marketplace サービス料金は通常の金額に戻ります。
