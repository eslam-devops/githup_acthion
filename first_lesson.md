

---

## أول حاجة: يعني إيه CI/CD؟ 🤔

بص يا معلم، الموضوع عامل زي مطبخ مطعم 🍔:

* **CI (Continuous Integration)** = كل ما تضيف وصفة جديدة أو تعدّل حاجة في الأكل، لازم الشيف يجربها بسرعة ويتأكد إنها بتمشي مع باقي المنيو.
  👨‍🍳 مثال: أنت عدلت كود في app فيه ٥٠ ميكروسيرفيسز. CI بيشغل **tests** ويتأكد إن الكود بتاعك ما بوّظش حاجة عند باقي السيرفيسز.

* **CD (Continuous Delivery / Continuous Deployment)** = بعد ما تأكدنا إن الأكلة تمام في المطبخ، نجرّب نوديها لصالة المطعم (staging أو شبه production).

  * **Delivery** = نجهز الأكلة، نوديها للجرسون، بس هو مستني إشارة من المدير يوديها للزبون (manual approval).
  * **Deployment** = لأ، ده الجرسون خد الأكلة على طول وحطها على الترابيزة 🚀. مفيش approvals—الثقة في المطبخ ١٠٠٪.

يعني CI يتأكد من "الكود compatible"، وCD يتأكد إن "الكود يشتغل فعلاً على السيرفر/البيئة اللي شبه production".

---

## طيب فين GitHub Actions في النص ده؟ 🤷‍♂️

الناس بتفكر إن GitHub Actions مجرد **CI/CD tool** زي Jenkins, GitLab CI, Travis… إلخ.
لكن الحقيقة: **هو مش بس CI/CD**، هو **Automation Platform** جوه GitHub.

تقدر تعمل بيه حاجات زي:

* أوتوميشن لحاجات مرتبطة بالـissues أو pull requests.
* تبعت إشعارات أو إيميلات.
* تبني Docker image وتبعتها لـDocker Hub.
* تعمل linting / security scanning.
  basically… أي حاجة تقدر تكتبها في script.

---

## طب إيه أصلاً GitHub؟ 📖

تاريخ صغير كده:

* اتعمل 2008 علشان يبقى فيه مكان تقدر تخزن فيه الكود أونلاين وتكولابوريت مع ناس تانية.
* دلوقتي GitHub مش مجرد **repo**:

  1. **Collaborative coding** (pull requests, issues).
  2. **Planning & discussions** (forums جوا GitHub).
  3. **Online editor** (IDE زي VSCode بس في المتصفح ✨).
  4. **Security** (بيعمل scanning ويقولك لو عندك vulnerability).
  5. **Copilot** 🤖 (AI assistant للكود).
  6. **Workflows (GitHub Actions)** = موضوعنا النهاردة.

---

## نخش بقى في Actions 🛠️

### يعني إيه Workflow؟

* ملف `.yml` جواه خطة التشغيل. بيتحط في `.github/workflows/`.
* جواه:

  * **Trigger (on)** = إيه اللي يشغّل الـworkflow (push, PR, issue, schedule).
  * **Jobs** = مهمات.
  * **Steps** = خطوات جوه المهمة.
  * **Actions** = حاجات جاهزة reusable (زي libraries).

### مثال Workflow بسيط 🎉

لو عايز تعمل workflow يشتغل كل مرة حد يعمل ⭐ على الـrepo:

```yaml
name: Star Event Workflow

on:
  watch:
    types: [started]   # لما حد يعمل star

jobs:
  log-star:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Somebody starred the repo! 🌟"
```

* هنا التريجر مش push، لأ… مجرد **star**! 😄
* ده بيوضح إن GitHub Actions مش بس CI/CD، ده أي حاجة.

---

## Real-life analogy 🎬

* **Workflow** = زي رحلة عميل في مطعم (يدخل → يقعد → يطلب → ياكل → يدفع).
* **Job** = كل محطة في الرحلة (الكاشير، المطبخ، الويتر).
* **Step** = خطوات جوه المحطة (الويتر يجيب منيو → يكتب order → يوديه المطبخ).
* **Action** = أداة أو وصفة جاهزة تساعدك (زي ماكينة كاشير، مش كل مرة تكتب الكود من الصفر).

---

## Extra حتة مهمة 💡

* **Runners** = الماكينات اللي بيشتغل عليها الكود (Linux/Windows/macOS machines).

* **Parallel vs Sequential**:

  * الـjobs بتشتغل parallel (إلا لو استخدمت `needs:`).
  * الـsteps جوه job بتشتغل sequential.

* **Marketplace** 🛒: أكتر من 18 ألف ready-made Actions—زي plugins تقدر تستخدمها.

---

## الخلاصة ✍️

* CI = تتأكد إن الكود compatible مع باقي الكود.
* CD = تتأكد إن الكود يشتغل على بيئة شبه/production.
* Continuous Delivery = محتاج manual approval.
* Continuous Deployment = أوتوماتيك لحد production.
* GitHub = مش مجرد repo، ده platform فيها coding, planning, security, AI, workflows.
* GitHub Actions = automation tool جوا GitHub، مش بس CI/CD.
* Workflow = YAML file فيه triggers → jobs → steps → actions.
* Actions = reusable modules من marketplace أو بتكتبها بنفسك.
* Jobs run parallel، Steps run sequential.
* Runners = الماكينات اللي بينفّذ عليها jobs.

