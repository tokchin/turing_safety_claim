# 第14章 サイバーセキュリティ方針（第2版新設ドラフト）

本ドラフトは、Turing_Safety_Claim 第2版における第14章の新設案である。第2版章立てに従い、14.1〜14.5の5節で構成する。

文体は初版Turing_Safety_Claim.mdに合わせ、簡潔な宣言文、安全主張の*斜体強調*、要点の表組みで構成する。

本章は、サイバーセキュリティケース（以下、Cybersecurity Case）そのものを記述するものではない。本書は最上位安全論証ハブとしての性格を保ち、サイバーセキュリティに関する主張・設計思想・参照ポインタのみを保持する。実体は衛星文書Cybersecurity Caseが担う。

---

## 14.1 Cybersecurity Caseの位置付け

### 14.1.1 サイバーセキュリティを独立章として整備する理由

L4自動運転車両は、運転者を介さずに走行・停止・MRC遷移を実行する。そのため、サイバー攻撃により以下のいずれかが発生した場合、安全性は直接損なわれる。

1. E2E AI入力（カメラ画像、車両状態量）への不正な改変または注入

2. ADS制御指令（舵角、加減速、モード遷移）への不正介入

3. 多重系ADS間のArbitration信号への介入

4. OTAによるAIモデル・ECUファームウェア更新への攻撃

5. 遠隔監視通信への攻撃（指示なりすまし、断絶、傍受）

6. DSSAD相当ログの改ざん・消去

7. 車両制御I/F（VMC I/F）への不正アクセス

これらは、本書第8章（E2E AI）、第9章（多重系ADS）、第10章（センサ・計算機・車両制御系の失陥安全）、第11章（MRC設計）、第12章（遠隔監視）、第13章（ログ）の各安全主張を、サイバー側面から無効化し得る。

したがって、サイバーセキュリティは安全論証の前提条件として独立章で扱う必要がある。初版本書では第6.8節でISO/SAE 21434への参照を最低限に記述するにとどまっていたが、第2版では本章として独立化する。

### 14.1.2 本章の位置付け

本章の位置付けは、以下である。

| 項目 | 本書本章での扱い |
| --- | --- |
| 安全主張に対するサイバー側面の前提条件の宣言 | 本章 |
| 主要攻撃面の俯瞰 | 14.2 |
| Safety/Security Co-Engineeringの基本方針 | 14.3 |
| OEM-Turingの分担 | 14.4 |
| UN-R 155準拠とCybersecurity Caseへのポインタ | 14.5 |
| TARA（Threat Analysis and Risk Assessment） | **本書では扱わない**。Cybersecurity Caseが担う |
| CS Concept、Product development、Validation | **本書では扱わない**。Cybersecurity Caseが担う |
| 鍵管理（HSM、PKI、鍵更新、鍵失効） | **本書では扱わない**。Cybersecurity Case + 運用文書 |
| SOC運用、PSIRT、脅威インテリジェンス | **本書では扱わない**。運用文書群 |
| 製造工程のCybersecurity | **本書では扱わない**。OEM側文書 |

本章は、Cybersecurity Caseの目次を本書側に複製しない。本章の役割は、安全論証本体とCybersecurity Caseの接続点を明示することに限定する。

### 14.1.3 安全とサイバーの関係に関する基本主張

本書の最上位安全主張（第4章）は、E2E AIによる通常走行安全と多重系ADSによる失陥時安全のいずれも、サイバー攻撃により当該主張の根拠（入力の真正性、出力の真正性、Arbitrationの真正性、ログの真正性）が失われると、それ自体が成立しない。

そこで、本書のサイバーセキュリティに関する基本主張は以下である。

*Turingは、本書の安全主張を支える入力・出力・Arbitration・I/F・ログ・更新・通信のそれぞれについて、ISO/SAE 21434に基づくTARAを実施し、UN-R 155のCSMS要件に準拠した対策を講じる。これにより、サイバー攻撃に起因して本書の最上位安全主張が無効化される残存リスクを、許容水準まで低減する。*

本主張の実体的な根拠（TARA結果、対策実装、検証エビデンス）は、衛星文書Cybersecurity Caseで提示する。

---

## 14.2 主要攻撃面と対策の概要

### 14.2.1 攻撃面の整理方針

本書では、攻撃面を「本書の安全主張を直接無効化し得る箇所」を起点に整理する。すなわち、E2E AIの入出力、多重系ADSのArbitration、車両制御I/F、遠隔監視通信、OTA更新、ログ、製造・サプライチェーンを軸とする。

