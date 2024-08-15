# WEB-CRAWLING-TUTORIAL
Tutorial for web-crawling with python

-------------------------------------------

1. 간단한 문법
   1. 자료구조
      1. 리스트
         1. 함수
            1. ``sum(arr)``
            2. ``sorted(arr)``
            3. ``for i in arr:``
            4. 엘레먼트 위치 찾기(i의 인덱스 찾기)
               1. ``arr.index(i)``
            5. 엘레먼트가 있는지
               1. ``element in arr``
      2. 튜플
         1. ``tuple`` or ``()``
         2. 리스트와의 차이
            1. ``assignment``가 ``tuple``에는 없다(불가변) // 반면 리스트는 (가변)
               1. ``element``의 값을 업데이트 하는 것
      3. 딕셔너리
         1. ``key``와 ``value``
         2. 어떤 ``key``가 있는지의 함수
         3. ``for`` 사용 가능
      4. 클래스(빵틀)와 오브젝트(빵)
         1. ``__init__``: 초기화 
      5. 상속
         1. 공통된 속성의 클래스가 있고, 그 밑에 기능을 추가하고 싶을 때
      6. package 만들기
         1. 폴더 만들기
         2. 클래스 파일 만들기
         3. ``__init__.py`` 만들어서 패키지 안의 모듈 정의(``from package import class``)
2. What is difference between web-crawling and web-scraping?
   1. Web-Crawling
      1. Dealing with deep and large data-sets
   2. Web-Scraping
      1. Retrieving information from any source(웹 포함)
3. Ref.
   1. Web-Scraping
      1. https://www.dataquest.io/blog/web-scraping-tutorial-python/
   2. Web-Crawling
      1. https://www.digitalocean.com/community/tutorials/how-to-crawl-a-web-page-with-scrapy-and-python-3
      2. 순서
         1. Creating Basic Scraper
            1. ``scrapy module`` 설치
               1. ``pip install scrapy``
            2. ``brickset-scraper`` package 생성
            3. ``scraper.py`` 파일 생성
               1. 코드 작성
            4. 코드 실행(Scrapy는 own comand line을 갖고 있다.)
               1. ``scrapy runspider scraper.py``
               2. 여기까지 따라했다면, 이 프로그램은 아무 것도 하지 않고 종료될 것이다. 우리가 따로 작업을 명령한 것이 아니기 때문에
         2. Extracting Data from a Page
            1. 해당 페이지의 ``pattern``을 찾아 원하는 데이터를 추출한다. ``parse`` 함수 추가
               1. 해당 페이지를 보면 각각의 name set은 ``h1 tag``에 있다.
               2. 코드를 추가하고 실행해보면 ``name``이라는 ``key``의 값이 출력되는 것을 볼 수 있다.
            2. ``img`` pattern을 보면 ``image``는 ``src``안에 있다.
               1. 소스 추가
         3. Crawling Multiple Pages
            1. 지금까지 한 페이지에서 원하는 데이터를 추출했다. 하지만, 이제 다른 페이지까지 해보자.(scrapying은 특정 소스에서 추출하는 것이고 crawling은 더 확장된 개념)
            2. 또 패턴을 보자면 페이지 넘김의 ``a`` tag에는 ``>``이 있다.
               1. 코드 추가
            3. 실행을 해보면 모든 페이지를 다 crawling할 것이다.
4. 시장성 및 비전 분석
   1. 다음에 입각하여 분석한다.
      1. 수요가 있는가?
         1. 현대 인간은 웹 검색이 생활화 되어 있다. 그에 따라서 원하는 정보를 찾는 것 또한 능력이자 시간(비용)의 소모이다.
            1. 예
               1. 인터넷 최저가 검색
                  1. 항공권
                  2. 각종 물품
               2. 주식 관련, 특히 가상화폐
                  1. 가상화폐의 경우 수익이 24시간 동안 발생하므로 실시간 정보가 필요된다.
      2. 지속 가능성 있는 수익모델인가?
         1. 필자는 4차 산업혁명의 키워드는 ``광고``, 자세히 말하자면 ``social marketing``이라고 생각한다.
            1. social marketing
               1. 사람들의 ``interest``와 ``behaviour``를 분석하여 맞춤 광고를 제공한다. 아니 들이민다. 근데 이게 먹힌다.
            2. 이러한 점에서 봤을 때 웹 크롤링의 기술의 깊이에 대해서 생각해 보면 특별히 어떤 기술이 뛰어나다든가 하는 ``시장장악력``에 의구심이 든다.
               1. 이를 가능케하는 기술력이 있다면 가능하지만 누구나 쉽게 할 수 있는 영역이라고 생각하며, 초기자본력이 낮아 시장 진입이 쉽다.
                  1. 결국 빠르게 ``red ocean``이 될 것이라는 주관적인 견해
      3. 그렇다면 어떤 비즈니스로 연계될 수 있을까?
         1. 단순히 ``crawling``의 기능을 강조하는 서비스 개발보다 ``user``의 ``접근성``을 높여야 한다고 생각한다.
            1. 접근성을 높인다는 것은 유저에게 맞는 애플리케이션의 형태로 연계되어 개발이 되어야 한다.
               1. 예
                  1. 주식/코인 투자용
                  2. 수강신청 전용
                  3. 항공권 좌석 예매 전용
                  4. 업로드되는 수많은 음원들에서 트렌디한 음악을 긁어오는 어플리케이션
         2. 위의 예를 봤을 때, 딱히 큰 수익이 날 수 있는 분야를 모르겠다리......흠,,,
      4. 결론
         1. ``crawling``은 현대에 필수적인 기술인 것 맞지만, 독자적으로는 빛을 볼 수 없다고 생각한다.
         2. 다양한 분야와 연계되어 기술이 사용될 때 시너지가 생길 것이다.