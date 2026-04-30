# 비정형 문서 RAG & 그래프 RAG 실습

비정형 문서(PDF, 이미지 등) 파싱부터 멀티모달 RAG, Neo4j 기반 Graph RAG까지 단계별로 구현하는 프로젝트입니다.

## 환경

- Python 3.10.x (Intel Mac 기준 — torch 2.2.2 최대 지원 버전)
- 패키지 관리: [uv](https://github.com/astral-sh/uv)

## 시작하기

```bash
# 1. Python 3.10 가상환경 생성
uv venv --python 3.10.12

# 2. 의존성 설치
uv sync

# 3. 환경변수 설정
cp .env.example .env   # .env 파일에 API 키 입력

# 4. Jupyter 커널 등록
.venv/bin/python -m ipykernel install --user --name 004-prj-uv --display-name "004_prj (.venv)"
```

## 필수 API 키 (.env)

```
OPENAI_API_KEY=
GOOGLE_API_KEY=
HUGGINGFACEHUB_API_TOKEN=
LANGCHAIN_API_KEY=
GROQ_API_KEY=
NEO4J_URI=
NEO4J_USERNAME=
NEO4J_PASSWORD=
NEO4J_DATABASE=
```

## 커리큘럼

### Week 1 — 비정형 문서 파싱 & RAG

| 노트북 | 내용 |
|--------|------|
| W1_001_Unstructured_Intro | Unstructured 라이브러리 기초 |
| W1_002_Unstructured_Docling | Docling을 활용한 PDF 파싱 |
| W1_003_Unstructured_LangChain | Unstructured + LangChain 통합 |
| W1_004_Unstructured_RAG_10-K | 10-K 연간보고서 RAG 구현 |
| W1_005_Docling_RAG_10-K | Docling 기반 10-K RAG |
| W1_006_SFT_Tool_Embedding_RunPod | SFT / Tool / Embedding (RunPod) |

### Week 2 — 멀티모달 RAG

| 노트북 | 내용 |
|--------|------|
| W2_001_Image_Processing (PIL) | PIL 이미지 처리 기초 |
| W2_002_Multimodal_LangChain_CLIP | CLIP 임베딩 & 이미지-텍스트 유사도 검색 |
| W2_003_Multimodal_LangChain_ChatModel | 멀티모달 Chat 모델 연동 |
| W2_004_Multimodal_RAG_Financial_Part1 | 금융 PDF 파티셔닝 (unstructured hi_res) |
| W2_005_Multimodal_RAG_Financial_Part2 | 멀티모달 RAG 구축 (이미지 + 테이블 + 텍스트) |
| W2_006_Multimodal_RAG_Financial_Part3 | 멀티모달 RAG 고도화 |
| W2_007_Multimodal_RAG_ColQwen | ColQwen 기반 멀티모달 RAG |

### Week 3 — Graph RAG (Neo4j)

| 노트북 | 내용 |
|--------|------|
| W3_001_neo4j_intro | Neo4j & Cypher 기초 |
| W3_002_neo4j_LangChain | LangChain + Neo4j 통합 |
| W3_003_neo4j_Build_KnowledgeGraph | ETF/기업 데이터로 지식 그래프 구축 |
| W3_004_Entity_Extraction_SimpleKGPipeline | LLM 기반 엔티티 추출 & KG 파이프라인 |
| W3_005_neo4j_10K_GraphRAG | 10-K 보고서 Graph RAG |

## 주요 의존성

| 패키지 | 버전 | 비고 |
|--------|------|------|
| torch | 2.2.2 | Intel Mac 최대 지원 버전 |
| transformers | >=4.47.1, <5.0 | torch 2.2.2 호환 |
| numpy | >=1.26.4, <2.0.0 | torch/numba 호환 |
| unstructured | >=0.18.32 | PDF hi_res 파싱 |
| langchain-core | >=1.3.0 | |
| langchain-chroma | >=1.1.0 | 벡터스토어 |

## Neo4j 설정 (Docker)

```bash
docker compose up -d
```

```yaml
# docker-compose.yml
services:
  neo4j:
    image: neo4j:5.26
    ports:
      - "7474:7474"
      - "7687:7687"
    environment:
      NEO4J_AUTH: neo4j/password
      NEO4J_PLUGINS: '["apoc"]'
      NEO4J_dbms_security_procedures_unrestricted: "apoc.*"
      NEO4J_dbms_security_procedures_allowlist: "apoc.*"
```
