# Kali Docs GitLab Mirror

이 저장소는 Kali Linux 공식 GitLab 문서 저장소를 GitHub로 읽기 전용 미러링하기 위한 자동화 저장소입니다.

- 원본: `https://gitlab.com/kalilinux/documentation/kali-docs`
- 자동화 브랜치: `main`
- 미러 브랜치: `gitlab/<원본 브랜치명>`
- 실행 시각: 매일 00:00, 12:00, 23:00 (Asia/Seoul)

`main` 브랜치는 GitHub Actions 설정만 보관합니다. 원본 GitLab 브랜치는 이름 충돌과 워크플로 삭제를 방지하기 위해 `gitlab/` 접두사 아래에 동기화됩니다. 원본의 `master` 브랜치는 이 저장소의 `gitlab/master`에서 확인할 수 있습니다.

미러 브랜치와 태그는 자동화가 관리하므로 직접 수정하지 마십시오.

## 자동화 저장소

이 저장소는 자동화 저장소이므로 사람의 개입은 불요합니다. 오로지 비교 검증용으로 사용되므로 수정하지 마세요.
