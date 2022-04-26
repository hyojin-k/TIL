# react-i18next

- react에서 다국어 처리를 하기 위해 사용

> index.js

```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import "./index.css";
import App from "./App";
import reportWebVitals from "./reportWebVitals";

// i18n.js 파일 import
import "./i18n/i18n";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();
```

**언어 별 json 파일 생성**

> src > i18n > locales> en> translation.ko.json

```jsx
{
  // 키 : 번역될 키 값
  "language" : "한국어"
}
```

> src > i18n > locales> en> translation.en.json

```jsx
{
  // 키 : 번역될 키 값
  "language" : "english"
}
```

**i18n.js**

> src > i18n > i18n.js

```jsx
import i18n from "i18next";
import { initReactI18next } from "react-i18next";

// 번역할 json 파일 import
import translationEn from "./locales/en/translation.en";
import translationKo from "./locales/ko/translation.ko";

// 사용할 언어
const resource = {
  en: {
    translation: translationEn,
  },
  ko: {
    translation: translationKo,
  },
};

i18n
  .use(initReactI18next) // passes i18n down to react-i18next
  .init({
    resources: resource,
    lng: "ko",
    fallbackLng: "ko",
    // ns: ['translation'],
    // defaultNS: "translation",
    debug: true,
    keySeparator: false, // we do not use keys in form messages.welcome
    interpolation: {
      escapeValue: false, // react already safes from xss
    },
  });

export default i18n;
```

**컴포넌트**

> src > components > i18Test.js

```jsx
import React from "react";
// t, i18n 를 사용할 수 있도록 하는 hook
import { useTranslation } from "react-i18next";

function I18Test() {
  const { i18n, t } = useTranslation();

  const onChangeLangKo = () => {
    i18n.changeLanguage("ko");
  };
  const onChangeLangEn = () => {
    i18n.changeLanguage("en");
  };

  return (
    <div>
      <button onClick={onChangeLangKo}> 한국어 </button>
      <button onClick={onChangeLangEn}> english </button>

      // i18n.js에서 지정한 키 사용
      <div>{t("language")}</div>
    </div>
  );
}

export default I18Test;
```