# 파이썬 로깅 모듈을 활용한 커스텀 로그 클래스

### Description
* 파이썬 프로젝트를 진행하던 도중 사용이 편리하고 자세한 정보를 전달해주는 로깅 클래스가 있었으면 좋겠다는 생각에 만든 클래스.
* 어떤 타입의 변수를 다수 던져도 str으로 출력해준다.
* 어느 파일 몇 번째 줄 어느 함수에서 실행되었는지 자체적으로 정보를 준다.
* 싱글턴 디자인 패턴을 사용해서 어디에서나 로거 클래스를 호출하면 이전에 반환되었던 인스턴스를 반환한다.

### Environment
* Windows 10 21H1, 19043.1165

### Prerequisite
* Python 3.8.8

### Files
* Logger.cpp

### Usage
* 인스턴스를 생성하고 로깅 레벨에 따라 내부 클래스 메소드를 호출한 뒤 변수 및 문장들을 인자로 주면 콘솔 및 파일에 저장된다.
* 다른 클래스의 인스턴스를 생성할 때 인스턴스 변수로 초기화해주고 사용한다면 인스턴스 생성도 로그로 남길 수 있다.
* 인스턴스 변수로 초기화 된 경우 __del__ 메소드에서는 gc가 먼저 작동하고 실행되기 때문에 로그 인스턴스를 사용할 수 없었다.  

* 다음과 같이 출력된다.(프로젝트 로그파일 중)
```
2021-09-06 22:26:02,816 [RunThread.py        :<module>             :181  ] [INFO] >> <SharedMem.SharedMem object at 0x03C2E8E0> 
2021-09-06 22:26:02,816 [SharedMem.py        :add                  :66   ] [INFO] >> <Stocks.Stock object at 0x03C2E9E8> 
2021-09-06 22:26:02,817 [Stocks.py           :__init__             :52   ] [INFO] >> Name: 5930StockValue <utilsLT.QueueLT object at 0x03C2EA18> 
2021-09-06 22:26:02,817 [utilsLT.py          :__init__             :43   ] [INFO] >> 5930StockValue Queue init, size: 20 
2021-09-06 22:26:02,817 [Stocks.py           :__init__             :57   ] [INFO] >> Name: 5930TradeVolume <utilsLT.QueueLT object at 0x03C2EA00> 
2021-09-06 22:26:03,717 [SendRequest2Api.py  :Send_Request_Throttle:98   ] [INFO] >> Name: Queue4Request2Api <utilsLT.QueueLT object at 0x03C2E940> 
2021-09-06 22:26:03,717 [utilsLT.py          :__init__             :46   ] [WARNING] >> Queue4Request2Api Queue Called Again 
2021-09-06 22:26:02,818 [utilsLT.py          :__init__             :43   ] [INFO] >> 5930PriceData Queue init, size: 64 
2021-09-06 22:26:02,819 [SharedMem.py        :add                  :66   ] [INFO] >> Stock init: 5930 <Stocks.Stock object at 0x03C2E9E8> 
2021-09-06 22:26:02,819 [SharedMem.py        :add                  :68   ] [INFO] >> New Stock Instance: 5930 
2021-09-06 22:26:02,819 [SharedMem.py        :request_initial_info :151  ] [INFO] >> Info Request Pushed {'StockID': 5930, 'Buy': -2, 'Sell': 0} 
2021-09-05 20:58:42,034 [GetPutDB.py         :exception_handling   :271  ] [ERROR] >> Exception Occured, table tHist000080PriceInfo has 8 columns but 7 values were supplied 
2021-09-05 20:58:42,035 [Stocks.py           :stock_volume         :272  ] [INFO] >> Stock ID: 80 Total Stock Volume Updated and Enqueued: 406271 
```

### Update Log
 * 2021.08.15 Logger 클래스 등록
 * 2021.09.13 파일 및 폴더 자동생성기능 추가/구조 통일을 통해 가독성 향상
