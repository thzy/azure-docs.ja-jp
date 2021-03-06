---
title: Azure Kubernetes Service でサポートされている Kubernetes のバージョン
description: Azure Kubernetes Service (AKS) の Kubernetes バージョン サポート ポリシーとクラスターのライフサイクルを理解する
services: container-service
author: sauryadas
ms.service: container-service
ms.topic: article
ms.date: 12/09/2019
ms.author: saudas
ms.openlocfilehash: bba4196547bda3d3ddcf3344032de5b9286639a0
ms.sourcegitcommit: d614a9fc1cc044ff8ba898297aad638858504efa
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74996750"
---
# <a name="supported-kubernetes-versions-in-azure-kubernetes-service-aks"></a>Azure Kubernetes Service (AKS) でサポートされている Kubernetes のバージョン

Kubernetes コミュニティでは、おおよそ 3 か月おきにマイナー バージョンをリリースしています。 これらのリリースには、新しい機能と機能強化が含まれます。 修正プログラムのリリースは、より頻繁で (場合によっては毎週)、マイナー バージョンでの重要なバグ修正のみを目的としています。 これらの修正プログラム リリースには、セキュリティの脆弱性や、多くの顧客や Kubernetes に基づく運用環境で実行されている製品に影響を与える主なバグの修正プログラムが含まれます。

AKS は、リリースの安定性によって異なりますが、アップストリーム リリースから 30 日以内に Kubernetes の新しいバージョンを認証およびリリースすることを目標としています。

## <a name="kubernetes-versions"></a>Kubernetes のバージョン

