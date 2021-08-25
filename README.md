# Linear_Regression
> Linear Regression 구현해보기

Machine Learning의 기초인 Linear Regression을 직접 구현하고 Weight 와 Bias 그리고 Cost의 값을 그래프로 확인하여 동작 원리를 올바르게 이해할 수 있도록 설계한 파이썬 코드입니다.

![](../header.png)

## 소개

이 Repository에서는 경향성이 있는 임의의 2차원 데이터를 400개 만들고 학습하여 이를 대표하는 선형함수(Hypothesis)를 찾는 과정을 쉽게 볼 수 있도록 만들었습니다. Linear Regression은 scikit learn와 같은 라이브러리에서 쉽게 가져와 사용할 수 있습니다. 하지만 Linear Regression을 직접 구현해보고 동작원리를 제대로 파악하지 않는다면 복잡한 상황에서 제대로 활용하기 어렵습니다.  Linear Regression의 Hypothesis를 이루는 Weight, Bias, Cost의 값을 확인하고 나아가 이 값들을 그래프로 표현하여 값의 변화를 확인합니다. 또한 학습이 진행되는 과정에서 H(x)함수가 어떻게 변화하는지 동영상으로 기록하여 확인합니다.

## 사용 예제

먼저 임의의 2차원 데이터를 경향성이 있도록 설정합니다.
```
mat_cov = [[1,0.9],[0.9,1]]
mu =  [4,3]
N = 400
X = np.random.multivariate_normal(mu, mat_cov, N)
```

_더 많은 예제와 사용법은 [Wiki][wiki]를 참고하세요._


## 업데이트 내역

* 0.2.1
    * 수정: 문서 업데이트 (모듈 코드 동일)
* 0.2.0
    * 수정: `setDefaultXYZ()` 메서드 제거
    * 추가: `init()` 메서드 추가
* 0.1.1
    * 버그 수정: `baz()` 메서드 호출 시 부팅되지 않는 현상 (@컨트리뷰터 감사합니다!)
* 0.1.0
    * 첫 출시
    * 수정: `foo()` 메서드 네이밍을 `bar()`로 수정
* 0.0.1
    * 작업 진행 중

## 정보

이름 – [@트위터 주소](https://twitter.com/dbader_org) – 이메일주소@example.com

XYZ 라이센스를 준수하며 ``LICENSE``에서 자세한 정보를 확인할 수 있습니다.

[https://github.com/yourname/github-link](https://github.com/dbader/)

## 기여 방법

1. (<https://github.com/yourname/yourproject/fork>)을 포크합니다.
2. (`git checkout -b feature/fooBar`) 명령어로 새 브랜치를 만드세요.
3. (`git commit -am 'Add some fooBar'`) 명령어로 커밋하세요.
4. (`git push origin feature/fooBar`) 명령어로 브랜치에 푸시하세요. 
5. 풀리퀘스트를 보내주세요.

<!-- Markdown link & img dfn's -->
[npm-image]: https://img.shields.io/npm/v/datadog-metrics.svg?style=flat-square
[npm-url]: https://npmjs.org/package/datadog-metrics
[npm-downloads]: https://img.shields.io/npm/dm/datadog-metrics.svg?style=flat-square
[travis-image]: https://img.shields.io/travis/dbader/node-datadog-metrics/master.svg?style=flat-square
[travis-url]: https://travis-ci.org/dbader/node-datadog-metrics
[wiki]: https://github.com/yourname/yourproject/wiki
