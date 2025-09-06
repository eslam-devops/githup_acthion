
---

## 🎤 Introduction

بص يا معلم، GitHub Actions ده يعتبر **المخ** بتاع الـ CI/CD جوه GitHub.
يعني إيه CI/CD؟

* CI = Continuous Integration (دمج الكود باستمرار)
* CD = Continuous Deployment/Delivery (نشر الكود باستمرار)

ببساطة: بدل ما تفضل تعمل build و test و deploy يدوي، GitHub Actions بيخليك تعمل **automation** لكل ده.
كل حاجة بتمشي لوحدها أول ما تعمل push أو PR. 🚀

في المحاضرة دي هنتكلم عن:

* إيه هو الـ Workflow
* إيه هو الـ Job
* إيه هو الـ Step
* وإزاي التلاتة دول بيركبوا فوق بعض زي **سندوتش كبدة بالعيش البلدي** 🥖😂

---

## 🧩 Main Explanation

### 1. Workflows

* الـ Workflow ده هو **السيناريو الكبير** أو الـ "script الرئيسي" اللي بيحدد إيه اللي هيحصل.
* بيتكتب في ملف YAML جوا `.github/workflows/`.
* لازم يكون مربوط بـ **Trigger** (اللي بيشغله).
  أمثلة:

  * أول ما تعمل push → workflow يشتغل.
  * أول ما يتفتح Pull Request → workflow يشتغل.
  * كل يوم الساعة 12 بالليل → workflow يشتغل.
* يقدر يحتوي على Job واحد أو أكتر.

تخيل الـ Workflow زي **قائمة التشغيل (playlist)** على Spotify 🎵.
الـ Trigger هو الزرار اللي بيخليك تشغلها، والـ Jobs هي الأغاني اللي جواها.

---

### 2. Jobs

* جوه الـ Workflow بيكون عندنا واحد أو أكتر **Job**.
* الـ Job بيشتغل في بيئة تشغيل (runner) زي:

  * `ubuntu-latest` 🐧
  * `windows-latest` 🪟
  * `macos-latest` 🍏
* كل Job بيتنفذ في **VM مستقلة** (يعني مفيش شيرنج بين jobs).
* الـ Jobs بتشتغل **بالتوازي** (parallel) إلا لو قولتلها تعتمد على بعض.

فكر فيها زي **فرق شغل في شركة**:

* كل فريق (Job) عنده مكتب خاص بيه (VM).
* يقدروا يشتغلوا مع بعض في نفس الوقت.
* بس لو في فريق لازم يخلص الأول عشان التاني يبدأ → تحط dependency.

---

### 3. Steps

* جوه كل Job عندك خطوات اسمها **Steps**.
* الخطوة ممكن تكون:

  * أمر Shell (زي `echo "Hello World"`)
  * أو GitHub Action جاهزة من Marketplace (زي Action بتنزل Node.js أو Checkout للكود).
* الـ Steps دايمًا بتتنفذ **واحدة ورا التانية** (sequential).
* لو عايز تعمل حاجات في نفس الوقت → تحطهم في Jobs مختلفة مش Steps.

تخيل إن الـ Job ده زي مطبخ 🍳.

* والـ Steps هي الوصفات اللي بتتنفذ واحدة ورا التانية.
* لو في نص خطوة مشيت غلط → الأكلة كلها هتبوظ 😂

---

### 4. GitHub Actions vs Workflow vs Action

ممكن هنا يحصل لخبطه:

* **GitHub Actions (بالمطلق)** = الـ Platform نفسها بتاعة CI/CD.
* **Workflow** = الملف اللي انت بتكتبه (السيناريو).
* **Action (مفرد)** = كود جاهز (عادة من Marketplace) بتستخدمه كـ Step.

يعني:
GitHub Actions = القهوة كلها ☕
Workflow = الكوباية اللي فيها القهوة 🥤
Action = السكر اللي بتحطه جوا الكوباية 🍬

---

### 5. مثال عملي سريع

ملف YAML بسيط:

```yaml
name: CI Example

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Run tests
        run: echo "Running tests..."
```

* Workflow اسمه `CI Example`
* بيتشغل لما تعمل push
* فيه Job اسمه `build` بيشتغل على Ubuntu
* جوه خطوتين:

  * واحدة Action جاهزة (`checkout`)
  * والتانية أمر Shell

---

## 📝 Summary & Revision Notes

* **Workflow** = الملف الكبير (بيتشغل بـ Trigger، جوا Repo)
* **Jobs** = وحدات الشغل (بتشتغل في VMs منفصلة، parallel by default)
* **Steps** = خطوات جوه الـ Job (sequential دايمًا)
* **Action** = كود جاهز بتستخدمه كـ Step
* Indentation في YAML = حياة أو موت 😅

---

## 🛠 Practical Exercises

1. اعمل Repo جديد على GitHub
2. جوه `.github/workflows/` اعمل ملف اسمه `first.yml`
3. جرب تكتب Workflow فيه Job واحد بيعمل:

   * Checkout للكود

