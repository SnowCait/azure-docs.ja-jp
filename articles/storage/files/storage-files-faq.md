---
title: "Azure Files についてよく寄せられる質問 | Microsoft Docs"
description: "Azure Files についてよく寄せられる質問とその回答を紹介します。"
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 10/13/2017
ms.author: renash
ms.openlocfilehash: 91c46ea0897f83811cfa5c1a8b67677caff14569
ms.sourcegitcommit: 76a3cbac40337ce88f41f9c21a388e21bbd9c13f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2017
---
# <a name="frequently-asked-questions-about-azure-files"></a>Azure Files に関してよく寄せられる質問
[Azure Files](storage-files-introduction.md) は、クラウド上で、業界標準の[サーバー メッセージ ブロック (SMB) プロトコル](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx) (別称 Common Internet File System または CIFS) を介してアクセスできる、完全に管理されたファイル共有を提供します。 Azure Files は、クラウドまたはオンプレミスにある Windows、macOS、および Linux に同時にマウントできます。 さらに、データが使用されている場所の近くから高速アクセスするため、Azure File Sync (プレビュー) を使用して、Windows サーバーに Azure File 共有をキャッシュできます。

この記事では、Azure File Sync を含む、Azure File 機能に関してよく寄せられる質問の一部について説明します。質問に対する回答がここで見つからない場合は、次のチャネルを通じて遠慮なくお問い合わせください (上から順に)。

