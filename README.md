# feedback-master

> 어려운 피드백·코칭·갈등 대화를 **딥인터뷰로 정돈한 뒤** 실전 스크립트를 만들어 주는 Claude Code 스킬입니다. 5개의 검증된 의사소통 프레임워크(**NVC 비폭력대화, 나 전달법 I-Message, DBT DEAR MAN, SBI-I, Radical Candor**)를 상황에 맞게 조합합니다.
>
> [English README](./README.en.md)

## 무엇인가요?

대부분의 사람은 "무엇을 말할지"보다 **"내가 진짜로 무엇을 원하는지"** 를 몰라서 어려운 대화를 망설입니다. 머릿속에는 서운함·걱정·죄책감·분노가 엉켜 있고, 상처 주기는 싫고, 안 하자니 찜찜하고, 막상 하려니 준비가 안 되어 있죠.

이때 "나 전달법 쓰세요" 같은 공식 한 줄은 별 도움이 안 됩니다. 공식을 쓰기 전에 먼저 **자기 마음을 풀어내는 과정**이 필요하기 때문입니다.

**feedback-master**는 그 풀어내는 과정을 Claude와 함께 하고, 그 다음에 실제로 쓸 수 있는 구체적 스크립트까지 만들어 주는 스킬입니다.

## 사용 흐름

1. **딥인터뷰** — Claude가 6단계(관찰 → 느낌 → 욕구 → 상대 이해 → 목표 → 제약) 질문을 하나씩 던집니다. 끝나면 당신 스스로 상황이 정리되어 있습니다.
2. **프레임워크 선택** — 인터뷰 내용을 바탕으로 5개 프레임워크 중 맞는 것(또는 조합)을 Claude가 고릅니다. 이름을 몰라도 됩니다.
3. **스크립트 생성** — 당신의 `user-preferences.md`에 기록된 톤·말투로 초안을 만듭니다. 대안 표현, 상대의 예상 반응과 재대응까지.
4. **리뷰 루프** — 어색한 부분을 말해 주면 즉시 고쳐 줍니다.
5. **메타 피드백 & 개인화** — "이 스크립트를 실제로 쓸 수 있을 것 같나요?"를 묻고, 당신의 답을 `user-preferences.md`에 축적합니다. 다음 번 실행 때 반영됩니다.

## 왜 만들었나요

- 많은 한국 조직은 "파괴적 공감(Ruinous Empathy)" — 단기 불편을 피하려고 꼭 필요한 말을 하지 않는 패턴 — 에 머물러 있습니다. 반대로 직설적이기만 한 "난폭한 솔직함(Obnoxious Aggression)"도 관계를 해칩니다. NVC, DEAR MAN 같은 프레임워크가 답이지만 습득에 수개월이 걸립니다.
- 개별 프레임워크마다 사각지대가 있습니다. 나 전달법은 부정적 감정 영역에서 효과가 제한적이라는 연구가 있고([Bippus & Young 2005](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=601983)), NVC는 깊이는 있지만 느리고, DEAR MAN은 구조적이지만 차갑게 들릴 수 있습니다. **하나의 공식이 아니라 상황별 선택·조합**이 더 효과적입니다.
- 영어권 프레임워크를 한국어에 그대로 쓰면 무례하거나 차갑게 들립니다. 이 스킬은 **한국 직장 맥락 적응층**(존대·호칭·완충 어휘·We/I 구분)을 내장합니다.

## 빠른 시작

### 설치 (Claude Code)

이 레포를 Claude Code 스킬 디렉토리로 복제하거나 심볼릭 링크를 겁니다.

```bash
git clone https://github.com/yourusername/feedback-master.git ~/Documents/feedback-master
ln -s ~/Documents/feedback-master ~/.claude/skills/feedback-master
```

또는 skills CLI 공개 후:

```bash
npx skills add yourusername/feedback-master@feedback-master -g -y
```

### 개인화 파일 초기화 (선택이지만 권장)

```bash
cp ~/Documents/feedback-master/user-preferences.md.template \
   ~/Documents/feedback-master/user-preferences.md
```

파일을 열어 선호하는 톤, 자주 쓰는 표현, 주요 대화 상대를 채워 두세요. 스킬이 사용할수록 이 파일을 자동 업데이트합니다.

