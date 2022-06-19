# 演習1. OpenShift ユーザエクスペリエンス 

## シナリオ

このラボでは、Red Hat OpenShift Container Platformでアプリケーションをデプロイするデモを行います。 

### 目標
* Web コンソールのパースペクティブ(DeveloperとAdministrator)を理解する。
* プロジェクトの作成
* Gitリポジトリからアプリケーションをビルドしてデプロイする
* ウェブコンソールのトポロジービューに慣れる
* アプリケーションのグループ化の一部としてリソースを関連付ける
* 配置されたリソースの管理者ビューを理解する

---
## Developer パースペクティブ

OpenShift Container PlatformのWebコンソールには、Administrator パースペクティブとDeveloperパースペクティブの2つのパースペクティブがあります。Developerパースペクティブでは、開発者のユースケースに特化したワークフローを提供します。

1. Developerパースペクティブに切り替えます。 アプリケーションを作成するためのオプションを持つTopologyビューが表示されます。

![./images/03_1_developer_perspective.png]()


![Freeプランの選択](./images/03_1_developer_perspective.png)
<div style="text-align: center;">Freeプランの選択</div>

=== Project 作成

プロジェクトによって、あるユーザーのコミュニティが他のコミュニティから切り離された状態でコンテンツを整理・管理できます。プロジェクトはKubernetesネームスペースに対するOpenShiftの拡張で、ユーザーのセルフプロビジョニングを可能にする機能を追加したものです。 ほとんどの場合に互換性があります。

. *Project* ドロップダウンメニューをクリックすると、利用可能なすべてのプロジェクトのリストが表示されます。 *Create Project* を選択します。
+
image:images/03_1_create_project_developer_perspective.png[]
+
NOTE: 異なるプロジェクトはそれぞれに対応した異なるユーザー権限とクォータを持つことができます

. *Name* を `test` として、プロジェクトを作成します。

== アプリケーションデプロイメント

Web コンソールの Developer パースペクティブでは、Add ビューからアプリケーションおよび関連サービスを作成し、それらを OpenShift Container Platform にデプロイするための以下のオプションが提供されます。

次の手順では、Developerパースペクティブでアプリケーションを作成するための *Import from git* オプションについて見ていきます。 GitHubにある既存のコードベースを利用して、以下のようにOpenShift Container Platform上でアプリケーションを作成、構築、デプロイします。

=== アプリケーションの作成
. Add ビューで From Git をクリックし、Import from Git フォームを表示します。
+
image:images/03_1_add_application_from_git.png[]
+
. Git セクションで、アプリケーションの作成に使用するコードベースの Git リポジトリー URL を入力します。
+
[source, plain]
----
https://github.com/sclorg/nodejs-ex.git
----
+
image:images/03_1_import_from_git_form_url.png[]
+
. ``を選択し、
. Builder セクションで、URL の検証後に、適切なビルダーイメージが検出され、スターのマークが付けられ、自動的に選択されます。https://github.com/sclorg/nodejs-ex Git URL の場合、Node.js ビルダーイメージがデフォルトで選択されます。ビルダーイメージが自動検出されていない場合は、ビルダーイメージを選択します。必要に応じて、Builder Image Version のドロップダウンリストを使用してバージョンを変更できます。

