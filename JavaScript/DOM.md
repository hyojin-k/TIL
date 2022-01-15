# DOM
- 문서 객체 모델 Document Object Model
- 브라우저 안에 있는 랜더링 엔진이 HTML 문서를 해석하여 브라우저가 문서를 이해할수 있도록 하고,  **문서를 객체화**하여 자바스크립트로 html 요소에 접근하고 제어할 수 있도록 함
- 브라우저에서 자바스크립트로 HTML 요소를 제어할 수 있도록 제공하는 API
- **트리 구조**로 되어 있음
    - 하나의 부모 태그와 n개의 자식 태그로 이루어 질 수 있음
    - 각각의 노드에 접근해서 제어할 수 있음

- document 객체
    - 웹페이지 자체
    - DOM 트리의 최상위 노드
    - document 객체로 원하는 노드에 접근할 수 있음

### 주요 노드
- 문서 노드(document node)
- 요소 노드(element node)
- 어트리뷰트 노드(attribute node)
- 텍스트 노드(text node)


## BOM
- 브라우저 객체 모델 Browser Object Model
- 브라우저 자체를 제어할 수 있도록 모델링한 것
- 자바스크립트가 브라우조와 소통하기 위해 만들어진 모델
- 웹페이지의 내용을 제외한 브라우저 창에 포함된 모든 객체 요소
- window 속성에 속하여 docment가 아닌 window를 제어
- navigator, window, document, location, history, screen


## CSSOM
- Cascading Style Sheets Object Model
- css 문서를 자바스크립트로 제어할 수 있도록 하는 것

**참고**

모던 자바스크립트 Deep Dive