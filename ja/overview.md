## Security > Security Advisor > 概要

Security Advisorは、顧客が作成したNHN Cloud組織およびプロジェクトリソースのセキュリティ設定状態を点検し、推奨ガイドを提示するサービスです。安全なクラウド環境のために推奨ガイドを活用できます。

## 主な機能
* NHN Cloud組織のガバナンス設定を点検し、推奨措置方法を適用してクラウド環境の安全性を高めることができます。
* NHN Cloudプロジェクトに属する長期未使用アカウントを点検し、推奨措置方法を案内します。
* Security Groupsを点検してインスタンスに適用されたセキュリティルールを確認できます。
* RDSへのアクセス設定を点検して不要なアクセスを遮断できます。
* 定期的な自動点検機能を提供し、結果をメールで送信できます。

## 対象リソース, サポートリージョン
### 選択点検リージョン別サポート範囲
|区分|サポートリージョン|
|---|---|
|組織で区分された 点検項目|韓国(パンギョ)リージョン, 韓国(ピョンチョン)リージョン、日本(東京)リージョン、米国(カリフォルニア)リージョン|
|プロジェクトで区分された 点検項目|韓国(パンギョ)リージョン、 韓国(ピョンチョン)リージョン、日本(東京)リージョン|

### 選択点検項目のプロジェクト項目点検対象リソース
|区分&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|点検項目|対象リソース|備考|
|---|---|---|---|
|プロジェクト &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |Security Groups点検|Instance, Security Groups|Database Instance、NKSクラスタ除外|
|プロジェクト &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|Database Security Groups点検|Database Instance(MS-SQL Instance, MySQL Instance, PostgreSQL Instance, CUBIRD Instance, MariaDB Instance, Tibero Instance, Redis Instance), Security Groups|
|プロジェクト &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |RDSアクセス制御点検 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|RDS for MariaDB, RDS for MS-SQLはパンギョリージョンでのみサービスされているため パンギョリージョンでのみ点検可能|
