# 디자인 패턴

## 싱글톤 패턴
게임에서 유일한 인스턴스를 만드는 방식(단일 객체)이며 전역적인 접근이 필요한 방식이다. 클래스의 인스턴스가 하나만 생성되도록 보장하고, 어디서든 동일한 인스턴스에 접근 할 수 있도록 한다.
- 게임매니저, 자원관리즈 등

## 상태 패턴
오브젝트의 동작이 상태에 따라 달라지는 경우 사용하는 패턴이며 각 상태를 클래스로 구현하고 상태에 따라 다른 동작을 수행하게 한다.   
캐릭터의 상태를 객체로 구현하면 새로운 상태가 추가되었을 때 상태를 사용하는 캐릭터 클래스를 많이 수정 할 필요가 없이 유연하게 대처가 가능하다.

- 캐릭터의 이동 상태, 공격상태, 대기상태 다루기 유용

## 오브젝트 풀 패턴
반복적으로 생성되고 소멸되는 객체를 효율적으로 관리하기 위한 패턴. 미리 생성된 객체들을 풀에 저장하고 필요할 때마다 객체를 재사용해 생성과 소멸의 오버헤드를 줄임

## 컴포넌트 패턴
오브젝트의 동작과 기능을 구현하는데 사용되는 패턴. 게임의 오브젝트는 여러개의 컴포넌트로 구성되며 독립적으로 동작하고 상호작용한다. 
자동차라는 객체가 있을 경우 이 객체를 만들 때 엔진객체, 휠 객체, 브레이크 객체 등 세분화된 객체를 조립해 하나의 객체를 구성하는 방법
- 유니티 엔진에서 만드는 객체들이 예시이다. 캐릭터를 만들고 필요에 따라 물리객체, 네트워크 관련 객체 등을 붙여서 원하는 객체를 만들어낸다.

## 옵저버 패턴
객체간의 일대 다 관계를 구성해 한 객체의 상태 변화에 따라 다른 객체들이 자동으로 업데이트 되도록 하는것을 목적으로 함.   
주제(Subject)와 옵저버(Observer) 로 구성된다.   
주제는 상태를 가지며 상태가 변경될 때 옵저버에게 알린다.   
옵저버는 주제를 구독하고 주제의 상태가 변경되면 업데이트를 수신해 동작을 수행한다.   
- 플레이어 정보 UI의 경우 플레이어의 정보를 항시 받아 출력하는것 보다 변동사항이 있을 때만 변동사항이 있다는 것을 객체들에게 전달하면 객체들의 결합도를 낮추고 유연성 및 확장성을 제공 할 수 있다.

## 팩토리 패턴
상속을 통해서만 인스턴스를 양산하면, 유형별로 클래스가 많이 생기고 각각의 클래스마다 가져야 하는 값이나 구현방법을 찾아야 한다.  
상속이 아닌 다형성확보를 통해 만드는경우, 매번 생성마다 각각의 필드를 지정해 주어야하고, 다른 값을 집어넣어서 상이한 데이터를 가지는 같은 유형의 객체를 만들어야 하는 경우가 있을 수 있다.   
이때 팩토리 패턴을 사용하면 인스턴스 생성 메서드를 활용해 객체를 만들 수 있다. 

#### 사용처
- 같은 클래스에 다른 유형의 인스턴스를 만들 때 좋다.
- 생성 과정을 팩토리에서만 관리해서 단일책임 원칙을 준수한다.
- 팩토리에서 생성과정을 담당해 개방폐쇄원칙을 준수한다.

#### 사용 예시

