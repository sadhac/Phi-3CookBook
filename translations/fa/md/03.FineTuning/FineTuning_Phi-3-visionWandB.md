<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "e0a07fd2a30fe2af30b1373df207a5bf",
  "translation_date": "2025-03-27T15:04:52+00:00",
  "source_file": "md\\03.FineTuning\\FineTuning_Phi-3-visionWandB.md",
  "language_code": "fa"
}
-->
# نمای کلی پروژه Phi-3-Vision-128K-Instruct

## مدل

مدل Phi-3-Vision-128K-Instruct، یک مدل چندوجهی سبک و پیشرفته، هسته اصلی این پروژه است. این مدل بخشی از خانواده مدل‌های Phi-3 بوده و از طول زمینه‌ای تا 128,000 توکن پشتیبانی می‌کند. این مدل بر روی مجموعه داده‌های متنوعی که شامل داده‌های مصنوعی و وب‌سایت‌های عمومی با کیفیت بالا و محتوای مبتنی بر استدلال هستند، آموزش دیده است. فرآیند آموزش شامل تنظیم دقیق تحت نظارت و بهینه‌سازی مستقیم ترجیحات برای تضمین پیروی دقیق از دستورالعمل‌ها و همچنین تدابیر ایمنی قدرتمند بوده است.

## ایجاد داده نمونه به دلایل مختلف بسیار مهم است:

1. **آزمایش**: داده‌های نمونه به شما امکان می‌دهد برنامه خود را تحت شرایط مختلف آزمایش کنید بدون اینکه داده‌های واقعی تحت تأثیر قرار گیرند. این موضوع به‌ویژه در مراحل توسعه و آزمایش اهمیت دارد.

2. **تنظیم عملکرد**: با داده‌های نمونه‌ای که مقیاس و پیچیدگی داده‌های واقعی را شبیه‌سازی می‌کنند، می‌توانید نقاط ضعف عملکرد را شناسایی کرده و برنامه خود را بهینه کنید.

3. **نمونه‌سازی اولیه**: داده‌های نمونه می‌توانند برای ایجاد نمونه‌های اولیه و ماکاپ‌ها استفاده شوند که به درک نیازهای کاربران و دریافت بازخورد کمک می‌کند.

4. **تحلیل داده**: در علم داده، داده‌های نمونه اغلب برای تحلیل اکتشافی داده‌ها، آموزش مدل‌ها و آزمایش الگوریتم‌ها استفاده می‌شود.

5. **امنیت**: استفاده از داده‌های نمونه در محیط‌های توسعه و آزمایش می‌تواند به جلوگیری از نشت تصادفی داده‌های حساس واقعی کمک کند.

6. **یادگیری**: اگر در حال یادگیری فناوری یا ابزار جدیدی هستید، کار با داده‌های نمونه می‌تواند راهی عملی برای اعمال آنچه یاد گرفته‌اید فراهم کند.

به یاد داشته باشید که کیفیت داده‌های نمونه شما می‌تواند تأثیر قابل توجهی بر این فعالیت‌ها داشته باشد. داده‌ها باید از نظر ساختار و تنوع تا حد ممکن به داده‌های واقعی نزدیک باشند.

### ایجاد داده نمونه
[اسکریپت ایجاد مجموعه داده](./CreatingSampleData.md)

## مجموعه داده

یک مثال خوب از مجموعه داده نمونه، [DBQ/Burberry.Product.prices.United.States dataset](https://huggingface.co/datasets/DBQ/Burberry.Product.prices.United.States) (موجود در Huggingface) است. مجموعه داده نمونه محصولات Burberry به همراه اطلاعات فراداده‌ای در مورد دسته‌بندی محصول، قیمت و عنوان با مجموع 3,040 ردیف، که هرکدام نمایانگر یک محصول منحصر به فرد است. این مجموعه داده به ما امکان می‌دهد توانایی مدل را در درک و تفسیر داده‌های بصری آزمایش کنیم، و متن‌های توصیفی تولید کنیم که جزئیات بصری پیچیده و ویژگی‌های خاص برند را به تصویر می‌کشند.

**توجه:** می‌توانید از هر مجموعه داده‌ای که شامل تصاویر است استفاده کنید.

## استدلال پیچیده

مدل باید بتواند فقط با استفاده از تصویر درباره قیمت‌ها و نام‌گذاری‌ها استدلال کند. این نیازمند آن است که مدل نه تنها ویژگی‌های بصری را شناسایی کند بلکه پیامدهای آن‌ها را از نظر ارزش محصول و برند درک کند. با تولید توصیفات متنی دقیق از تصاویر، این پروژه پتانسیل ادغام داده‌های بصری برای بهبود عملکرد و تنوع مدل‌ها در کاربردهای دنیای واقعی را برجسته می‌کند.

## معماری Phi-3 Vision

معماری این مدل نسخه چندوجهی Phi-3 است. این مدل هم داده‌های متنی و هم تصویری را پردازش می‌کند و این ورودی‌ها را برای انجام وظایف جامع درک و تولید به یک توالی یکپارچه تبدیل می‌کند. مدل از لایه‌های جاسازی جداگانه برای متن و تصاویر استفاده می‌کند. توکن‌های متنی به بردارهای متراکم تبدیل می‌شوند، در حالی که تصاویر از طریق مدل CLIP Vision پردازش شده و جاسازی ویژگی‌ها استخراج می‌شوند. این جاسازی‌های تصویری سپس به ابعاد جاسازی‌های متنی تبدیل می‌شوند تا یکپارچگی کامل آن‌ها تضمین شود.

## ادغام جاسازی‌های متن و تصویر

توکن‌های ویژه‌ای در توالی متن مشخص می‌کنند که جاسازی‌های تصویری در کجا باید وارد شوند. در حین پردازش، این توکن‌های ویژه با جاسازی‌های تصویری مربوطه جایگزین می‌شوند و به مدل امکان می‌دهند که متن و تصاویر را به‌عنوان یک توالی واحد مدیریت کند. قالب درخواست برای مجموعه داده ما با استفاده از توکن ویژه <|image|> به صورت زیر تنظیم شده است:

```python
text = f"<|user|>\n<|image_1|>What is shown in this image?<|end|><|assistant|>\nProduct: {row['title']}, Category: {row['category3_code']}, Full Price: {row['full_price']}<|end|>"
```

## نمونه کد
- [اسکریپت آموزش Phi-3-Vision](../../../../code/03.Finetuning/Phi-3-vision-Trainingscript.py)
- [راهنمای مثال Weights and Bias](https://wandb.ai/byyoung3/mlnews3/reports/How-to-fine-tune-Phi-3-vision-on-a-custom-dataset--Vmlldzo4MTEzMTg3)

**سلب مسئولیت**:  
این سند با استفاده از سرویس ترجمه هوش مصنوعی [Co-op Translator](https://github.com/Azure/co-op-translator) ترجمه شده است. در حالی که تلاش ما بر دقت است، لطفاً توجه داشته باشید که ترجمه‌های خودکار ممکن است شامل خطاها یا نارسایی‌هایی باشند. سند اصلی به زبان مادری آن باید به عنوان منبع معتبر در نظر گرفته شود. برای اطلاعات حیاتی، ترجمه حرفه‌ای انسانی توصیه می‌شود. ما مسئولیتی در قبال سوء تفاهم‌ها یا تفسیرهای نادرست ناشی از استفاده از این ترجمه نداریم.