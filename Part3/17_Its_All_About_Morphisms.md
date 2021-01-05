## 17. It's All About Morphisms

카테고리 이론이 결국 모두 사상에 관한 것이라는것을 아직 충분히 설명하지 못한것같습니다. 다음 주제는 수반(adjuction)입니다. 이는 홈셋의 동형사상에 대하여 정의되어 있기 때문에 지금까지 해왔던 홈셋을 만드는 기본을 리뷰하려고합니다. 또한 수반으로 지금까지 해왔던 구조들을 더 일반적으로 묘사할 수 있을것임을 볼것입니다. 그러기에 이전에 한것을 리뷰하는것은 도움이 될 수 있습니다.



### 17.1 Functors

시작하며 펑터를 사상을 미팽하는것 위주로 생각해야합니다. 하스켈에서 fmap을 중심으로 하여 Functor 타입클래스를 정의하던거 처럼요. 물론 펑터는 대상도 - 사상의 엔드포인트로 말입니다- 매핑합니다. 그럴 수 없다면 구조를 보존하며 매핑을 할 수 없을것입니다. 대상으로 어떤 사상이 합성가능한지 알 수 있습니다. 둘이 합성할 수 있다면 한 사상의 타겟 타입은 다른 사상의 소스 타입과 일치 하여야 합니다. 그렇기에 합성된 사상을 리프팅된 사상의 합성으로 매핑하고 싶다면 합성된 사상의 앤드포인트가 어떻게 리프팅 되어 매핑될것인지는 매우 자명합니다.



### 17.2 Commuting Diagrams

가환 다이어그램(commuting diagrams)으로 사상의 많은 속성들이 설명될 수 있습니다. 만일 특정 사상이 하나 이상의 다른 사상들의 합성으로 묘사될 수 있다면 여기서 가환 다이어그램을 얻을 수 있습니다.

특히 가환 다이어그램은 대부분의 universal construction의 기초를 형성합니다(이니셜, 터미널 오브젝트 제외). 이를 product, coproduct, (co-)limit, exponential object, free monoid를 통해 보았습니다.

곱은 universal construction의 단순한 예 입니다. 우리는 두개의 대상 a, b를 선택하고 그들의 곱으로서 보편의 성질을 가진 한쌍의 사상 p, q를 지니는 대상 c가 있는지 확인하였습니다.

곱은 극한의 특수한 케이스 입니다. 뿔에의해 극한은 정의되고 일반적인 뿔은 가환 다이어그램에 의해 형성됩니다. 디 다이어그램간의 가환은 펑터 매핑을 위한 적절한 naturality condition으로 대체 될 수 있습니다. 이런식으로 가환성은 자연변환의 상위 수준 언어에 대한 기본적인 역할로 축소됩니다.



### 17.3 Natural Transformations

일반적으로 자연변환은 사상을 가환 다이어그램으로 매핑할때 매우 편리합니다. 두개의 반대되는 naturality square는 어떤 사상 f를 두개의 펑터 F, G로 매핑한것입니다. 다른 사이드는 자연변환의 컴포넌트 입니다(이경우에도 물론 사상입니다.)

