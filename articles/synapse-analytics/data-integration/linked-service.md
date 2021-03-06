---
title: リンクされたサービスをセキュリティで保護する
description: マネージド Vnet を使用してリンクされたサービスをプロビジョニングしてセキュリティで保護する方法について説明します
services: synapse-analytics
author: acomet
ms.service: synapse-analytics
ms.topic: how-to
ms.subservice: ''
ms.date: 04/15/2020
ms.author: acomet
ms.reviewer: jrasnick
ms.openlocfilehash: 7c7cf8ec7297b3c0ef855936becc3c06a5120a38
ms.sourcegitcommit: 3543d3b4f6c6f496d22ea5f97d8cd2700ac9a481
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/20/2020
ms.locfileid: "86496079"
---
# <a name="securing-a-linked-service-with-private-links"></a>Private Links を使用したリンクされたサービスのセキュリティ保護 

この記事では、プライベート エンドポイントを使用して Synapse 内のリンクされたサービスをセキュリティで保護する方法について説明します。

## <a name="prerequisites"></a>前提条件

* **Azure サブスクリプション**:Azure サブスクリプションをお持ちでない場合は、開始する前に[無料の Azure アカウント](https://azure.microsoft.com/free/)を作成してください。
* **Microsoft Azure Storage アカウント**:"*ソース*" データ ストアとして Azure Data Lake Gen 2 を使用します。 ストレージ アカウントがない場合の作成手順については、「[Azure Storage アカウントの作成](../../storage/blobs/data-lake-storage-quickstart-create-account.md)」を参照してください。 ストレージ アカウントにそれにアクセスするための Synapse Studio IP フィルタリングが用意されていること、**選択されたネットワーク**のみにストレージ アカウントへのアクセスを許可していることを確認します。 **[ファイアウォールと仮想ネットワーク]** ブレードでの設定は次の図のようになります。

![セキュリティで保護されたストレージ アカウント](./media/secure-storage-account.png)

## <a name="create-a-linked-service-with-private-links"></a>Private Link を使用してリンクされたサービスを作成する

Azure Synapse Analytics で、リンクされたサービスとは、他のサービスへの接続情報を定義した場所です。 このセクションでは、リンクされたサービスとして Azure Synapse Analytics と Azure Data Lake Gen 2 を追加します。

1. Azure Synapse Studio を開き、 **[管理]** タブに移動します。
1. **[外部接続]** で、 **[リンクされたサービス]** を選択します。
1. リンクされたサービスを追加するには、 **[新規]** をクリックします。
1. リストから [Azure Data Lake Storage Gen2] タイルを選択し、 **[続行]** をクリックします。
1. **[Interactive Authoring]\(インタラクティブな作成\)** を必ず有効にしてください。 これは有効になるまでに 1 分程かかる場合があります。 
1. ご利用の認証資格情報を入力します。 アカウント キー、サービス プリンシパル、およびマネージド ID が現在サポートされている認証の種類です。 [テスト接続] をクリックして、ご利用の資格情報が正しいことを確認します。
1. **[テスト接続]** を選択します。プライベート エンドポイントを作成および承認しなければストレージ アカウントにアクセスできないようになっているため、これは失敗するはずです。 エラー メッセージ内に、**プライベート エンド ポイント**を作成するためのリンクが表示されます。それをたどることで、次の部分に進むことができます。 そのリンクをたどる場合は、次の部分をスキップします。
1. 入力し終えたら **[作成]** を選択します。

## <a name="create-a-managed-private-endpoint"></a>マネージド プライベート エンドポイントを作成する

上記の接続をテストするときにハイパーリンクをクリックしなかった場合は、次のパスに従います。 次に、上で作成したリンクされたサービスに接続するマネージド プライベート エンドポイントを作成する必要があります。

1. **[管理]** タブに移動します。
1. **[Managed Virtual Networks]\(マネージド仮想ネットワーク\)** セクションに移動します。
1. マネージド プライベート エンドポイントで、 **[+ 新規]** を選択します。
1. リストから [Azure Data Lake Storage Gen2] タイルを選択し、 **[続行]** を選択します。
1. 上で作成したストレージ アカウントの名前を入力します。
1. **[作成]**
1. 数秒待った後で、作成されたプライベート リンクに承認が必要であることが示されます。

## <a name="approval-of-a-private-link"></a>プライベート リンクの承認
1. 上で作成したプライベート エンドポイントを選択します。 ストレージ アカウント レベルでプライベート エンドポイントを承認するためのハイパーリンクが表示されます。 "*別の方法としては、Azure portal ストレージ アカウントに直接アクセスし、 **[プライベート エンドポイント接続]** ブレードにアクセスします。* "
1. Studio で作成したプライベート エンドポイントを選択し、 **[承認]** を選択します。
1. 説明を追加して、 **[はい]** をクリックします。
1. **[管理]** タブの **[Managed Virtual Networks]\(マネージド仮想ネットワーク\)** セクションで Synapse Studio に戻ります。
1. 使用するプライベート エンドポイントに対して承認が反映されるまで、約 1 分かかります。

## <a name="check-the-connection-works"></a>接続の動作を確認する
1. **[管理]** タブに移動して、作成したリンクされたサービスを選択します。
1. **[Interactive Authoring]\(インタラクティブな作成\)** がアクティブになっていることを確認します。
1. **[接続テスト]** を選択します。 接続が成功したことがわかります。

これで、Synapse とリンクされたサービスとの間にセキュリティで保護されたプライベート接続が確立されました。

## <a name="next-steps"></a>次のステップ

Synapse Analytics でのマネージド プライベート エンドポイントについてさらに理解を深めるには、[Synapse マネージド プライベート エンドポイントの概念](data-integration-data-lake.md)に関する記事を参照してください。

Synapse Analytics のデータ統合の詳細については、[Data Lake へのデータの取り込み](data-integration-data-lake.md)に関する記事を参照してください。
