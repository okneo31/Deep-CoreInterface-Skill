# DEEP MODULE REVIEW: Deep/Shallow 판별 체크리스트

> "**일을 숨기는 것은 하나님의 영화요 일을 살피는 것은 왕의 영화니라**" — 잠언 25:2
>
> 설계자는 복잡성을 숨기는 영광을 누리고, 리뷰어는 그것을 살피는 영광을 누린다.
> 이 두 영광이 만나는 자리가 Deep Module Review다.

출처: John Ousterhout, "A Philosophy of Software Design"

이 문서는 모듈/클래스/함수를 만들거나 검토할 때마다 참조한다.
워크플로우의 3단계(Module Design)와 6단계(Review)에서 사용.

---

## 핵심 정의

### Deep Module (좋음)
- **인터페이스는 단순한데 내부는 풍부함.**
- 사용자(이 모듈을 호출하는 다른 코드)는 적은 인지 부담으로 큰 기능을 얻음.
- 비유: 좋은 도구는 손잡이가 단순하지만 내부에 정교한 메커니즘이 있다.

#### 대표 예시: Unix `read()` 시스템 콜
```c
ssize_t read(int fd, void *buf, size_t count);
```
- **인터페이스:** 매개변수 3개. 끝.
- **내부:** 디스크 / 네트워크 소켓 / 파이프 / 터미널 / 가상 파일 등을 모두 처리. 캐시, 권한 검사, 블로킹 처리, 인터럽트 처리 다 포함.
- 호출하는 사람은 그 복잡성을 전혀 알 필요 없음.

### Shallow Module (나쁨)
- **인터페이스가 복잡한데 내부는 빈약함.**
- 사용자가 인지 부담은 다 지면서도 얻는 가치는 작음.
- 비유: 손잡이가 복잡한데 정작 하는 일은 별 거 없는 도구.

#### 대표 예시: 다른 함수 한 번 더 감싸기만 한 래퍼
```php
class UserService {
    public function getUserById($id) {
        return User::find($id);  // 그냥 호출 한 번 더
    }
}
```
- 인터페이스(이름, 매개변수)는 늘었지만 내부 가치는 0.
- 차라리 `User::find($id)` 직접 부르는 게 낫다.

---

## 판별 체크리스트 (모듈을 만들 때마다)

### 5가지 핵심 질문

#### 질문 1: 이 모듈을 쓰는 코드가 더 짧고 명료해지는가?
- **YES → Deep 신호.** 사용 측이 깔끔해지면 모듈이 가치를 더한 것.
- **NO → Shallow 의심.** 모듈 도입으로 오히려 코드가 늘어나면 의심.

#### 질문 2: 이 모듈을 쓰려면 내부 구조를 알아야 하는가?
- **YES → Shallow 신호.** 내부를 알아야 쓸 수 있는 모듈은 추상화에 실패한 것.
- **NO → Deep 신호.** 사용자가 내부를 신경 쓸 필요 없으면 추상화 성공.

#### 질문 3: 이 모듈의 인터페이스(공개 메서드/매개변수)가 내부 코드 양에 비해 큰가?
- **인터페이스 > 내부 → Shallow.** 메서드 5개 있는데 각 메서드가 3줄짜리?
- **인터페이스 << 내부 → Deep.** 메서드 1개에 매개변수 3개인데 내부 100줄?

#### 질문 4: 이 모듈을 제거하면 어떻게 되나?
- **사용 측 코드가 더 명료해진다 → Shallow였다.** 제거해라.
- **여러 곳에 복잡한 코드가 흩어진다 → Deep이었다.** 유지해라.

#### 질문 5: 이 모듈의 이름을 들었을 때, 사용자가 안에서 무엇을 할지 정확히 예상할 수 있나?
- **YES → Deep 신호.** 인터페이스가 의도를 잘 전달한다.
- **NO → 재명명 또는 재설계 필요.**

---

## 흔한 Shallow 패턴 (피해야 할 것)

> 📖 **마태복음 21:19 (잎사귀만의 무화과나무)**
>
> "한 무화과나무를 보시고 그리로 가사 **잎사귀 밖에 아무 것도 찾지 못하시고**... 이러므로 네게 영원토록 열매가 맺지 못하리라"
>
> Shallow Module은 잎사귀만 무성한 무화과나무다. 인터페이스(잎)는 그럴듯한데 정작 열매(내부 가치)가 없다. 모듈 리뷰의 핵심 질문은 단 하나로 압축된다 — **"이 모듈은 잎사귀뿐인가, 열매가 있는가?"** 열매 없는 모듈은 영원토록 그 자리에 두지 말 것.

### Anti-pattern 1: 의미 없는 래퍼
```typescript
function getUserName(user: User): string {
  return user.name;  // 그냥 속성 접근
}
```
→ `user.name` 직접 써라.

### Anti-pattern 2: getter/setter 폭증
```java
public class Config {
  private String host;
  private int port;
  private String username;
  // ... 20개 필드
  public String getHost() { return host; }
  public void setHost(String h) { this.host = h; }
  // ... 40개 메서드
}
```
→ 그냥 public 필드를 가진 데이터 구조체로 충분할 때가 많다.

