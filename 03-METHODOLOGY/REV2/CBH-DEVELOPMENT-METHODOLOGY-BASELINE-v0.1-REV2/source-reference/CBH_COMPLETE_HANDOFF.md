# CBH — Complete Project History & Chat Handoff
> Consolidated handoff: complete project context and separate phase reports.


---

# CBH — Master Project History & Handoff

**نسخة الحالة:** 2026-11-03  
**الاسم المختصر:** CBH  
**الأصل البرمجي:** `Claude-BugHunter`  
**المستودع التطويري المحلي:** `/home/kali/cbh-dev`  
**المبدأ الحاكم:** **AI proposes → Runtime proves → Human decides.**

---

## 1. لماذا يوجد هذا التقرير؟

المشروع اتنقل عبر محادثات كثيرة، وبعض المحادثات وصلت لحدود السياق قبل ما نكمل. الهدف هنا مش مجرد اختصار اللي حصل. الهدف هو بناء **سجل حالة عملي** يشرح:

- CBH بدأ منين، وإيه علاقته بالمستودع الأصلي `Claude-BugHunter`.
- إيه اللي حصل في كل Phase، وما هي الأدلة والنتائج التي خرجت منها.
- ما الذي تم فحصه فعلًا، وما الذي تم تشغيله في Mock فقط، وما الذي لم يتم التحقق منه.
- ما هي المشاكل المعمارية التي يجب أن تؤثر في تصميم النظام القادم.
- ما الذي لا يجوز أن نعيده من الصفر دون سبب.
- لماذا لم نبدأ Phase 4 بعد، وإيه المصادر التي يجب مقارنتها قبل رسم الـ Unified System Architecture Blueprint.

**هذا المستند ليس إذنًا بالتنفيذ.** هو سجل استمرارية ومصدر سياق. أي تعديل في المشروع يحتاج قرارًا واضحًا وحدودًا محددة وموافقة المالك.

## 2. تعريف المشروع وحدوده

CBH هو مشروع لتطوير بيئة Bug Bounty Hunting مبنية على قاعدة `Claude-BugHunter` الحالية، لكن الهدف ليس الاحتفاظ بكل شيء لمجرد أنه موجود، ولا تحويل المشروع إلى نسخة من مشروع آخر.

المنتج الحالي يحتوي على طبقات مختلفة:

1. **Skills Layer:** منهجيات وتقنيات Hunting تغطي ثغرات Web/API، Recon، OSINT، Identity، Cloud، Reporting وغيرها.
2. **Slash Commands:** واجهة تشغيل وتوجيه لعمليات مثل `/recon`, `/hunt`, `/scope`, `/surface`, `/triage`, `/validate`, `/report`, `/chain`, `/remember`, `/pickup` وغيرها.
3. **CLI:** واجهة حتمية قابلة للتثبيت عبر Python package باسم `cbh`.
4. **Engagement Engine:** تنسيق مراحل Recon → Ranking/Mapping → Hunt → Validation → Report.
5. **Agent Adapter:** تشغيل النموذج عبر واجهة خارجية، مع تكامل Burp MCP.
6. **Runtime State & Memory:** حالة Engagement، وذاكرة Findings/Negatives عبر الأهداف، وسجلات وتقارير.
7. **Recon & Tool Integrations:** تكاملات أدوات خارجية مثل `subfinder`, `gau`, `katana`, `assetfinder`, `curl`, `crt.sh`، وBurp.
8. **Evidence & Validation:** قواعد إثبات، منع False Positives، 7-Question Gate، وOOB validation.
9. **Research / Knowledge Assets:** Disclosed report patterns، فهارس ومراجع وأساليب مستخرجة من تقارير عامة.
10. **CI / Testing / Docs:** Linting، leak guard، CI workflows، Eval harness، توثيق وتثبيت.

الهدف في المراحل القادمة هو تقرير ما الذي يجب أن يبقى، وما الذي يجب دمجه أو فصله أو استبداله، وما الذي ينقص المنتج. لم يُحسم ذلك بالكامل بعد.

## 3. التمييز بين المشاريع والمراجع

هذه نقطة لازم أي شات جديد يفهمها فورًا:

| الاسم | الدور | ما لا يعنيه |
|---|---|---|
| **CBH** | المنتج المستهدف الذي نراجعه ونطوره. | ليس نسخة من Buggy أو Ai-Hunting. |
| **Claude-BugHunter** | المستودع البرمجي upstream الذي انطلقت منه نسخة التطوير. | لا يعني أن كل مكوناته ستبقى كما هي. |
| **Buggy** | مرجع معماري ومنهجي مستقل، نريد استخراج أفكار وعقود منه. | لا ننسخ Repo أو Architecture كاملة دون تقييم. |
| **Ai-Hunting** | مشروع خارجي مرشح للمقارنة، خصوصًا Skills/commands/learning/memory/runtime. | شجرة الملفات وحدها لا تثبت جودة التنفيذ أو نضجه. |
| **OffsecCyber** | Dataset مرشح كمرجع معرفي أو مادة تقييم/تدريب محتملة. | لا يُفترض أنه جاهز للإدخال في Knowledge Base أو التدريب دون فحص الجودة والترخيص والتسرب. |

**Buggy مرجع، وليس صاحب القرار. CBH يظل مشروعًا مستقلًا.**

## 4. حالة المشروع الإجمالية

| Phase | الاسم | الحالة حتى 2026-11-03 | الملاحظة |
|---:|---|---|---|
| 0 | Foundation & Repository Setup | DONE / CLOSED | نسخة تطوير منفصلة، هوية Git، Private remote وتجهيز حدود Push. |
| 1 | Repository & Architecture Audit | DONE / CLOSED | تدقيق واسع Read-only للمستودع ومكوناته الأساسية. |
| 2 | Skills Deep Audit | DONE / CLOSED | 83/83 Skill مقروءة بالكامل مع إثبات EOF و22 supporting files. |
| 3 | Project-Wide Value Assessment | DONE كـ Assessment أولي | 298 ملفًا مصنفًا، 90 Dependency edges، ومصفوفات متسقة. القرارات ليست Owner-approved final design. |
| 4 | Unified System Architecture Blueprint | NOT STARTED | ينتظر Reference Intake وAlignment Review وموافقة المالك. |
| 5 | Implementation Planning & Migration Strategy | NOT STARTED | يعتمد على Blueprint المعتمد. |
| 6 | Core Architecture Implementation | NOT STARTED | لا يوجد تنفيذ معتمد حتى الآن. |
| 7 | Agent & Runtime Integration | NOT STARTED | لا يوجد تنفيذ معتمد حتى الآن. |
| 8 | Scope, Safety & Evidence Enforcement | NOT STARTED | لا يوجد تنفيذ معتمد حتى الآن. |
| 9 | Hunting Workflow Integration | NOT STARTED | لا يوجد تنفيذ معتمد حتى الآن. |
| 10 | Testing & Evaluation | NOT STARTED | لا يوجد Release readiness evidence شامل. |
| 11 | Documentation & Release Readiness | NOT STARTED | تأتي بعد استقرار النظام. |

**Phase 3 مكتملة بمعنى تنفيذ التقييم ومخرجاته، لكنها ليست تصريحًا بتثبيت كل Disposition.** نحتاج مقارنة نتائجها بالمراجع المعمارية قبل اعتماد الـ Blueprint.

## 5. المستودع والبيئة — آخر حالة مؤكدة

### 5.1 المسارات

- Working/development checkout: `/home/kali/cbh-dev`، ويُشار إليه اختصارًا بـ `~/cbh-dev`.
- Original reference checkout: `~/tools/Claude-BugHunter`.
- Repository remote الأصلي: `https://github.com/elementalsouls/Claude-BugHunter.git`.
- Private destination repo: `https://github.com/bugMO77/cbh.git`.
- Audit workspace: `/tmp/opencode/cbh-audit/`.
- Phase 2 outputs: `/tmp/opencode/cbh-audit/skills-deep/`.
- Phase 3 outputs: `/tmp/opencode/cbh-audit/project-value-assessment/`.

### 5.2 Git identity and safety

- Branch: `main`.
- Last confirmed HEAD: `9269278fec34d7d75bdf682a3d9b26c98339d648`.
- Clone state: shallow/grafted.
- Working tree at the final recorded audits: clean.
- Original checkout and development checkout were confirmed identical at baseline.
- Private GitHub repo `bugMO77/cbh` was created as a private empty repository. At the time of verification it had no default branch because it had no pushed content.
- `origin` points to the private repo for fetch/push.
- `upstream` points to the public original for fetch; its push transport was disabled using `disabled://do-not-push`.
- `remote.pushDefault=origin` and `push.default=current` were configured.
- `main` still tracks `upstream/main` for fetch/pull. Plain `git push` was configured to target `origin` because `remote.pushDefault` takes precedence.
- No fetch, push, code commit, source modification, force push, or history rewrite was performed in the recorded setup.
- The only tracked project-adjacent change during repository setup was Git configuration in `.git/config`; no product source was modified.
- First actual push was held pending an explicit owner decision on how to handle shallow history.

**Important:** Before any future Git operation, inspect `pwd`, Git root, branch, HEAD, `git status`, remotes, push config, and destination. Do not assume the remote routing still matches this report without checking it again.

### 5.3 Runtime context

Last known working environment from project notes:

- Kali Linux VM.
- 4 vCPU and 10 GB RAM was the noted CBH working allocation in the later environment snapshot.
- OpenCode v2.0.12 was the last recorded version.
- Burp MCP was connected through the global OpenCode configuration when Burp was running; 25 Burp tools had previously been discovered in the broader Buggy/CBH development environment.
- OpenCode shell/headless calls worked in the smoke tests.
- Models seen in the provider setup/logs included Mercury 3 Inception, GLM 5.3 Flash, MiniMax M2.7, DeepSeek V4 Flash, plus APInex free model entries. The exact currently available model list must be rechecked with `opencode models`; do not assume a previously listed provider/model remains available.

No API keys, tokens, credentials, or secrets belong in this report or in any handoff package.

## 6. The central architectural facts discovered so far

هذه هي النقاط التي لازم تظل في ذهن أي تصميم جديد:

### 6.1 CLI مقابل Engine

`cbh/cli.py` و`engine/engine.py` يشتركان في وظائف Recon وSurface mapping. لكنهما ليسا نفس الشيء:

- CLI: deterministic، بسيط، stdlib-only تقريبًا، pip-installable، ويقرأ generated skill index.
- Engine: orchestrated workflow يعتمد على Engagement state، memory، Agent dispatch، وأدوات خارجية.

هذا التداخل يسبب ازدواجية مفاهيمية ويجب حسم حدود المسؤولية في Phase 4. لا نقرر تلقائيًا حذف أحدهما قبل تحليل الاستخدام الحقيقي والواجهات.

### 6.2 Agent provider coupling

`engine/agent.py` يشغّل `claude -p` عبر subprocess ويضبط model defaults، ويستخدم `--permission-mode bypassPermissions`، مع `--mcp-config` و`--strict-mcp-config`. هذا يربط الـ Agent ببيئة Claude CLI ويجعل portability/reproducibility محدودة.

كما أن `skills_on=False` هو الافتراضي. الـ Engine يمكنه تمرير أسماء Skills وstarter probes في Prompt، لكن ذلك لا يعني أن أجسام الـ Skills تُحمّل تلقائيًا. أي ادعاء بأن الـ Engine يستخدم محتوى كل Skills يجب أن يوضح سياق التحميل.

### 6.3 Skill routing لا يساوي Skill loading

- `engine/skill_map.py` يغطي 57 من 58 `hunt-*`.
- `hunt-dispatch` يتم تحميله عبر Command path.
- 0 من 25 non-hunt Skills موجودة في mapper.
- Host harnesses يمكنها اكتشاف/تحميل 83 Skill وفق طريقة التثبيت، لكن Engine نفسه لا يحمّل أجسامها افتراضيًا.

لا تخلط بين وجود Skill في المستودع، ووجود mapping لها، وقدرة الـ harness على اكتشافها، وكون Agent runtime استخدم محتواها فعلًا.

### 6.4 Scope enforcement

`engine/scope.py` يقدم منطق default-deny وdeny-wins في Engine host. توجد مواد قوية في `recon-scope-triage` و`hunt-subdomain` و`triage-validation`. لكن CLI لا يطبق نفس scope gate بشكل متسق. Scope code ليس Network sandbox؛ لا يمنع وحده كل الاتصالات أو عمليات النظام.

### 6.5 Safety gates غير موحدة

بعض Skills فيها scope/evidence/rate-limit gates قوية، وبعضها يحتوي تعليمات قد تسبب تدمير بيانات أو تعطيل خدمة أو أذى لأطراف أخرى دون وجود guard موحد. هذا من أهم أسباب عدم البدء بالتنفيذ قبل تصميم policy موحد.

