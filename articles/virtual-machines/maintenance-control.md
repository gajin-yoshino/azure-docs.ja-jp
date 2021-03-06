---
title: Azure portal を使用した Azure 仮想マシンのメンテナンス コントロールの概要
description: メンテナンス コントロールを使用して、ご利用の Azure VM にメンテナンスを適用するタイミングを制御する方法について説明します。
author: cynthn
ms.service: virtual-machines
ms.topic: conceptual
ms.workload: infrastructure-services
ms.date: 04/22/2020
ms.author: cynthn
ms.openlocfilehash: 950f4cfda73b40db0de8ba035868573cda1a5017
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "84675799"
---
# <a name="managing-platform-updates-with-maintenance-control"></a>メンテナンス コントロールによるプラットフォームの更新の管理 

メンテナンス コントロールを使用して、再起動が不要なプラットフォームの更新を管理します。 Azure は、信頼性、パフォーマンス、セキュリティを改善し、新機能を導入する目的で、インフラストラクチャを頻繁に更新しています。 ほとんどの更新は、ユーザーからは透過的に行われます。 ゲーム、メディア ストリーミング、金融取引などの一部のセンシティブなワークロードでは、数秒間であっても、メンテナンスのために VM がフリーズしたり切断したりすることが許されません。 メンテナンス コントロールが提供するオプションを使用すると、プラットフォームの更新を待機し、35 日間のローリング期間内にそれらの更新を適用できます。 

メンテナンス コントロールを使用すると、分離された VM や Azure 専用ホストに更新プログラムを適用するタイミングをユーザーが決定できます。

メンテナンス コントロールを使用すると、次のことができます。
- 更新プログラムを 1 つの更新プログラム パッケージにまとめる。
- 最大 35 日間待機して更新プログラムを適用する。 
- Azure Functions を使用して、メンテナンス期間のプラットフォームの更新を自動化する。
- メンテナンス構成が、複数のサブスクリプションやリソース グループ全体で機能するようにする。 

## <a name="limitations"></a>制限事項

- VM は、[専用ホスト](./linux/dedicated-hosts.md)上にあるか、[分離された VM サイズ](./linux/isolation.md)を使用して作成される必要があります。
- 35 日後に、更新プログラムが自動的に適用されます。
- ユーザーは、**リソース共同作成者**のアクセス権を持っている必要があります。

## <a name="management-options"></a>管理オプション

次のいずれかのオプションを使用して、メンテナンス構成を作成および管理できます。

- [Azure CLI](maintenance-control-cli.md)
- [Azure PowerShell](maintenance-control-powershell.md)
- [Azure Portal](maintenance-control-portal.md)

## <a name="next-steps"></a>次のステップ

詳細については、[メンテナンスと更新プログラム](maintenance-and-updates.md)に関するページを参照してください。
