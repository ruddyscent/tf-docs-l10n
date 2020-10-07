# MLIR 언어

## 개요

서로 다른 하드웨어 및 소프트웨어 대상을 분리하기 위해 MLIR에는 다음과 같은 "언어"가 있습니다.

- TensorFlow IR, TensorFlow 그래프에서 가능한 모든 것을 나타냅니다.
- XLA HLO IR, XLA의 컴파일 기능(특히 TPU에 대한 출력 포함)을 활용하도록 설계되었습니다.
- [다형 표현](https://en.wikipedia.org/wiki/Polytope_model)과 최적화에 초점을 맞춘 실험적인 affine 언어
- LLVM IR, LLVM 자체 표현과의 1:1 매핑을 사용하여 MLIR이 LLVM을 통해 GPU 및 CPU 코드를 내보낼 수 있습니다.
- TensorFlow Lite, 모바일 플랫폼에서 실행되는 코드로 변환됩니다.

각 언어는 "이것은 이항 연산자이며, 입력과 출력의 유형이 같습니다."와 같이 정의된 고정 연산 집합으로 구성됩니다.

## MLIR에 추가하기

MLIR에는 전 세계적으로 알려진 연산의 고정/내장 목록이 없습니다("내부 함수" 없음). 언어는 완전히 사용자 정의 유형을 정의할 수 있으며, MLIR이 LLVM IR 유형 시스템(일급 집계 포함), 양자화 유형과 같은 ML 최적화 가속기에 중요한 도메인 추상화, Swift 또는 Clang 유형 시스템(Swift/Clang 선언 노드를 중심으로 구축) 등을 모델링할 수 있습니다.

하위 수준의 새로운 컴파일러를 연결하려면 TensorFlow Graph 언어와 자신의 언어 간에 새로운 언어와 수준 낮추기(lowerings)를 생성합니다. 이렇게 하면 하드웨어 및 컴파일러 제조업체 경로가 매끄러워집니다. 같은 모델에서 다양한 수준의 언어를 대상으로 할 수도 있습니다. 높은 수준의 옵티마이저는 IR의 익숙하지 않은 부분을 존중하고 낮은 수준에서 처리할 때까지 기다립니다.