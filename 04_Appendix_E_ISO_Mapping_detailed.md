# Appendix E. ISO・規制対応マップ（詳細版）

本Appendixは、Turing_Safety_Claim 第2版において、初版Appendix Eを章・要求項目単位に詳細化したものである。

---

# E.0 凡例

## 対応区分

各要求項目について、本書（Turing Safety Claim）の対応状態を以下の四区分で示す。

| 区分 | 意味 |
| --- | --- |
| **フル対応** | 本書または衛星文書で要求項目に対応する論証・実装・エビデンスを提供する |
| **観点参照** | 要求項目の考え方を本書で参照するが、形式的な準拠は目的としない |
| **将来対応** | 現時点では対応しないが、Phase 2以降で対応する計画 |
| **不対応** | 対応しない。理由を併記する |

## 一次出典

Turing Safety Claim、衛星文書、後続証拠文書のいずれが一次出典かを示す。

---

# E.1 ISO/TS 5083:2025（ADS Safety）

ISO/TS 5083:2025は、ADSの設計・検証・妥当性確認に関する包括的なフレームワークである。本書は、本TSをトップレベルの構造的参照として用いる。

| 章/要求項目 | 区分 | 本書での対応 | 一次出典 |
| --- | --- | --- | --- |
| Clause 5: Safety lifecycle | フル対応 | TSC第1章（位置付け）、第20章（証拠の位置づけ）、第21章（更新方針） | TSC本書 |
| Clause 6: Safety assurance | フル対応 | TSC第4章（最上位安全主張）、第5章（論証の全体構造） | TSC本書 |
| Clause 7: ODD specification | フル対応 | TSC第7章 + ODD定義書 | ODD定義書 |
| Clause 8: Hazard analysis & risk assessment | フル対応 | TSC第4章（HARA要約）+ HARA文書 | HARA文書 |
| Clause 9: Safety concept | フル対応 | TSC第4章〜第13章 | TSC本書 |
| Clause 10: Verification | フル対応 | TSC第20章 + 検証計画書群 | 検証文書群 |
| Clause 11: Validation | フル対応 | TSC第20章 + 妥当性確認エビデンス | 検証文書群 |
| Clause 12: Safety case | フル対応 | TSC全体 + 衛星文書群（Safety Caseのハブ）| TSC本書 |
| Annex（AI）| 観点参照 | TSC第8章 + AI Safety Case | AI Safety Case |

---

# E.2 ISO 26262:2018（Functional Safety）

ISO 26262は、車両電子システムの機能安全規格である。本書は、車両アーキテクチャ起因の失陥（HW失陥、systematic failure）について、本規格を主要参照として用いる。

| Part / Clause | 区分 | 本書での対応 | 一次出典 |
| --- | --- | --- | --- |
| Part 2: Safety management | フル対応 | TSC第17章（責任分界）、第20章（証拠）、Phase別運用 | TSC本書 |
| Part 3: Concept phase – Item Definition | フル対応 | TSC第2章（対象システム概要） | TSC本書 |
| Part 3: HARA | フル対応 | TSC第4章（HARA要約）+ HARA文書 | HARA文書 |
| Part 3: Functional Safety Concept | フル対応 | TSC第4〜13章 | TSC本書 |
| Part 4: System level – Technical Safety Concept | フル対応 | 車両要求仕様書 + VMC I/F仕様書 | 衛星文書 |
| Part 4: Hardware-Software interface | フル対応 | VMC I/F仕様書 | VMC I/F |
| Part 5: Hardware – Hardware safety analysis | 観点参照 | TSC第10章 + 車両要求仕様書 | 車両要求仕様書 |
| Part 5: Latent fault metric (LFM) | フル対応 | TSC第6.3章（拡充）+ 車両要求仕様書 | 車両要求仕様書 |
| Part 5: Single point fault metric (SPFM) | フル対応 | 車両要求仕様書 + FMEA | FMEA |
| Part 5: PMHF（確率的目標）| 観点参照 | 車両要求仕様書 | 車両要求仕様書 |
| Part 6: Software | フル対応 | ADS設計書 + AI Safety Case | 衛星文書 |
| Part 6: Software unit testing | フル対応 | ADS検証計画書 | 検証文書 |
| Part 7: Production, operation, service, decommissioning | フル対応 | 車両要求仕様書第12章、運用文書群 | 衛星文書 |
| Part 8: Supporting processes | フル対応 | 衛星文書群（プロセス文書） | 衛星文書 |
| Part 9: ASIL-oriented and safety-oriented analyses | フル対応 | TSC第6.3章、HARA、FMEA、FTA、DFA | 衛星文書 |
| Part 9: Dependent Failure Analysis (DFA) | フル対応 | TSC第9.10章（CCF）+ DFA文書 | TSC + DFA文書 |
| Part 9: Cascading Failure | フル対応 | TSC第9.10章（拡充） | TSC本書 |
| Part 10: Guideline | 観点参照 | 全章で考え方を参照 | TSC本書 |
| Part 11: Adaptation for semiconductors | 観点参照 | 通常走行用ECU/MRC用ECU Safety Manual準拠 | ECUサプライヤSafety Manual |
| Part 12: Adaptation for motorcycles | 不対応 | 対象外 | — |

