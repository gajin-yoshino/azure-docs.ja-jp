---
title: 概念 - ロールベースのアクセス制御 (RBAC)
description: Azure VMware Solution (AVS) のロールベースのアクセス制御の主な機能について説明します
ms.topic: conceptual
ms.date: 06/30/2020
ms.openlocfilehash: 8628c88c300ef8ed271f5e06a8e8dfae40231fec
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85656772"
---
# <a name="role-based-access-control-rbac-for-azure-vmware-solution-avs"></a>Azure VMware Solution (AVS) のロールベースのアクセス制御 (RBAC)

vCenter および ESXi オンプレミス展開では、管理者は vCenter administrator@vsphere.local アカウントにアクセス可能であり、その他の Active Directory (AD) ユーザーまたはグループが割り当てられている場合があります。 ただし、Azure VMware Solution (AVS) デプロイでは、管理者は管理者ユーザー アカウントにアクセスすることはできませんが、AD ユーザーとグループを vCenter の CloudAdmin ロールに割り当てることができます。  また、AVS プライベート クラウド ユーザーには、クラスター、ホスト、データストア、分散仮想スイッチなど、Microsoft がサポートおよび管理する特定の管理コンポーネントへのアクセスまたは構成を行うアクセス許可がありません。


AVS では、vCenter に、組み込みの CloudAdmin ロールに割り当てられている cloudadmin という組み込みのローカル ユーザーがあります。 ローカルの cloudadmin ユーザーは、AD で追加のユーザーを設定するために使用されます。 CloudAdmin ロールには、一般に、プライベート クラウド (仮想マシン、リソース プール、データストア、ネットワーク) でワークロードを作成および管理するアクセス許可があります。 AVS の CloudAdmin ロールには、他の VMware クラウド ソリューションとは異なる一連の vCenter 特権があります。   

> [!NOTE]
> 現在、AVS では、vCenter または AVS ポータルにカスタム ロールが提供されていません。 

## <a name="avs-cloudadmin-role-on-vcenter"></a>vCenter の AVS CloudAdmin ロール

AVS プライベート クラウド vCenter で AVS CloudAdmin ロールに付与された特権を確認できます。

1. SDDC vSphere Client にログインし、 **[Menu]\(メニュー\)**  >  **[Administration]\(管理\)** に移動します。
1. **[Access Control]\(アクセス制御\)** で、 **[Roles]\(ロール\)** を選択します。
1. ロールの一覧から **[CloudAdmin]** を選択し、 **[Privileges]\(特権\)** を選択します。 

   :::image type="content" source="media/rbac-cloudadmin-role-privileges.png" alt-text="vSphere Client で CloudAdmin ロールの特権を確認する方法":::

AVS の CloudAdmin ロールには、vCenter に対する次の特権があります。 各特権の詳細については、[VMware の製品ドキュメント](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.security.doc/GUID-ED56F3C4-77D0-49E3-88B6-B99B8B437B62.html)を参照してください。

