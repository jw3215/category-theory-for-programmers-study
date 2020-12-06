## 10. Natural Transformations

일전에 펑터는 카테고리 사이에서 구조를 유지하며 매핑을 한다는것을 보았습니다.

펑터는 한 카테고리를 다른것에 "embed" 시킵니다. 펑터는 연결을 유지하면서 여러개를 하나로 축소시킵니다. 이는 한 카테고리를 다른 카테고리로 내부에 위치시키는 것으로 모델링 할 수 있습니다. 소스 카테고리는 대상 카테고리의 일부인 구조에 대하여 모델, 청사진 역할을 합니다.

하나를 다른 카테고리에 내장시키는 방식은 매우 많습니다. 어떤 경우 두 카테고리는 비슷하거나 혹은 매우 다를 수 있습니다. 한 카테고리 전체를 하나의 대상으로 축소시키는 경우도 있고 모든 대상과 사상을 다른 카테고리의 대상과 사상으로 매핑하는 경우도 있습니다. 동일한 청사진이 각기 다른 방식으로 존재할것입니다. 자연변환(Natural transformations)은 우리에게 이 관계를 이해하는데 도움을 줍니다. 이는 펑터의 특성을 유지시키는 펑터들의 매핑입니다.

두개의 카테고리 C, D 사이에 두개의 펑터 F, G가 있다고 가정합시다. C에 존재하는 하나의 대상 a에 집중하여 두 펑터에 의해 각각 Fa, Ga로 매핑될것입니다. 펑터의 매핑은 Fa를 Ga로 매핑합니다.

Fa와 Ga는 카테고리 D에 속한 대상입니다. 같은 카테고리 내에서 매핑은 카테고리의 범위를 어긋나서는 안됩니다. 이 객체들 사이에 인위적인 연결을 만들수는 없습니다. 그래서 존재하는 연결 - 사상을 이용하는것은 매우 natural 합니다. 자연변환은 즉 사상을 선택하는 것 입니다. 모든 대상 a에 대해서 Fa에서 Ga까지 하나의 사상을 선택합니다. 자연변환 𝛼라는 사상은 a에대한 𝛼의 구성요소 혹은 𝛼𝑎.라 합니다.

```
𝛼a :: Fa -> Ga
```

a는 카테고리 c의 대상이고 𝛼a은 카테고리 D의 사상이라는 점을 유의하세요. 𝛼a사상이 없다면 F와 G간의 자연변환이 존재하지 않는다는것을 뜻합니다.

펑터는 대상은 물론 사상도 매핑합니다. 자연변환은 이 매핑에서 어떤 역할을 할까요? 사상의 매핑은 고정되어 있습니다. F와 G사이의 자연변환 하에서 Ff는 Gf 로 변환되어야 합니다. 더욱이 펑터에 의한 사상의 매핑은 자연변환을 고려할때 선택권을 더욱 제한합니다.

```haskell
-- f :: a -> b
Ff :: Fa -> Fb
Gf :: Ga -> Gb
```

자연변환 𝛼에 의해 다음 두가지 사상이 제공합니다.

```
𝛼a :: Fa -> Ga
𝛼b :: Fb -> Gb
```

