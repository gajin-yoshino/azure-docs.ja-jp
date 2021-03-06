---
title: インクルード ファイル
description: インクルード ファイル
services: container-registry
author: dlepow
ms.service: container-registry
ms.topic: include
ms.date: 01/23/2019
ms.author: danlep
ms.custom: include file
ms.openlocfilehash: b10bf18fde850223bda80a597f448747558113f1
ms.sourcegitcommit: 4ac596f284a239a9b3d8ed42f89ed546290f4128
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2020
ms.locfileid: "84752196"
---
## <a name="push-image-to-registry"></a>レジストリにイメージをプッシュする

Azure Container Registry にイメージをプッシュするには、まずイメージを用意する必要があります。 ローカル コンテナー イメージがまだない場合は、次の [docker pull][docker-pull] コマンドを実行して、既存のイメージを Docker Hub からプルします。 この例では、`hello-world` イメージをプルします。

```
docker pull hello-world
```

イメージをレジストリにプッシュするには、レジストリのログイン サーバーの完全修飾名を使用して、そのイメージにタグを付けておく必要があります。 ログイン サーバー名は、 *\<registry-name\>.azurecr.io* (すべて小文字) という形式です (*mycontainerregistry007.azurecr.io* など)。

[docker tag][docker-tag] コマンドを使用してイメージにタグ付けします。 `<login-server>` を ACR インスタンスのログイン サーバー名で置き換えます。

```
docker tag hello-world <login-server>/hello-world:v1
```

最後に、[docker push][docker-push] を使用して、レジストリ インスタンスにイメージをプッシュします。 `<login-server>` をレジストリ インスタンスのログイン サーバー名で置き換えます。 この例では、**hello-world** レポジトリを作成します。これには、`hello-world:v1` イメージが含まれています。

```
docker push <login-server>/hello-world:v1
```

コンテナー レジストリにイメージをプッシュした後は、ローカルの Docker 環境から `hello-world:v1` イメージを削除します (この [docker rmi][docker-rmi] コマンドは、Azure コンテナー リポジトリ内の **hello-world** リポジトリからイメージを削除しないことに注意してください)。

```
docker rmi <login-server>/hello-world:v1
```

<!-- LINKS - External -->
[docker-push]: https://docs.docker.com/engine/reference/commandline/push/
[docker-pull]: https://docs.docker.com/engine/reference/commandline/pull/
[docker-rmi]: https://docs.docker.com/engine/reference/commandline/rmi/
[docker-run]: https://docs.docker.com/engine/reference/commandline/run/
[docker-tag]: https://docs.docker.com/engine/reference/commandline/tag/

<!-- LINKS - Internal -->

