
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
   * يطبع جملة "Hello from GitHub Actions!"
4. اعمل Commit وشوف النتيجة في تبويب **Actions** في Repo

---

تحب يا إسلام أزودلك كمان **رسم توضيحي مرسوم بالـ emojis** يوريك شكل الـ Workflow → Jobs → Steps زي هرمي كده؟