**E.2 補足**：本書が提示するE2E AI型ADSは、ISO 26262の典型的なソフトウェア構造（モジュラー設計、要求トレーサビリティ、ユニットテスト）と必ずしも一致しない。AI部分はISO/PAS 8800で扱い、26262は車両アーキテクチャ・ECU・Safety Mechanism実装に対して適用する、という方針を明示する。

---

# E.3 ISO 21448:2022（SOTIF）

ISO 21448は、意図された機能の安全性（性能限界・想定外シナリオによるリスク）を扱う。本書はSOTIFをE2E AIの性能限界・トリガー条件の体系として参照する。

| 章/要求項目 | 区分 | 本書での対応 | 一次出典 |
| --- | --- | --- | --- |
| Clause 5: SOTIF activities | フル対応 | TSC第6.4章、第8章 | TSC本書 |
| Clause 6: Functional & system specification | フル対応 | TSC第8章、AI Safety Case | TSC + AI Safety Case |
| Clause 7: Identification & evaluation of hazards | フル対応 | TSC第4章、HARA文書 | HARA |
| Clause 8: Specification & design | フル対応 | TSC第8章、AI Safety Case | AI Safety Case |
| Clause 9: Triggering conditions identification | フル対応 | TSC第7.4章（ODD境界）+ 第8.5章 + ODD定義書 | TSC + ODD定義書 |
| Clause 9: Triggering conditions と本書概念のマッピング | フル対応 | TSC第6.4章（用語マッピング） | TSC本書 |
| Clause 10: V&V | フル対応 | AI Safety Case + 検証文書群 | AI Safety Case |
| Clause 11: Operation phase activities | フル対応 | TSC第21章、運用文書群 | TSC + 運用文書 |
| Annex C: Triggering conditions examples | 観点参照 | お台場ODD定義書での具体化 | ODD定義書 |
| Misuse（特に乗員misuse）| フル対応 | TSC第6.4章（追加）、内向けHMI仕様書 | TSC + HMI仕様書 |

---

# E.4 ISO/PAS 8800:2024（Safety and AI）

ISO/PAS 8800は、AIを含むシステムの安全性を扱う規格である。本書のE2E AI部分はこの規格を主要参照とする。