### Anti-pattern 3: 인터페이스 1:1 대응 클래스
```php
interface UserRepository {
    public function find($id);
    public function save($user);
}
class UserRepositoryImpl implements UserRepository {
    // 인터페이스와 정확히 1:1, 단 하나의 구현체
}
```
→ 정말 다른 구현체가 필요한가? 아니면 그냥 클래스 하나로?

### Anti-pattern 4: 너무 작은 단위로 쪼갠 함수
```javascript
function isValidEmail(email) {
  return checkEmailFormat(email) && checkEmailDomain(email) && checkEmailLength(email);
}
function checkEmailFormat(email) {
  return email.includes('@');  // 한 줄
}
function checkEmailDomain(email) {
  return email.split('@')[1].length > 0;  // 한 줄
}
function checkEmailLength(email) {
  return email.length < 100;  // 한 줄
}
```
→ 그냥 `isValidEmail` 안에 다 두는 게 더 명료할 수 있다.

### Anti-pattern 5: 과한 계층화
- Controller → Service → Repository → DAO → DB 헬퍼 → ORM
- 각 층이 정말 가치를 더하는가, 아니면 그저 "교과서적"이라서 만든 것인가?

---

## Deep Module 만드는 패턴

### Pattern 1: 큰 책임을 단순 인터페이스 뒤에 감춤
- 좋은 예: HTTP 클라이언트의 `request(url, options)` — 내부엔 연결 풀, 재시도, 인증, 캐시 등 다 있지만 인터페이스는 단순.

> 📖 **누가복음 7:7~8 (백부장의 믿음)**
>
> "**말씀만 하사** 내 하인을 낫게 하소서... 나도 남의 수하에 든 사람이요 내 아래에도 군인이 있으니 이더러 가라 하면 가고 저더러 오라 하면 오고 내 종더러 이것을 하라 하면 하나이다"
>
> 백부장이 청한 "말씀만 하사"는 인터페이스/구현 분리의 신앙적 원형이다. 호출자(백부장)는 한 줄 명령만 던지고, 내부 메커니즘은 알 필요 없다. 백부장이 이걸 이해할 수 있었던 건 그가 군대 명령 체계 — 즉 추상화 계층 — 안에 살고 있었기 때문. 예수님이 이 믿음을 "이만한 믿음은 만나보지 못하였노라"고 칭찬하신 건, 단순 인터페이스 뒤에 풍부한 내부가 있음을 알아본 통찰 자체에 대한 칭찬이다.

### Pattern 2: 기본값으로 단순함 유지, 옵션으로 풍부함 제공
- 좋은 예: `fetch(url)`만으로도 동작, `fetch(url, {method, headers, body})`로 풍부.

### Pattern 3: 한 가지 강력한 추상을 정확히 구현
- 좋은 예: Redis의 키-값 모델 — 인터페이스는 단순(get/set/del)인데 내부엔 다양한 자료구조와 영속성.

### Pattern 4: 사용 측 코드의 반복 패턴을 모듈 안으로 흡수
- 사용 측 코드 여러 곳에서 똑같이 반복되는 흐름이 있다면, 그것을 모듈이 내부에서 처리.

---

## TTL 프로젝트 적용 예시

### TTL 맞고: 게임 룰 엔진
- **Deep 후보:** `Game::naeda($card)` — 인터페이스 단순, 내부에선 규칙 검증, 점수 계산, 다음 차례 결정 다 처리. (Ubiquitous Language 원칙대로 한국 화투 용어 유지)
- **Shallow 위험:** 각 규칙을 따로 클래스로 만들고 외부에서 조합 — 그러면 사용자가 규칙 순서를 알아야 함.

### HOSU: 결제 모듈
- **Deep 후보:** `Payment::charge($resident, $amount)` — PortOne V2 통합, 재시도, 영수증 발급, 알림 다 내부.
- **Shallow 위험:** PortOne API를 그저 한 번 감싼 클래스 — 그러면 PortOne 직접 쓰는 게 낫다.

### TTL Forge: 도메인 어댑터
- **Deep 후보:** `Forge::generate($domain, $prompt)` — 도메인(간판/건축/게임)에 따라 내부에서 다른 모델/프롬프트/후처리 적용.
- **Shallow 위험:** 도메인별로 별도 함수 노출 — 사용자가 도메인 분기 로직을 직접 짜야 함.

---

## 매주 점검 (Kent Beck의 매일의 설계와 결합)

매주 월요일 30분 동안:

1. 지난주 만든 모듈 목록 작성.
2. 각 모듈에 대해 위 5가지 질문 적용.
3. Shallow로 판정된 모듈은:
   - 합치기, 또는
   - 없애기, 또는
   - 재설계
4. 1개라도 발견하면 다음 주 코딩 시 같은 실수 안 하도록 메모.

---

## 한 줄 요약

> "좋은 모듈은 사용자에게 적은 것을 묻고 많은 것을 준다.
> 나쁜 모듈은 많은 것을 묻고 적은 것을 준다."
