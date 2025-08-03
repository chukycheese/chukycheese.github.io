---
layout: post
title: "(번역) AI 가 우리에게 다가오고 있다"
date: 2025-08-02
toc: true
toc_sticky: true
category:
    - ai
tag:
    - ai
    - mcp
mathjax: false
comment: true
---

 이 글은 AI가 데이터베이스에 직접 접근해 인간 전문가처럼 데이터를 분석하는 새로운 워크플로우를 소개합니다. 단순한 질의응답을 뛰어넘는 이러한 도약은 데이터 분석가의 역할이 근본적으로 재정의될 미래를 암시합니다.

## 들어가기에 앞서

- 아래의 번역된 글은 원문의 저자에게 번역 및 게재 허락은 받았습니다.
- 원문: [Small Data and self service - AI is coming for us](https://datamonkeysite.com/2025/08/01/ai-is-coming-for-us/)

![using-mcp](https://datamonkeysite.com/wp-content/uploads/2025/08/mcp.png?w=1024)

살다보면 이전의 상태로 돌아갈 수는 없겠다 싶은 순간들이 생기기 마련입니다. 저는 10년 전 Gary 가 제게 PowerPivot 을 알려줬던 게 특히 기억에 남고, 데이터를 다루는 게 엑셀을 가지고 노는 것만큼 쉬워지는 날이 올 것이라고 생각했습니다. 또 다른 순간은 이틀 전 제가 Claude Desktop 을 데이터베이스에 연결한 뒤, "너는 뭐라고 생각해?" 라는 질문을 던졌을 때였습니다.

이건 아주 낯선 경험이었습니다. 기존에 겪었던 "데이터를 살펴보고 멋진 차트를 그려줘" 와 같은 게 아니었으니까요. 오히려 사람과 이야기를 나누고 나서 보고서 작성을 요청하는 것 같았습니다. LLM 이 모든 테이블을 나열하더니, 데이터를 살펴보고, 각 데이터셋이 어떤 것인지도 알아냈습니다. 어떤 방식을 썼는지는 모르겠지만, 전력 생산과 관련된 숫자가 MW 단위인 걸 알아냈습니다. 이를 MWh 로 변환하기 위해서는 12로 나눠줘야 합니다.

이런 방식이 전형적인 데이터와 대화를 나누는 워크플로우 (chat with your data workflow) 에 비해 강력한 이유는 단순합니다. LLM 이 데이터에 대한 읽기 권한을 가지고 있기 때문입니다. 이는 여전히 안전하고, 당신이 부여한 접근 대상을 읽을 수만 있습니다. 제가 알기로는, 이러한 LLM 들은 자가 학습을 하거나, 데이터를 학습에 사용하지는 않습니다. 적어도 엔터프라이즈 API 를 사용한다면 말이죠.

또 흥미로운 것이 있었습니다. 비개발자로서 저는 코딩 분야에 있어서 AI 의 진보를 매우 흥미롭게 지켜봤으며, 개발자들에게 크게 공감을 느끼지는 않았습니다. 저는 그들이 위협을 과장하는 줄 알았습니다. 그런데 AI 가 분석 또한 잘 하게 될 것이라는 걸 보고 난 뒤 마음이 바뀌었습니다.

Note: 앞으로는 LLM 을 AI 라고 하겠습니다. [Kurt 의 블로그](https://www.sqlbi.com/articles/ai-in-power-bi-time-to-pay-attention/)를 한 번 읽어봐주시고, MCP 에 대해 알려준 [Pawel](https://www.linkedin.com/in/pawelpotasinski/) 에게도 감사하다는 말씀을 드립니다.

## 일반적인 "데이터로 채팅하기" 워크플로우

![chat-with-your-data-workflow](https://lh7-rt.googleusercontent.com/docsz/AD_4nXet9t8htx-IdK8tfOWqqX_NMIRR4yUYdrB0R7b8Bf-x0grYeZue5tZVa1M9CT_VXr8MgGksUd9BRMTSy0V4UZfd5mI3lcsLsn03qxzx7mnX5zzu8GDU9bZMJDG3EoniAKjHx12F6g?key=bK7lxoHndzf8UGJhddmq5Q)

여기서 중요한 부분은 AI 는 여러분의 데이터에 접근 권한이 없다는 것입니다. 여러분은 데이터에 대해 최대한 많은 정보를 모아서, 이 정보와 함께 질문을 AI 에게 보냅니다. 그러면 AI 는 SQL 이나 DAX 를 생성해서 보내주고, 사용자는 이를 자신의 서버에 직접 실행하여 답변을 얻습니다. 만약 질문이 충분히 명확하지 않았다면, 이를 명확하게 하기 위한 질문을 다시 합니다. 예를 들면, '세계에서 가장 큰 나라가 어디냐' 는 질문은 했다면, AI 는 영토를 기준으로 하는 것인지, GDP 를 기준으로 하는 것인지 등을 되물을 것입니다. 실제로는 훨씬 더 복잡하긴 하겠지만, 핵심 아이디어는 이렇습니다.

기본적으로 우리는 AI 가 우리의 데이터를 볼 수 없게 하기 위해 많은 노력을 들입니다. 가끔은 쓰다 보면 왜 이렇게 명백한 질문에도 제대로 답변을 못하는지 의문을 가지기도 할 겁니다. 생각해보세요. 다른 사람이 데이터 분석가인 여러분에게 아무런 숫자를 보지 않고 보고서를 작성하달라고 하면 어떨 것 같나요?

## MCP 를 사용했을 때

![using-mcp](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdHs81TKh_1auMYmWWO9YuXJCkY_wFMjlkzqm5lIvOCtSr3vSqwLivNVg-3aQ1VHgwOBXhRG8QXk7XQOhzqKKtQRELGhspHsFUJyhPRh2LBtAGq5EUSLXCFrhWDEu6Gx5VhdmD7rA?key=bK7lxoHndzf8UGJhddmq5Q)

이 환경에서 AI 는 고삐가 풀린 상태입니다. 데이터를 직접 읽을 수 있고 (다시 말씀드리지만, 여러분이 부여한 데이터에 대해, 이상적으로는 읽기 권한만 가지고 있습니다), 쉽게 말해서 대리인의 역할을 하면서, 더 많은 자율성을 가지고 있습니다. 그리고 메타데이터에 제한된 것도 아닙니다.

## OneLake 의 데이터를 사용하는 사례

- OneLake 는 Microsoft 의 Data Lake 관련 제품입니다
- [Microsoft - OneLake](https://learn.microsoft.com/ko-kr/fabric/onelake/onelake-overview)

제 OneLake 에는 아래와 같은 데이터가 있는데, 이는 모두 정제된 데이터입니다.

![onelake-tables](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcApIa7ip8qCW5ZhoPRykd7f7Fe3FAeP4ydM4cjcO8MIXqJVFNo7gtlqoS1XXAsHEsVV9OlegashjZ4MvfqvVfJmmHgxkH00oLVlg1wlKi-yyRhFV3YbDYjYhl-mS9Qjmwvnar74Q?key=bK7lxoHndzf8UGJhddmq5Q)

아직 Fabric 데이터웨어하우스를 위한 MCP 서버가 없어서, [DuckDB MCP 서버](https://github.com/motherduckdb/mcp-server-motherduck) 를 사용하여 OneLake 에서 데이터를 읽어왔습니다. 편의를 위해 직접 쿼리를 사용하지 않고, 데이터를 로컬 DuckDB 파일로 저장했습니다.

```python
import duckdb
 
con = duckdb.connect()
con.sql("ATTACH 'aemo_delta.duckdb' AS db; USE db")
 
for tbl in ['duid', 'summary', 'calendar', 'mstdatetime']:
    con.sql(f"""
        CREATE OR REPLACE TABLE {tbl} AS 
        FROM delta_scan('abfss://serving@onelake.dfs.fabric.microsoft.com/datamart.Lakehouse/Tables/aemo/{tbl}')
    """)
 
con.close()
```

MCP 를 설치하고, Claude Desktop 과 연결 설정을 마쳐야 합니다. 명확히 하자면, 모든 MCP 클라이언트와 사용할 수 있지만, 제가 찾을 수 있는 것들 중 가장 괜찮았던 것이 이것이었습니다. 언젠가는 Power BI Desktop 이 MCP 클라이언트가 될지 누가 알겠어요 (완전히 만들어낸 이야기입니다. 힌트 같은 게 아니에요).

그런 뒤 Claude Desktop 에 아래 설정을 추가해줍니다.

```
{
  "mcpServers": {
    "mcp-server-motherduck": {
      "command": "uvx",
      "args": [
        "mcp-server-motherduck",
        "--db-path",
        "/tmp/llm/aemo_delta.duckdb"
      ]
    }
  }
}
```

제가 느끼기에는 AI 를 위한 OBDC 같았습니다. 모든 사람들이 이 프로토콜을 사용하고 있으니까요.

## 경험

데이터도 공개되어 있어서 [전체 채팅 기록](https://claude.ai/share/97158cab-9402-494c-80fc-388bc59a2d3e)도 공개하겠습니다. 저는 AI 가 문제에 접근한 방식이 매우 마음에 들었는데, 첫 번째로 테이블을 확인한 것이었습니다. 이는 매우 사람 같은 행동이라고 생각합니다.

![analyse-the-data-in-duckdb-and-give-me-key-insights](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf5XbTn72nxnGSIfNlTsbqWiDEKG-4RtTbxgaN33UKjQvgV5GG4s8YAPnP6FLih2h_Xm_N26CpqL4hwuWupet0H8FFC9TRmtfwt1BBx6n2_dX73yX6TxStmBpLsiwX6XIoQgOC8nA?key=bK7lxoHndzf8UGJhddmq5Q)

채팅을 읽어보시면, 완벽하지는 않다는 것을 알 수 있을 겁니다. 재생에너지에 대해 이야기하면서 수력 발전을 생략하기도 하고, 전날에는 맞게 계산했지만 MWh 를 잘못 계산하기도 했습니다.

![key-revelations](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfVLbnKI8Y9yh3ROSn_fGSFAEKAigPYGofbkJvwyh0KHbC2YYR3yg5Emr71rxyPPclK_yDQyuO_BoQFyEsirQ0fRGZP9sXh56LsI2ttqFRIKQ7FvFq2V7U4EN1Ddn7ocA?key=bK7lxoHndzf8UGJhddmq5Q)

## 발견한 것들

- 간단하게 사용하려고 해도 여전히 시멘틱 모델 (semantic model) 이 필요합니다. 만약에 제가 MWh = MW/12 로 측정했었다면 AI 는 항상 그렇게 했을 것입니다. 적어도 이론적으론 말이죠. 복잡한 모델에 있어서는 더욱 중요합니다. 말이 나와서 하는 말인데, AI 는 모델링 또한 잘 합니다. 이제 인간이 필요할까요?
- 놀랍게도 이 단순한 워크플로우에서 모든 연산을 변경할 수 있습니다. 진짜로 중요한 것은 스토리지입니다!
- 제가 사용한 모든 데이터는 공개되어 있기 때문에 보안에 주의하지 않아도 되었습니다. 기업에서 사용하는 것이라면 Claude Desktop 같은 도구를 사용할 수 없을 것이고, Azure AI Foundry 같은 솔루션을 고려해볼 수 있을 것입니다.
- 지금까지 대부분의 모델은 서빙 단계에서는 추가적인 지식을 습득하지 못하고 있지만, 향후 10년 동안 어떻게 바뀔지 누가 알겠어요? 사용자, 그리고 데이터와 상호작용을 하면서 학습하는 AI 를 상상해보세요. 완전히 새로운 질문들을 하게 될 겁니다. 사용자 마다 특정한 모델이 필요한가요? 아직 그 단계는 아니지만, 언젠가는 해결해야할 문제라고 생각합니다.

- 절대 MCP 에게 그 어떤 쓰기 권한도 주지 마세요.
