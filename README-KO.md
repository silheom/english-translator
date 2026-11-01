# 영어 문장별 번역기 - GitHub 로컬 모델 버전

## 꼭 읽어주세요
이 ZIP에는 HTML 코드와 폴더 구조만 들어 있습니다. **AI 모델 가중치 파일 자체는 포함되어 있지 않습니다.** 모델 파일은 별도로 해당 폴더에 넣어야 실제 번역이 작동합니다.

## 폴더 구조
```
/
├── index.html
└── models/
    └── Xenova/
        └── nllb-200-distilled-600M/
            └── (Transformers.js 호환 모델 파일 전체)
```

이 앱은 `env.localModelPath='./models/'` 및 `env.allowRemoteModels=false`로 설정되어 Hugging Face에서 모델을 자동 다운로드하지 않습니다.

## GitHub Pages 설정
1. ZIP을 압축 해제합니다.
2. `index.html`과 `models` 폴더를 저장소 최상위에 올립니다.
3. Settings → Pages → Deploy from a branch → `main` → `/(root)`로 설정합니다.

## 모델 파일에 관한 중요한 제한
- 일반 PyTorch `.bin` 또는 `.safetensors`만으로는 브라우저에서 실행되지 않습니다. Transformers.js 호환 ONNX 모델과 tokenizer/config 파일이 필요합니다.
- GitHub 일반 저장소는 단일 파일 100MB 초과 업로드에 제한이 있습니다.
- 따라서 모델 ONNX 파일이 100MB를 넘는 경우 일반 GitHub 웹 업로드로는 올릴 수 없습니다. Git LFS를 Pages 정적 호스팅 해결책으로 가정해서는 안 됩니다.
- NLLB-200 distilled 600M 계열은 모델 파일이 큰 편이라 GitHub Pages에 그대로 넣는 방식이 실제로는 제한에 걸릴 수 있습니다. 실제 모델 파일 용량과 파일 목록을 확인한 뒤 배포 방식을 결정해야 합니다.

## 네트워크
원문 번역은 브라우저 로컬 모델로 수행하도록 구성했습니다. 다만 Transformers.js 라이브러리와 WASM 실행 파일은 CDN에서 받아오므로 최초 접속 시 인터넷 연결이 필요합니다.