詳細な攻撃面リスト、TARAの結果、攻撃シナリオ、Annex 5 Part Aへのマッピングは、Cybersecurity Caseに整備する。

### 14.2.2 主要攻撃面と本書での対策の概要

| 攻撃面 | 想定される攻撃 | 本書側の主たる対策方針 | 詳細整備先 |
| --- | --- | --- | --- |
| E2E AI入力（カメラ） | 物理的なセンサ妨害、画像注入、Replay、ファームウェア改ざん | カメラとECUを直結し物理経路を限定（10章）／カメラ健全性監視（10.5）／MRC専用カメラの完全独立配置（9.4、10.2）／カメラFWの真正性検証 | Cybersecurity Case + 車両要求仕様書第8章 |
| ADS制御指令（VMC I/F） | なりすまし、Replay、矛盾指令、信号化け、Counter停止 | CMACメッセージ認証（VMC I/F仕様書第6.4節）／E2E protection（CRC32 + Counter）／車両側Plausibility Check（VMC I/F仕様書第6.2節） | Cybersecurity Case + VMC I/F仕様書 |
| 多重系ADS Arbitration | Arbitration信号への介入、両系統への同時介入 | Arbitrationの車両側独立実装（VMC I/F仕様書第5章）／異種ECU冗長による攻撃面のDiversification（9.4） | Cybersecurity Case + VMC I/F仕様書 |
| OTA更新（AIモデル、FW） | 偽のモデル/FW配信、Rollback、不整合バージョン | ISO 24089準拠の配信認証・整合性検証・ロールバック（モデル更新管理書）／rolling update中の系間バージョン整合管理（6.7） | モデル更新管理書 + Cybersecurity Case |
| 遠隔監視通信 | なりすまし、傍受、リプレイ、断絶 | 認証付きセッション／通信断時はMRC前提に組み込まない原則（12.2）／指示なりすまし時もMRC成立（12.4） | Cybersecurity Case + 遠隔監視運用文書 |
| DSSAD相当ログ | 改ざん、消去、なりすまし | ADS側・車両側のDual recording（VMC I/F仕様書第8章）／署名・タイムスタンプ／改ざん検出 | ログ項目定義書 + Cybersecurity Case |
| 診断ポート（OBD-II、UDS） | 不正アクセス、Service ID悪用 | UDSのSecurity Access、診断ポート物理アクセス制限、製造工程と整備工程の分離 | 車両要求仕様書第10章 + Cybersecurity Case |
| 車載通信（CAN、車載Ethernet、Wi-Fi、Cellular） | バス不正注入、外部通信経由侵入 | 車載ネットワーク分離・ゲートウェイ・侵入検知（OEM主管）／Safety-Critical系統の論理・物理分離 | 車両要求仕様書第7章・第10章 + Cybersecurity Case |
| ECUファームウェア | 改ざん、なりすまし更新 | Secure Boot、Hardware Root of Trust、署名検証 | 車両要求仕様書第10章 + 各ECU Safety Manual |
| 製造工程・サプライチェーン | 製造時の悪意混入、共通CVE、共通サプライヤ脆弱性 | 製造工程のCS（OEM主管）／ECUサプライヤPSIRTの継続フォロー（9.4.4）／共通サプライヤ依存リスクの定期評価 | OEM側文書 + Cybersecurity Case |
| 物理アクセス（車内コネクタ、車載ストレージ） | 抜去・改造、ストレージ取出 | 物理アクセス制限、車載ストレージの暗号化、改造検出 | 車両要求仕様書第10章 + Cybersecurity Case |

本表は俯瞰用の対応関係であり、定量的なリスク評価、Threat Scenarioの詳細列挙、対策の実装仕様、検証手順は、Cybersecurity Caseに整備する。

### 14.2.3 安全と攻撃の二重化原則

サイバー側の対策は、機能安全側の対策（CRC、E2E protection、Plausibility Check、Arbitration、安全監視系、MRCモード遷移）を**置き換えない**。両者は二重化して動作する。

すなわち、サイバー攻撃が成功しメッセージ認証を突破した場合でも、車両側Plausibility Check、安全監視系、MRC系ADSにより、車両は危険挙動を継続しない。逆に、機能安全機構が誤動作した場合でも、サイバー側の認証・整合性検証は独立に動作する。

