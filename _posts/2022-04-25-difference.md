---
title: “require와 import의 차이점”
categories:
- blogging
last_modified_at: 2022-04-25T15:00:00+09:00
toc: true
---
### JS ES6 - require, import
```
const ShuffleData = require('functionGroup');
import ShuffleData from "functionGroup";
```
두 줄의 코드는 functionGroup 모듈을 불러오는 동일한 기능의 코드입니다.
> require - CommonJS
import - ES6


CommonJS 방식을 따른 첫번째 코드는 require 키워드를 사용하여 다른 변수를 할당하듯이 모듈을 불러오는 반면에, ES6 방식을 따른 두번째 코드는 Java나 Python처럼 import 키워드를 사용하여 좀 더 명시적으로 모듈을 불러오고 있습니다. 
두 가지 방법의 주요한 차이점은 아래와 같습니다.


**✋✋ JavaScript에서 require와 import의 주요 차이점**
- require()는 CommonJS를 사용하는 node.js문이지만 import()는 ES6에서만 사용됩니다.

- require()는 파일 (어휘가 아님)에 들어있는 곳에 남아 있으며 import()는 항상 맨 위로 이동합니다.

- require()는 프로그램의 어느 지점에서나 호출 할 수 있지만 import()는 파일의 시작 부분에서만 실행할 수 있습니다. (하지만 import전용 비동기 문법으로 처리 가능)

- 대부분의 사람들은 require()문으로 직접 코드를 실행하지만 import()로 작업 할 때 실험적 모듈 기능 플래그를 사용하는 것을 선호합니다.

- 프로그램에서 동시에 사용할 수 없습니다.

- 일반적으로 import()는 사용자가 필요한 모듈 부분 만 선택하고 로드 할 수 있기 때문에 더 선호됩니다. 이 명령문은require()보다 성능이 우수하며 메모리를 절약합니다.

가독성, 메모리, 모듈호출등 import를 사용하는게 더 좋아보입니다.

하지만 무조건적으로 import하는 방식이 좋다고 할 순 없습니다.<br><br>
**CommonJS 모듈 시스템의 필요성**
아직까지는 import는 100% 를 대체할수는 없습니다.
**_Babel과 같은 ES6 코드를 변환 해주는 도구를 사용할 수 없을 땐 require 키워드를 사용해야합니다._**

### require 모듈 불러오기/내보내기

```
exports.IncreaseAdUid = IncreaseAdUid;
exports.InsertAd = InsertAd;

```
이처럼 내보낼 객체를 하나씩 지정해 줘야 합니다. 
그리고 불러올 땐
```
const { IncreaseAdUid, InsertAd } = require('./function');

const ad = require('./function');
```
이렇게 두 가지 방법으로 호출을 할 수있습니다.
첫 번째 방법으로 할 시 객체를 직접 명시하여 사용하고
두 번째 방법은 **ad.InsertAd()** 이렇게 변수화시킨 객체를 불러줍니다.

### <br>ES6모듈의 좋은 점
ES6 모듈이 좀 더 최신모듈, Commonjs 방식 대비 이점들이 있습니다.
import, from, export, default 처럼 모듈 관리 전용 키워드를 사용하기때문에 가독성이 좋습니다.
그리고 비동기 방식으로 작동, 모듈에서 실제로 쓰이는 부분만 불러오기때문에 성능, 메모리에서 유리합니다.
모듈 호출때 써야 할 Named Parameter와 같이 CommonJS에서는 지원하지 않는 기능들이 있습니다.

### import 모듈 불러오기/내보내기

```
let module = {IncreaseAdUid, InsertAd}
export default module;
--------------------- 
불러오기
1. import {IncreaseAdUid, InsertAd} from './function'  
2. import module from './function' 
```

등 다양한 방법으로 모듈을 불러오거나 내보낼 수 있습니다.


> "test" = "module"

참고로 pakage.json 에 명시를 해놓아야 합니다.(cannot find module이런 오류 납니다.)<br><br><br>
**reference**
* https://inpa.tistory.com/entry/NODE-📚-require-⚔️-import-CommonJs와-ES6-차이-1 
* https://www.daleseo.com/js-module-require/
