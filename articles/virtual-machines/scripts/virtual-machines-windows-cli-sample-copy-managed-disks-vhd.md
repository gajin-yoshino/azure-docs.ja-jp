---
title: ストレージ アカウントにマネージド ディスクをコピーする - Windows CLI サンプル
description: Azure CLI サンプル - ストレージ アカウントにマネージド ディスクをエクスポートまたはコピーします。
services: virtual-machines-windows
documentationcenter: storage
author: ramankumarlive
manager: kavithag
tags: azure-service-management
ms.assetid: ''
ms.service: virtual-machines-windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 09/17/2018
ms.author: ramankum
ms.custom: mvc,seodec18
ms.openlocfilehash: 17ca58a8c03def3565bf7e38099d84cf767d333c
ms.sourcegitcommit: 3d79f737ff34708b48dd2ae45100e2516af9ed78
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "87010099"
---
# <a name="exportcopy-a-managed-disk-to-a-storage-account-using-the-azure-cli"></a>Azure CLI を使用してストレージ アカウントにマネージド ディスクをエクスポート/コピーする

このスクリプトは、マネージド ディスクの基盤となる VHD を、同じまたは別の地域のストレージ アカウントにエクスポートします。 最初にマネージド ディスクの SAS URI を生成し、続いてそれを使用して VHD をストレージ アカウントにコピーします。 このスクリプトを使用して、地域拡張のために、マネージド ディスクをコピーします。

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>サンプル スクリプト

[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-managed-disks-vhd-to-storage-account/copy-managed-disks-vhd-to-storage-account.sh "Copy the VHD of a managed disk")]

## <a name="script-explanation"></a>スクリプトの説明

このスクリプトでは、次のコマンドを使用してマネージド ディスク用の SAS URI を生成し、SAS URI を使用して基盤となる VHD をストレージ アカウントにコピーします。 表内の各コマンドは、それぞれのドキュメントにリンクされています。

| command | メモ |
|---|---|
| [az ディスク アクセスの許可](/cli/azure/disk?view=azure-cli-latest#az-disk-grant-access) | 基盤となる VHD ファイルをストレージ アカウントにコピーするか、オンプレミスにダウンロードするために使用される、読み取り専用の SAS を生成します。  |
| [az storage blob copy start](/cli/azure/storage/blob/copy) | BLOB を、あるストレージ アカウントから別のストレージ アカウントに非同期的にコピーします |

## <a name="next-steps"></a>次のステップ

[VHD からマネージド ディスクを作成する](virtual-machines-windows-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

Azure CLI の詳細については、[Azure CLI のドキュメント](/cli/azure)のページをご覧ください。

その他の仮想マシンとマネージド ディスクの CLI サンプル スクリプトは、[Azure Windows VM のドキュメント](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)にあります。