この二重化により、サイバー側単独の故障または機能安全側単独の故障が、本書の安全主張を直接破壊しない設計とする。

---

## 14.3 Safety/Security Co-Engineering

### 14.3.1 Co-Engineeringを採用する理由

本書では、機能安全（ISO 26262）、SOTIF概念（ISO 21448、概念借用）、AI安全（ISO/PAS 8800）、Safety Case（ISO/TS 5083、UL 4600）と、サイバーセキュリティ（ISO/SAE 21434、UN-R 155）を、独立した工程としては扱わない。

理由は、以下である。

サイバー脅威への対策が機能安全要件と矛盾し得る（例：認証鍵失効により正規通信が遮断され、安全機能が停止する）／機能安全機構がサイバー攻撃の入口になり得る（例：診断機能が不正アクセスに悪用される）／AIモデルへの攻撃（敵対的攻撃、データ汚染）はSOTIF的なTriggering Conditionとサイバー脅威の境界が曖昧／OTA更新は機能安全とサイバーの両側面を持つ。

したがって、安全工学とサイバー工学の双方を統合的に扱うCo-Engineeringを基本方針とする。

### 14.3.2 Co-Engineeringの基本構造

Turingは、以下の4軸でCo-Engineeringを行う。

| 軸 | 内容 | 対応する規格・本書章 |
| --- | --- | --- |
| Hazard ↔ Threat統合分析 | HARAとTARAの相互整合。Safety GoalがCS脅威により侵害されないことを確認 | ISO 26262 + ISO/SAE 21434 / 第4章 + Cybersecurity Case |
| Concept ↔ CS Concept整合 | Functional Safety ConceptとCS Conceptの整合性確認、矛盾解消 | ISO 26262 + ISO/SAE 21434 / 第9〜11章 + Cybersecurity Case |
| AI Safety ↔ CS整合 | AIモデルへの敵対的攻撃・データ汚染を、AI Safety RequirementsとCSの両面から扱う | ISO/PAS 8800 + ISO/SAE 21434 / 第8章 + AI Safety Case + Cybersecurity Case |
| 運用統合 | 運用後監視（Field Monitoring）でSafetyイベントとCSイベントを共通の運用フローで扱う | ISO 26262 Part 7 + ISO/SAE 21434 Clause 13/15 / 運用文書群 |

本構造の実装手続き、レビューゲート、トレーサビリティは、Cybersecurity CaseおよびSafety Plan、CS Planで規定する。

### 14.3.3 Hazard ↔ Threat分析の整合

HARA（Hazard Analysis and Risk Assessment）とTARA（Threat Analysis and Risk Assessment）は、独立に実施した上で、以下の観点で相互整合を取る。

| 整合観点 | 整合内容 |
| --- | --- |
| Item Definition | HARAとTARAで同一のItem Definition（システム境界、外部I/F、想定運用）を共有 |
| Safety Goal vs Cybersecurity Goal | 各Safety Goal（第4章）が、CS脅威により侵害される経路を、TARAが網羅していることを確認 |
| Hazardous Event vs Threat Scenario | Safety側のHazardous Eventに、それを誘発し得るThreat Scenarioが対応付けされていることを確認 |
| Safety Mechanism vs Cybersecurity Control | Safety Mechanism（CRC、E2E protection、Plausibility Check、安全監視系、MRC）に対し、CS Control（メッセージ認証、Secure Boot、ログ保全）が衝突せず両立することを確認 |
| 残存リスク | Safety残存リスク（第21章）とCS残存リスクを、本書第21章で統合的に扱う |

本整合プロセスは、Cybersecurity Caseの「Safety/Security Interface Document」で具体化する。

### 14.3.4 サイバー事象と機能安全事象の切り分け

走行中に異常が検出された場合、それが機能安全側の故障か、サイバー攻撃の兆候かを、車両単独で完全に切り分けることは要求しない。

本書では、以下の方針で扱う。

走行中の異常検出時の挙動は、原因がSafety故障であるかCS事象であるかを問わず、安全監視系の判断によりMRCモードへ遷移し、車両単独でリスク最小状態に到達する（第9章、第11章）。

事後の原因切り分けは、DSSAD相当ログ（第13章）、車両側ログ、ECU個別ログ、CS監視ログ（IDS/IPSログ、認証失敗ログ、Secure Bootログ等）を統合的に分析することで行う。分析の結果、CS事象であると判定された場合、PSIRT手順とリコール対応プロセス（第18章）に接続する。

