---
title: Azure サービス タグの概要
titlesuffix: Azure Virtual Network
description: サービス タグについて確認します。 サービス タグを使用すると、セキュリティ規則の作成の複雑さを最小限に抑えることができます。
services: virtual-network
documentationcenter: na
author: jispar
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/22/2019
ms.author: jispar
ms.reviewer: kumud
ms.openlocfilehash: ed9b893b11f96a813cee4c751743ceb182a9a0bf
ms.sourcegitcommit: 87781a4207c25c4831421c7309c03fce5fb5793f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2020
ms.locfileid: "76543037"
---
# <a name="virtual-network-service-tags"></a>仮想ネットワーク サービス タグ 
<a name="network-service-tags"></a>

サービス タグは、指定された Azure サービスからの IP アドレス プレフィックスのグループを表します。 サービス タグに含まれるアドレス プレフィックスの管理は Microsoft が行い、アドレスが変化するとサービス タグは自動的に更新されます。これにより、ネットワーク セキュリティ規則に対する頻繁な更新の複雑さを最小限に抑えられます。 

サービス タグを使用して、 [ネットワーク セキュリティ グループ](https://docs.microsoft.com/azure/virtual-network/security-overview#security-rules) または  [Azure Firewall](https://docs.microsoft.com/azure/firewall/service-tags) でのネットワーク アクセス制御を定義できます。 セキュリティ規則を作成するときに、特定の IP アドレスの代わりにサービス タグを使用します。 規則の適切な " *ソース* " または " *宛先* " フィールドにサービス タグ名 (たとえば  **ApiManagement**) を指定することにより、対応するサービスのトラフィックを許可または拒否できます。 

サービス タグを使用すると、ネットワーク分離を実現し、パブリック エンドポイントを持つ Azure サービスへのアクセス時に一般のインターネットから Azure リソースを保護できます。 受信/送信ネットワーク セキュリティ グループ規則を作成して、**インターネット**との間のトラフィックを拒否し、**AzureCloud** または他の特定の Azure サービスの[利用可能なサービス タグ](#available-service-tags)との間のトラフィックを許可します。 

## <a name="available-service-tags"></a>利用可能なサービス タグ
次の表には、[ネットワーク セキュリティ グループ](https://docs.microsoft.com/azure/virtual-network/security-overview#security-rules)の規則で使用できるすべてのサービス タグが含まれています。

各列は、タグが次を満たすかどうかを示しています。

- 受信または送信トラフィックを扱う規則に適している。
- [リージョン](https://azure.microsoft.com/regions) スコープをサポートしている。
- [Azure Firewall](https://docs.microsoft.com/azure/firewall/service-tags) 規則で使用可能である。

既定では、サービス タグにはクラウド全体の範囲が反映されます。 サービス タグによっては、対応する IP 範囲を指定されたリージョンに制限することで、より詳細な制御を実現することもできます。 たとえば、サービス タグ **Storage** はクラウド全体の Azure Storage を表していますが、**Storage.WestUS** を使用すると、WestUS リージョンのストレージ IP アドレスのみに範囲が限定されます。 次の表に、各サービス タグでそのようなリージョン スコープがサポートされるかどうかを示します。  

| タグ | 目的 | 受信または送信で使用できるか | リージョン別か | Azure Firewall と共に使用できるか |
| --- | -------- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **ApiManagement** | Azure API Management 専用デプロイのための管理トラフィック。 | 両方 | いいえ | はい |
| **ApplicationInsightsAvailability** | Application Insights の可用性。 | 両方 | いいえ | いいえ |
| **AppService**    | Azure App Service。 このタグは、Web アプリのフロントエンドに対する送信セキュリティ規則で推奨されます。 | 送信 | はい | はい |
| **AppServiceManagement** | App Service Environment 専用デプロイのための管理トラフィック。 | 両方 | いいえ | はい |
| **AzureActiveDirectory** | Azure Active Directory。 | 送信 | いいえ | はい |
| **AzureActiveDirectoryDomainServices** | Azure Active Directory Domain Services 専用デプロイのための管理トラフィック。 | 両方 | いいえ | はい |
| **AzureAdvancedThreatProtection** | Azure Advanced Threat Protection。 | 送信 | いいえ | いいえ |
| **AzureBackup** |Azure Backup。<br/><br/>*注:* このタグは、**Storage** タグと **AzureActiveDirectory** タグに依存します。 | 送信 | いいえ | はい |
| **AzureBotService** | Azure Bot Service。 | 送信 | いいえ | いいえ |
| **AzureCloud** | すべての[データセンター パブリック IP アドレス](https://www.microsoft.com/download/details.aspx?id=56519)。 | 送信 | はい | はい |
| **AzureCognitiveSearch** | Azure Cognitive Search (スキルセットでインデクサーを使用する場合)。 | 両方 | いいえ | いいえ |
| **AzureConnectors** | プローブ/バックエンド接続用の Azure Logic Apps コネクタ。 | 受信 | はい | はい |
| **AzureContainerRegistry** | Azure Container Registry。 | 送信 | はい | はい |
| **AzureCosmosDB** | Azure Cosmos DB。 | 送信 | はい | はい |
| **AzureDatabricks** | Azure Databricks。 | 両方 | いいえ | いいえ |
| **AzureDataExplorerManagement** | Azure Data Explorer 管理。 | 受信 | いいえ | いいえ |
| **AzureDataLake** | Azure Data Lake。 | 送信 | いいえ | はい |
| **AzureEventGrid** | Azure Event Grid。 <br/><br/>*注:* このタグは、米国中南部、米国東部、米国東部 2、米国西部 2、および米国中部の Azure Event Grid エンドポイントのみを対象としています。 | 両方 | いいえ | いいえ |
| **AzureFrontDoor** | Azure Front Door。 | 両方 | いいえ | いいえ |
| **AzureInformationProtection** | Azure Information Protection。<br/><br/>*注:* このタグは、**AzureActiveDirectory** タグと **AzureFrontDoor.Frontend** タグに依存します。 次の IP もホワイトリストに登録してください (この依存関係は間もなく削除予定です)。13.107.6.181 & 13.107.9.181. | 送信 | いいえ | いいえ |
| **AzureIoTHub** | Azure IoT Hub。 | 送信 | いいえ | いいえ |
| **AzureKeyVault** | Azure Key Vault。<br/><br/>*注:* このタグは、**AzureActiveDirectory** タグに依存します。 | 送信 | はい | はい |
| **AzureLoadBalancer** | Azure インフラストラクチャのロード バランサー。 このタグは、Azure の正常性プローブの送信元となる[ホストの仮想 IP アドレス](security-overview.md#azure-platform-considerations) (168.63.129.16) に変換されます。 Azure Load Balancer を使っていない場合は、この規則をオーバーライドできます。 | 両方 | いいえ | いいえ |
| **AzureMachineLearning** | Azure Machine Learning | 両方 | いいえ | はい |
| **AzureMonitor** | Log Analytics、Application Insights、AzMon、およびカスタム メトリック (GiG エンドポイント)。<br/><br/>*注:* Log Analytics では、このタグは **Storage** タグに依存します。 | 送信 | いいえ | はい |
| **AzurePlatformDNS** | 基本インフラストラクチャ (既定) の DNS サービス。<br/><br>このタグを使用すると、既定の DNS を無効にすることができます。 このタグを使用する場合は注意が必要です。 「[Azure プラットフォームに関する考慮事項](https://docs.microsoft.com/azure/virtual-network/security-overview#azure-platform-considerations)」を参照することをお勧めします。 また、このタグを使用する前にテストを実行することをお勧めします。 | 送信 | いいえ | いいえ |
| **AzurePlatformIMDS** | Azure Instance Metadata Service (IMDS)。これは基本的なインフラストラクチャ サービスです。<br/><br/>このタグを使用すると、既定の IMDS を無効にすることができます。 このタグを使用する場合は注意が必要です。 「[Azure プラットフォームに関する考慮事項](https://docs.microsoft.com/azure/virtual-network/security-overview#azure-platform-considerations)」を参照することをお勧めします。 また、このタグを使用する前にテストを実行することをお勧めします。 | 送信 | いいえ | いいえ |
| **AzurePlatformLKM** | Windows のライセンスまたはキー管理サービス。<br/><br/>このタグを使用すると、ライセンスの既定値を無効にすることができます。 このタグを使用する場合は注意が必要です。 「[Azure プラットフォームに関する考慮事項](https://docs.microsoft.com/azure/virtual-network/security-overview#azure-platform-considerations)」を参照することをお勧めします。  また、このタグを使用する前にテストを実行することをお勧めします。 | 送信 | いいえ | いいえ |
| **AzureResourceManager** | Azure Resource Manager。 | 送信 | いいえ | いいえ |
| **AzureSiteRecovery** | Azure Site Recovery。<br/><br/>*注:* このタグは、**Storage** タグ、**AzureActiveDirectory**タグ、および **EventHub** タグに依存します。 | 送信 | いいえ | いいえ |
| **AzureTrafficManager** | Azure Traffic Manager プローブ IP アドレス。<br/><br/>Traffic Manager プローブ IP アドレスについて詳しくは、「[Traffic Manager についてよく寄せられる質問 (FAQ)](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-faqs)」をご覧ください。 | 受信 | いいえ | はい |  
| **BatchNodeManagement** | Azure Batch 専用デプロイのための管理トラフィック。 | 両方 | いいえ | はい |
| **CognitiveServicesManagement** | Azure Cognitive Services のトラフィックのアドレス範囲。 | 送信 | いいえ | いいえ |
| **Dynamics365ForMarketingEmail** | Dynamics 365 のマーケティング電子メール サービスのアドレス範囲。 | 送信 | はい | いいえ |
| **ElasticAFD** | エラスティック Azure Front Door。 | 両方 | いいえ | いいえ |
| **EventHub** | Azure Event Hubs。 | 送信 | はい | はい |
| **GatewayManager** | Azure VPN Gateway と Application Gateway 専用デプロイのための管理トラフィック。 | 受信 | いいえ | いいえ |
| **GuestAndHybridManagement** | Azure Automation とゲスト構成。 | 両方 | いいえ | はい |
| **HDInsight** | Azure HDInsight。 | 受信 | はい | いいえ |
| **Internet** | パブリック インターネットによってアクセスできる仮想ネットワークの外部の IP アドレス空間。<br/><br/>このアドレス範囲には、[Azure によって所有されているパブリック IP アドレス空間](https://www.microsoft.com/download/details.aspx?id=41653)が含まれています。 | 両方 | いいえ | いいえ |
| **MicrosoftCloudAppSecurity** | Microsoft Cloud App Security。 | 送信 | いいえ | いいえ |
| **MicrosoftContainerRegistry** | Azure Container Registry。 | 送信 | はい | はい |
| **ServiceBus** | Premium サービス レベルを使用する Azure Service Bus トラフィック。 | 送信 | はい | はい |
| **ServiceFabric** | Azure Service Fabric。 | 送信 | いいえ | いいえ |
| **Sql** | Azure SQL Database、Azure Database for MySQL、Azure Database for PostgreSQL、および Azure SQL Data Warehouse。<br/><br/>*注:* このタグはサービスだけを表し、サービスの特定のインスタンスは表しません。 たとえば、このタグは Azure SQL Database サービスを表しますが、特定の SQL データベースや SQL サーバーは表しません。 | 送信 | はい | はい |
| **SqlManagement** | SQL 専用デプロイのための管理トラフィック。 | 両方 | いいえ | はい |
| **Storage** | Azure Storage です。 <br/><br/>*注:* このタグはサービスだけを表し、サービスの特定のインスタンスは表しません。 たとえば、このタグは Azure Storage サービスを表しますが、特定の Azure Storage アカウントは表しません。 | 送信 | はい | はい |
| **VirtualNetwork** | 仮想ネットワーク アドレス空間 (仮想ネットワークに対して定義されているすべての IP アドレスの範囲)、すべての接続されたオンプレミスのアドレス空間、[ピアリング](virtual-network-peering-overview.md)された仮想ネットワーク、[仮想ネットワーク ゲートウェイ](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%3ftoc.json)に接続された仮想ネットワーク、[ホストの仮想 IP アドレス](security-overview.md#azure-platform-considerations)、および[ユーザーが定義したルート](virtual-networks-udr-overview.md)で使用されるアドレス プレフィックス。 このタグには、既定のルートも含まれる場合もあります。 | 両方 | いいえ | いいえ |

>[!NOTE]
>(Azure Resource Manager の前の) クラシック デプロイ モデルでは、前の表に示したタグのサブセットがサポートされます。 これらのタグは、スペルが異なります。
>
>| クラシックのスペル | 同等のリソース マネージャー タグ |
>|---|---|
>| AZURE_LOADBALANCER | AzureLoadBalancer |
>| INTERNET | インターネット |
>| VIRTUAL_NETWORK | VirtualNetwork |

> [!NOTE]
> Azure サービスのサービス タグは、使用される特定のクラウドのアドレス プレフィックスを表します。 たとえば、Azure パブリック クラウドの **Sql** タグ値に対応する基になる IP 範囲は、Azure China クラウドの基になる範囲とは異なります。

> [!NOTE]
> Azure Storage や Azure SQL Database などのサービスの[仮想ネットワーク サービス エンドポイント](virtual-network-service-endpoints-overview.md)を実装する場合、Azure はサービスの仮想ネットワーク サブネットへの[ルート](virtual-networks-udr-overview.md#optional-default-routes)を追加します。 ルートのアドレス プレフィックスは、対応するサービス タグと同じアドレス プレフィックスまたは CIDR 範囲になります。

## <a name="service-tags-on-premises"></a>オンプレミスのサービス タグ  
現在のサービス タグと範囲情報を、オンプレミスのファイアウォール構成の一部として取得して含めることができます。 この情報は、各サービス タグに対応する現在の特定時点の IP 範囲の一覧です。 次のセクションで説明するように、プログラムまたは JSON ファイルのダウンロードを使用して、この情報を取得できます。

### <a name="use-the-service-tag-discovery-api-public-preview"></a>Service Tag Discovery API を使用する (パブリック プレビュー)
サービス タグの現在の一覧を IP アドレス範囲の詳細と共にプログラムで取得できます。

- [REST](https://docs.microsoft.com/rest/api/virtualnetwork/servicetags/list)
- [Azure PowerShell](https://docs.microsoft.com/powershell/module/az.network/Get-AzNetworkServiceTag?view=azps-2.8.0&viewFallbackFrom=azps-2.3.2)
- [Azure CLI](https://docs.microsoft.com/cli/azure/network?view=azure-cli-latest#az-network-list-service-tags)

> [!NOTE]
> パブリック プレビューの段階であるため、Discovery API によって返される情報は、JSON のダウンロードによって返される情報よりも新しくない場合があります (次のセクションを参照してください)。


### <a name="discover-service-tags-by-using-downloadable-json-files"></a>ダウンロード可能な JSON ファイルを使用してサービス タグを検出する 
サービス タグの現在の一覧と IP アドレス範囲の詳細を含む JSON ファイルをダウンロードできます。 これらの一覧は、毎週更新されて公開されます。 各クラウドの場所は次のとおりです。

- [Azure Public](https://www.microsoft.com/download/details.aspx?id=56519)
- [Azure US Government](https://www.microsoft.com/download/details.aspx?id=57063)  
- [Azure China](https://www.microsoft.com/download/details.aspx?id=57062) 
- [Azure Germany](https://www.microsoft.com/download/details.aspx?id=57064)   

> [!NOTE]
>[Azure Public](https://www.microsoft.com/download/details.aspx?id=41653)、[Azure China](https://www.microsoft.com/download/details.aspx?id=42064)、および [Azure Germany](https://www.microsoft.com/download/details.aspx?id=54770) については、この情報のサブセットが XML ファイルで公開されています。 これらの XML ダウンロードは、2020 年 6 月 30 日に非推奨となり、その後は使用できなくなります。 前のセクションの説明に従って、Discovery API または JSON ファイルのダウンロードの使用に移行してください。

### <a name="tips"></a>ヒント 
- ある公開からその次の公開に更新されたかどうかは、JSON ファイル内の *changeNumber* の値の増加に注目することで理解できます。 各サブセクション (たとえば **Storage.WestUS**) には、変更が発生するたびに増えていく固有の *changeNumber* があります。 ファイルの *changeNumber* の最上位レベルは、サブセクションのいずれかが変更されると増加します。
- サービス タグ情報を解析する方法の例 (WestUS のストレージについてのすべてのアドレス範囲を取得する方法など) については、[Service Tag Discovery API PowerShell](https://aka.ms/discoveryapi_powershell) のドキュメントを参照してください。

## <a name="next-steps"></a>次のステップ
- [ネットワーク セキュリティ グループの作成](tutorial-filter-network-traffic.md)方法を確認します。