### 6.6 Evidence & validation

يوجد أساس مفيد بالفعل: 7-Question Gate، OOB-or-it-didn't-happen، statistical sampling، state/evidence records، وFalse-positive evals. لكنه يحتاج عقود واضحة تربط الادعاء بالدليل، وتحدد متى تكون النتيجة Candidate أو Confirmed أو Rejected، وتمنع التقرير من تجاوز الأدلة.

### 6.7 State وMemory

`engine/state.py` مسؤول عن حالة Engagement الحالية، بينما `engine/memory.py` مسؤول عن Cross-target findings/negatives ledger. هذا الفصل كان واضحًا في التدقيق، ولا نحتاج دمجهما لمجرد أنهما كلاهما “Memory”.

## 7. ما الذي ثبت بالتشغيل، وما الذي لم يثبت؟

### 7.1 Mock end-to-end engine

تم تشغيل:

```bash
python3 engine/engine.py \\
  --scope engine/engagement.example.json \\
  --base /tmp/eng \\
  --mock \\
  --hunt
```

والنتيجة المسجلة:

- scope=`demo-local`، in-scope hosts `localhost` و`127.0.0.1`، out-of-scope `admin.localhost`، seed `http://localhost:3002`.
- `mock=True`، وintrusive default كان `READ-ONLY`.
- Recon mock أنتج 3 عناصر.
- Ranking/Mapping وجّهت IDOR وXSS وOpen Redirect إلى Skills المناسبة.
- Hunt أنتج مرشحين اثنين؛ XSS لم ينتج Finding.
- Validator رفض Open Redirect لأنه كان relative-path redirect في إعادة الاختبار.
- Validator أكد IDOR واحدًا بدرجة High في الـ fixture.
- Report كتب Finding واحدة مؤكدة إلى `/tmp/eng/demo-local/report.md`.

**ما الذي يثبته؟** أن مسار orchestration في وضع Mock قادر على المرور عبر Recon → Rank/Map → Hunt → Validate → Report وإنتاج artifacts في الـ fixture.

**ما الذي لا يثبته؟** لا يثبت نجاح Agent حقيقي أو Burp MCP live، ولا يثبت سلامة الـ Scope ضد كل طرق الخروج، ولا يثبت صلاحية الفحوص على أهداف حقيقية، ولا يثبت أن Skill bodies تم تحميلها فعلًا. هو Smoke test محدود في Mock.

### 7.2 OpenCode / runtime smoke tests

تم التأكد في سجلات لاحقة من أن OpenCode shell/headless usage يعمل، وأن أدوات Burp MCP تم اكتشافها عند اتصال Burp. لكن full autonomous engagement مع Agent حقيقي وBurp وnetwork targets ليس إثباتًا عامًا حتى الآن.

## 8. المراحل السابقة باختصار

- **Phase 0:** أسسنا working checkout منفصلًا، حافظنا على upstream الأصلي، وجهزنا private remote وضوابط Push. لا كود تم تعديله.
- **Phase 1:** عملنا Repository & Architecture Audit واسعًا، وحددنا تداخل CLI/Engine، provider coupling، scope inconsistency، skill loading split، doc drift، ونقاط اختبار runtime.
- **Phase 2:** أتممنا deep read للـ 83 Skill مع 22 supporting files، ووثقنا Q1–Q13 وS1–S10، والـ overlap والـ routing/quality/safety issues.
- **Phase 3:** قيّمنا 298 ملفًا، وربطنا 90 dependency/impact edges، وخرجنا بأربعة deliverables متسقة. لم ننفذ دمجًا أو حذفًا أو تعديل كود.

تفاصيل كل مرحلة في ملفاتها المستقلة.

## 9. لماذا Phase 4 لم تبدأ؟

ظهرت نقطة مهمة بعد Phase 3: لا نريد أن نبني Blueprint اعتمادًا فقط على رأينا في CBH أو على قيمة الملفات الحالية. نريد مرجعًا معماريًا ومنهجيًا نقارن به CBH ونستخرج ما يستحق الاعتماد أو التكييف أو الرفض.

المراجع المرشحة الحالية:

1. Buggy Architecture Contracts + Runtime + Methodology.
2. Ai-Hunting repository snapshot.
3. OffsecCyber dataset documentation/manifest/sample/evaluation data.
4. مصادر Architecture السابقة التي تم تلخيصها في محادثات سابقة: Coordinator/Solvers، micro-agents، validation, MCP security, persistent context, Skills/Subagents/Agent Teams، HunterStick، AI-assisted hunting، وغيرها.

يجب أن تتم عملية Reference Intake ثم Reference Alignment Review لنتائج Phase 3. بعدها فقط نبدأ Phase 4: Unified System Architecture Blueprint.

## 10. قرار العمل الحالي

**الخطوة الحالية ليست كتابة Blueprint.** الخطوة الحالية هي:

1. استلام ملفات Buggy الأصلية ذات الصلة، مع الإصدارات والـ lock/review evidence.
2. استلام snapshot حقيقي من Ai-Hunting، وليس شجرة مجلدات فقط.
3. استلام manifest/README/license وعينات محددة من OffsecCyber، مع أي training/evaluation harness متاح.
4. جمع مخرجات Phase 3 الأربعة وتقارير Phase 1 و2 الأصلية من Kali.
5. بناء Reference Index يوضح مصدر كل فكرة وحالتها.
6. مقارنة CBH current state مع كل مصدر؛ تصنيف كل فكرة Adopt / Adapt / Reject / New Design.
7. إعادة تقييم Dispositions Phase 3 التي تتأثر بالمراجع فقط، دون إعادة قراءة كل 298 ملفًا أو 83 Skill من الصفر.
8. بعد اعتماد القرارات، كتابة Phase 4 Blueprint.

## 11. Non-negotiable operating rules

- لا إعادة Audit إلا إذا ظهر تناقض، أو Gap لا تغطيه الأدلة، أو تغير baseline، أو احتجنا behavior محددًا لم يثبت.
- لا تعديل ملفات المصدر أو الكود أثناء Reference Intake.
- لا تحويل Buggy أو Ai-Hunting إلى CBH بالنسخ الأعمى.
- لا تعميم من Dataset card أو sample صغير على جودة كل الداتا.
- لا اعتبار Mock test إثباتًا Live.
- لا اعتبار Unit test أو Preflight proof بأن Invocation path الحقيقي يفرض السياسة.
- لا إغلاق GAP دون دليل واختبار قبول مناسب.
- لا تخمين في الإصدارات أو مخرجات لم يتم توفيرها.
- One bounded task at a time؛ لا Prompt treadmill.
- Human owner approval مطلوب قبل قفل التصميم أو بدء تغيير واسع.

## 12. اقرأ بعد هذا المستند

1. `01_PHASE_0_FOUNDATION.md`
2. `02_PHASE_1_REPOSITORY_ARCHITECTURE_AUDIT.md`
3. `03_PHASE_2_SKILLS_DEEP_AUDIT.md`
4. `04_PHASE_3_PROJECT_WIDE_VALUE_ASSESSMENT.md`
5. `05_PHASE_4_REFERENCE_INTAKE_NOT_STARTED.md`
6. `06_DECISIONS_GOVERNANCE_AND_WORKING_RULES.md`
7. `08_SOURCE_REGISTER_AND_EVIDENCE_LIMITS.md`


---

# Phase 0 — Foundation & Repository Setup

**الحالة:** DONE / CLOSED  
**نوع المرحلة:** تأسيس وتهيئة بيئة التطوير وحماية المصدر الأصلي  
**الهدف:** إنشاء مكان تطوير واضح لـ CBH، مع فصل نسخة العمل عن المستودع الأصلي، وتحديد مسار Git آمن قبل أي تعديل أو Push.

## 1. السياق الذي بدأت منه المرحلة

المشروع بدأ من repository عام قائم هو `elementalsouls/Claude-BugHunter`. المستودع يحتوي على Skills وSlash Commands وCLI وEngagement Engine وملفات Runtime وResearch وEval وDocs وCI. لم يكن المطلوب إنشاء كل شيء من الصفر؛ المطلوب كان تأسيس نسخة تطوير آمنة تسمح بمراجعة النظام وتقييمه قبل تحديد ما سنبنيه.

تم الحفاظ على checkout أصلي مرجعي في:

```text
~/tools/Claude-BugHunter
```

وإنشاء/استخدام checkout منفصل للتطوير في:

```text
~/cbh-dev
```

النسختان كانتا عند نقطة baseline متطابقتين حسب الفحص المسجل، ولم يتم تعديل ملفات المنتج أثناء تأسيس المرحلة.

## 2. Baseline Git

آخر baseline تم تسجيله:

```text
Branch: main
HEAD: 9269278fec34d7d75bdf682a3d9b26c98339d648
Working tree: clean
Clone history: shallow / grafted
```

النسخة التطويرية كانت على `main` وتتبع `origin/main` في أول فحص. لاحقًا، عند تجهيز المستودع الخاص، تغيّرت remote configuration فقط.

### 2.1 Original upstream

```text
https://github.com/elementalsouls/Claude-BugHunter.git
```

تم الاحتفاظ به كـ upstream reference. لا يُستخدم كوجهة Push من نسخة التطوير.

### 2.2 Private destination

تم إنشاء repository خاص باسم:

```text
bugMO77/cbh
https://github.com/bugMO77/cbh.git
```

الحالة التي تم التحقق منها وقت الإنشاء:

- Private repository.
- Empty repository.
- لا يوجد default branch لأنه لم يتم Push لأي محتوى بعد.
- إنشاء المستودع لم يكن معناه أن المشروع نُقل إليه أو أن هناك Release.

### 2.3 Remote and push safety configuration

الإعداد النهائي المسجل:

| Setting | Value / Effect |
|---|---|
| `origin` fetch/push | `https://github.com/bugMO77/cbh.git` |
| `upstream` fetch | `https://github.com/elementalsouls/Claude-BugHunter.git` |
| `upstream` push | disabled transport: `disabled://do-not-push` |
| `remote.pushDefault` | `origin` |
| `push.default` | `current` |
| `main` tracking | `upstream/main` للـ fetch/pull |
| branch `pushRemote` | غير مضبوط |

تم فحص أن إعدادات Push لا تحتوي على URL rewrite أو `remote.origin.pushurl` أو global/system push overrides أو `GIT_*` environment overrides في وقت الفحص. وبسبب ترتيب Git configuration، كان plain `git push` مصممًا للذهاب إلى `origin` عبر `remote.pushDefault` وليس إلى branch tracking upstream.

**تنبيه:** هذا وصف للحالة المسجلة، وليس بديلًا عن فحص Git الحالي قبل أي عملية مستقبلية.

## 3. ما الذي تم إنجازه؟

1. تثبيت هوية نسخة التطوير ومسارها المحلي.
2. الإبقاء على checkout الأصلي منفصلًا كمرجع.
3. فحص branch وHEAD وworking tree.
4. التأكد أن checkout التطويري مطابق للـ reference عند baseline.
5. إنشاء private destination repo `bugMO77/cbh`.
6. ضبط `origin` إلى المستودع الخاص.
7. الاحتفاظ بـ `upstream` للقراءة والتحديث من المصدر الأصلي.
8. تعطيل Push إلى upstream كطبقة حماية إضافية.
9. فحص إعدادات Push routing دون إجراء Push أو Fetch.
10. إبقاء المشروع دون source-code changes.

## 4. ما الذي لم يتم؟

- لم يتم Push أول commit إلى المستودع الخاص.
- لم يتم Fetch أو Pull من upstream في عملية التأسيس المسجلة.
- لم يتم تغيير تاريخ Git أو إزالة shallow history.
- لم يتم عمل commit أو merge أو rebase أو force push.
- لم يتم نقل الكود إلى private remote.
- لم يتم تنفيذ أي scan أو script أو skill ضمن التأسيس.
- لم يتم اعتماد سياسة migration نهائية.

## 5. Blocker / Decision مؤجل

الـ clone كان shallow/grafted. تم تعليق أول Push إلى المستودع الخاص لحين اتخاذ قرار صريح بشأن الاحتفاظ بالتاريخ المتاح أو جلب تاريخ أوسع بطريقة آمنة قبل أول Push.

هذا ليس blocker لتدقيق المستودع أو تصميم architecture. لكنه blocker قبل اعتبار private repo نسخة تطوير منشورة أو قبل أول عملية نقل تاريخية.

## 6. Exit assessment

**STATUS: DONE / CLOSED**