すなわち、車両は「安全側に止まる」、原因切り分けは「事後に行う」、対応は「組織プロセスで行う」、という分担とする。

### 14.3.5 AIモデルに対する攻撃の扱い

E2E AIに対する攻撃は、機能安全側のSOTIF的Triggering Conditionとサイバー側の脅威の境界が曖昧である。本書では、以下のように整理する。

| 攻撃カテゴリ | 一次的扱い | 二次的扱い |
| --- | --- | --- |
| 物理的なセンサ妨害（カメラ汚損、強光、レーザー等） | SOTIF的Triggering Condition（8章、ODD境界、ODD逸脱判定） | カメラ健全性監視（10.5）と組合せ |
| 物理空間に置かれた敵対的パッチ・敵対的標識 | SOTIF的Triggering Condition + AI Safety Requirements | TARA上もThreat Scenarioとして列挙 |
| 通信経路から注入されるカメラ画像偽装 | サイバー脅威（CS Concept） | カメラ-ECU直結配置（10章）で経路を限定 |
| 学習データへのデータ汚染 | サイバー脅威（CS + AI Safety） | データガバナンス（AI Safety Case） |
| モデルパラメータ抜取・改ざん | サイバー脅威（CS） | Secure Boot、署名検証 |
| Prompt-injection的入力（マルチモーダル広告等） | SOTIF的Triggering Condition + CS脅威 | 両側面で対策（AI Safety Case + Cybersecurity Case） |

本整理は、AI Safety CaseとCybersecurity Caseの双方で詳細化する。

---

## 14.4 OEM-Turing分担

### 14.4.1 分担を明示する目的

L4対応車両のサイバーセキュリティは、車両プラットフォーム（OEM主管）とADS（Turing主管）にまたがる。Phase 1〜2における型式指定スキーム、UN-R 155 CSMSの組織責任、PSIRT・SOC運用は、OEMとTuringの双方が関与しなければ成立しない。

本節は、本書第17章（責任分界）およびAppendix I（責任分界マトリクス）と整合する形で、サイバーセキュリティに限定した分担を整理する。

### 14.4.2 分担の概要

分担の概要は、以下である。詳細は車両要求仕様書第10章および別文書「OEM-Turing協定書（Cybersecurity Annex）」で確定する。

| 領域 | 主管 | 補足 |
| --- | --- | --- |
| 車両ECU群（制動、操舵、電源、通信、診断）のセキュア実装 | OEM | ISO/SAE 21434準拠、Secure Boot、HSM搭載 |
| ADS構成要素（通常走行用ECU、MRC用ECU、AIモデル、ADS基盤）のセキュア実装 | Turing | ISO/SAE 21434準拠、ECUサプライヤSafety/Security Manual適用 |
| 車載ネットワーク（バックボーンEthernet、ゲートウェイ、CAN、車載Wi-Fi/Cellular） | 共同 | OEMが基盤、Turingが安全主張側の要件を提示 |
| VMC I/F（ADS〜車両I/F） | 共同 | VMC I/F仕様書がI/Fを確定。CMAC、E2E protection、鍵管理は共同設計 |
| OTA更新（車両ECU FW、ADS構成要素FW、AIモデル） | 共同 | OEMがOTAインフラ、TuringがADS側構成要素の更新フローを主管 |
| 鍵管理（HSM、PKI、鍵更新、鍵失効） | 共同 | 鍵の所在・運用主体は協定書で確定 |
| 製造工程のセキュリティ（書込ツール、製造ライン、ロット管理） | OEM | 製造工程CSはUN-R 155準拠 |
| サプライチェーン管理（ECUサプライヤ、半導体サプライヤ） | 共同 | OEMが車両ECU側、TuringがADS側ECU・AI関連 |
| TARA | 共同 | 全体TARAをCybersecurity Caseとして統合管理。OEMとTuringそれぞれ主管領域のTARAを実施し統合 |
| 運用後SOC | 共同 | OEM車両SOCとTuring ADS SOCを連携。プレイブックは協定書で規定 |
| 運用後PSIRT | 共同 | 共通の脆弱性受付窓口、共通のトリアージ基準 |
| 脅威インテリジェンス | 共同 | 業界情報、ECUサプライヤ情報、AI関連情報を相互共有 |
| 事故・インシデント対応 | 共同 | 第18章のインシデント対応プロセスに統合 |
| 当局・調査機関対応 | 共同 | 第18章に従う |

