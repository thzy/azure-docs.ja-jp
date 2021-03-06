---
title: ポータルを使用して Azure 共有イメージ ギャラリーを作成する
description: Azure portal を使用して、仮想マシン イメージを作成して共有する方法について説明します。
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: gwallace
editor: tysonn
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-windows
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 11/06/2019
ms.author: cynthn
ms.custom: ''
ms.openlocfilehash: 6273b58d9db53cfc4f6647885c70148982f0b950
ms.sourcegitcommit: 5ab4f7a81d04a58f235071240718dfae3f1b370b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74975501"
---
# <a name="create-an-azure-shared-image-gallery-using-the-portal"></a>ポータルを使用して Azure 共有イメージ ギャラリーを作成する

[共有イメージ ギャラリー](shared-image-galleries.md)により、組織全体でのカスタム イメージの共有が簡素化されます。 カスタム イメージは Marketplace のイメージに似ていますが、カスタム イメージは自分で作成します。 カスタム イメージは、デプロイ タスク (アプリケーションのプリロード、アプリケーションの構成、その他の OS 構成など) のブートストラップを実行するために使用できます。 

共有イメージ ギャラリーを使用すると、組織内、リージョン内またはリージョン間、AAD テナント内で、他のユーザーとご自身のカスタム VM イメージを共有できます。 どのイメージを共有するか、どのリージョンでそのイメージを使用できるようにするか、および、だれと共有するかを選択することができます。 複数のギャラリーを作成することで、共有イメージを論理的にグループ化できます。 

ギャラリーは最上位リソースで、完全なロールベースのアクセス制御 (RBAC) が可能です。 イメージのバージョン管理もできるため、Azure リージョンの別のセットに各イメージのバージョンをレプリケートできます。 ギャラリーは、マネージド イメージでのみ機能します。

共有イメージ ギャラリー機能には、リソースの種類が複数あります。 それらを、この記事の中で使用または作成していきます。

