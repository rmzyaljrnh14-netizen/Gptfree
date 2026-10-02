# Gptfree

تشغيل **نماذج مفتوحة المصدر كبيرة** على سيرفرات GPU المجانية، بلا عتاد خاص.

هذا المستودع يحتوي على دفاتر جاهزة (Jupyter Notebooks) تُشغّل نماذج بحجم 14B–32B
على بطاقات Google/Kaggle المجانية، وتُتيح لك استخدامها من جهازك عبر رابط عام.

## 📓 الدفاتر

| الدفتر | المنصة | العتاد المجاني | النموذج الافتراضي |
| --- | --- | --- | --- |
| `run_open_llm_kaggle.ipynb` | Kaggle (تملكها Google) | **2× NVIDIA T4 = 32GB** | `qwen3:32b` |
| `run_open_llm_colab.ipynb` | Google Colab | 1× NVIDIA T4 = 16GB | `qwen3:14b` |

## ⚡ التشغيل في 3 خطوات

1. **افتح الدفتر:**
   - Kaggle: ارفع `run_open_llm_kaggle.ipynb` كـ Notebook جديد.
   - Colab: `File → Upload notebook`.
2. **اضبط الإعدادات:**
   - Kaggle: من **Settings** → **Accelerator: GPU T4 x2**، و**Internet: On**.
   - Colab: **Runtime → Change runtime type → T4 GPU**.
3. **اضغط Run All** وانتظر حتى يظهر الرابط العام.

> Kaggle يطلب **تحققاً برقم الهاتف** مرة واحدة قبل إتاحة GPU.

## 🧠 النماذج المتاحة (بدّل المتغيّر `MODEL`)

| النموذج | الحجم التقريبي | الرخصة | ملاحظة |
| --- | --- | --- | --- |
| `qwen3:32b` | ~20GB | Apache-2.0 | الأقوى على بطاقتَي Kaggle |
| `qwen3:30b-a3b` | ~19GB | Apache-2.0 | MoE أخف وأسرع |
| `qwen3:14b` | ~9GB | Apache-2.0 | الأفضل على Colab |
| `gemma3:27b` | ~17GB | Gemma | بديل قوي |
| `gpt-oss:20b` | ~13GB | **Apache-2.0** | من OpenAI، يعمل على 16GB |
| `deepseek-r1:32b` | ~20GB | MIT | نماذج استدلال |

الأسماء من مكتبة [Ollama](https://ollama.com/library) — يمكنك استبدالها بأي نموذج مفتوح آخر.

## 🌍 الوصول من جهازك

الخلية الأخيرة تنشئ **نفق Cloudflare** مجانياً، فتحصل على:

- `https://xxxx.trycloudflare.com` → واجهة Ollama
- `https://xxxx.trycloudflare.com/v1` → نقطة **متوافقة مع OpenAI**

يمكنك استخدام الرابط مع أي عميل يدعم OpenAI API:

```bash
curl https://xxxx.trycloudflare.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{"model":"qwen3:32b","messages":[{"role":"user","content":"مرحبا"}]}'
```

> ⚠️ **تنبيه أمني:** الرابط العام **مؤقت وغير محمي** — يتغيّر مع كل جلسة، ولا يطلب مصادقة.
> لا تشاركه ولا ترسل عبره أي بيانات حساسة. أوقف الجلسة عند الانتهاء.

## 📊 مقارنة عروض GPU المجانية (أكتوبر 2026)

| المنصة | العتاد | الحد | بطاقة ائتمان؟ |
| --- | --- | --- | --- |
| **Kaggle** ⭐ | 2× T4 (32GB) | 30 ساعة/أسبوع، جلسة 12 ساعة | لا (تحقق هاتفي) |
| **Google Colab** | 1× T4 (16GB) | جلسة 12 ساعة | لا |
| **HF Spaces (ZeroGPU)** | A100 (مشترك) | حسب التوفر | لا |
| **Cerebras** | Llama 70B عبر API | تجربة 30 يوم | نعم |
| **Groq** | API لنماذج مفتوحة | 1000 طلب/يوم | لا |

## ⚠️ حدود يجب معرفتها

- **16GB** في Colab تكفي لنموذج 14B مكمَّم. النماذج الأكبر تحتاج بطاقتَي Kaggle.
- السرعة المتوقعة: 8B ≈ 30 كلمة/ث، 14B ≈ 14 كلمة/ث، 32B ≈ 9 كلمة/ث.
- الجلسة تُوقف بعد خمول ~60 دقيقة (Kaggle).
- الحصة الأسبوعية (30 ساعة) مشتركة بين كل جلساتك.

## 📄 الرخصة

الكود في هذا المستودع متاح تحت رخصة MIT. أما النماذج المُشغَّلة فلكلٍّ رخصته الخاصة
(راجع صفحة النموذج على Ollama أو Hugging Face).