. General セクションで、以下を実行します。
.. *Application* フィールドに、アプリケーションを分類するために一意の名前 (nodejs-ex-app など) を入力します。アプリケーション名が namespace で一意であることを確認します。
.. *Name* フィールドに、このアプリケーション用に作成されたリソースを分類するために一意な名前を入力します。これは Git リポジトリー URL をベースとして自動的に設定されます。
+
注: リソース名は namespace で一意である必要があります。エラーが出る場合はリソース名を変更します。
+
. *操作*: *Resources* セクションで、デフォルトのリソース *Deployment* を選択します 
. *説明* Deployment は単純な Kubernetesスタイルのアプリケーションを作成します。 "Deployment Config" は OpenShiftスタイルのアプリケーションを作成します。 "Knative Service" はマイクロサービスを作成します。
+
注: Knative Service オプションは、Serverless Operator がクラスターにインストールされている場合にのみ、Import from git 形式で表示されます。詳細は、OpenShift Serverless のインストールについてのドキュメントを参照してください。
+
. *説明*: Advanced Options セクションでは、Create a route to the application がデフォルトで選択されるため、公開されている URL を使用してアプリケーションにアクセスできます。アプリケーションをパブリックルートに公開したくない場合は、チェックボックスをクリアできます。
. *操作*: Create をクリックして、アプリケーションを作成し、Topology ビューでビルドのステータスを確認します。

=== アプリケーションの作成 その２ （実施してみてください。）
. 以下の設定で、アプリケーションをデプロイしてみてください。
+
* GitHub レポジトリ URL：
+
[source, plain]
----
https://github.com/RedHatGov/openshift-workshops.git
----
+
* *Show Advanced Git Options* → ：
+
[source, plain]
----
. /dc-metro-map
----
+
. デプロイして、*Route* からアプリケーションにアクセスしてみてください。
+
image:images/03_1_import_from_git_form_url.png[]


=== Topology ビュー

. Web コンソールのDeveloperパースペクティブにあるTopologyビューでは、プロジェクト内のすべてのアプリケーション、そのビルドステータス、およびそれらに関連するコンポーネントとサービスを視覚的に表示します。
+
image:images/03_1_topology_view_a.png[]
+
[NOTE]
====
*操作*: グラフィカルな表示が表示されない場合は、Web コンソールの右上にある「Topologyビュー」アイコンをクリックします。

image:images/03_1_topology_view_switch_view.png[width=50%]
====
+
. *説明*: Developer パースペクティブの左側のナビゲーションパネルを使用すると、Topology ビューに移動できます。アプリケーションを作成したら、Topology ビューに自動的に移動します。ここでは、アプリケーション Pod のステータスの確認、パブリック URL でのアプリケーションへの迅速なアクセス、ソースコードへのアクセスとその変更、最終ビルドのステータスの確認ができます。ズームインおよびズームアウトにより、特定のアプリケーションの詳細を表示することができます。
. *説明*: Podの状態やフェーズは、色で区別され、ツールチップで次のように表示されます。Running (image:images/03_1_pod_running.png[]), Not Ready (image:images/03_1_pod_not_ready.png[]), Warning (image:images/03_1_pod_warning.png[])、Failed(image:images/03_1_pod_failed.png[])、Pending (image:images/03_1_pod_pending.png[])、Succeeded(image:images/03_1_pod_succeeded.png[])、Terminating(image:images/03_1_pod_terminating.png[])、またはUnknown(image:images/03_1_pod_unknown.png[])のいずれかになります。 Podの状態の詳細については、Kubernetesのドキュメントを参照してください。

. *説明*: アプリケーションを作成し、イメージがデプロイされると、ステータスは Pending と表示されます。アプリケーションをビルドすると、Runningと表示されます。
+
image:images/03_1_topology_nodejs_pod_running.png[width=50%]

* 以下のように、異なるタイプのリソースオブジェクトのインジケーターと共に、アプリケーションリソース名が追加されます。
** *D*: Deployment
** *DC*: Deployment Configs
** *SS*: StatefulSet
** *DS*: Daemonset

注: OpenShift Deployment Configsに加えて、Kubernetes _Deployments_ もサポートされています。

== Monitoring ビューの確認 (OpenShift Monitoring)

Red Hat は最近、モニタリング機能をウェブコンソールに統合しました。プロジェクト全体のメトリクスとイベントについてはこちらをご覧ください。

