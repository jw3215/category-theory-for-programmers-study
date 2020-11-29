## 8. Functoriality

몇개지 예를 통하여 펑터가 무엇인지 알아봤었습니다. 이제 작은 펑터로 부터 더 큰 펑터를 어떻게 만드는지 알아봅시다. 특별히 어떤 타입 생성자(카테고리 대상간 매핑에 해당하는)가 펑터(사상의 매핑도 포함하는)로 확장 될 수 있는지 말입니다.



### 8.1 Bifunctors

펑터는 Cat(카테고리의 카테고리)에서의 사상이기 때문에 사상에 대한 많은 직관들이(특히 함수에 대한) 펑터 자체에도 적용됩니다. 예를들어 두개의 인자를 받는 함수가 있을때 두 인자의 펑터 혹은 bifunctor를 가질 수 있습니다. 대상에게  바이펑터는 모든 쌍의 대상(하나는 카테고리 C에서, 다른 하나는 카테고리 D 에서)을 카테고리 E의 어떤 대상으로 매핑합니다. 이것은 카테고리의 Cartesian product C x D 에서 E로의 매핑 입니다.

![](https://bartoszmilewski.files.wordpress.com/2015/01/bifunctor.jpg?w=300&h=286)

이것은 매우 직관적 입니다. 하지만 펑터적 성질(functoriality)은 바이펑터가 사상도 매핑해야함을 의미합니다. 이경우에 마찬가지로 두개의 사상(각 카테고리 C, D에서)을 카테고리 E의 특정 사상으로 매핑말입니다.

다시말하지만 두 사상의 쌍은 CxD product 카테고리에서 E 카테고리까지 하나의 사상 이라는 점 입니다. 범주의 cartesian product에서 사상을 한쌍의 사상으로 정의합니다. - 한 쌍의 대상에서 다른 쌍의 대상으로 가는. 이 사상 쌍은 아래와같이 합성할 수 있습니다.

```haskell
(f, g) . (f', g') = (f.f', g.g')
```

합성은 결합법칙을 만족하고 identity도 지니고 있습니다. (Identity 사상의 페어는 (id, id)이기 때문에). 그러기 때문에 카테고리의 Cartesian product는 진정 카테고리 입니다.

바이펑터를 더 쉽게 생각하는 방법은 각 아규먼트에 따라서 다르게 펑터를 고려하는 것 입니다. 그렇기 때문에 functorial laws를(결합법칙과 identity 보존) 펑터에서 바이펑터로 변환하는 대신에 각 아규먼트에 별로 따로 체크하는 것만으로도 충분합니다. (하지만 일반적으로 분리된 funtoriality는 joint functoriality를 증명하는것에는 충분하지 않습니다. Joint functoriality가 실패하는 카테고리는 premonoidal이라 불립니다.)

하스켈에서 바이펑터를 정의해 봅시다. 이경우에 나오는 3가지 카테고리는 모두 하스켈 타입의 카테고리 입니다. 바이펑터는 두가지 타입을 받는 타입 생성자 입니다. 다음은 Control 라이브러리에서 가져온 바이펑터 타입 클래스의 정의 입니다.

```haskell
class Bifunctor f where
	bimap :: (a -> c) -> (b -> d) -> f a b -> f c d
	bimap g h = first g . second h
	first :: (a -> c) -> f a b -> f c b
	first g = bimap g id
	second :: (b -> d) -> f a b -> f a d
	second = bimap id
```

![bimap](https://bartoszmilewski.files.wordpress.com/2015/01/bimap.jpg)

타입 변수 f는 바이펑터를 나타냅니다. 모든 타입의 시그니처에서 항상 두 타입 인수에 적용됨을 볼 수 있습니다. 첫번쨰 타입 시그니처는 두 함수를 동시에 매핑하는 것으로 bimap을 정의합니다. 결과는 바이펑터의 타입 생성자에 의해 만들어진 타입에 작동하는 리프팅된 함수입니다.( f a b -> f c d). first, second라는 측면으로 bimap이 기본구현 되어 있습니다.(위에서 언급했듯이 이것은 언제나 적용되지는 않습니다. first g . second h는second h . first g와 항상 같지는 않기 때문입니다.)

두개의 다른 타입 시그니처 first, second는 각각 첫번쨰, 두번쨰 인수에 대한 f의 펑터적 성질을 확인해주는 fmap 입니다.

![](https://bartoszmilewski.files.wordpress.com/2015/01/first.jpg?w=150&h=124)![](https://bartoszmilewski.files.wordpress.com/2015/01/second.jpg?w=150&h=138)

(좌측: first, 우측: second )

타입 클래스의 정의는 bimap 측면에서 두가지 기본 구현을 제공합니다.

Bufunctor의 인스턴스를 선언할떄, bimap 구현하고 first, second의 기본구현을 사용하거나 first, second를 구현하고 bimap의 디폴트 구현을 사용하던가 해야합니다.(물론 이 3가지 모두 구현할 수 있습니다.)

### 8.2 Product and Coproduct Bifunctors

바이펑터의 중요한 예는 카테고리적인 product 입니다. (universal construction에 의해 정의된 두 대상간의 product) 만일 어떤 대상의 쌍에서든 product이 존재한다면 이 대상들로 부터 곱 까지의 매핑은 bifunctorial 입니다. 이는 보편적 그리고 특별히 하스켈에서 참 입니다. 다음은 가장 단순한 product 타입 pair 생성자에 대한 Bifunctor 인스턴스 입니다.

```haskell
instance Bifunctor (,) where
	bimap f g (x, y) = (f x, g y)
	-- bimap이 단순하게 첫번쨰 함수를 pair의 첫번쨰 인자에, 두번쨰 함수를 pair의 두번째 인자에 적용합니다.
	-- bimap :: (a -> c) -> (b -> d) -> (a, b) -> (c, d)
	-- f :: (a -> c), g :: (b -> d) 이 bmap에 의하여 쌍으로 변환
```

쌍대성에 의하여 카테고리에서 어떤 대상 쌍에 대하여 coproduct가 정의된다면 이것또한 bifunctor 입니다.하스켈에서 Bifunctor의 인스턴스인 Either 타입 생성자를 이용하여 예를 들을 수 있습니다.

```haskell
instance Bifunctor Either where
	bimap f _ (Left x) = Left (f x)
	bimap _ g (Right y) = Right (g y)
```

~~모노이드 카테고리(monoidal category)에 대하여 이야기했던것이 기억납니까? 모노이드 카테고리는 유닛 오브젝트와 함께 대상에 대한 binary operator를 정의합니다.  일전에 Set은 싱글톤 셋이 unit으로 작동하는 카르테시안 곱에서 모노이드 범주가 됩니다. 마찬가지로 엠티셋이 unit으로 작동하는 disjoint union에서 모노이드 범주가 된다 언급했었습니다. 그때 언급하지 않았던 모노이드 카테고리의 요구사항 중 하나가 binary operator가 bifunctor가 된다는 것 입니다. 이는 매우 중요합니다. monoidal product이 사상에 의해 정의된 카테고리의 구조와 호환되기를 원합니다. 이로써 모노이드 카테고리의 완전한 정의에 한발짝 더 가까워 졌습니다.~~

### 8.3 Functorial Algebraic Data Types

펑터로 판명된 매개변수화된 몇가지 타입의 예를 보았습니다. 복잡한 데이터 타입은 단순한 타입의 데이터로 만들어집니다. 특별히 대수적인 데이터 타입들은 (ADTS) sum과 product을 이용하여 만들어 집니다. sum과 product이 펑터적 성질을 지니는지 보았고 펑터를 합성하는것도 압니다. -> **ADTS를 만드는 방식이 펑터적이라는 것을 보았고 이제 ADTS도 펑터적 성질을 지닌다는것을 볼것입니다.**

매개변수화된 ADTS를 만드는 단위(or 구성요소)는 무엇일까요? 우선 펑터의 타입 매개변수에 의존을 지니지 않는 항목들이 있습니다: Maybe에서 Nothing, List에서 Nil 처럼. 이것들은 Const functor와 비슷합니다(Const functor는 타입 파라미터를 무시합니다)

그리고나서 단지 타입 파라미터를 캡슐화 시키는 항목이 있습니다: Maybe에서의 Just 처럼. 이것들은 Identity functor와 동일합니다. 일전에 Cat에서 identity 사상으로 identity functor를 언급했었습니다. 아래는 하스켈에서의 정의입니다.

```haskell
data Identity a = Identity a

instance Functor Identity where
	fmap f (Identity x) = Identity (f x)
```

Identity가 불변한 값 a를 단순히 저장하는 역할만 한다고 생각할수도 있습니다.

대수적 데이터 구조에서 모든것은 이 두가지 기본 요소를 sum과 product를 이용하여 구성됩니다.

```haskell
data Maybe a = Nothing | Just a
-- maybe는 두 타입의 sum입니다. + sum은 펑터적 성질을 지닙니다.
```

Maybe에서 Nothing은 Cons ( ) a 와 같습니다. 두번째 는 단지 다른 이름의 Identity functor로 볼 수 있습니다.

```haskell
type Maybe a = Either (Const () a) (Identity a)
```

Maybe는 두 펑터( Const ( ), Identity) 와  바이펑터 (Either)의 합성입니다.

펑터의 합성은 펑터라는 것을 보았습니다. 바이펑터의 경우도 동일합니다. 이제 알아봐야 할것은 사상에 대해 동작하는 두개의 펑터가 있는 바이펑터의 합성이 어떨것 일것 이냐는 겁니다. 우선 두개의 사상을 각자 다른 펑터로 리프팅 하고 결과 쌍을 바이펑터를 이용하여 리프팅 합니다.

위와같은 합성을 하스켈에서 정의해 봅시다.

```haskell
newtype BiComp bf fu gu a b = BiComp (bf (fu a) (gu b))
-- 두개의 펑터, fu, gu와 두개의 타입 a, b를 받음
-- fu를 a에, gu를 b에 적용한 결과값을 bf로 적용.
```

새로운 타입 BiComp는 a와 b에 대한 바이펑터 입니다.(bf가 바이펑터고 fu, gu는 펑터). 컴파일러는 bf에 사용할 수 있는 bimap의 정의가 있음을 그리고 fu, gu에 해당하는 fmap이 있음을 알아야 합니다. 하스켈에서 이것은 인스턴스 선언의 전제 조건으로 표현됩니다.(이중화살표 뒤에 클래스의 제약조건들을 나열)

```haskell
instance (Bifunctor bf, Functor fu, Functor gu) => 
	Bifunctor (BiComp bf fu gu) where
		bimap f1 f2 (BiComp x) = BiComp ((bimap (fmap f1) (fmap f2)) x)
```

데이터 스트럭처에 펑터를 이끌어 내는것은 하스켈의 특정 extension을 이용하여 다음과 같이 정의할 수 있습니다.(펑터 말고도 앞서 언급하였던 Eq 타입 클래스를 포함란 여러 다른 타입 클래스 인스턴스를 유도할 수 있게 합니다. )

```haskell
{-# LANGUAGE DeriveFunctor #-}

data Maybe a = Nothing | Just a deriving Functor
```



### 8.4 Functors in ~~C++~~(Swift)

```haskell
-- Tree in haskell
data Tree a = Leaf a | Node (Tree a) (Tree a)
--	deriving Functor
	
instance Functor Tree where
	fmap f (Leaf a) = Leaf (f a)
	fmap f (Node t t') = Node (fmap f t) (fmap f t')
```

```swift
// Tree in swift
indirect enum Tree<A> {
  case leaf(A)
  case node(Tree<A>, Tree<A>)
}

func fmap<A, B>(tree: Tree<A>, function: (A) -> B) -> Tree<B> {
    switch tree {
    case let .leaf(a):
        return .leaf(function(a))
        
    case let .node(lhs, rhs):
        return .node(fmap(tree: lhs, function: function),
                     fmap(tree: rhs, function: function))
    }
}
```



### 8.5 The Writer Functor

일전에 이야기했던 클라이슬리 카테고리에서 사상은(Writer을 리턴하는) embellished된 함수로 나타났었습니다.

```haskell
type Writer a = (a, String)
```

embellishment는 endofunctor와 관련이 있습니다. 그리고 실제 Writer타입 생성자는 a의 펑터 입니다. 이는 매우 단순한 product 타입이기 떄문에 fmap을 구현하지 않았습니다.

하지만 클라이슬리 카테고리와 펑터와의 일번적인 관계는 무엇입니까? 클라이슬리 카테고리가 카테고리가 되기 위하여 identity와 합성을 아래와 같이 정의했었습니다.

```haskell
-- 합성
(>=>) :: (a -> Writer b) -> (b -> Writer c) -> (a -> Writer c)
m1 >=> m2 = \x ->
	let (y, s1) = m1 x
			(z, s2) = m2 y
	in (z, s1 ++ s2)
	
-- identity
return :: a -> Writer a
return x = (x, "")
```

fmap의 역할을 할 올바른 타입 시그니처를 가진 함수를 생성하기 위해 이들을 다음과 같이 결합할 수 있습니다.

```haskell
fmap f = id >=> (\x -> return (f x))
-- id 함수와 람다 아규먼트에 대하여 f를 적용한 결과값을 return에 적용한 함수를 합성
-- id는 writer a를 받아 writer a로 반환, fish 오퍼레이터는 a값을 람다의 x로 전달
-- f는 a를 b로 바꾸고 return으로 embellish하여 Writer b를 만듬
-- 결론적으로 Writer a를 Writer b로 반환 -> fmap
```

Writer를 확장하여 어느타입의 생성자로 교체할 수 있습니다. fish오페레이터와 return을 지원하는한 fmap 또한 정의할 수 있습니다. 이러기때문에 클라이슬리 카테고리는 항상 functor 입니다.(모든 펑터가 클라이슬리 카테고리를 발생시키는것은 아닙니다.)

~~deriving Functor를 통하여 불러오는 fmap과 위에서 정의한 fmap이 동일한것인지 궁금해할 수 있습니다. 흥미롭게도 그렇습니다. 이는 하스켈의 다형성 함수로 인해 가능합니다 이를 parametric polymorphism이라 부르고 theorems for free 라 불리는 것의 근원입니다. 이 정리가 말하는것은 어떤 타입 생성자에 대한 fmap의 구현이 존재할 경우에 그것은 고유해야 한다는 점 입니다.~~

### 8.6 Covariant and Contravariant Functors

이번에는 reader functor로 다시 돌아가 봅시다. 리더 펑터에서 화살표는 두번쨰 어규먼트에 대한 펑터적 성질을 지닙니다.

```haskell
-- (->) a b = a -> b
-- 화살표(->)는 a, b타입을 받는 타입 생성자: a -> b 형식의 함수를 만들어냄
-- (-> ) r은 타입 인자를 하나 받아서 새로운타입(함수)를 리턴하는 타입 생성자
(->) r

type Reader r a = r -> a

instance Functor (Reader r) where
	fmap f g = f . g
```

페어의 타입 생성자나 Either의 타입 생성자와 같이 함수의 타입 생성자는 두개의 타입을 입력받습니다. 페어나 Either는 두개의 어규먼트에 대하여 펑터적 성질을 지닙니다. - 이것들은 바이펑터 입니다. 그러면 위의 함수 생성자도 바이펑터 일까요?

첫번쨰 아규먼트 r에 대해서 펑터를 만들어 봅시다. 

```haskell
-- 리턴 타입의 아규먼트를 뒤집었음, 이경우에 리턴타입 r이 고정이고 a타입이 가변임
type Op r a = a -> r

-- 원래는
-- fmap :: (a -> b) -> f a -> f b
-- f가 (-> r)이면
-- fmap :: (a -> b) -> (->) r a -> (->) r b
-- fmap :: (a -> b) -> (r -> a) -> (r -> b)

-- fmap을 구현하기 위해 다음과 같은 타입 시그니처를 어떻게 만존시킬 수 있을까
fmap :: (a -> b) -> Op r a -> Op r b
fmap :: (a -> b) -> (a -> r) -> (b -> r)
```

a -> b로 가는 함수와 a -> r인 함수를 합쳐 b -> r을 만들수는 없다. 최초의 화살표 a -> b를 뒤집으면 위의 관계가 만족될 수 있다. 그렇다고 임의의 함수를 뒤집을 수 없다, 하지만 카테고리를 뒤집어 생각해 볼 수 있다.

(recap) 모든 카테고리 C에는 쌍 카테고리 𝐂op 가 있습니다. 이 카테고리에서 대상은 C와 동일하지만 사상들은 모두 반대방향입니다. 이 Cop 카테고리에서 다른 카테고리 D로 이동하는 펑터가 있다 가정해보세요

```haskell
F :: Cop -> D
--Cop의 사상 fop :: a -> b를 펑터가 카테고리 D로 다음과 같이 매핑
-- Ffop :: F a -> F b
-- fop 사상은 카테고리 C과 역방향이고 C에서는 다음과 같음
-- f :: b -> a
```

F는 일반적인 펑터이지만 F에 따라 다른 종류의 매핑을 정의할 수 있습니다(펑터는 아닙니다). 그것을 G라 부르기로 합시다. G는 C에서 D로의 매핑을 합니다. G는 F와 동일하게 대상을 매핑하지만 사상을 매핑하는 경우에는 방향을 뒤집습니다. 

```haskell
-- 카테고리 C에서 f
-- f :: b -> a
Gf :: (b -> a) -> (G a -> G b)
-- Ff의 결과 사상과 방향이 반대
```

이는 뒤틀린 펑터 입니다. 이러한 방식으로 사상을 뒤집는 범주 매핑을 contravariant functor라 부릅니다. (일반적인 펑터는 covirant functor라 부릅니다) Contravariant functor는 반대 카테고리(원래 카테고리)에서는 일반적인 펑터입니다.

![](https://bartoszmilewski.files.wordpress.com/2015/01/contravariant.jpg?w=300&h=295)

하스켈에서 contravariant funtor의 타입클래스 정의는 다음과 같습니다.

```haskell
class Contravariant f where
	contramap :: (b -> a) -> (f a -> f b)
	
-- 앞서 정의한 타입 생성자 Op는 Contravariant의 인스턴스일 수 있습니다.
instance Contravariant (Op r) where
	-- (b -> a) -> Op r a -> Op r b
	contramap f g = g . f
```

Op에 대한 콘트라맵의 정의가 단순히 인수가 뒤집힌 함수 구성 연산자 일 뿐이라는 것을 알면 위의 표현은 더 간결해질 수 있습니다.

```haskell
-- 어규먼트를 뒤집는 flip이라 불리는 특별한 함수
flip :: (a -> b -> c) -> (b -> a -> c)
flip f y x = f x y

contramap = flip(.)
```



### 8.7 Profunctors

함수-화살표 연산자가 첫번쨰 인자에 대해서는 반변(contravariant) 하고 두번쨰 인자에 대해서는 공변(covariant) 하다는 것을 보았습니다. 이런 흉측한? 괴물?을 뭐라 부를까요? 타켓 카테고리가 Set인 경우 이와같은 괴물을 profunctor라 합니다.

```haskell
-- 타겟 카테고리가 Set인 경우
Cop x D -> Set
```

```haskell
class Profunctor p where
	dimap :: (a -> b) -> (c -> d) -> p b c -> p a d
	dimap f g = lmap f . rmap g
	lmap :: (a -> b) -> p b c -> p a c
	lmap f = dimap f id
	rmap :: (b -> c) -> p a b -> p a c
	rmap = dimap id
```

이제 함수-화살표 생성자는 Profunctor의 인스턴스로 구현할 수 있습니다.

```haskell
instance Profunctor (->) where
	dimap ab cd bc = cd . bc . ab
	lamp = flip (.)
	rmap = (.)
```



### ~~8.8 The Hom-Functor~~