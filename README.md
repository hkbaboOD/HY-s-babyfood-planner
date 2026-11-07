# 이유식 식단·큐브

아이폰 홈 화면에 설치해 쓰는 이유식 식단표·큐브 재고 앱입니다. 앱 화면은 이 저장소에서 GitHub Pages로 배포되고, 기록은 Firebase Firestore(`families/{가족코드}/…`)에 저장됩니다. 이 공개 저장소에는 아기 이름·식단 같은 개인 정보가 들어 있지 않습니다.

- 식단표: 하루 1끼/2끼, 곡류·단백질·채소·과일·알레르기 드롭다운 수정, 먹음 체크 시 큐브 자동 차감
- 큐브 현황: 제작일별 재고, −/+ 로 사용·되돌리기
- 필요수량: 기간별 필요 큐브, 소진 예상일, 만들 차례
- 알레르기: 노출 날짜·횟수, 재료 도입 기록

## 사용
1. 앱 주소 열기 → 새 가족 공간 만들기
2. 설정 → 아기 이름·생년월일, 백업 파일이 있으면 불러오기
3. 설정 → 가족 초대 링크 복사 → 가족에게 전송 (링크를 아는 사람은 기록을 보고 고칠 수 있으니 가족에게만)

## Firestore 보안 규칙
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /families/{family}/{document=**} {
      allow read, write: if family.size() >= 16;
    }
  }
}
```