| 章/要求項目 | 区分 | 本書での対応 | 一次出典 |
| --- | --- | --- | --- |
| Clause 5: AI safety lifecycle | フル対応 | AI Safety Case（衛星文書）| AI Safety Case |
| Clause 6: AI item definition | フル対応 | TSC第8章 + AI Safety Case | AI Safety Case |
| Clause 7: AI safety requirements | フル対応 | TSC第8.8章（新節）+ AI Safety Case | AI Safety Case |
| Clause 8: Data-driven design – Data lifecycle | フル対応 | AI Safety Case「データライフサイクル」 | AI Safety Case |
| Clause 8: Data quality | フル対応 | AI Safety Case「データ品質管理」 | AI Safety Case |
| Clause 8: Data coverage / completeness | フル対応 | AI Safety Case「データ網羅性」+ ODD定義書 | AI Safety Case |
| Clause 8: Data bias | フル対応 | AI Safety Case「データバイアス分析」 | AI Safety Case |
| Clause 9: Model design & training | フル対応 | AI Safety Case | AI Safety Case |
| Clause 9: Uncertainty quantification | フル対応 | AI Safety Case「Epistemic/Aleatoric uncertainty」 | AI Safety Case |
| Clause 9: OOD detection | フル対応 | AI Safety Case「Out-of-Distribution検知」 | AI Safety Case |
| Clause 10: Verification | フル対応 | AI Safety Case + 検証文書群 | AI Safety Case |
| Clause 11: Validation | フル対応 | AI Safety Case + フィールド検証 | AI Safety Case |
| Clause 12: Operation & monitoring | フル対応 | TSC第13章（ログ）+ 運用文書群 | 運用文書 |
| Clause 12: Continuous learning / model update | フル対応 | TSC第6.7章（ISO 24089）+ モデル更新管理書 | モデル更新管理書 |

**E.4 補足**：初版Turing Safety ClaimではPAS 8800への言及が限定的であった。第2版ではPAS 8800を「E2E AI部分の主要参照」として位置付け直し、AI Safety Caseという衛星文書で実体を整備する。

---

# E.5 ISO 34502:2022 / 34503（Scenario-based safety）

ISO 34502系は、シナリオベース安全評価のフレームワークである。本書は、E2E AI検証のシナリオ網羅性論証で本規格を参照する。

| 章/要求項目 | 区分 | 本書での対応 | 一次出典 |
| --- | --- | --- | --- |
| ISO 34502: Scenario-based safety evaluation framework | フル対応 | 検証計画書、AI Safety Case | 検証文書 |
| ISO 34501: Vocabulary | 観点参照 | TSC第3章（用語）、Appendix F | TSC本書 |
| ISO 34503: ODD taxonomy | フル対応 | TSC第7章 + ODD定義書 | ODD定義書 |
| ISO 34504: Scenario categories | 観点参照 | 検証計画書 | 検証文書 |
| ISO 34505: Scenario evaluation methods | 観点参照 | 検証計画書 | 検証文書 |

---

# E.6 ISO 24089:2023（Software Update Engineering）

ISO 24089は、車両ソフトウェア更新の機能安全規格である。本書はOTAおよびモデル更新で本規格を参照する。

| 章/要求項目 | 区分 | 本書での対応 | 一次出典 |
| --- | --- | --- | --- |
| Clause 5: Update management | フル対応 | TSC第6.7章 + モデル更新管理書 | モデル更新管理書 |
| Clause 6: Software update package | フル対応 | モデル更新管理書 + Cybersecurity Case | 衛星文書 |
| Clause 7: Update process | フル対応 | モデル更新管理書 | モデル更新管理書 |
| Clause 8: Verification & validation of update | フル対応 | モデル更新管理書 + 検証文書 | 衛星文書 |
| Rolling update中の通常走行系/MRC系不整合の扱い | フル対応 | TSC第6.7章（追記）+ モデル更新管理書 | TSC + 衛星文書 |
| Rollback要件 | フル対応 | モデル更新管理書 + 車両要求仕様書第10章 | 衛星文書 |
| OEM-Turing協調更新 | フル対応 | モデル更新管理書 + 車両要求仕様書第13章 | 衛星文書 |

---

# E.7 ISO/SAE 21434:2021（Cybersecurity）

ISO/SAE 21434は、車両サイバーセキュリティ工学規格である。本書はUN-R 155準拠の前提として参照する。

