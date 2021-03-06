---
title: Azure CLI のサンプル スクリプト - プレフィックスでコンテナーを削除する | Microsoft Docs
description: コンテナー名のプレフィックスに基づいて Azure Storage Blob コンテナーを削除します。
services: storage
author: tamram
ms.service: storage
ms.subservice: blobs
ms.devlang: cli
ms.topic: sample
ms.date: 06/22/2017
ms.author: tamram
ms.openlocfilehash: 71bffe004ae8f2ac2060c1bfc12c4fff0be95c34
ms.sourcegitcommit: 3d79f737ff34708b48dd2ae45100e2516af9ed78
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "87006213"
---
# <a name="use-an-azure-cli-script-to-delete-containers-based-on-container-name-prefix"></a>Azure CLI スクリプトを使用して、コンテナー名のプレフィックスに基づいてコンテナーを削除する

このスクリプトでは、まず Azure Blob ストレージにいくつかのサンプルのコンテナーを作成してから、コンテナー名のプレフィックスに基づいてコンテナーの一部を削除します。

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>サンプル スクリプト

[!code-azurecli-interactive[main](../../../cli_scripts/storage/delete-containers-by-prefix/delete-containers-by-prefix.sh?highlight=2-3 "Delete containers by prefix")]

## <a name="clean-up-deployment"></a>デプロイのクリーンアップ

次のコマンドを実行して、リソース グループ、残りのコンテナー、すべての関連リソースを削除します。

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>スクリプトの説明

このスクリプトでは、次のコマンドを使用して、コンテナー名のプレフィックスに基づいてコンテナーを削除します。 表内の各項目は、コマンドごとのドキュメントにリンクされています。

| command | メモ |
|---|---|
| [az group create](/cli/azure/group) | すべてのリソースを格納するリソース グループを作成します。 |
| [az storage account create](/cli/azure/storage/account) | 特定のリソース グループに Azure Storage アカウントを作成します。 |
| [az storage container create](/cli/azure/storage/container) | Azure Blob ストレージにコンテナーを作成します。 |
| [az storage container list](/cli/azure/storage/container) | Azure Storage アカウントのコンテナーを一覧表示します。 |
| [az storage container delete](/cli/azure/storage/container) | Azure Storage アカウントのコンテナーを削除します。 |

## <a name="next-steps"></a>次のステップ

Azure CLI の詳細については、[Azure CLI のドキュメント](/cli/azure)のページをご覧ください。

その他のストレージ CLI サンプル スクリプトは、[Azure Storage 用 Azure CLI サンプル](../blobs/storage-samples-blobs-cli.md)のページにあります。