Phase 0 حققت هدفها: بيئة تطوير منفصلة، upstream محفوظ، private destination موجود، وطبقة حماية تمنع Push غير المقصود إلى المصدر العام. لا يوجد ادعاء بأن المستودع الخاص أصبح نسخة كاملة أو أن الكود تم نشره.

## 7. ما يجب على الشات الجديد تذكره

- `~/cbh-dev` هو repo التطوير المقصود.
- `~/tools/Claude-BugHunter` هو checkout المرجعي الأصلي.
- لا تستخدم `git push` دون فحص remotes الحالية.
- لا تفترض أن `bugMO77/cbh` يحتوي على الكود؛ آخر حالة مؤكدة وقت الإنشاء أنه كان فارغًا.
- لا تعالج shallow history تلقائيًا؛ ينتظر قرار المالك.


---

# Phase 1 — Repository & Architecture Audit

**الحالة:** DONE / CLOSED  
**الهدف:** فهم المستودع الحالي على مستوى البنية، والـ components، والـ data/runtime flow، والـ dependencies، والـ security boundaries، والاختبارات والتوثيق قبل اتخاذ أي قرار معماري.

## 1. نوع التدقيق ونطاقه

تم إجراء تدقيق واسع Read-only على `~/cbh-dev`. التقرير النهائي الموصوف في السجل احتوى على 18 قسمًا تشمل:

1. Repository identity وGit state.
2. File inventory.
3. CLI architecture.
4. Engagement Engine.
5. Agent execution.
6. Scope handling.
7. Recon and external-tool integrations.
8. Skill routing.
9. State management.
10. Memory and OSINT.
11. Skills corpus structure.
12. Slash Commands.
13. Documentation accuracy.
14. CI workflows.
15. Evaluation/test system.
16. OpenCode/MCP integration surface.
17. Discrepancy register.
18. Audit limitations and next steps.

التدقيق كان في الأساس Static/code/documentation inspection. السجل الأولي ذكر بوضوح أن هذه المرحلة لم تكن تشغيلًا شاملًا للاختبارات أو الـ Engine أو CLI أو Scanner. بعض Smoke tests المحدودة حدثت لاحقًا وتم توثيقها بشكل منفصل في Master handoff.

## 2. Repository inventory at audit baseline

| العنصر | العدد / القيمة |
|---|---:|
| Physical files observed | 310 |
| Tracked / in-scope files | 298 |
| Ignored `.pyc` cache files | 12 |
| `SKILL.md` files | 83 |
| `hunt-*` Skills | 58 |
| Slash Commands | 15 |
| GitHub workflow files | 7 |
| HEAD | `9269278fec34d7d75bdf682a3d9b26c98339d648` |

كانت هناك 5 `__pycache__` directories تحتوي على 12 ملفات `.pyc` غير tracked. تم استبعادها من product inventory.

### 2.1 Identifier denylist discrepancy

تم حسم discrepancy خاصة بـ `scripts/.identifier-denylist.sha256`:

- الملف موجود.
- tracked وليس ignored.
- الحجم المسجل 1364 bytes و23 سطرًا.
- يحتوي 7 entries فعلية غير التعليقات.
- تم حساب digest وتسجيله في audit evidence.
- لم يتم طباعة محتوى القائمة، ولم يتم تشغيل scanner.

وجود الملف وفحصه لا يعني أن scanner نفسه تم تشغيله أو اختبار فعاليته في هذه المرحلة.

## 3. Component audit

### 3.1 CLI (`cbh/cli.py`)

CLI واجهة deterministic قابلة للتثبيت عبر Python package، ولا تحتاج LLM كي تنفذ وظائفها الأساسية. من الوظائف المسجلة:

- `recon`
- `surface`
- `classify`
- `triage`
- `report`
- `nearby`

الـ CLI يقرأ generated `cbh/data/skill_index.json` وبعض report-library references. تصميمه بسيط وقابل للتوزيع، لكن ظهر تداخل في المسؤوليات مع `engine/engine.py` خصوصًا Recon وSurface mapping.

### 3.2 Engagement Engine (`engine/`)

الـ Engine ينظم Engagement متعدد المراحل ويضم modules مثل:

- `engine.py`: orchestration.
- `recon.py`: recon and external tooling.
- `scope.py`: scope validation.
- `skill_map.py`: routing from surface/class to Skills.
- `state.py`: per-engagement state.
- `memory.py`: cross-target findings/negative memory.
- `osint.py`: OSINT expansion.
- `agent.py`: Agent adapter.

التصميم يقدم قيمة عالية لأنه ينقل النظام من مجرد محتوى Skills إلى workflow متسلسل. لكنه يحتوي احتكاكات integration وprovider coupling ويكرر أجزاء من CLI.

### 3.3 Agent adapter

الملاحظة المحورية: `engine/agent.py` يستدعي `claude -p` عبر subprocess، ويستخرج JSON من الرد. هذا يجعل agent adapter مرتبطًا ببيئة Claude CLI وليس واجهة مستقلة عن الـ provider.

أهم إعدادات التنفيذ التي ظهرت في الفحص:

- `--mcp-config`
- `--strict-mcp-config`
- `--permission-mode bypassPermissions`
- model default داخل الكود.
- `skills_on=False` افتراضيًا.

وجود `bypassPermissions` لا يجب التعامل معه كإعداد آمن تلقائيًا. يلزم تصميم Permission/Sandbox layer حقيقية مرتبطة بـ Scope وTool dispatch. كما أن تعطيل Skills يؤثر في claims الخاصة بقدرات الـ Engine.

### 3.4 Scope handling

`engine/scope.py` يحتوي منطق default-deny وdeny-wins للـ Engine host. وتدعم بعض Skills هذا الاتجاه مثل `recon-scope-triage` و`hunt-subdomain` و`triage-validation`.

لكن `cbh/cli.py` لا يطبق نفس scope enforcement بشكل متكامل. هذا يخلق اختلافًا بين مساري تشغيل مختلفين داخل المشروع. أيضًا، Scope validator ليس Network sandbox؛ وجود validation code لا يعني أن كل subprocess أو HTTP request ممنوع من الخروج خارج النطاق.

### 3.5 Skill routing vs loading

- `engine/skill_map.py` يربط 57/58 من `hunt-*` classes/technologies إلى Skills.
- `hunt-dispatch` يعالج عبر command path وليس mapper التقليدي.
- 25 non-hunt Skills غير موجودة في mapper.
- الـ host harnesses تثبت Skills ضمن مجلداتها ويمكنها auto-activate حسب السياق.
- Engine Agent default عنده `skills_on=False`، وبالتالي يمرر أسماء Skills/Starter probes لكنه لا يحمل نصوصها تلقائيًا.

الاستنتاج: وجود Skill في المستودع لا يثبت أنها تُستخدم في Engine. كما أن host-level discovery مختلف عن engine-level loading.

### 3.6 State, Memory, Evidence

تم العثور على فصل وظيفي بين:

- `state.json` وملفات engagement: سياق الهدف الحالي، وما تم اختباره وما تبقى.
- `engine/memory.py`: سجل findings والـ negative knowledge عبر الأهداف.
- Evidence files/logs: تخزين الطلبات والردود والنتائج التي تدعم validation.

هذا الفصل مفيد ويجب أن يظل واضحًا في التصميم المستهدف بدل دمج كل شيء في ملف ذاكرة واحد.

### 3.7 Recon and external tools

التكاملات تتضمن أدوات ومصادر مثل:

- `gau`
- `katana`
- `curl`
- `subfinder`
- `assetfinder`
- `crt.sh`

بعض الوظائف deterministic وبعضها يعتمد على أدوات أو خدمات خارجية. CLI أبسط وأكثر استقلالية من Engine، بينما Engine يوفر orchestration وstate.

### 3.8 Slash Commands

عددها 15. تشمل أوامر مثل:

`hunt`, `recon`, `scope`, `surface`, `triage`, `validate`, `report`, `chain`, `intel`, `remember`, `memory-gc`, `pickup`, `token-scan`, `autopilot`, `web3-audit`.

تعمل كطبقة UX/orchestration فوق Skills وEngine في بعض المسارات. يجب لاحقًا التحقق من أن أوامرها تتفق مع contracts runtime وليس مجرد prose instructions.

### 3.9 Scripts and installers

تم فحص مجموعة scripts تشمل install/setup، target scaffolding، catalog/index generation، scan identifiers، linting، CVE index refresh وغيرها.

أهم الملاحظات:

- `scan_identifiers.py` مع `.identifier-denylist.sha256` يشكل Leak guard مهمًا.
- `lint_skills.py` هو Skill quality gate، لكن بعض القيود warnings وليست hard failures.
- `gen_skill_index.py` يولد index يستهلكه CLI.
- `gen_skill_catalog.py` يولد توثيق Skills.
- `scripts/cbh.py` لاحقًا تم تقييمه كـ thin shim redundant نسبيًا بعد وجود console entrypoint في `pyproject.toml`، مع الاحتفاظ به مؤقتًا للتوافق.

### 3.10 Testing & Evaluation

المشروع يحتوي على Eval assets تشمل:

- Juice Shop oracle.
- PortSwigger lab runners.
- False-positive eval harness.
- `test_harness.py` لsanity checks بدون شبكة.

يوجد تنبيه بخصوص Juice Shop ceiling effect؛ أي أن درجات التقييم لا يجب تفسيرها بمعزل عن صعوبة الـ benchmark. كما أن full Agent evals تحتاج Docker + Burp + Claude CLI، وبالتالي لا تعمل بنفس الطريقة داخل network-free CI.

## 4. أهم findings المعمارية

### F1 — CLI vs Engine overlap

نفس المفاهيم (Recon/Surface) موجودة في مسارين. إما نحدد حدودًا صارمة: CLI = local deterministic utilities، Engine = orchestration؛ أو نتخذ قرار convergence/deprecation بعد مقارنة الواجهات والاستخدام. لم يُحسم القرار بعد.

### F2 — Agent provider coupling

الـ Agent ليس provider-agnostic؛ هو wrapper حول Claude CLI. هذا يحد من قابلية استخدام providers/harnesses أخرى، ويجعل الاختبارات مرتبطة ببيئة تنفيذ معينة.

### F3 — Skills loading is context-dependent

Engine default يشغل `skills_on=False`. وجود mapper ليس دليلًا على تحميل Skill body، ووجود Skills في host directory لا يعني أن subprocess agent يراها.

### F4 — Scope enforcement inconsistency

Engine عنده scope module واضح؛ CLI ليس لديه نفس enforcement. وهذا يخلق احتمال أن بعض العمليات تحدث قبل تطبيق gate موحد.

### F5 — Runtime verification gap

Static evidence وحده لا يثبت end-to-end live operation. يلزم اختبار invocation path الحقيقي، وMCP، وfailure behavior، والـ scope-denial behavior.

### F6 — Documentation drift

تم توثيق فروقات بين بعض claims في Docs والتنفيذ، مثل:

- `docs/architecture.md` يذكر claim قديمًا بأن automated exploitation tooling غير موجود، بينما Engine/skills لديها workflows اختبار فعلية.
- `docs/_config.yml` به وصف قديم `51+ skills` رغم أن العدد الحالي 83.
- بعض Skill references قديمة مثل `hunt-cache-poisoning` و`hunt-subdomain-takeover`.
- `engine/README.md` يحتوي claims عن OSINT/behavior تحتاج reconciliation مع `--expand` وimplementation.
- `CHANGELOG.md` و`new_skill.yml` وبعض Docs لديها أرقام Skills أقدم مثل 82 أو 51.

### F7 — Safety risk in content does not align with uniform policy

المشروع يملك بعض أقوى safety gates في corpus، لكن توزيعها غير موحد. Phase 2 فحص هذا بشكل أعمق.

## 5. CI / Research / Documentation observations

- توجد workflows للـ skill lint، leak guard، doc count، eval harness sanity، installer smoke، research tools، star history.
- Leak guard عنده permissions مقيدة ومربوط بـ pre-commit وCI حسب الفحص.
- Research pipeline يجمع/يصنف تقارير عامة ويولد pattern libraries في `docs/disclosed-reports/`.
- Docs تشمل architecture، CLI، multi-harness، recon manifest، verification labs، disclosed reports، specifications وغيرها.
- بعض التوثيق صحيح وظيفيًا، وبعضه stale أو لا يطابق مسارات التنفيذ الحالية.

## 6. Limitations of Phase 1

لازم نكون دقيقين:

- التدقيق كان read-only/static في المقام الأول.
- لم يتم في هذه المرحلة تشغيل كل الاختبارات أو Engine/CLI/scanner end-to-end.
- 12 Skill فقط حصلت على deep reading في مرحلة Phase 1 الأولى؛ Phase 2 عالج هذه الفجوة لاحقًا بقراءة 83/83.
- نصوص disclosed-report bodies ومعظم verification labs لم تكن قد قرئت كلها.
- `engine/burp-mcp.json` غير موجود كملف tracked، الموجود `.example` فقط؛ وجوده الفعلي في deployment لم يثبت في audit.
- مدى auto-loading للـ skills في headless `claude -p` مع `--disable-slash-commands` لم يثبت في Phase 1.
- scanner لم يُشغّل عند حسم denylist discrepancy.

