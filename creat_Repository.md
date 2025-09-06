

## المقدمة 🎯

النهارده هنتعلم مع بعض أول خطوة فعلية علشان نبدأ شغلنا مع **GitHub Actions** وهي إننا نعمل **Repository** من الصفر ونربطه بجهازنا أو بيئة العمل اللي بنشتغل عليها، ونتأكد إننا مجهزين كل حاجة صح (Git، SSH، الملفات الأساسية) علشان أي أكشن هنضيفه بعد كده يشتغل بدون مشاكل.

ليه ده مهم؟ 🤔

* عشان أي مشروع على GitHub لازم يبقى ليه ريبو منظم وواضح
* عشان نقدر نستخدم الـ Actions في CICD، لازم يكون فيه كود مرفوع ومربوط صح
* عشان من أول يوم ما نضيعش وقتنا في أخطاء الإعدادات

---

## الشرح خطوة بخطوة 🛠

### 1. إنشاء Repository على GitHub

* روح على GitHub → New Repository
* الاسم: `github-actions-course`
* الوصف: جملة بسيطة توضح المحتوى، حتى لو placeholder، ممكن تعدلها بعدين
* النوع: **Public** (علشان الكل يقدر يشوفه)
* اضغط **Create Repository**

💡 ملاحظة: ممكن الشاشة اللي هتطلعلك تختلف حسب وقت المشاهدة، المهم تتأكد إنك محدد **SSH** في Quick Setup.

---

### 2. ربط الريبو بالـ IDE (أو بيئتك المحلية)

* خد أوامر **Push an existing repository from the command line** من الصفحة
* في IDE أو Terminal:

  ```bash
  git init
  git branch -M main
  ```
* لو زهقت من رسالة التحذير الصفراء الخاصة بالـ branch الافتراضي، ممكن تعمل إعداد عام:

  ```bash
  git config --global init.defaultBranch main
  ```

---

### 3. إنشاء الملفات الأساسية 📂

* `README.md` → اكتب فيه وصف بسيط للمشروع
* `.gitignore` → حط فيه `node_modules/` علشان تتجاهل فولدرات الـ npm بعدين

---

### 4. أول Commit

```bash
git add .
git commit -m "First commit"
```

---

### 5. حل مشكلة Author identity (لو ظهرت) 🕵️‍♂️

لو Git قالك "Author identity unknown"، اعمل إعداد عام:

```bash
git config --global user.name "اسمك"
git config --global user.email "بريدك"
```

في بعض البيئات هيطلب منك تدخل على محرر نصوص وتضغط:

* `I` للدخول في وضع الكتابة
* بعد التعديل: `Esc` → `:wq` → Enter

---

### 6. ربط الريبو بالـ Remote ودفع الكود 🚀

```bash
git remote add origin git@github.com:username/github-actions-course.git
git push -u origin main
```

أول مرة هتحتاج تكتب:

```bash
yes
```

علشان تثق في github.com.

---

### 7. إعداد SSH لو مفيش صلاحيات Push 🔑

1. على GitHub: Profile → Settings → SSH and GPG Keys → New SSH Key
2. العنوان: أي اسم وصفي (مثلاً: Udemy Profile)
3. في جهازك:

   ```bash
   ssh-keygen -t ed25519 -C "بريدك"
   ```

   دوس Enter لكل الأسئلة (ممكن تسيب الـ passphrase فاضي)
4. انسخ محتوى الملف `.pub`

   ```bash
   cat ~/.ssh/اسم_المفتاح.pub
   ```

   وحطه في خانة Key على GitHub
5. فعل الـ SSH Agent:

   ```bash
   ssh-add ~/.ssh/اسم_المفتاح
   ```
أها! المشكلة واضحة. انت حاولت تسجل المفتاح في مسار `/users/ec2-user/.ssh/zain-key` لكن **هذا المسار غير موجود** على جهازك.

السبب: المسار الصحيح هو `/home/ec2-user/.ssh/` مش `/users/ec2-user/.ssh/`.

---

### الحل الصحيح:

#### 1. أولاً: اروح للمسار الصحيح لليوزر ec2-user
```bash
cd /home/ec2-user/
```

#### 2. ثانياً: تأكد من وجود فولدر `.ssh` أو اعمله لو مش موجود
```bash
mkdir -p .ssh
```

#### 3. ثالثاً: اعمل المفتاح في المكان الصحيح
```bash
ssh-keygen -t ed25519 -f /home/ec2-user/.ssh/zain-key
```

الـ `-f` هنا علشان تحدد المسار الصحيح مباشرة.

#### 4. رابعاً: غير ملكية الملفات لليوزر ec2-user (مهم جداً)
```bash
chown -R ec2-user:ec2-user /home/ec2-user/.ssh/
```
(ده لأنك عملت الملفات كـ `root` فمحتاجين تخليهم ملك لـ `ec2-user`)

#### 5. أخيراً: جرب تشوف المفاتيح اتعملت
```bash
ls -la /home/ec2-user/.ssh/
```

---

### لو عاوز تعمل المفتاح وأنت داخل كـ ec2-user مباشرة:

1. **ارجع لليوزر ec2-user:**
   ```bash
   exit
   ```

2. **اعمل المفتاح:**
   ```bash
   ssh-keygen -t ed25519 -f ~/.ssh/zain-key
   ```

3. **شوف المفاتيح:**
   ```bash
   ls -la ~/.ssh/
   ```

كده هتشتغل بشكل صحيح بدون أي أخطاء! ✅
---

### 8. التحقق من الربط ✅

بعد الخطوات دي:

* اعمل `git push` تاني
* هتلاقي الملفات ظهرت على GitHub في الريبو اللي أنشأته

---

## الملخص 📝

* أنشأنا ريبو جديد على GitHub
* أضفنا ملفات أساسية: `README.md` و `.gitignore`
* عملنا أول Commit
* ربطنا الريبو بجهازنا باستخدام SSH
* جهزنا صلاحيات الـ Push

---

## تمارين عملية 💪

1. جرب تعمل Repository جديد بنفس الخطوات لكن اسمه مختلف
2. ضيف ملف جديد (مثلاً `test.txt`) واعمل Commit وPush
3. جرب تمسح مفتاح SSH من GitHub وشوف إيه اللي هيحصل لما تعمل Push
4. جرب تغير الوصف في README واعمله Update على GitHub

---

لو تحب، أقدر أعملك **جدول أو Flowchart بصري** يوضح خطوات إنشاء وربط الريبو بالـ SSH خطوة خطوة، بحيث تبقى مرجع بصري ليك وانت بتشتغل.
تحب أعملهولك دلوقتي؟
