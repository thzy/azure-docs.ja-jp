---
title: PowerShell で RDP のユーザー名とパスワードを更新する
description: Azure PowerShell スクリプトのサンプル - 特定のノード型のすべての Service Fabric クラスター ノードの RDP ユーザー名とパスワードを更新します。
services: service-fabric
documentationcenter: ''
author: athinanthny
manager: chackdan
editor: ''
tags: azure-service-management
ms.assetid: ''
ms.service: service-fabric
ms.workload: multiple
ms.topic: sample
ms.date: 03/19/2018
ms.author: atsenthi
ms.custom: mvc
ms.openlocfilehash: 0cf9f8362d3fa683084aef840cf35cd9a843608a
ms.sourcegitcommit: 003e73f8eea1e3e9df248d55c65348779c79b1d6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75614810"
---
# <a name="update-the-admin-username-and-password-of-the-vms-in-a-cluster"></a>クラスター内の VM の管理者のユーザー名とパスワードを更新します。

Service Fabric クラスター内の各[ノード型](../service-fabric-cluster-nodetypes.md)は仮想マシン スケール セットです。 このサンプル スクリプトは、特定のノード型のクラスター仮想マシンの管理者のユーザー名およびパスワードを更新します。  管理者のパスワードは変更可能なスケール セット プロパティではないため、スケール セットに VMAccessAgent 拡張機能を追加します。  ユーザー名とパスワードの変更は、スケール セット内のすべてのノードに適用されます。 必要に応じてパラメーターをカスタマイズします。

[!INCLUDE [updated-for-az](../../../includes/updated-for-az.md)]

必要に応じて、[Azure PowerShell ガイド](/powershell/azure/overview)の手順に従って Azure PowerShell をインストールします。 

## <a name="sample-script"></a>サンプル スクリプト

[!code-powershell[main](../../../powershell_scripts/service-fabric/change-rdp-user-and-pw/change-rdp-user-and-pw.ps1 "Updates a RDP username and password for cluster nodes")]

## <a name="script-explanation"></a>スクリプトの説明

このスクリプトでは以下のコマンドを使用します。表内の各コマンドは、それぞれのドキュメントにリンクされています。

| command | メモ |
|---|---|
| [Get-AzVmss](/powershell/module/az.compute/get-azvmss) | クラスター ノード型 (仮想マシン スケール セット) のプロパティの取得   |
| [Add-AzVmssExtension](/powershell/module/az.compute/add-azvmssextension)| 仮想マシン スケール セットに拡張機能を追加します。|
| [Update-AzVmss](/powershell/module/az.compute/update-azvmss)|仮想マシン スケール セットの状態を、ローカル VMSS オブジェクトの状態に更新します。|

## <a name="next-steps"></a>次のステップ

Azure PowerShell モジュールの詳細については、[Azure PowerShell のドキュメント](/powershell/azure/overview)を参照してください。

その他の Azure Service Fabric 用 Azure PowerShell サンプルは、[Azure PowerShell サンプル](../service-fabric-powershell-samples.md)のページにあります。