## 7. Supplementary smoke evidence added later

بعد التدقيق الأساسي، تم إجراء تجربة Mock للـ Engine كما هو موثق في Master Handoff. هذه تجربة إضافية لا تغير توصيف Phase 1 كـ static audit، ولا تعني أن كل فجوات التشغيل أُغلقت.

## 8. Phase 1 outcome

**STATUS: DONE / CLOSED**

Phase 1 نجحت في بناء خريطة architecture أولية وتحديد أهم نقاط القرار. المخرجات الأساسية ليست قائمة bugs فقط؛ هي صورة عن أماكن المسؤوليات والحدود التي تحتاج إلى توحيد.

**أهم قرار مؤجل إلى Phase 4:** تحديد العلاقة النهائية بين CLI وEngine، ثم ربط ذلك بعقد Skill loading وAgent adapter وScope enforcement وEvidence validation.


---

# Phase 2 — Skills Deep Audit

**الحالة:** DONE / CLOSED  
**النطاق:** 83 `SKILL.md` + 22 supporting files  
**الهدف:** تحويل Skills من مجرد corpus كبير إلى inventory موثق: محتوى، استخدام، تكامل، جودة، تكرار، مخاطر تشغيلية، وقراءة مثبتة من أول الملف إلى آخره.

## 1. لماذا احتجنا Phase 2؟

Phase 1 أعطت قراءة معمارية عامة، لكنها لم تكن deep content audit لكل Skill. لأن الـ Skills تمثل جزءًا كبيرًا من قيمة المنتج الفعلية، كان لازم نفحص كل ملف ونفهم:

- ما الذي يعلمّه Skill فعلًا؟
- ما الـ vulnerability classes أو التقنيات التي يغطيها؟
- هل عنده owner boundary واضح أم يتداخل مع Skills أخرى؟
- ما الأدوات التي يفترض وجودها؟
- هل خطواته قابلة للتنفيذ أم مجرد وصف عام؟
- هل فيه false-positive gates وevidence requirements؟
- هل توجد تعليمات destructive أو unbounded؟
- هل descriptions/frontmatter تساعد على routing صحيح عبر harnesses؟
- هل references والمسارات التي يذكرها موجودة؟

## 2. نطاق التغطية النهائي

| النوع | العدد | حالة الفحص |
|---|---:|---|
| Skill directories | 83 | Inventory كامل |
| `SKILL.md` | 83 | FULL_VERBATIM_READ 83/83 |
| Supporting files | 22 | 21 full read + 1 binary metadata inspection |
| Total unique paths | 105 | متسق بعد reconciliation |
| Total `SKILL.md` payload size | 1,678,896 bytes | حسب baseline الفحص |
| `hunt-*` Skills | 58 | جزء من الـ 83 |
| Non-hunt Skills | 25 | Recon/OSINT/Reporting/Cloud/Identity/Mobile/Web3 وغيرها |

تم توثيق القراءة عبر coverage ledger وbatch reports مع full read ranges وإثبات آخر line/EOF. الـ supporting file الوحيد الذي لم يُقرأ كنص هو `archivo-black.woff2`، وتم فحص metadata الخاصة به فقط لأنه Binary font asset.

### 2.1 Reconciliation detail

حدث confusion مؤقت في العد بسبب grep token counts التي جمعت بيانات الجداول والجمل التوضيحية، فظهر الرقم 106 بدل العدد المتوقع. تم حل ذلك بعمل exact-path reconciliation:

- 83 Skill paths فريدة، كلها `FULL_VERBATIM_READ`.
- 22 supporting paths فريدة: 21 `FULL_VERBATIM_READ` + WOFF2 واحد `BINARY_METADATA_INSPECTED`.
- المجموع 105 unique paths.
- batch reports union يطابق الـ 83 Skill paths بالضبط: لا gaps ولا duplicate assignments.
- الـ capability matrix: 83 rows، 13 columns، 0 malformed rows.

تم توثيق batch mapping في `SKILLS_AUDIT_COVERAGE.md` وbatch reports `batch01` إلى `batch11`، إضافة إلى `batch02-original.md` للـ 11 Skills القديمة التي كانت قراءتها موجودة في جلسة سابقة لكنها لم تكن ممثلة في تقرير batch مستقل.

## 3. منهجية الفحص

- Inventory لكل Skill directory وملفاتها الداعمة.
- قراءة كاملة لكل `SKILL.md` وتأكيد EOF.
- استخراج frontmatter، descriptions، headings، line counts، code fences، tool references، Skill cross-references، scope/evidence/rate keywords.
- فحص التكرار والتقاطع بين Skills.
- فصل Quality findings عن Safety findings.
- إعطاء confidence level: H مباشر، M استنتاج من عدة دلائل، L يحتاج Runtime verification.
- عدم تنفيذ أوامر Skills على أهداف حقيقية أثناء التدقيق.
- إصلاح coverage ledger والتأكد أن عدد الملفات والتقارير متطابق.

## 4. Corpus-level observations

### 4.1 بنية corpus

- 58 `hunt-*` skills تصنف ثغرات/تقنيات.
- 25 non-hunt skills تغطي workflow ومجالات أخرى مثل Recon وOSINT وMethodology وReporting وMobile وCloud/Identity وWeb3 وSupply Chain.
- أغلب `hunt-*` تتبع skeleton متشابهًا: Crown Jewel Targets → Attack Surface Signals → Step-by-Step Hunting Methodology → Payload & Detection Patterns → Common Root Causes / Bypass Techniques → Validation / Severity.
- أربعة non-hunt Skills كبيرة جدًا وتتحول إلى monoliths: `osint-methodology` (1704 lines)، `bug-bounty` (1604)، `bb-local-toolkit` (1558)، `security-arsenal` (912).
- 15 من 22 supporting files تابعة لـ `offensive-osint` وتستخدم progressive disclosure عبر `references/`; أغلب Skills الأخرى ملف واحد.

### 4.2 Frontmatter and descriptions

- 13 Skills لا تحتوي `report_count:`.
- 3 Descriptions تجاوزت حد 1024 characters الموثق في `docs/multi-harness.md`: `bb-local-toolkit`, `bug-bounty`, `osint-methodology`.
- هذه الثلاثة لها grandfather exceptions في `scripts/lint_skills.py`، لذلك الحد المعلن ليس hard fail فعليًا.
- 11 Skills تجاوزت 500 body lines guideline، لكن اللينتر يعرضها Warning وليس CI failure.
- بعض Skills القديمة لها descriptions عامة مولدة مثل “Hunting skill for X”، وهذا يضعف auto-routing.
- بعض Skills الحديثة تصف boundaries مع Skills الأخرى وتوضح false-positive gates، وهذا pattern يستحق الحفاظ عليه.

### 4.3 NUL byte defect

`skills/hunt-auth-bypass/SKILL.md` يحتوي raw NUL byte واحدة عند byte offset 23277، في جملة كان المقصود فيها كتابة `\x00` كنص. الأثر:

- `file` يتعرف على الملف كـ `data`.
- grep يتعامل معه كملف binary.
- بعض أدوات القراءة والبحث تتوقف أو تتخطاه.
- الملف mapped داخل `engine/skill_map.py` ومشار إليه من 18 Skill أخرى.

تم فحص آخر جزء من الملف عبر byte-level read بسبب رفض read tool للنص binary، ووُثق هذا على أنه defect Q1/S1.

## 5. Quality findings Q1–Q12

| ID | finding | الأثر الأساسي |
|---|---|---|
| Q1 | Raw NUL byte داخل `hunt-auth-bypass` | أدوات grep/diff/scanners قد تتخطى الملف أو تقرأه كـ binary. |
| Q2 | Stale Skill references مثل `hunt-cache-poisoning` و`hunt-subdomain-takeover` | Links/ownership references لا تطابق الأسماء الحالية. |
| Q3 | تعارض بين القول إن OTP brute force غير عملي وبين أمر 1,000,000 request في `hunt-mfa-bypass` | Methodology متناقضة وقد تسبب rate/lockout impact. |
| Q4 | `hunt-html-injection` يستخدم XSS proof رغم نفي أن XSS هو المقصود | Category boundary غير واضحة. |
| Q5 | Copy-paste syntax defect في `hunt-source-leak` عند `. replace(` | مثال أو recipe قد يفشل عند نسخه. |
| Q6 | Descriptions عامة/قالبية في hub Skills مثل `hunt-rce`, `hunt-misc`, `hunt-idor`, `hunt-oauth` | Routing quality أضعف من Skills ذات boundaries دقيقة. |
| Q7 | `reports/NNN` notation تشير إلى مسار غير موجود | غموض بين HackerOne IDs ومسارات repository. |
| Q8 | تجاوز 11 Skill لحد 500 lines | صعوبة صيانة وcontext efficiency، والـ linter لا يمنع ذلك. |
| Q9 | ثلاثة Descriptions grandfathered فوق 1024 chars | تعارض بين التوثيق والـ enforcement. |
| Q10 | `redteam-report-template` يشير إلى `templates/reference.docx` غير موجود داخل Skill tree | asset مفقود أو packaging path غير مكتمل. |
| Q11 | `offensive-osint/README.md` قديم مقابل SKILL v3.0 | إصدار ووصف وروابط لا تتوافق. |
| Q12 | README/font assets غير مرتبطة بوضوح بنقطة دخول Skill | orphaned assets / uncertain packaging. |

تمت إضافة Q13 في reconciliation اللاحق لموضوع changelog/version mismatch. يجب قراءة Q13 من النسخة الأصلية الكاملة `SKILLS_DEEP_FINDINGS.md` إذا احتجنا صياغتها الحرفية؛ لا نخترع لها وصفًا تفصيليًا هنا.

### 5.1 Overlap clusters

أبرز مجموعات التداخل:

- `bug-bounty` / `bb-local-toolkit` / `bb-methodology`: overlap واضح، description Jaccard 0.70 لبعض المقارنات، وجداول ASI09 وأدوات متكررة.
- `osint-methodology` و`offensive-osint`: الأول planning/methodology والثاني arsenal/reference index، مع وجود overlap في بعض المحتوى.
- Authentication/ATO: `hunt-ato`, `hunt-forgot-password`, `hunt-mfa-bypass`, `hunt-jwt-crypto`, `hunt-session`, `hunt-oauth`, `hunt-saml`, `hunt-auth-bypass`, `okta-attack`, `m365-entra-attack`.
- HTML Injection/XSS.
- Shadow API/API misconfiguration/Subdomain.
- JWT/AUTH bypass/ATO.
- SPA API/source leak/shadow API.

وجود overlap لا يعني أن الحل merge تلقائيًا. المطلوب هو تحديد ownership وinterfaces، وربما إبقاء Skills متعددة مع delegation واضح بدل دمجها كلها.

## 6. Safety findings S1–S10

الهدف ليس منع Active Testing عمومًا؛ الهدف هو تحديد الأوامر التي يمكن أن تسبب أذى خارج حدود الهدف أو تتجاوز proof necessity أو لا تحدد rate/blast radius.

| ID | finding | الخطر العملي |
|---|---|---|
| S1 | 33/83 Skills لا تحتوي scope/authorization keyword | لا يثبت سوء النية، لكنه يعني أن Standalone Skill قد لا تذكر حدود التفويض بوضوح. |
| S2 | Redis `flushall` و`CONFIG SET` webshell instructions في `hunt-nosqli` | حذف بيانات أو persistence على Redis حقيقي. |
| S3 | Admin delete كدليل JWT في `hunt-jwt-crypto` | تغيير destructive في حساب/خدمة production. |
| S4 | `/actuator/shutdown` يظهر كـ finding في `hunt-springboot` | تعطيل توفر الخدمة. |
| S5 | Firebase PUT write test وbucket-name brute force في `hunt-cloud-misconfig` | تعديل بيانات طرف ثالث أو probing غير محدود. |
| S6 | مليون OTP requests في `hunt-mfa-bypass` | Lockout/load/collateral damage. |
| S7 | تنزيل exploit code دون checksum/provenance pinning في `hunt-deserialization` | Supply-chain compromise على جهاز الباحث. |
| S8 | HTTP smuggling ضد shared CDN/proxy دون blast-radius controls | التأثير على tenants أو مستخدمين آخرين. |
| S9 | Safety gates جيدة موجودة لكن غير موحدة | دليل أن gating ممكن، لكن تطبيقه inconsistent. |
| S10 | CLI لا يطبق نفس Scope enforcement الموجود في Engine | قد تحدث عمليات قبل gate متسق. |