```c#
using System.Runtime.CompilerServices;
using System.Security.Cryptography.X509Certificates;
using static DesignPattern.Item;

namespace DesignPattern
{
    // 상속을 통해서만 아이템 종류를 양산하면
    // 1. 유형별로 클래스가 너무 많이 생김
    // 2. 각각의 클래스마다 가져야 하는 값이나 구현방법들을 찾아야함

    // 상속이 아닌 다형성확보를 통해 만드는 경우
    // 1. 매번 생성마다 각각의 필드를 지정해줘야함
    // 2. 다른 값을 집어넣어서 상이한 데이터를 가지는 같은 유형의 객체가 있을 수 있다.
    internal class Program
    {
        static void Main(string[] args)
        {
            Item potion1 = ItemFactory.Instantiate("포션");
            Item potion2 = ItemFactory.Instantiate("큰 포션");
        }
    }

    public class ItemFactory

        //아이템 테이블 (단일책임)
        // 견본품   (프로토타입)
        // 추가과정 (팩토리메서드)
        // 제작부품 (빌더)
    {
        public static T Instantiate<T>(string name) where T : Item //제약조건을 걸어 형변환이 불가능한 상황을 받지 않는다
        {
            if (name == "포션")
            {
                Potion potion = new Potion();
                potion.name = "포션";
                potion.weight = 3;
                potion.image = "유리병에 담긴 빨간액체";
                potion.hp = 30;
                return potion as T;
            }
            else if (name == "큰포션")
            {
                Potion potion = new Potion();
                potion.name = "큰포션";
                potion.weight = 10;
                potion.image = "뚱뚱한 유리병에 담긴 빨간액체";
                potion.hp = 100;
                return potion as T;
            }
            else
            {
                Console.WriteLine("해당 이름의 아이템이 없습니다.");
                return null;
            }
        }

        // enum { 큰포션, 작은포션,노랑포션}
        public static Item Instantiate(string name)
        {
            if (name == "포션")
            {
                Potion potion = new Potion();
                potion.name = "포션";
                potion.weight = 3;
                potion.image = "유리병에 담긴 빨간 액체";
                potion.hp = 30;
                return potion;

            }
            else if (name == "큰 포션")
            {
                Potion potion = new Potion();
                potion.name = "큰포션";
                potion.weight = 10;
                potion.image = "뚱뚱한 유리병에 담긴 빨간 액체";
                potion.hp = 100;
                return potion;
            }
            else
            {
                Console.WriteLine("그 아이템은 없습니다.");
                return null;
            }
        }
    }

    public class Item
    {
        public string name;
        public int weight;
        public string image;

        public Item()
        {
            this.name = "아이템";
            this.weight = 1;
            this.image = "기본 이미지";
        }

        public class Potion : Item
        {
            public int hp;           
        }
    }    
}
```

## 빌더
복잡한 객체를 단계별로 생성할 수 있도록 하는 생성 디자인 패턴으로 같은 제작코드를 사용하여 다양한 유형들의 표현을 제작 할 수 있다.   
빌더 패턴은 자신의 클래스에서 객체 생성 코드를 추출해 빌더라는 별도의 객체들로 이동하도록 한다.   
객체를 생성하고 싶다면 빌더 객체를 실행하여 생성하면 되며 모든 단계를 호출 할 필요 없이 객체의 특정 설정을 제작하는데 필요한 단계만을 호출할 수 있다.

