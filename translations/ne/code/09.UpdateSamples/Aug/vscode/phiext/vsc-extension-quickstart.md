# तपाईको VS Code एक्स्टेन्सनमा स्वागत छ

## फोल्डरमा के छ

* यो फोल्डरमा तपाईको एक्स्टेन्सनका लागि आवश्यक सबै फाइलहरू छन्।
* `package.json` - यो म्यानिफेस्ट फाइल हो जहाँ तपाईले आफ्नो एक्स्टेन्सन र कमाण्ड घोषणा गर्नुहुन्छ।
  * नमूना प्लगइनले एउटा कमाण्ड दर्ता गर्छ र यसको शीर्षक र कमाण्ड नाम परिभाषित गर्छ। यस जानकारीको आधारमा VS Code ले कमाण्ड प्यालेटमा कमाण्ड देखाउन सक्छ। यसले प्लगइन लोड गर्न अझै आवश्यक पर्दैन।
* `src/extension.ts` - यो मुख्य फाइल हो जहाँ तपाई आफ्नो कमाण्डको कार्यान्वयन प्रदान गर्नुहुन्छ।
  * यो फाइलले एउटा फङ्सन `activate` निर्यात गर्छ, जुन तपाईको एक्स्टेन्सन पहिलो पटक सक्रिय हुँदा (यस अवस्थामा कमाण्ड कार्यान्वयन गरेर) बोलाइन्छ। `activate` फङ्सनभित्र हामी `registerCommand` बोलाउँछौं।
  * हामी कमाण्डको कार्यान्वयन रहेको फङ्सनलाई `registerCommand` मा दोस्रो प्यारामिटरको रूपमा पास गर्छौं।

## सेटअप

* सिफारिस गरिएका एक्स्टेन्सनहरू (amodio.tsl-problem-matcher, ms-vscode.extension-test-runner, र dbaeumer.vscode-eslint) इन्स्टल गर्नुहोस्।

## तुरुन्तै सुरु गर्नुहोस्

* आफ्नो एक्स्टेन्सन लोड गरिएको नयाँ विन्डो खोल्नका लागि `F5` थिच्नुहोस्।
* कमाण्ड प्यालेटबाट आफ्नो कमाण्ड चलाउनका लागि (`Ctrl+Shift+P` वा Mac मा `Cmd+Shift+P`) थिचेर `Hello World` टाइप गर्नुहोस्।
* आफ्नो एक्स्टेन्सन डिबग गर्न `src/extension.ts` भित्र ब्रेकप्वाइन्टहरू सेट गर्नुहोस्।
* डिबग कन्सोलमा आफ्नो एक्स्टेन्सनको आउटपुट फेला पार्नुहोस्।

## परिवर्तन गर्नुहोस्

* `src/extension.ts` मा कोड परिवर्तन गरेपछि डिबग टुलबारबाट एक्स्टेन्सन पुन: सुरु गर्न सक्नुहुन्छ।
* आफ्नो परिवर्तन लोड गर्न VS Code विन्डो पुन: लोड गर्न पनि सक्नुहुन्छ (`Ctrl+R` वा Mac मा `Cmd+R`)।

## API अन्वेषण गर्नुहोस्

* फाइल `node_modules/@types/vscode/index.d.ts` खोल्दा हाम्रो API को पूर्ण सेट हेर्न सक्नुहुन्छ।

## टेस्टहरू चलाउनुहोस्

* [Extension Test Runner](https://marketplace.visualstudio.com/items?itemName=ms-vscode.extension-test-runner) इन्स्टल गर्नुहोस्।
* **Tasks: Run Task** कमाण्ड प्रयोग गरेर "watch" टास्क चलाउनुहोस्। यो चलिरहेको सुनिश्चित गर्नुहोस्, अन्यथा टेस्टहरू फेला नपर्न सक्छन्।
* एक्टिभिटी बारबाट Testing भ्यू खोल्नुहोस् र "Run Test" बटन थिच्नुहोस्, वा `Ctrl/Cmd + ; A` हटकी प्रयोग गर्नुहोस्।
* टेस्ट नतिजाको आउटपुट Test Results भ्यूमा हेर्नुहोस्।
* `src/test/extension.test.ts` मा परिवर्तन गर्नुहोस् वा `test` फोल्डर भित्र नयाँ टेस्ट फाइलहरू सिर्जना गर्नुहोस्।
  * प्रदान गरिएको टेस्ट रनरले केवल `**.test.ts` नाम ढाँचासँग मिल्ने फाइलहरूलाई विचार गर्छ।
  * तपाईले आफ्नो टेस्टहरू संरचना गर्न `test` फोल्डर भित्र फोल्डरहरू सिर्जना गर्न सक्नुहुन्छ।

## अझ अगाडि बढ्नुहोस्

* [आफ्नो एक्स्टेन्सन बन्डल गरेर](https://code.visualstudio.com/api/working-with-extensions/bundling-extension) एक्स्टेन्सनको साइज घटाउनुहोस् र स्टार्टअप समय सुधार गर्नुहोस्।
* [आफ्नो एक्स्टेन्सन प्रकाशित गर्नुहोस्](https://code.visualstudio.com/api/working-with-extensions/publishing-extension) VS Code एक्स्टेन्सन मार्केटप्लेसमा।
* [Continuous Integration](https://code.visualstudio.com/api/working-with-extensions/continuous-integration) सेटअप गरेर बिल्डहरू स्वचालित गर्नुहोस्।

**अस्वीकरण**:  
यो दस्तावेज मेसिन-आधारित एआई अनुवाद सेवाहरू प्रयोग गरेर अनुवाद गरिएको हो। यद्यपि हामी शुद्धताका लागि प्रयास गर्छौं, कृपया जानकार रहनुहोस् कि स्वचालित अनुवादमा त्रुटिहरू वा अशुद्धताहरू हुन सक्छन्। यसको मौलिक भाषामा रहेको मूल दस्तावेजलाई प्रामाणिक स्रोत मानिनुपर्छ। महत्वपूर्ण जानकारीका लागि, व्यावसायिक मानव अनुवाद सिफारिस गरिन्छ। यस अनुवादको प्रयोगबाट उत्पन्न हुने कुनै पनि गलतफहमी वा गलत व्याख्याको लागि हामी जिम्मेवार हुने छैनौं।