### 6.1 تفسير S1 بدقة

غياب كلمة `scope` أو `authorization` لا يثبت أن Skill خطيرة. بعض الملفات قد تحتوي توجيهات أمان بصياغة أخرى أو تعتمد على engagement-level policy. الخطر هنا هو تشغيل Skill standalone دون تذكير بحد التفويض، خاصة عندما تحتوي نفس Skill أوامر destructive. لذلك تم وصف finding على أنها condition-specific وليست اتهامًا عامًا للـ corpus.

## 7. Runtime / Integration conclusions

### 7.1 Routing coverage

- 57/58 hunt Skills mapped في `engine/skill_map.py`.
- `hunt-dispatch` يتم التعامل معها من Commands.
- 0/25 non-hunt Skills في mapper.
- Host harness distribution/load mechanism منفصل عن Engine mapping.
- `skills_on=False` default يعني أن Engine لا يحمل body تلقائيًا.

### 7.2 Browser capability gap

بعض Skills تحتاج browser proof مثل clickjacking وCORS وDOM XSS. الـ `ALLOWED_TOOLS` في agent adapter لم يظهر فيه browser tool. وجود Skill procedure لا يعني وجود execution path يدعم كل متطلباتها.

### 7.3 Unresolved runtime questions

التدقيق سجل أسئلة لا يجوز تحويلها إلى حقائق:

1. هل Claude auto-loads named Skills في headless `claude -p` مع `--disable-slash-commands`؟ لم يثبت.
2. هل `engine/burp-mcp.json` موجود في deployed installs؟ tracked `.example` فقط؛ وجود الملف الحقيقي لم يثبت.
3. هل `reports/NNN` IDs أم repository paths؟ غير محسوم.
4. هل 15 `offensive-osint` references متوافقة بالكامل مع index v3.0؟ لم يتم التحقق سطرًا بسطر من كل ملف.
5. هل truncation للـ 3 long descriptions في Codex installer يعمل كما هو موثق؟ لم يتم تشغيله.
6. هل NUL byte يؤثر على كل harness loaders أم فقط tooling معينة؟ غير محسوم.
7. هل subagent scope inheritance المذكور في `hunt-dispatch` enforced by code؟ لم يثبت.
8. هل هناك Engine execution path للـ browser-required Skills؟ غير مثبت.

## 8. Deliverables الأصلية

المخرجات المسجلة تحت:

```text
/tmp/opencode/cbh-audit/skills-deep/
```

وتشمل:

- `SKILLS_INVENTORY.md`
- `SKILLS_CAPABILITY_MATRIX.md`
- `SKILLS_DEEP_FINDINGS.md`
- `SKILLS_AUDIT_COVERAGE.md`
- `batches/batch01.md` … `batches/batch11.md`
- `batches/batch02-original.md`
- `remaining_manifest.json`

الـ coverage ledger reconciled ويشير إلى 83 Skill full read و22 supporting resources.

## 9. Phase 2 outcome

**STATUS: DONE / CLOSED**

أهم قيمة للمرحلة أنها نقلت Skills layer من افتراض أنها corpus جيدة إلى معرفة دقيقة بمحتواها وحدودها. لكنها لم تصلح الـ Skills أو تنفذ تعديلات. findings ما زالت inputs للتصميم والتنفيذ، وليست إذنًا بتشغيل payloads أو إجراء تغييرات.


---

# Phase 3 — Project-Wide Value Assessment

**الحالة:** DONE كعملية تقييم أولية  
**التاريخ المسجل:** 2026-11-03  
**Repository baseline:** `9269278fec34d7d75bdf682a3d9b26c98339d648`  
**Workspace:** `/tmp/opencode/cbh-audit/project-value-assessment/`

## 1. قرار توسيع نطاق المرحلة

كان المقترح الأول أن نعمل Skills Value Assessment منفصلًا. تم تعديل ذلك قبل التنفيذ: بدل تقييم Skills وحدها ثم اكتشاف أن Engine/CLI/Agent تحتاج قرارات منفصلة، تم توسيع Phase 3 إلى **Project-Wide Value Assessment** لكل المكونات الأصلية ذات الصلة.

سبب هذا القرار هو أن الـ Blueprint لا يجب أن يُبنى على انطباعات عن Skills فقط، بل على معرفة المشروع بالكامل ووظائفه واعتمادياته ومخاطر تغييره.

## 2. ما الذي تم تقييمه؟

النطاق شمل:

- Skills وreferences وsupporting resources.
- Slash Commands.
- CLI ومكوناته.
- Engagement Engine.
- Agent execution/provider integration.
- Runtime state/memory/evidence/logging.
- Recon and tool integrations.
- Scripts/installers/utilities.
- Configuration/manifests/examples.
- Testing/evaluation/labs.
- CI/CD workflows.
- Documentation/README/guides/changelog.
- Assets/templates/data/resources المساعدة.

تم استبعاد `.git/` وcaches وdependencies المنزّلة وgenerated artifacts من تقييم المنتج، مع تقييم lockfiles/manifests/binary assets حسب دورها.

## 3. منهجية إعادة استخدام الأدلة

القاعدة الأساسية التي اعتمدناها:

> **Never Repeat Verified Work. Reuse Evidence, Investigate Gaps, and Focus on Decisions.**

تم تقسيم الملفات إلى ثلاث مجموعات:

| المجموعة | طريقة التعامل |
|---|---|
| Previously Audited | إعادة استخدام audit evidence السابق مباشرة. |
| Partially Audited | فحص targeted للجزء الناقص فقط. |
| Not Audited | تقييم لأول مرة. |

قبل التقييم تم إجراء Audit Evidence Reconciliation لمطابقة الملفات الحالية مع التقارير السابقة. لأي ملف سبق تدقيقه، تم تسجيل ما إذا كانت الأدلة كافية، والـ findings السابقة، وحالة Git، والمعلومة الناقصة، وهل يحتاج reuse أو targeted inspection أو full re-audit.

لم تتم إعادة قراءة الـ 83 Skill. تم استعادة 92 persisted read payloads من OpenCode session store، منها 38 payload لملفات غير Skills من Phase 1. وتم إجراء targeted inspection لـ 33 ملفًا فقط حين كانت هناك معلومة ناقصة تؤثر على disposition.

## 4. حجم التقييم ومكونات المستودع

تم تقييم 298 project-owned files عبر 17 فئة رئيسية:

| الفئة | الملفات | الفئة | الملفات |
|---|---:|---|---:|
| Skills (`SKILL.md`) | 83 | Docs | 10 |
| Skills supporting | 22 | Docs assets | 3 |
| Commands | 15 | Disclosed reports | 37 |
| CLI | 3 | Verification docs/assets | 25 |
| Engine | 12 | Docs ops | 1 |
| Scripts | 17 | Docs specs | 2 |
| Eval | 16 | CI workflows | 7 |
| Research | 9 | CI meta | 8 |
| Assets | 12 | Plugin manifests | 2 |
| Git hooks | 1 | Root files | 13 |

**ملاحظة reconciliation:** النص الوصفي في التقرير يقول **17 فئة رئيسية**، بينما جدول التصنيف المعروض يحتوي على **20 تسمية فئة** (10 أزواج في الجدول). لا أتعامل مع هذا الاختلاف على أنه محسوم. يجب الرجوع إلى `PROJECT_FILE_INVENTORY.csv` الأصلي لتحديد عدد الفئات المقصود، قبل استخدام هذا الرقم في أي تصميم أو تحليل إحصائي. إجمالي الملفات المصنفة المعلن يظل 298.

العدد 298 يمثل in-scope project-owned files وفق طريقة inventory، وليس عدد كل physical paths بما فيها caches و`.git`.

## 5. كيف تم تقييم كل ملف؟

المعايير المتفق عليها تضمنت:

1. Purpose & Necessity.
2. Mission Value.
3. Functionality.
4. Integration.
5. Dependencies.
6. Uniqueness.
7. Technical Quality.
8. Security & Safety.
9. Maintainability.
10. Testing.

تم الفصل بين قيمة الملف في المنتج وقيمته المباشرة في hunting. على سبيل المثال، `engine/scope.py` قد لا يصطاد ثغرة مباشرة، لكنه قد يكون أساسيًا لسلامة المنتج.

## 6. Disposition counts

| القرار | العدد | التفسير |
|---|---:|---|
| KEEP AS-IS | 267 | الاحتفاظ كما هو في التقييم الأولي. |
| MODIFY | 18 | ملفات فيها مبررات تعديل محدد. |
| OPTIONAL | 12 | إضافات أو مكونات غير أساسية يمكن إبقاؤها اختيارية. |
| DEPRECATE | 1 | `scripts/cbh.py` thin shim؛ يُحتفظ به مؤقتًا للتوافق قبل وقف الاعتماد. |
| REFACTOR | 0 | لم يُعتمد قرار نهائي. |
| MERGE | 0 | التداخلات سُجلت كمرشحين ولم يتم اعتماد دمج. |
| REPLACE | 0 | لا قرار استبدال. |
| CREATE NEW | 0 | بناء المكونات الناقصة مؤجل إلى Phase 4. |
| SPLIT | 0 | لا تقسيم معتمد. |
| MOVE | 0 | لا نقل معتمد. |
| REMOVE | 0 | لا حذف معتمد. |

المجموع: 298 ملفًا. هذه تصنيفات تقييمية أولية، لا تغييرات تم تنفيذها. وعبارة KEEP AS-IS لا تعني أن الملف مثالي؛ تعني أن التقييم لم يحدد في تلك المرحلة سببًا كافيًا لتغيير محدد ضمن النطاق الحالي.

### 6.1 Files recommended for MODIFY

الـ 18 ملفًا/مكونًا المشار إليها في التقرير:

**Safety gating cluster (6 Skills):**

- `hunt-nosqli`
- `hunt-deserialization`
- `hunt-springboot`
- `hunt-laravel`
- `hunt-mfa-bypass`
- `hunt-jwt-crypto`

**Defect cluster (5 Skills):**

- `hunt-auth-bypass` (NUL byte)
- `hunt-saml`
- `hunt-html-injection`
- `hunt-source-leak`
- `hunt-ssti`

**Core/docs:**

- `engine/engine.py`
- `engine/agent.py`
- `engine/README.md`
- `docs/architecture.md`
- `docs/_config.yml`
- `USAGE.md`
- `ENGAGEMENTS.md`

### 6.2 OPTIONAL examples

التقرير جمع أمثلة مثل:

- `autopilot`
- `web3-audit`
- `install-community-skills` (sh/ps1)
- `refresh-cve-index.py`
- `gen_star_history.py`
- `setup_harness_mcp.py`
- `docs/automation/cve-refresh.yml.template`
- superpowers specifications
- star-history CI
- `harvest_intigriti`

راجع `PROJECT_DECISION_MATRIX.csv` للحصول على التصنيف الدقيق لكل path بدل الاعتماد على قائمة أمثلة فقط.

## 7. أهم النتائج المعمارية

### 7.1 CLI vs Engine overlap — أعلى قرار أولوية

`cbh/cli.py` و`engine/engine.py` يكرران Recon وSurface mapping. CLI deterministic وstdlib-only وpip-installable، بينما Engine orchestrator لإدارة Engagement مع memory/state/agent dispatch. هذا التداخل يحتاج حسم: فصل المسؤوليات بوضوح، أو convergence، أو deprecation لأحد المسارات. لا يوجد owner decision نهائي بعد.

### 7.2 Agent provider coupling + skills-off default

`agent.py` يستدعي `claude -p` ويستخدم default model/provider مرتبطًا بـ Claude CLI. `skills_on=False` يعني أن أسماء Skills قد تظهر في Prompt دون تحميل bodies. كذلك `burp-mcp.json` غير tracked والـ tracked file الموجود `.example` فقط. هذا يؤثر على تشغيل `--strict-mcp-config` وعلى reproducibility.

### 7.3 Skill discovery/loading split

Engine mapping يغطي 57/58 hunt-*، ولا يشير إلى 25 non-hunt Skills. Host harnesses لديها mechanism مختلف لاكتشاف Skills. يلزم عقد واضح يحدد مصدر الحقيقة وآلية loading لكل harness.

### 7.4 Scope enforcement inconsistency

Engine scope + بعض Skills فيها gates جيدة، لكن `cbh/cli.py` لا يطبق scope gate نفسه. كذلك S1–S10 بيّنت أن safety controls داخل Skills غير موحدة. يجب تصميم layered enforcement: policy + dispatcher gate + actual tool boundary، لا الاكتفاء بكلمات Prompt.

