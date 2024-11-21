# 프론트엔드 배포 파이프라인



> **목차**
> ---
> 1. [진행 순서](#1-진행-순서)
> 2. [주요 링크](#2-주요-링크)
> 3. [주요 개념](#3-주요-개념)
> 4. [CDN과 성능최적화](#4-cdn과-성능최적화)

## 1. 진행 순서
<img width="587" alt="스크린샷 2024-11-22 오전 12 24 32" src="https://github.com/user-attachments/assets/68a2b44d-acb6-4087-8149-22c12af9bf7e">

1. 저장소를 체크아웃합니다.
2. 프로젝트 의존성을 설치합니다.
4. Next.js 프로젝트를 빌드합니다.
5. AWS 자격 증명을 구성합니다.
6. 빌드된 파일을 S3 버킷에 동기화합니다.
7. CloudFront 캐시를 무효화합니다.

## 2. 주요 링크
- S3 버킷 웹사이트 엔드포인트: http://ahngh0113-bucket.s3-website.eu-north-1.amazonaws.com/
- CloudFrount 배포 도메인 이름: https://d23si7qmel0ujy.cloudfront.net/

## 3. 주요 개념
| 항목 |설명 |
|---|---|
| **GitHub Actions과 CI/CD 도구** | - GitHub의 자동화 도구로 사용됩니다. <br>- main에 push되면 빌드/테스트/배포가 자동으로 진행됩니다. |
| **S3와 스토리지** | - 정적 웹 사이트 호스팅에 사용됩니다. <br>- 파일(빌드된 파일, 이미지, 미디어 등)이 저장됩니다. 
| **CloudFront와 CDN** | - S3와 연결된 콘텐츠를 빠르게 전달합니다. <br>- 사용자와 가까운 서버에서 콘텐츠를 제공합니다. |
| **캐시 무효화(Cache Invalidation)** | - CloudFront의 캐시된 콘텐츠를 무효화하여 최신 파일을 제공할 수 있습니다.(/*) |
| **Repository secret과 환경변수** | - 민감한 정보를 안전하게 저장하고 빌드 및 배포 시 사용합니다. |

## 4. CDN과 성능최적화
S3의 로드 시간은 1.46초, cloudFront(CDN)의 로드 시간은 390밀리초로 약 <u>***73%***</u> 정도 감소했다.

<img width="1282" alt="스크린샷 2024-11-22 오전 12 46 10" src="https://github.com/user-attachments/assets/5726cff3-f1c1-4b5d-b2aa-e51b27ba05ae">