---

تحب أكمّل بنفس الأسلوب في الفيديوهات الجاية (كل مرة تبعتلي transcript وأنا أشرحه بالستايل ده)، ولا عايز ألخصلك الكورس كله chunk by chunk؟

تمام 🙌 ناخد الكلام ده واحدة واحدة ونشرحه بطريقة كده خفيفة دم مصرية مع شوية أمثلة من الحياة الواقعية 🧑‍🍳💻.

---

## 🟢 أول حاجة: يعني إيه Checkout الكود؟

بص يا باشا، أي **Workflow** في GitHub Actions عشان يشتغل على الكود بتاعك، لازم أصلاً يجيب الكود من الريبوزيتوري.
Think of it كده:
إنت شيف 👨‍🍳، وعايز تعمل أكل… ينفع تبدأ تطبخ من غير ما تروح تجيب المكونات من التلاجة؟ مستحيل 😅.
نفس الحكاية هنا: أول **step** في أي workflow بتبقى غالبًا اسمها **Checkout code** = نزل الكود من الريبوزيتوري.

---

## 🟡 إزاي نعمل Checkout باستخدام Action جاهزة؟

GitHub عنده **Action** مشهورة جدًا اسمها [`actions/checkout`](https://github.com/actions/checkout).
دي بالظبط زي ما تقول "Delivery guy" 🚴‍♂️ اللي بيجيبلك المكونات من التلاجة ويحطها قدامك.

الكود هيبقى كده مثلًا:

```yaml
steps:
  - name: Checkout Repository
    uses: actions/checkout@v3
```

* **name**: ده مجرد label عشان تعرف في اللوج إيه اللي بيحصل.
* **uses**: دي معناها "استعمل Action جاهز" → وهنا استعملنا `actions/checkout`.
* **@v3**: يعني النسخة الثالثة (version 3). كل Action ليها إصدارات، زي ما بتشتري موبايل iPhone 12 أو 15 😅، كل واحد فيه إمكانيات مختلفة.

---

## 🟠 بعد الـ Checkout… نعمل إيه؟

هنا بقى إنت حر 🎨.
في المثال اللي إنت سامعه في الفيديو: الراجل بيعمل مجرد **logging message**.
يعني يطبع حاجة على الـ console، كنوع من الاختبار إن الورك فلو شغال.

```yaml
  - name: Log Star Event
    run: |
      echo "Somebody starred the repo! 🌟"
```

* هنا استخدمنا `run` → معناها "اكتبلي أمر shell".
* مش لازم تبقى Action، ممكن تبقى أي command عادي (echo, cat, npm install, python script...).
* الـ `|` اللي في الـ YAML معناها "multi-line string" → يعني ممكن تكتب أكتر من command تحت بعض.

---

## 🟤 Real-life Example 🛒

خلينا نقول إنك عامل **Delivery Workflow**:

1. **Checkout step** = حد جابلك المقاضي من السوبر ماركت.
2. **Run step** = إنت وقفت في المطبخ وبدأت تطبخ (commands/scripts).
3. ممكن تضيف بعد كده **Actions** جاهزة، زي:

   * تبعت إشعار على Slack 📩.
   * ترفع logs على ElasticSearch 📊.
   * تبني Docker image 🐳.

يعني الموضوع Modular… زي LEGO 🧩، بتركب اللي إنت عايزه.

---

## 🟢 Bonus: Public vs Private Repo 🗝️

* **Public repo** = أي حد يقدر يشوف الكود → perfect لو إنت بتعمل open source. وده كمان بيديك unlimited GitHub Actions minutes مجانًا ⏱️.
* **Private repo** = الكود مقفول عليك وعلى فريقك. GitHub بيديك 2000 دقيقة مجانًا (على free plan)، وبعدها تدفع حسب نوع الـ runner:

  * Linux = أرخص ⬅️ \$0.008/min
  * Windows = أغلى شوية ⬅️ \$0.016/min
  * macOS = أغلى واحد فيهم ⬅️ \$0.084/min

ولو عندك self-hosted runner (يعني بتشغل jobs على سيرفراتك إنت) → GitHub مش بيحاسبك على حاجة 🥳.

---

## 🟣 Enterprise Options 🏢

لو إنت شركة كبيرة عندك compliance requirements (زي HIPAA, ISO, GDPR)… ساعتها فيه:

* **GitHub Enterprise Cloud** = GitHub بيستضيفلك كل حاجة عنده.
* **GitHub Enterprise Server** = إنت تستضيف GitHub على سيرفرك الخاص.
  وده بيديك control زيادة (IPs, SSO, reports...).

---

## ✅ الخلاصة (Cheat Sheet)

* **Checkout Action** = تجيب الكود للـ runner (`actions/checkout@v3`).
* **uses** = استعمل Action جاهزة.
* **run** = نفّذ أمر shell.
* Public repos = unlimited free minutes 🎉.
* Private repos = 2000 free minutes → بعدها حسب نوع الـ runner.
* Self-hosted runners = free تمامًا.
* Enterprise plans = للشركات اللي محتاجة security و compliance عالي.

---

تحب أعملك مثال عملي كامل من أول `on: push` لحد checkout + logging، بحيث يبقى جاهز تنسخه وتحطه في أول lab عندك؟ 🧑‍💻