### 7.5 Evidence & validation

يوجد أساس جيد في 7-Question Gate وOOB discipline وfalse-positive evals، لكن full runtime validation غير reproducible في CI بسبب Docker/Burp/Claude requirements. يلزم Offline/Mock harness وproof gate integrated مع actual invocation path.

### 7.6 Documentation drift

توجد أسماء Skills ومسارات وأعداد قديمة، إضافة إلى docs تحتاج شرح engine/CLI split وskills-off behavior. يجب تحديث docs بعد استقرار architecture، لا قبلها بشكل عشوائي.

## 8. Dependency & Impact Map

تم إنشاء مصفوفة فيها 90 dependency rows. من High-impact hubs:

- `engine/skill_map.py`
- `engine/recon.py`
- `cbh/data/skill_index.json`
- `scripts/install.sh`
- `scripts/scan_identifiers.py`
- `skills/` كـ corpus data
- `docs/disclosed-reports/`

لم يتم رصد circular dependencies في الرسم الذي تم تحليله. أمثلة ripple effects:

- تعديل `scripts/gen_skill_index.py` يؤثر على `cbh/data/skill_index.json` ثم `cbh classify`.
- تعديل `engine/engine.py` قد يؤثر على Commands التي تستند إلى Engine semantics.

المصفوفة الكاملة هي المرجع لتقييم impact أي تغيير لاحق.

## 9. Missing capabilities / Build candidates

هذه ليست قرارات بناء نهائية؛ هي candidate gaps ظهرت من التقييم:

1. Engine-agnostic Skill-loading contract.
2. Offline/mock runtime test harness للـ Engine.
3. Scope enforcement داخل CLI.
4. Uniform safety-gate defaults للـ destructive Skills.
5. Local light sandbox لتشغيل/اختبار Skill bodies بشكل محدود.
6. Documentation refresh بعد حسم Architecture.

## 10. أسئلة مفتوحة تحتاج Runtime Verification

1. هل الـ host harness auto-loads named Skills مع `--disable-slash-commands`؟
2. هل `engine/burp-mcp.json` موجود في deployed installs؟
3. هل `reports/NNN` هي HackerOne IDs أم repo paths؟
4. هل Skill bodies تعمل end-to-end في live engagement؟
5. هل `docs/automation/cve-refresh.yml.template` يعمل بعد تفعيله؟

لا يجوز اعتبار الأسئلة هذه محلولة لمجرد وجود code أو documentation.

## 11. Deliverables الأصلية وIntegrity checks

المخرجات المسجلة تحت:

```text
/tmp/opencode/cbh-audit/project-value-assessment/
```

- `PROJECT_FILE_INVENTORY.csv` — 298 rows.
- `PROJECT_VALUE_ASSESSMENT.md` — تقرير التقييم.
- `DEPENDENCY_IMPACT_MATRIX.csv` — 90 rows.
- `PROJECT_DECISION_MATRIX.csv` — 298 rows.

Integrity validation المسجل:

- Inventory paths = Decision matrix paths: 298 = 298.
- Zero missing/extra decisions.
- Zero empty dispositions.
- 83 Skills + 22 supporting files متطابقة بين المخرجات.
- Dependency endpoints ضمن inventory paths.
- Git HEAD بقي كما هو.
- Working tree ظل clean.
- لا repository files modified.
- لا Git operations أو live scans أو network activity في جلسة Phase 3.

## 12. حدود Phase 3

- 298 ملفًا تم inventory وتصنيفها، لكن هذا لا يعني أن كل ملف قرئ بنفس مستوى deep audit. تم reuse للأدلة السابقة وإجراء targeted inspection لـ 33 ملفًا.
- لم يتم اعتماد MERGE/REFACTOR/CREATE NEW رغم وجود مرشحين واضحين؛ تم تأجيلها لPhase 4 وقرار المالك.
- Phase 3 لم تصمم architecture المستهدفة.
- Phase 3 لم تنفذ أي code changes.
- التقييم الحالي سابق لـ Reference Alignment مع Buggy/Ai-Hunting/OffsecCyber؛ لذلك يجب اعتبار dispositions مدخلات أولية قابلة للمراجعة، لا قرارات نهائية.

## 13. الفرق بين Phase 3 وPhase 4 وPhase 5

- Phase 3 تجيب: عندنا إيه؟ كل مكون بيعمل إيه؟ إيه المفيد/المكرر/الضعيف؟ إيه اللي يحتاج تعديل أو بناء؟ وما تأثير كل قرار؟
- Phase 4 تجيب: CBH المستهدف شكله إيه؟ ما هي architecture والـ components والـ interfaces والـ contracts والـ data flows؟ ماذا سنحتفظ/نعدل/ندمج/نبني؟
- Phase 5 تحول الـ Blueprint المعتمد إلى Implementation Planning & Migration Strategy، بترتيب وتبعيات واختبارات ومعايير قبول.

## 14. Phase 3 outcome

**STATUS: DONE — PRELIMINARY ASSESSMENT**

Phase 3 مكتملة من ناحية inventory والـ value assessment ومصفوفة الاعتماديات والقرارات الأولية. لكنها لا تغلق باب إعادة النظر في القرارات المتأثرة بالمراجع الجديدة. الخطوة الصحيحة هي Reference Alignment Review محدود وموجه، وليس إعادة تدقيق 298 ملفًا من الصفر.


---

# Phase 4 — Reference Intake & Alignment Gate (قبل Unified Blueprint)

**الحالة:** NOT STARTED كـ Blueprint  
**الحالة العملية الحالية:** Reference Intake مطلوب قبل Phase 4 formal start  
**قاعدة:** لا نبدأ Blueprint قبل مراجعة المصادر ذات الصلة وتوثيق ما نستفيد منه وما نرفضه.

## 1. لماذا أوقفنا الانتقال المباشر إلى Blueprint؟

بعد Phase 3 أصبح لدينا تقييم للمشروع الحالي، لكن لا نريد أن نصمم CBH اعتمادًا على رأي عام أو على تشابه سطحي مع مشروع آخر. المطلوب أن يكون لدينا:

- Architecture & Runtime principles واضحة.
- Development methodology وdecision-control واضحة.
- أمثلة حقيقية من مشاريع مشابهة، مع فحص implementation وليس tree فقط.
- Dataset evaluation يوضح ما إذا كانت المعرفة قابلة للاستخدام، وما مخاطرها.
- traceability تربط كل تصميم أو قرار بمصدره أو بسبب مستقل.

لذلك تم تأجيل صياغة Unified System Architecture Blueprint لحين بناء Reference Package ومراجعة نتائج Phase 3 في ضوئه.

## 2. مصادر المرجعية الثلاثة

### A. Buggy — Architecture / Runtime / Methodology Reference

Buggy مشروع مستقل سبق العمل على تصميمه. دوره أن يوفّر Contracts وruntime policies وreview discipline وgovernance يمكن مقارنة أفكارها مع CBH.

الملفات التي طلبنا تجهيزها على دفعات:

**Architecture contracts:**

1. `architecture/file-contracts.md` v1.3.
2. `architecture/agent-architecture-rules.md` v1.2.
3. `architecture/validation-model.md` v1.1.
4. `architecture/knowledge-flow.md` v1.1.
5. `architecture/learning-flow.md` v1.1.
6. `architecture/agent-security.md` — النسخة التي يعتبرها المالك authoritative، مع سجل v1.0/v1.1 لحسم الاختلاف.
7. `architecture/model-routing.md` v0.1 مع lock/review.
8. `architecture/review-discipline.md` النص الكامل v0.2، مع lock history لـ v0.1 إذا كان منفصلًا.

**Runtime policies and inventory:**

9. `runtime/tool-manifest.md` v1.5 مع lock/change/review.
10. `runtime/registry.json` v0.7-rev2 مع lock record/schema assumptions/validation.
11. `runtime/redaction.md` v1.2 وسجلات النسخ المجمدة السابقة إذا كانت مهمة لتفسير التغييرات.
12. `runtime/provider-failure-policy.md` v0.1 مع review/lock.
13. `runtime/model-routing.md` v0.5 مع lock/review وسجل الإصدارات السابقة ذات الصلة.

**Implementation and test evidence:**

14. `scripts/runtime_preflight.py` النسخة المقصودة الحالية.
15. `scripts/test_runtime_contract.py` النسخة المقصودة الحالية.
16. Test output/logs للـ 41 tests المشار إليها إن كانت متاحة.
17. GAP register والـ GAP closure evidence، خصوصًا IDs المتعلقة بـ tool trust/invocation/egress/validation.

المجموعات التي ظهرت في المرجع تشمل:

- Definition integrity، trusted reference، invocation choke point، وCLI/MCP/built-in handling (`GAP-TM-11`).
- MCP trust-list ownership/policy (`GAP-AS-03`, `GAP-TM-05`).
- Egress/redirects/URL normalization/binding/follow-up requests (`GAP-TM-18`, `GAP-TM-22` إلى `GAP-TM-26`).
- Independent validation/proof gate (`GAP-VM-01`, `GAP-VM-04`, `GAP-VM-09`).
- Finding/validation/coverage output contracts (`GAP-VM-03`, `GAP-VM-05`, `GAP-VM-06`).

**مهم:** أسماء وإصدارات الملفات أعلاه هي intake list من سجل Buggy، ولا تعني أن الملفات تم استلامها جميعًا أو مراجعتها في هذه الحزمة. نحتاج exact full text + review/lock evidence حيث ينطبق.

### B. Ai-Hunting — External implementation reference

الرابط الذي وفره المالك:

`https://github.com/0xmannaf/Ai-Hunting`

الـ tree snapshot المرسل أظهر مكونات مثل:

- `.agents/skills`
- `.github/workflows`
- `.opencode/commands`
- `learning_engine`
- `memory`
- `references`
- `runtime`
- `scripts`
- `skills`
- `testing`
- `wordlist`
- `writeups`
- `.opencode.json`
- `AGENTS.md`
- `agent-briefing.md`
- `opencode.json`
- `package.json`
- `prioritization.md`
- `prompts.md`

وكان الـ snapshot يعرض initial commit `3c1e9a0`، وذكر أن repository لم يكن لديه README وقت الصورة.

**المعلومة التي لدينا حاليًا:** directory tree snapshot وبيانات commit ظاهرة في الرسالة. هذا لا يكفي للحكم على بنية النظام أو جودة runtime أو فعالية learning engine. لا تدّعِ أن repo كاملًا تم تحليله أو تشغيله.

**المطلوب:** ZIP من repo عند commit محدد أو snapshot نظيف، ومعه commit hash. لا نحتاج history كاملًا في البداية، لكن نحتاج الملفات الفعلية ذات الصلة.

**أجزاء الفحص المقترحة:**

- Skills: structure، frontmatter، invocation، scope/evidence gates، overlap.
- Commands/orchestration: من يستدعي من؟ كيف يتم dispatch؟ ما lifecycle؟
- `learning_engine`: ما الذي يتعلمه؟ من أي data؟ كيف يمنع feedback loops وpoisoning؟
- `memory`: schema، persistence، versioning، target separation، retention، contamination controls.
- `runtime`: tool boundaries، safety، permissions، timeouts، retries، redaction، isolation.
- `testing`: fixtures، evaluations، regression، false positives، deterministic evidence.
- `references` و`writeups`: provenance، citations، licensing، update policy.
- `AGENTS.md`, `agent-briefing.md`, prioritization/prompt/config files: role boundaries, task constraints, model routing and governance.

### C. OffsecCyber — Dataset / Knowledge / Evaluation Reference

الرابط الذي وفره المالك:

`https://huggingface.co/datasets/PentesterFlow/OffsecCyber`

الـ Dataset card snapshot الذي تم فحصه وصف dataset بحجم ظاهر يقارب 92.8 MB، والملفات الأساسية:

- `manifest.json`
- `README.md`
- `LICENSE`
- `train.jsonl`
- `valid.jsonl`
- `test.jsonl`
- `banner.png`

والأرقام التي ظهرت في بطاقة البيانات التي فُحصت وقتها:

- 39,548 total examples.
- 35,423 `qwen_cve_input` rows.
- 4,125 `h1_input` rows.
- Splits: train 35,594 / validation 1,977 / test 1,977.
- 35 classes.
- 13,403 leakage groups.
- 282 exact duplicate rows removed.
- 3,908 records marked `has_future_cve: true`.
- بطاقة البيانات لم تعرض model benchmark results مرفقة.

هذه metadata وصف للبطاقة وقت الفحص، وليست إثباتًا أن dataset مناسبة أو غير مناسبة.

**ملاحظات تحقق أولية:**

