# AI Design Skills

نسخة من مهارات التصميم الثلاث لـ Elaya: [elayadesign/ai-design-skills](https://github.com/elayadesign/ai-design-skills) و [elayadesign/redesign-skill](https://github.com/elayadesign/redesign-skill) (رخصة MIT)، ومهارة `unslop` لـ Damir Sokolovsky: [heydamir/unslop](https://github.com/heydamir/unslop) (رخصة CC BY 4.0)، مجهزة للتثبيت كـ Plugin في Claude Code وللرفع في claude.ai.

| المهارة | وظيفتها |
|---|---|
| [`landing-page-design`](./skills/landing-page-design/SKILL.md) | بناء صفحة هبوط من الصفر: أسئلة البداية، هيكل الصفحة، كتابة النصوص للتحويل، ونظام بصري صارم (الخطوط، المسافات، الزوايا، الحركة) |
| [`design-to-motion`](./skills/design-to-motion/SKILL.md) | تحويل تصميم ثابت (Figma أو لقطة) إلى نسخة HTML مطابقة تتحرك: تبدأ فارغة ثم تتعبأ، وكل عنصر يمثّل وظيفته في حلقة متكررة، مع تصدير MP4 لـ X و GIF للموقع و GIF بمقاس 800×500 |
| [`redesign-existing-projects`](./skills/redesign-existing-projects/SKILL.md) | فحص موقع أو تطبيق موجود: يكشف أنماط التصميم المكررة والحالات الناقصة والكود الضعيف، يعرض التشخيص أولًا، ثم يصلح داخل نفس التقنية بدون إعادة بناء |
| [`unslop`](./skills/unslop/SKILL.md) | تحويل واجهة «شكلها مولّد بالذكاء الاصطناعي» إلى واجهة لها شخصية: يفحص العلامات المعروفة (تدرجات بنفسجية، توهج، إيموجي، مسافات غير منتظمة)، ثم يصلح المسافات والألوان والأيقونات والنصوص والخطوط والتخطيط والحركة بالترتيب، ويقدر يصوّر موقعًا مباشرًا أو يصدّر فيديو قبل/بعد |

المصدر: `ai-design-skills` عند الإيداع `38bbe57` (25 أكتوبر 2026)، و `redesign-skill` عند الإيداع `64627f6` (20 يوليو 2026)، و `unslop` عند الإيداع `4652254` (29 أكتوبر 2026). النصوص منقولة كما هي بدون تعديل.

---

## التثبيت

### 1) Claude Code على جهازك (كل المشاريع)
داخل Claude Code:
```
/plugin marketplace add navcoaching/ai-design-skills
/plugin install ai-design-skills@navcoaching-skills
```
أو من الطرفية:
```bash
claude plugin marketplace add navcoaching/ai-design-skills
claude plugin install ai-design-skills@navcoaching-skills
```

### 2) Claude Code على الويب (كل الجلسات السحابية)
جلسات الويب تبدأ في حاوية جديدة كل مرة، فأضف هذا في **Setup script** للبيئة (قائمة البيئة في شريط عنوان الجلسة ← Edit):
```bash
git clone --depth 1 https://github.com/navcoaching/ai-design-skills /tmp/ai-design-skills
mkdir -p ~/.claude/skills
cp -r /tmp/ai-design-skills/skills/* ~/.claude/skills/
```

### 3) مشروع واحد فقط
```bash
mkdir -p .claude/skills
cp -r skills/* .claude/skills/
```

### 4) claude.ai (المحادثات العادية)
نزّل ملف المهارة من مجلد [`dist/`](./dist) ثم ارفعه من **Settings ← Capabilities** (قسم Skills):
- [`landing-page-design.zip`](./dist/landing-page-design.zip)
- [`design-to-motion.zip`](./dist/design-to-motion.zip)
- [`redesign-existing-projects.zip`](./dist/redesign-existing-projects.zip)
- [`unslop.zip`](./dist/unslop.zip)

---

## قبل الاستخدام

- **`landing-page-design` واسعة جدًا:** وصفها يطلب تفعيلها مع أي واجهة ويب، حتى لو ما ذكرت التصميم. قواعدها تفرض خطوطًا لاتينية فقط (Geist و Manrope و Poppins) وتشترط خلفيات مسطحة بلا تدرج، وتلزم بمقاسات Tailwind ومسافات محددة. هذا قد يتعارض مع الهويات العربية (Alexandria و IBM Plex Sans Arabic وخلفية الشبكة). المهارة نفسها تقول إن طلبك الصريح يتقدّم عليها، فاذكر هويتك في الطلب أو في `CLAUDE.md` المشروع.
- **`redesign-existing-projects`** تستبدل الخطوط والألوان والأيقونات بقيم قسم «Design values» في آخر ملفها (نفس قيم `landing-page-design`)، فنفس التحذير ينطبق: لا تشغّلها على مشروع بهوية عربية قبل ما تعدّل ذلك القسم أو تذكر هويتك. ميزتها أنها تعرض التشخيص وتنتظر موافقتك قبل التعديل.
- **`design-to-motion`** تحتاج رمز Figma API (يُقرأ من متغير بيئة، ولا يُكتب في المحادثة) و `ffmpeg` و Playwright للتصدير.
- المهارات الثلاث الأولى نصوص Markdown فقط: لا سكربتات ولا روابط تنفيذ ولا طلبات شبكة.
- **`unslop`** تختلف: فيها سكربتان Node (`scripts/snapshot.mjs` يحفظ نسخة من موقع مباشر مع لقطة شاشة، و `scripts/story.mjs` يصدّر فيديو MP4 بخادم محلي على `127.0.0.1` و ffmpeg). يحتاجان Playwright، ولا يرسلان بيانات لأي جهة خارجية (فُحصا قبل النسخ). وفيها صور مرجعية (~1.4MB). قواعدها لاتينية الطابع أيضًا، فاذكر هويتك العربية في الطلب.

## الرخصة
MIT. حقوق المهارات الثلاث © 2026 Elaya ([LICENSE](./LICENSE)). مهارة `design-to-motion` تقتبس قواعد عامة من مستودعات MIT مذكورة في آخر ملفها.

مهارة `unslop` من إنشاء Damir Sokolovsky ([@heydamir](https://x.com/heydamir))، برخصة CC BY 4.0 ([skills/unslop/LICENSE](./skills/unslop/LICENSE))، منقولة بدون تعديل. الرخصة تشترط إبقاء هذا النسب في أي نسخة.
