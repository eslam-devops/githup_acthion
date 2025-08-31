
---

## **1. GitHub Actions مش مجرد CI/CD!**
GitHub Actions هو أداة من GitHub بتسمحلك **بأتمتة سير العمل (workflows)** في مستودعاتك (repositories). مش بس **CI/CD** (التكامل المستمر والنشر المستمر)، لا! هو بيقدم لك **أكثر من كده بكتير**! 🚀

### **CI (Continuous Integration) إيه؟**
- كل ما ترفع كود جديد (`push`) على الريبوزيتوري، **CI** بيشغل **tests** عشان يتأكد إن الكود الجديد متوافق مع بقيه الكود.
- مثال: لو عملت **feature** جديدة أو **fix** لباگ، **CI** هيشغل **tests** عشان يتأكد إن الكود مش هيكسر أي حاجه في النظام.
- زي ما تكون بتفحص السياره قبل ما تسافر! 🚗💨

### **CD (Continuous Delivery/Deployment) إيه؟**
- بعد ما **CI** يتأكد إن الكود شغال، **CD** بيشوف إن الكود ينفع ينزل على **production** أو **staging** من غير مشاكل.
- **Continuous Delivery**: الكود بيتنزل على **staging** عشان يتاخد **approval** قبل ما ينزل على **production**.
- **Continuous Deployment**: الكود بيتنزل **تلقائياً** على **production** بعد ما يجتاز كل الاختبارات. 🎯

---

## **2. ليه GitHub Actions مختلف؟**
GitHub Actions مش مجرد أداة **CI/CD** زي **Jenkins** أو **CircleCI**. هو بيقدم:
1. **أتمتة أي شيء** في GitHub: مش بس **build, test, deploy**، لا! ممكن تعمل **automation** لأي حاجه في الريبوزيتوري.
2. **Marketplace**: فيه **18,000+ action جاهزة** تقدر تستخدمها بدون ما تكتب كود! زي ما تكون بتستخدم **plugins** في برامج التعديل. 🔌
3. **Self-hosted runners**: تقدر تشغل **workflows** على سيرفراتك الخاصة.
4. **Event-driven**: ممكن تشغل **workflow** بناء على **events** زي:
   - **Push** أو **Pull Request**.
   - **Issue** أو **Star** على الريبوزيتوري.
   - **Schedule** (مواعيد محدده).
5. **Security**: GitHub بيقدم **scanning** للكود عشان يكتشف ثغرات أمنية. 🔒

---

## **3. أمثلة من الحياة اليومية**
- **مثال 1**: لو عندك **مطعم** 🍔، وكل ما حد يطلب **طعمية**، الطاهي (`GitHub Actions`) بيبدأ يعملها تلقائياً.
- **مثال 2**: لو عندك **مصنع** 🏭، وكل ما توصل **مواد خام** (`push`), الآلات (`workflow`) تبدا تصنع المنتج (`deploy`).

---

## **4. مكونات GitHub Actions**
### **1. Workflow**
- هو **وصفة** بتقول لـ GitHub Actions يعمل إيه بالضبط.
- بيتكتب في ملف `.yml` داخل مجلد `.github/workflows/`.
- مثال:
  ```yaml
  name: CI
  on: [push]  # التريجر: كل ما حد يعمل بوش
  jobs:
    test:
      runs-on: ubuntu-latest  # الرانر: نظام التشغيل
      steps:
        - uses: actions/checkout@v4  # عمل تشيك اوت للكود
        - run: npm test  # تشغيل الاختبارات
  ```

### **2. Events (التريجرز)**
- **الحدث** اللي بيشغل الـ **workflow**.
- أمثلة:
  - `push`: كل ما حد يرفع كود.
  - `pull_request`: كل ما حد يعمل **pull request**.
  - `schedule`: في وقت معين (مثلا كل يوم في الساعة 12 صباحاً).

### **3. Jobs و Steps**
- **Job**: مجموعة من **الخطوات** (`steps`) بتتنفذ على **runner** (سيرفر).
- **Step**: أمر معين، زي تشغيل **test** أو **build**.
- مثال:
  ```yaml
  jobs:
    build:
      runs-on: ubuntu-latest
      steps:
        - name: Checkout code
          uses: actions/checkout@v4
        - name: Install dependencies
          run: npm install
  ```

### **4. Runners**
- **السيرفر** اللي بيشغل الـ **jobs**.
- ممكن يكون:
  - **GitHub-hosted runners** (مجاني لمشروعات **public**).
  - **Self-hosted runners** (على سيرفراتك الخاصة).