1. この記事のコメント セクション。
2. [Azure Storage フォーラム](https://social.msdn.microsoft.com/Forums/home?forum=windowsazuredata)
3. [Azure Files UserVoice](https://feedback.azure.com/forums/217298-storage/category/180670-files) 
4. Microsoft サポート: 新しいサポート ケースを作成するには、Azure Portal の [ヘルプとサポート] タブに移動し、[新しいサポート要求] をクリックします。

## <a name="general"></a>全般
* <a id="why-files-useful"></a>**Azure Files はどのように便利なのですか。**  
   Azure Files は、クラウド内にファイル共有を作成することを可能にします。その際に、物理サーバーやデバイス/アプライアンスのオーバーヘッドを管理する必要はありません。 これは、OS 更新プログラムを適用して、不良ディスクを置き換える時間を短縮できることを意味します。単調な作業をすべて、ユーザーに代わって実行します。 Azure Files を利用できるシナリオの詳細については、「[Azure Files の適用ケース](storage-files-introduction.md#why-azure-files-is-useful)」をご覧ください。

* <a id="file-access-options"></a>**Azure Files でファイルにアクセスするさまざまな方法を挙げてください。**  
    SMB 3.0 プロトコルを使用してローカル コンピューターにファイル共有をマウントするか、[ストレージ エクスプローラー](http://storageexplorer.com/)などのツールを使用してファイル共有内のファイルにアクセスできます。 アプリケーションから、ストレージ クライアント ライブラリ、REST API、 PowerShell、または CLI を使用して、Azure File 共有内のファイルにアクセスできます。

* <a id="what-is-afs"></a>**Azure ファイル同期とは何ですか。**  
    Azure ファイル同期を使用すると、オンプレミスのファイル サーバーの柔軟性、パフォーマンス、互換性を損なわずに Azure Files で組織のファイル共有を一元化できます。 これは、Windows Server を Azure ファイル共有のクイック キャッシュに変換することで行います。 Windows Server で使用可能な任意のプロトコル (SMB、NFS、FTPS など) を使用してデータにローカル アクセスすることができ、世界中に必要な数だけキャッシュを持つことができます。

* <a id="files-versus-blobs"></a>**データに Azure ファイル共有または Azure Blob ストレージを使用する理由を教えてください。**  
    Azure Files と Azure Blob ストレージは両方とも、クラウドで大量のデータを格納する手段を提供していますが、やや目的に役立ちます。 Azure Blob ストレージは、構造化されていないデータを格納する必要がある大規模なクラウド ネイティブ アプリケーションに役立ちます。 パフォーマンスとスケールを最大限に高めるには、Azure Blob ストレージは、実際のファイル システムよりも単純なストレージの抽出になります。 さらに、Azure Blob ストレージは、REST ベースのクライアント ライブラリ経由でのみ (または REST ベースのプロトコルを介して直接) アクセスできます。

    一方で、Azure Files では、何年も使用しているオンプレミスのオペレーティング システムから愛用しているすべてのファイルを抽出して、明確にファイル システムを形成しようとします。 Azure Blob ストレージと同様に、Azure Files では 1 つの REST インターフェイスと REST ベースのクライアント ライブラリを提供していますが、Azure Blob ストレージとは違って、Azure Files では Azure ファイル共有への SMB アクセスも提供しています。 これは、Windows、Linux、または macOS、オンプレミスまたはクラウドの VM に Azure ファイル共有を直接マウントできることを意味します。コードを記述したり、特別なドライバーをファイル システムにアタッチする必要はありません。 さらに、データが使用されている領域の周辺に高速でアクセスするために、Azure ファイル同期を使用してオンプレミスのファイル サーバー上に Azure ファイル共有をキャッシュできます。 
   
    Azure Files と Azure Blob ストレージ間の違いに関する詳細な議論については、「[Azure BLOB、Azure Files、Azure ディスクの使い分け](../common/storage-decide-blobs-files-disks.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)」をご覧ください。 Azure Blob ストレージの詳細については、「[Blob ストレージの概要](../blobs/storage-blobs-introduction.md)」をご覧ください。

* <a id="files-versus-disks"></a>**Azure ファイル共有または Azure ディスクを使用する理由を教えてください。**  
    Azure ディスクは単なるディスクです。 スタンドアロンのディスクは、単独ではあまり便利ではありません。Azure ディスクから値を取得するために、Azure で実行されている仮想マシンにアタッチする必要があります。 Azure ディスクは、OS システム ディスク、OS のスワップ領域、またはアプリケーションの専用ストレージとして、オンプレミス サーバーでディスクを使用するあらゆるコンテンツに対して利用できます。 Azure ディスクの興味深い使用方法として、Azure ファイル共有を使う場所とまったく同じ場所で使用するために、クラウドにファイル サーバーを作成することです。 Azure VM にファイル サーバーをデプロイすることは、Azure Files では現在サポートされていないデプロイ オプションを必要とする場合 (NFS プロトコル サポートやプレミアム ストレージなど) に Azure でファイル ストレージを取得するための、高パフォーマンスの優れた方法です。 

    一方で、Azure ディスクを保持するファイル サーバーをバックエンド ストレージとして実行すると、いくつかの理由から、通常は Azure ファイル共有を使用するよりも高コストになります。 第一に、ディスク ストレージの料金を支払うだけでなく、 1 つまたは複数の Azure VM を実行する費用を支払う必要があります。 第二に、OS アップグレードなどに対して責任を持つなど、ファイル サーバーの実行に使用される VM を管理する必要もあります。最後に、オンプレミスでデータをキャッシュする必要が最終的に生じた場合、ユーザーの判断でレプリケーション テクノロジ (分散ファイル システムのレプリケーションなど) を設定して管理し、キャッシュを行う必要があります。

    Azure Files と Azure ディスクをバックエンド ストレージとして使用した Azure VM でホストされているファイル サーバーの両方の利点を活かす興味深い方法は、クラウドの VM でホストされたファイル サーバーに Azure ファイル同期をインストールすることです。 Azure ファイル共有がお使いのファイル サーバーと同じリージョンにある場合、クラウドの階層化を有効にして、ボリュームの空き領域を最大 (99%) に設定できます。 これにより、NFS プロトコル サポートを必要とするアプリケーションなど、ファイル サーバーに対してどのようなアプリケーションを使用したい場合でも、その使用を可能にしたうえで、データの重複を最小限に抑えることができます。

    Azure で高パフォーマンスで高可用なファイル サーバーを設定する方法に関する詳細については、「[Deploying IaaS VM Guest Clusters in Microsoft Azure](https://blogs.msdn.microsoft.com/clustering/2017/02/14/deploying-an-iaas-vm-guest-clusters-in-microsoft-azure/)」 (Microsoft Azure に IaaS VM ゲスト クラスターをデプロイする) をご覧ください。 Azure Files と Azure ディスクの違いに関する詳細な議論については、「[Azure BLOB、Azure Files、Azure ディスクの使い分け](../common/storage-decide-blobs-files-disks.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)」をご覧ください。 Azure ディスクの詳細については、「[Azure Managed Disks overview](../../virtual-machines/windows/managed-disks-overview.md)」 (Azure Managed Disks の概要) をご覧ください。

* <a id="get-started"></a>**どのようにすれば Azure Files の使用を開始できますか。**  
    Azure ファイルの使用を開始するのは簡単です。単純に、[ファイル共有を作成](storage-how-to-create-file-share.md)して、次のうちのお好きなオペレーティング システムでマウントしてください。 

    - [Windows でのマウント](storage-how-to-use-files-windows.md)
    - [Linux でのマウント](storage-how-to-use-files-linux.md)
    - [macOS でのマウント](storage-how-to-use-files-mac.md)

    Azure ファイル共有をデプロイして組織内の運用ファイルの共有を置き換える方法についての詳しいガイドは、「[Azure Files のデプロイの計画](storage-files-planning.md)」をご覧ください。

* <a id="redundancy-options"></a>**Azure Files では、どのようなストレージ冗長性オプションがサポートされていますか。**  
    Azure Files では現在、ローカル冗長ストレージ (LRS) と geo 冗長ストレージ (GRS) のみがサポートされています。 今後、ゾーン冗長ストレージ (ZRS) と読み取りアクセスの geo 冗長ストレージ (RA-GRS) をサポートすることを計画していますが、現時点でスケジュールをお伝えすることはできません。

* <a id="tier-options"></a>**Azure Files では、どのようなストレージ層がサポートされていますか。**  
    Azure Files では、現在標準的なストレージ層のみがサポートされています。 プレミアム層およびクール層のサポートについては、現時点でスケジュールをお伝えすることはできません。 Blob のみのストレージ アカウントまたは Premium Storage アカウントからは、Azure ファイル共有を作成できないことに注意してください。

* <a id="give-us-feedback"></a>**Azure Files に *x* 機能が追加されることを強く望んでいるのですが、追加できますか。**  
    もちろん、Azure Files チームは、サービスに関するユーザーからのあらゆるフィードバックに耳を傾けたいと思っています。 [Azure Files の UserVoice](https://feedback.azure.com/forums/217298-storage/category/180670-files) まで機能に関する要望をお寄せください。 多くの新しい機能を皆様に喜んでいただけることを楽しみにしています。

## <a name="azure-file-sync"></a>Azure ファイル同期
* <a id="afs-region-availability"></a>**Azure ファイル同期 (プレビュー) は現在、どのリージョンでサポートされていますか。**  
    Azure ファイル同期は現在、米国西部、西ヨーロッパ、オーストラリア東部、および東南アジアで利用可能です。 別の地域のサポートも追加することを予定しており、一般利用に向けて取り組んでいます。 詳細については、「[利用可能なリージョン](storage-sync-files-planning.md#region-availability)」をご覧ください。

* <a id="cross-domain-sync"></a>**同じ同期グループ内にドメイン参加とドメイン非参加のサーバーを保持することはできますか。**  
    はい。ドメイン非参加を含めて、同期グループに別の Active Directory メンバーシップを持つサーバー　エンドポイントを保持できます。 構成が技術的にうまく機能している場合、これはお勧めできません。1 つのサーバーでファイル/フォルダー用に定義された ACL としての通常の構成を、同期グループ内の他のサーバーで強制的に設定できない場合があるためです。 最良の結果を得るには、同じ Active Directory フォレスト内にあるいずれかのサーバー間、別 の Active Directory フォレスト内にあり信頼関係が確立されているサーバー間、または 1 つのドメインにはないサーバー間で同期することをお勧めします。ただし、上記のすべてを混同しないようにしてください。

* <a id="afs-change-detection"></a>**SMB またはポータル経由で Azure ファイル共有に直接ファイルを作成しました。同期グループのサーバーにファイルが同期されるまでどのくらいの時間がかかりますか。** 
    [!INCLUDE [storage-sync-files-change-detection](../../../includes/storage-sync-files-change-detection.md)]

* <a id="afs-conflict-resolution"></a>**2 つのサーバーで同じファイルがほぼ同時に変更された場合、どうなりますか。**  
    Azure ファイル同期では、シンプルな競合解決方法が採用されており、両方の変更が保持されます。 最新の書き込みでは、元のファイル名が引き続き使用されます。 古いファイルでは、以下の分類と共に、'ソース' マシンと競合番号が名前に追加されます。 
   
    `<FileNameWithoutExtension>-<MachineName>[-#].<ext>`  

    たとえば、`CentralServer` が古い書き込みが行われた場所である場合、`CompanyReport.docx` の最初の競合は `CompanyReport-CentralServer.docx` になります。 2 番目の競合は、`CompanyReport-CentralServer-1.docx` として識別されます。

* <a id="afs-storage-redundancy"></a>**Azure ファイル同期では、geo 冗長ストレージ (GRS) はサポートされますか。**  
    はい。ローカル冗長ストレージ (LRS) と geo　冗長ストレージ (GRS) はどちらも、Azure ファイル同期でサポートされています。ペアになっているリージョン間での GRS フェールオーバーの場合、新しいリージョンをデータのバックアップとしてのみ扱うことをお勧めします。 Azure ファイル同期は、新しいプライマリ リージョンで自動的に同期を開始することはありません。 

* <a id="sizeondisk-versus-size"></a>**ファイルの *[ディスク上のサイズ]* プロパティが、Azure ファイル同期を使用した後の *[サイズ]* プロパティと一致しないのはどうしてですか。**  
    Windows のエクスプローラーでは、**[サイズ]** と **[ディスク上のサイズ]** という、ファイルのサイズを表現する 2 つのプロパティを公開しています。 これらのプロパティは微妙に意味が違います。**[サイズ]** はファイルの完全なサイズを表し、**[ディスク上のサイズ]** はディスクに実際に格納されたファイル ストリームのサイズを表します。 圧縮、データ重複除去の使用、この記事で紹介している Azure ファイル同期の使用によるクラウド階層化など、さまざまな理由から、これらの値が異なる場合があります。ファイルが Azure ファイル共有に階層化された場合、ディスク上ではなく Azure ファイル共有にファイル ストリームが格納されるため、ディスク上のサイズはゼロになります。 また、ファイルが部分的に階層化される (または、部分的に再現される) 場合もあります。つまり、ファイルの一部がディスク上にあるということです。 これは、マルチメディア プレーヤーや圧縮ユーティリテイなどのアプリケーションによってファイルが部分的に読み込まれた場合に、発生する可能性があります。 

* <a id="is-my-file-tiered"></a>**ファイルが階層化されているかどうかは、どうやって判断できますか。**  
    ファイルが Azure ファイル共有に階層化されたかどうかを確認するには、以下の複数の方法があります。
    
    1. **ファイル上でファイル属性を確認する** これを行うには、ファイルを右クリックして **[詳細]** に移動し、**[属性]** プロパティまで下へスクロールします。 階層化されたファイルは、以下のような属性設定になっています。     
        
        | 属性の文字 | Attribute | 定義 |
        |:----------------:|-----------|------------|
        | A | Archive | バックアップ ソフトウェアによって、ファイルがバックアップされる必要があることを示します。 この属性は、ファイルが階層化されているか、ディスク上に完全に格納されているかに関係なく、常に設定されます。 |
        | P | スパース ファイル | ファイルがスパース ファイルであることを示します。スパース ファイルとは、ディスク ストリーム上のファイルがほぼ空である場合に、効率的に使用するために NTFS が提供している特別なファイルの種類です。 ファイルは完全に階層化されている (そのファイル ストリームがクラウドのみに格納されていることを意味します) か、または部分的に再現されている (ファイルの一部が既にディスク上にあることを意味します) ため、Azure ファイル同期ではスパース ファイルを使用します。 ファイルがディスク上に完全に再現されている場合、Azure ファイル同期では、スパース ファイルから正規のファイルに変換します。 |
        | L | 再解析ポイント | ファイルが再解析ポイントを保持していることを示します。再解析ポイントは、ファイル システム フィルターで使用するための特殊なポインターです。 Azure ファイル同期では、クラウド内でファイルが格納される Azure ファイル同期のファイル システム フィルター (StorageSync.sys) に対して定義した再解析ポイントを使用します。 これにより、シームレスなアクセスが可能になります。エンド ユーザーが Azure ファイル同期を利用していることや、Azure ファイル共有内のファイルへのアクセスを取得する方法を知る必要はありません。 ファイルが完全に再現されている場合、Azure ファイル同期では、そのファイルから再解析ポイントを削除します。 |
        | O | オフライン | ファイルのコンテンツの一部またはすべてがディスク上に保存されていないことを示します。 ファイルが完全に再現されている場合、Azure ファイル同期ではこの属性を削除します。 |

        ![[詳細] タブが選択されている、ファイルの [プロパティ] ダイアログ ボックス](media/storage-files-faq/azure-file-sync-file-attributes.png)
        
        また、**[属性]** フィールドをエクスプローラーのテーブル表示に追加することで、フォルダー内のすべてのファイルの属性を確認できます。 これを行うには、既存の列 (たとえば、[サイズ]) を右クリックして、**[詳細]** を選択し、ドロップダウン リストから **[属性]** を選択します。
        
    2. **`fsutil` を使用して、ファイル上の再解析ポイントを確認します。** 前記のオプションで説明したように、階層化されたファイルには再解析ポイントという、Azure ファイル同期のファイル システム フィルター (StorageSync.sys) の特別なポインターが常に設定されます。 管理者特権でのコマンド プロンプトまたは PowerShell セッションで、`fsutil` ユーティリティを使ってファイルに再解析ポイントがあるかどうかを確認できます。
    
        ```PowerShell
        fsutil reparsepoint query <your-file-name>
        ```

        ファイルに再解析ポイントがある場合、**Reparse Tag Value : 0x8000001e** を確認する必要があります。 この 16 進値は、Azure ファイル同期が所有する再解析ポイントの値です。また、出力には、Azure ファイル共有内のファイルへのパスを表す再解析データが含まれます。

        > [!Warning]  
        > `fsutil reparsepoint` ユーティリティ コマンドには、再解析ポイントを削除する機能も含まれています。 Azure ファイル同期のエンジニア チームによって指示されないかぎり、このコマンドは実行しないでください。実行すると、データを損失する恐れがあります。 

* <a id="afs-recall-file"></a>**使用したいファイルが階層化されています。ローカルで使用するためにこのファイルをディスクに再現するには、どうすればよいですか。**  
    ディスクにファイルを再現する最も簡単な方法は、ファイルを開くことです。 Azure ファイル同期のファイル システム フィルター (StorageSync.sys) は、Azure ファイル共有からファイルをシームレスにダウンロードします。ユーザーが何らかの作業を行う必要はありません。 マルチメディア ファイルや zip ファイルなど、部分的に読み込みできるファイルの種類の場合、ファイルを開いても、ファイル全体がダウンロードされることはありません。

    また、PowerShell を使ってファイルを強制的に再現することも可能です。 たとえば、多数のファイル (フォルダー内にあるすべてのファイルなど) を一度に再現したい場合に、これが役立つことがあります。 Azure ファイル同期がインストールされているサーバー ノードへの PowerShell セッションを開き、次の PowerShell コマンドを実行します。
    
    ```PowerShell
    Import-Module "C:\Program Files\Azure\StorageSyncAgent\StorageSync.Management.ServerCmdlets.dll"
    Invoke-StorageSyncFileRecall -Path <file-or-directory-to-be-recalled>
    ```

* <a id="afs-force-tiering"></a>**ファイルまたはディレクトリを強制的に階層化するには、どうすればよいですか。**  
    クラウドの階層化機能が有効な場合は、最新のアクセスに基づいて自動的にファイルが階層化され、クラウド エンドポイントに指定されているボリューム空き領域の割合を達成するために階層数が変更されます。ただし、時には、手動で強制的にファイルを階層化したい場合があります。 たとえば、これから長期間、再使用する予定がない大きなファイルを保存して、今はボリューム上に他のファイル/フォルダーのための領域を空けておきたい場合、手動による階層化が役立つ可能性があります。 次の PowerShell コマンドを使って、強制的に階層化できます。

    ```PowerShell
    Import-Module "C:\Program Files\Azure\StorageSyncAgent\StorageSync.Management.ServerCmdlets.dll"
    Invoke-StorageSyncCloudTiering -Path <file-or-directory-to-be-tiered>
    ```

* <a id="afs-files-excluded"></a>**Azure ファイル同期によって自動的に除外されるのは、どのファイルまたはフォルダーですか。**
    Azure ファイル同期は既定で、次のファイルを除外します。
    
    - desktop.ini
    - thumbs.db
    - ehthumbs.db
    - ~$\*.\*
    - \*.laccdb
    - \*.tmp
    - 635D02A9D91C401B97884B82B3BCDAEA.\*

    また、既定で、次のフォルダーも除外します。

    - \System Volume Information
    - \$RECYCLE.BIN
    - \SyncShareState

* <a id="afs-os-support"></a>**Windows Server 2008 R2、Linux、または自分の NAS デバイスで Azure ファイル同期を使用したいと考えています。Azure ファイル同期では、それらをサポートしていますか。**
    今日、Azure ファイル同期では、Windows Server 2016 および Windows Server 2012 R2 しかサポートしていません。 現時点でお伝えできる他の計画はありませんが、顧客の要望を基にサポートするプラットフォームを追加することには前向きな関心を持っています。 [Azure Files の UserVoice](https://feedback.azure.com/forums/217298-storage/category/180670-files) までサポート対象にしたいプラットフォームに関するご意見をお寄せください。

## <a name="security-authentication-and-access-control"></a>セキュリティ、認証、およびアクセス制御
* <a id="ad-support"></a>**Azure Files では、Active Directory ベースの認証とアクセス制御はサポートされていますか。**  
    Azure Files では、次の 2 つの方法でアクセス制御を管理することができます。

    - SAS を使用すると、指定した期間中有効な特定のアクセス許可を持つトークンを生成できます。 たとえば、特定のファイルへの読み取り専用のアクセス許可を持ち、有効期限が 10 分間であるトークンを生成できます。 このトークンを所有するすべてのユーザーは、トークンが有効な間、そのファイルへの 10 分間の読み取り専用アクセスを持ちます。 SAS キーは今日、REST API または クライアント ライブラリ経由でしかサポートされていません。ストレージ アカウント キーを使って SMB 経由で Azure ファイル共有をマウントする必要があります。

    - Azure ファイル同期では、すべての ACL (AD ベースまたはローカル) を保存して、同期先のすべてのサーバー エンドポイントにレプリケートします。 Windows Server は既に Active Directory で認証しているので、Azure ファイル同期では、AD ベース認証の完全サポートと ACL のサポートが実現するまでの優れた応急策を提供しています。

    Azure Files は、現時点で Active Directory を直接はサポートしていません。

* <a id="encryption-at-rest"></a>**自分の Azure ファイル共有が暗号化して保存されていることを確認するには、どうすればよいですか。**  
    保存時の暗号化は、既定ですべてのリージョンで有効になっています。 これらのリージョンでは、暗号化を有効にするために特に何もする必要はありません。 他のリージョンについては、「[サーバー側の暗号化](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)」を参照してください。

* <a id="access-via-browser"></a>**Web ブラウザーを使用して特定のファイルにアクセスできるようにするにはどうすればよいですか。**  
    SAS を使用すると、指定した期間中有効な特定のアクセス許可を持つトークンを生成できます。 たとえば、特定の期間に特定のファイルに対する読み取り専用アクセス権だけを持つトークンを生成できます。 この URL を持つユーザーは、それが有効な間、任意の Web ブラウザーから直接ファイルにアクセスできます。 SAS キーは、ストレージ エクスプローラーなどの UI から簡単に生成できます。

* <a id="file-level-permissions"></a>**共有内のフォルダーに読み取り専用または書き込み専用の権限を指定できますか。**  
    SMB を使用してファイル共有をマウントした場合、このレベルでアクセス許可を制御することはできません。 ただし、REST API またはクライアント ライブラリを使用して Shared Access Signature (SAS) を作成することでこれを実現することができます。

* <a id="ip-restrictions"></a>**Azure ファイル共有に IP 制限を実装することはできますか。**  
    はい。Azure ファイル共有へのアクセスはストレージ アカウント レベルで制限できます。 詳細については、「[Azure Storage ファイアウォールおよび仮想ネットワークの構成 (プレビュー)](../common/storage-network-security.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)」を参照してください。

* <a id="data-compliance-policies"></a>**Azure Files ではどのようなデータ コンプライアンス ポリシーがサポートされていますか。**  
   Azure Files は、Azure Storage の他のストレージ サービスと同じストレージ アーキテクチャ上で実行され、同じデータ コンプライアンス ポリシーを適用します。 Azure Storage のデータ コンプライアンスの詳細については、[Microsoft Azure のデータ保護に関するドキュメント](http://go.microsoft.com/fwlink/?LinkID=398382&clcid=0x409)をダウンロードして参照したり、[Microsoft セキュリティ センター](https://www.microsoft.com/TrustCenter/default.aspx)を参照したりすることができます。

## <a name="on-premises-access"></a>オンプレミスのアクセス
* <a id="expressroute-not-required"></a>**Azure Files に接続するためや、Azure ファイル同期をオンプレミスで使用するために、Azure ExpressRoute を使用する必要はありますか。**  
    いいえ。ExpressRoute から Azure ファイル共有にアクセスする必要はありません。 Azure ファイル共有を直接オンプレミスにマウントしている場合、必要なのは、インターネット アクセスのためにポート 445 (TCP 送信) が開かれていることだけです (これは SMB が通信するポートです)。 Azure ファイル同期を使用している場合、必要なのは、HTTPS アクセスのためのポート 443 (TCP 送信) だけです (SMB は必要ありません)。 ただし、ExpressRoute は、必要であれば、いずれかのアクセス オプションで使用できます。

* <a id="mount-locally"></a>**ローカル コンピューターに Azure ファイル共有をマウントするにはどうすればよいですか。**  
    ポート 445 (TCP 送信) が開いており、クライアントが SMB 3.0 プロトコルをサポートしている (たとえば、Windows 10 や Windows Server 2016 を使用している) 場合は、SMB プロトコル経由でファイル共有をマウントできます。 ポート 445 が組織のポリシーまたはお使いの ISP によってブロックされている場合は、Azure ファイル同期を使用して Azure ファイル共有にアクセスできます。

## <a name="backup"></a>Backup
* <a id="backup-share"></a>**Azure ファイル共有はどのようにバックアップしますか。**  
    誤って削除しないように、定期的に[共有スナップショット (プレビュー)](storage-how-to-use-files-snapshots.md) を使用して保護できます。 AzCopy、RoboCopy、またはマウントされているファイル共有をバックアップできるサードパーティー製のバックアップ ツールを使用できます。 

## <a name="share-snapshots"></a>共有スナップショット
### <a name="share-snapshots---general"></a>共有スナップショット - 一般
* <a id="what-are-snaphots"></a>**ファイル共有スナップショットとは何ですか。**  
    Azure ファイル共有では、読み取り専用バージョンのファイル共有を作成できます。 また、古いバージョンのコンテンツをコピーして同じ共有に戻したり、Azure またはオンプレミス内で場所を変更してさらに変更を加えたりできます。 共有スナップショットの詳細については、[共有スナップショットの概要](storage-snapshots-files.md)に関する記事をご覧ください。

* <a id="where-are-snapshots-stored"></a>**共有スナップショットはどこに格納されていますか。**  
    共有スナップショットは、ファイル共有と同じストレージ アカウントに格納されています。

* <a id="snapshot-perf-impact"></a>**パフォーマンスに影響はありますか。**  
    共有スナップショットには、パフォーマンスのオーバーヘッドはありません。

* <a id="snapshot-consistency"></a>**共有スナップショット アプリケーションに一貫性はありますか。**  
    
いいえ。 共有スナップショットにアプリケーションの一貫性はありません。 共有スナップショットを取得する前に、ユーザーは、アプリケーションから共有へ書き込みをフラッシュする必要があります。

* <a id="snapshot-limits"></a>**共有スナップショットの数に制限はありますか。**  
    Azure Files が保持できる共有スナップショットの数は、最大で 200 までです。 共有スナップショットは共有クォータに対してカウントされないので、すべての共有スナップショットで利用される合計領域に共有ごとの制限はありません。 ストレージ アカウントの制限は、引き続き適用されます。 共有スナップショットの数が 200 を超えると、新しい共有スナップショットを作成するために、古い共有スナップショットを削除する必要があります。

### <a name="create-share-snapshots"></a>共有スナップショットを作成する
* <a id="file-snaphsots"></a>**個々のファイルの共有スナップショットを作成できますか。**  
    共有スナップショットは、ファイル共有レベルで作成されます。 ファイル共有スナップショットから個々のファイルを復元できますが、ファイル レベルの共有スナップショットは作成できません。 ただし、共有レベルの共有スナップショットを取得して、特定のファイルが変更された共有スナップショットを一覧表示したい場合は、Windows にマウントされた共有で、"以前のバージョン" のエクスペリエンスからこれを行うことができます。 [Azure Files UserVoice](https://feedback.azure.com/forums/217298-storage/category/180670-files) でファイル スナップショット機能を使用したい場合は、ぜひお知らせください。

* <a id="encypted-snapshots"></a>**暗号化されたファイル共有の共有スナップショットを作成できますか。**  
    保存時に暗号化を有効にした Azure ファイル共有の共有スナップショットを取得できます。 共有スナップショットから暗号化されたファイル共有に、ファイルを復元できます。 お使いの共有が暗号化されている場合、共有スナップショットも暗号化されます。

* <a id="geo-redundant-snaphsots"></a>**使用している共有スナップショットは geo 冗長性でしょうか。**
    共有スナップショットには、そのスナップショットが対象としている Azure ファイル共有と同じ冗長性があります。 お使いのアカウントに geo 冗長ストレージ (GRS) を選択した場合、共有スナップショットもペアになっているリージョンに冗長的に保存されます。

### <a name="manage-share-snapshots"></a>共有スナップショットを管理する
* <a id="browse-snapshots-linux"></a>**Linux から 共有スナップショットを参照できますか。**  
    Azure CLI 2.0 を使用して、Linux 上で作成、一覧表示、参照、および 復元が可能です。

* <a id="copy-snapshots-to-other-storage-account"></a>**共有スナップショットを別のストレージ アカウントにコピーできますか。**  
    共有スナップショットから別の場所にファイルをコピーできますが、共有スナップショット自体はコピーできません。

### <a name="restore-data-from-share-snapshots"></a>共有スナップショットからデータを復元する
* <a id="promote-share-snapshot"></a>**基本の共有に共有スナップショットを昇格させることはできますか。**  
    共有スナップショットから目的の宛先にデータをコピーすることのみが可能です。 しかし、基本の共有に共有スナップショットを昇格させることはできません。

* <a id="restore-snapshotted-file-to-other-share"></a>**共有スナップショットから別のストレージ アカウントにデータを復元できますか。**  
    はい。 共有スナップショットのファイルは、同じまたは別のリージョンにある同じ/別のストレージ アカウントを含む同じまたは別の場所にコピーできます。 また、オンプレミスまたはその他のクラウドにファイルをコピーすることもできます。    
  
### <a name="cleanup-share-snapshot"></a>共有スナップショットをクリーンアップする
* <a id="delete-share-keep-snapshots"></a>**共有スナップショットは削除せずに、共有を削除することはできますか。**
    お使いの共有にアクティブな共有スナップショットがある場合、共有を削除することはできません。 共有と一緒に共有スナップショットを削除するために使用可能な API があり、Azure ポータルからも同じ操作を行うことができます。

* <a id="delete-share-with-snapshots"></a>**ストレージ アカウントを削除した場合、共有スナップショットはどうなりますか。**
    ストレージ アカウントを削除すると、共有スナップショットも削除されます。

## <a name="billing-and-pricing"></a>課金と価格
* <a id="vm-file-share-network-traffic"></a>**Azure VM と Azure ファイル共有間のネットワーク トラフィックは、サブスクリプションに課金される外部帯域幅としてカウントされますか。**  
    ファイル共有と VM が同じ Azure リージョン内にある場合、それらの間のトラフィックは無料です。 それらが異なるリージョンに置かれている場合、それらの間のトラフィックは外部帯域幅として課金されます。

* <a id="share-snapshot-price"></a>**共有スナップショットにかかるコストを教えてください。**
     共有スナップショットがプレビューの間は、容量には課金されません。 標準ストレージのエグレスとトランザクションのコストが、引き続き適用されます。 一般利用になると、以降は共有スナップショットの容量とトランザクションの両方に課金されます。
     
     共有スナップショットは、本質的に増分です。 基本の共有スナップショットは、共有そのものです。 それ以降の共有スナップショットはすべて増分であり、以前の共有スナップショットとの差分のみを格納しています。 変更されたコンテンツに対してのみ、課金されます。 共有に 100 GB のデータがあり、最新の共有スナップショットの後に 5 GB だけが変更された場合、共有スナップショットは追加の 5 GB のみを消費し、正味の 105 GB に対して課金されます。 トランザクションおよび標準エグレスの課金の詳細については、[課金に関するページ](https://azure.microsoft.com/pricing/details/storage/files/)をご覧ください。

## <a name="scale-and-performance"></a>スケールとパフォーマンス
* <a id="files-scale-limits"></a>**Azure Files のスケールの上限を教えてください。**  
    Azure Files のスケーラビリティおよびパフォーマンスのターゲットの詳細については、「[Azure Files のスケーラビリティおよびパフォーマンスのターゲット](storage-files-scale-targets.md)」を参照してください。

* <a id="need-larger-share"></a>**Azure Files で現在提供されているサイズより大きなファイル共有を必要としています。Azure ファイル共有のサイズを増やすことはできますか。**  
    いいえ。Azure ファイル共有の最大サイズは、5 TB です。 これは、現時点でのハード制限であり、調整することはできません。 共有サイズを 100 TB に増やすソリューションを進行中ですが、現時点でスケジュールをお伝えすることはできません。

* <a id="open-handles-quota"></a>**同じファイルに同時にアクセスできるクライアントの数はどのくらいですか。**  
    1 つのファイルに 2000 のオープン ハンドル クォータがあります。 2000 のオープン ハンドルを作成したら、クォータに達したことを示すエラーが表示されます。

* <a id="zip-slow-performance"></a>**Azure Files にファイルを解凍する際にパフォーマンスが低かった場合は、どうすればよいですか。**  
    Azure Files に大量のファイルを転送する場合、ネットワーク転送に最適化されている AzCopy (Windows 用、Linux/Unix 用はプレビュー) または Azure Powershell を使用することをお勧めします。

* <a id="slow-perf-windows-81-2012r2"></a>**Windows Server 2012 R2 または Windows 8.1 に Azure ファイル共有をマウントしました。パフォーマンスが低下していますが、なぜでしょうか。**  
    2014 年 4 月の Windows 8.1 および Windows Server 2012 R2 向けの累積更新プログラムでパッチが適用された Windows Server 2012 R2 および Windows 8.1 に Azure ファイル共有をマウントした場合、既知の問題があります。 Windows Server 2012 R2 および Windows 8.1 のすべてのインスタンスに、パフォーマンス最適化のためのこのパッチが適用されていることを確認してください (もちろん、Windows Update ですべての Windows パッチを取得することは常に推奨されます)。 詳細については、関連するサポート技術情報の記事「[Slow performance when you access Azure Files from Windows 8.1 or Server 2012 R2 (Windows 8.1 または Server 2012 R2 から Azure Files にアクセスするときにパフォーマンスが低下する)](https://support.microsoft.com/kb/3114025)」を参照してください。

## <a name="features-and-interoperability-with-other-services"></a>機能およびその他のサービスとの相互運用性
* <a id="cluster-witness"></a>**Azure ファイル共有を Windows Server フェールオーバー クラスターの*監視用ファイル共有*として使用できますか。**  
    これは現在、Azure ファイル共有ではサポートされていません。 Azure Blob ストレージ用にこれを設定する方法の詳細については、「[Deploy a Cloud Witness for a Failover Cluster](https://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness)」 (フェールオーバー クラスターのクラスター監視を展開します) をご覧ください。

* <a id="containers"></a>**Azure Container Instances で Azure ファイル共有をマウントできますか。**  
    はい。Azure ファイル共有は、コンテナー インスタンスの有効期間が過ぎた後も情報を保持する優れたオプションです。 詳細については、「[Azure Container Instances での Azure ファイル共有のマウント](../../container-instances/container-instances-mounting-azure-files-volume.md)」を参照してください。

* <a id="rest-rename"></a>**REST API に名前変更の操作はありますか。**  
    現時点ではありません。

* <a id="nested-shares"></a>**共有は入れ子にできますか。つまり共有の下に共有を配置できますか。**  
    
いいえ。 ファイル共有はマウント可能な仮想ドライバーであるため、共有の入れ子はサポートしていません。

* <a id="ibm-mq"></a>**IBM MQ での Azure Files の使用**  
    IBM は、IBM MQ ユーザーが IBM のサービスで Azure Files を構成する際にガイドとなるドキュメントを公開しました。 詳細については、「 [How to setup IBM MQ Multi instance queue manager with Microsoft Azure File Service (IBM MQ マルチ インスタンス キュー マネージャーを Microsoft Azure File サービスでセットアップする方法)](https://github.com/ibm-messaging/mq-azure/wiki/How-to-setup-IBM-MQ-Multi-instance-queue-manager-with-Microsoft-Azure-File-Service)」を参照してください。

## <a name="see-also"></a>関連項目
* [Windows での Azure Files に関する問題のトラブルシューティング](storage-troubleshoot-windows-file-connection-problems.md)
* [Linux での Azure Files に関する問題のトラブルシューティング](storage-troubleshoot-linux-file-connection-problems.md)
* [Azure ファイル同期のトラブルシューティング (プレビュー)](storage-sync-files-troubleshoot.md)