Kubernetes は、標準の[セマンティック バージョニング](https://semver.org/)のバージョン管理スキームを使用します。 これは、Kubernetes の各バージョンがこの番号付け方式に従うことを意味します。

```
[major].[minor].[patch]

Example:
  1.12.14
  1.12.15
```

バージョンのそれぞれの数字は、前のバージョンとの一般的な互換性を示します。

* メジャー バージョンは、互換性のない API の変更や下位互換性が破棄されている可能性があるときに変更されます。
* マイナー バージョンは、その他のマイナー リリースに対する下位互換性のある機能の変更が行われたときに変更されます。
* 修正プログラムのバージョンは、下位互換性のあるバグ修正が行われたときに変更されます。

ユーザーは、実行中のマイナー バージョンの最新の修正プログラムのリリースを実行するよう努める必要があります。たとえば、運用環境クラスターが *1.12.14* 上にあり、*1.12.15* が *1.12* シリーズ用に使用できる最新の使用可能な修正プログラムのバージョンである場合は、クラスターに完全にパッチが適用されサポートされていることを確認できるようになったらすぐに *1.12.15* にアップグレードする必要があります。

## <a name="kubernetes-version-support-policy"></a>Kubernetes バージョン サポート ポリシー

AKS では、Kubernetes の 3 つのマイナー バージョンがサポートされています。

* AKS (N) でリリースされている現在のマイナー バージョン
* 2 つの以前のマイナー バージョン。 各サポートされているマイナー バージョンは 2 つの安定性の高い修正プログラムもサポートしています。

これは "N-2" として知られています: (N (最新リリース) - 2 (マイナー バージョン))。

たとえば、AKS が *1.15.a* を本日導入した場合は、次のバージョンのサポートが提供されます。

新しいマイナー バージョン    |    サポートされているバージョンの一覧
-----------------    |    ----------------------
1.15.a               |    1.15.a、1.15.b、1.14.c、1.14.d、1.13.e、1.13.f

ここで、".<英字>" はパッチ バージョンを表します。

バージョンの変更と要件に関する通知の詳細については、以下の「通知」を参照してください。

新しいマイナー バージョンが導入されると、サポートされている最も古いマイナー バージョンと修正プログラムのリリースは、非推奨となり削除されます。 たとえば、現在次のバージョンがサポートされているとします。

```
1.15.a
1.15.b
1.14.c
1.14.d
1.13.e
1.13.f
```

また、AKS では 1.16. *をリリースしているとします。これは、1.13.* バージョン (すべての 1.13 バージョン) は削除され、サポート対象外になることを意味します。

> [!NOTE]
> なお、お客様がサポートされていない Kubernetes バージョンを実行している場合は、クラスターのサポートを要求したときにアップグレードするよう求められます。 サポートされていない Kubernetes リリースを実行しているクラスターは、[AKS サポート ポリシー](https://docs.microsoft.com/azure/aks/support-policies)の対象ではありません。

上記のマイナー バージョンに加え、AKS は、特定のマイナー バージョンの 2 つの最新の**修正プログラム**のリリースをサポートしています。 たとえば、次のようなサポートされているバージョンがあるとします。

```
Current Supported Version List
------------------------------
1.15.2, 1.15.1, 1.14.5, 1.14.4
```

上流 Kubernetes が 1.15.3 および 1.14.6 をリリース済みで、AKS がそれらの修正プログラムのバージョンをリリースしている場合、最も古い修正プログラムのバージョンは非推奨となって削除され、サポートされているバージョンの一覧は次のようになります。

```
New Supported Version List
----------------------
1.15.*3*, 1.15.*2*, 1.14.*6*, 1.14.*5*
```

### <a name="communications"></a>通知

* 新しい**マイナー** バージョンの Kubernetes の場合
  * すべてのユーザーには、新しいバージョンと削除される予定のバージョンが公的に通知されます。
  * 新しい修正プログラムのバージョンがリリースされると、同時に最も古い修正プログラムのリリースが削除されます。
  * お客様は、公示日から **60 日間**の間に、サポートされているマイナー バージョンのリリースにアップグレードすることができます。
* 新しい**修正プログラム**のバージョンの Kubernetes の場合
  * すべてのユーザーには、リリースされている修正プログラムの新しいバージョンが通知され、最新の修正プログラムのリリースにアップグレードするよう通知されます。
  * ユーザーは、**30 日間**の間に、サポートされている新しい修正プログラム リリースにアップグレードすることができます。 ユーザーは、**30 日間** の間に、最も古いものが削除される前にサポートされている修正プログラムのリリースにアップグレードすることができます。

AKS は "リリース済みバージョン" を、すべての SLO およびサービス品質の測定で有効であり、すべてのリージョンで利用可能な、一般提供バージョンとして定義します。 さらに、AKS は、明示的にラベル付けされ、プレビューの利用規約の対象となるプレビュー バージョンをサポートする場合もあります。

#### <a name="notification-channels-for-aks-changes"></a>AKS の変更についての通知チャネル

AKS では、[GitHub](https://github.com/Azure/AKS/releases) のサービスでリリースされた新しい Kubernetes バージョン、サービスの変更、コンポーネントの更新をまとめた定期的なサービス更新プログラムを公開します。

これらの変更は、マネージド サービスの一部として提供される定期的なメンテナンスの一環としてすべてのお客様に継承されます。明示的なアップグレードが必要な方もいれば、アクションを必要としない方もいます。

通知は次の方法でも送信されます。

* [AKS リリース ノート](https://aka.ms/aks/releasenotes)
* Azure Portal の通知
* [Azure 更新チャネル][azure-update-channel]

### <a name="supported-versions-policy-exceptions"></a>サポートされているバージョンのポリシーの例外

AKS は、バグまたはセキュリティの問題に影響を与える 1 つ以上の重要な運用があることが識別された新しいバージョンまたは既存のバージョンを、予告なしに追加または削除する権利を留保します。

特定の修正プログラムのリリースは、バグまたはセキュリティの問題の重大度に応じて、スキップされるか、ロールアウトが高速になる場合があります。

### <a name="azure-portal-and-cli-default-versions"></a>Azure portal と CLI の既定のバージョン

ポータルまたは Azure CLI を使用して AKS クラスターをデプロイする場合、クラスターは既定で N-1 マイナー バージョンおよび最新修正プログラムに設定されます。 たとえば、AKS でサポートされているのが *1.15.a*、*1.15.b*、*1.14.c*、*1.14.d*、*1.13.e*、および *1.13.f* であれば、選択される既定のバージョンは *1.14.c* となります。

AKS は既定で N-1 を選択し、既定で既知の安定した、修正プログラムが適用されたバージョンをお客様に提供します。

## <a name="list-currently-supported-versions"></a>現在サポートされているバージョンの一覧表示

ご使用のサブスクリプションとリージョンで現在使用可能なバージョンを確認するには、[az aks get-versions][az-aks-get-versions] コマンドを使用します。 次の例では、*EastUS* リージョンで使用可能な Kubernetes のバージョンが一覧表示されます。

```azurecli-interactive
az aks get-versions --location eastus --output table
```

## <a name="faq"></a>FAQ

**顧客がサポートされていないマイナー バージョンの Kubernetes クラスターをアップグレードするとどうなりますか。**

*n-3* バージョンを使用している場合は、サポート外であり、アップグレードするよう求められます。 バージョン n-3 から n-2 へのアップグレードに成功した場合は、サポート ポリシーの対象になります。 例:

- サポートされている最も古い AKS のバージョンが *1.13.a* で、使用しているバージョンが *1.12.b* またはそれ以前の場合は、サポート対象外です。
- *1.12.b* から *1.13.a* 以降へのアップグレードが成功すると、サポート ポリシー対象に戻ります。

*N-2* のサポート対象期間より前のバージョンへのアップグレードはサポートされていません。 このような場合、新しい AKS クラスターを作成し、サポート対象期間のバージョンでワークロードを再デプロイすることをお勧めします。

**サポート外とは**

"サポート外" とは、実行しているバージョンがサポートされているバージョンの一覧に含まれていないことを意味し、サポートを要求すると、クラスターをサポートされているバージョンにアップグレードするよう求められます。 さらに、AKS は、サポートされているバージョンの一覧に含まれていないクラスターのランタイムなどを保証しません。

**顧客がサポートされていないマイナー バージョンの Kubernetes クラスターを拡大縮小するとどうなりますか。**

AKS でサポートされていないマイナー バージョンの場合、スケールインまたはスケールアウトは引き続き機能しますが、アップグレードしてクラスターをサポート対象に戻すことを強くお勧めします。

**顧客が Kubernetes バージョンをそのまま永久に使用し続けることはできますか。**

はい。 ただし、クラスターが AKS でサポートされているバージョンのいずれかにない場合、クラスターは AKS サポート ポリシー外となります。 Azure は、自動的にクラスターをアップグレードしたり削除したりすることはありません。

**ノード プールがサポートされている AKS バージョンのいずれかにない場合、コントロール プレーンはどのバージョンをサポートしますか。**

コントロール プレーンは、すべてのノード プールのバージョンの期間内になければなりません。 コントロール プレーンまたはノード プールのアップグレードの詳細については、[ノード プールのアップグレード](use-multiple-node-pools.md#upgrade-a-cluster-control-plane-with-multiple-node-pools)に関するドキュメントを参照してください。

## <a name="next-steps"></a>次の手順

クラスターをアップグレードする方法の詳細については、「[Azure Kubernetes Service (AKS) クラスターのアップグレード][aks-upgrade]」をご覧ください。

<!-- LINKS - External -->
[aks-engine]: https://github.com/Azure/aks-engine
[azure-update-channel]: https://azure.microsoft.com/updates/?product=kubernetes-service

<!-- LINKS - Internal -->
[aks-upgrade]: upgrade-cluster.md
[az-aks-get-versions]: /cli/azure/aks#az-aks-get-versions