### **5. Actions**
- **وحدات جاهزة** تقدر تستخدمها في **steps**.
- مثال: `actions/checkout@v4` لعمل **checkout** للكود.

---

## **5. مثال عملي: CI/CD لبرنامج بسيط**
### **الخطوات:**
1. **إنشاء ملف workflow**:
   ```yaml
   name: Node.js CI
   on: [push]
   jobs:
     test:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v4
         - uses: actions/setup-node@v4
           with:
             node-version: 20
         - run: npm install
         - run: npm test
   ```

2. **رفع الكود**:
   - كل ما تعمل `push`, GitHub Actions هيشغل **tests**.
   - لو **tests** نجحت، ممكن تنزل الكود على **production**.

---

## **6. أسعار GitHub Actions**
- **مجاناً** لمشروعات **public**.
- **2000 دقيقة/شهر** مجاناً لمشروعات **private**.
- لو عديت الحد، بتدفع **$0.008 لكل دقيقة** على **Linux**.

---

## **7. ملخص النقاط الرئيسية**


| النقطة | الشرح |
|--------|-------|
| **GitHub Actions** | أداة لأتمتة سير العمل في GitHub. |
| **CI/CD** | تكامل ونشر الكود تلقائياً. |
| **Workflow** | ملف `.yml` بيحدد الخطوات اللي هتنفذ. |
| **Events** | الأحداث اللي تشغل الـ **workflow** (مثل `push`). |
| **Jobs** | مجموعة من الخطوات (`steps`) بتتنفذ على **runner**. |
| **Actions** | وحدات جاهزة تقدر تستخدمها في **steps**. |
| **Runners** | السيرفرات اللي بتشغل **jobs**. |
| **Marketplace** | مكان لتحميل **actions** جاهزة. |

---

**سؤال مهم:** عايز نطبق مثال معين؟ ولا في جزء محتاج توضيح أكتر؟ 🤔
*(قول لي، وانا هاشرحه زي ما تكون بتشرح لاصدقائك على الكوشة!)* ☕😃

**اهلا يا اسطورة!** 👋 اليوم هنتكلم عن **GitHub Actions** بطريقة سهلة ومسلية، زي ما بنشرب شاي ونضحك! ☕😄

---

## **1. الويب هوك تريجرز (Webhook Triggers)**
### **مثال عملي: تشغيل الـ Workflow عند عمل Pull Request**
1. **إنشاء ملف الـ Workflow**:
   - ملف اسمه `push-pr.yml` داخل `.github/workflows/`:
     ```yaml
     name: CI
     on:
       push:
         branches: [main]
       pull_request:
         branches: [main]
     jobs:
       test:
         runs-on: ubuntu-latest
         steps:
           - uses: actions/checkout@v4
           - run: npm test
     ```

2. **عمل تعديل في الكود**:
   - عملنا **branch** جديد اسمه `test`.
   - عدّلنا ملف `app.js` ورفعنا التعديلات.
   - عملنا **Pull Request** من `test` إلى `main`.

3. **نتائج الـ Workflow**:
   - الـ **Workflow** اشتغل تلقائياً عند عمل **Pull Request**.
   - شغال **tests** على الكود الجديد.
   - لو الـ **tests** نجحت، ممكن نعمل **merge** بأمان.

---

## **2. السكديولد تريجرز (Schedule Triggers)**
### **مثال: تشغيل الـ Workflow كل يوم في وقت معين**
1. **إنشاء ملف الـ Workflow**:
   ```yaml
   name: Scheduled Task
   on:
     schedule:
       - cron: '0 12 * * *'  # كل يوم الساعة 12 ظهراً بتوقيت جرينتش
   jobs:
     task:
       runs-on: ubuntu-latest
       steps:
         - run: echo "Running scheduled task!"
   ```

2. **تفسير الـ `cron`**:
   - `0 12 * * *`: كل يوم في الساعة 12 ظهراً.
   - `0 8 * * 1`: كل يوم اثنين في الساعة 8 صباحاً.
   - `*/30 * * * *`: كل 30 دقيقة.

3. **استخدامات**:
   - عمل **backup** للبيانات.
   - إرسال **تقارير** دورية.
   - فحص **الويب سايت** إذا كان شغال.

---

