# আপনার VS Code এক্সটেনশনে স্বাগতম

## ফোল্ডারে কী আছে

* এই ফোল্ডারটিতে আপনার এক্সটেনশনের জন্য প্রয়োজনীয় সমস্ত ফাইল রয়েছে।
* `package.json` - এটি ম্যানিফেস্ট ফাইল যেখানে আপনি আপনার এক্সটেনশন এবং কমান্ড ঘোষণা করেন।
  * উদাহরণস্বরূপ প্লাগিন একটি কমান্ড নিবন্ধন করে এবং তার শিরোনাম ও কমান্ডের নাম সংজ্ঞায়িত করে। এই তথ্যের সাহায্যে VS Code কমান্ড প্যালেটে কমান্ডটি প্রদর্শন করতে পারে। প্লাগিনটি এখনও লোড করার প্রয়োজন হয় না।
* `src/extension.ts` - এটি প্রধান ফাইল যেখানে আপনি আপনার কমান্ডের বাস্তবায়ন প্রদান করবেন।
  * ফাইলটি একটি ফাংশন `activate` এক্সপোর্ট করে, যা আপনার এক্সটেনশন প্রথমবার সক্রিয় হওয়ার সময় (এই ক্ষেত্রে কমান্ডটি চালানোর মাধ্যমে) ডাকা হয়। `activate` ফাংশনের ভিতরে আমরা `registerCommand` কল করি।
  * আমরা কমান্ডের বাস্তবায়ন থাকা ফাংশনটি `registerCommand`-এর দ্বিতীয় প্যারামিটার হিসেবে পাঠাই।

## সেটআপ

* প্রস্তাবিত এক্সটেনশনগুলি ইনস্টল করুন (amodio.tsl-problem-matcher, ms-vscode.extension-test-runner, এবং dbaeumer.vscode-eslint)।

## সরাসরি শুরু করুন

* `F5` চাপুন এবং আপনার এক্সটেনশন লোড করা একটি নতুন উইন্ডো খুলুন।
* কমান্ড প্যালেট থেকে আপনার কমান্ড চালান (`Ctrl+Shift+P` অথবা `Cmd+Shift+P` ম্যাক-এ) এবং `Hello World` টাইপ করুন।
* আপনার এক্সটেনশনে ডিবাগ করার জন্য `src/extension.ts` ফাইলের মধ্যে ব্রেকপয়েন্ট সেট করুন।
* ডিবাগ কনসোলে আপনার এক্সটেনশনের আউটপুট খুঁজুন।

## পরিবর্তন করুন

* `src/extension.ts` ফাইলে কোড পরিবর্তন করার পরে ডিবাগ টুলবার থেকে এক্সটেনশনটি পুনরায় চালু করতে পারেন।
* আপনি VS Code উইন্ডোও পুনরায় লোড করতে পারেন (`Ctrl+R` অথবা `Cmd+R` ম্যাক-এ) আপনার পরিবর্তন লোড করার জন্য।

## API অনুসন্ধান করুন

* আপনি `node_modules/@types/vscode/index.d.ts` ফাইলটি খুললে আমাদের API-এর সম্পূর্ণ সেট দেখতে পারবেন।

## টেস্ট চালান

* [Extension Test Runner](https://marketplace.visualstudio.com/items?itemName=ms-vscode.extension-test-runner) ইনস্টল করুন।
* **Tasks: Run Task** কমান্ড ব্যবহার করে "watch" টাস্ক চালান। এটি চালু না থাকলে টেস্ট আবিষ্কৃত নাও হতে পারে।
* অ্যাক্টিভিটি বারের Testing ভিউ খুলুন এবং "Run Test" বোতামে ক্লিক করুন, অথবা `Ctrl/Cmd + ; A` শর্টকাট ব্যবহার করুন।
* টেস্টের ফলাফল Test Results ভিউতে দেখুন।
* `src/test/extension.test.ts`-এ পরিবর্তন করুন অথবা `test` ফোল্ডারের ভিতরে নতুন টেস্ট ফাইল তৈরি করুন।
  * প্রদত্ত টেস্ট রানার শুধুমাত্র `**.test.ts` নামের প্যাটার্নের সাথে মিলে যাওয়া ফাইল বিবেচনা করবে।
  * আপনি `test` ফোল্ডারের ভিতরে আপনার টেস্টগুলো কাঠামোগতভাবে সাজানোর জন্য নতুন ফোল্ডার তৈরি করতে পারেন।

## আরও এগিয়ে যান

* [আপনার এক্সটেনশন বান্ডল করে](https://code.visualstudio.com/api/working-with-extensions/bundling-extension?WT.mc_id=aiml-137032-kinfeylo) এক্সটেনশনের সাইজ কমান এবং স্টার্টআপ টাইম উন্নত করুন।
* [আপনার এক্সটেনশন প্রকাশ করুন](https://code.visualstudio.com/api/working-with-extensions/publishing-extension?WT.mc_id=aiml-137032-kinfeylo) VS Code এক্সটেনশন মার্কেটপ্লেসে।
* [কন্টিনিউয়াস ইন্টিগ্রেশন সেটআপ](https://code.visualstudio.com/api/working-with-extensions/continuous-integration?WT.mc_id=aiml-137032-kinfeylo) করে বিল্ড প্রক্রিয়া স্বয়ংক্রিয় করুন।

**অস্বীকৃতি**:  
এই নথি মেশিন-ভিত্তিক এআই অনুবাদ পরিষেবা ব্যবহার করে অনুবাদ করা হয়েছে। আমরা যথাসম্ভব সঠিকতার জন্য চেষ্টা করি, তবে দয়া করে মনে রাখবেন যে স্বয়ংক্রিয় অনুবাদে ভুল বা অসংগতি থাকতে পারে। নথিটির মূল ভাষায় রচিত সংস্করণটিকেই প্রামাণিক উৎস হিসেবে বিবেচনা করা উচিত। গুরুত্বপূর্ণ তথ্যের জন্য পেশাদার মানব অনুবাদ সুপারিশ করা হয়। এই অনুবাদ ব্যবহারের ফলে উদ্ভূত কোনো ভুল বোঝাবুঝি বা ভুল ব্যাখ্যার জন্য আমরা দায়ী নই।