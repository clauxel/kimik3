# Kimi K3는 Claude·GPT·Gemini와 어디서 갈라지는가

![Kimi K3 frontier model landscape](https://raw.githubusercontent.com/clauxel/kimik3/main/assets/kimi-k3-model-landscape.svg)

요즘 모델 비교 글을 읽다 보면 묘한 피로감이 온다. 대부분은 같은 문장으로 시작한다. “A 모델이 B 벤치마크에서 C 모델을 이겼다.” 몇 줄 뒤에는 가격표가 나오고, 마지막에는 “어떤 모델이 더 낫다”는 단정이 붙는다. 그런데 실제 팀에서 모델을 고를 때 문제는 그렇게 깔끔하지 않다. 좋은 답변을 한 번 뽑는 일과, 긴 코드베이스를 붙들고 사흘 동안 수정하는 일은 전혀 다른 문제다. PDF를 읽는 일과, 그 PDF에서 나온 가정을 스프레드시트와 문서와 프런트엔드 코드로 옮기는 일도 다르다.

Kimi K3가 흥미로운 이유는 여기 있다. 이 모델은 단순히 “중국에서 나온 큰 모델”이 아니다. Moonshot AI가 공개한 자료에 따르면 K3는 2.8조 개 파라미터, Kimi Delta Attention, Attention Residuals, 네이티브 비전, 100만 토큰 컨텍스트를 앞세운다. 동시에 Kimi.com, Kimi Work, Kimi Code, Kimi API 같은 작업 표면 위에 올라가 있다. 그러니까 K3를 제대로 보려면 “Claude보다 똑똑한가”, “GPT보다 싼가” 같은 질문만으로는 부족하다. 더 정확한 질문은 이쪽이다.

**이 모델은 어디까지 작업 공간을 오래 붙들 수 있는가. 그리고 그 비용, 통제권, 검증 가능성은 감당할 만한가.**

## 먼저, 출시 주간의 소음과 사실을 분리해야 한다

Kimi K3의 공식 스토리는 꽤 강하다. [Kimi K3 공식 기술 블로그](https://www.kimi.com/blog/kimi-k3)는 K3를 “open 3T-class model”로 설명하고, 장기 코딩, 지식 작업, 추론을 위해 설계됐다고 말한다. Kimi 쪽 문서는 K3가 현재 Kimi의 가장 강한 모델이며 Kimi Agent, Agent Swarm, Kimi Work, Kimi Code, API에서 쓰인다고 설명한다. [Kimi API 문서](https://platform.kimi.ai/docs/guide/kimi-k3-quickstart)는 `kimi-k3` 모델 ID, `reasoning_effort`의 `low/high/max`, 100만 토큰까지의 큰 출력 한도, 비전 입력, 구조화 출력, 툴 호출을 다룬다. [Kimi Code 문서](https://www.kimi.com/code/docs/en/kimi-code/models.html)는 코딩용 모델 ID `k3`와 100만 컨텍스트 설정을 별도로 설명한다.

하지만 공식 자료가 말하지 않는 것도 중요하다. Kimi의 공식 블로그는 전체 성능이 가장 강한 폐쇄형 모델인 Claude Fable 5와 GPT 5.6 Sol에는 아직 뒤진다고 적는다. K3의 기술 보고서와 전체 가중치는 이 글을 정리한 시점에는 아직 후속 공개 대상으로 남아 있다. MoonshotAI의 공식 GitHub와 Hugging Face 조직에서도 Kimi-K3 공식 가중치 저장소를 확인하지 못했다. 이름이 비슷한 제3자 페이지는 있었지만, 그것을 공식 배포로 다루면 안 된다.

그래서 K3에 대한 좋은 분석은 두 문장을 동시에 붙잡아야 한다. 하나는 “K3는 실제로 매우 야심찬 모델이다.” 다른 하나는 “아직 독립 검증과 배포 세부사항이 충분하지 않다.” 어느 한쪽만 말하면 글이 너무 쉽게 납작해진다.

## K3의 핵심은 크기가 아니라 기억의 방식이다

2.8조 파라미터라는 숫자는 시선을 끈다. 하지만 큰 숫자는 종종 사고를 멈추게 만든다. 더 중요한 건 그 크기를 어떤 방식으로 계산 가능한 작업 흐름으로 바꾸느냐다.

여기서 Kimi Delta Attention과 Attention Residuals가 나온다. [Kimi Linear 논문](https://arxiv.org/abs/2510.26692)은 Kimi Delta Attention을 통해 긴 컨텍스트에서 KV cache 사용을 줄이고, 100만 컨텍스트 디코딩 처리량을 크게 끌어올릴 수 있다고 주장한다. [Attention Residuals 논문](https://arxiv.org/abs/2603.15031)은 기존 Transformer의 고정적인 residual 누적이 깊이가 깊어질수록 각 층의 신호를 희석시키는 문제를 지적하고, 이전 층 출력들을 attention으로 선택적으로 모으는 방식을 제안한다.

이 두 기술은 K3를 “거대한 MoE 모델” 이상의 것으로 보이게 만든다. K3의 공개 설명은 896개 expert 중 16개를 활성화하는 sparse MoE 구조를 말한다. 하지만 sparse MoE는 그 자체로 마법이 아니다. 라우팅이 불안정하면 expert가 편향되고, 긴 문맥을 잘라내면 큰 모델도 좁은 방에서 일하게 된다. KDA와 AttnRes는 K3가 “긴 시간 동안 정보를 잃지 않고 일하는 모델”이 되기 위한 인프라에 가깝다.

![Kimi K3 architecture lens](https://raw.githubusercontent.com/clauxel/kimik3/main/assets/kimi-k3-architecture-lens.svg)

이 지점에서 Claude, GPT, Gemini와의 비교가 흥미로워진다. 폐쇄형 최상위 모델들은 내부 구조를 자세히 공개하지 않는다. 대신 제품 완성도, 추론 효율, 안전장치, API 안정성, 생태계 통합에서 승부한다. Claude는 긴 글의 판단과 문체 감각에서 여전히 강한 인상을 준다. GPT 계열은 도구 생태계와 범용성에서 압도적이다. Gemini는 구글 제품군과 멀티모달 통합에서 자연스러운 장점이 있다. K3는 이들과 같은 방식으로 경쟁하지 않는다. K3는 “긴 컨텍스트를 가진 agentic workspace”라는 각도에서 들어온다.

## 코딩에서는 “한 번 맞히기”보다 “오래 버티기”가 더 중요하다

K3의 출시 자료에서 가장 설득력 있는 부분은 코딩이다. 공식 블로그는 커널 최적화, GPU 컴파일러 개발, 게임 개발, 칩 설계, 연구 코드 구현 사례를 길게 제시한다. 외부에서도 CNBlogs의 한 실험처럼 빈 프로젝트에서 물리 엔진, 게임, 논리 퍼즐 실험실을 만들고 테스트까지 돌린 사례가 나왔다. 이런 글이 의미 있는 이유는 단순하다. 알고리즘 문제 하나를 푸는 것보다, 작은 제품 하나를 만들며 계속 수정하고 검증하는 일이 모델의 약점을 훨씬 빨리 드러내기 때문이다.

Kimi K3가 이 영역에서 강해 보이는 이유는 세 가지다.

첫째, 컨텍스트가 크다. 큰 저장소, 스펙, 실패 로그, 스크린샷, 테스트 결과를 한 세션 안에 오래 유지할 수 있다는 건 coding agent에게 실제 무기다. 둘째, 비전이 붙어 있다. 프런트엔드와 게임 개발은 코드만 읽는 일이 아니라 화면을 보고 고치는 일이다. 셋째, Kimi Code라는 전용 작업면이 있다. `/model`로 K3와 K2.7 Code를 오가고, 서드파티 도구에서는 OpenAI/Anthropic 호환 엔드포인트를 쓸 수 있다.

다만 여기서도 조심해야 한다. Claude나 GPT가 약하다는 뜻이 아니다. 오히려 많은 팀은 여전히 Claude의 수정 감각이나 GPT의 툴 생태계에서 더 안정감을 느낄 수 있다. K3가 좋아 보이는 작업은 “오래 붙잡는 작업”이다. 이미 잘게 쪼개진 티켓을 빠르게 처리하는 업무라면 K3의 100만 컨텍스트가 비용만 키울 수 있다. 반대로 레거시 코드, 긴 PRD, 화면 캡처, 데이터 파일, 실패 로그를 한꺼번에 들고 들어가야 한다면 K3의 설계 철학이 더 직접적으로 살아난다.

## K3는 싸지 않다. 그래서 가격보다 reasoning efficiency가 더 중요하다

Kimi API 플랫폼의 공개 가격은 cache hit 100만 토큰당 0.30달러, input 3달러, output 15달러다. 숫자만 보면 “중국 오픈 모델은 싸다”는 이미지와 조금 다르다. K3는 싼 모델이라기보다, frontier work를 API로 제공하는 모델에 더 가깝다.

여기서 실제 비용을 결정하는 것은 토큰 단가만이 아니다. 모델이 문제를 풀기 위해 얼마나 오래 생각하는지, 같은 작업을 몇 번 되돌리는지, 실패했을 때 사람이 얼마나 개입해야 하는지가 더 중요하다. 공식 문서도 K3가 항상 thinking을 켠다고 설명한다. `reasoning_effort`를 낮출 수는 있지만, thinking 자체를 꺼서 같은 모델을 가볍게 쓰는 방식은 기본 설계가 아니다.

이 부분에서 Claude와 GPT는 강하다. 폐쇄형 모델들은 내부적으로 reasoning budget을 더 정교하게 조절하고, 사용자에게는 매끈한 제품 경험으로 보여준다. Open model 계열은 단가와 통제권에서 유리하지만, 운영자가 직접 latency, throughput, quantization, serving stack, safety layer를 다뤄야 한다. K3는 그 중간의 이상한 위치에 있다. API로 쓰면 비싸고, self-host를 기다리면 하드웨어가 무겁다. 그래서 K3는 “모든 요청에 쓰는 기본 모델”이라기보다, 비싼 세션을 정당화할 만큼 문맥과 작업 난도가 큰 경우에 빛난다.

## 멀티모달과 문서 작업에서는 K3가 “챗봇”보다 “사무실”에 가깝다

Kimi 도움말 문서는 K3가 이미지, 비디오, PDF, Word, Excel, PPT 같은 입력을 이해하고, `.pptx`, `.docx`, `.xlsx`, `.pdf` 같은 편집 가능한 산출물을 만들 수 있다고 설명한다. 이건 단순한 multimodal demo와 다르다. 실무에서는 모델이 이미지를 설명하는 능력보다, 문서와 표와 화면을 왕복하며 결과물을 만드는 능력이 더 중요하다.

예를 들어 긴 시장 조사 PDF와 Excel 데이터, 기존 발표 자료, 웹 페이지 스크린샷이 있다고 하자. 이때 좋은 모델은 요약을 잘하는 데서 멈추면 안 된다. 논리의 충돌을 찾고, 표의 가정을 다시 계산하고, 발표 흐름을 바꾸고, 필요한 경우 HTML 대시보드나 슬라이드 초안까지 이어가야 한다. K3가 내세우는 “workspace” 이미지는 바로 이 연결에서 나온다.

Gemini는 구글 생태계와 멀티모달에서 자연스럽게 강하다. GPT는 플러그인과 도구, API 생태계가 넓다. Claude는 긴 문서의 의미와 문체를 다루는 데 여전히 좋은 평가를 받는다. K3의 차별점은 문서와 코드와 agent 작업을 하나의 Kimi 표면으로 묶어 보려는 방향이다. 성공하면 사용자는 모델을 바꾸는 대신 작업 공간 안에서 문맥을 계속 가져갈 수 있다. 실패하면 거대한 컨텍스트와 다양한 도구가 오히려 느리고 비싼 혼란이 된다.

![Kimi K3 workload matrix](https://raw.githubusercontent.com/clauxel/kimik3/main/assets/kimi-k3-workload-matrix.svg)

## 오픈 웨이트라는 말은 조심해서 써야 한다

K3는 “open 3T-class model”이라는 표현으로 소개됐다. 하지만 이 글을 정리한 시점에는 기술 보고서와 전체 가중치가 아직 확인되지 않았다. 그래서 지금 단계에서 “K3를 로컬에서 돌릴 수 있다”고 쓰는 건 부정확하다. 더 정확한 표현은 “K3는 open-weight 방향을 예고했지만, 실제 배포와 라이선스, serving stack, 하드웨어 요구사항은 공개 후 확인해야 한다”다.

이 차이는 작지 않다. DeepSeek, Qwen, GLM 같은 공개 모델들은 이미 self-host와 fine-tuning, serving 경험이 쌓인 경우가 많다. 어떤 팀에게는 그쪽이 더 현실적이다. 모델이 조금 약해도 비용이 낮고, 내부망에 올릴 수 있고, 데이터 경계를 직접 통제할 수 있기 때문이다. 반대로 K3는 훨씬 큰 frontier-scale 모델이다. 2.8T MoE는 이름만 들어도 운영 부담이 보인다. sparse activation이 있어도 전체 weight와 memory footprint는 사라지지 않는다.

그래서 K3의 오픈성은 “노트북에서 바로 돌리는 자유”라기보다 “최상위급 모델도 폐쇄 API만의 영역은 아니라는 압박”으로 읽는 편이 맞다. 이 압박은 시장에 중요하다. 폐쇄형 모델 회사들은 가격과 lock-in을 다시 생각해야 하고, 오픈 모델 진영은 단순한 저가 대체재에서 frontier 경쟁자로 올라설 수 있다.

## 벤치마크보다 좋은 평가는 작은 프로덕션 리허설이다

Nature, AP, Tom’s Hardware 같은 외부 매체는 K3의 출시가 미국과 중국 AI 경쟁 구도에 주는 충격을 다뤘다. Bilibili와 V2EX, Hacker News에서는 가격, 멤버십, 100만 컨텍스트, 코딩 성능, self-host 가능성을 두고 빠르게 토론이 붙었다. 이런 반응은 분명 신호다. 하지만 팀이 실제로 모델을 선택할 때는 기사와 댓글만으로는 부족하다.

내가 권하는 평가는 작지만 집요해야 한다.

1. 같은 코드베이스에서 세 모델 이상을 돌린다.
2. 프롬프트를 짧게 만들지 말고 실제 스펙, 로그, 스크린샷, 실패 조건을 넣는다.
3. 성공한 결과만 보지 말고 실패한 중간 경로를 기록한다.
4. 토큰 사용량, latency, 재시도 횟수, 사람이 고친 줄 수를 남긴다.
5. 마지막에는 “누가 정답을 냈는가”가 아니라 “누가 팀의 시간을 덜 먹었는가”로 본다.

이렇게 보면 모델 비교가 훨씬 덜 낭만적이고 훨씬 유용해진다. K3는 긴 문맥과 agentic coding에서 높은 점수를 받을 가능성이 있다. Claude는 어려운 글과 판단에서 여전히 강할 수 있다. GPT는 도구 연결과 범용 워크플로에서 강할 수 있다. Gemini는 멀티모달과 구글 작업 환경에서 이길 수 있다. DeepSeek, Qwen, GLM은 가격과 통제권에서 이길 수 있다. 승자는 하나가 아니다. 작업마다 다른 모델이 이긴다.

## 결론: Kimi K3가 바꾼 질문

Kimi K3를 “Claude 킬러”나 “GPT 대체재”로 부르면 자극적이지만 별로 정확하지 않다. K3가 던진 질문은 다르다. 앞으로 최상위 모델 경쟁은 단일 답변의 품질보다, 긴 작업 세션을 얼마나 오래 유지하고, 코드와 문서와 화면과 도구를 얼마나 자연스럽게 묶고, 그 비용을 얼마나 투명하게 제어하는가로 옮겨갈 것이다.

그 관점에서 K3는 아직 완성된 판결이 아니라 강한 가설이다. 공식 자료만 봐도 야심은 충분하다. KDA와 Attention Residuals는 긴 문맥과 깊은 모델의 병목을 정면으로 건드린다. Kimi Code와 Kimi Work는 모델을 단순 API가 아니라 작업 공간으로 밀어 올린다. 동시에 기술 보고서, 전체 가중치, 독립 benchmark, 실제 serving 경험은 더 확인해야 한다.

그래서 지금 K3를 보는 가장 좋은 태도는 과장도 냉소도 아니다. K3를 frontier workspace 모델의 강한 후보로 두고, Claude·GPT·Gemini·DeepSeek·Qwen·GLM을 같은 작업대 위에 올려 실제로 굴려보는 것이다. 모델의 시대에는 질문을 잘못 잡는 순간 비교가 광고가 된다. K3가 정말 중요한 이유는, 우리에게 더 좋은 질문을 강요하기 때문이다.

---

### Sources and further reading

- [Kimi K3 official technical blog](https://www.kimi.com/blog/kimi-k3)
- [Kimi API K3 guide](https://platform.kimi.ai/docs/guide/kimi-k3-quickstart)
- [Kimi Code model configuration](https://www.kimi.com/code/docs/en/kimi-code/models.html)
- [Kimi Linear paper](https://arxiv.org/abs/2510.26692)
- [Attention Residuals paper](https://arxiv.org/abs/2603.15031)
- [MoonshotAI GitHub organization](https://github.com/MoonshotAI)
- [Moonshot AI Hugging Face organization](https://huggingface.co/moonshotai)
- [Independent Kimi K3 source map](https://github.com/clauxel/kimik3)
- [Kimi3.org resource hub](https://kimi3.org/)