تمام يا إسلام 😎
هنا هنحول الكلام اللي فوق لمحاضرة كاملة بالمصري، مع الأمثلة والـ emojis، بحيث تحس إنك في كلاس مباشر وبتنفذ أول Practical Exercise على GitHub Actions بنفسك.

---

## 🎤 Introduction

النهاردة هنشتغل عملي لأول مرة على GitHub Actions.
هدفنا إننا نعمل **Workflow بسيط لكنه شغال 100%** عشان نثبت فهمنا للمفاهيم اللي شرحناها في المحاضرة اللي فاتت.
هنتعلم:

* إزاي نكتب أول ملف Workflow
* إزاي نحدد Trigger
* إزاي نضيف Jobs و Steps
* وهنشوف إيه اللي بيحصل لما Step تفشل 🛑

---

## 🧩 Main Explanation

### 1. إنشاء هيكل الملفات

أي Workflow في GitHub Actions **لازم** يتخزن في مكان ثابت داخل الـ Repo:

```
.github/workflows/
```

📌 الخطوات:

1. جوه الـ Repo، اعمل فولدر `.github`
2. جواه اعمل فولدر `workflows`
3. جواه أنشئ ملفك مثلاً:

   ```
   01-building-blocks.yml
   ```

💡 مفيش أي Workflow GitHub Actions هيشوفه إلا لو مكانه بالهيكل ده.

---

### 2. تجهيز بيئة الكتابة

لو بتستخدم VS Code، نزّل Extension اسمه **GitHub Actions** من GitHub الرسمي.
ده بيديك:

* Validation للملفات
* Hints على الكلمات المفتاحية
* Links للدعم والـ docs

هيخليك تعرف لو في خطأ في الـ YAML قبل ما ترفع الملف.

---

### 3. كتابة أول Workflow

#### شكل أول ملف:

```yaml
name: 01-building-blocks

on: push

jobs:
  echo-hello:
    runs-on: ubuntu-latest
    steps:
      - name: Say hello
        run: echo "Hello World"
```

📌 هنا:

* `name` = اسم الـ Workflow (هيظهر في Actions tab)
* `on: push` = الـ Trigger (لما تعمل push لأي فرع)
* `jobs` = فيه Job اسمه `echo-hello`
* `runs-on: ubuntu-latest` = بيشتغل على Linux runner
* `steps` = خطوة واحدة بتطبع "Hello World"

---

### 4. إضافة Job تاني مع Step فاشلة

تعال نضيف Job تاني عشان نشوف إيه اللي بيحصل لما Step تفشل:

```yaml
  echo-goodbye:
    runs-on: ubuntu-latest
    steps:
      - name: Failed step
        run: |
          echo "I will fail"
          exit 1
      - name: Say goodbye
        run: echo "Goodbye"
```

💡 `exit 1` = كود خروج معناه فشل
⚠️ لما Step تفشل، باقي الـ Steps في نفس الـ Job مش هتتنفذ.

---

### 5. رفع الملف وتشغيله

1. `git add .`
2. `git commit -m "Add building blocks workflow"`
3. `git push`

هتروح على الـ Repo في GitHub → تبويب Actions → هتلاقي الـ Workflow بدأ يشتغل:

* ✅ `echo-hello` هينجح
* ❌ `echo-goodbye` هيفشل في أول Step، والتانية هتكون Skipped

---

### 6. تجربة النجاح

لو غيرنا:

```bash
exit 1
```

إلى:

```bash
exit 0
```

ده معناه نجاح الـ Step.
لما ترفع التعديل:

* ✅ كل Steps هتشتغل
* اللون هيكون أخضر في Actions tab

---

## 📝 Summary & Revision Notes

* **Folder structure**: `.github/workflows/` إجباري
* **Workflow file**: صيغة YAML
* **Triggers**: `on:` لتحديد متى يشتغل الـ Workflow
* **Jobs**: بتشتغل في VMs منفصلة
* **Steps**: بتتنفذ بالترتيب، ولو Step فشلت الباقي بيتوقف
* **exit 0** = نجاح، **exit 1** = فشل

---

## 🛠 Practical Exercises

1. اعمل Workflow جديد باسم `practice.yml`
2. خليه يشتغل على `pull_request` بدل `push`
3. أضف Job فيه 3 Steps:

   * Step تطبع "Starting..."
   * Step تنزل `actions/checkout@v3`
   * Step تطبع "Finished!"
4. جرب تخلي Step 2 تفشل، وشوف النتيجة في GitHub Actions.

---

لو تحب يا إسلام، أقدر في الرد الجاي أعملك **رسم توضيحي هرمي بالـ emojis** يوريلك Workflow → Jobs → Steps، عشان تحفظهم زي الخريطة. تحب أعمله؟

   * يطبع جملة "Hello from GitHub Actions!"
4. اعمل Commit وشوف النتيجة في تبويب **Actions** في Repo

---

تحب يا إسلام أزودلك كمان **رسم توضيحي مرسوم بالـ emojis** يوريك شكل الـ Workflow → Jobs → Steps زي هرمي كده؟
