---
title: "Azure Machine Learning データ準備の実行環境とデータ環境のサポートされている組み合わせ | Microsoft Docs"
description: "このドキュメントでは、Azure Machine Learning データ準備用の各種ランタイムおよびデータ ソースのサポートされている組み合わせの全一覧を示します"
services: machine-learning
author: euangMS
ms.author: euang
manager: lanceo
ms.reviewer: 
ms.service: machine-learning
ms.workload: data-services
ms.custom: 
ms.devlang: 
ms.topic: article
ms.date: 09/15/2017
ms.openlocfilehash: 413bc8a0e0347498c004b93fb37f51d86ad029f5
ms.sourcegitcommit: 2d1153d625a7318d7b12a6493f5a2122a16052e0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2017
---
# <a name="supported-matrix-for-this-release"></a>このリリースでサポートされているマトリックス 
コードで Azure Machine Learning データ ソースを使用して、または Azure Machine Learning データ準備でデータを読み込み、Pandas または Spark データフレームのどちらかを取得するとき、実験的コンピューティング環境とデータの場所の組み合わせとして、次のものがサポートされています。

|     |ローカル ファイル  |Azure BLOB ストレージ  |SQL Server データベース***  |
|---------|---------|---------|---------|---------|
|ローカルの Python    |     サポートされています    |サポートされていません         | サポートされていません        |         |
|Docker (Linux VM) Python     |プロジェクト ファイルのみでサポート*         | サポートされていません        |        サポートされていません |         |
|Docker (Linux VM) PySpark     |プロジェクト ファイルのみでサポート*     |サポートされています         | サポートされています**        |         |
|Azure Data Science Virtual Machine Python     |プロジェクト ファイルのみでサポート*         |サポートされていません         |サポートされていません         |         |
|Azure Data Science Virtual Machine PySPark     | プロジェクト ファイルのみでサポート*        |サポートされていません         |サポートされていません         |         |
|Azure HDInsight PySpark     | サポートされていません        |サポートされています         |サポートされています**         |         |
|Azure HDInsight Python     | サポートされていません        | サポートされていません        | サポートされていません        |         |

Azure Data Lake Store は現在、どのコンピューティング ターゲット向けにもサポートされていません。

*ローカル ファイル パスが使用されるとき、プロジェクト内部のファイルはコンピューティング環境にコピーされた後、そこで読み取られます。 プロジェクトの外にあるファイルはコピーされず、コンピューティング環境ではパスが解決されなくなります。 ローカルで実行するときにコードがローカル ファイルを使用できるように、Data Source Substitution の使用を検討してください。 その後、別の実行構成用に Azure Storage BLOB に切り替えます。 データ ソースでサンプリング サポートを使用し、特定の実行構成においてのみ大規模データに対する実行を管理することもできます。

**Maven JDBC SQL Server ドライバー 6.2.1 を使用します。 このパッケージ (または互換性のあるパッケージ) が、コンピューティング環境用の spark_dependencies.yml ファイルに含まれていることを確認する必要があります。

***コンピューティング環境からデータベースと通信できるという条件のもと、Azure SQL Database、Azure SQL Data Warehouse、または SQL Server をサポートします。 
