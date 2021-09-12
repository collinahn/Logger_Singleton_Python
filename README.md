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
> 2021-08-13 16:32:35,088 [SharedMem.py:__new__:27] [INFO] >> <SharedMem.SharedMem object at 0x0000029623DE4C40> 
> 2021-08-13 16:32:35,089 [TradeLogic.py:__init__:28] [INFO] >> <TradeLogic.TradeLogic object at 0x0000029623DE4B20> 
> 2021-08-13 16:32:35,089 [GetPutDB.py:__init__:30] [INFO] >> <GetPutDB.GetPutDB object at 0x0000029623DE4C10> 
> 2021-08-13 16:32:35,090 [RunThread.py:call_price:75] [INFO] >> thread start 
> 2021-08-13 16:32:35,090 [RunThread.py:update_info:60] [INFO] >> thread start 
> 2021-08-13 16:32:35,091 [SharedMem.py:__new__:27] [INFO] >> <SharedMem.SharedMem object at 0x0000029623DE4C40> 
> 2021-08-13 16:32:35,091 [SharedMem.py:update_current_stock_price:103] [INFO] >> Shared Memory Updated: Price 
> 2021-08-13 16:32:35,092 [SharedMem.py:update_current_stock_quantity:112] [INFO] >> Shared Memory Updated: Quantity 
> 2021-08-13 16:32:35,093 [SharedMem.py:update_trade_volume:121] [INFO] >> Shared Memory Updated: Total Trade Volume(should be presented once a day) 
```
