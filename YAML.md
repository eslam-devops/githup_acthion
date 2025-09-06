تمام يا إسلام
هعملك المحاضرة دي كشرح حي كأننا قاعدين مع بعض، باللهجة المصرية، مع شوية أمثلة واقعية وإيموجي عشان يثبت في دماغك

---

## المقدمة 🎯

قبل ما نبدأ نكتب أي **GitHub Actions workflow**، لازم نفهم لغة الـ **YAML**
ليه؟
لأن GitHub Actions بيعتمد عليها في وصف كل حاجة: الـ Jobs، الـ Steps، الإعدادات، المتغيرات… إلخ

فلو مش فاهم YAML كويس، هتحس إن الأكواد غامضة أو مش مترتبة
النهاردة هنعرف الأساسيات اللي تكفينا عشان نكتب أي Workflow من غير ما نتوه

---

## الشرح خطوة بخطوة 🛠

### 1. يعني إيه YAML؟

* الاسم أصله **Yet Another Markup Language**
* هي لغة نصية (Text-based)
* فكرتها إنها **مبسطة** و**سهلة القراءة** للإنسان
* شكلها بيشبه القواميس أو الملفات الـ Config

---

### 2. أبسط شكل في YAML: Key → Value

زي قاموس:

```yaml
name: My workflow
```

* `name` → المفتاح (Key)
* `My workflow` → القيمة (Value)

---

### 3. القيم الأساسية في YAML (Primitive values)

عندنا 3 أنواع أساسية:

1. **String** (نص) → `"Hello"` أو بدون علامات اقتباس `Hello`

   * لو فيه رموز خاصة أو مسافات غريبة، حطها بين " " أو ' '
2. **Number** (رقم) → `10`، `25`، `1000`
3. **Boolean** (صح أو غلط) → `true` أو `false`

---

### 4. القواميس (Dictionaries / Objects) 📂

مفتاح بيحتوي على أكتر من مفتاح وقيمة داخله:

```yaml
config:
  path: first-directory/file.yaml
  environment: staging
```

* هنا `config` فيه جواه قاموس صغير فيه `path` و `environment`

📌 في GitHub Actions ده بيحصل كتير جدًا مع الحاجات زي:

```yaml
runs-on: ubuntu-latest
steps:
```

---

### 5. القوائم (Arrays / Lists) 📜

القائمة في YAML بتبدأ بـ `-` قبل كل عنصر:

```yaml
colors:
  - red
  - green
  - blue
```

ممكن تخلط بين الأنواع:

```yaml
items:
  - "text"
  - 25
  - true
```

---

### 6. قوائم من كائنات (Arrays of objects)

هنا كل عنصر في القائمة بيبقى كائن كامل:

```yaml
colors:
  - name: red
    hex: "#FF0000"
  - name: green
    hex: "#00FF00"
  - name: blue
    hex: "#0000FF"
```

---

### 7. التعشيش (Nesting)

ممكن تعمق أكتر:

```yaml
colors:
  - name: red
    hex: "#FF0000"
    labels:
      - experimental
      - accessibility
```

هنا `labels` نفسها قائمة جوا الكائن الأول

---

### 8. المسافات (Indentation) 🚨

* أهم حاجة في YAML
* مفيش `{}` أو `[]` زي JSON، كله بيعتمد على المسافات لتحديد الـ Parent/Child
* الأفضل تستخدم **مسافتين** لكل مستوى

✅ مثال صحيح:

```yaml
name: My workflow
environment: staging
```

❌ مثال غلط (هيكسر الملف):

```yaml
name: My workflow
  environment: staging
```

لأنك كده بتقول إن `environment` جوا `name` بس `name` أصلاً واخد قيمة نصية

---

### 9. الفكرة العامة في القراءة

لو عايز تفكر فيها، YAML زي خريطة شجرية:

```
config
  path
  environment
```

يعني كل مستوى بالمسافة بيمثل عمق أكتر

---

## الملخص 📝

* YAML = لغة بسيطة لتنظيم البيانات على شكل Key-Value
* القيم الأساسية: String, Number, Boolean
* عندك كمان Dictionaries (كائنات) و Arrays (قوائم)
* ممكن تعمل تعشيش (Nesting) بدون حدود
* المسافات (Indentation) هي اللي بتحدد العلاقات
* القوائم تبدأ بـ `-`

---

## تمارين عملية 💪

1. اكتب ملف YAML فيه:

   * اسم المشروع
   * الإعدادات (Config) فيها Path و Environment
   * قائمة ألوان فيها 3 ألوان، كل لون فيه اسم وكود HEX
2. جرب تخلي YAML يكسر (غلط في المسافات) وشوف رسالة الخطأ
3. اكتب قائمة فيها عناصر مختلفة الأنواع (String, Number, Boolean)

---

لو تحب، أقدر أعملك **Visual Cheat Sheet** لليـ YAML يوضح أشكال الـ Strings, Numbers, Lists, Dictionaries في صفحة واحدة تبقى مرجع سريع ليك وانت بتكتب Workflows
تحب أعملهولك دلوقتي؟
