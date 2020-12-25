---
layout: post
title: "Web Mission4 - React 2-4장"
authors: [zeze1004]
tags: ["Web"]
image:
description: "React"
featured: false
---

Web 팀의 4번째 미션은 React 아래의 교재로 리액트 공부를 하는 것입니다.
이번 포스팅에서는 교재의 2-4장을 리뷰하겠습니다.

> [#4 Mission : React](https://react.vlpt.us/)

이번 미션은 이전 미션과 다르게 조건에 맞춰 코딩하는 것이 아닌 React를 배우는 것이 목표임으로 정해진 요구사항은 없습니다.

장에 맞춰서 리뷰하겠습니다.

## [2장] 리액트 컴포넌트 스타일링하기

1.  Sass
    Sass는 CSS의 전처리기로써 웹에서 컴파일이 안되지만, CSS보다 간단한 문법을 제공합니다.

        'node-sass' 라이브러리를 통해 Sass가 CSS로 변환되어 웹에서 컴파일 됩니다.

        sass는 css와 상당히 유사한 문법을 가지고 있습니다. 지금부터 소개할 몇 가지 문법은 css와 다른 sass의 문법입니다.

        1. 변수 선언

           ```css
           $변수명: 값;
           ```

           css는 변수명 앞에 '$' 붙이지 않는다는 차이점이 있습니다.
           변수 사용시 $변수명; 으로 사용합니다.

        2. 셀렉터 선언

           - css로 작성시

           ```css
            div.container h4 {
                color : blue;
            }
            div.container p {
                color : green;
            }
            ```

            - sass로 작성시

            ```css
            div.container {
                h4 {
                    color : blue;
                }
                p {
                    color : green;
                }
            }
            ```

            셀렉트는 h4, p와 같이 html 스타일 요소를 뜻합니다.

            css와 달리 sass는 관련된 class 안에 셀렉터들을 선언합니다. css보다 코드가 간결해지고 셀럭터 해석이 편하다는 장점이 있습니다.

2.  CSS Module
    코드가 길어지면 중복되는 클래스 이름이 생길 수 있습니다. CSS Module은 클래스 이름을 고유하게 만들어 겹치지 않도록 해줍니다.

    따로 라이브러리를 설치할 필요 없이 기존 css 파일 확장자를 .module.css로 설정하면 됩니다.

    Sass에서도 사용 가능합니다. .module.scss로 바꿔주면 됩니다.

    가령 Box.css를 Box.module.css로 바꾼 후 js 파일에 import할려면 아래와 같이 하면 됩니다.

    ```javascript
    import React from "react";
    import styles from "./Box.module.css";

    function Box() {
      return <div className={styles.Box}>{styles.Box}</div>;
    }
    ```

    import로 불러온 styles 객체 안에 있는 값을 참조해야 합니다.

3.  styled-components
    styled-components는 js 안에 css(CSS in JS)를 작성할 수 있는 리액트 라이브러리 입니다.

        보통 react 컴포넌트를 스타일링할 때 외부 css 파일을 className으로 속성을 전달 받아서 렌더링하여 사용했는데요.

        styled-components을 사용하면 css를 컴포넌트 내부에 넣기 때문에 수정이 훨씬 쉽다는 장점이 있습니다.

        `npm add styled-components` 설치해주세요.

        ![blue_circle.png](../assets/images/post-WEB-Mission4/blue_circle.png)

        styled-components를 이용하여 css 파일없이 위의 파란원을 만들어봅시다.

        [App.js]

        ```javascript
        import React from 'react';

        import styled from 'styled-components';

        const Circle = styled.div`
            width: 5rem;
            height: 5rem;
            background: ${props => props.color || 'black'};
            border-radius: 50%;
            `;
            <!-- ` ` <= 사용 주의! -->

        function App() {
        return <Circle color="blue" />;
        }

        export default App;
        ```

        App.js 파일의 Circle 컴포넌트에 css가 들어갔습니다.
        이제 js파일 내에서 바로 css 수정이 가능합니다!

        div를 스타일링하였으므로 ```styled.div```를 사용했습니다.

        Circle 컴포넌트에 color라는 props를 넣어 색깔도 변경 가능합니다.

        `props: <컴포넌트이름: props이름 = "값">`

## [3장] 멋진 투두리스트 만들기