. 左側のパネルで *Monitoring* をクリックします。
+
image:images/03_1_developer_perspective_monitoring.png[]
+
. *Dashboard* タブをクリックする。
* Dashboardタブは、プロジェクトのメトリクスをまとめて表示します。
. *Metrics* タブをクリックする。
* Metricsタブは、Prometheus Metricsのカスタムグラフを作成することができます。
. *Events* タブをクリックする。
* Eventsタブは、報告されたイベントが一つのストリームとして表示され、フィルターできます。


== Pod の確認 (Readiness Probe / Liveness Probes)

. 左側のメニューから、 *Workloads -> Pods* を選びます
* プロジェクトの *Pods* ページは、プロジェクトの中で現在実行中の全てのPodを表示します。
** `Running`, `Pending` などコンテナの状態を確認することができます。
**  *Ready*  列は Readiness チェックにもとづいたコンテナ内アプリケーションの状態が表示されます。

. `mongodb-XXXXX` Pod をリストから選びます。
* それぞれの *Pod* ページでは以下が表示されます。
**  *Pod* セクション
*** *Memory Usage*, *CPU Usage*, *Filesystem* のグラフ
+
image:images/03_1_admin_pod_details.png[]
*** Podのステータスとそれをホストする OpenShift ノード
** *Containers* セクションでは、, イメージ名とコンテナの状態を含む情報が表示されます

. `mongodb` という名前のコンテナをクリックして *Container Details* ページを開く。
** mongodb アプリケーションコンテナの *Readiness Probe* と *Liveness Probes* を確認します。
** mongodb アプリケーションコンテナの *Resource Requests* と *Resource Limits* を確認します。

. ブラウザの *戻る* をクリックして、 *Pod Details* ページに戻る。
** *Volumes* セクションに表示される情報は、名前、タイプ、権限など。
**  現在、2つのボリュームがマウントされています。
*** mongodb-data ボリュームは PVC *mongodb-data* にバインドされており、 Read/Writeが可能です。
*** default-token *Secret* ボリュームは バインドされており、 読み込み専用です。

. *Logs* タブを選択します
* *Logs* タブは Podのログを表示します。
** Podのメッセージはここに表示され、更新されるにしたがって追跡することができます。
** 更新によるログの出力を一時停止および再開することができます。

. *Terminal* タブを選択します
* *Terminal* タブでは Pod 内の任意のコンテナ内で端末を使えます。
** デバッグやテストのためにコンテナ内でコマンドを実行することができます。

. *Events* タブを選択します
* *Events* タブはPodに関連したイベントを表示します。
** このリストはPodのDeploymentで何かがおかしいかを探したり、イベントの連鎖を追跡したりするために使えます。

== OperatorHub から Operatorのインストール
=== OpenShiftパイプラインのインストール

他のデモンストレーションを実施する前に、 OpenShift Container Platform の webコンソールのホームページへ行き、プロジェクトを削除しましょう。

. OpenShiftパイプラインをインストール
* 管理者パースペクティブの下の左側のメニューから、Operators → OperatorHubに移動します。
* 検索ボックスでパイプラインを検索し、 OpenShiftPipelinesOperatorをクリックします。
+
image:images/03_100_prerequisites_operatorhub.png[]
+
* 説明ビューで、[インストール]をクリックして、すべてのインストール設定を確認します。
+
image:images/03_101_prerequisites_operatorhub_install_pipelines.png[]
+
* Update Channelがstableに設定されていることを確認し、 InstallをクリックしてOperatorのインストールを開始します。
+
image:images/03_102_prerequisites_operatorhub_install_operator.png[]
+
* 数秒後、インストールは正常に完了し、[ステータス]列で確認でき、ステータスが[成功]であるかどうかを確認できます。
+
image:images/03_103_prerequisites_operatorhub_pipelines_installed.png[]

=== OpenShift loggingのインストール
同様の手順でインストールしてみましょう。

=== AMQ Streamsのインストール
同様の手順でインストールしてみましょう。