| 章/要求項目 | 区分 | 本書での対応 | 一次出典 |
| --- | --- | --- | --- |
| Clause 5: Organization | フル対応 | Cybersecurity Case「組織・プロセス」 | CS Case |
| Clause 6: Project dependent | フル対応 | Cybersecurity Case | CS Case |
| Clause 7: Continuous activities | フル対応 | TSC第14章 + Cybersecurity Case | CS Case |
| Clause 8: Risk assessment methods – TARA | フル対応 | Cybersecurity Case「TARA」 | CS Case |
| Clause 9: Concept | フル対応 | Cybersecurity Case「CS Concept」 | CS Case |
| Clause 10: Product development | フル対応 | Cybersecurity Case + 車両要求仕様書第10章 | 衛星文書 |
| Clause 11: Cybersecurity validation | フル対応 | Cybersecurity Case + 検証文書 | 衛星文書 |
| Clause 12: Production | フル対応 | 車両要求仕様書第12章 | 衛星文書 |
| Clause 13: Operations & maintenance | フル対応 | 運用文書群（SOC、PSIRT） | 運用文書 |
| Clause 14: End of cybersecurity support | 将来対応 | Phase 3で確定 | — |
| Clause 15: Threat intelligence | フル対応 | Cybersecurity Case + 運用文書 | 衛星文書 |
| Annex A: Examples | 観点参照 | Cybersecurity Case | CS Case |

**E.7 補足**：初版Turing Safety Claimでは6.8で最低限の言及にとどまっていた。第2版では第14章を独立化し、衛星文書Cybersecurity Caseとして実体整備する。

---

# E.8 UL 4600:2023（Safety Case for Autonomous Products）

UL 4600は、自律製品のSafety Caseフレームワークである。E2E AI型ADSとの相性が良く、参照価値がある。

| 章/要求項目 | 区分 | 本書での対応 | 一次出典 |
| --- | --- | --- | --- |
| Section 5: Safety case structure | フル対応 | TSC全体（GSN相当のArgumentation構造）| TSC本書 |
| Section 6: Risk identification | フル対応 | TSC第4章、HARA文書 | HARA |
| Section 7: Hazards & sources of variation | フル対応 | TSC第7章（ODD）、ODD定義書 | ODD定義書 |
| Section 8: Autonomy functions | フル対応 | TSC第8章、AI Safety Case | AI Safety Case |
| Section 9: Software & system engineering process | フル対応 | TSC第20章、衛星文書群 | TSC本書 |
| Section 10: Dependability | フル対応 | TSC第9〜10章、車両要求仕様書 | 衛星文書 |
| Section 11: Data | フル対応 | AI Safety Case | AI Safety Case |
| Section 12: V&V | フル対応 | TSC第20章、検証文書群 | 検証文書 |
| Section 13: Tool qualification, COTS, legacy | 将来対応 | Phase 2で整備 | — |
| Section 14: Lifecycle concerns – field engineering, OTA | フル対応 | モデル更新管理書、運用文書 | 衛星文書 |
| Section 15: Maintenance & metrics | フル対応 | 運用文書群、TSC第21章 | 運用文書 |
| Section 16: Assessment | フル対応 | TSC全体（GSN相当）+ 第三者評価プロセス | TSC本書 |
| Edge case enumeration | 観点参照 | お台場ODD定義書、AI Safety Case | ODD定義書 |
| Argumentation structure | 観点参照 | TSC全体構造 | TSC本書 |

**E.8 補足**：UL 4600の参照は初版にはなかった。第2版で第6.10章として位置付け、E2E AI型ADSへの相性の良さを活用する。

---

# E.9 UN-R 157（ALKS / 自動運転）

UN-R 157は、UNECE WP.29における自動運転規則であり、L3 ALKSをカバーする。L4向け規則は将来整備されるが、現状ではDSSAD要件など参照価値が高い。

