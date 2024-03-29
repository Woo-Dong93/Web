# Html 태그들...

### 1. `<!DOCTYPE html>`

- Document Type의 약자로 HTML이 어떤 버전으로 작성되었는지 미리 선언하여 웹브라우저가 내용을 올바로 표시할 수 있도록 해준다. <!DOCTYPE> 을 선언하지 않으면 호환모드(quirks mode)로 동작하는데, 호환 모드의 경우 각 브라우저마다 문서를 나타내는 방식이 다르기 때문에 크로스 브라우징 이슈가 훨씬 심해진다. 호환 모드로 렌더링을 하게 되면 오래된 웹페이지들을 최신 버전의 브라우저에서도 깨지지 않게 하기 위해 각 브라우저마다 다르게 보일 수 있다. 
- HTML 5를 의미
- 예를 들어, IE의 경우 호환 모드에서 박스모델을 잘못 해석하지만, 나머지 브라우저들을 제대로 해석한다.



### 2. `<html lang="en">`

- 웹 접근성에 관한 내용입니다. 꼭 선언을 안해도 아무 지장은 없다.
- 명시를 제대로 해주어야 스크린리더기가 이 언어를 인식하며 자동으로 음성을 변환하거나, 해당 언어에 적합한 발음을 제공하기 때문이다. 스크린 리더기는 시각장애인을 위한 기기이다. 
- 또한, 검색 옵션에서 '한국어로 된 문서로' 범위를 제한할 경우 `lang='ko'` 인 문서를 우선으로 검색한다고 한다.



### 3. `<meta charset='utf-8'>`

- `<meta>` 태그 : 다른데이터를 설명해 주는 데이터를 의미

- html 파일이 웹브라우저에서 표시되는 과정에서 인코딩할때 지정된 문자코드로 인코딩해라 
- 인코딩을 명확하게 알려주지 않으면 웹브라우저 설정 상황에 따라 자동으로 인코딩을 추정해서 처리해주는데, 처리가 정확할 때도 있 지만, 그렇지 못한 경우도 있다. 다양한 경우에 한글이 깨지지 않고 잘 보이기를 기대한다면 꼭 적어주는게 좋다.



#### 4. `<meta http-equiv="X-UA-Compatible" content="IE=edge">`

- 마이크로소프트에서 만든 익스플로러 브라우저는 호환성 보기 모드가 존재하는데 이는 사용자가 지원하는 브라우저에 따라 오래된 브라우저에서 정상적으로 출력되지 않는 이슈가 발생할 수 있다. 최신 브라우저만 지원하는 환경이라면 사실 이 태그를 사용하는 의미가 거의 없다. 하지만 일부 웹사이트는 오래된 버전의 브라우저까지 모두 지원하기도 하는데 이런 경우 필요한 메타 태그이다. IE 에서의 호환성 보기와 관련된 태그이다. `<meta http-equiv='X-UA-Compatible' content='IE=edge' />`로 사용하면 모든 IE 브라우저에 호환성보기를 무시해준다. `IE=edge`는 IE 브라우저의 최신 버전의 엔진을 사용하라는 뜻이다. 그 외에도 IE=5, IE=7 등등이 있다. 해당 렌더링 방식을 적용하라는 것이다.
- 마이크로소프트는 실험적인 프로젝트가 아닌 이상 `IE=edge` 모드를 지정할 것을 권장한다. 요즘에 개발하는 웹사이트를 IE5, 7의 렌더링 방식에 맞출 필요는 없기 때문에 IE를 지원하려면 `IE=edge`를 적어주면 될 것 같다.



#### 5. `<meta name="viewport" content="width=device-width, initial-scale=1.0">`

- meta viewport 태그는 애플이 아이폰, 아이패드 등 자사의 모바일 브라우저의 뷰포트 크기 조절을 위해 만들었다. meta viewport 태그는 W3C 명세에는 없는 즉, 표준이 아니지만 IOS 장치가 널리 사용 됨에 따라 사실상 표준처럼 사용되고 있고, 다른 브라우저들도 이 태그를 채택하게 된다.

- width=320 같이 지정된 넓이를 적어주면 이 웹페이지가 이 너비에서 가장 잘보인다고 알려주는 것과 같다. 

- 그러나 이 페이지를 하나의 장치에서만 보는 것이 아니기 때문에 반응형 디자인에 적합하지 않다. 

- 반응형 디자인을 위한 최선의 방법은 device-width로 적어 사용중인 장치와 동일하게 뷰포트를 설정하는 것이다.

- 또한, 웹 페이지가 처음 표시 될 때 확대되지 않도록 초기 배율 속성을 사용하여 기본 확대 / 축소를 설정할 수 있다. 사용자가 페이지를 방문할 때 확대 / 축소 할 필요가 없도록 하려면 비율을 1로 설정한다.

  - `maximum-scale=1` 로 설정하면 사용자가 스크롤하지 못 하도록 막을 수도 있다.

  