- لا نفترض أن dataset عبارة عن full HackerOne archive؛ H1-tagged rows حوالي 4,125 فقط في snapshot المذكور، بينما الغالبية CVE-oriented.
- بعض preview examples تضمنت قيمًا غير متجانسة أو suspicious في حقول مثل `cvss_score` (قيم تشبه سنوات أو 0/1). هذا red flag يحتاج schema validation، وليس دليلًا وحده على فساد dataset كلها.
- وجود `has_future_cve` مهم لمراجعة temporal leakage: هل المثال يستخدم معلومات لم تكن متاحة وقت CVE؟ كيف تم بناء split؟
- 13,403 leakage groups لا تكفي وحدها للحكم على عدم وجود leakage. نحتاج فهم group construction وsplit methodology.
- أي claim بأن Qwen3.5-4B تم تدريبه وحقق نتائج جيدة يحتاج artifacts أو test harness أو benchmark examples، وليس النص الترويجي وحده.

**المطلوب أولًا بدل تنزيل dataset كاملة:**

1. `README.md`.
2. `manifest.json`.
3. `LICENSE`.
4. Samples صغيرة متوازنة من train/valid/test.
5. Data schema/field definitions.
6. Source/provenance notes.
7. أي training harness/configuration مستخدمة.
8. Evaluation results / test prompts / comparison baseline إن وجدت.

بعدها نقرر هل نحتاج dataset كاملة، وما هو دورها الصحيح في CBH: retrieval knowledge، eval set، fine-tuning، أو لا شيء من ذلك.

## 3. CBH current-state package المطلوب للمقارنة

مخرجات Phase 3 الأصلية:

```text
/tmp/opencode/cbh-audit/project-value-assessment/
  PROJECT_FILE_INVENTORY.csv
  PROJECT_VALUE_ASSESSMENT.md
  DEPENDENCY_IMPACT_MATRIX.csv
  PROJECT_DECISION_MATRIX.csv
```

ومخرجات Phase 2:

```text
/tmp/opencode/cbh-audit/skills-deep/
  SKILLS_INVENTORY.md
  SKILLS_CAPABILITY_MATRIX.md
  SKILLS_DEEP_FINDINGS.md
  SKILLS_AUDIT_COVERAGE.md
  batches/
```

نحتاج أيضًا التقرير النهائي لـ Phase 1 / repository architecture audit إذا لم يكن ضمن التسليم السابق. لا نطلب إعادة تدقيقها؛ نطلب الأدلة الأصلية حتى تكون المقارنة traceable.

## 4. Reference Alignment Review — كيف نقارن؟

كل فكرة أو عقد أو implementation pattern من مصدر خارجي يمر عبر سجل منظم:

| الحقل | معناه |
|---|---|
| Source ID | اسم المصدر والنسخة والcommit/date |
| Source evidence | الملف/القسم/السطر أو test الذي يدعم الفكرة |
| Source claim | ماذا يقول المصدر حرفيًا أو يثبته؟ |
| CBH counterpart | المكون أو القرار المقابل في CBH |
| Current CBH evidence | أين يظهر حاليًا؟ وما دليله؟ |
| Gap / conflict | ما الفرق أو التناقض؟ |
| Decision candidate | Adopt / Adapt / Reject / New Design |
| Rationale | لماذا هذا القرار مناسب لـ CBH؟ |
| Dependencies | ماذا يتأثر لو اعتمدناه؟ |
| Verification | ما test/acceptance criteria اللازمة؟ |
| Owner decision | Pending / Approved / Rejected |

### 4.1 تصنيفات القرارات

- **Adopt:** نأخذ التصميم أو القاعدة كما هي لأن سياق CBH متوافق.
- **Adapt:** الفكرة مفيدة لكن تحتاج تعديلًا لبيئة CBH أو متطلباته.
- **Reject:** غير مناسبة أو لا يوجد دليل كافٍ على فائدتها أو تتعارض مع invariant مهم.
- **New Design:** لا يوجد مصدر يقدم حلًا مناسبًا، فنصمم عقدًا جديدًا مسببًا ومختبرًا.

لا يتم تحويل اقتراح إلى قرار نهائي دون Owner approval.

## 5. التمييز بين المصدر والاستنتاج

كل تقرير مقارنة يجب أن يفصل بين:

1. **Source fact:** ما يقوله الملف أو يثبته التنفيذ.
2. **Observed behavior:** ما تم تشغيله ونتيجته.
3. **Reviewer analysis:** تفسيرنا لما يعنيه بالنسبة لـ CBH.
4. **Decision proposal:** ما نقترح اعتماده.
5. **Owner decision:** ما وافق عليه صاحب المشروع صراحة.

لا نستخدم اسم مشروع مشهور أو عدد ملفات كبير كدليل على الجودة. لا نستخدم سرعة النموذج كبديل عن reasoning quality. لا نستخدم Dataset card كبديل عن Data validation.

## 6. ترتيب العمل الحالي

1. استلام Architecture contracts من Buggy بالترتيب.
2. استلام Runtime policies وregistry.
3. استلام scripts/test logs/GAP register.
4. استلام Ai-Hunting snapshot وcommit hash.
5. استلام OffsecCyber docs/license/manifest/samples/training/eval.
6. استلام CBH phase audit outputs الأصلية.
7. إنشاء `REFERENCE_INDEX.md` و`REFERENCE_ALIGNMENT_MATRIX.csv`.
8. مراجعة مخرجات Phase 3 حسب الاعتماديات، مع targeted checks فقط عند الحاجة.
9. كتابة Architecture Decision Records للقرارات الكبيرة.
10. بعد اعتماد المالك فقط: Phase 4 Unified System Architecture Blueprint.

## 7. نموذج الموديلات

الـ architecture analysis ليس task مناسبًا لاختيار أسرع model تلقائيًا. الاقتراح المبدئي:

- Main Architect/Reasoner: model قوي في reasoning وmulti-file consistency.
- Fast extraction worker: model سريع لبناء inventories أو تلخيص batches محددة.
- Independent reviewer: model مستقل يراجع قرارات الـ Architect.
- Human owner: يعتمد أو يرفض القرار النهائي.

تجربة Bake-off يجب أن تستخدم نفس task set ونفس acceptance rubric، لا انطباعًا من محادثة واحدة. أعد فحص `opencode models` في البيئة الحالية. لا ترسل API keys.

## 8. Exit gate قبل Phase 4

لا تبدأ Blueprint حتى تتحقق الشروط التالية:

- استلام المصادر الأساسية أو تسجيل أنها غير متاحة.
- معرفة exact versions/commits لكل مصدر.
- فحص LICENSE/provenance للـ external materials قبل إعادة الاستخدام.
- اكتمال Reference Index.
- مقارنة أهم CBH architectural findings بالمراجع.
- تحديد conflicts وGAPs ومخاطر تبني كل design.
- اتخاذ Owner decisions للقرارات التي تمنع التصميم.
- تسجيل unresolved issues بدل تخمين حلها.

**الحالة الحالية: هذه الشروط لم تُستوفَ بالكامل. Phase 4 Blueprint لم تبدأ.**


---

# CBH — Decisions, Governance & Working Rules

## 1. الأدوار

| الدور | المسؤولية | الحدود |
|---|---|---|
| Owner (المستخدم) | صاحب المنتج والقرار النهائي، يجهز الملفات ويحدد الأولويات ويعتمد الإصدارات. | لا يتم اعتبار صمت المالك موافقة. |
| ChatGPT — Architect / Reviewer | تحليل المصادر، استخراج المتطلبات، بناء المقارنات، اقتراح architecture، مراجعة الملفات والقرارات. | لا يدّعي تنفيذ شيء في Repo أو اختبار شيء لم يشغله. |
| DeepSeek داخل ChatGPT — Document Author | صياغة ملف كامل بناءً على prompt bounded ومصادر محددة. | لا يختار المرحلة التالية بنفسه ولا يعتبر مراجعته Owner lock. |
| OpenCode / model داخل Kali — Repository Operator | قراءة وكتابة ملفات المشروع وتنفيذ tests/commits/pushes ضمن task مصرح به. | هو الكاتب/المنفذ الوحيد داخل repo في المسارات المعتمدة؛ لا يعيد تصميم النظام أو يغير ملفات مقفولة من تلقاء نفسه. |

## 2. المبدأ الحاكم

**AI proposes → Runtime proves → Human decides.**

- AI يقترح بناءً على الأدلة.
- Runtime/Tests تثبت السلوك المحدد فقط.
- Human owner يقرر اعتماد التصميم أو التغيير.

لا يمكن اعتبار رد AI دليل Runtime. ولا يمكن اعتبار unit test محدود إثباتًا لنظام كامل.

## 3. دورة العمل الرسمية

```text
Analyze → Design → Review → Approve → Implement → Verify
```

1. **Analyze:** قراءة المصادر والتدقيق الحالي واستخراج facts/GAPs.
2. **Design:** اقتراح قرار محدد مع dependencies وtrade-offs.
3. **Review:** مراجعة مستقلة ومقارنة acceptance criteria.
4. **Approve:** موافقة صريحة على نطاق التغيير والنسخة.
5. **Implement:** تنفيذ bounded task واحدة.
6. **Verify:** tests/behavior evidence، ثم تقرير صريح بما نجح وما لم يُختبر.

لا يتم القفز من Analyze إلى Implement.

## 4. قواعد تغيير الملفات

- كل task يجب أن يذكر source inputs، allowed changes، dependencies، outputs، acceptance checks، stop conditions.
- ملف locked لا يتم تعديله داخل نفس version. أي تعديل normative يتطلب successor version.
- لا يتم تغيير أكثر من artifact كبير في task واحدة إلا إذا كانت dependency غير قابلة للفصل ومذكورة صراحة.
- لا يتم إجراء sweeping rewrite أو migration دون manifest/plan وموافقة المالك.
- لا يتم حذف/دمج/نقل أي ملف لأن Assessment صنفه كمقترح فقط.
- لا تكتب أسرارًا في Git أو prompts أو logs أو packages.
- لا تستخدم hashes كبديل عن trusted reference؛ hash مفيد فقط إذا كان المرجع الذي نقارنه موثوقًا.

## 5. قواعد الاختبار والإثبات

- كل test يجب أن يوضح ما الذي يثبته وما الذي لا يثبته.
- Mock test يثبت السلوك في Mock فقط.
- Preflight check لا يثبت أن actual dispatcher يطبّق نتيجة preflight.
- Unit test لvalidator لا يثبت أن كل invocation path يمر عبره.
- نجاح report generation لا يثبت صحة finding.
- رفض request خارج scope في module لا يثبت أن كل network egress مغلق.
- أي test لم يتم تشغيله يجب أن يظهر `NOT RUN` أو `NOT VERIFIED`، لا `PASS`.
- Evidence يجب أن يكون قابلًا للربط بالـ finding والـ target والـ request/response أو artifact الأصلي.

## 6. قواعد Scope وSafety

- Default-deny عند غياب scope أو وجود ambiguity.
- Deny wins عند تعارض allow/deny.
- لا توسع scope تلقائيًا من hostname أو redirect أو discovered asset.
- افصل passive collection عن active testing وعن intrusive testing.
- Destructive/state-changing operations ليست default، وتحتاج ضرورة واختبارًا آمنًا وموافقة مناسبة.
- Rate/concurrency/timeouts/blast radius يجب أن تكون محددة عند الحاجة.
- Tool execution يحتاج policy enforcement عند invocation boundary، لا مجرد Prompt instruction.
- Scope validator ليس network sandbox؛ يجب أن تكون العزلة على طبقة runtime/egress أيضًا.

## 7. قواعد الـ Skills

- لا تنشئ Agent لكل vulnerability class؛ استخدم عددًا محدودًا من Agents وSkill catalog واضحًا.
- Skill ownership boundaries مهمة لمنع تكرار probes وإرباك routing.
- Skill discovery ≠ Skill mapping ≠ Skill loading ≠ Skill execution.
- Required tool capability يجب أن يعلن بوضوح؛ لا تذكر Browser proof إذا لم يكن هناك browser path فعلي.
- الأوامر داخل Skill يجب أن تكون قابلة للتحقق، bounded، ومناسبة للهدف.
- destructive payloads يجب ألا تظهر كأنها proof عادي أو default validation.
- أي Skill update يجب أن يمر عبر lint/schema/cross-reference/safety review واختبارات مناسبة.

## 8. No prompt treadmill

- One bounded task at a time.
- لا تطلب من النموذج إعادة فحص corpus كامل عند وجود أدلة قابلة لإعادة الاستخدام.
- لا تكرر نفس audit أو نفس test بنفس inputs دون سبب جديد.
- إذا ظهر نقص: سجّل gap محددًا واطلب الجزء اللازم فقط.
- لا تنشئ سلسلة prompts لنفس النتيجة دون أن يتغير المصدر أو acceptance criteria.
- اجمع القرارات حسب dependency cluster بدل توزيعها عشوائيًا على عشرات prompts.