> **개인정보 보호**: `user-preferences.md`는 `.gitignore`에 포함되어 절대 공개 레포에 커밋되지 않습니다. 안심하고 쓰세요.

### 사용

Claude Code에서 상황을 편하게 얘기하면 됩니다. 스킬이 이런 표현에서 자동으로 트리거됩니다.

- "팀원한테 피드백 해야 하는데 어떻게 말해야 할지 모르겠어"
- "상사한테 안 된다고 해야 하는데 너무 어려워"
- "매번 같은 걸로 싸우는데 어떻게 풀어야 할까"
- "부모님이랑 어려운 얘기를 해야 해"
- "1on1에서 이 얘길 꺼낼지 말지 고민돼"

Claude가 딥인터뷰 흐름으로 들어가 뒤엉킨 마음 → 쓸 수 있는 스크립트까지 데려다 줍니다.

## 사용 예시

```
사용자: 팀원에게 납기 지연 피드백을 해야 하는데 상처 주기 싫어서 망설이고 있어.

Claude (feedback-master):
개인화 메모를 읽었어요. "아쉽다" 대신 "답답하다"를 쓰시는 톤 반영할게요.

상황을 조금 더 이해하고 싶어서 몇 가지 여쭤볼게요.

먼저 최근에 정확히 어떤 일이 있었는지, 영상으로 찍었다면 거기에 
무엇이 담겨 있을까요? 언제, 몇 번 정도였나요?

사용자: 지난 3주에 두 번 있었어. A프로젝트랑 B프로젝트 납기...

(Claude가 6단계 인터뷰를 진행, SBI-I + Radical Candor 선택,
 사용자 말투로 한국어 스크립트 생성, 대안 표현 3개 제시,
 예상 반응과 재대응 시나리오 제공)

(대화 마무리 단계:)
오늘 만든 스크립트가 실제로 쓸 수 있을 것 같나요?
다음 번에 제가 다르게 해야 할 점이 있을까요?

사용자: 두 번째 문장이 너무 딱딱해. 좀 부드럽게 풀어줘.
        그리고 "답답했어요"보다 "당황스러웠어요"가 내 말투에 가까워.

Claude: 반영했습니다. "당황스러웠어요" 선호를 user-preferences.md에 
기록했어요. 다음 번에 기본값으로 쓸게요. (재작성된 스크립트 제시)
```

## 파일 구조

```
feedback-master/
├── SKILL.md                       # Claude가 읽는 진입점
├── README.md                      # 한국어 (default, 지금 보고 있는 파일)
├── README.en.md                   # English
├── LICENSE                        # MIT
├── .gitignore                     # user-preferences.md 제외
├── .claude-plugin/
│   └── plugin.json                # 플러그인 메타데이터
├── references/
│   ├── interview-flow.md          # 6단계 인터뷰 질문 세트
│   ├── i-message.md               # 나 전달법 (Thomas Gordon)
│   ├── nvc.md                     # 비폭력대화 (Marshall Rosenberg)
│   ├── dear-man.md                # DEAR MAN (Marsha Linehan, DBT)
│   ├── sbi.md                     # SBI-I (CCL)
│   ├── radical-candor.md          # Radical Candor (Kim Scott)
│   ├── framework-selection.md     # 프레임워크 선택 결정 트리
│   ├── korean-workplace.md        # 한국어·한국 직장 적응층
│   └── examples.md                # 8가지 실전 시나리오 완성 스크립트
├── user-preferences.md.template   # 개인화 파일 템플릿
└── user-preferences.md            # (gitignore됨) 당신의 개인 메모
```

## 개인화가 작동하는 방식

1. 스킬 실행 시 맨 먼저 `user-preferences.md`를 읽습니다.
2. 당신이 선호하는 표현을 쓰고, 싫어하는 표현을 피하며, 과거 피드백 이력을 참고합니다.
3. 매 세션 마지막에 Claude가 묻습니다 — **"이 스크립트를 실제로 쓸 수 있을 것 같나요? 다음 번엔 뭘 다르게 할까요?"**
4. 당신의 답변은 `user-preferences.md`의 "과거 피드백 이력"에 **추가**됩니다(덮어쓰지 않음).
5. 시간이 지나면서 스킬이 **당신의 목소리로 수렴**합니다.

