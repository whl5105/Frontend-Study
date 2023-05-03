# DDD
**DDD**는 **Domain Driven Design**의 약어로, 소프트웨어 개발에서 도메인을 중심으로 설계하는 방법론입니다.
도메인은 문제 영역에서 중요한 개념이나 업무 프로세스를 의미하며, 이를 기반으로 소프트웨어를 설계합니다.
DDD는 도메인 모델링, 리팩터링, 아키텍처 패턴 등의 기법을 활용하여 복잡한 문제를 해결하고 유연하고 확장 가능한 소프트웨어를 만드는데에 적합합니다.

<br>

# MSA
**MSA**는 **Microservices Architecture**의 약어로, 하나의 큰 애플리케이션을 작은 단위로 분리하여 각각의 서비스로 운영하는 아키텍처입니다. 이를 통해 개발과 배포가 더 빠르고 유연하게 이루어지며, 각각의 서비스를 독립적으로 확장하거나 교체할 수 있습니다. 또한 MSA는 다양한 프로그래밍 언어와 기술 스택을 혼용하여 사용할 수 있기 때문에, 팀의 선호나 요구사항에 따라 다양한 선택지가 있습니다.

<br>

# DDD를 활용한 MSA
MSA(마이크로서비스 아키텍처)를 구축하기 위해 좋은 방법 중 하나는 DDD(도메인 주도 설계)입니다.

MSA를 구현하는 필수 개념들이 DDD에서 왔고, 그 중 **Loose Coupling(느슨한 결합)** 과 **High Cohesion(높은 응집)** 은 DDD에서의 좋은 서비스를 개발하기 위한 핵심 기본 요소 중 하나입니다.

<br>

# DDD의 주요 설계 원칙 : Loose Coupling(느슨한 결합) & High Cohesion(높은 응집)
![](https://velog.velcdn.com/images/boniteterain/post/18789e19-c255-4dca-97b0-cb05eb960436/image.png)

도메인들 간에는 Loose Coupling하고 도메인 내에서는 High Cohesion 해야 합니다.
도메인은 소프트웨어로 해결하고자 하는 문제의 영역, 즉 개발하고자 하는 전체 서비스를 잘라낸 단위를 가리킵니다.

도메인을 잘못 나누면 DDD나 MSA 입장에서는 많은 혼란이 가중됩니다.
왜냐하면, Loose Coupling 해야 하는 연동 인터페이스를 High Cohesion 하게 되어 시스템 복잡도를 높이거나, High Cohesion 해야 할 서비스들 간을 Loose Coupling 해서 예상하지 못한 시스템 문제를 야기할 수 있기 때문입니다.

따라서, 도메인을 잘게 나누는 것, 즉 Loose Coupling 시키는 것만이 능사가 아니라, 어떤 서비스들을 하나의 도메인으로 잘 묶어서 High Cohesion 하게 할지 설계하는 것까지가 DDD나 MSA가 추구하는 지향점이 되어야 합니다. _**즉, 도메인을 Loose Coupling과 High Cohesion 관점에서 잘 나누는 것이 DDD와 MSA에서 가장 중요하다 할 수 있습니다**_. 

비즈니스 문제를 잘 투영한 서비스 도메인을 잘 나누는 것에서부터 시작하며, 각 도메인 서비스들이 Loose Coupling과 High Cohesion 각각을 지원할 수 있는 기술적 또는 아키텍처적 설계 원칙을 준수하는 것이 좋은 서비스 시스템을 개발하는 기본 원칙입니다.

[참고](https://helloworld.kurly.com/blog/ddd-msa-service-development/)