| リソース | 説明|
|----------|------------|
| **マネージド イメージ** | 単独で使用することも、イメージ ギャラリーに**イメージ バージョン**を作成するために使用することもできる基本的なイメージ。 マネージド イメージは、[一般化された](shared-image-galleries.md#generalized-and-specialized-images) VM から作成されます。 マネージド イメージは、複数の VM を作成する際に使用できる特別な種類の VHD で、共有イメージ バージョンを作成する際にも使用できるようになりました。 |
| **スナップショット** | **イメージ バージョン**の作成に使用できる VHD のコピー。 [特殊化された](shared-image-galleries.md#generalized-and-specialized-images) VM (一般化されていない VM) からスナップショットを取得し、単独でまたはデータ ディスクのスナップショットと一緒に使用して、特殊化されたイメージ バージョンを作成できます。
| **イメージ ギャラリー** | Azure Marketplace などの **イメージ ギャラリー**は、イメージを管理して共有するためのリポジトリです。ただし、アクセス権の所有者を制御します。 |
| **イメージ定義** | イメージはギャラリー内で定義され、組織内で使用するためにイメージと要件に関する情報を伝達します。 イメージが一般化されているか特殊化されているか、オペレーティング システム、最小および最大メモリ要件、リリース ノートなどの情報を含めることができます。 これは、イメージの種類の定義です。 |
| **イメージ バージョン** | **イメージ バージョン**は、ギャラリーを利用している場合に、VM の作成に使用します。 お使いの環境に必要な複数のイメージ バージョンを保持できます。 マネージド イメージのように、**イメージ バージョン**を使用して VM を作成する場合、イメージ バージョンは VM 用の新しいディスクを作成するために使用されます。 イメージ バージョンは複数回、使用できます。 |

<br>


> [!IMPORTANT]
> 特殊化されたイメージは現在、パブリック プレビュー段階です。
> このプレビュー バージョンはサービス レベル アグリーメントなしで提供されています。運用環境のワークロードに使用することはお勧めできません。 特定の機能はサポート対象ではなく、機能が制限されることがあります。 詳しくは、[Microsoft Azure プレビューの追加使用条件](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)に関するページをご覧ください。
>
> **プレビューに関する既知の制限事項**: VM は、ポータルまたは API を使用して、特殊化されたイメージからのみ作成できます。 プレビューでは CLI や PowerShell はサポートされていません。

## <a name="before-you-begin"></a>開始する前に

この記事の例を完了するには、一般化された VM の既存のマネージド イメージか、特殊化された VM のスナップショットが必要です。 お持ちでない場合は、「[チュートリアル: Azure PowerShell を使用して Azure VM のカスタム イメージを作成する](tutorial-custom-images.md)」に従って、マネージド イメージを作成するか、特殊化された VM の場合は[スナップショットを作成](snapshot-copy-managed-disk.md)してください。 マネージド イメージの場合もスナップショットの場合も、データ ディスクのサイズが 1 TB を超えることはできません。

この記事の作業に出現するリソース グループと VM の名前は適宜置き換えてください。


[!INCLUDE [virtual-machines-common-shared-images-portal](../../../includes/virtual-machines-common-shared-images-portal.md)]
 
## <a name="create-vms"></a>VM の作成

これで、1 つ以上の新しい VM を作成できるようになりました。 この例では、"*米国東部*" のデータセンターにある *myResourceGroup* に、*myVM* という名前の VM を作成します。

1. イメージ定義に移動します。 リソース フィルターを使用すると、使用可能なすべてのイメージ定義を表示できます。
1. イメージ定義のページで、ページの上部にあるメニューから **[VM の作成]** を選択します。
1. **[リソース グループ]** で、 **[新規作成]** を選択し、名前として「*myResourceGroup*」と入力します。
1. **[仮想マシン名]** に、「*myVM*」と入力します。
1. **[リージョン]** で、 *[米国東部]* を選択します。
1. **[可用性オプション]** で、既定の *[インフラストラクチャ冗長は必要ありません]* のままにします。
1. イメージ定義のページから操作を開始していれば、 **[イメージ]** の値に `latest` イメージ バージョンが自動的に入力されます。
1. **[サイズ]** では、利用可能なサイズの一覧から VM サイズを選択し、 **[選択]** を選択します。
1. そのイメージが一般化されている場合は、 **[管理者アカウント]** で、ユーザー名 (*azureuser* など) とパスワードを指定する必要があります。 パスワードは 12 文字以上で、[定義された複雑さの要件](faq.md#what-are-the-password-requirements-when-creating-a-vm)を満たす必要があります。 イメージが特殊化されている場合は、ソース VM のユーザー名とパスワードが使用されるため、[ユーザー名] と [パスワード] のフィールドはグレーアウトされます。
1. VM へのリモート アクセスを許可する場合、 **[パブリック受信ポート]** で、 **[選択したポートを許可する]** を選択し、ドロップダウンから **[RDP (3389)]** を選択します。 VM へのリモート アクセスを許可しない場合、 **[パブリック受信ポート]** で、 **[なし]** を選択したままにします。
1. 完了したら、ページの下部にある **[Review + create]\(確認と作成\)** ボタンを選択します。
1. VM が検証に合格したら、ページの下部にある **[作成]** を選択し、デプロイを開始します。


## <a name="clean-up-resources"></a>リソースのクリーンアップ

必要がなくなったら、リソース グループ、仮想マシン、およびすべての関連リソースを削除できます。 これを行うには、仮想マシンのリソース グループを選択し、 **[削除]** を選択して、削除するリソース グループの名前を確認します。

個々のリソースを削除する場合は、逆の順序でそれらを削除する必要があります。 たとえば、イメージ定義を削除するには、そのイメージから作成されたすべてのイメージ バージョンを削除する必要があります。

## <a name="next-steps"></a>次の手順

共有イメージ ギャラリー リソースは、テンプレートを使用して作成することもできます。 いくつかの Azure クイック スタート テンプレートが用意されています。 

- [共有イメージ ギャラリーを作成する](https://azure.microsoft.com/resources/templates/101-sig-create/)
- [共有イメージ ギャラリーにイメージ定義を作成する](https://azure.microsoft.com/resources/templates/101-sig-image-definition-create/)
- [共有イメージ ギャラリーにイメージのバージョンを作成する](https://azure.microsoft.com/resources/templates/101-sig-image-version-create/)
- [イメージ バージョンから VM を作成する](https://azure.microsoft.com/resources/templates/101-vm-from-sig/)

共有イメージ ギャラリーの詳細については、[概要](shared-image-galleries.md)のページをご覧ください。 問題が生じた場合は、「[共有イメージ ギャラリーのトラブルシューティング](troubleshooting-shared-images.md)」を参照してください。

