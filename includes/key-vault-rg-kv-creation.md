---
author: msmbaldwin
ms.service: key-vault
ms.topic: include
ms.date: 07/20/2020
ms.author: msmbaldwin
ms.openlocfilehash: 2b5533da1e81cf37dfba47bf84bd05f083d62dea
ms.sourcegitcommit: 3d79f737ff34708b48dd2ae45100e2516af9ed78
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "87013117"
---
このクイックスタートでは、あらかじめ作成しておいた Azure キー コンテナーを使用します。 キー コンテナーは、[Azure CLI のクイックスタート](/azure/key-vault/general/quick-create-cli)、[Azure PowerShell のクイックスタート](/azure/key-vault/general/quick-create-powershell)、または [Azure portal のクイックスタート](/azure/key-vault/general/quick-create-portal)の手順に従って作成できます。 

また、以下の Azure CLI または Azure PowerShell コマンドを実行するだけでもかまいません。

> [!Important]
> 各キー コンテナーには一意の名前が必要です。 次の例では、<your-unique-keyvault-name> をお使いのキー コンテナーの名前に置き換えてください。

```azurecli
az group create --name "myResourceGroup" -l "EastUS"

az keyvault create --name <your-unique-keyvault-name> -g "myResourceGroup"
```

```azurepowershell
New-AzResourceGroup -Name myResourceGroup -Location EastUS

New-AzKeyVault -Name <your-unique-keyvault-name> -ResourceGroupName "myResourceGroup" -Location "EastUS"
```