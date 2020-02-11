
# CSS-in-JS

SPA가 확산됨에 따라 Web Front-end 개발은 점차 Component 기반으로 진행되었습니다. 그 흐름을 따라 개발자는 컴포넌트 별로 스타일을 관리해야 했고, js 안에서 css를 직접 사용하는 방법이 등장하면서 많은 개발자들은 컴포넌트 기반으로 개발과 스타일링을 병행할 수 있었습니다.

물론 css-in-js의 장접은 className hashing, SSR에 특화된 점 등 다양하게 이야기할 수 있지만, 가장 대표적으로는 컴포넌트 기반 개발 방법을 위해 적합한 기법이라는 것입니다.

우리는 React에서의 css-in-js 기법을 살펴볼 예정입니다. 만약 react에 대한 이해가 부족하다면 [React 공식 한글 문서](https://ko.reactjs.org/docs) 혹은 [react4newbie](https://github.com/rayleighko/react4newbie)를 참고하시길 바랍니다.

보편적으로 React에서의 css-in-js를 위한 도구는 styled-components, emotion, jss가 있고, 이 문서에서는 Styled-Components를 중심으로 설명할 예정입니다.

## Styled-Components

styled-components는 React 컴포넌트 시스템의 스타일링을 위해 CSS를 어떻게 향상된 방법으로 활용할 지에 대한 고민의  결과입니다. 단일 사용 사례(a single use case)에 중점을 두어 개발자의 경험과 최종 사용자의 결과를 최적화했습니다.

개발자를 위한 향상된 경험 외에도 styled-components는 다음을 제공합니다.

- **Automatic critical CSS**: styled-components는 페이지에 렌더링되는 컴포넌트를 추적하고 해당 스타일과 다른 요소를 완전히 자동으로 주입(injects)합니다. code splitting과 결합하면 사용자는 필요한 최소량의 코드를 로드할 수 있습니다.

- **No class name bugs** : styled-components는 스타일에 대해 각 태그가 고유 한 클래스 이름을 갖도록 합니다. 중복, 겹침 또는 철자 오류에 대해 걱정할 필요가 없습니다. 협업을 위해 클래스에 라벨링하는 것도 가능합니다.

- **Easier deletion of CSS** : 기존의 방법에서는 클래스 이름이 코드베이스 어디에서 사용되는지 알기가 어려웠습니다. styled-components는 모든 스타일링이 특정 컴포넌트에 연결되어 있기 때문에 어디에 사용되는지 분명합니다. 컴포넌트가 사용되지 않고 삭제되면 모든 스타일이 컴포넌트와 함께 삭제됩니다(which tooling can detect).

- **Simple dynamic styling** : props 또는 글로벌 테마를 기반으로 컴포넌트의 스타일을 조정하는 것은 수십 개의 클래스를 수동으로 관리하지 않아도 간단하고 직관적으로 컴포넌트를 볼 수 있습니다.

- **Painless maintenance** : 컴포넌트에 영향을 미치는 스타일을 찾기 위해 다른 파일을 찾아 다닐 필요가 없으므로 코드베이스의 크기에 상관없이 유지 관리는 매우 중요합니다.

- **Automatic vendor prefixing** : CSS를 최신의 표준에 맞게 작성하고 스타일이 지정된 컴포넌트가 브라우저 공급자를 자동으로 감지해 나머지를 처리하도록 합니다. 개별 컴포넌트에 바인딩되어 즐겁게 CSS를 작성하면서 이러한 모든 이점을 누릴 수 있습니다.

일반적으로 다음과 같이 사용할 수 있습니다.

```javascript
import React, { Components } from "react";
import styled from "styled-components";

// Create a Title component that'll render an <h1> tag with some styles
const Title = styled.h1`
  font-size: 1.5em;
  text-align: center;
  color: palevioletred;
`;

// Create a Wrapper component that'll render a <section> tag with some styles
const Wrapper = styled.section`
  padding: 4em;
  background: papayawhip;
`;

class App extends Components {
  // Use Title and Wrapper like any other React component – except they're styled!
  render() {
    return (
      <Wrapper>
        <Title>Hello World!</Title>
      </Wrapper>
    );
  }
}
```