### 14.4.3 分担に関する原則

分担に関する原則は、以下である。

サイバーセキュリティに関する責任は、OEMとTuringのいずれか一方が単独で担うことはない。型式認証取得時のCSMS提出主体、運用時のSOC・PSIRT主管、事故時の届出主体は、車両型式とADS主管の関係から決定するが、技術的責任は常に共同で負う。

VMC I/F上のセキュリティ実装（CMAC、Counter、Replay対策、鍵管理）は、ADS側と車両側で**対称な実装**を行う。一方が他方を信頼する片方向設計は採らない。

製造工程・OTAインフラ・車載ネットワーク基盤はOEMの責任領域だが、Turingはこれらに対する要件を車両要求仕様書第10章を通じて提示する。OEMはこれを受け、Cybersecurity Case（OEM側）として実装エビデンスを提供する。

ADS構成要素（通常走行用ECU、MRC用ECU、E2E AIモデル、ADS基盤ソフトウェア）はTuringの責任領域だが、車両プラットフォームへの組込時のセキュリティ要件は、OEM車両CSMSと整合させる。

### 14.4.4 分担の具体化先

本節の分担を具体化する文書は、以下である。

| 文書 | 役割 |
| --- | --- |
| 車両要求仕様書（03_Vehicle_Requirements_Specification_draft.md）第10章 | OEM側に提示するCS要件 |
| VMC I/F仕様書（02_VMC_IF_Specification_draft.md）第6.4節 | I/F上のCSメカニズム |
| Cybersecurity Case | TARA、CS Concept、対策、検証エビデンス、CSMS文書 |
| OEM-Turing協定書（Cybersecurity Annex） | 鍵管理主体、SOC連携、PSIRT手順、脅威インテリジェンス共有、事故対応 |
| モデル更新管理書 | AIモデル・ADS構成要素の更新時のCS要件 |
| 運用文書群（SOC、PSIRTプレイブック） | 運用フェーズの手続き |

---

## 14.5 UN-R 155準拠とCybersecurity Caseへの参照

### 14.5.1 UN-R 155への準拠方針

UN-R 155は、車両のサイバーセキュリティ管理システム（CSMS）規則であり、型式認証の前提となる。Turingは、本Phaseにおいて、UN-R 155の要求事項にOEMと共同で準拠する方針を採る。

| UN-R 155要求項目 | 本書での扱い | 主たる対応文書 |
| --- | --- | --- |
| 7.2 CSMS要件（プロセス・組織・継続性）| 本書第14章 + 共同CSMS | Cybersecurity Case + OEM側CSMS文書 |
| 7.3 リスク管理プロセス | TARA | Cybersecurity Case |
| 7.4 サイバーセキュリティ脅威への対策 | 本書14.2 + 詳細対策 | Cybersecurity Case + 車両要求仕様書第10章 |
| Annex 5 Part A: Threats（脅威リスト） | 攻撃面整理（14.2）の起点 | Cybersecurity Case「脅威リスト」 |
| Annex 5 Part B: Mitigations（対策リスト） | 14.2の対策方針の起点 | Cybersecurity Case「対策リスト」 |
| Annex 5 Part C: Monitoring（運用後監視）| 運用文書群 | SOC・PSIRT文書 |

UN-R 155の対応は、ISO/SAE 21434に基づくCybersecurity Caseとして整備し、車両型式の認証申請時にOEMと共同で提出する。

### 14.5.2 ISO/SAE 21434との関係

本書では、ISO/SAE 21434を、UN-R 155準拠の実装手段として位置付ける。ISO/SAE 21434の各Clauseと本書の対応は、Appendix EおよびCybersecurity Caseで整理する。本書本章で確定する範囲は、第6.8節および本章で示した位置付けに限定する。

| Clause | 本書での扱い | 一次出典 |
| --- | --- | --- |
| Clause 5: Organization | 14.4 + 共同CSMS | Cybersecurity Case |
| Clause 6: Project dependent | Cybersecurity Case | Cybersecurity Case |
| Clause 7: Continuous activities | 14.3 + 14.4 | Cybersecurity Case + 運用文書 |
| Clause 8: TARA | 14.2 + 14.3.3 | Cybersecurity Case |
| Clause 9: Concept | 14.3 | Cybersecurity Case |
| Clause 10: Product development | 14.4 + 車両要求仕様書第10章 | Cybersecurity Case + 衛星文書 |
| Clause 11: Cybersecurity validation | Cybersecurity Case + 検証文書 | 衛星文書 |
| Clause 12: Production | OEM側 | 車両要求仕様書 + OEM文書 |
| Clause 13: Operations & maintenance | 14.4.2 SOC・PSIRT | 運用文書群 |
| Clause 14: End of cybersecurity support | Phase 3で確定 | — |
| Clause 15: Threat intelligence | 14.4.2 共有 | 運用文書群 |
| Annex A: Examples | 観点参照 | Cybersecurity Case |

