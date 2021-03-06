---
title: Azure Monitor for VMs の有効化の概要
description: Azure Monitor for VMs のデプロイと構成の方法を説明します。 システム要件を確認してください。
ms.subservice: ''
ms.topic: conceptual
author: bwren
ms.author: bwren
ms.date: 06/25/2020
ms.openlocfilehash: 072f8fd44fa45648afd15cb40cba26bb427c7b56
ms.sourcegitcommit: 3543d3b4f6c6f496d22ea5f97d8cd2700ac9a481
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/20/2020
ms.locfileid: "86539620"
---
# <a name="enable-azure-monitor-for-vms-overview"></a>Azure Monitor for VMs の有効化の概要

この記事では、Azure Monitor for VMs を有効にして、次の正常性とパフォーマンスを監視するために使用できるオプションの概要について説明します。

- Azure の仮想マシン 
- Azure Virtual Machine Scale Sets
- Azure Arc に接続されているハイブリッド仮想マシン
- オンプレミスの仮想マシン
- 別のクラウド環境でホストされている仮想マシン  

Azure Monitor for VMs を設定する方法は、次のとおりです。

* Azure portal のメニューから直接 **[Insights]** を選択して、単一の Azure VM、Azure VMSS、または Azure Arc マシンを有効にします。
* Azure Policy を使用して、複数の Azure VM、Azure VMSS、または Azure Arc マシンを有効にします。 この方法を使用すると、既存および新規の VM とスケール セットに、必要な依存関係が確実にインストールされ、適切に構成されます。 準拠していない VM とスケール セットがレポートされるので、それらを有効にするかどうかと、それらを修復するかどうかを決めることができます。
* PowerShell を使用して、指定されたサブスクリプションまたはリソース グループにわたって、複数の Azure VM、Azure Arc VM、Azure VMSS、または Azure Arc マシンを有効にします。
* 企業ネットワークまたはその他のクラウド環境でホストされている VM または物理コンピューターを監視するために、Azure Monitor for VMs を有効にします。

## <a name="prerequisites"></a>前提条件

始める前に、次のセクションの情報を理解しておいてださい。 

>[!NOTE]
>このセクションで説明する次の情報は、[Service Map ソリューション](service-map.md)にも適用できます。  

### <a name="log-analytics"></a>Log Analytics

Azure Monitor for VMs は、次のリージョンで Log Analytics ワークスペースをサポートします。

- 米国中西部
- 米国西部
- 米国西部 2
- 米国中南部
- 米国東部
- 米国東部 2
- 米国中部
- 米国中北部
- US Gov アリゾナ州
- US Gov バージニア州
- カナダ中部
- 英国南部
- 北ヨーロッパ
- 西ヨーロッパ
- 東アジア
- 東南アジア
- インド中部
- 東日本
- オーストラリア東部
- オーストラリア南東部

>[!NOTE]
>Azure VM は任意のリージョンで監視できます。 VM 自体は、Log Analytics ワークスペースでサポートされているリージョンに限定されません。
>

Log Analytics ワークスペースがない場合は、次のいずれかのリソースを使用して作成できます。
* [Azure CLI](../../azure-monitor/learn/quick-create-workspace-cli.md)
* [PowerShell](../platform/powershell-workspace-configuration.md)
* [Azure Portal](../../azure-monitor/learn/quick-create-workspace.md)
* [Azure Resource Manager](../../azure-monitor/platform/template-workspace-configuration.md)

Azure portal で単一の Azure VM または仮想マシン スケール セットに対する監視を有効にしているときにも、ワークスペースを作成できます。

Azure Policy テンプレート、Azure PowerShell テンプレート、または Azure Resource Manager テンプレートを使用した大規模なシナリオを設定するには、*VMInsights* をインストールする必要があります。 これは、次のいずれか方法で実行できます。