## 9. Progress vocabulary

في project roadmap استخدم الحالات:

- `TODO`
- `IN_PROGRESS`
- `DONE`

أما `LOCKED` فهي Owner decision منفصلة مرتبطة بartifact/version محدد. لا تكتب `LOCKED` كحالة lifecycle إلا إذا كان contract يسمح بذلك صراحة.

## 10. Git safety

قبل تنفيذ أي operation:

1. `pwd -P`
2. `git rev-parse --show-toplevel`
3. `git branch --show-current`
4. `git rev-parse HEAD`
5. `git status --short --branch`
6. inspect remotes and push routing.
7. confirm intended repo/branch and task.

لا تنفذ `reset --hard`, `clean`, force push, history rewrite, branch delete أو تغيير remotes دون موافقة محددة. حافظ على user changes.

## 11. Required end-of-task report

كل task تنفيذية ترجع:

1. نطاق العمل الذي اكتمل.
2. الملفات التي أُنشئت/عُدلت ومساراتها.
3. commands/tests التي تم تشغيلها بالنتائج الفعلية.
4. source discrepancies وGAPs وblockers.
5. commit hash وpush destination فقط إذا تمت فعلًا.
6. ما لم يتم عمله.

**File transfer is not implementation. Test pass proves only its scope. Commit/push is not proof of runtime safety.**


---

# Prompt جاهز لبداية الشات الجديد

انسخ النص التالي في أول رسالة بعد رفع حزمة CBH:

---

أنت الآن تعمل معي على مشروع **CBH (Claude-BugHunter)**. أرفقت حزمة handoff تحتوي على تاريخ المشروع وتقارير Phases 0–3 وخطة الاستعداد لـ Phase 4.

**قبل أن تقترح أي خطوة:** اقرأ كل ملفات الحزمة، وليس `README` فقط. ابدأ بـ `00_MASTER_HANDOFF.md` ثم تقارير Phase 0 و1 و2 و3، وبعدها `05_PHASE_4_REFERENCE_INTAKE_NOT_STARTED.md` وملف governance وsource register.

## فهم المشروع

- CBH هو المنتج المستهدف.
- `Claude-BugHunter` هو upstream/codebase الذي انطلقت منه نسخة التطوير.
- Buggy وAi-Hunting وOffsecCyber مراجع مستقلة للمقارنة، وليست مشاريع سننسخها.
- مبدأ المشروع: **AI proposes → Runtime proves → Human decides.**
- الأدوار: أنا Owner وصاحب القرار النهائي؛ ChatGPT Architect/Reviewer؛ DeepSeek في ChatGPT Document Author محدود؛ OpenCode في Kali Repository Operator/Executor ضمن مهام مصرح بها.

## الحالة التي يجب أن تبدأ منها

- Phase 0 Foundation & Repository Setup: DONE.
- Phase 1 Repository & Architecture Audit: DONE.
- Phase 2 Skills Deep Audit: DONE؛ تم توثيق 83/83 Skills و22 supporting files.
- Phase 3 Project-Wide Value Assessment: DONE كـ preliminary assessment؛ inventory 298 files، dependency matrix 90 rows، decision matrix 298 rows.
- Phase 4 Unified System Architecture Blueprint: NOT STARTED.
- Phases 5–11: NOT STARTED.
- لا يوجد تصريح بتعديل source code أو بدء implementation.

## المطلوب الآن

لا تكتب Blueprint مباشرة. ساعدني في إكمال Reference Intake:

1. راجع قائمة Buggy source files المطلوبة، وإصداراتها، وlock/review evidence.
2. راجع Ai-Hunting من snapshot/commit حقيقي، لا من directory tree فقط.
3. راجع OffsecCyber manifest/README/LICENSE وعينات train/valid/test وأدلة التدريب والتقييم.
4. اربط هذه المصادر بمخرجات Phase 1–3 الحالية.
5. أنشئ Reference Index وReference Alignment Matrix.
6. صنّف كل فكرة إلى Adopt / Adapt / Reject / New Design مع evidence وdependencies وtest requirements.
7. اطلب مني فقط الملف التالي المطلوب، ولا تطلب إعادة رفع ما تم توفيره بالفعل.
8. لا تعيد قراءة الـ 83 Skill أو إعادة تقييم 298 ملفًا من الصفر. استخدم تقاريرها، واطلب targeted inspection فقط عندما توجد gap حقيقية.
9. لا تنفذ code changes أو migrations أو Git operations.

## قواعد ضرورية

- افصل Source facts عن استنتاجاتك ومقترحاتك.
- لا ترفع confidence من غير دليل.
- لا تعتبر mock test إثباتًا live.
- لا تعتبر `KEEP AS-IS` أو `MODIFY` في Phase 3 قرارًا نهائيًا من المالك.
- لا تنسخ Buggy أو Ai-Hunting wholesale.
- لا تفترض أن OffsecCyber dataset صالحة للتدريب أو RAG دون فحص schema, provenance, licensing, duplicates, temporal leakage, and evaluation.
- لا تختر model architecture بناءً على السرعة فقط؛ استخدم controlled bake-off إذا احتجنا الاختيار.
- One bounded task at a time. لا prompt treadmill.
- لا تسألني عن معلومة موجودة بالفعل في الحزمة.

**أول رد منك يجب أن يكون:** تأكيد فهم الحالة عبر موجز منظم، وذكر ما هو مكتمل وما هو غير مكتمل، ثم تحديد أول ملف واحد مطلوب لبدء Reference Intake بناءً على ترتيب الأولوية. لا تبدأ Phase 4 Blueprint قبل اكتمال بوابة المرجعيات وموافقتي.

---


---

# Source Register & Evidence Limits

## 1. ما الذي بُني عليه هذا الـ Handoff؟

تم تجميع سجل CBH من المحادثات والسجلات/المخرجات التي كانت متاحة في سياق العمل، خصوصًا:

- سجل تأسيس نسخة `cbh-dev` وتكوين Git remotes.
- سجل Repository & Architecture Audit.
- سجل Phase 2 Skills Deep Audit، بما فيه coverage reconciliation والـ batch mappings.
- سجل Phase 3 Project-Wide Value Assessment ونتائج integrity checks.
- سجل تشغيل Engine في Mock mode.
- رسائل المالك حول تعديل نطاق Phase 3 وتأجيل Phase 4 لحين استلام المراجع.
- ملفات Buggy management/reference التي أُرسلت سابقًا، وملاحظات المصادر التقنية السابقة.
- Snapshot وصف OffsecCyber dataset card الذي أرسله المالك.
- Tree snapshot لمشروع Ai-Hunting الذي أرسله المالك.

## 2. الملفات/المخرجات التي توجد على Kali حسب السجلات

### 2.1 Phase 1

التقرير النهائي الكامل لـ repository audit كان موصوفًا في سجل OpenCode بأنه مخرجات داخل `/tmp/opencode/cbh-audit/` أو في session artifacts. الملخص المتاح يشير إلى 18 sections، لكن النسخة الكاملة لم تُرفق داخل حزمة handoff الحالية.

### 2.2 Phase 2

المسار:

```text
/tmp/opencode/cbh-audit/skills-deep/
```

المخرجات:

- `SKILLS_INVENTORY.md`
- `SKILLS_CAPABILITY_MATRIX.md`
- `SKILLS_DEEP_FINDINGS.md`
- `SKILLS_AUDIT_COVERAGE.md`
- `batches/batch01.md` إلى `batches/batch11.md`
- `batches/batch02-original.md`
- `remaining_manifest.json`

### 2.3 Phase 3

المسار:

```text
/tmp/opencode/cbh-audit/project-value-assessment/
```

المخرجات:

- `PROJECT_FILE_INVENTORY.csv`
- `PROJECT_VALUE_ASSESSMENT.md`
- `DEPENDENCY_IMPACT_MATRIX.csv`
- `PROJECT_DECISION_MATRIX.csv`
- `_evidence/` (persisted/recovered evidence and metadata)

### 2.4 Repo source

```text
/home/kali/cbh-dev
```

Baseline HEAD:

```text
9269278fec34d7d75bdf682a3d9b26c98339d648
```

## 3. ما الذي لم يتم نقله إلى هذه الحزمة؟

- النسخ الأصلية الكاملة من Phase 1 audit.
- ملفات Phase 2 الأربعة الأصلية كاملة بكل line-level details، والـ batch reports الأصلية.
- ملفات Phase 3 الأربعة CSV/MD الأصلية.
- كل source repository contents من CBH.
- Ai-Hunting repository ZIP/snapshot الكامل.
- ملفات Buggy الأصلية الكاملة لكل Architecture/Runtime contracts.
- OffsecCyber full dataset/training files.

لذلك هذا التقرير لا يدّعي أنه يحتوي كل raw evidence، بل يحافظ على أهم النتائج والسياق والقرارات والمخرجات والمسارات. عندما نحتاج مراجعة تفصيلية أو اتخاذ قرار على ملف محدد، يجب الرجوع إلى الملف الأصلي الموجود على Kali أو طلبه من المالك.

## 4. Source facts vs analysis

| النوع | مثال | كيف نستخدمه |
|---|---|---|
| Source fact | Git HEAD والـ clean working tree | fact حسب فحص مسجل في تاريخ محدد؛ أعد الفحص قبل عمليات جديدة. |
| Audit finding | Engine `skills_on=False` | نتيجة static/code inspection؛ نحدد حدودها. |
| Runtime observation | mock engine produced 1 confirmed fixture finding | يثبت mock path فقط. |
| Assessment | CLI/Engine responsibility overlap | استنتاج معماري يحتاج Owner decision. |
| Planned | Reference alignment before Blueprint | خطة لم تنفذ بعد. |
| Unknown | live headless Skill auto-load | لا تعلن نجاحه حتى يختبر. |

## 5. Source notes from earlier architecture research

كانت هناك source notes في محادثات سابقة حول:

- Coordinator → Solvers → isolated runtime → async events → validators → report.
- AI-assisted hunting / protobuf reversing / coverage / self-improving memory.
- MCP security.
- Micro-agents for offensive security and AI fuzzing.
- Skills, methodology, notes, validator, report writer.
- Claude Code architecture: `CLAUDE.md`, Skills, Subagents, Agent Teams.
- HunterStick: persistent target context and focused hunting workspace.
- AI Hunting Agent Architecture v0.5.
- فيديوهات/مصادر متعددة تم تلخيصها في شكل notes وليس كلها original transcripts.

هذه الملاحظات مفيدة كـ source index أولي، لكنها ليست بديلًا عن رابط المصدر الأصلي أو transcript كامل عند الحاجة لإثبات claim محدد. يجب تسجيل original source vs derived summary في Reference Index.

## 6. Integrity notes

- Phase 2 coverage reconciliation: 83 unique Skill paths + 22 supporting paths = 105.
- Phase 3 reconciliation: inventory paths = decision matrix paths = 298، 0 missing/extra/empty dispositions، dependency endpoints متسقة مع inventory.
- Git state at Phase 3 completion: HEAD unchanged and working tree clean.
- No code modifications, merge, deletion, commit or push was performed in Phase 1–3 audit sessions according to the records.

## 7. What a new chat must not assume

- لا تفترض أن تقرير Markdown الحالي يساوي نسخة Phase 1/2/3 الأصلية.
- لا تفترض أن Ai-Hunting تم فحصه بالكامل.
- لا تفترض أن OffsecCyber dataset تم تحليل كل سطر فيها أو اختبار training عليها.
- لا تفترض أن كل Disposition في Phase 3 approved.
- لا تفترض أن Mock pipeline يثبت production readiness.
- لا تفترض أن private `bugMO77/cbh` أصبح يحتوي source code؛ آخر حالة مسجلة أنه كان فارغًا ولم يتم Push.
- لا تفترض أن model/provider list في OpenCode لم تتغير.

## 8. Recommended source recovery order

عند توفر وصول Kali، استرجع الملفات بالترتيب:

1. Phase 3 four deliverables + `_evidence/` index.
2. Phase 2 `SKILLS_DEEP_FINDINGS.md`, `SKILLS_AUDIT_COVERAGE.md`, `SKILLS_CAPABILITY_MATRIX.md`, `SKILLS_INVENTORY.md`.
3. Phase 1 full repository audit report and discrepancy register.
4. Exact current Git state and any current source modifications.
5. Buggy files requested in Phase 4 intake.
6. Ai-Hunting exact commit snapshot.
7. OffsecCyber documentation and samples.

لا تعيد تنفيذ audit كاملًا أثناء استعادة الملفات. المطلوب هو نقل الأدلة الموجودة.