![](https://bartoszmilewski.files.wordpress.com/2015/04/3_naturality.jpg?w=216&h=179)

Naturality는 "neighboring" 컴포넌트로 이동할때(neighboring는 사상으로 연결됨을 뜻함) 카테고리나 펑터의 구조를 해치지 않음을 뜻합니다. 먼저 자연변환을 선택하고 펑터로 점핑하거나 반대로 하거나 상관이 없습니다. 두 길은 직교합니다. 자연변환은 왼쪽에서 오른쪽으로 이동하고 펑터는 위에서 아래방향으로 이동합니다. 펑터틔 이미지를 타겟 카테고리의 종이 같이 시각화 할 수 있습니다. 여기서 자연변환은 한편에서 대응되는 다른편으로 매핑을 합니다.

![](https://bartoszmilewski.files.wordpress.com/2015/11/sheets.png)

이 직교성을 하스켈에서 예를들어 보았었습니다. 여기서 펑터는 모양 변경없이 컨테이너의 내용물을 바꾸고, 자연변환은 내용물을 건들지 않고 다른 컨테이너로 리 패키징 합니다. 이 연산의 순서는 상관없습니다.

극한의 정의에서 뿔이 자연 변환으로 대체되는 것을 보았습니다. Naturality은 뿔의 모든 측면이 가환(commute) 함을 보입니다. 그런 와중에도 극한은 뿔 간의 매핑 이라는 측면으로 정의됩니다. 이 매핑은 가환 조건을 따라야 합니다(예를 들어 곱의 정의에서 삼각형들이 가환이라는 것 처럼 말입니다.)

이 조건도 naturality에 의하여 대체될 수 있습니다. 유니버셜 콘이나 극한이 (반변) 홈 펑터 간의 자연변환으로 정의되었던것을 기억하세요

```haskell
F :: c -> C(c, LimD)
```

그 자체로 자연변환인 C의 대상에서 콘으로 매핑하는 (반변) 펑터도 있음을 기억하세요

```haskell
G :: c -> Nat(Δ𝑐,𝐷)
```

Δ𝑐는 constant 펑터 이고 D는 C의 다이어그램에 정의된 펑터 입니다. 두 펑터 F, G는 C의 사상에 대하여 정의됩니다. F와 G 간의 특별한 자연적 변환은 동형 사상입니다.



### 17.4 Natural Isomorphisms

자연 동형사상(natural isomorphism)은 자연 변환의 모든 컴포넌트들이 역의 방향이 존재함을 뜻합니다. 그리고 이는 카테고리 이론에서 두개가 같음을 의미합니다. 이 변환의 컴넌트는 대상간 동형이여야합니다 - 사상에 역이 존재합니다. 펑터 이미지를 종이로 시각화 한다면 자연 동형은 이 두 종이간에 역이 있는 일대일 매핑을 의미합니다.



### 17.5 Hom-Sets

그러면 사상은 무엇일까요? 이들은 대상보다 구조가 좀더 있습니다: 대상과 다르게 사상은 두개의 끝이 있습니다. 하지만 만일 시작점이나 끝점을 고정한다면 이는 두 점간의 시시한 집합을 형성합니다.(적어도 스몰 카테고리에서는 말입니다.) 이와같은 집합의 원소에 구분을 위하여 f나 g같은 이름을 부여할 수 있습니다. - 하지만 본질적으로 이게 뭐하는 짓일까요? 이게 차이를 만드나요?

홈셋에 속한 사상을 구분할 수 있는 유일한 방법은 그들이 다른 사상과 어떻게 합성하느냐 입니다. 예를 들어 다음과 같이 어떤 사상 h가 f, g와 합성했을때 이들이 다르다면 f와 g가 다르다는 것을 직관적으로 관찰할 수 있습니다.

>h . f != h . g

이 둘의 차이를 직접적으로 관측할 수 없더라도 우리는 펑터로 이들을 리프팅하여 이를 확대해서 볼 수 있습니다. 이들이 다르다면 펑터는 두 사상을 각기 다른 구분되는 사상으로 매핑할것입니다.

> 𝐹𝑓 ≠𝐹𝑔

리치 카테고리에서 인접한?(abuttin) hom-sets은 더 많은 해결책을 제시합니다.

>h′ ∘ 𝐹𝑓 ≠ h′ ∘ 𝐹 𝑔

여기서 h′는 F의 이미지에 없습니다.



### 17.6 Hom-Set Isomorphisms

많은 카테고리적 구조들은 홈셋의 동형에 의지합니다. 하지만 홈셋은 단순한 집합 이기 때문에, 단순한 동형은 이들간의 충분한 정보를 주지는 않습니다. 유한한 집합의 경우 동형은 두 집합의 원소의 수가 같음을 의미하고 무한한 집합에서는 그들의 cardinality가 같아야 함을 의미합니다. 하지만 홈셋간의 동형에 제일 중요한 부분은 합성입니다. 합성에는 하나 이상의 홈셋이 포함됩니다. 우리는 홈셋의 전체 컬렉션을 포괄하는 동형사상을 정의할 필요가 있으며 상호간 합성되는 컴포넌트간에 일부 가환조건을 부과하여야 합니다. 이경우에 natural isomorphism이 최상의 방법 입니다.

하지만 홈셋의 natural isomorphism은 무엇일까요? Naturality는 펑터간 매핑의 속성입니다. 그렇기에 hom-set-valued 펑터간의 natural isomorphism에 대하여 이야기 해봐야 합니다. 사상에 대한 이들의 동작은 적절한 hom-functor에 의해 유도됩니다. 사상은 펑터가 반변/공변이냐에 따라 사전 혹은 사후 합성을 이용하여 hom-functor에 의해 매핑됩니다.

요네다 임베딩은 이와같은 동형의 예 입니다. 이는 카테고리 C의 홈셋을 펑터 카테고리의 홈셋으로 매핑합니다. 그리고 이는 자연적 입니다. 요네다 임베딩의 한 펑터는 C에서 홈 펑터 이고 다른것은 대상을  홈셋간의 자연변환의 집합으로 대상을 매핑합니다.

극한의 정의도 역시 홈셋간의 자연 동형입니다.

>𝐂(𝑐, Lim𝐷) ≃ 𝐍𝐚𝐭(Δ𝑐 , 𝐷)

이를 이용하여 exponential object나 free monoid의 구조도 홈셋간의 자연 동형으로 묘사할 수 있습니다.

이는 우연이 아닙니다. 이제 곧 이것들이 단지 hom-set의 자연 동형으로 정의되는 adjuction의 다른 예 이라는 것을 보게될 것 입니다.



### 17.7 Asymmetry of Hom-Sets

adjunction을 이해할 수 있는 한가지 더 관찰할 수 있는 점이 있습니다. Hom-set은 일반적으로 대칭적이지 않습니다. 홈셋 C(a, b)는 홈셋 C(b, a)와 매우 다릅니다. 이 비대칭의 극단적인 예로 카테고리적인 측면에서 본 partial order를 들 수 있습니다. partial order에서 a보다 b가 더 낫거나 같다라는 조건이 있는경우 a -> b인 사상이 있을 수 있습니다. a와 b가 다르다면 b -> a와 같은 형태의 사상은 존재할 수 없습니다. 그렇기에 만약 C(a, b)가 비어있지않는 경우 특별히 싱글톤 셋인 경우 a와 b가 다르다면 C(b, a)는 엠티셋이 되어야 합니다. 이와같은 카테고리에서 화살표는 한 방향만 정의됩니다.

비대칭일 필요가 없는 관계를 기반으로 하는 preorder의 경우 가끔 순환하는 경우를 제외하고는 단방향을 형성합니다. 임의의 카테고리를 preorder의 일반화로 생각하는것이 편리합니다.

preorder는 thin 카테고리 입니다. 이경우 모든 hom-set은 싱글톤이거나 엠티입니다. 일반 카테고리의 경우는 thick한 preorder로 시각화 할 수 있습니다. 