* [Azure PowerShell](vminsights-enable-at-scale-powershell.md#set-up-a-log-analytics-workspace) を使用します。
* Azure Monitor for VMs の [ **[ポリシー対象範囲]** ](vminsights-enable-at-scale-policy.md#manage-policy-coverage-feature-overview) ページで、 **[ワークスペースの構成]** を選択します。 

### <a name="azure-arc-machines"></a>Azure Arc マシン
Azure Monitor for VMs は、Arc 拡張サービスが利用可能なリージョンの Azure Arc 対応サーバーで使用できます。 Arc 対応サーバーで Azure Monitor for VMs を有効にするには、ユーザーが Arc エージェントのバージョン 0.9 以降を実行している必要があります。

### <a name="supported-operating-systems"></a>サポートされるオペレーティング システム

次の表は、Azure Monitor for VMs でサポートされている Windows および Linux オペレーティング システムの一覧です。 メジャーおよびマイナーの Linux OS リリースとサポートされているカーネルのバージョンの詳細な一覧は、このセクションの後の方にあります。

|OS バージョン |パフォーマンス |マップ |
|-----------|------------|-----|
|Windows Server 2019 | X | X |
|Windows Server 2016 1803 | X | X |
|Windows Server 2016 | X | X |
|Windows Server 2012 R2 | X | X |
|Windows Server 2012 | X | X |
|Windows Server 2008 R2 | X | X|
|Windows 10 1803 | X | X |
|Windows 8.1 | X | X |
|Windows 8 | X | X |
|Windows 7 SP1 | X | X |
|Red Hat Enterprise Linux (RHEL) 6、7| X | X| 
|Ubuntu 18.04、16.04 | X | X |
|CentOS Linux 7、6 | X | X |
|SUSE Linux Enterprise Server (SLES) 12 | X | X |
|Debian 9.4、8 | X<sup>1</sup> | |

<sup>1</sup> Azure Monitor for VMs のパフォーマンス機能は、Azure Monitor からのみ使用できます。 Azure VM の左側のウィンドウから直接使用することはできません。

>[!NOTE]
>Linux オペレーティング システムでは、次のようになっています。
> - 既定と SMP Linux のカーネル リリースのみがサポートされています。
> - Physical Address Extension (PAE) や Xen などの非標準のカーネル リリースは、どの Linux ディストリビューションでもサポートされていません。 たとえば、リリースの文字列が *2.6.16.21-0.8-xen* であるシステムはサポートされていません。
> - カスタム カーネル (標準カーネルの再コンパイルを含む) はサポートされていません。
> - CentOSPlus カーネルはサポートされています。
> - Spectre の脆弱性のために、Linux カーネルに修正プログラムを適用する必要があります。 詳細については、Linux ディストリビューション ベンダーに問い合わせてください。

#### <a name="red-hat-linux-7"></a>Red Hat Linux 7

| OS バージョン | カーネル バージョン |
|:--|:--|
| 7.6 | 3.10.0-957 |
| 7.5 | 3.10.0-862 |
| 7.4 | 3.10.0-693 |

#### <a name="red-hat-linux-6"></a>Red Hat Linux 6

| OS バージョン | カーネル バージョン |
|:--|:--|
| 6.10 | 2.6.32-754 |
| 6.9 | 2.6.32-696 |

#### <a name="centosplus"></a>CentOSPlus

| OS バージョン | カーネル バージョン |
|:--|:--|
| 6.10 | 2.6.32-754.3.5<br>2.6.32-696.30.1 |
| 6.9 | 2.6.32-696.30.1<br>2.6.32-696.18.7 |

#### <a name="ubuntu-server"></a>Ubuntu Server

| OS バージョン | カーネル バージョン |
|:--|:--|
| 18.04 | 5.3.0-1020<br>5.0 (Azure で調整されたカーネルを含む)<br>4.18 *<br>4.15* |
| 16.04.3 | 4.15。* |
| 16.04 | 4.13.\*<br>4.11.\*<br>4.10.\*<br>4.8.\*<br>4.4.\* |

#### <a name="suse-linux-12-enterprise-server"></a>SUSE Linux 12 Enterprise Server

| OS バージョン | カーネル バージョン |
|:--|:--|
|12 SP4 | 4.12。* (Azure で調整されたカーネルを含む) |
|12 SP3 | 4.4.* |
|12 SP2 | 4.4.* |

#### <a name="debian"></a>Debian 

| OS バージョン | カーネル バージョン |
|:--|:--|
| 9 | 4.9 | 

### <a name="the-microsoft-dependency-agent"></a>Microsoft Dependency Agent

Azure Monitor for VMs のマップ機能では、Microsoft Dependency Agent からデータが取得されます。 Dependency Agent は、Log Analytics への接続に関して Log Analytics エージェントに依存しています。 そのため、お使いのシステムに Log Analytics エージェントをインストールし、Dependency Agent を使用して構成する必要があります。

単一の Azure VM に対して Azure Monitor for VMs を有効にするか、または大規模なデプロイ方法を使用するかにかかわらず、[Windows](../../virtual-machines/extensions/agent-dependency-windows.md) または [Linux](../../virtual-machines/extensions/agent-dependency-linux.md) 用 Azure VM Dependency Agent 拡張機能を使用し、エクスペリエンスの一部としてエージェントをインストールします。

>[!NOTE]
>このセクションで説明する次の情報は、[Service Map ソリューション](service-map.md)にも適用できます。  

ハイブリッド環境では、手動または自動化された方法で Dependency Agent をダウンロードしてインストールできます。

次の表では、ハイブリッド環境でマップ機能がサポートしている接続先ソースについて説明します。

| 接続先ソース | サポートされています | 説明 |
|:--|:--|:--|
| Windows エージェント | はい | Windows エージェントには、[Windows の Log Analytics エージェント](../../azure-monitor/platform/log-analytics-agent.md)の他に、Dependency Agent が必要です。 詳細については、[サポートされているオペレーティング システム](#supported-operating-systems)のセクションを参照してください。 |
| Linux エージェント | はい | Linux エージェントには、[Linux の Log Analytics エージェント](../../azure-monitor/platform/log-analytics-agent.md)の他に、Dependency Agent が必要です。 詳細については、[サポートされているオペレーティング システム](#supported-operating-systems)のセクションを参照してください。 |
| System Center Operations Manager 管理グループ | いいえ | |

Dependency Agent は、以下の場所からダウンロードできます。

| ファイル | OS | Version | SHA-256 |
|:--|:--|:--|:--|
| [InstallDependencyAgent-Windows.exe](https://aka.ms/dependencyagentwindows) | Windows | 9.10.4.10090 | B4E1FF9C1E5CD254AA709AEF9723A81F04EC0763C327567C582CE99C0C5A0BAE  |
| [InstallDependencyAgent-Linux64.bin](https://aka.ms/dependencyagentlinux) | Linux | 9.10.4.10090 | A56E310D297CE3B343AE8F4A6F72980F1C3173862D6169F1C713C2CA09660A9F |

## <a name="role-based-access-control"></a>ロールベースのアクセス制御

Azure Monitor for VMs の機能を有効にしてアクセスするには、"*Log Analytics 共同作成者*" ロールが必要です。 パフォーマンス、正常性、およびマップのデータを表示するには、Azure VM に対する "*監視閲覧者*" ロールが必要です。 Azure Monitor for VMs 用に Log Analytics ワークスペースを構成する必要があります。

Log Analytics ワークスペースへのアクセスを制御する方法の詳細については、「[ワークスペースを管理する](../../azure-monitor/platform/manage-access.md)」を参照してください。

## <a name="how-to-enable-azure-monitor-for-vms"></a>Azure Monitor for VMs を有効にする方法

この表で説明されているいずれかの方法で、Azure Monitor for VMs を有効にします。

| デプロイの状態 | Method | 説明 |
|------------------|--------|-------------|
| 単一の Azure VM、Azure VMSS、または Azure Arc マシン | [ポータルから有効にする](vminsights-enable-single-vm.md) | Azure portal のメニューから直接 **[Insights]** を選択します。 |
| 複数の Azure VM、Azure VMSS、または Azure Arc マシン | [Azure Policy を介して有効にする](vminsights-enable-at-scale-policy.md) | Azure Policy を使用して、VM または VMSS の作成時に自動的に有効にします。 |
| | [Azure PowerShell または Azure Resource Manager テンプレートを介して有効にする](vminsights-enable-at-scale-powershell.md) | Azure PowerShell テンプレートまたは Azure Resource Manager テンプレートを使用して、指定されたサブスクリプションまたはリソース グループにわたって、複数の Azure VM、Azure Arc VM、または Azure VMSS を有効にします。 |
| ハイブリッド クラウド | [ハイブリッド環境用に有効にする](vminsights-enable-hybrid-cloud.md) | ご自身のデータセンターやその他のクラウド環境でホストされている VM または物理コンピューターにデプロイできます。 |

## <a name="management-packs"></a>管理パック

Azure Monitor for VMs が有効になっていて、Log Analytics ワークスペースで構成されている場合、管理パックはそのワークスペースに対してレポートを行うすべての Windows コンピューターに転送されます。 Log Analytics ワークスペースと [System Center Operations Manager 管理グループを統合](../../azure-monitor/platform/om-agents.md)している場合は、Service Map 管理パックが、管理グループから、管理グループにレポートを行う Windows コンピューターにデプロイされます。  

この管理パックは、*Microsoft.IntelligencePacks.ApplicationDependencyMonitor* という名前で、 `%Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs\` フォルダーに書き込まれます。 管理パックで使用されるデータ ソースは、`%Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources\<AutoGeneratedID>\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll` です。

## <a name="diagnostic-and-usage-data"></a>診断と使用状況データ

Microsoft は、お客様による Azure Monitor サービスの使用を通して、使用状況とパフォーマンス データを自動的に収集します。 Microsoft はこのデータを使用して、サービスの品質、セキュリティ、および整合性の向上に努めています。 

正確で効果的なトラブルシューティング機能を提供するために、マップ機能にはソフトウェアの構成に関するデータが含まれています。 このデータによって、オペレーティング システムとバージョン、IP アドレス、DNS 名、ワークステーション名などの情報が提供されます。 名前や住所などの連絡先情報は収集されません。

データの収集と使用の詳細については、「[Microsoft オンライン サービスのプライバシーに関する声明](https://go.microsoft.com/fwlink/?LinkId=512132)」を参照してください。

[!INCLUDE [GDPR-related guidance](../../../includes/gdpr-dsr-and-stp-note.md)]

VM の監視が有効になったので、Azure Monitor for VMs での分析に監視情報を使用できます。

## <a name="next-steps"></a>次のステップ

パフォーマンスの監視機能の使用方法については、[Azure Monitor for VMs のパフォーマンスの表示](vminsights-performance.md)に関する記事をご覧ください。 検出されたアプリケーションの依存関係を表示するには、[Azure Monitor for VMs のマップの表示](vminsights-maps.md)に関する記事をご覧くださいい。
