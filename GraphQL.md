1. graphql
   1. 기존 rest api의 두가지 문제점을 해결
      1. Overfetching-problem
      2. Underfetching-problem
2. user가 보내는 request는 항상 두번째 argument에 위치한다.
3. Query type에 대한 정의를 반드시 작성해줘야 한다.
4. Document를 쉽게 작성할 수 있다.
5. 다른 server의 api에 request를 보내서 받은 json을 내 server에서 다시 응답해서 graphql query로 보내서 json을 재정의할 수 있다. 심지어 문서까지 가능. 그런데, 대상의 api가 변경되면 내 것도 에러가 날듯
6. 기존 api는 받는 json의 모든 타입을 정해주거나 받는 데이터의 타입을 정해주지 않아 error가 발생하지도 않았는데, graphql을 이용하면 받는 data의 type을 지정해줄 수 있어, 오류가 날 확률을 줄여주고 필요한 data만 지정하여 받을 수 있는 등의 장점이 있다.
7. 이러한 점들을 활용해서 기존의 api들을 활용하여 새로운 api서비스를 만드는 것이 가능할 듯 하다.