### 14.5.3 UN-R 156（SUMS）との接続

UN-R 156（Software Update Management System）は、車両ソフトウェア更新規則であり、サイバーセキュリティと連動する。AIモデル・ECU FW・ADS構成要素のOTA更新は、ISO 24089に基づき、UN-R 156準拠で行う。本章本節では、その接続点のみを示し、詳細はモデル更新管理書で扱う。

| 接続観点 | 内容 |
| --- | --- |
| 配信経路の真正性 | OTAサーバ〜車両間の認証、署名検証 |
| 配信物の整合性 | ハッシュ・署名・ロールバック耐性 |
| 通常走行系/MRC系の系間バージョン整合 | rolling update中の不整合状態の許容範囲とMRC遷移ルール（6.7、9.10） |
| 更新後検証 | 更新後の自己診断・健全性確認 |
| 更新失敗時の挙動 | ロールバックの安全側挙動 |

### 14.5.4 衛星文書Cybersecurity Caseへの参照

本章の主張・方針を支える実体的なエビデンスは、衛星文書Cybersecurity Caseで整備する。Cybersecurity Caseが扱う内容は、以下である。

| 区分 | 内容 |
| --- | --- |
| 組織・プロセス | CSMSの組織構造、役割、レビュープロセス、継続的活動 |
| TARA | Item Definition、資産特定、Threat Scenario、Attack Path、Impact/Feasibility評価、リスク決定 |
| CS Concept | Cybersecurity Goals、Cybersecurity Requirements、Cybersecurity Controlsの導出 |
| Product Development | 設計エビデンス、実装エビデンス、テストエビデンス（Pen-test、Fuzzing、Static analysis、Code review） |
| Validation | CS Validation結果 |
| Production | 製造時のセキュリティ実装エビデンス（OEM主管） |
| Operations | SOCプレイブック、PSIRT手順、脅威インテリジェンス、Incident Responseプロセス |
| Maintenance | パッチ管理、End of cybersecurity support方針（Phase 3で確定） |
| Safety/Security Interface Document | HARA-TARA整合、Safety Goal-Cybersecurity Goal整合、残存リスク統合 |
| UN-R 155 CSMS文書 | 認証申請時にOEMと共同提出 |

### 14.5.5 本章の安全主張

本章の安全主張は、以下である。

*Turingは、本書が依拠する入力・出力・Arbitration・I/F・ログ・更新・通信のそれぞれについて、ISO/SAE 21434に基づくTARAを実施し、UN-R 155のCSMS要件にOEMと共同で準拠する。サイバー側の対策は、機能安全機構と二重化して動作するように設計し、いずれか一方の単独故障または単独の攻撃成功により、本書の最上位安全主張が無効化されない構造とする。残存するサイバー残存リスクは、本書第21章において、機能安全側残存リスクと統合的に管理する。*

本主張の実体的根拠（TARA結果、CS Concept、実装エビデンス、検証エビデンス、CSMS）は、衛星文書Cybersecurity Caseで提示する。

---

# 参考：本ドラフトと初版・第2版章立ての対応

| 第2版節 | 状態 | 初版での位置付け |
| --- | --- | --- |
| 14.1 Cybersecurity Caseの位置付け | **新設** | 初版6.8で最低限の言及のみ |
| 14.2 主要攻撃面と対策の概要 | **新設** | 初版なし |
| 14.3 Safety/Security Co-Engineering | **新設** | 初版なし |
| 14.4 OEM-Turing分担 | **新設** | 初版第15章「責任分界」の一部観点を継承し再整理 |
| 14.5 UN-R 155準拠とCybersecurity Caseへの参照 | **新設** | 初版6.8の参照を独立章へ昇格 |

初版第14章「安全論証を支える証拠の位置づけ」は、第2版章立てでは第20章へ移動する。

---

Turing Confidential Draft
