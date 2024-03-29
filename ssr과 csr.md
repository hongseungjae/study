SSR vs CSR
서버 사이드 렌더링(SSR)이란 브라우저가 페이지에 그려낼 HTML 파일을 서버에서 가지고 있다가 바로 주거나, 서버에서 동적으로 생성해서 주는 방식을 말한다. 
이와 반대로 클라이언트 사이드 렌더링(CSR)은 최소한의 HTML파일을 먼저 받고, 이후 렌더링에 필요한 데이터를 브라우저가 요청, 데이터를 기반으로 브라우저에서 렌더링하는 방식이다.

SPA vs MPA
이와 관련해서 Single Page Application(SPA), Multi Page Application(MPA)이라는 개념도 존재한다. 
여기서 오해할 수 있는 내용이 있는데, SPA는 반드시 CSR이고, MPA는 반드시 SSR이다는 것이다. 일반적으로는 맞지만 사실 섞일 수 있는 개념들이다

SPA는 웹 페이지 로딩시 하나의 HTML를 받고, 파싱 과정에서 필요한 정적 파일들(css, js, 이미지 등..)을 받는다. 
이후 주로 CSR 방식으로 렌더링을 하기 때문에 SPA는 CSR로 구현한다고 알려져있다. 
다만 요즘 최근 트렌드는 첫 화면은 SSR로 나타내고 이후 사용자 인터렉션에 따른 변화를 CSR로 나타내는 방식이다. 
이유는 SSR의 장점인 SEO(검색 엔진 최적화)와 첫 페이지 로딩 속도를 개선하기 위해서다.

MPA는 웹 어플리케이션의 각 페이지마다 서버에서 그에 맞는 HTML 파일을 주는 방식이기 때문에 페이지마다 SSR을 통해 서버가 제공하는 HTML을 브라우저가 그려낸다고 알려져 있다. 
하지만 MPA에서도 페이지 내의 작은 부분에서는 CSR로 구현하는게 가능하다.

결론은..
즉, SPA와 MPA의 주요한 차이점은 웹 어플리케이션의 각 페이지를 위한 HTML의 수가 하나인가, 
여러 개인가이고 CSR과 SSR의 차이는 하나의 HTML 파일을 어디서 동적으로 생성하고 변경하는가이다. 
상황에 따라 여러가지 조합으로 사용할 수 있다!