### 빌더 패턴 예시
```c# 
using System.Text;

namespace _02._Builder
{
    internal class Program
    {
        static void Main(string[] args)
        {
            //체인 메서드
            StringBuilder sb1 = new StringBuilder();
            sb1.AppendLine("안녕하시오").AppendLine("반갑소").AppendLine("");

            OrcBuilder warriorOrcBuilder = new OrcBuilder();
            warriorOrcBuilder.SetName("오크 전사");
            warriorOrcBuilder.SetHP(300);

            OrcBuilder archorOrcBuilder = new OrcBuilder();
            archorOrcBuilder.SetName("오크 궁수");
            archorOrcBuilder.SetWeapon("나무 활");
            archorOrcBuilder.SetLevel(10);

            OrcBuilder shamanOrcBuilder = new OrcBuilder();
            shamanOrcBuilder.SetName("오크 주술사");
            shamanOrcBuilder.SetWeapon("저주받은 지팡이");
            shamanOrcBuilder.SetArmor("의식복");
            shamanOrcBuilder.SetHP(50);

            OrcBuilder chiefShamanOrcBuilder = new OrcBuilder();
            chiefShamanOrcBuilder.SetName("오크 주술사 족장");
            chiefShamanOrcBuilder.SetWeapon("의식의 지팡이");
            chiefShamanOrcBuilder.SetArmor("족장의 옷");
            chiefShamanOrcBuilder.SetHP(100);


            Orc[] orcs = new Orc[9];

            //Orc orc1 = warriorOrcBuilder.Build();
            //Orc orc2 = warriorOrcBuilder.Build();
            //Orc orc3 = warriorOrcBuilder.Build();

            //Orc orc4 = archorOrcBuilder.Build();
            //Orc orc5 = archorOrcBuilder.Build();
            //Orc orc6 = archorOrcBuilder.Build();

            //Orc orc7 = shamanOrcBuilder.Build();
            //Orc orc8 = shamanOrcBuilder.Build();
            //Orc orc9 = shamanOrcBuilder.Build();
             orcs[0] = warriorOrcBuilder.Build();
             orcs[1] = warriorOrcBuilder.Build();
             orcs[2] = warriorOrcBuilder.Build();
                
             orcs[3] = archorOrcBuilder.Build();
             orcs[4] = archorOrcBuilder.Build();
             orcs[5] = archorOrcBuilder.Build();
                
             orcs[6] = shamanOrcBuilder.Build();
             orcs[7] = shamanOrcBuilder.Build();
             orcs[8] = shamanOrcBuilder.Build();

            OrcBuilder uniqueOrcBuilder = new OrcBuilder();
            uniqueOrcBuilder
                .SetName("희귀 오크")
                .SetWeapon("희귀 무기")
                .SetArmor("희귀 옷")
                .SetHP(50);

            // 스트링 빌더도 빌더다
            StringBuilder sb2 = new StringBuilder();
            sb2.AppendLine("안녕하세요");
            sb2.AppendLine("반갑습니다"); // 조립과정
            string str = sb2.ToString(); // 결과물

            // 서브웨이 : 빌더
            // 맥도날드 : 팩토리
        }
    }

    public class OrcBuilder
    {
        public string name;
        public string weapon;
        public string armor;
        public int level;
        public int hp;

        public OrcBuilder()
        {
            name = "오크";
            weapon = "몽둥이";
            armor = "천옷";
            level = 1;
            hp = 100;
        }

        public Orc Build()
        {
            Orc orc = new Orc();
            orc.name = name;
            orc.weapon = weapon;
            orc.armor = armor;
            orc.level = level;
            orc.hp = hp;

            return orc;
        }

        //public void SetName(string name)
        //{
        //    this.name = name;
        //}

        // 자기 자신을 결과로 주는 체인 메서드 방식, 기존처럼 쓰는것도 지장없음
        public OrcBuilder SetName(string name)
        {
            this.name = name;
            return this;
        }

        public OrcBuilder SetWeapon(string weapon)
        {
            this.weapon = weapon;
            return this;
        }

        public OrcBuilder SetArmor(string armor)
        {
            this.armor = armor;
            return this;
        }

        public void SetLevel(int level)
        {
            this.level = level;
        }

        public void SetHP(int hp)
        {
            this.hp = hp;
        }
    }

    public class Orc
    {
        public string name;
        public string weapon;
        public string armor;
        public int level;
        public int hp;
    }
}
```


### 팩토리 패턴과 빌더의 차이점
팩토리 메서드 패턴은 객체 생성을 위한 인터페이스를 정의하고, 객체 생성을 서브 클래스에 위임하는 패턴이다.  
- 팩토리는 제품 표가 있어 미리 생산될 제품이 준비 된 경우
이에 비해 빌더 패턴은 객체 생성 과정을 다루는 패턴으로, 객체 생성을 단계적으로 수행한다    
- 빌더의 경우 뼈대가 있는 상황에서 여러 요소를 붙여줄 수 있는 경우