| 要求項目 | 区分 | 本書での対応 | 一次出典 |
| --- | --- | --- | --- |
| 5.1 General requirements | 観点参照 | TSC第2、4、5章 | TSC本書 |
| 5.1.1 Avoidance of collisions | フル対応 | TSC第8、9、10、11章 | TSC本書 |
| 5.1.2 Manoeuvring | フル対応 | TSC第8、11章 | TSC本書 |
| 5.1.4 Dynamic driving task | フル対応 | TSC第8、9章 | TSC本書 |
| 5.1.5 Minimum risk manoeuvre (MRM) | フル対応 | TSC第11章（MRC）| TSC本書 |
| 5.2 ODD | フル対応 | TSC第7章 + ODD定義書 | ODD定義書 |
| 5.3 Driver availability | 不対応（理由：L4のため運転者前提なし） | TSC第3.1章で明示 | — |
| 5.4 Failsafe response | フル対応 | TSC第9、10、11章 | TSC本書 |
| 6 DSSAD（Data Storage System for Automated Driving）| フル対応 | TSC第13章（再構成）+ ログ項目定義書 | TSC + ログ定義書 |
| 6.1 DSSAD: Data elements | フル対応 | TSC第13章 + ログ項目定義書 | ログ定義書 |
| 6.2 DSSAD: Activation/deactivation logging | フル対応 | TSC第13章 | TSC本書 |
| 6.3 DSSAD: Transition demand logging | フル対応 | TSC第13章 + VMC I/F仕様書 | 衛星文書 |
| 6.4 DSSAD: Override logging | フル対応 | TSC第13章 | TSC本書 |
| 6.5 DSSAD: MRM logging | フル対応 | TSC第13章 | TSC本書 |
| 6.6 DSSAD: System failure logging | フル対応 | TSC第13章 + VMC I/F仕様書第9章 | 衛星文書 |
| 6.7 DSSAD: Storage requirements | フル対応 | ログ項目定義書 | ログ定義書 |
| 7 Cybersecurity (UN-R 155連携) | フル対応 | TSC第14章 + Cybersecurity Case | CS Case |
| 8 Software updates (UN-R 156連携) | フル対応 | モデル更新管理書 | モデル更新管理書 |
| Annex 4: New Assessment Test Procedures | 観点参照 | 検証文書群 | 検証文書 |
| Annex 5: Audit & Reporting | フル対応 | TSC第18、20章 | TSC本書 |

**E.9 補足**：UN-R 157はL3 ALKS向けだが、L4向け規則整備に向けてWP.29 GRVAで議論が進む。本書はL4向け規則整備への日本側貢献を視野に、UN-R 157の構造を参考としつつL4特有の要件（MRC、運転者非前提）を本書独自に整理する。

---

# E.10 UN-R 155（Cybersecurity）

UN-R 155は、車両のサイバーセキュリティ管理システム（CSMS）規則である。型式認証の前提となる。

| 要求項目 | 区分 | 本書での対応 | 一次出典 |
| --- | --- | --- | --- |
| 7.2 CSMS要件 | フル対応 | TSC第14章 + Cybersecurity Case | CS Case |
| 7.3 リスク管理プロセス | フル対応 | Cybersecurity Case「TARA」 | CS Case |
| 7.4 サイバーセキュリティ脅威への対策 | フル対応 | Cybersecurity Case「対策」 | CS Case |
| Annex 5 Part A: Threats | フル対応 | Cybersecurity Case「脅威リスト」 | CS Case |
| Annex 5 Part B: Mitigations | フル対応 | Cybersecurity Case「対策リスト」 | CS Case |
| Annex 5 Part C: Monitoring | フル対応 | 運用文書（SOC、PSIRT） | 運用文書 |

---

# E.11 UN-R 156（Software Update）

UN-R 156は、車両ソフトウェア更新管理システム（SUMS）規則である。

| 要求項目 | 区分 | 本書での対応 | 一次出典 |
| --- | --- | --- | --- |
| 7.1 SUMS要件 | フル対応 | モデル更新管理書 | モデル更新管理書 |
| 7.1.1 ソフトウェア識別 | フル対応 | 車両要求仕様書第12.1章（VIN単位構成管理） | 衛星文書 |
| 7.1.2 更新プロセス | フル対応 | モデル更新管理書 | モデル更新管理書 |
| 7.2 OTA要件 | フル対応 | モデル更新管理書 + 車両要求仕様書第10.3章 | 衛星文書 |

---

# E.12 UN-R 152（AEBS）等の関連規則