![](https://bartoszmilewski.files.wordpress.com/2015/04/3_naturality.jpg)

위에서 보듯이 이제 Fa에서 Gb로 가는 길이 두개 생겼습니다. 두개가 동일하다는 것을 보이기 위해서는 f를 들고있는 사상에 naturality condition을 부과해야합니다.

```
Gf . 𝛼a = 𝛼b . Ff
```

naturality condition은 매우 엄격한 조건 입니다. 예를들어 Ff의 역이 존재한다면 자연적으로 𝛼b은 다음과 같이 정의할 수 있습니다. 이는 f를 따라 𝛼a를 전송합니다.

```
𝛼𝑏 =(𝐺𝑓)∘𝛼𝑎 ∘(𝐹𝑓)−1
```

![](https://bartoszmilewski.files.wordpress.com/2015/04/4_transport.jpg)

두 대상사이에 역 사상 말고 더 많은 사상이 있을 수 있습니다. 일반적으로 사상에 역이 꼭 존재하지는 않습니다. 그러나 일반적으로 사상은 아니지만 두 펑터 사이의 자연변환의 존재는 보장되지 않는것을 알 수 있습니다. 따라서 자연 변형과 관련하여 희소하거나 풍부한 펑터가 작동하는 카테고리의 구조에 대해 많은것을 알수있습니다. 극한과 Yoneda lemma에서 더 많은 예를 볼것입니다.

구성요소적인 측면에서 자연변환을 보면 대상으로 사상으로 매핑하는 것으로 볼 수 있습니다. naturality 조건에 의하여 사상을 연결된 사각형으로 매핑한다고 볼수 도 있습니다. - 카테고리 C에 존재하는 모든 사상의 대해 카테고리 D에서는 연결된 사각형이 하나 있습니다.

![](https://bartoszmilewski.files.wordpress.com/2015/04/naturality.jpg)

이 자연변환의 속성은 많은 카테고리적 구조에 매우 유용합니다. 펑터를 신중하게 선택하면 이런 commutativity 조건 중 많은 부분이 naturality conditions으로 간주될 수 있습니다. limit, colimit, adjunction에서 더 많은 예제를 알아볼 것 입니다.

마지막으로 자연변환은 펑터의 동형을 정의하는데 쓰입니다. 두 펑터가 자연적으로 동형이란 말은 두개가 같다는 것을 의미합니다. 자연동형 사상(natural isomorphism) 구성 요소가 모두 동형인 자연변환으로 정의됩니다.(역이 존재하는 사상)



### 10.1 Polymorphic Functions

일전에 프로그래밍에서의 펑터에 역할에대해 알아봤습니다.(특히 엔도펑터에 대하여). 이것은 타입에서 타입을 매핑하는 타입 생성자와 같았습니다. 또한 고차함수 fmap을 이용하여 사상을 사상으로 매핑하기도 합니다.

대상을 시작으로 자연변환을 모델링해 봅시다. 타입 a가 있을때 Fa, Ga로 매핑하는 펑터 F, G가 있다고 합시다. 자연변환의 구성요소인 a에 대한 aplha는 하스켈에서 수도코드로 다음과 같습니다.

```haskell
alpha_a :: F a -> G a
```

자연변환은 모든 타입 a에 대하여 정의되어야하는 다형성 함수입니다.

```haskell
alpha :: forall a . F a -> G a
-- forall은 하스켈에서 옵셔널입니다.
alpha :: F a -> G a
```

a로 매개변수화된 함수들의 집합이라는것에 유의하세 이는 하스켈 구문의 간결함을 보여주는 한가지 예라 할 수 있습니다.

하스켈의 다형성 함수와 C++의 제네릭 함수간에는 보다 심오한 차이가 있습니다. 이러한 점이 기능이 구현되고 타입체크를 하는 방식에 반영됩니다. 하스켈에서 다형성 함수는 모든 타입에 대하여 동일하게 정의되어야합니다. 하나의 공식이 모든 타입에 작동해야합니다. 이를 parametric polymorphism라 부릅니다.

반면 C++은 디폴트  ad hoc polymorphism 이 지원됩니다 -> 이는 템플렛이 모든 타입에 대하여 정의될 필요가 없음을 뜻합니다. 템플렛이 주어진 타입에 작동하는지 여부는 인스턴스화 시점에 결정되고 구체적인 타입이 매개변수로 대체됩니다. 타입 체크가 동적이고 이는 종종 이해할 수 없는 에러를 발생시킵니다.

또한 C++에는 함수 오버로딩 및 템플릿 구체화를 위한 메커니즘이 있고 이는 같은 함수가 다른 타입에 대하여 다른 정의를 지니도록하게 합니다. 하스켈에서 이 기능은 타입클래스와 타입 패밀리에 의해 제공됩니다.

하스켈의 parametric polymorphism에 의하여 예측하지못한 결과가 발생합니다. 다음과 같은 다형성 함수에 대하여

```haskell
alpha :: F a -> G a
```

F, G가 펑터일때 이는 자동으로 자연변환을 만족합니다. 하스켈에서 펑터 G에 작동하는 사상 f는 fmap으로 구현됩니다.

```haskell
-- 𝐺𝑓 ∘ 𝛼𝑎 = 𝛼𝑏 ∘ 𝐹𝑓
-- fmap_G f . alpha_a = alpha_b . fmap_F f
-- 타입 추론에 의하여 어노테이션은 불필요
fmap f . alpha = alpha . fmap f
```

함수의 동등피교는 코드로 표현될 수 없기때문에 위는 하스켈 코드가 아닙니다. 그러나 이는 프로그래머가 equational reasoning에서 정체성으로 사용하거나 컴파일러에 의해 최적화 구현되는데 쓰입니다.

하스켈에서 자연변환이 자동인 이유는 "theorems for free"와 관련이 있습니다. Parametric polymorphism은 하스켈에서 자연변환을 정의하는데 쓰이고 모든 타입을 위한 하나의 공식이라는 점에서 구현을 하는데 매우 강력한 제한을 부과합니다. 펑터를 변환시키는 함수에대하여  free theorems은 naturaity conditions 입니다.

하스켈에서 펑터를 생각하는 방식을 컨테이너에 비유했었습니다. 자연변환에도 이 개념을 적용해 생각해봅시다. 자연변환은 컨테이너에 담긴 값을 빼내어 다른 컨테이너로 담는것과 같습니다. 내부 값을 수정하거나 새로운 값을 만들어내지 않습니다. 단지 새 컨테이너로 옮기는 작업을 합니다.

자연 변환은 fmap 적용을 통해 내부 값을 먼저 수정하고 다시 패키징 하거나 패키징한 다음에 fmap을 이용하여 내부 값을 수정하는것에 대해 상관 없습니다. 재포장,  fmapping 이 두가지 동작은 직교(orthogonal)합니다. 

하스켈에서 자연변환의 몇가지 예를 봅시다. 첫번째는 list와 Maybe 펑터 입니다. 리스트가 비어있지 않은 경우에만 리스트의 헤드를 반환하는 예제입니다.

```haskell
safeHead :: a -> Maybe a
safeHead [] = Nothing
safehead (x:xs) = Just x
```

모든 a에 대하여 위는 정의됩니다. 네추럴 컨디션을 증명해봅시다.

```haskell
-- fmap for list
fmap f [] = []
fmap f (x:xs) = f x : fmap f xs
-- fmap for Maybe
fmap f Nothing = Nothing
fmap f (Just x) = Just (f x)

-- naturality condition
fmap f . safehead = safehead . fmap f

fmap f (safeheader []) = famp f Nothing = Nothing
safehead (fmap f []) = safehead [] = Nothing

fmap f (safeheaer (x:xs)) = fmap f (Just x) = Just (f x)
safehead (fmap f (x:xs)) = safehead (f x: fmap f xs) = Just (f x)
```

재미있는 경우는 펑터 중 하나가 Const  펑터 인 경우 입니다. Const 펑터로 부터의 자연변환에서 펑터는 입력과 혹은 리턴타입이 다형성을 보입니다.

```haskell
-- list 펑터와 Const Int 펑터
length :: [a] -> Const Int a
length [] = Const 0
length (x:xs) = Const (1 + unConst (length xs))

unConst :: Const c a -> c
unConst (Const x) = x
```

실제 length 의 구현은 다음과 같습니다. 그리고 사실 이는 자연변환을 숨기고 있습니다.

```haskell
length :: [a] -> Int
```

Const 펑터에서 매개변수의 다형성을 찾는것은 좀 까다롭습니다. 그 이유는 nothing에 해당하는 값을 만들어내야하는 경우인데 아래와같이 할 수 있습니다.

```haskell
scam :: Const Int a -> Maybe a
scam (Const x) = Nothing
```

일전에 보았고 Yoneda lemma에서 중요한 역할을 하는 펑터는 Reader 펑터입니다.

```haskell
newtype Reader e a = Reader (e -> a)
```

이는 두 타입에 대해 정의되어있지만 두번째 타입에 대해서만(공변) 펑터적 성질을 지닙니다.

```haskell
instance Functor (Reader e) where
	fmap f (Reader e) = Reader (\x -> f(g x))
```

모든 타입 e에 대하여 Reader e가 어느타입 f 펑터로 대하여 자연변환 패밀리를 정의할 수 있습니다. 추후에 이 패밀리의 멤버는 언제나 f e의 원소와 일치한다는 것을 알아볼것입니다.

(생략)

### 10.2 Beyond Naturality

두 펑터 사이에 매개변수가 다형성을 지니는 함수는 언제나 자연변환을 만족합니다. 모든 대수적 데이터 타입은 펑터이기 떄문에 이 타입간 다형성 함수는 항상 자연변환입니다.

함수타입도 알아봤었습니다. 그리고 이것들은 리턴타입이 펑터적 특성을 지니는것을 보았습니다. 이를 사용하여 펑터를 구축하고 고차함수인 자연변환을 정의할 수 있습니다.

하지만 함수 타입은 인자 타입에 대하여 공변(covariant)이 아닙니다. 반변(contravariant)입니다. 물론 반변 펑터들은 반대의 카테고리에서 공변입니다. 두개의 반변성 펑터 사이의 다형성 함수는 여전히 범주적 의미에서 자연변형입니다. 하스켈 타입에서는 반대되는 범주의 펑터에서 작동하는 경우를 제외하고요

```haskell
newType Op r a -> Op (a -> r)
-- Op 펑터는 a에 대해 반변
instance Contravariant (Op r) where
	contramap f (Op g) = Op (g . f)
	
-- Op Bool -> Op String 다형성 함수를 정의한다치면
predToStr (Op f) = Op (\x -> if f x when "T" else "F")
```

두 펑터는 공변이 아니고 Hask에서 자연변환이 아닙니다. 하지만 두 펑터는 모두 반변이기 때문에 반대의 내추럴 조건을 만족합니다.

```haskell
contramap f . predToStr = predToStr . contramap f

-- constramap :: (b -> a) -> (Op Bool a -> Op Bool b)
```

공변이든 반변이든 펑터가 아닌 타입 생성자가 있습니다.

```haskell
a -> a
```

이는 펑터가 아닙니다. 동일한 타입 a가 반변,공변 위치에 쓰였기 때문입니다. 이 타입을 위해 fmap이나 contramap을 구현할 수 없습니다.

```haskell
(a -> a) -> f a
```

 따라서 f가 임의의 펑터일때 위의 함수는 자연변환이 아닙니다. 흥미롭게도 위와같은 경우 dinatural transformations라 부르는 자연변환의 일반화 케이스가 있습니다. 나중에 알아보죠(~~나중에 알아볼꺼면 나중에 알려줘요제발..~~)

### 10.3 Functor Category

이제 자연변환이라는 펑터간 매핑이 생겼습니다. 그러면 이 펑터들이 카테고리를 형성하냐 묻는것은 자연스러웁니다. 그리고 가능합니다. 카테고리 C, D에 대한 펑터를 위한 하나의 카테고리가 있습니다. 이 카테고리에서 대상은 펑터이고 사상은 자연변환입니다.

카테고리의 성질을 만족하려면 자연변환간의 합성을 정의해야합니다. 자연변환은 사상으로 간주하면 어떻게 합성하여야하는지 쉽게 보입니다.

```
𝛼𝑎 ∷ 𝐹𝑎 → 𝐺𝑎
𝛽𝑎 ∷ 𝐺𝑎 → 𝐻𝑎
// 𝛼와 𝛽를 합성해봅시다. 
𝛽𝑎 ∘ 𝛼𝑎 ∷ 𝐹 𝑎 → 𝐻 𝑎
```

위에서 만든 사상은 자연변환 𝛽 . 𝛼의 구성요소 입니다.

![](https://bartoszmilewski.files.wordpress.com/2015/04/5_vertical.jpg?w=300&h=203)

아랭의 다이어그램은 F에서 H의 자연변환임을 보입니다.

```
𝐻𝑓 ∘ (𝛽 ⋅ 𝛼)𝑎 = (𝛽 ⋅ 𝛼)𝑏 ∘ 𝐹𝑓
```



![](https://bartoszmilewski.files.wordpress.com/2015/04/6_verticalnaturality.jpg)

그들의 구성요소는 사상들 이기 때문에 자연변환은 결합법칙을 만족합니다.

마지막으로 각각의 펑터 F에 대하여 아이덴티티 자연변환이 존재합니다. 1𝐹로 나타내고 이들의 컴포넌트는 항등사상입니다.

```haskell
id_Fa :: Fa -> Fa
```

위의 자연변환 합성에 두가지 방법이 존재한다는 문제가 있습니다. 그중 하나는 Vertical composition이라 불립니다(펑터가 수직으로 쌓이는것처럼 합성된 경우). 수직적 합성은 펑터 카테고리를 정의하는데 매우 중요합니다. 반대의 경우 수평적 합성에 대해 짧게 설명하겠습니다.

![](https://bartoszmilewski.files.wordpress.com/2015/04/6a_vertical.jpg?w=220&h=145)

카테고리 C, D사이의 펑터 카테고리는 다음과 같이 씁니다. Fun(C, D) or [C, D] or D^C. 마지막 노테이션의 경우 펑터 카테고리 자체가 일부의 카테고리에서 하나의 함수 객체로 간주된다고 할 수 있습니다(익스포넨셜 형태) 진짜일까요?

지금까지 해왔던 추상화를 다시 돌아봅시다. 대상과 사상이 모인 카테고리에서 시작했었습니다. 카테고리(엄밀히 말하면 대상이 집합인 small category)들은 한단계 높은 레벨인 Cat 카테고리에서 대상으로 간주됩니다. 그리고 Cat에서 사상은 펑터입니다. 고로 Cat의 Hom-set은 펑터집합입니다. 예를들어 Cat(C, D)는 두 카테고리 C, D간의 팡터 집합입니다.

![](https://bartoszmilewski.files.wordpress.com/2015/04/7_cathomset.jpg?w=215&h=211)

펑터 카테고리 [C, D]도 마찬가지로 두 C, D 카테고리간 펑터들의 집합입니다(+ 자연변환은 사상임). 이 원소들은 Cat(C, D)의 멤버입니다. 더욱이 펑터 카테고리는 그 자체가 Cat의 대상이여야합니다(small 카테고리간의 펑터카테고리도 small이다). Hom-set 간 관계도 있고 동이란 대상이 카테고리에 있습니다. 이는 일전에 보았던 익스포넨셜 오브젝트와 일치합니다.

기억할지 모르겠지만 익스포넨셜 구조를 위해서는 product을 정의해야 하였습니다. Cat에서 그것은 매우 쉽습니다. small 카테고리는 대상들의 집합이고 집합간 Cartesian products을 어떻게 만들어야하는지 압니다. 즉 C x D 카테고리의 대상은 (c, d) 페어입니다. 동일하게 두 페어 (c, d), (c', d')사이의 사상에 대한 페어는 (f, g)입니다(f:: c -> c', g :: d -> d'). 이러한 쌍들은 구성요소별로 구성되며 항등사상의 쌍으로 이루어진 항등쌍이 있습니다. 요약하자면 Cat은 모든 범주 쌍에 대해 익스포넨셜 객체 D^C가 있는 완전한 카르테시안 폐쇄범주 입니다. 그리고 Cat의 대상은 카테고리고 D^C(C와 D간의 펑터) 도 카테고리 입니다.



### 10.4 2-Categories

Cat을 자세히 들여다 봅시다. Cat의 Hom-set은 펑터의 집합니다. 하지만 위에서 보았듯이 두 대상간 펑터는 집합에서의 구조보다 더 많은 정보를 지니고 있습니다. 자연변환이 사상역할을하며 카테고리를 구성합니다. 펑터가 Cat에서 사상으로 간주되기 때문에 자연변환은 사상간의 사상이 됩니다.

이 풍부한 구조는 2-카테고리의 예 입니다. 2-카테고리는 대상과 사상을 지니고 사상간 사상인 2-morphism가 존재하는 카테고리의 일반화 버전입니다.

Cat을 2-category로 볼때 다음이 존재합니다.

1. Objects: (Small) categories
2. 1-morphisms: Functors between categories
3. 2-morphisms: Natural transformations between functors.

![](https://bartoszmilewski.files.wordpress.com/2015/04/8_cat-2-cat.jpg?w=216&h=172)

카테고리 C, D간 홈셋 대신에 홈 카테고리 D^C 가 있습니다. 다음과 같은 펑터 합성이 있습니다. 카테고리 D^C의 펑터 F 카테고리 E^D의 펑터  G가 있을때 G.F는 E^C에서 나온 펑터. 그리고 또한 자연변환 사상들간(2-morphism)간의 수직 합성도 있습니다.

2-카테고리에 존재하는 두가지 합성방식(수직, 수평)에 의하여 다음과 같은 질문이 가능해집니다. 어떻게 두개가 상호작용할까?

```haskell
-- 1-morphisms in Cat
F :: C -> D
G :: D -> E
G . F :: C -> E

-- natural transformation alpha on F, beta on G
alpha :: F -> F'
beta :: G -> G'
```

![](https://bartoszmilewski.files.wordpress.com/2015/04/10_horizontal.jpg?w=300&h=166)

alpha와 beta는 각기 다른 펑터 카테고리의 멤버이기 때문에 합성할 수 없습니다. 하지만 F'와 G'는  합성 가능합니다. G'.F'와 G.F의 관계는 어떻게 나타낼까요?

![](https://bartoszmilewski.files.wordpress.com/2015/04/9_horizontal.jpg?w=369&h=268)

(각 화살표에 대한 설명 생략) 우리의 목표는 G(Fa)에서 G'(F'a)로 이르는 길을 찾는 것 입니다. 

```
-- 가능한 후보
𝐺′𝛼𝑎 ∘𝛽𝐹𝑎
𝛽𝐹′𝑎 ∘𝐺𝛼𝑎
```

위에서 만든 스퀘어는 베타에 대한 naturality square 이기 때문에 두 길은 같습니다.(죄다 생략..)

이 자연변환을 알파, 베타의 수평합성이라 부릅니다.

```
𝛽 ∘ 𝛼 ∷ 𝐺 ∘ 𝐹 → 𝐺′ ∘ 𝐹′
```

자연변환의 수직적 합성은 펑터 카테고리의 일부임을 보았었습니다. 그러면 수평적 합성은 어느 카테고리에 속합니까?

자연변환을 펑터간의 사상말고 카테고리간 사상이라 생각하고 보세요. 자연변환이 변형하는 펑터로 연결된 두 카테고리 사이에 있습니다. 이는 두 카테고리간의 연결로 볼 수 있습니다.

Cat의 두가지 대상인 C, D에 초점을 맞춥시다. C와 D를 연결하는 펑터 사이에는 일련의 자연변환이 있습니다. 그리고 이 자연변환은 C, D간의 새로운 화살표 입니다. 같은원리로 비슷한 자연변환이 D, E를 연결합니다. 자연변환은 이 화살표 간의 합성입니다.

또한 카테고리 C에서 C로 가는 아이덴티티 화살표도 있습니다. C의 아이덴티티 펑터를 그 자체로 매핑하는것은 아이덴티티 자연변환입니다. 수평적 아이덴티티 합성은 수직적 아이텐티티 합성과 동일하지만 반대는 아닙니다.

마지막으로 두 합성은 교환법칙을 만족합니다.

```
(𝛽′ ⋅𝛼′)∘(𝛽 ⋅𝛼) = (𝛽′ ∘𝛽)⋅(𝛼′ ∘𝛼)
```

미래에 유용히 쓰일 한가지 개념이 남았습니다. Cat을 새로운 측면에서 해석할때 대상에서 대상으로 이동하는 두가지 방식이 있습니다: 펑터를 이용하던지 자연변환을 이용하던지. 여기서 펑터를 특별한 종류의 자연변환으로 재해석합니다: 아이덴티티 자연변환이 펑터에 동작합니다. 추후에 이와같은 노테이션을 볼것입니다.

```haskell
𝐹∘𝛼
-- where F is a functor from D to E
-- and 𝛼 is a natural transformation between two functors going from C to D
```

펑터와 자연변환을 합성할 수는 없기 때문에 아이덴티티 자연변환 1F 와 알파의 수평적 합성으로 해석됩니다.



### 10.5 Conclusion

~~(결론만 보고싶네..)~~

파트1이 끝났습니다. 카테고리 이론의 기본을 배웠습니다. 카테고리의 대상을 명로 그리고 사상, 펑터, 자연변환을 동사로 생각 할 수 있습니다. 사상은 대상을 연결하고 펑터는 카테고리를, 자연변환은 펑터를 연결합니다.

한단계 추상화를 통해 대상이 어떻게 바뀌는지도 보았습니다. 사상의 집합은 함수 객체가 됩니다. 대상은 어떤 사상의 소스나 타겟이 될 수 있고 이것은 고차함수에 아이디어를 제공합니다.

펑터는 대상에서 대상을 매핑하기때문에 이를 타입 생성자나 매개변수 타입(parametric type)으로 사용할 수 있습니다. 펑터는 또한 사상도 매핑하고 이것은 fmap이라는 고차함수입니다. 간단한 종류의 펑터 Const, product, coproduct를 보았고 이들을 이용하여 많은 종류의 대수적 데이터 타입을 만들 수 있습니다. 함수 타입은 공변, 반변에 대하여 펑터적 성질을 지니고 있고 이것또한 대수적 데이터 타입으로 확장시킬 수 있습니다.

펑터는 펑터 카테고리에서 대상으로 간주됩니다. 또한 그들은 자연변환 이라는 사상에서 소스, 타겟 객제가 됩니다. 자연변환은 다형성 함수의 특별한 타입입니다.


