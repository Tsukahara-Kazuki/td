# はじめに
この資料は、`Treasure Data Toolbelt: Command-line Interface` を使用する際のコマンドTips集です。
  
# TDアカウントへのログイン
  
`td account -f`
  
※SSOログインの場合
1. 事前のログイン情報削除
`rm ~/.td/td.conf`
  
2. API KEYをセッティング
`td apikey:set YOUR_API_KEY`  

※Tokyoリージョンの場合  
`td -e https://api.treasuredata.co.jp account -f`  

※TokyoリージョンからUSに戻す  
`td -e https://api.treasuredata.com account -f`  

# WorkflowのDLやUploadの際のフォルダ変更（チェンジディレクトリ）
  
`cd AAAA/BBBB`

# WorkflowのDL
  
`td wf download target_workflow_name`

# Workflowのアップロード
  
以下コマンドを実行する前に`cd`コマンドでアップロードしたいWFファイルが存在するフォルダに移動してください。
  
`td wf push set_project_name`
  
# secrets keyの設定
  
1. 設定するプロジェクト,呼び出しkey,値の設定
  
   `td wf secrets --project set_project_name --set td.apikey`
  
   ※この場合`set_project_name`というWFに`td.apikey`というkeyを設定する。
  
2. 🔑の中に値を設定（CLIでは値は確認できません）
  
3. WFでの呼び出しかた
`${secret:td.apikey}`
  
# Workflow Project ID確認方法
  
1. TDのリージョン変更（us:.com,tokyo:.co.jp）&API Keyの入力後コマンド実行。
  
   `% curl 'https://api-workflow.treasuredata.com/api/projects/' -H "Authorization: TD1 [API Key]" -H"Accept: application/json" | jq .`
  
# CLIでTDのデータベース確認
  
`td db:list`. 

# 該当JOBの確認とデータダウンロード
  
`td job:show xxxxxxxxxxx -f csv -o xxxxxxxxxxx.csv --column-header`
  
# スケジュールQueryの確認
  
`td sched:list`
  
## CSVに変換
  
`td sched:list -f csv`
  
## CSVでダウンロードする場合
`td sched:list -f csv > sample.csv`
  
## テーブル名などフィルタをかける場合
`td sched:list | grep "filter"`
  
# Other
現在いるディレクトリを表示
`pwd`
  
# Jupyter Setup
  
1. Dockerのダウンロード. 
  `https://hub.docker.com/editions/community/docker-ce-desktop-mac`
  
2. Jupyterのインストール. 
  `docker run -it --name Jupyter -p 8888:8888 -e JUPYTER_ENABLE_LAB=yes -v /Users/USERディレクトリ/Desctop/local/Jupyter:/home/jovyan jupyter/all-spark-notebook`
  
3. Jupyterが立ち上がったら実行. 
  `pip install pandas pytd numpy matplotlib`