| 特権 | 説明 |
| --------- | ----------- |
| **アラーム** | アラートの確認<br />アラームの作成<br />アラーム アクションの無効化<br />アラームの変更<br />アラームの削除<br />アラームの状態の設定 |
| **アクセス許可** | アクセス許可の変更 |
| **コンテンツ ライブラリ** | ライブラリ項目の追加<br />発行されたライブラリのサブスクリプションの作成<br />ローカル ライブラリの作成<br />サブスクライブ済みライブラリの作成<br />ライブラリ項目の削除<br />ローカル ライブラリの削除<br />サブスクライブ済みライブラリの削除<br />発行されたライブラリのサブスクリプションの削除<br />ファイルのダウンロード<br />ライブラリ項目の強制削除<br />サブスクライブ済みライブラリの強制削除<br />ストレージのインポート<br />サブスクリプション情報のプローブ<br />ライブラリ項目のサブスクライバーへの発行<br />ライブラリのサブスクライバーへの発行<br />ストレージの読み取り<br />ライブラリ項目の同期<br />サブスクライブ済みライブラリの同期<br />イントロスペクションの入力<br />構成設定の更新<br />ファイルの更新<br />ライブラリの更新<br />ライブラリ項目の更新<br />ローカル ライブラリの更新<br />サブスクライブ済みライブラリの更新<br />発行されたライブラリのサブスクリプションの更新<br />構成設定の表示 |
| **暗号化操作** | 直接アクセス |
| **データストア** | 領域の割り当て<br />データストアを参照する<br />データストアの構成<br />低レベルのファイル操作<br />ファイルの削除<br />仮想マシン メタデータの更新 |
| **フォルダー** | フォルダーの作成<br />フォルダーの削除<br />フォルダーの移動<br />フォルダー名の変更 |
| **グローバル** | タスクの取り消し<br />グローバル タグ<br />Health<br />イベントのログ記録<br />カスタム属性の管理<br />サービス マネージャー<br />カスタム属性の設定<br />システム タグ |
| **Host** | vSphere レプリケーション<br />&#160;&#160;&#160;&#160;レプリケーションの管理 |
| **vSphere のタグ付け** | vSphere タグの割り当てと割り当て解除<br />vSphere タグの作成<br />vSphere タグ カテゴリの作成<br />vSphere タグの削除<br />vSphere タグ カテゴリの削除<br />vSphere タグの編集<br />vSphere タグ カテゴリの編集<br />カテゴリの UsedBy フィールドの変更<br />タグの UsedBy フィールドの変更 |
| **Network** | ネットワークの割り当て |
| **リソース** | Apply recommendation<br />リソース プールへの vApp の割り当て<br />リソース プールへの仮想マシンの割り当て<br />リソース プールの作成<br />電源がオフの仮想マシンの移行<br />電源がオンの仮想マシンの移行<br />リソース プールの変更<br />リソース プールの移動<br />vMotion のクエリ<br />リソース プールの削除<br />リソース プールの名前変更 |
| **スケジュールされたタスク** | タスクを作成する<br />タスクの変更<br />タスクの削除<br />タスクの実行 |
| **セッション** | Message<br />セッションの検証 |
| **プロファイル** | プロファイル駆動型ストレージ ビュー |
| **ストレージ ビュー** | 表示 |
| **vApp** | 仮想マシンの追加<br />リソース プールの割り当て<br />vApp の割り当て<br />複製<br />作成<br />削除<br />エクスポート<br />[インポート]<br />詳細ビュー<br />電源オフ<br />電源投入<br />[名前の変更]<br />[中断]<br />Unregister<br />OVF 環境の表示<br />vApp アプリケーション構成<br />vApp インスタンス構成<br />vApp managedBy 構成<br />vApp リソース構成 |
| **仮想マシン** | 構成の変更<br />&#160;&#160;&#160;&#160;ディスク リースの取得<br />&#160;&#160;&#160;&#160;既存のディスクの追加<br />&#160;&#160;&#160;&#160;新しいディスクの追加<br />&#160;&#160;&#160;&#160;デバイスの追加または削除<br />&#160;&#160;&#160;&#160;詳細な構成<br />&#160;&#160;&#160;&#160;CPU 数の変更<br />&#160;&#160;&#160;&#160;メモリの変更<br />&#160;&#160;&#160;&#160;設定の変更<br />&#160;&#160;&#160;&#160;スワップファイル配置の変更<br />&#160;&#160;&#160;&#160;リソースの変更<br />&#160;&#160;&#160;&#160;ホスト USB デバイスの構成<br />&#160;&#160;&#160;&#160;raw デバイスの構成<br />&#160;&#160;&#160;&#160;managedBy の構成<br />&#160;&#160;&#160;&#160;接続設定の表示<br />&#160;&#160;&#160;&#160;仮想ディスクの拡張<br />&#160;&#160;&#160;&#160;デバイスの設定の変更<br />&#160;&#160;&#160;&#160;フォールト トレランス互換性のクエリ<br />&#160;&#160;&#160;&#160;所有者のないファイルのクエリ<br />&#160;&#160;&#160;&#160;パスからの再読み込み<br />&#160;&#160;&#160;&#160;ディスクの削除<br />&#160;&#160;&#160;&#160;名前の変更<br />&#160;&#160;&#160;&#160;ゲスト情報のリセット<br />&#160;&#160;&#160;&#160;注釈の設定<br />&#160;&#160;&#160;&#160;ディスク変更追跡の切り替え<br />&#160;&#160;&#160;&#160;フォークの親の切り替え<br />&#160;&#160;&#160;&#160;仮想マシン互換性のアップグレード<br />インベントリの編集<br />&#160;&#160;&#160;&#160;既存からの作成<br />&#160;&#160;&#160;&#160;新規作成<br />&#160;&#160;&#160;&#160;移動<br />&#160;&#160;&#160;&#160;登録<br />&#160;&#160;&#160;&#160;削除<br />&#160;&#160;&#160;&#160;登録解除<br />ゲスト操作<br />&#160;&#160;&#160;&#160;ゲスト操作エイリアスの変更<br />&#160;&#160;&#160;&#160;ゲスト操作エイリアスのクエリ<br />&#160;&#160;&#160;&#160;ゲスト操作の変更<br />&#160;&#160;&#160;&#160;ゲスト操作プログラム実行<br />&#160;&#160;&#160;&#160;ゲスト操作クエリ<br />相互作用<br />&#160;&#160;&#160;&#160;質問に答える<br />&#160;&#160;&#160;&#160;仮想マシンに対するバックアップ操作<br />&#160;&#160;&#160;&#160;CD メディアの構成<br />&#160;&#160;&#160;&#160;フロッピー メディアの構成<br />&#160;&#160;&#160;&#160;デバイスの接続<br />&#160;&#160;&#160;&#160;コンソール対話<br />&#160;&#160;&#160;&#160;スクリーンショットの作成<br />&#160;&#160;&#160;&#160;すべてのディスクのデフラグ<br />&#160;&#160;&#160;&#160;ドラッグ アンド ドロップ<br />&#160;&#160;&#160;&#160;VIX API によるゲスト オペレーティング システム管理<br />&#160;&#160;&#160;&#160;USB HID スキャン コードの挿入<br />&#160;&#160;&#160;&#160;VMware ツールのインストール<br />&#160;&#160;&#160;&#160;一時停止または一時停止解除<br />&#160;&#160;&#160;&#160;ワイプまたはシュリンク操作の実行<br />&#160;&#160;&#160;&#160;電源オフ<br />&#160;&#160;&#160;&#160;電源オン<br />&#160;&#160;&#160;&#160;仮想マシン上のセッションの記録<br />&#160;&#160;&#160;&#160;仮想マシン上のセッションの再生<br />&#160;&#160;&#160;&#160;一時停止<br />&#160;&#160;&#160;&#160;フォールト トレランスの一時停止<br />&#160;&#160;&#160;&#160;フェールオーバーのテスト<br />&#160;&#160;&#160;&#160;セカンダリ VM の再起動のテスト<br />&#160;&#160;&#160;&#160;フォールト トレランスの無効化<br />&#160;&#160;&#160;&#160;フォールト トレランスの有効化<br />プロビジョニング<br />&#160;&#160;&#160;&#160;ディスク アクセスの許可<br />&#160;&#160;&#160;&#160;ファイル アクセスの許可<br />&#160;&#160;&#160;&#160;読み取り専用ディスク アクセスの許可<br />&#160;&#160;&#160;&#160;仮想マシンのダウンロードの許可<br />&#160;&#160;&#160;&#160;テンプレートのクローン<br />&#160;&#160;&#160;&#160;仮想マシンのクローン<br />&#160;&#160;&#160;&#160;仮想マシンからのテンプレートの作成<br />&#160;&#160;&#160;&#160;ゲストのカスタマイズ<br />&#160;&#160;&#160;&#160;テンプレートのデプロイ<br />&#160;&#160;&#160;&#160;テンプレートとしてマーク<br />&#160;&#160;&#160;&#160;カスタマイズ仕様の変更<br />&#160;&#160;&#160;&#160;ディスクの昇格<br />&#160;&#160;&#160;&#160;カスタマイズ仕様の読み取り<br />サービス構成<br />&#160;&#160;&#160;&#160;通知の許可<br />&#160;&#160;&#160;&#160;グローバル イベント通知のポーリングの許可<br />&#160;&#160;&#160;&#160;サービスの構成の更新<br />&#160;&#160;&#160;&#160;サービス構成の変更<br />&#160;&#160;&#160;&#160;サービス構成のクエリ<br />&#160;&#160;&#160;&#160;サービス構成の読み取り<br />スナップショットの管理<br />&#160;&#160;&#160;&#160;スナップショットの作成<br />&#160;&#160;&#160;&#160;スナップショットの削除<br />&#160;&#160;&#160;&#160;スナップショット名の変更<br />&#160;&#160;&#160;&#160;スナップショットを元に戻す<br />vSphere レプリケーション<br />&#160;&#160;&#160;&#160;レプリケーションの構成<br />&#160;&#160;&#160;&#160;レプリケーションの管理<br />&#160;&#160;&#160;&#160;レプリケーションの監視 |
| **vService** | 依存関係の作成<br />依存関係の破棄<br />依存関係の再構成<br />依存関係の更新 |



## <a name="next-steps"></a>次のステップ

各特権の詳細については、[VMware の製品ドキュメント](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.security.doc/GUID-ED56F3C4-77D0-49E3-88B6-B99B8B437B62.html)を参照してください。

<!-- LINKS - internal -->

<!-- LINKS - external-->
[VMware product documentation]: https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.security.doc/GUID-ED56F3C4-77D0-49E3-88B6-B99B8B437B62.html