## **3. المانيوال تريجرز (Manual Triggers)**
### **مثال: تشغيل الـ Workflow يدوياً**
1. **إنشاء ملف الـ Workflow**:
   ```yaml
   name: Manual Deploy
   on:
     workflow_dispatch:
       inputs:
         environment:
           description: 'Choose environment'
           required: true
           default: 'staging'
           type: choice
           options:
             - staging
             - production
   jobs:
     deploy:
       runs-on: ubuntu-latest
       steps:
         - run: echo "Deploying to ${{ github.event.inputs.environment }}"
   ```

2. **تشغيل الـ Workflow**:
   - من خلال **GitHub UI**:
     - ادخل على **Actions** → اختر الـ **Workflow** → اضغط **Run workflow**.
     - اختر **environment** (staging أو production).

   - من خلال **GitHub CLI**:
     ```bash
     gh workflow run manual.yml -f environment=production
     ```

---

## **4. استخدام الـ GitHub CLI**
1. **تثبيت الـ CLI**:
   - حمل الـ **GitHub CLI** من [هنا](https://cli.github.com/).
   - ثبت البرنامج على جهازك.

2. **تشغيل الـ Workflow**:
   ```bash
   gh auth login  # تسجيل الدخول
   gh workflow run manual.yml -f environment=production
   ```

---

## **5. ملخص النقاط الرئيسية**


| النوع | الاستخدام | مثال |
|-------|------------|-------|
| **Webhook** | تشغيل عند **push** أو **pull request** | `on: [push, pull_request]` |
| **Schedule** | تشغيل في وقت معين | `on: schedule: - cron: '0 12 * * *'` |
| **Manual** | تشغيل يدوياً | `on: workflow_dispatch` |

---

**سؤال مهم:** عايز نطبق مثال معين؟ ولا في جزء محتاج توضيح أكتر؟ 🤔
*(قول لي، وانا هاشرحه زي ما تكون بتشرح لاصدقائك على الكوشة!)* ☕😃

**اهلا يا اسطورة!** 👋 اليوم هنتكلم عن **GitHub Actions** بطريقة سهلة ومسلية، زي ما بنشرب شاي ونضحك! ☕😄

---

## **1. تشغيل الـ Workflow يدوياً (Manual Triggers)**

### **تشغيل الـ Workflow باستخدام GitHub UI**
1. **إنشاء ملف الـ Workflow**:
   - ملف اسمه `manual.yml` داخل `.github/workflows/`:
     ```yaml
     name: Manual Deploy
     on:
       workflow_dispatch:
         inputs:
           environment:
             description: 'Choose environment'
             required: true
             default: 'staging'
             type: choice
             options:
               - staging
               - production
     jobs:
       deploy:
         runs-on: ubuntu-latest
         steps:
           - run: echo "Deploying to ${{ github.event.inputs.environment }}"
     ```

2. **تشغيل الـ Workflow**:
   - ادخل على **Actions** في الريبوزيتوري.
   - اختر الـ **Workflow** (`Manual Deploy`).
   - اضغط **Run workflow**.
   - اختر **environment** (staging أو production).

---

## **2. تشغيل الـ Workflow باستخدام GitHub CLI**
1. **تثبيت الـ CLI**:
   - حمل **GitHub CLI** من [هنا](https://cli.github.com/).
   - ثبت البرنامج على جهازك.

2. **تشغيل الـ Workflow**:
   ```bash
   gh auth login  # تسجيل الدخول
   gh workflow run manual.yml -f environment=production
   ```

---

## **3. تشغيل الـ Workflow باستخدام API Call**
1. **إنشاء Personal Access Token**:
   - ادخل على **Settings** في حسابك على GitHub.
   - اختر **Developer settings** → **Personal access tokens**.
   - انشئ **token** جديد مع صلاحيات `repo` و `workflow`.

2. **إرسال طلب API**:
   ```bash
   curl -X POST \
   -H "Authorization: token YOUR_TOKEN" \
   -H "Accept: application/vnd.github.v3+json" \
   https://api.github.com/repos/OWNER/REPO/actions/workflows/WORKFLOW_ID/dispatches \
   -d '{"ref":"main","inputs":{"environment":"production"}}'
   ```

---

## **4. استخدام الـ Matrix Strategy**
### **مثال: تشغيل الاختبارات على عدة إصدارات من Node.js ونظم تشغيل مختلفة**
1. **إنشاء ملف الـ Workflow**:
   ```yaml
   name: Node.js CI
   on: [push]
   jobs:
     test:
       runs-on: ${{ matrix.os }}
       strategy:
         matrix:
           os: [ubuntu-latest, windows-latest, macos-latest]
           node-version: [14.x, 16.x, 18.x]
       steps:
         - uses: actions/checkout@v4
         - uses: actions/setup-node@v4
           with:
             node-version: ${{ matrix.node-version }}
         - run: npm install
         - run: npm test
   ```

2. **تفسير الـ Matrix**:
   - الـ **Matrix** بيشغل الـ **job** على كل تولفة من **os** و **node-version**.
   - يعني هتشتغل 9 مرات (3 أنظمة تشغيل × 3 إصدارات من Node.js).

---

## **5. استخدام الـ Conditions في الـ Steps**
### **مثال: تشغيل خطوة معينة فقط إذا كان الحدث هو `push`**
1. **إنشاء ملف الـ Workflow**:
   ```yaml
   name: Conditional Step
   on: [push, pull_request]
   jobs:
     test:
       runs-on: ubuntu-latest
       steps:
         - if: github.event_name == 'push'
           run: echo "This step runs only on push events"
         - run: echo "This step runs on all events"
   ```

2. **تفسير الـ Condition**:
   - الخطوة الأولى هتشتغل فقط إذا كان الحدث هو `push`.
   - الخطوة الثانية هتشتغل في جميع الأحداث.

---

## **6. استخدام الـ Functions في الـ Expressions**
### **مثال: استخدام الـ `contains` و `startsWith`**
1. **إنشاء ملف الـ Workflow**:
   ```yaml
   name: Functions Example
   on: [push]
   jobs:
     test:
       runs-on: ubuntu-latest
       steps:
         - if: contains(github.event.commit.message, 'fix')
           run: echo "This commit contains the word 'fix'"
         - if: startsWith(github.event.ref, 'refs/tags/')
           run: echo "This is a tag push"
   ```

2. **تفسير الـ Functions**:
   - `contains`: بيفحص إذا كانت الرسالة تحتوي على كلمة معينة.
   - `startsWith`: بيفحص إذا كان الرفرنس يبدا بكلمة معينة.

---

## **7. استخدام الـ Secrets**
### **مثال: استخدام الـ `secrets` في الـ Workflow**
1. **إنشاء الـ Secret**:
   - ادخل على **Settings** في الريبوزيتوري.
   - اختر **Secrets** → **Actions**.
   - انشئ **secret** جديد اسمه `API_KEY` وقيمته `your_api_key_here`.

2. **استخدام الـ Secret**:
   ```yaml
   name: Secrets Example
   on: [push]
   jobs:
     test:
       runs-on: ubuntu-latest
       steps:
         - run: echo "The API key is ${{ secrets.API_KEY }}"
   ```

---

## **8. استخدام الـ Docker Containers**
### **مثال: تشغيل الـ Workflow داخل الـ Docker Container**
1. **إنشاء ملف الـ Workflow**:
   ```yaml
   name: Docker Example
   on: [push]
   jobs:
     test:
       runs-on: ubuntu-latest
       container: node:18
       steps:
         - run: node --version
   ```

2. **تفسير الـ Container**:
   - الـ **job** هيتشغل داخل **Docker container** باستخدام صورة `node:18`.

---

## **9. استخدام الـ Services**
### **مثال: تشغيل قاعدة بيانات Redis داخل الـ Workflow**
1. **إنشاء ملف الـ Workflow**:
   ```yaml
   name: Services Example
   on: [push]
   jobs:
     test:
       runs-on: ubuntu-latest
       services:
         redis:
           image: redis
           ports:
             - 6379:6379
       steps:
         - run: redis-cli ping
   ```

2. **تفسير الـ Service**:
   - الـ **job** هيتصل بقاعدة بيانات **Redis** أثناء التشغيل.

---

## **10. ملخص النقاط الرئيسية**


| النقطة | الشرح |
|--------|-------|
| **Manual Triggers** | تشغيل الـ Workflow يدوياً باستخدام GitHub UI أو CLI أو API. |
| **Matrix Strategy** | تشغيل الـ Workflow على عدة تولفات من المتغيرات. |
| **Conditions** | تشغيل خطوات معينة بناءً على شروط. |
| **Functions** | استخدام دوال مثل `contains` و `startsWith`. |
| **Secrets** | استخدام البيانات الحساسة بشكل آمن. |
| **Docker Containers** | تشغيل الـ Workflow داخل حاويات Docker. |
| **Services** | تشغيل خدمات إضافية مثل قواعد البيانات. |

---

**سؤال مهم:** عايز نطبق مثال معين؟ ولا في جزء محتاج توضيح أكتر؟ 🤔
*(قول لي، وانا هاشرحه زي ما تكون بتشرح لاصدقائك على الكوشة!)* ☕😃


**اهلا يا اسطورة!** 👋 اليوم هنتكلم عن **GitHub Actions** بطريقة سهلة ومسلية، زي ما بنشرب شاي ونضحك! ☕😄

---

## **1. استخدام الـ Workflow Commands**

### **أمر `warning` و `error`**
- **أمر `warning`**: يستخدم لإظهار تحذير في سجلات الـ Workflow.
  ```yaml
  - name: Show warning
    run: echo "::warning::Deprecated function found!"
  ```

- **أمر `error`**: يستخدم لإظهار خطأ في سجلات الـ Workflow.
  ```yaml
  - name: Show error
    run: echo "::error::Missing required file!"
  ```

### **مثال عملي**
```yaml
name: Workflow Commands Example
on: [push]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Check for deprecated function
        run: |
          echo "::warning::Deprecated function 'oldFunction' found!"
          echo "::error::Missing 'README.md' file!"
```

---

## **2. استخدام الـ Environment Variables**

### **مشاركة المتغيرات بين الخطوات**
- يمكن مشاركة المتغيرات بين الخطوات باستخدام `GITHUB_ENV`.
- مثال:
  ```yaml
  - name: Set environment variable
    run: echo "API_KEY=12345" >> $GITHUB_ENV

  - name: Use environment variable
    run: echo "The API key is ${{ env.API_KEY }}"
  ```

---

## **3. استخدام الـ Masking**

### **إخفاء المعلومات الحساسة**
- يمكن إخفاء المعلومات الحساسة مثل `API keys` باستخدام الأمر `::add-mask::`.
- مثال:
  ```yaml
  - name: Mask sensitive data
    run: echo "::add-mask::12345"
  ```

### **مثال عملي**
```yaml
name: Masking Example
on: [push]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Set and mask API key
        run: |
          echo "API_KEY=12345" >> $GITHUB_ENV
          echo "::add-mask::$API_KEY"
      - name: Use masked API key
        run: echo "The masked API key is ${{ env.API_KEY }}"
```

---

## **4. استخدام الـ Debug Messages**

### **إظهار رسائل تصحيح الأخطاء**
- يمكن استخدام الأمر `::debug::` لإظهار رسائل تصحيح الأخطاء.
- مثال:
  ```yaml
  - name: Debug message
    run: echo "::debug::This is a debug message!"
  ```

---

## **5. استخدام الـ Grouping**

### **تجميع الخطوات**
- يمكن تجميع الخطوات باستخدام الأمر `::group::` و `::endgroup::`.
- مثال:
  ```yaml
  - name: Grouped steps
    run: |
      echo "::group::Installing dependencies"
      npm install
      echo "::endgroup::"
  ```

---

## **6. استخدام الـ File Commands**

### **إخفاء محتويات الملفات الحساسة**
- يمكن إخفاء محتويات الملفات الحساسة باستخدام الأمر `::add-mask::` مع قراءة الملف.
- مثال:
  ```yaml
  - name: Mask file contents
    run: |
      API_KEY=$(cat api_key.txt)
      echo "::add-mask::$API_KEY"
  ```

---

## **7. ملخص النقاط الرئيسية**


| الأمر | الاستخدام | مثال |
|-------|------------|-------|
| `::warning::` | إظهار تحذير | `echo "::warning::Deprecated function found!"` |
| `::error::` | إظهار خطأ | `echo "::error::Missing required file!"` |
| `GITHUB_ENV` | مشاركة المتغيرات | `echo "API_KEY=12345" >> $GITHUB_ENV` |
| `::add-mask::` | إخفاء المعلومات الحساسة | `echo "::add-mask::12345"` |
| `::debug::` | إظهار رسائل تصحيح الأخطاء | `echo "::debug::This is a debug message!"` |
| `::group::` و `::endgroup::` | تجميع الخطوات | `echo "::group::Installing dependencies"` |

---

**سؤال مهم:** عايز نطبق مثال معين؟ ولا في جزء محتاج توضيح أكتر؟ 🤔
*(قول لي، وانا هاشرحه زي ما تكون بتشرح لاصدقائك على الكوشة!)* ☕😃