이 개인화는 **feedback-master 스킬에 한정된 메모리**입니다. Claude의 일반 메모리에는 관여하지 않습니다.

## 인용하는 프레임워크

이 스킬은 다섯 개의 의사소통 전통 위에 서 있습니다. 전체 출처는 각 reference 파일 하단에 있습니다.

| 프레임워크 | 창시자 | 연도 | 주 용도 |
|---|---|---|---|
| 나 전달법 (I-Message) | Thomas Gordon | 1970 | 짧은 1문장 피드백 |
| NVC (비폭력대화) | Marshall Rosenberg | 1960~70년대 | 깊은 관계 대화 |
| DEAR MAN / GIVE / FAST | Marsha Linehan (DBT) | 1980년대 | 구조적 요청·경계 |
| SBI / SBI-I | Center for Creative Leadership | 1990~2000년대 | 직장 피드백 |
| Radical Candor | Kim Scott | 2017 | 관리자 자세 프레임 |

**feedback-master**는 메타 스킬입니다. 위 프레임워크들을 **선택 로직과 딥인터뷰 기반 elicitation** 아래 통합합니다. 원전 학습을 대체하지 않습니다 — 특정 프레임워크에 관심이 생기면 각 reference 파일 하단의 원저서를 읽어 보세요.

## 설계 원칙

- **공식보다 자기공감 먼저.** 자기 이해 없는 공식은 공허한 수행이 됩니다. 인터뷰를 먼저 합니다.
- **도그마가 아닌 선택.** 어떤 프레임워크도 만능이 아닙니다. 상황에 맞게 매칭합니다.
- **누적되는 개인화.** 쓸수록 당신 목소리에 맞게 진화합니다.
- **한국 직장 맥락 내장.** 존대, 완충 어휘, We/I 구분이 적응층에 포함됩니다.
- **안전 우선.** 위기(자해·폭력·심한 심리적 고통) 신호에서는 전문 자원(자살예방상담 1393, 정신건강위기상담 1577-0199)을 명시적으로 안내합니다.

## 한계

- 임상 치료나 전문 심리상담·코칭의 대체재가 아닙니다.
- 구조적 권력 불평등(직장 괴롭힘·차별·학대)은 해결하지 못합니다. 이 경우 HR·노무·법적 경로로 안내합니다.
- 경험적 증거 강도는 프레임워크마다 다릅니다(DBT 강, 나 전달법 중, NVC 신흥). 각 reference 파일 참조.
- 한국어 적응층은 일반 패턴 기반입니다. 구체적 문화 맥락(특정 업계·지역)에서는 사용자 조정이 필요할 수 있습니다.

## 기여 (Contributing)

기여를 환영합니다. 특히:

- `references/examples.md`에 추가 시나리오
- 한국어 외 문화권 적응층
- 각 reference 파일의 실증 연구 업데이트
- 프레임워크 선택 로직이 실패하는 엣지 케이스

큰 변경은 Discussion을 먼저 열어 주세요. 이 스킬은 초점을 유지하며 작게 가려고 합니다.

## 라이선스

MIT. [LICENSE](./LICENSE) 참조.

각 의사소통 프레임워크 자체의 지적 재산권은 원저자에게 있습니다. 이 스킬은 그 프레임워크들을 실무 대화 목적으로 재구성·운용화한 것이며, Gordon Training, Center for Nonviolent Communication, Behavioral Tech(DBT), CCL, Radical Candor의 공식 제품이 아닙니다.

## 감사의 말

임상 심리학, 경영학, 조직행동론을 가로지른 피드백·갈등·의사소통 연구 위에서 만들어졌습니다. 특히 다음 분들께 감사드립니다:

- Thomas Gordon (1918–2002)
- Marshall Rosenberg (1934–2015)
- Marsha Linehan
- Kim Scott
- 각 reference 파일에 인용된 연구자와 실무자들

---

이 스킬로 단 한 번의 어려운 대화가 더 나아진다면, 그걸로 충분합니다.