| 要求項目 | 区分 | 本書での対応 | 一次出典 |
| --- | --- | --- | --- |
| UN-R 152（AEBS）| 観点参照 | 車両要求仕様書第3章（緊急ブレーキ性能） | 衛星文書 |
| UN-R 79（操舵）| 観点参照 | 車両要求仕様書第4章 | 衛星文書 |
| UN-R 13-H（制動）| 観点参照 | 車両要求仕様書第3章 | 衛星文書 |
| UN-R 10（EMC）| フル対応 | 車両要求仕様書第8.3章、第6章 | 衛星文書 |
| UN-R 100（HV安全）| フル対応 | 車両要求仕様書第6章 | 衛星文書 |

---

# E.13 IEEE / SAE 関連規格

| 規格 | 区分 | 本書での対応 |
| --- | --- | --- |
| IEEE 802.1AS（gPTP）| フル対応 | VMC I/F仕様書第7章 |
| IEEE 802.1Qbv（TSN Time-Aware Shaper）| フル対応 | VMC I/F仕様書第2.2章、第7章 |
| IEEE 802.1CB（FRER）| フル対応 | VMC I/F仕様書第2.3章、車両要求仕様書第7章 |
| ISO 14229（UDS）| フル対応 | VMC I/F仕様書第9章 |
| AUTOSAR E2E Profile | フル対応 | VMC I/F仕様書第6章 |
| SAE J3016（Levels of Driving Automation）| 観点参照 | TSC第3章 |

---

# E.14 日本国内法令との対応

詳細はAppendix H（法令対応マップ）を参照。本Appendix Eでは概要のみ示す。

| 法令・規則 | 区分 | 本書での対応 | 一次出典 |
| --- | --- | --- | --- |
| 道路運送車両法 | フル対応 | TSC第15章 + Appendix H | TSC + Appendix H |
| 保安基準（道路運送車両の保安基準）| フル対応 | TSC第15章 + 車両要求仕様書 + Appendix H | 衛星文書 |
| 道路交通法 | フル対応 | TSC第15章 + Appendix H | TSC + Appendix H |
| 特定自動運行制度（道交法第5章の3）| フル対応 | TSC第12.5章、第15.3章、第18章 + 特定自動運行計画書 | 衛星文書 |
| 個人情報保護法（DSSADデータ等）| フル対応 | TSC第13章 + データ保護方針書 | データ保護方針書 |

---

# E.15 不対応項目の理由整理

本書が「不対応」とする項目とその理由を整理する。

| 規格・要求 | 不対応の理由 |
| --- | --- |
| ISO 26262 Part 12（motorcycles）| 対象車両がモーターサイクルではないため |
| UN-R 157 5.3 Driver availability | L4自動運転を対象とするため、運転者の介入を前提としない |
| ISO/SAE 21434 Clause 14 End of cybersecurity support | Phase 3（量産フェーズ）で確定する。現Phaseでは対応しない |
| UL 4600 Section 13 Tool qualification (一部) | Phase 2で整備する。現Phaseでは観点参照のみ |

---

# E.16 観点参照項目の扱い

「観点参照」とは、規格の考え方を本書設計に反映するが、形式的な準拠（チェックリスト合格）は目的としないことを意味する。これは初版Turing Safety Claim 6.1の方針「ISO準拠ではなく抜け漏れチェックと共通言語のための参照」を、項目レベルで具体化したものである。

「観点参照」とした項目について、当局審査・第三者評価の場で「なぜ準拠主張ではなく観点参照とするのか」を説明できるよう、本書および衛星文書群で論拠を整備する。

---

# E.17 マップの更新管理

本Appendix Eは、Turing Safety Claim本書の改版、ISO規格の改訂、UN規則の改訂、衛星文書群の整備状況に応じて更新する。

更新時は、以下を確認する。
新規格・新規則の出版（特にL4向けUN規則整備）／ISO/PAS 8800の本番規格化／既存衛星文書の改版／本書の章番号変更／対応区分の変更（観点参照→フル対応への昇格、将来対応の対応開始）。

---

Turing Confidential Draft
